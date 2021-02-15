# Установка на ZFS без таблицы разделов

`ZFS` - относительно недавно портированная в `FreeBSD` файловая система, примечательная множеством интересных особенностей. В этой заметке рассмотрим как установить `FreeBSD` на пул `ZFS` и как этот пул сделать загрузочным.

## Создание пула

Создание пула на одном диске

```text
zpool create -R /var zroot da0
```

или зеркала на двух дисках

```text
zpool create -R zroot mirror da0 da1
```

## Настройка загрузки

```text
sysctl kern.geom.debugflags=16
dd if=/boot/zfsboot of=/dev/da0 count=1
dd if=/boot/zfsboot of=/dev/da0 skip=1 seek=1024
zpool set bootfs=zroot zroot
```

В случае, если пул собран как зеркало или `RAID`, аналогичную операцию необходимо произвести с каждым диском для обеспечения загрузки с любого из них.

## Создание раздела swap

```text
zfs create -V 2G -o org.freebsd:swap=on -o checksum=off -o compression=off \
  -o dedup=off -o sync=disabled -o primarycache=none zroot/swap
```

## Разметка пула

Это пример для тестового варианта, тонкая настройка разделов и параметров `zfs` является темой другой заметки.

```text
zfs create zroot/home
zfs create zroot/usr
zfs create zroot/var
zfs create zroot/tmp
```

## Установка системы

```text
cd /usr/freebsd-dist
for file in base docs kernel src; do ( tar -C /var/zroot -xvzf $file.txz ); done
```

## Настройка установленной системы

```text
chroot /var/zroot

echo 'zfs_load="YES"' >> /boot/loader.conf
echo 'hostname="freebsd.local"' >> /etc/rc.conf
echo 'zfs_enable="YES"' >> /etc/rc.conf

touch /etc/fstab

exit
```

## Размонтирование пула

```text
zfs unmount -a
```

## Изменение точки монтирования

```text
zfs set mountpoint=/ zroot
```

Далее проводятся необходимые настройки и установка программного обеспечения.


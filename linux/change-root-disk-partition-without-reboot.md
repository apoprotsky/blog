# Изменение корневого раздела диска без перезагрузки

## Сбор информации

После изменение размера диска, например виртуальной машины, увидеть изменения можно с помощью команды `fdisk -l`:

```bash
Disk /dev/sda: 70 GiB, 75161927680 bytes, 146800640 sectors
Disk model: Virtual disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x5eec38c3

Device     Boot Start       End   Sectors Size Id Type
/dev/sda1  *     2048 113246207 113244160  54G 83 Linux
```

Полный размер диска составляет 70 ГБ, а первый раздел, на котором располагается корень файловой системы, 54 ГБ.

## Изменение таблицы разделов диска

Для изменения таблицы разделов запустим утилиту `fdisk` в режиме редактирования нужного нам диска:

```bash
fdisk /dev/sda
```

Сначала нужно удалить существующий раздел диска командой `d`:

```bash
Command (m for help): d
Selected partition 1
Partition 1 has been deleted.
```

Затем создаем новый раздел, но уже большего размера командой `n`:

```bash
Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1):
First sector (2048-146800639, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-146800639, default 146800639):

Created a new partition 1 of type 'Linux' and of size 70 GiB.
Partition #1 contains a ext4 signature.

Do you want to remove the signature? [Y]es/[N]o: N
```

{% hint style="danger" %}
При создании нового раздела важно указать тип и первый сектор такие же, которые получили в выводе команды `fdisk -l`. А также оставить сигнатуру файловой системы без изменений.
{% endhint %}

Указываем флаг активного раздела при необходимости командой `a`:

```bash
Command (m for help): a
Selected partition 1
The bootable flag on partition 1 is enabled now.
```

Проверяем что получилось командой `p`:

```bash
Command (m for help): p
Disk /dev/sda: 70 GiB, 75161927680 bytes, 146800640 sectors
Disk model: Virtual disk
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x5eec38c3

Device     Boot Start       End   Sectors Size Id Type
/dev/sda1  *     2048 146800639 146798592  70G 83 Linux
```

Затем сохраняем изменения командой `w`:

```bash
Command (m for help): w
The partition table has been altered.
Syncing disks.
```

## Расширение файловой системы

После изменения таблицы разделов диска необходимо расширить файловую систему. Это можно сделать следующей командой `resize2fs /dev/sda1`:

```bash
resize2fs 1.44.5 (15-Dec-2018)
Filesystem at /dev/sda1 is mounted on /; on-line resizing required
old_desc_blocks = 7, new_desc_blocks = 9
The filesystem on /dev/sda1 is now 18349824 (4k) blocks long.
```

Расширение размера корневого раздела на этом завершено

## Ссылки

[https://devops.ionos.com/tutorials/increase-the-size-of-a-linux-root-partition-without-rebooting](https://devops.ionos.com/tutorials/increase-the-size-of-a-linux-root-partition-without-rebooting)  
[https://www.codenotary.com/blog/enlarge-a-disk-and-partition-of-any-linux-vm-without-a-reboot](https://www.codenotary.com/blog/enlarge-a-disk-and-partition-of-any-linux-vm-without-a-reboot/)


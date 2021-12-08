# Полезные заметки

## aio\_submit retries

В логах наблюдаются сообщения подобного вида

> bdev(0x562645298000 /var/lib/ceph/osd/ceph-28/block) aio\_submit retries 14 bdev(0x562645298000 /var/lib/ceph/osd/ceph-28/block) aio\_submit retries 8

Рекомендуют увеличить значение параметра `bdev_aio_max_queue_depth`:

```shell
ceph config set global bdev_aio_max_queue_depth 4096
```

### Ссылки

[https://tracker.ceph.com/issues/19511](https://tracker.ceph.com/issues/19511)

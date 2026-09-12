List all partitions
```bash
lsblk -o KNAME,TYPE,SIZE,MODEL
```

List all block devices
```bash
ls -l /dev /dev/mapper |grep '^b'
```
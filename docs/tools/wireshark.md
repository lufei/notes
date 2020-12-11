# Wireshark

## The capture session could not be initiated on interface 'en0' ((all BPF devices are busy))

```bash
sudo dseditgroup -o edit -a `whoami` -t user access_bpf
sudo "/Library/Application Support/Wireshark/ChmodBPF/ChmodBPF"
```

还是不行就重启后执行
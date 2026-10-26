# iPXE install scripts for the btcstore bare-metal server (Vultr, Debian 13)

- `boot.ipxe`: paste the WHOLE text into Vultr -> Orchestration -> Scripts (type PXE/iPXE), not a URL.
  Set `set raid raid1` or `set raid raid0` at the top before pasting. It loads `preseed-<platform>-<raid>.cfg` from this repo.
- `preseed-efi-raid1.cfg`, `preseed-pcbios-raid1.cfg`: / on RAID 1 (mirrored). Use when the two drives hold the chain data
  with room to grow (e.g. 2 x 1.9 TB, plan vbm-8c-64gb-amd).
- `preseed-efi-raid0.cfg`, `preseed-pcbios-raid0.cfg`: / on RAID 0 (striped). Only when the drives are too small to mirror
  (e.g. 2 x 960 GB, plan vbm-6c-32gb-amd). One failed drive loses the install.
- `preseed-efi.cfg`, `preseed-pcbios.cfg`: the original RAID 0 files, kept unchanged so an older pasted boot.ipxe still works.

The raid1 and raid0 pairs differ only in the `partman-auto-raid/recipe` line for `/` (`1 2 0` vs `0 2 0`) and comments.
/boot is RAID 1 in every variant. Everything else (hostname test-1, root password, SSH key, 8 GB /swapfile) is identical.

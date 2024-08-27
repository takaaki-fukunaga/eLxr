# Install eLxr on KVM

## Evaluation Environment
```
+---------------------------+
| +-----------------------+ |
| | +-------------------+ | |
| | | eLxr              | | |
| | +-------------------+ | |
| | KVM                   | |
| +-----------------------+ |
| Ubuntu Server 20.04.6 LTS |
+---------------------------+
```
## Install eLxr
1. Create directories as below.
   ```
   /home/user/
    |
    +-- cd/   * Save ISO image files
    |
    +-- kvm/  * Save qcow2 files
   ```
1. Download ISO image file and save it on `/home/user/cd`.
   - https://elxr.org/downloads
1. Create a qcow2 file on `/home/user/kvm/elxr12-201`.
   ```sh
   cd /home/user/kvm/elxr12-201
   ```
   ```sh
   qemu-img create -f qcow2 elxr12-201.qcow2 128G
   ```
1. Create `install.sh` file as below.
   ```
   name=elxr12-201
   
   virt-install \
   --name $name \
   --hvm \
   --virt-type kvm \
   --ram 8192 \
   --vcpus 8 \
   --arch x86_64 \
   --os-type linux \
   --disk /home/user/kvm/$name/$name.qcow2 \
   --network bridge=virbr0 \
   --graphics none \
   --serial pty \
   --console pty \
   --location /home/user/cd/elxr-12-amd64-CD-1.iso,kernel=install.amd/vmlinuz,initrd=install.amd/initrd.gz \
   --extra-args "console=ttyS0"   
   ```
1. Run `install.sh` and install eLxr following steps as Debian installation.

## Link
- https://elxr.org/documentation

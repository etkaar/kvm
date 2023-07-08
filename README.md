# KVM
Simple scripts for kernel-based virtual machines (KVM). Written in DASH ([Debian Almquist Shell](https://wiki.archlinux.org/title/Dash)) to offer POSIX compliance.

Tested on Debian 12 Bookworm.

## 1.0 Introduction

The purpose of these scripts is to make the creation and the backup of the virtual machines on your system easier. Thus, this is mainly for your *internal* use.

### 1.1 Features

- Creation
- Backup

---

## 2.0 Installation

You are required to install a few packages first:

```
apt install whois libosinfo-bin dnsmasq-base
apt install qemu-system-x86 virtinst libvirt-daemon-system
apt install libguestfs-tools
```

After that, create the directory `/opt/kvm` and manually download the scripts:

```
mkdir /opt/kvm
cd /opt/kvm
wget https://github.com/etkaar/kvm/archive/refs/heads/main.tar.gz
tar -xzf main.tar.gz --strip-components=1
rm main.tar.gz
```

Then, update permissions:

```
chown 0700 /opt/kvm/create-vm.sh
```

⛔️ Do **not** automatically update these scripts. In case you need to update it, make sure that it won't break your system.

---

## 3.0 Isolated Network

```
touch /etc/libvirt/qemu/networks/isolated.xml

<network>
	<name>isolated</name>
	<uuid>6b45d478-f1c3-4b36-9796-efc95b33d10b</uuid>
	<bridge name='virbr0' stp='on' delay='0'/>
	<mac address='52:54:00:e4:e9:ec'/>
	<ip address='192.168.254.1' netmask='255.255.255.0'>
		<dhcp>
			<range start='192.168.254.2' end='192.168.254.254'/>
		</dhcp>
	</ip>
</network>

```


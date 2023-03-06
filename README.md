# LIBVIRT (QEMU & KVM)

## Installation sous Linux
### Test de compatibilité avec notre CPU
```
kvm-ok
```

### Installation sous Ubuntu
```
sudo apt install -y qemu qemu-kvm libvirt-daemon bridge-utils virt-manager virtinst
```
### Démarrage de Libvirt
```
sudo systemctl start libvirtd
sudo systemctl enable libvirtd --now
```


## Machine Virtuelle 

### Vérification des réseaux  disponibles
```
virsh net-list --all
```
### Activer le réseau par défaut " Default"  s'il existe
```
virsh net-start default
virsh net-autostart default
```
### Créer un réseau
#### Créer un fichier network.xml pour la configuration réseau

```
<network connections='1'>
  <name>reseau1</name>
  <forward mode='nat'>
    <nat>
      <port start='1024' end='65535'/>
    </nat>
  </forward>
  <bridge name='pont1' stp='on' delay='0'/>
  <mac address='52:54:00:0a:cd:22'/>
  <ip address='192.168.0.1' netmask='255.255.255.0'>
    <dhcp>
      <range start='192.168.0.2' end='192.168.0.254'/>
    </dhcp>
  </ip>
</network>
```

#### mettre en place le réseau défini sur le fichier XML
```
virsh netdefine network.xml
```



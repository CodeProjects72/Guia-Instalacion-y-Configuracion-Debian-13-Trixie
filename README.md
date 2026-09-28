# Guía Completa de Instalación y Configuración Debian 13 Trixie

Configuración básica y programas esenciales para una instalación nueva de Linux.

---

## Configuración inicial

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Códecs y herramientas básicas

```bash
sudo apt-get install libavcodec-extra curl nano wget git -y
```

---

## Tipografías

```bash
sudo apt-get install ttf-mscorefonts-installer -y
```

---

## GDebi y Synaptic

```bash
sudo apt-get install gdebi gdebi-core synaptic -y
```

---

## Compresores y descompresores

```bash
sudo apt-get install p7zip-full p7zip-rar rar unrar -y
```

---

## Compiladores

```bash
sudo apt-get install build-essential -y
sudo apt-get install linux-headers-$(uname -r) -y
```

---

## Drivers de impresoras

```bash
sudo apt-get install printer-driver-all -y
```

---

## Programas y paquetes

```bash
sudo apt install cmatrix btop htop fastfetch mousepad evince eog ffmpeg obs-studio kdenlive qbittorrent vlc -y
```

---


# VirtualBox · Instalación y configuración

> Instalación de Oracle VirtualBox en Debian Trixie, incluyendo módulos del kernel, repositorio oficial, configuración del usuario y solución de conflictos con KVM.

---

## Preparar el sistema

Actualiza los repositorios e instala las dependencias necesarias para compilar los módulos de VirtualBox:

```bash
sudo apt update

sudo apt install -y \
    build-essential \
    dkms \
    linux-headers-$(uname -r) \
    linux-headers-amd64 \
    perl \
    wget \
    gnupg \
    ca-certificates \
    apt-transport-https
```

Comprueba que los headers del kernel están disponibles:

```bash
ls -ld /usr/src/linux-headers-$(uname -r)
```

---

## Añadir la clave de Oracle

Crea el directorio para las claves de APT:

```bash
sudo install -d -m 0755 /etc/apt/keyrings
```

Descarga la clave oficial de Oracle:

```bash
wget -O /tmp/oracle_vbox.asc \
    https://www.virtualbox.org/download/oracle_vbox_2016.asc
```

Convierte la clave al formato utilizado por APT:

```bash
sudo gpg --dearmor \
    -o /etc/apt/keyrings/oracle-virtualbox.gpg \
    /tmp/oracle_vbox.asc
```

---

## Añadir el repositorio

Añade el repositorio oficial de VirtualBox para Debian Trixie:

```bash
echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/oracle-virtualbox.gpg] https://download.virtualbox.org/virtualbox/debian trixie contrib" | \
sudo tee /etc/apt/sources.list.d/virtualbox.list
```

Actualiza la información de los repositorios:

```bash
sudo apt update
```

Comprueba la versión disponible:

```bash
apt policy virtualbox-7.2
```

---

## Instalar VirtualBox

Instala VirtualBox:

```bash
sudo apt install -y virtualbox-7.2
```

Comprueba la instalación:

```bash
VBoxManage --version
```

---

## Añadir usuario a VirtualBox

Añade tu usuario al grupo `vboxusers`:

```bash
sudo usermod -aG vboxusers "$USER"
```

Aplica el cambio de grupo sin cerrar la sesión:

```bash
newgrp vboxusers
```

Comprueba los módulos de VirtualBox:

```bash
lsmod | grep vbox
```

---

## Solución de conflictos con KVM

Si VirtualBox presenta problemas relacionados con los módulos KVM, comprueba si están cargados:

```bash
lsmod | grep kvm
```

Si utilizas un procesador AMD:

```bash
sudo modprobe -r kvm_amd
sudo modprobe -r kvm
```

> Si utilizas Intel, el módulo correspondiente normalmente será `kvm_intel`.

---

## Desactivar KVM

Crea un archivo de configuración para los módulos:

```bash
sudo nano /etc/modprobe.d/virtualbox.conf
```

Añade:

```text
blacklist kvm_amd
blacklist kvm
```

Guarda el archivo y actualiza el `initramfs`:

```bash
sudo update-initramfs -u
```

Reinicia el sistema:

```bash
sudo reboot
```

---

## Limpieza final

```bash
sudo apt autoremove -y
sudo apt clean
sudo apt autoclean
```

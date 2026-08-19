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

## Limpiar sistema

```bash
sudo apt autoremove -y
sudo apt clean
sudo apt autoclean
```

---

## Limpieza final

```bash
sudo apt autoremove -y
sudo apt clean
sudo apt autoclean
```

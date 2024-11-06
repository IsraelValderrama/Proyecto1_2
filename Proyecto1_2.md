id: arranque_seguro_debian
title: Guía de Arranque seguro en Debian
description: Codelab de Arranque seguro en Debian.
author: Israel Valderrama García
summary: Codelab de instalación de BIOS/UEFI
categories: codelab, markdown
environments: Web
status: Published

# Configuración del arranque seguro en Debian

## Protegemos GRUB2 con contraseña
![etc/grub/40_custom](img_proyecto1_2/etc_grub.png)
1. Editamos el archivo de configuración personalizada de GRUB:

```bash
sudo nano /etc/grub.d/40_custom
```

2. Agregamos las siguientes líneas al final del archivo:

```bash
set superusers="root"
password root PruebaDebian123!
```
3. Guardamos y cerramos el archivo.

```text
CTRL ^O para guardar.
CTRL ^x para salir.
```
## Ciframos la contraseña.

![etc/grub/40_custom](img_proyecto1_2/etc_grub_hash.png)
1. Generamos una contraseña cifrada:

```bash
sudo grub-mkpasswd-pbkdf2
```
2. Copiamos el hash generado y editamos nuevamente el archivo 40_custom:

```bash
sudo nano /etc/grub.d/40_custom
```
3. Reemplazamos la línea de la contraseña por:
![hash_contraseña](img_proyecto1_2/hash_contrasena.png)

## Ajustamos permisos del archivo de configuración.

![privilegios](img_proyecto1_2/privilegios.png)

```bash
sudo chmod 700 /etc/grub.d/40_custom
```
## Ocultamos el menú de GRUB.

1. Editamos el archivo de configuración de GRUB:

![etc/default/grub](img_proyecto1_2/etc_default_grub.png)

```bash
sudo nano /etc/default/grub
```

2. Cambiamos la línea 'GRUB_TIMEOUT=5' por:

```text
    GRUB_TIMEOUT=0
```
3. Guardamos y cerramos el archivo.

```text
CTRL ^O para guardar.
CTRL ^x para salir.
```

## Actualizamos la configuración de GRUB.

Después de que hayamos realizado los cambios en la terminal debemos de poner este comando:
```bash
sudo update-grub
```

## Reininciamos la máquina y ponemos las credenciales.

![imagen_arranque](img_proyecto1_2/arranque.png)
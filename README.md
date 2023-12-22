_TODO - Readme con detalles..._

Loc-OS 23 KDE, una distribución de GNU/Linux que ofrece como base a Loc-OS 23, creada por Nicolás Longardi, en la que se le ha añadido el escritorio KDE Plasma 5.27 y realizado una serie de optimizaciones. La distribución, en las pruebas realizadas, logra arrancar con 371MiB en PCs de 32bit y 526MiB en PCs de 64bit (con UEFI).

Inicialmente, en la versión de noviembre de 2023 cree la versión con KDE Plasma utilizando como base la ISO de Loc-OS 23 XFCE (build de noviembre).

Ahora, en la siguiente build, de diciembre de 2023, he utilizado la iso de Debian 12 NetInstaller y la he convertido en un Loc-OS 23 al cuál le he instalado KDE Plasma con lo mínimo y le he realizado modificaciones de configuración, tanto en las Preferencias del Sistema como a nivel interno en los ficheros del sistema.

La ISO utiliza Calamares como instalador y cualquiera puede instalarla normalmente y crear su usuario, y sí, las configuraciones que modifiqué se aplicarán al nuevo usuario. Lás imágenes a continuación muestran el uso de RAM después de haber instalado la ISO.

## Especificaciones
### Requisitos mínimos [^1]
|Requisito|versión x86_64| versión i686|
|---|---:|---:|
|CPU|amd64 @1,0GHz|Pentium 4/i386 @1,00GHz|
|Memoria RAM|1 GiB|512 MiB|
|Espacio en Disco|10 GiB|10 GiB|
|Gráfica|vga|vga|

[^1]: Las especificaciones pueden variar y son aproximadas.

### Estadísticas de interés
|Especificación|versión x86_64| versión i686|
|---|---:|---:|
|Ram de inicio|483MiB~|358MiB~|
|Tamaño de la ISO|1.9GiB|1.9GiB|


## Build
Puedes construir tu popia ISO instalable con Calamares de Loc-OS 23 KDE realizando los siguientes pasos:

1. Descarga la *ISO NetInstaller* de Debian 12 Bookworm en https://www.debian.org/CD/netinst/
2. Instala el sistema con los siguientes parámetros para root:
    - contraseña root: root
3. Instala el sistema con los siguientes parámetros para el usuario:
    - usuario: live
    - contraseña: live
4. En un terminal ejecuta como root: [^2]
    ```bash
    cd /root
    wget -O script-base.sh https://staging.karlaperezyt.com/locoskde/src/script-base_64b.sh.txt
    chmod +x script-base.sh
    ./script-base.sh
    ```
    [^2]: Si tu sistema es de 32bits, en script a descargar con `wget` es `script-base_32b.sh.txt`en lugar de `script-base_64b.sh.txt`
5. Se reiniciará el sistema. Ahora ejecuta otra vez en un terminal como root: [^3]
    ```bash
    ./script-desktop.sh
    ./script-dependency.sh
    ./script-customs.sh
    ```
    [^3]: Cada vez que ejecutes un script, se reiniciará el sistema.
6. Haz las modoficaciones que quieras sobre la instalación.
7. Para construir la ISO en un terminal ejecuta como root:
    ```bash
    refractasnapshot
    ```
    1. Se mostrará un menú enumerado. Presiona `1` para iniciar el proceso.
    2. Se mostrará el espacio libre en disco. Si está todo bien, presiona `q` para continuar.
    3. El script te preguntará el nombre de la ISO, pon el que quieras o `Loc-OS 23 KDE`
8. La ISO se guardará en `/home/snapshot/` en formato ISO juntamente con un sha.

## Descargas

Última versión de las ISOs: **Loc-OS 23 KDE build 23.12.2**

**Release ISO 32bit (i686):**

- Web personal: https://staging.karlaperezyt.com/locoskde/iso/23m12/Loc-OS-23-KDE-i686.iso
- Sourceforge: https://sourceforge.net/projects/loc-os/files/Loc-OS%2023/Loc-OS-23-KDE-i686.iso/download

**Release ISO 64bit (x86_64):**

- Web personal: https://staging.karlaperezyt.com/locoskde/iso/23m12/Loc-OS-23-KDE-x86_64.iso
- Sourceforge: https://sourceforge.net/projects/loc-os/files/Loc-OS%2023/Loc-OS-23-KDE-x86_64.iso/download

## Imágenes
### Loc-OS Linux 23 KDE en 32bit
![Loc-OS Linux 23 KDE en 32bit](https://raw.githubusercontent.com/KarlaPM101/Loc-OS_Linux_KDE/master/pub/locos_23_kde_32bit.png)

### Loc-OS Linux 23 KDE en 64bit
![Loc-OS Linux 23 KDE en 32bit](https://raw.githubusercontent.com/KarlaPM101/Loc-OS_Linux_KDE/master/pub/locos_23_kde_64bit.png)

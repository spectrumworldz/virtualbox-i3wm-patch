# virtualbox-i3wm-patch

## Bugs

## Patching on Arch Llinux
  1. Remove the installed version
  
  ``` bash
    sudo pacman -Rns virtualbox
  ```
  1. Download the source code: https://www.virtualbox.org/wiki/Downloads
  
  1. Extract it
  
  ``` bash
    tar -xvf VirtualBox-*.tar.bz2
  ```
  1. Apply the patch
  
  ``` bash
    cd VirtualBox-*
    wget PATCH_RAW_URL
    patch -p1 < virtualbox-5.1.16-i3wm.patch
  ```

## Building on Arch Linux

  1. Intall the required packages (64 bit system)
  
  ``` bash
    sudo pacman -S --needed binutils bison flex pkg-config multilib-devel wget yasm nasm \
                   libidl2 linux-headers texlive-most sdl sdl_ttf \
                   lib32-glibc lib32-libstdc++5 lib32-gcc-libs gcc-multilib qt5 \
                   iasl cdrkit jd8-openjdk texlive-fontsextra
    
    yaourt makeself
  ```
  1. Set java home directory
  
  ``` bash
    export VBOX_JAVA_HOME=/usr/lib/jvm/java-8-openjdk/
  ```
  1. Configure and build the source
  
  ``` bash
    ./configure
    source env.sh
    kmk all
    kmk packing
  ```
  1. Intall Virtualbox using the generated package
  
  ``` bash
    out/linux.amd64/release/bin/VirtualBox-*.run
    
    #uninstall
    out/linux.amd64/release/bin/VirtualBox-*.run uninstall
  ```
  1. Compile and install the kernel modules
  
  ``` bash
    cd ./out/linux.amd64/release/bin/src
    make
    sudo make install
  ```

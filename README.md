# Configuración para BSPWM en Arch/Arcolinux

Leer toda la guía primero, antes de comenzar.

## 1.- Preparar el ambiente

Para ir preparando el sistema, en la carpeta de usuario clonan el repo:

```
	git clone https://github.com/emersondivB0/Bspwm-deb-config.git
```

Se ubican en la carpeta:

```
	cd Bspwm-deb-config
```


## 1.- Instalar los paquetes necesarios

* *[Bspwm](https://wiki.archlinux.org/title/Bspwm_(Español)#:~:text=bspwm%20es%20un%20gestor%20de,controla%20a%20través%20de%20mensajes.)*: el windows manager
	
```
	sudo pacman -Sy bspwm
```

* *[Sxhkd](https://wiki.archlinux.org/title/Sxhkd_(Español))*: el mapeo de teclas par los atajos de teclado

```
	sudo pacman -S sxhkd
```


* *[Polybar](https://polybar.github.io)*: la barra superior

```
	sudo pacman -S polybar
```

* *[zsh](https://www.zsh.org)*: shell interactiva y brutal (amo bash también)

```
	sudo pacman -S zsh
```

* *[Rofi](https://github.com/davatorium/rofi)*: aplicación para buscar y lanzar aplicaciones, cambiar ventanas y otras cosas (para resumir bastante)

```
	sudo pacman -S rofi
```

* *[Feh](https://wiki.archlinux.org/title/Feh_(Español))*: gestor de imágenes, administrador de fondos de escritorio para wallpapers estáticos

```
	sudo pacman -S feh
```


* *[Variety](https://github.com/varietywalls/variety)*: gestor de fondos de escritorio dinámicos, muy configurable para que el fondo cambie cada *x* tiempo, ya sea desde sitios online o deste las carpetas que escojas.

```
	sudo pacman -S variety
```


* *[Conky](https://github.com/brndnmtthws/conky)*: monitor de sitema para *X*. Me obsesiona saber los recursos del sistema, por eso siempre lo pongo

```
	sudo pacman -S conky
```

* *[Picom](https://github.com/yshui/picom)*: compositor brutal par *X11* -> transparencias.

Este es entretenido de instalar, requiere dependencias específicas

```
	sudo pacman -S meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-composite0-dev libxcb-image0-dev libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev libpcre2-dev libevdev-dev uthash-dev libev-dev libx11-xcb-dev libxcb-glx0-dev libpcre3 libpcre3-dev
```
```
	git clone https://github.com/ibhagwan/picom.git
```
```
	cd picom
```
```
	git submodule update --init --recursive
```
```
	meson --buildtype=release . build
```
```
	ninja -C build
```
```
	sudo ninja -C build install
```


#### Software que neecsitan y tal vez no esté instalado:

1. **Git**: Sistema de control de versiones para rastrear cambios en archivos y colaborar en proyectos de desarrollo de software.

2. **Neovim / Vim**: Editores de texto potentes y altamente configurables utilizados para programación y edición de texto en la línea de comandos. Uso Neovim.

3. **XCB**: Biblioteca de conexión X (X protocol C-language Binding) utilizada para interactuar con el servidor X Window System en sistemas Unix.

4. **CMake**: Herramienta de generación de proyectos que simplifica la construcción de software y permite compilar programas en varios sistemas y entornos de compilación.

5. **Scrot**: Utilidad de captura de pantalla en línea de comandos para tomar y guardar capturas de pantalla en sistemas Unix/Linux.




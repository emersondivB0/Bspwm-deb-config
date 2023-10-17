# Configuración para BSPWM en Arch/Arcolinux

Leer toda la guía primero, antes de comenzar.

## 0.- Preparar el ambiente

Para ir preparando el sistema, en la carpeta de usuario clonan el repo:

```
	git clone https://github.com/emersondivB0/Bspwm-deb-config.git
```

Se ubican en la carpeta:

```
	cd Bspwm-deb-config
```


## 1.- Instalar los paquetes necesarios

#### Software que necesitan y tal vez no esté instalado:

1. **Git**: Sistema de control de versiones para rastrear cambios en archivos y colaborar en proyectos de desarrollo de software.

2. **Neovim / Vim**: Editores de texto potentes y altamente configurables utilizados para programación y edición de texto en la línea de comandos. Uso Neovim.

3. **XCB**: Biblioteca de conexión X (X protocol C-language Binding) utilizada para interactuar con el servidor X Window System en sistemas Unix.

4. **CMake**: Herramienta de generación de proyectos que simplifica la construcción de software y permite compilar programas en varios sistemas y entornos de compilación.

5. **Scrot**: Utilidad de captura de pantalla en línea de comandos para tomar y guardar capturas de pantalla en sistemas Unix/Linux.

**Ahora si los principales del repositorio:**

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

* *[Powerlevel10k](https://github.com/romkatv/powerlevel10k)*: tema de terminal, junto con zsh se puede hacer una terminal mucho más amigable y amistosa.

```
	git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.powerlevel10k
```
```
	echo 'source ~/.powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```
También se instala para usuario root:

```
	sudo git clone --depth=1 https://github.com/romkatv/powerlevel10k.git /root/.powerlevel10k
```

* *[lsd](https://github.com/lsd-rs/lsd)*: es un ls más futurista

```
	sudo pacman -S lsd
```

* *[kitty](https://sw.kovidgoyal.net/kitty/)*: esta terminal aceptó todas las configuraciones sin problemas, URxvt era la que usaba siempre, pero sólo un software no mostró bien y por eso cambié.

```
	sudo pacman -S kitty
```



## 2.- Configuraciones

Importante, revisen la carpeta Config del repo y la .config de su usuario, antes de sobreescribir la configuración, guárdenla en un backup, por si acaso. Si no existe config previa, no hay problema entonces. Eso también aplica a .zshrc

 Copiamos la config y el tema Nord de Rofi (el tema es opcional) para cambiar de tema en rofi puse el atajo de teclado *super + F11*:

```
	cp rofi/config.rasi ~/.config/rofi/
```

```
	mkdir -p ~/.config/rofi/themes
```
```
	cp rofi/nord.rasi ~/.config/rofi/themes/
```

Instalar las fuentes, primero verifiquen dónde están, puede ser en /usrlocal/share, en /usr/share, incluso en usuario ~/.local/share

```
	sudo cp -v fonts/Nerd/* ~/.local/share
```

 Instalamos las Fuentes de Polybar


```
	sudo cp -v Config/polybar/fonts/* /usr/share/fonts/truetype/
```

Configuraciones para kitty:

```
	sudo cp -rv kitty /opt/
```
```
	sudo cp -rv Config/kitty /root/.config/
```

El resto de archivos de configuración los pueden sólo copiar y pegar, aunque recomiendo ir uno por uno, queda de su parte:

```
	cp -rv Config/* ~/.config/
```

Las configuraciones de terminal y zsh:

```
	rm -rf ~/.zshrc
```
```
	cp -v .zshrc ~/.zshrc
```
```
	cp -v .p10k.zsh ~/.p10k.zsh
```
```
	sudo cp -v .p10k.zsh-root /root/.p10k.zsh
```

Plugins zsh:


```
	sudo pacman -S zsh-syntax-highlighting zsh-autosuggestions zsh-autocomplete
```
```
	sudo mkdir /usr/share/zsh-sudo
```
```
	cd /usr/share/zsh-sudo
```
```
	sudo wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/plugins/sudo/
```
```
	sudo.plugin.zsh
```


 Cambiando de SHELL a zsh


```
	chsh -s /usr/bin/zsh
```
```
	sudo usermod --shell /usr/bin/zsh root
```
```
	sudo ln -s -fv ~/.zshrc /root/.zshrc
```


 Asignamos Permisos a los Scritps esta parte es opcional, sólo si da algún problema

```
chmod +x ~/.config/bspwm/bspwmrc
```
```
chmod +x ~/.config/bspwm/scripts/bspwm_resize
```
```
chmod +x ~/.config/polybar/launch.sh
```
```
sudo chmod +x /usr/local/bin/screenshot
```


 Configuramos el Tema de Rofi

```
	rofi-theme-selector
```


## 3.- Datos extra

En este punto con reiniciar la máquina, escoger bspwm como sesión en la ventana de login, ya debería funcionar todo. Pero, cada sistema y cada hardware son distintos. Cualquier cosa preguntan y vemos qué se puede hacer.

Mientras, revisen todo, poco a poco, para mí han sido meses aprendiendo, aún luego de usar linux por años. Mucho de aquí es Frankenstein de otras configuraciones, mías, de Arcolinux, de otra gente. Al final, es adaptarlo a tu conveniencia.

Como tips extra, la mayoría de las configuraciones están en .config dentro de la carpeta de usuario. Si observan bien, encontrarán 2 carpetas de sxhkd, una está dentro de la carpeta bspwm, eso es porque puse el launcher para bspwm del Arcolinux, me pareció mejor, más ordenado.

Dentro de ~/.config/bspwm/sxhkd está el archivo de configuración de todos los atajos de teclado, la tecla super el la tecla 'windows'. Puse varias personales, las pueden cambiar. La terminal es *super + t* por ejemplo, revisen esa config y pongan o quiten aplicaciones de acuerdo a lo que usen o tengan instalado.

Puse un launcher de rofi que seguro les guste, es con *super + d*

Para reiniciar las configuraciones de Bspwm es con: *super + shift + r*
Para reiniciar las configuraciones de Sxhkd es con: *super + shift + s*
Para reiniciar las configuraciones de terminal es con:
```
	source ~/.zshrc
```


Si les gusta ser más minnimalistas,  o quieren impresionar a la mamá pareciendo hackers, instalen 'dmenu', es un launcher de aplicaciones, lo abrirían con *super + shift + d* es una barrita superior, donde teclean la aplicación y luego enter.

Hay software y configs que no puse ahí, pero recomiendo y uso.

* *[vtop](https://es.linux-console.net/?p=401)* es un monitor de recursos en terminal, más bonito que htop, no mejor, cada uno sirve a su propósito. Entren al enlace, yo uso el tema brew. En la config que pasé, es el tema que se usa por defecto.

* *[Neovim](https://neovim.io)*: el mejor editor para mi gusto, migré definitivamente hace poco, se tarda en aprender, pero vale la pena, sobre todo cuando lo tuneas.

Ok, en ~/.config/bspwm/bspwmrc está la config básica del WM, lo primero que verán es la geometría y espaciado, 

+ window_gap: espacio entre ventanas
+ top_padding: espacio superio de las ventanas, para darle espacio a la polybar
+ bottom_pading: espacio inferios, etc

También encontrarán reglas para algunas aplicaciones como las que se abren fullscreen por defecto, o las que se abren en un workspace específico, pueden hacer lo que quieran ahí.

Ahí tambien está el autostat.sh el archivo que arranca todo el WM, si da error o algo le dan permisos de ejecución
```
	chmod +x ~/.config/bspwm/autostart.sh
```

Ahí cargan todas las aplicaciones y configuraciones del escritorio, verán líneas como esta:
```
feh --bg-fill /usr/share/backgrounds/archlinux/arch-wallpaper.jpg &
```
Esto establece el fondo de escritorio con feh, la ruta la pueden cambiar, aunque yo no uso feh.

Verán esta:
```
run variety &
```
es el que uso para los fondos, revisenla, y configuren a gusto.

Puse Conky para que siempre esté presente:  
```
killall conky
conky -c $HOME/.config/bspwm/system-overview &
```
 Pueden desmarcar cualquiera o agregar para abrir aplicaciones apenas enciendan el equipo: 
 
```
run firefox &
```

### ZSH

Esta parte es importante.

~/.zshrc es la configuración principal de la terminal, tienen para días de diversión revisándola y modificándola.

una parte importante son los alias, son caminos cortos a comandos que usen seguido, quité los míos y dejé los más básicos, por ejemplo, hay uno:
```
alias vtop='vtop --theme brew'
```
este alias hace que al ejecutar *vtop* en terminal, se abra con el tema brew por defecto, pueden cambiarlo al tema que sea o eliminarlo y dejar vtop por defecto.

Un alias que uso, es este:
```
alias upate='sudo pacman -Syyu'
```
así para actualizar el sistema, sólo debo escribir update y listo. Los invito a jugar con los alias.

### Polybar

Recuerden reiniciar bspwm para cargar los cambios que hagan.

Esta es otra bien extensa, pero tal vez la más entretenida. La barra superior, la configuración está en ~/.config/polybar, El lanzador de la barra (que también debería tene permiso de ejecucuón) es launch.sh

En esta configuración, son varios páneles, y cada panel se le puede agregar módulos.

yo puse los workspaces en el centro y la config está en ~/.config/polybar/workspace.ini

Partes importantes de la configuración: 

width = 20% ancho total que va a tener esta sección
height = 25 alto total de esta sección
radius-top = 10.0   radio superor de las esquinas
radius-bottom = 10.0   radio inferior de las esquinas

[bar/primary]: es el panel que  tiene todos los workspaces, el ofset-y es para cuadrar si lo quieren separado de la parte superior de la pantalla. El offset-x es dónde quieren que comience la barra, en términos de posición horizontal.

modules-center: es la propiedad que indica qué módulos quieres ver en el panel, en este caso los workspaces, pero puedes poner los que quieras, siempre que de el espacio.

[modules/workspaces]: es el elementoq ue se mostrará en el panel central, en este caso, aquí verán los íconos de cada workspace, pueden poner los que quieran mientras los acepte la barra, los que están los busqué yo.

En ~/.config/polybar/colors.ini está el mapeo de colores, definidos con variables, por ejemplo:

bg = #99435060 indica un color en hexadecimal, los primeros 2 dígitos son el nivel de transparencia, lo puse en 99 = 60%, pueden cambiarlo como quieran, los otros 6 dígitos son el color como tal, hay bastante para jugar.

Los invito a revisar los otros páneles y módulos por su cuenta, quiten y pongan los que quieran.

PAZ!

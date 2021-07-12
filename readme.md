# Ubuntu Setup

Aplicaciones y configuraciones iniciales para un equipo con Ubuntu 20.04 LTS.

### Tabla de contenidos

- [Actualización del sistema](#actualizacion-del-sistema)
- [Navegador: Mozilla Firefox](#navegador-mozilla-firefox)
- [Shell: ZSH](#shell-zsh)
- [Control de versiones: GIT](#control-de-versiones-git)
- [Ohmyzsh](#ohmyzsh)
- [Powerlevel 10K](#powerlevel10k)
- [Multiplexor: Tmux](#multiplexor-tmux)
- [Diseño de Tmux: Drácula](#diseno-de-tmux-dracula)
- [Editor de código: Visual Studio Code](#editor-de-codigo-visual-studio-code)
- [Administrador de ambientes: Docker](#administrador-de-ambientes-docker)

## Actualización del sistema

```
sudo apt-get update && sudo apt-get upgrade
```

## Navegador: Mozilla Firefox

Instalo navegador e instalo plugin [Firefox Multi-Account Containers](https://addons.mozilla.org/es/firefox/addon/multi-account-containers/). Este plugin permite usar varias sesiones de las mismas páginas web dado que almacena las cookies en containers. Por ejemplo permite abrir varios usuarios de Github en la misma ventana de Firefox.

## Shell: ZSH

[Documentación oficial](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)


```
sudo apt install zsh
```

Convertir en shell por defecto:

```
chsh -s $(which zsh)
```

Reiniciar equipo. O finalizar e iniciar sesión de usuario en Linux.

Probar que se aplicó el cambio con:
```
echo $SHELL
```

## Control de versiones: GIT

```
sudo apt install git-all
```

## Ohmyzsh

Instalo con wget que viene nativo en Ubuntu.

```
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
### Plugin
Agrego el plugin de sugerencias de completado de instrucciones de git:

 [Documentación](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Edito el archivo `~/.zshrc` e incluyo el nombre del plugin:

```
plugins=(
    git
    zsh-autosuggestions
```

## Powerlevel 10K

Herramienta que permite personalizar el diseño de la terminal.

Instalo las fuentes de letras según se indican en la [documentación](https://github.com/romkatv/powerlevel10k/blob/master/README.md#meslo-nerd-font-patched-for-powerlevel10k).

Clono el repositorio:
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
Edito en el archivo `~/.zshrc` lo siguiente:
```
ZSH_THEME="powerlevel10k/powerlevel10k"
```

## Multiplexor: Tmux

```
sudo apt install tmux
```

## Diseño de Tmux: Drácula
```
tmux new
```

Instalo tpm que es un manager de plugins:
```
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

Creo y edito un `~/.tmux.conf` insertando lo siguiente:

```
# List of plugins
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'tmux-plugins/tmux-sensible'

# Other examples:
# set -g @plugin 'github_username/plugin_name'
# set -g @plugin 'git@github.com:user/plugin'
# set -g @plugin 'git@bitbucket.com:user/plugin'

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```

Reinicio el ambiente de tmux:
```
# type this in terminal if tmux is already running
tmux source ~/.tmux.conf
```

Ahora que el plugin funciona, instalo Drácula agregando lo siguiente al archivo `~/.tmux.conf`:

```
set -g @plugin 'dracula/tmux'

# Set 256 colors
set -s default-terminal 'tmux-256color'
```

Para instalarlo presionar: `ctrl+b+I`

Más [información](https://dev.to/andrenbrandao/terminal-setup-with-zsh-tmux-dracula-theme-48lm).

## Editor de código: Visual Studio Code

[Instalación DIRECTA](https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64)

## Administrador de ambientes: Docker

[Instalación](https://docs.docker.com/engine/install/ubuntu/)

[Post-instalación](https://docs.docker.com/engine/install/linux-postinstall/)

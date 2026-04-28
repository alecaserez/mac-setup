# new_macos

Setup de una Mac nueva. Ejecutar en orden.

## Índice

1. [🍺 Homebrew](#1--homebrew)
2. [👻 Ghostty](#2--ghostty)
3. [🐚 Oh My Zsh](#3--oh-my-zsh)
4. [🛠️ CLI tools](#4--cli-tools)
5. [🐍 Lenguajes y runtimes](#5--lenguajes-y-runtimes)
6. [🤖 Claude Code](#6--claude-code)
7. [📦 Apps](#7--apps)
8. [📋 Comandos útiles de brew](#8--comandos-útiles-de-brew)

---

## 1. 🍺 Homebrew

Gestor de paquetes para macOS. Base del resto del setup.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

Verificar con `brew doctor`. Si pide Xcode Command Line Tools: `xcode-select --install`.

---

## 2. 👻 Ghostty

Terminal moderno, rápido y configurable. Reemplaza a Terminal.app.

```bash
brew install --cask ghostty
```

Abrir desde Spotlight (`⌘ + Space` → `ghostty`) y dejarlo como terminal por defecto.

### Configuración

Suprime el mensaje "Last login..." al abrir la terminal.

```bash
touch ~/.hushlogin
```

Escribe `~/.config/ghostty/config` con tema oscuro, tamaño de fuente y padding de ventana.

```bash
mkdir -p ~/.config/ghostty
cat > ~/.config/ghostty/config <<'EOF'
background = 1c1c1c
foreground = f8f8f2
cursor-color = ffffff
font-size = 13
window-padding-x = 12
window-padding-y = 8
EOF
```

---

## 3. 🐚 Oh My Zsh

Framework para `zsh`: temas, plugins, mejor prompt. Va antes de los CLI tools porque sobrescribe `~/.zshrc`.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/install.sh)"
```

Cerrar y volver a abrir la terminal. Tema en `~/.zshrc`:

```bash
ZSH_THEME="robbyrussell"
```

---

## 4. 🛠️ CLI tools

Versión de `git` más nueva que la de Xcode CLT.

```bash
brew install git
```

CLI oficial de GitHub.

```bash
brew install gh
```

Gestor rápido de Python y paquetes.

```bash
brew install uv
```

Crea túneles SSH de forma simple.

```bash
brew install mole
```

---

## 5. 🐍 Lenguajes y runtimes

### Python (vía uv)

Instala Python 3.14 y deja `python` apuntando a esa versión.

```bash
uv python update-shell
uv python install 3.14
echo 'alias python="python3.14"' >> ~/.zshrc
source ~/.zshrc
```

### Node (vía nvm)

Instala el gestor y crea el directorio donde guarda las versiones de Node.

```bash
brew install nvm
mkdir -p ~/.nvm
```

`nvm` instalado por brew necesita que `nvm.sh` se cargue en cada shell.

```bash
cat >> ~/.zshrc <<'EOF'

export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && . "/opt/homebrew/opt/nvm/nvm.sh"
EOF
source ~/.zshrc
```

Instala y activa la última versión LTS.

```bash
nvm install --lts
nvm use --lts
```

---

## 6. 🤖 Claude Code

CLI oficial de Anthropic para programar con Claude desde la terminal. Requiere Node (paso 5).

```bash
npm install -g @anthropic-ai/claude-code
```

Verificar con `claude --version`. La primera ejecución pide autenticación.

---

## 7. 📦 Apps

Navegador.

```bash
brew install --cask google-chrome
```

Smooth scroll para mouse externo.

```bash
brew install --cask mos@beta
```

Editor de código rápido y colaborativo.

```bash
brew install --cask zed
```

Corre varios agentes de Claude en paralelo.

```bash
brew install --cask conductor
```

---

## 8. 📋 Comandos útiles de brew

Actualizar el listado de fórmulas y los paquetes instalados.

```bash
brew update
brew upgrade
```

Actualizar una app o herramienta específica.

```bash
brew upgrade <nombre>
```

Eliminar una herramienta CLI.

```bash
brew uninstall <nombre>
```

Ver lo instalado.

```bash
brew list
```

Buscar un paquete antes de instalarlo.

```bash
brew search <nombre>
```

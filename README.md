🌐 **Read this in other languages:** [English](README.en.md)

# 🚀 Curso de Claude Code — Bitácora y Proyectos

¡Bienvenido/a a este repositorio! Aquí recopilo notas, aprendizajes, ejercicios y proyectos desarrollados a lo largo del curso de **Claude Code** (el asistente de terminal de Anthropic para desarrollo asistido por IA).

---

## 📁 Estructura del Repositorio

A medida que avancemos en el curso, iremos organizando los ejercicios prácticos y proyectos en subcarpetas temáticas:

```text
repo/
├── README.md             # Documentación principal en español
├── README.en.md          # Documentación en inglés
└── projects/             # Subcarpetas con los proyectos del curso
    ├── 01-getting-started/
    ├── 02-automations/
    └── ...
```

---

## 🛠️ Requisitos y Configuración del Entorno en WSL

Para trabajar cómodamente con Claude Code en un entorno Linux (WSL), configuraremos las siguientes herramientas:

### 1. Node.js

Claude Code requiere un entorno de ejecución Node.js (versión 18 o superior). Se recomienda instalarlo utilizando `nvm` (Node Version Manager):

```bash
# 1. Instalar nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash

# 2. Recargar configuración de la terminal
source ~/.bashrc

# 3. Instalar y usar la versión LTS de Node.js
nvm install --lts
nvm use --lts

# 4. Verificar instalación
node -v
npm -v
```

---

### 2. Claude Code

Claude Code es la CLI oficial de Anthropic para interactuar con modelos Claude directamente en tu flujo de trabajo de desarrollo:

```bash
# 1. Instalar Claude Code globalmente mediante npm
npm install -g @anthropic-ai/claude-code

# 2. Iniciar Claude Code y seguir las instrucciones de autenticación
claude
```

> **Nota:** La primera vez que ejecutes `claude`, te guiará para iniciar sesión con tu cuenta de Anthropic Console o autenticarte con tu clave de API (`ANTHROPIC_API_KEY`).

---

### 3. Warp Terminal

[Warp](https://www.warp.dev/) es una terminal moderna acelerada por GPU con funciones avanzadas de autocompletado, historial y soporte de IA.

#### Opciones de uso con WSL:
- **Warp en Windows:** Instala Warp en Windows y abre una pestaña o sesión directa hacia tu distribución WSL.
- **Warp para Linux:** Si cuentas con soporte de entorno gráfico en Linux/WSL, puedes instalar el paquete `.deb`:

```bash
# Descargar e instalar el paquete .deb para distribuciones basadas en Debian/Ubuntu
sudo apt update && sudo apt install -y wget
wget -O warp-terminal.deb https://releases.warp.dev/stable/v0.2024.02.20.08.02.stable_02/warp-terminal_0.2024.02.20.08.02.stable.02_amd64.deb
sudo apt install ./warp-terminal.deb
rm warp-terminal.deb
```

---

### 4. Git y Conexión mediante SSH

Configuración de Git y autenticación segura con GitHub/GitLab a través de llaves SSH:

#### Paso 1: Configurar identidad de Git
```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu-email@ejemplo.com"
```

#### Paso 2: Generar un par de llaves SSH (algoritmo Ed25519)
```bash
ssh-keygen -t ed25519 -C "tu-email@ejemplo.com"
```
*(Presiona `Enter` para aceptar la ruta predeterminada `~/.ssh/id_ed25519` y define una frase de paso opcional).*

#### Paso 3: Iniciar el agente SSH y añadir tu llave privada
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

#### Paso 4: Copiar la llave pública
```bash
cat ~/.ssh/id_ed25519.pub
```
Copia todo el contenido de la salida.

#### Paso 5: Registrar la llave en GitHub
1. Ve a **GitHub > Settings > SSH and GPG keys**.
2. Haz clic en **New SSH key**.
3. Asigna un título descriptivo (por ejemplo: `WSL-Ubuntu`) y pega la llave pública.
4. Haz clic en **Add SSH key**.

#### Paso 6: Probar la conexión
```bash
ssh -T git@github.com
```
Deberías recibir un mensaje similar a:
`Hi <usuario>! You've successfully authenticated, but GitHub does not provide shell access.`

---

## ⚙️ Configuraciones Personales

En esta sección se documentan configuraciones personalizadas, extensiones, skills y ajustes del flujo de trabajo con Claude Code.

### 1. Caveman Skill

**Caveman** es un skill / modo para asistentes y Claude Code que fuerza respuestas concisas, directas al grano y sin rodeos innecesarios (estilo "lenguaje de cavernícola" o ultra-resumido), ideal para ahorrar tokens y acelerar las respuestas.

#### Métodos de instalación / configuración:

##### Opción A: A través de Claude Code Skills / Plugins
Si estás usando el sistema de plugins/skills de Claude Code:
```bash
# Dentro de la sesión de Claude Code o vía CLI
/plugin install caveman
# o instalar desde el repositorio de la skill
/skill add https://github.com/anthropics/claude-plugins-official/tree/main/plugins/caveman
```

##### Opción B: Instrucciones globales (`~/.claude/CLAUDE.md` o `CLAUDE.md` del proyecto)
Puedes añadir la instrucción directa a tu archivo de reglas de Claude (`CLAUDE.md`) para activar el comportamiento de Caveman:

```markdown
# Personal Instructions - Caveman Mode
When answering technical questions, be extremely concise. Skip greetings, disclaimers, and unnecessary pleasantries. Give code first, explain only what is critical.
```

##### Opción C: Comando personalizado / Slash command
Puedes configurar un prompt rápido o comando `/caveman` para alternar este modo cuando necesites máxima síntesis y menor consumo de tokens.

---

## 📌 Próximos Pasos

- [ ] Completar configuración del entorno en WSL.
- [ ] Explorar los primeros comandos y capacidades de Claude Code.
- [ ] Añadir proyectos y módulos prácticos en subcarpetas.

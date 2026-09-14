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

### 5. Ollama

[Ollama](https://ollama.com/) permite ejecutar modelos de lenguaje de forma local. En la página oficial de descargas ([Download Ollama on Linux](https://ollama.com/download/linux)), selecciona la pestaña correspondiente a tu sistema (macOS, Linux o Windows); como estamos trabajando dentro de **WSL**, seleccionamos la versión de **Linux**.

#### Instalación en WSL (Linux)
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

> **Nota (Solución de red en WSL):** Si al descargar modelos obtienes un error como `network is unreachable` por IPv6, desactiva IPv6 temporalmente con:
> ```bash
> sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
> ```

#### Descarga de Modelos Locales Recomendados
```bash
ollama pull glm-4.7-flash
ollama pull qwen3.5
```

#### Ejecutar Claude Code con un Modelo Local de Ollama
Para iniciar Claude Code utilizando directamente un modelo local ejecutado en Ollama:
```bash
ollama launch claude --model qwen3.5
```

---

## ⚙️ Configuraciones Personales

En esta sección se documentan configuraciones personalizadas, extensiones, skills y ajustes del flujo de trabajo con Claude Code.

### 1. Caveman Skill

**Caveman** es un skill para Claude Code y asistentes de IA diseñado para forzar respuestas ultra-concisas, directas al grano y sin rodeos innecesarios. Esto ayuda a reducir drásticamente el consumo de tokens y acelerar el tiempo de respuesta.

#### Instalación

Puedes instalar la skill directamente usando `npx`:

```bash
npx skills add JuliusBrussee/caveman
```

#### Uso

Una vez instalada, Claude responderá de manera concisa y orientada a código/solución rápida. También puedes invocarla o configurarla según las opciones de la skill.

---

## �️ Comandos Útiles

Comandos y herramientas esenciales para gestionar tus sesiones y flujos de trabajo en Claude Code:

### 1. `/rewind` (Rebobinar / Revertir Estado)

El comando `/rewind` te permite **retroceder en el tiempo** dentro de tu sesión activa de Claude Code.

```text
/rewind
```

#### ¿Para qué sirve y cómo funciona?
- **Deshacer cambios de código:** Revierte los cambios de archivos y ediciones realizadas por Claude en pasos anteriores de la conversación.
- **Restaurar el contexto de la conversación:** Elimina los últimos turnos o mensajes que hayan desviado al asistente o consumido contexto innecesario, permitiéndote retomar la tarea desde un punto previo más limpio.
- **Selector interactivo:** Al ejecutar `/rewind`, Claude Code muestra un historial de acciones/mensajes recientes para que elijas exactamente hasta qué punto deseas rebobinar.

---
### 2. `/tasks` (Gestión de Tareas y Procesos en Segundo Plano)

El comando `/tasks` permite ver, gestionar y monitorear tareas activas, ejecuciones de comandos en segundo plano y procesos concurrentes.

```text
/tasks
```

#### ¿Para qué sirve y cómo funciona?
- **Monitoreo de tareas en background:** Visualiza los procesos en ejecución que Claude o el usuario hayan iniciado en segundo plano (servidores de desarrollo, compiladores, watchers, tests largos).
- **Control de ejecución:** Permite consultar el estado, ver logs de salida o cancelar/detener tareas que ya no sean necesarias.
- **Seguimiento estructurado:** Ayuda a mantener visibilidad de las operaciones asíncronas sin bloquear la sesión interactiva principal.

---
### 3. `/init` (Inicializar Configuración del Proyecto)

El comando `/init` analiza el espacio de trabajo actual y genera automáticamente el archivo de configuración y contexto `CLAUDE.md`.

```text
/init
```

#### ¿Para qué sirve y cómo funciona?
- **Análisis del proyecto:** Escanea la arquitectura del código, dependencias, frameworks, linters y scripts de construcción del repositorio.
- **Creación de `CLAUDE.md`:** Genera una guía con las convenciones del proyecto, comandos frecuentes (build, test, run) y reglas de arquitectura para que Claude entienda el contexto de inmediato.
- **Estandarización del equipo:** Sirve como punto de partida para que cualquier miembro del equipo o sesión de Claude comparta las mismas instrucciones y mejores prácticas.

---
## �📌 Próximos Pasos

- [ ] Completar configuración del entorno en WSL.
- [ ] Explorar los primeros comandos y capacidades de Claude Code.
- [ ] Añadir proyectos y módulos prácticos en subcarpetas.

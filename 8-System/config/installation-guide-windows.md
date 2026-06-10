---
type: system-doc
version: 1.0.0
created: 2026-06-10
os: windows
---

# WasakaAI — Guía de Instalación en Windows

## Paso 0 — Antes de empezar

Asegúrate de tener:
- Windows 10/11 actualizado
- Al menos 20GB libres en disco
- Conexión a internet (solo para descargar, luego todo es local)
- Cuenta de GitHub (para clonar el vault)

---

## Paso 1 — Git

```powershell
# Descargar Git para Windows
# https://git-scm.com/download/win

# Verificar
git --version

# Configurar (usa TUS datos)
git config --global user.name "wasakabeofficial"
git config --global user.email "wasakabeofficial@gmail.com"
```

---

## Paso 2 — Obsidian

```powershell
# Descargar Obsidian
# https://obsidian.md/download

# Instalar normally

# Abrir Obsidian → "Open folder as vault"
# Seleccionar la carpeta donde clonaste WasakaAI
```

---

## Paso 3 — Clonar WasakaAI

```powershell
# Crear carpeta de trabajo
mkdir C:\Users\TU_USUARIO\WasakaAI
cd C:\Users\TU_USUARIO\WasakaAI

# Clonar el repo
git clone https://github.com/wasakabeofficial/WasakaAI.git .
```

**Alternativa con SSH** (si configuraste llave SSH):
```powershell
git clone git@github.com:wasakabeofficial/WasakaAI.git .
```

---

## Paso 4 — Ollama (LLM Local)

```powershell
# Descargar Ollama para Windows
# https://ollama.com/download

# Instalar y verificar
ollama --version

# Descargar modelos
ollama pull llama3.2:3b          # Razonamiento general
ollama pull phi3:mini            # Alternativa ligera
ollama pull nomic-embed-text     # Embeddings (ESNCIAL para bsqueda)

# Verificar que corre
ollama run llama3.2:3b
# Escribir: "Hola, responde en espaol"
# Debe responder. Escribir: /bye para salir
```

**Nota para Intel Iris Xe**: Los modelos corren en CPU. Con 32GB RAM, modelos hasta 7B funcionan bien. El primer arranque es lento, luego es más rápido.

---

## Paso 5 — Python + ChromaDB

```powershell
# Descargar Python 3.12+
# https://www.python.org/downloads/
# IMPORTANTE: Marcar "Add to PATH" al instalar

# Verificar
python --version

# Instalar ChromaDB
pip install chromadb

# Instalar herramientas adicionales
pip install openai-whisper   # Transcripción de voz
pip install pymupdf          # Lectura de PDFs
pip install python-frontmatter  # Parsing de YAML en notas
```

---

## Paso 6 — Obsidian Plugins

Abrir Obsidian → Settings → Community Plugins:

### Esenciales (instalar en este orden)

1. **Smart Connections**
   - Buscar "Smart Connections" → Install → Enable
   - Settings → Embeddings Provider: "Ollama"
   - Settings → Ollama URL: `http://localhost:11434`
   - Settings → Embedding Model: `nomic-embed-text`
   
2. **Copilot**
   - Buscar "Copilot" → Install → Enable
   - Settings → Model Provider: "Ollama"
   - Settings → Ollama URL: `http://localhost:11434`
   - Settings → Default Model: `llama3.2:3b`

3. **Templater**
   - Buscar "Templater" → Install → Enable
   - Settings → Template folder path: `7-Templates`

4. **Calendar**
   - Buscar "Calendar" → Install → Enable
   - Settings → New note location: `5-Daily`
   - Settings → Format: `YYYY-MM-DD`

5. **Dataview**
   - Buscar "Dataview" → Install → Enable

6. **Obsidian Web Clipper**
   - Instalar la extensión de navegador desde obsidian.md
   - Configurar para guardar en `0-Inbox`

### Opcionales pero recomendados

7. **Excalidraw** — Diagramas
8. **Kanban** — Tableros de proyectos
9. **Tag Wrangler** — Gestión de tags
10. **Linter** — Formato consistente

---

## Paso 7 — OpenCode Go

```powershell
# Descargar OpenCode Go
# https://github.com/opencode-ai/opencode

# Instalar
# Seguir instrucciones oficiales

# Configurar el agente JARVIS para que lea WasakaAI
# Apuntar el system prompt al INDEX del vault
```

---

## Paso 8 — Verificación

```powershell
# Verificar que todo funciona
ollama list                              # Debe mostrar los 3 modelos
python -c "import chromadb; print('OK')" # Debe decir OK
obsidian                                 # Debe abrir el vault

# En Obsidian:
# 1. Verificar que Smart Connections indexa las notas
# 2. Verificar que Copilot responde
# 3. Crear una nota de prueba en 0-Inbox
# 4. Abrir el graph view — debe mostrar conexiones
```

---

## Estructura Final en Windows

```
C:\Users\TU_USUARIO\
├── WasakaAI\                    ← Vault (clonado de GitHub)
├── .ollama\                     ← Modelos Ollama
├── .opencode\                   ← Config OpenCode
└── AppData\Local\chromadb\      ← Base vectorial
```

---

## Sincronización

```powershell
# Antes de cada sesión:
cd C:\Users\TU_USUARIO\WasakaAI
git pull

# Al terminar cambios:
git add -A
git commit -m "update: descripción del cambio"
git push
```

## Backup

El vault se sincroniza con GitHub (privado). Para backup adicional:
- Copia local en disco externo
- Git push regular asegura versión en la nube
- ChromaDB se regenera desde las notas

---

## Troubleshooting

| Problema | Solución |
|----------|----------|
| Ollama no arranca | `ollama serve` en terminal separada |
| Modelos lentos | Usar `llama3.2:1b` o `phi3:mini` en vez de 3B |
| Smart Connections no indexa | Verificar Ollama esté corriendo y URL correcta |
| Copilot no conecta | Verificar `http://localhost:11434` accesible |
| Git push rechazado | `git pull --rebase && git push` |
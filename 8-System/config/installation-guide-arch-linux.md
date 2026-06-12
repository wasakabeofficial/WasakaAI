---
type: system-doc
version: 2.0.0
created: 2026-06-10
updated: 2026-06-11
os: arch-linux
---

# WasakaAI — Guía de Instalación en Arch Linux

## Estado actual del sistema

| Componente | Estado | Versión |
|-----------|--------|---------|
| OS | ✅ Arch Linux | KDE Plasma 6 + Wayland |
| Git | ✅ Instalado | 2.54.0 |
| Python | ✅ Instalado | 3.14.5 |
| Node.js | ✅ Instalado | 26.2.0 |
| Obsidian | ✅ Instalado | 1.12.7 (Flatpak) |
| WasakaAI repo | ✅ Clonado | `~/WasakaAI/` |
| Ollama | ❌ Pendiente | — |
| ChromaDB | ❌ Pendiente | — |
| Plugins Obsidian | ❌ Pendiente | — |

---

## Paso 1 — Ollama (LLM Local)

```bash
# Instalar Ollama
sudo pacman -S ollama

# O iniciar el servicio si ya está en AUR:
# paru -S ollama   (o yay -S ollama)

# Iniciar el daemon
ollama serve &

# Descargar modelos
ollama pull llama3.2:3b          # Razonamiento general (~2GB)
ollama pull phi3:mini            # Alternativa ligera (~2.3GB)
ollama pull nomic-embed-text     # Embeddings (~274MB, ESENCIAL)

# Verificar
ollama list
ollama run llama3.2:3b
# Escribir: "Hola, responde en español"
# Debe responder. Escribir: /bye para salir
```

**Nota para Intel Iris Xe**: Los modelos corren en CPU. Con 32GB RAM, modelos hasta 7B funcionan bien. El primer arranque es lento, luego es más rápido.

---

## Paso 2 — ChromaDB

```bash
# Instalar vía pip
pip install chromadb

# Herramientas adicionales
pip install pymupdf              # Lectura de PDFs
pip install python-frontmatter   # Parsing de YAML en notas

# Verificar
python -c "import chromadb; print('ChromaDB OK')"
```

**Opcional — Transcripción de voz:**
```bash
pip install openai-whisper       # Transcripción local
```

---

## Paso 3 — WasakaAI Vault en Obsidian

```bash
# El vault ya está clonado en ~/WasakaAI/
ls ~/WasakaAI/

# Abrir Obsidian
# 1. Settings → Vault → Open folder as vault
# 2. Seleccionar ~/WasakaAI/
# 3. Confiamos en el autor del plugin (nosotros mismos, es nuestro vault)
```

---

## Paso 4 — Obsidian Plugins

Abrir Obsidian → Settings → Community Plugins → **Turn on community plugins** → Browse

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
   - Instalar extensión de navegador desde obsidian.md
   - Configurar para guardar en `0-Inbox`

### Opcionales pero recomendados

7. **Excalidraw** — Diagramas
8. **Kanban** — Tableros de proyectos
9. **Tag Wrangler** — Gestión de tags
10. **Linter** — Formato consistente

---

## Paso 5 — Verificación

```bash
# Verificar Ollama
ollama list
# Debe mostrar: llama3.2:3b, phi3:mini, nomic-embed-text

# Verificar ChromaDB
python -c "import chromadb; print('OK')"

# Verificar vault
ls ~/WasakaAI/6-Maps/MOC-Home.md
```

En Obsidian:
1. Verificar que Smart Connections indexa las notas
2. Verificar que Copilot responde
3. Crear una nota de prueba en `0-Inbox`
4. Abrir graph view — debe mostrar conexiones

---

## Estructura en Arch Linux

```
/home/wasakabe/
├── WasakaAI/                    ← Vault (clonado de GitHub)
├── .ollama/                     ← Modelos Ollama
├── .local/share/opencode/       ← OpenCode Go
└── .local/share/chromadb/       ← Base vectorial (auto)
```

---

## Sincronización

```bash
# Antes de cada sesión:
cd ~/WasakaAI && git pull

# Al terminar cambios:
cd ~/WasakaAI && git add -A && git commit -m "update: descripción" && git push
```

---

## Troubleshooting

| Problema | Solución |
|----------|----------|
| Ollama no arranca | `systemctl --user start ollama` o `ollama serve &` |
| Modelos lentos | Usar `llama3.2:1b` o `phi3:mini` en vez de 3B |
| Smart Connections no indexa | Verificar que `ollama serve` esté corriendo y URL `http://localhost:11434` |
| Copilot no conecta | Verificar `http://localhost:11434` accesible en navegador |
| Git push rechazado | `git pull --rebase && git push` |
| Flatpak Obsidian no accede a ~/WasakaAI | `flatpak override --filesystem=home md.obsidian.Obsidian` |
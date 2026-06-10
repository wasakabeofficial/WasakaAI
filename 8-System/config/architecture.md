---
type: system-doc
version: 1.0.0
created: 2026-06-10
---

# WasakaAI — Arquitectura Detallada

## Flujo de Información

```
                        ┌─────────────────────┐
                        │    CAPTURA            │
                        │  ┌─────┐ ┌─────────┐  │
      Chat ───────────► │  │Inbox│ │WebClip  │  │
      Voz ─────────────► │  └──┬──┘ └────┬────┘  │
      Código ──────────► │     │         │       │
      Docs/PDFs ───────► │     ▼         ▼       │
      Screenshots ─────► │  ┌────────────────┐  │
                        │  │  PROCESAR      │  │
                        │  │  (manual/JARVIS)│  │
                        │  └───────┬────────┘  │
                        │          │            │
                        │          ▼            │
                        │  ┌────────────────┐  │
                        │  │  ESTRUCTURA     │  │
                        │  │  PARA+          │  │
                        │  └───────┬────────┘  │
                        │          │            │
                        │          ▼            │
                        │  ┌────────────────┐  │
                        │  │  INTELIGENCIA   │  │
                        │  │  Ollama+Chroma  │  │
                        │  └───────┬────────┘  │
                        │          │            │
                        │          ▼            │
                        │  ┌────────────────┐  │
                        │  │  INSIGHTS       │  │
                        │  │  Conexiones     │  │
                        │  │  Recuperación    │  │
                        │  │  Generación      │  │
                        │  └────────────────┘  │
                        └─────────────────────┘
```

## Componentes Detallados

### 1. Ollama (LLM Local)

**Instalación en Windows**:
```powershell
# Descargar de https://ollama.com/download
# Instalar y verificar
ollama --version

# Modelos necesarios
ollama pull llama3.2:3b          # Razonamiento general (3B params, ~2GB RAM)
ollama pull phi3:mini            # Alternativa ligera (3.8B, ~2.3GB RAM)
ollama pull nomic-embed-text     # Embeddings (274MB, esencial para búsqueda)
```

**Configuración para Intel Iris Xe**:
- Modelos ≤7B parámetros únicamente
- CPU inference (la GPU Intel no tiene soporte completo para Ollama)
- `OLLAMA_NUM_PARALLEL=1` en variables de entorno
- Con 32GB RAM, modelos de 7B corren sin problemas

### 2. ChromaDB (Base Vectorial)

```powershell
pip install chromadb
```

Almacena embeddings de todas las notas para búsqueda semántica:
- Cada nota se convierte en vectores via nomic-embed-text
- Búsquedas por significado, no por palabra clave
- Persistente en disco (sobrevive reinicios)

### 3. Obsidian Plugins

**Esenciales**:
1. **Smart Connections** — Encuentra notas semánticamente similares
   - Configurar con Ollama local (no OpenAI)
   - Modelo: `nomic-embed-text`
   
2. **Copilot** — Asistente IA dentro de Obsidian
   - Configurar con Ollama local
   - Modelo: `llama3.2:3b`
   
3. **Templater** — Templates dinámicos
   
4. **Calendar** — Vista de notas diarias

5. **Dataview** — Queries dinámicas sobre el vault

6. **Web Clipper** — Guardar artículos web directamente

**Opcionales pero recomendados**:
7. **Excalidraw** — Diagramas visuales
8. **Kanban** — Tableros para proyectos
9. **Tag Wrangler** — Gestión de tags
10. **Linter** — Formato consistente

### 4. Whisper (Transcripción de Voz)

```powershell
pip install openai-whisper
# O usar la versión de Python para transcripción local
# Modelo "base" (~140MB) para Intel Iris Xe
```

Permite grabar notas de voz y convertirlas a texto automáticamente.

### 5. Scripts de Automatización

Ubicación: `8-System/automations/`

Scripts Python para:
- `sync-embeddings.py` — Sincronizar vault con ChromaDB
- `capture-web.py` — Web clipping automatizado
- `daily-note-creator.py` — Crear nota diaria automáticamente
- `ask-jarvis.py` — Interfaz CLI con JARVIS para consultar el vault

## Interacción JARVIS ↔ WasakaAI

JARVIS (OpenCode Go) es el agente principal que:

1. **Lee** el vault al inicio de cada sesión (INDEX → MOCs → contexto relevante)
2. **Pregunta** antes de registrar cualquier cosa
3. **Escribe** notas nuevas solo cuando tú confirmas
4. **Conecta** notas entre sí propuesta, no impuesta
5. **Busca** en el vault para responder preguntas contextuales
6. **Genera** resúmenes, conexiones e insights basados en TU conocimiento

### Flujo de sesión JARVIS

```
1. Leer INDEX.md y MOC-Home.md
2. Cargar contexto relevante según tema
3. Conversar normalmente
4. Al detectar información valiosa:
   → "¿Registro esto en WasakaAI?"
5. Si sí → crear nota con template apropiado
6. Si la nota conecta con otra:
   → "¿Conecto esto con [[X]]?"
7. Al final de sesión:
   → "¿Resumo esta sesión en tu nota diaria?"
```
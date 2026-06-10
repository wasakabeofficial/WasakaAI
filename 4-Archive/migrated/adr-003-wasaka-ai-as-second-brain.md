---
type: decision
status: active
created: 2026-06-10
tags: [system, second-brain, architecture, wasaka-ai]
related: ["[[WasakaAI]]", "[[Alan de Jesus Martinez]]"]
---

# ADR-003: WasakaAI como Segundo Cerebro

## Contexto

Se necesitaba un sistema de conocimiento personal potenciado por IA que funcionara como "otro Alan" — sin límites, sin restricciones, 100% local.

## Decisión

- Nombre: **WasakaAI**
- Estructura: PARA+ expandida (9 carpetas + Atlas)
- Privacidad: 100% local, sin APIs externas para almacenar conocimiento
- Stack: Obsidian + Ollama + ChromaDB + OpenCode Go (JARVIS)
- Protocolo: Siempre preguntar antes de registrar/modificar/crear
- Hardware: Intel i5-1135G7, 32GB RAM, Intel Iris Xe GT2
- Migración: JARVIS knowledge base absorbida completamente

## Razón

- Obsidian es multiplataforma y gratuito
- Ollama corre modelos locales en CPU con 32GB RAM
- ChromaDB permite búsqueda semántica local
- OpenCode Go es el agente que razona con el vault
- Sin restricciones = Alan decide qué entra
- Sin excepciones al protocolo de preguntar = confianza

## Consecuencias

- JARVIS como sistema separado deja de existir → se transforma en el agente de WasakaAI
- Todo el conocimiento previo se migra a la nueva estructura
- El vault se sincroniza via Git + GitHub (privado)
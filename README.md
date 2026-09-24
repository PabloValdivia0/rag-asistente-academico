# rag-asistente-academico
Asistente académico con RAG para EP1 ISY0101

---------------------------------------------------------------------------------

# RAG Asistente Académico - EP1 ISY0101

Sistema RAG (Retrieval-Augmented Generation) para consultar reglamentos y normativas académicas de una institución de educación superior.

## 🎯 Caso de uso

Los estudiantes y docentes pierden tiempo buscando información dispersa en reglamentos, mallas y protocolos. Este asistente responde preguntas en lenguaje natural y cita la fuente exacta.

## 🏗️ Arquitectura

1. Ingesta de documentos (TXT/PDF)
2. Chunking con `RecursiveCharacterTextSplitter`
3. Embeddings con `gemini-embedding-001`
4. Vector store con FAISS
5. Retriever semántico (top-k=4)
6. Prompt anclado (grounding)
7. Generación con `gemini-3.6-flash`
8. Evaluación con LLM-as-a-Judge

Ver diagrama completo en `docs/diagrama_arquitectura.png`.

## 🚀 Cómo ejecutar

### Requisitos
- Python 3.10+
- Cuenta de Google AI Studio (API Key de Gemini)

### Instalación

\`\`\`bash
git clone https://github.com/PabloValdivia0/rag-asistente-academico.git
cd rag-asistente-academico
pip install -r requirements.txt
\`\`\`

### Configuración

Crea un archivo `.env` con:

\`\`\`
GOOGLE_API_KEY=tu_api_key_aqui
\`\`\`

### Ejecución

Abre el notebook en Google Colab:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/PabloValdivia0/rag-asistente-academico/blob/main/notebooks/rag_asistente_academico.ipynb)

O ejecuta los scripts en `/src`.

## 📊 Resultados

| Métrica | Valor |
|---------|-------|
| Chunks generados | 5 |
| Vectores almacenados | 5 |
| Latencia promedio | ~3 s |
| Fidelidad promedio | 0.9 |

## 🛠️ Tecnologías

- LangChain
- Google Gemini (chat + embeddings)
- FAISS
- Pydantic

## 📝 Declaración de uso de IA

Este proyecto utilizó IA (Gemini y ChatGPT) como apoyo para:
- Redacción y estructura del código
- Búsqueda de referencias técnicas

Las conclusiones, justificaciones y reflexión personal fueron redactadas sin apoyo de IA.

## 📚 Referencias

- LangChain. (2024). *LangChain Documentation*. https://python.langchain.com/
- Google. (2025). *Gemini API Documentation*. https://ai.google.dev/gemini-api/docs
- Duoc UC. (2024). *Reglamento Académico*. https://www.duoc.cl/

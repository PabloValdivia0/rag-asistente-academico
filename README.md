# rag-asistente-academico
Asistente académico con RAG para EP1 ISY0101

---------------------------------------------------------------------------------

# RAG Asistente Académico - EP1 ISY0101

Sistema RAG (Retrieval-Augmented Generation) para consultar reglamentos y normativas académicas de una institución de educación superior.

## 🎯 Caso de uso

Los estudiantes y docentes pierden tiempo buscando información dispersa en reglamentos, mallas y protocolos. Este asistente responde preguntas en lenguaje natural y cita la fuente exacta.

## 🏗️ Arquitectura

1. Ingesta de documentos (PDF/TXT)
2. Chunking con `RecursiveCharacterTextSplitter`
3. Embeddings con `gemini-embedding-001`
4. Vector store con FAISS
5. Retriever semántico (top-k=4)
6. Prompt anclado (grounding)
7. Generación con `gemini-3.6-flash`
8. Evaluación con LLM-as-a-Judge

## 🚀 Cómo ejecutar

### Requisitos
- Python 3.10+
- Cuenta de Google AI Studio (API Key de Gemini)

### Instalación

```bash
git clone https://github.com/TU_USUARIO/rag-asistente-academico.git
cd rag-asistente-academico
pip install -r requirements.txt

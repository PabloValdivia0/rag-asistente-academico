# Proyecto Integrador: RAG y Agente Autónomo para Gestión Académica (ISY0101)

## Integrante
* [Pablo Valdivia]

## 📌 Descripción General
Este repositorio contiene el desarrollo completo para las Evaluaciones Parciales 1 y 2 de la asignatura *Ingeniería de Soluciones con IA*.
*   **EP1:** Construcción de un sistema RAG (Retrieval-Augmented Generation) para consultar normativas académicas.
*   **EP2:** Evolución hacia un **Agente Funcional Autónomo** que integra el RAG anterior como una herramienta de consulta, sumando herramientas de razonamiento y escritura, junto con sistemas de memoria y planificación.

## 🏗️ Arquitectura y Orquestación (IE2, IE8, IE9)
*   **Framework Elegido:** **LangChain** (utilizando `create_tool_calling_agent`). Se seleccionó por su alta escalabilidad y capacidad para integrar herramientas modulares mediante el decorador `@tool`, garantizando compatibilidad técnica.
*   **Modelo LLM:** Google Gemini (`gemini-3.8-flash`).
*   **Integración entre módulos (Decisiones de Diseño):**
    1.  *Consulta:* El agente se conecta a la base de datos vectorial FAISS (creada en la EP1) para extraer información real de los documentos.
    2.  *Razonamiento:* Una función lógica evalúa las notas del alumno contra los prerrequisitos.
    3.  *Escritura:* Una herramienta que permite al agente redactar correos formales de solicitud.

**Diagrama de Orquestación:**
*(Nota para el estudiante: Genera el diagrama en Draw.io con el código Mermaid proporcionado, descárgalo como imagen, súbelo a la carpeta `docs/` de tu GitHub y reemplaza esta línea con la imagen. Ejemplo: `![Diagrama](docs/diagrama_ep2.png)`)*

## 🧠 Sistema de Memoria y Recuperación de Contexto (IE3, IE4)
Para asegurar la continuidad en tareas prolongadas, el agente implementa dos capas de memoria:
1.  **Memoria a Corto Plazo:** Utiliza `ConversationBufferMemory` para mantener el hilo de la conversación actual (ej. recordar el contexto de la última pregunta del alumno).
2.  **Memoria a Largo Plazo:** Utiliza un archivo de persistencia (`memoria_largo_plazo.txt` en Google Drive). El agente lee las interacciones pasadas al iniciar y guarda un resumen al finalizar, permitiendo retomar el contexto en futuras sesiones.

## ⚙️ Planificación y Toma de Decisiones (IE5, IE7)
El agente opera bajo un Prompt de Orquestación estructurado (patrón Plan-and-Execute / ReAct):
1.  **Análisis:** Evalúa la consulta del usuario.
2.  **Planificación:** Si el usuario pide inscribir un ramo, el agente planifica consultar primero el reglamento y luego validar las notas.
3.  **Decisión Adaptativa:** Si la herramienta de razonamiento arroja "RECHAZADO", el agente **cambia su comportamiento** dinámicamente y utiliza la herramienta de escritura para generar una solicitud de excepción, en lugar de simplemente negar la respuesta.

## 🔄 Ejemplos de Flujos de Trabajo (IE6)
*(Nota para el estudiante: En tu informe y aquí en el README, debes incluir capturas de pantalla del `verbose=True` de Colab donde se vea el razonamiento paso a paso. Puedes resumirlo así):*

**Flujo 1: Consulta al RAG Oficial**
*   **Input:** "¿Cuál es el requisito de asistencia?"
*   **Thought:** El agente decide usar la herramienta de consulta RAG.
*   **Action:** Invoca `buscar_reglamento_educativo`.
*   **Output:** Respuesta exacta basada en el Artículo 1 del documento.

**Flujo 2: Toma de Decisión y Escritura**
*   **Input:** "Quiero inscribir Base de Datos II, pero no he aprobado Base de Datos I."
*   **Thought:** El agente decide validar prerrequisitos.
*   **Action:** Usa `validar_prerrequisito`.
*   **Observation:** Retorna "RECHAZADO".
*   **Decisión:** El agente cambia su plan y usa `redactar_correo`.
*   **Output:** Entrega el borrador del correo para pedir la excepción.

## 🚀 Instrucciones para Ejecutar el Sistema
El proyecto está diseñado para ejecutarse íntegramente en **Google Colab**.

### Requisitos
- Cuenta de Google (para Colab y Google AI Studio).
- API Key de Gemini.

### Configuración y Ejecución
1. Abrir el archivo `notebooks/EP2_Agente_Autonomo.ipynb` en Google Colab.
2. En la barra lateral izquierda de Colab (ícono de llave 🔑), agregar un nuevo secreto llamado `GOOGLE_API_KEY` con tu clave de API.
3. Ejecutar la **Celda 1** para instalar las dependencias necesarias.
4. Ejecutar la **Celda 2** (solicitará permiso para montar tu Google Drive para cargar el índice FAISS de la EP1).
5. Ejecutar las **Celdas 3 y 4** para definir las herramientas, la memoria y crear el agente.
6. Ejecutar la **Celda 5** para correr las pruebas automatizadas y visualizar la demostración de autonomía y toma de decisiones.

## 🛠️ Tecnologías Utilizadas
- **Lenguaje:** Python 3.10+
- **Framework de Agentes:** LangChain
- **Modelo de Lenguaje:** Google Gemini
- **Base de Datos Vectorial:** FAISS
- **Entorno:** Google Colab

## 📝 Declaración de Uso de IA
Este proyecto utilizó herramientas de IA (Gemini y ChatGPT) como apoyo para:
- Estructuración y depuración de código técnico.
- Redacción de la documentación técnica del README.

*Las conclusiones, justificaciones de diseño y reflexiones personales en el informe escrito fueron redactadas sin apoyo de IA.*

## 📚 Referencias (Formato APA)
- LangChain. (2024). *LangChain Documentation*. https://python.langchain.com/
- Google. (2025). *Gemini API Documentation*. https://ai.google.dev/gemini-api/docs
- Duoc UC. (2024). *Reglamento Académico*. https://www.duoc.cl/

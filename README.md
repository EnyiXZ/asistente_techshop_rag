# Asistente Virtual RAG de Atención al Cliente (100% Local)

Este repositorio contiene la implementación de un sistema de **Generación Aumentada por Recuperación (RAG)** diseñado para actuar como el asistente virtual interactivo de soporte y atención al cliente de la tienda online **TechShop**. 

La característica clave de este proyecto es que está diseñado para ejecutarse **100% en local**. Toda la base de conocimiento confidencial de la empresa, el procesamiento de vectores y la inferencia del modelo de lenguaje se ejecutan de manera privada en tu propia máquina, garantizando **privacidad absoluta de los datos**, cero latencias de red externa y ausencia total de costes por APIs de terceros.

## 🧠 Características Principales

* **Inferencia 100% Local:** Integración nativa con **Ollama** para la ejecución local tanto del modelo de embeddings como del LLM de generación.
* **Privacidad de Datos:** La base de conocimiento corporativa (políticas de envíos, devoluciones, garantías y pagos) jamás sale de la infraestructura local.
* **Chunking Semántico por Párrafos:** Algoritmo personalizado de segmentación que corta los documentos respetando las estructuras de los párrafos (`\n\n`), evitando fracturar ideas o frases a la mitad.
* **Mitigación Estricta de Alucinaciones:** El sistema incluye un *System Prompt* avanzado que obliga al LLM a responder **únicamente** con el contexto inyectado por la base de datos vectorial, forzándolo a admitir desconocimiento o a declarar que no posee la información si esta no existe en los documentos.
* **Base Vectorial en Memoria:** Uso de **ChromaDB** en modo local/memoria para una indexación y recuperación de contexto por similitud de manera ultrarrápida.

## 🛠️ Arquitectura del Pipeline RAG

```text
[Documentos Corporativos] ──► [Chunking por Párrafos] ──► [Ollama: bge-m3 (Embeddings)]
                                                                    │
[Respuesta Ingerida + Citas] ◄── [Ollama: gemma4] ◄── [ChromaDB (Query Vectorial)]
```

## 📦 Requisitos y Configuración de Ollama (Local)

Para garantizar la ejecución local, debes tener instalado **Ollama** en tu sistema operativo.

1. **Instalar Ollama:** Descárgalo e instálalo desde su sitio oficial en [ollama.com](https://ollama.com).
2. **Descargar los Modelos del Notebook:**
   El proyecto utiliza un modelo avanzado de lenguaje y un modelo especializado en embeddings multilingües de texto. Asegúrate de tenerlos disponibles ejecutando en tu terminal:

   ```bash
   # Descargar el modelo optimizado de Embeddings Multilingües
   ollama pull bge-m3:latest

   # Descargar el modelo de lenguaje para la generación de respuestas
   ollama pull gemma4:latest
   ```

## 📁 Componentes del Código

El notebook se estructura en secciones modulares listas para producción:

1. **Imports y Verificación:** Carga y validación de las librerías `chromadb`, `ollama` y `numpy`.
2. **Configuración de Parámetros:** Ajuste de constantes críticas del sistema como el tamaño de los fragmentos (`CHUNK_SIZE = 600` caracteres) y el número de documentos a recuperar (`N_CHUNKS_RECUPERADOS = 5`).
3. **Base de Conocimiento (Knowledge Base):** Ingesta estructurada de las 4 políticas comerciales de TechShop (Envíos, Devoluciones, Garantías y Métodos de Pago).
4. **Clase `AsistenteTechShop`:** Módulo principal que encapsula la base de datos vectorial, las llamadas a la API local de Ollama, la lógica de indexación semántica y el bucle de chat interactivo.

## 💻 Instrucciones de Uso

1. **Clonar este repositorio:**
   ```bash
   git clone https://github.com/TU_USUARIO/asistente-rag-local.git
   cd asistente-rag-local
   ```

2. **Instalar dependencias de Python:**
   ```bash
   pip install chromadb ollama numpy
   ```

3. **Ejecutar el Chat Interactivo:**
   Abre el entorno del notebook (`asistente_techshop_rag.ipynb`) y corre las celdas de forma secuencial. La última sección desplegará un bucle interactivo en consola (`while True`) donde podrás chatear en tiempo real con el bot formulando preguntas sobre las políticas de la tienda. Escribe `salir` para terminar la ejecución.

---
*Nota: Asegúrate de tener el servicio de Ollama activo en segundo plano antes de inicializar el cuaderno.*

# Asistente Virtual RAG de Atención al Cliente (100% Local)

Este repositorio contiene la implementación de un sistema de **Generación Aumentada por Recuperación (RAG)** diseñado para actuar como el asistente virtual interactivo de la tienda online ficticia **TechShop**. 

La característica clave de este proyecto es que está diseñado para ejecutarse **100% en local**. Toda la base de conocimiento confidencial de la empresa, el procesamiento de vectores y la inferencia del modelo de lenguaje se ejecutan de manera privada en tu propia máquina, garantizando **privacidad absoluta de los datos**, cero latencias de red externa y ausencia total de costes por APIs de terceros.

## 🧠 Características Principales

* **Inferencia 100% Local:** Integración nativa con **Ollama** para la ejecución local tanto del modelo de embeddings como del LLM de generación.
* **Privacidad de Datos:** La base de conocimiento corporativa (políticas de envíos, devoluciones, garantías y pagos) jamás sale de la infraestructura local.
* **Chunking Semántico por Párrafos:** Algoritmo personalizado de segmentación que corta los documentos respetando las estructuras de los párrafos (`\n\n`), evitando fracturar ideas o frases a la mitad.
* **Mitigación Estricta de Alucinaciones:** El sistema incluye un *System Prompt* avanzado que obliga al LLM a responder **únicamente** con el contexto inyectado por la base de datos vectorial, forzándolo a citar las fuentes oficiales o a declarar que no posee la información si esta no existe en los documentos.
* **Base Vectorial en Memoria:** Uso de **ChromaDB** en modo local/memoria para una indexación y recuperación de alta velocidad.

## 🛠️ Arquitectura del Pipeline RAG

```text
[Documentos Corporativos] ──► [Chunking por Párrafos] ──► [Ollama: bge-m3 (Embeddings)]
                                                                    │
[Respuesta Ingerida + Citas] ◄── [Ollama: gemma4] ◄── [ChromaDB (Query Vectorial)]

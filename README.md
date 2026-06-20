# Portafolio de Inteligencia Artificial, Visión Artificial y Deep Learning

Bienvenido a mi repositorio central de proyectos de Inteligencia Artificial. Este espacio funciona como un contenedor organizado que recopila desarrollos de extremo a extremo (End-to-End) enfocados en tres de las áreas más demandadas del sector tecnológico actual: **Sistemas RAG (Generación Aumentada por Recuperación) 100% locales, Motores de Recomendación basados en Deep Learning y Clasificación de Imágenes Médicas mediante Visión Artificial.**

Cada proyecto está contenido en su respectiva carpeta con su código fuente, configuraciones y datos necesarios para su total reproducibilidad.

---

## 📁 Estructura del Repositorio

```text
├── 📁 01-Asistente-RAG-Local-TechShop/   --> Sistema RAG de atención al cliente con Ollama (100% Local)
│   └── asistente_techshop_rag.ipynb
├── 📁 02-Sistema-Recomendacion-DL/       --> Motor de recomendación híbrido con Embeddings en Keras
│   └── Sistema de Recomendacion con Deep Learning.ipynb
├── 📁 03-Clasificacion-ISIC-CancerPiel/  --> Pipeline de visión artificial y CNN para imágenes médicas
│   └── proyecto-isic-detecci-n-de-c-ncer-de-piel.ipynb
└── README.md                             --> Portada y documentación general del portafolio
```

---

## 🛠️ Proyecto 1: Asistente Virtual RAG de Atención al Cliente (100% Local)

### 📝 Descripción
Implementación de un sistema de **Generación Aumentada por Recuperación (RAG)** diseñado para actuar como el asistente interactivo de soporte y atención al cliente de la tienda online **TechShop**.

La arquitectura está diseñada bajo el principio de **Soberanía y Privacidad Absoluta de Datos**. Todo el pipeline —desde la ingesta y segmentación de documentos corporativos hasta la generación de incrustaciones (embeddings) y la inferencia del modelo de lenguaje— se ejecuta **100% en local**. La información confidencial de la empresa jamás se envía a servidores externos, garantizando coste cero de APIs y privacidad total.

### 🧠 Características Técnicas
* **Segmentación Semántica por Párrafos:** Algoritmo de chunking personalizado que respeta los saltos de línea dobles (`\n\n`), preservando la cohesión de las políticas de la empresa sin fragmentar ideas.
* **Base de Datos Vectorial Nativa:** Integración con **ChromaDB** operando en memoria local para indexación ultrarrápida y recuperación de contexto por similitud de coseno.
* **Mitigación Estricta de Alucinaciones:** Diseño de un *System Prompt* avanzado que restringe las respuestas del LLM únicamente al contexto inyectado por ChromaDB, obligándolo a admitir desconocimiento si la respuesta no se encuentra en las fuentes oficiales.
* **Inferencia Local Exclusiva:** Conexión nativa con la API de **Ollama** para la orquestación de modelos de lenguaje y embeddings en local.

### 📦 Configuración e Instalación de Modelos (Ollama)
Para replicar este proyecto en tu entorno local, es imprescindible disponer de Ollama instalado en el sistema operativo.

1. Descarga e instala el motor desde el sitio oficial de [Ollama](https://ollama.com).
2. Ejecuta los siguientes comandos en tu terminal para descargar los modelos específicos implementados en el notebook:
```bash
# Descargar el modelo optimizado de Embeddings Multilingües
ollama pull bge-m3:latest

# Descargar el modelo de lenguaje para la generación de respuestas
ollama pull gemma4:latest
```

---

## 🧠 Proyecto 2: Sistema de Recomendación Personalizado con Deep Learning

### 📝 Descripción
Desarrollo de un **Motor de Recomendación Inteligente** estructurado bajo un enfoque de aprendizaje supervisado profundo. El modelo procesa más de 5,000 interacciones históricas entre usuarios y productos para predecir probabilísticamente la afinidad de compra, incorporando capacidades avanzadas para resolver el problema clásico del **Inicio en Frío (Cold Start)**.

### ⚙️ Arquitectura del Modelo y Stack
Construido mediante la API funcional de **TensorFlow y Keras**, el modelo procesa entradas híbridas (categóricas dispersas y binarias continuas):
* **Capas de Embedding en Paralelo:** Reducción de dimensionalidad para `USER_ID` (dim: 16), `ITEM_ID` (dim: 16), `CATEGORY` (dim: 8), `STYLE` (dim: 8) y `SEASON` (dim: 4).
* **Fusión Densa:** Concatenación de vectores continuos junto con la feature binaria `IS_TRENDING`.
* **Bloques de Regularización:** Red totalmente conectada (128 -> 64 -> 32 neuronas) con capas intercaladas de **BatchNormalization** y **Dropout** (0.3 y 0.2) para evitar el sobreajuste.
* **Capa de Salida:** Activación sigmoide para computar una probabilidad en el rango $[0, 1]$.

### 📈 Resultados de Rendimiento
* **Manejo del Desbalanceo:** Ajuste fino mediante pesos de clase calculados matemáticamente (`{0: 1.0, 1: 1.71}`) debido al ratio de conversión base del 25.4%.
* **Métricas en Test:** **72.60% de Accuracy** y un **AUC-ROC de 0.6058**, logrando una convergencia óptima en la época 13 gracias a los callbacks de `EarlyStopping` y `ReduceLROnPlateau`.

---

## 📊 Proyecto 3: Detección de Lesiones Cutáneas y Cáncer de Piel (ISIC 2016)

### 📝 Descripción
Solución de **Visión Artificial** enfocada a la salud digital (e-Health). Consiste en un pipeline automatizado de preprocesamiento, análisis exploratorio y preparación de imágenes médicas dermatológicas procedentes del dataset internacional **ISIC 2016 (Task 3)** para la clasificación binaria de melanomas (Benignos vs. Malignos).

### 🛠️ Características del Pipeline
* **Análisis Exploratorio de Imágenes (EDA):** Evaluación del desbalanceo crítico de clases (80.7% benignas frente a 19.2% malignas) y visualización matemática de los canales y dimensiones de las muestras mediante `PIL` y `matplotlib`.
* **Automatización de Sistemas de Archivos:** Limpieza y parseo de dataframes con etiquetas heterogéneas, unificando formatos flotantes a string y distribuyendo de forma automatizada 1,279 imágenes de alta resolución mediante `SHUtil` y `Pathlib`.
* **Estructura de Datos de Alto Rendimiento:** Partición automatizada de los conjuntos de datos en una estructura jerárquica nativa compatible con optimizaciones de carga por lotes (`image_dataset_from_directory` de Keras).
* **Mapeo de Aceleración por Hardware:** Script integrado para la detección, inicialización y reserva de recursos de cómputo basados en GPUs duales mediante el backend de TensorFlow.

---

## 🚀 Requisitos Globales del Entorno

Para ejecutar cualquiera de los cuadernos de este portafolio, se recomienda configurar un entorno virtual de Python 3.10+ e instalar las dependencias requeridas:

```bash
# Clonar el portafolio completo
git clone https://github.com/TU_USUARIO/Portafolio-IA.git
cd Portafolio-IA

# Instalar el conjunto de librerías base
pip install tensorflow chromadb ollama pandas numpy scikit-learn matplotlib seaborn pillow
```

*Nota: Asegúrate de tener el demonio de Ollama corriendo en segundo plano antes de inicializar el cuaderno del Asistente RAG.*

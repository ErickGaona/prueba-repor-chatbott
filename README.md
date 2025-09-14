¡Excelente\! El `README` de tu amigo es muy profesional y está muy bien estructurado. Es la base perfecta.

Vamos a acoplar toda la información de tu proyecto (el trabajo en equipo, las tecnologías que elegimos como Gemini y Tavily, y la evaluación con Ragas) en esa estructura de alto nivel. El resultado será un `README` igual de profesional, pero que represente fielmente **tu proyecto**.

Aquí tienes la versión fusionada y adaptada. Simplemente copia y pega esto en tu archivo `README.md`.

-----
Claro, aquí tienes el código completo en formato Markdown listo para que lo copies y pegues directamente en tu archivo `README.md` en GitHub.

-----

```markdown
# 🤖 Asistente IA para Pólizas de Seguro

Un agente inteligente y multi-herramienta diseñado para optimizar la creación de pólizas, la evaluación de riesgos y la recuperación de información en la industria de seguros.

Repositorio de GitHub: [MichaelYnoa/proyectoFinal_InsuranceChatBot](https://github.com/MichaelYnoa/proyectoFinal_InsuranceChatBot)

## Contenido

- [El Problema](#-el-problema)
- [Nuestra Solución](#-nuestra-solución)
- [Características Principales](#-características-principales)
- [Arquitectura del Sistema](#️-arquitectura-del-sistema)
- [Stack Tecnológico](#-stack-tecnológico)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Cómo Empezar](#-cómo-empezar)
- [Equipo del Proyecto](#-equipo-del-proyecto)

---

## 🎯 El Problema

En la industria de seguros, el proceso de suscripción (evaluar y analizar riesgos para aprobar o rechazar una póliza) es fundamental. Este proceso, junto con la generación de nuevos documentos, suele ser lento, repetitivo y requiere un análisis meticuloso de pólizas existentes y datos de mercado. El esfuerzo manual puede llevar a tiempos de respuesta más lentos para los clientes y a un aumento de los costos operativos.

---

## 💡 Nuestra Solución

Este proyecto introduce un **Chatbot potenciado por IA** que actúa como un asistente y asesor inteligente para las compañías de seguros. Aprovechando Modelos de Lenguaje Grandes (LLMs) y una arquitectura de agente con múltiples herramientas, nuestro chatbot agiliza el ciclo de vida de creación y consulta de pólizas. Puede acceder instantáneamente a una base de datos de pólizas para responder preguntas complejas, buscar en la web las últimas noticias del sector y proporcionar resúmenes concisos para mantener informados a los agentes.

Esta herramienta transforma un proceso tedioso en una experiencia dinámica y conversacional, asegurando que los profesionales de seguros tengan información fiable y precisa al alcance de su mano.

---

## ✨ Características Principales

* **Preguntas y Respuestas Conversacionales**: Realiza preguntas complejas sobre las pólizas de seguro existentes en lenguaje natural.
* **Base de Conocimiento Dinámica (RAG)**: El chatbot utiliza Generación Aumentada por Recuperación (RAG) para extraer información de una base de datos vectorial **ChromaDB** con las pólizas.
* **Búsqueda Web en Tiempo Real**: El agente puede acceder a internet usando **Tavily Search** para encontrar las últimas noticias, regulaciones o información relevante, optimizando los resultados para la IA.
* **Conversaciones con Estado (Memoria)**: El chatbot recuerda las interacciones previas dentro de una sesión para proporcionar respuestas contextuales y coherentes.
* **Evaluación Cuantitativa del Modelo**: Se utiliza la librería **Ragas** para evaluar objetivamente la calidad, precisión y relevancia de las respuestas generadas por el sistema RAG.
* **Arquitectura Desacoplada y Escalable**: La aplicación completa está contenerizada con **Docker**, asegurando un despliegue fácil y una alta escalabilidad.

---

## 🏗️ Arquitectura del Sistema

El proyecto se basa en una arquitectura de dos servicios desacoplados (frontend y backend) orquestados por Docker Compose.

1.  **Frontend (Streamlit)**:
    * Una interfaz de usuario web amigable construida con Streamlit.
    * Gestiona las sesiones de usuario y el historial de la conversación.
    * Se comunica con el backend a través de peticiones HTTP.

2.  **Backend (FastAPI)**:
    * Una API robusta construida con FastAPI que expone los endpoints para la lógica del chatbot.
    * Aloja el **Agente de LangChain**, que es el núcleo del sistema.
    * Gestiona la base de datos vectorial **ChromaDB** para la información de las pólizas.

### Flujo de Datos:

1.  Un usuario envía un mensaje a través de la **UI de Streamlit**.
2.  La UI envía una petición con la pregunta y el historial de chat al endpoint `/ask` en el **Backend de FastAPI**.
3.  El backend dirige la petición al **Agente de LangChain**.
4.  El Agente, potenciado por el modelo **Gemini de Google**, procesa la pregunta y decide qué herramienta usar:
    * **Herramienta de Pólizas**: Busca en la base de datos vectorial **ChromaDB** información relevante sobre las pólizas.
    * **Herramienta de Búsqueda Web**: Usa **Tavily Search** para buscar en internet información en tiempo real.
5.  La herramienta elegida devuelve sus hallazgos al agente.
6.  El agente sintetiza la información y formula una respuesta final.
7.  El backend de FastAPI envía la respuesta a la UI de Streamlit, que la muestra al usuario.

---

## 🛠️ Stack Tecnológico

| Categoría                 | Tecnología / Herramienta                                  |
| :------------------------ | :-------------------------------------------------------- |
| **Framework IA / NLP** | LangChain                                                 |
| **Proveedor de LLM** | Google Gemini API                                         |
| **Base de Datos Vectorial**| ChromaDB                                                  |
| **Backend** | FastAPI                                                   |
| **Frontend** | Streamlit                                                 |
| **Herramienta Búsqueda Web**| Tavily Search                                             |
| **Evaluación de Modelos** | Ragas                                                     |
| **Contenerización** | Docker, Docker Compose                                    |
| **Lenguaje** | Python 3.10                                               |

---

## 📁 Estructura del Proyecto

```

├── api/
│   ├── logic/
│   │   ├── agent.py             \# Lógica del agente, prompts y herramientas.
│   │   ├── config\_model.py      \# Configuración del modelo Gemini.
│   │   ├── config\_vectordb.py   \# Configuración de ChromaDB.
│   │   └── pdf\_processor.py     \# Utilidades para cargar y procesar los PDFs.
│   ├── data/                    \# PDFs de pólizas para construir la base de datos.
│   ├── main.py                  \# Aplicación FastAPI, endpoints y lógica de la API.
│   ├── Dockerfile               \# Dockerfile para el servicio de backend.
│   └── .env                     \# Para almacenar las claves de API.
│
├── ui/
│   ├── main.py                  \# El código de la aplicación frontend de Streamlit.
│   └── Dockerfile               \# Dockerfile para el servicio de frontend.
│
├── notebooks/
│   └── EDA.ipynb                \# Análisis Exploratorio de Datos de las pólizas.
│
├── evaluation/
│   └── ragas\_evaluation.py      \# Scripts para la evaluación del chatbot con Ragas.
│
├── .gitignore
├── docker-compose.yml           \# Orquesta el inicio de todos los servicios.
└── README.md                    \# ¡Estás aquí\!

````

---

## 🚀 Cómo Empezar

Sigue estas instrucciones para ejecutar el proyecto en tu máquina local.

### Prerrequisitos

Debes tener instalado lo siguiente:
* **Docker**
* **Docker Compose** (generalmente incluido con Docker Desktop)

### Instalación y Configuración

1.  **Clona el repositorio:**
    ```bash
    git clone [https://github.com/MichaelYnoa/proyectoFinal_InsuranceChatBot.git](https://github.com/MichaelYnoa/proyectoFinal_InsuranceChatBot.git)
    cd proyectoFinal_InsuranceChatBot/
    ```

2.  **Crea el archivo de entorno:** Crea un archivo llamado `.env` en la carpeta `/api`. Este archivo contendrá tus claves de API.
    ```
    GOOGLE_API_KEY="TU_API_KEY_DE_GEMINI_AQUI"
    TAVILY_API_KEY="TU_API_KEY_DE_TAVILY_AQUI"
    ```
    * Puedes obtener una clave de API de Gemini en [Google AI Studio](https://aistudio.google.com/).
    * Puedes obtener una clave de API de Tavily en [Tavily.com](https://tavily.com/).

3.  **Construye y ejecuta la aplicación:** Toda la aplicación está orquestada por Docker Compose. Simplemente ejecuta el siguiente comando desde el directorio raíz del proyecto:
    ```bash
    docker compose up --build
    ```
    El flag `--build` asegura que las imágenes de Docker se reconstruyan si hay cambios en el código. La primera vez tardará un tiempo en descargar las imágenes base y crear la base de datos vectorial.

4.  **Accede a la aplicación:** Una vez que los contenedores estén en funcionamiento, puedes acceder a la interfaz web del chatbot en:
    [**http://localhost:8501**](http://localhost:8501)

¡Listo! Ya puedes empezar a interactuar con tu Asistente de Seguros IA.

---

## 👥 Equipo del Proyecto

Este proyecto fue desarrollado por un equipo dedicado, donde cada miembro se enfocó en un componente clave del sistema:

* **[Nombre del Integrante 1]** - [GitHub Profile Link] - *Análisis Exploratorio de Datos (EDA)*
* **[Nombre del Integrante 2]** - [GitHub Profile Link] - *Interfaz de Usuario (Streamlit)*
* **[Nombre del Integrante 3]** - [GitHub Profile Link] - *Base de Datos Vectorial (ChromaDB) y Procesamiento de Datos*
* **[Nombre del Integrante 4]** - [GitHub Profile Link] - *Backend (FastAPI) e Integración de la API*
* **[Nombre del Integrante 5]** - [GitHub Profile Link] - *Lógica del Agente, Memoria Conversacional e Integración de LLMs*
* **[Nombre del Integrante 6]** - [GitHub Profile Link] - *Evaluación del Modelo (Ragas)*

*(Nota: Reemplaza los placeholders con los nombres y enlaces de tu equipo).*
````
```markdown
# 🤖 Asistente IA para Pólizas de Seguro

Un agente inteligente y multi-herramienta diseñado para optimizar la creación de pólizas, la evaluación de riesgos y la recuperación de información en la industria de seguros.

Repositorio de GitHub: [MichaelYnoa/proyectoFinal_InsuranceChatBot](https://github.com/MichaelYnoa/proyectoFinal_InsuranceChatBot)

## Contenido

- [El Problema](#-el-problema)
- [Nuestra Solución](#-nuestra-solución)
- [Características Principales](#-características-principales)
- [Arquitectura del Sistema](#️-arquitectura-del-sistema)
- [Stack Tecnológico](#-stack-tecnológico)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Cómo Empezar](#-cómo-empezar)
- [Equipo del Proyecto](#-equipo-del-proyecto)

## 🎯 El Problema

En la industria de seguros, el proceso de suscripción (evaluar y analizar riesgos para aprobar o rechazar una póliza) es fundamental. Este proceso, junto con la generación de nuevos documentos, suele ser lento, repetitivo y requiere un análisis meticuloso de pólizas existentes y datos de mercado. El esfuerzo manual puede llevar a tiempos de respuesta más lentos para los clientes y a un aumento de los costos operativos.

## 💡 Nuestra Solución

Este proyecto introduce un **Chatbot potenciado por IA** que actúa como un asistente y asesor inteligente para las compañías de seguros. Aprovechando Modelos de Lenguaje Grandes (LLMs) y una arquitectura de agente con múltiples herramientas, nuestro chatbot agiliza el ciclo de vida de creación y consulta de pólizas. Puede acceder instantáneamente a una base de datos de pólizas para responder preguntas complejas, buscar en la web las últimas noticias del sector y proporcionar resúmenes concisos para mantener informados a los agentes.

Esta herramienta transforma un proceso tedioso en una experiencia dinámica y conversacional, asegurando que los profesionales de seguros tengan información fiable y precisa al alcance de su mano.

## ✨ Características Principales

* **Preguntas y Respuestas Conversacionales**: Realiza preguntas complejas sobre las pólizas de seguro existentes en lenguaje natural.
* **Base de Conocimiento Dinámica (RAG)**: El chatbot utiliza Generación Aumentada por Recuperación (RAG) para extraer información de una base de datos vectorial **ChromaDB** con las pólizas.
* **Búsqueda Web en Tiempo Real**: El agente puede acceder a internet usando **Tavily Search** para encontrar las últimas noticias, regulaciones o información relevante, optimizando los resultados para la IA.
* **Conversaciones con Estado (Memoria)**: El chatbot recuerda las interacciones previas dentro de una sesión para proporcionar respuestas contextuales y coherentes.
* **Evaluación Cuantitativa del Modelo**: Se utiliza la librería **Ragas** para evaluar objetivamente la calidad, precisión y relevancia de las respuestas generadas por el sistema RAG.
* **Arquitectura Desacoplada y Escalable**: La aplicación completa está contenerizada con **Docker**, asegurando un despliegue fácil y una alta escalabilidad.

## 🏗️ Arquitectura del Sistema

El proyecto se basa en una arquitectura de dos servicios desacoplados (frontend y backend) orquestados por Docker Compose.

1.  **Frontend (Streamlit)**:
    * Una interfaz de usuario web amigable construida con Streamlit.
    * Gestiona las sesiones de usuario y el historial de la conversación.
    * Se comunica con el backend a través de peticiones HTTP.

2.  **Backend (FastAPI)**:
    * Una API robusta construida con FastAPI que expone los endpoints para la lógica del chatbot.
    * Aloja el **Agente de LangChain**, que es el núcleo del sistema.
    * Gestiona la base de datos vectorial **ChromaDB** para la información de las pólizas.

### Flujo de Datos:

1.  Un usuario envía un mensaje a través de la **UI de Streamlit**.
2.  La UI envía una petición con la pregunta y el historial de chat al endpoint `/ask` en el **Backend de FastAPI**.
3.  El backend dirige la petición al **Agente de LangChain**.
4.  El Agente, potenciado por el modelo **Gemini de Google**, procesa la pregunta y decide qué herramienta usar:
    * **Herramienta de Pólizas**: Busca en la base de datos vectorial **ChromaDB** información relevante sobre las pólizas.
    * **Herramienta de Búsqueda Web**: Usa **Tavily Search** para buscar en internet información en tiempo real.
5.  La herramienta elegida devuelve sus hallazgos al agente.
6.  El agente sintetiza la información y formula una respuesta final.
7.  El backend de FastAPI envía la respuesta a la UI de Streamlit, que la muestra al usuario.

## 🛠️ Stack Tecnológico

| Categoría | Tecnología / Herramienta |
| :--- | :--- |
| **Framework IA / NLP** | LangChain |
| **Proveedor de LLM** | Google Gemini API |
| **Base de Datos Vectorial**| ChromaDB |
| **Backend** | FastAPI |
| **Frontend** | Streamlit |
| **Herramienta de Búsqueda Web** | Tavily Search |
| **Evaluación de Modelos** | Ragas |
| **Contenerización** | Docker, Docker Compose |
| **Lenguaje** | Python 3.10 |

## 📁 Estructura del Proyecto

El repositorio está organizado en dos componentes principales: el backend (`api`) y el frontend (`ui`), junto con carpetas para el análisis y la evaluación.

```

├── api/
│   ├── logic/
│   │   ├── agent.py             \# Lógica del agente, prompts y herramientas.
│   │   ├── config\_model.py      \# Configuración del modelo Gemini.
│   │   ├── config\_vectordb.py   \# Configuración de ChromaDB.
│   │   └── pdf\_processor.py     \# Utilidades para cargar y procesar los PDFs.
│   ├── data/                    \# PDFs de pólizas para construir la base de datos.
│   ├── main.py                  \# Aplicación FastAPI, endpoints y lógica de la API.
│   └── Dockerfile               \# Dockerfile para el servicio de backend.
│   └── .env                     \# Para almacenar las claves de API.
│
├── ui/
│   ├── main.py                  \# El código de la aplicación frontend de Streamlit.
│   └── Dockerfile               \# Dockerfile para el servicio de frontend.
│
├── notebooks/
│   └── EDA.ipynb                \# Análisis Exploratorio de Datos de las pólizas.
│
├── evaluation/
│   └── ragas\_evaluation.py      \# Scripts para la evaluación del chatbot con Ragas.
│
├── .gitignore
├── docker-compose.yml           \# Orquesta el inicio de todos los servicios.
└── README.md                    \# ¡Estás aquí\!

````

## 🚀 Cómo Empezar

Sigue estas instrucciones para ejecutar el proyecto en tu máquina local.

### Prerrequisitos

Debes tener instalado lo siguiente:
* **Docker**
* **Docker Compose** (generalmente incluido con Docker Desktop)

### Instalación y Configuración

1.  **Clona el repositorio:**
    ```bash
    git clone [https://github.com/MichaelYnoa/proyectoFinal_InsuranceChatBot.git](https://github.com/MichaelYnoa/proyectoFinal_InsuranceChatBot.git)
    cd proyectoFinal_InsuranceChatBot/
    ```

2.  **Crea el archivo de entorno:** Crea un archivo llamado `.env` en la carpeta `/api`. Este archivo contendrá tus claves de API.
    ```
    GOOGLE_API_KEY="TU_API_KEY_DE_GEMINI_AQUI"
    TAVILY_API_KEY="TU_API_KEY_DE_TAVILY_AQUI"
    ```
    * Puedes obtener una clave de API de Gemini en [Google AI Studio](https://aistudio.google.com/).
    * Puedes obtener una clave de API de Tavily en [Tavily.com](https://tavily.com/).

3.  **Construye y ejecuta la aplicación:** Toda la aplicación está orquestada por Docker Compose. Simplemente ejecuta el siguiente comando desde el directorio raíz del proyecto:
    ```bash
    docker compose up --build
    ```
    El flag `--build` asegura que las imágenes de Docker se reconstruyan si hay cambios en el código. La primera vez que lo ejecutes, tardará un tiempo en descargar las imágenes base y crear la base de datos vectorial.

4.  **Accede a la aplicación:** Una vez que los contenedores estén en funcionamiento, puedes acceder a la interfaz web del chatbot en:
    [**http://localhost:8501**](http://localhost:8501)

¡Listo! Ya puedes empezar a interactuar con tu Asistente de Seguros IA.

## 👥 Equipo del Proyecto

Este proyecto fue desarrollado por un equipo dedicado, donde cada miembro se enfocó en un componente clave del sistema:

* **[Nombre del Integrante 1]** - [GitHub Profile Link] - *Análisis Exploratorio de Datos (EDA)*
* **[Nombre del Integrante 2]** - [GitHub Profile Link] - *Interfaz de Usuario (Streamlit)*
* **[Nombre del Integrante 3]** - [GitHub Profile Link] - *Base de Datos Vectorial (ChromaDB) y Procesamiento de Datos*
* **[Nombre del Integrante 4]** - [GitHub Profile Link] - *Backend (FastAPI) e Integración de la API*
* **[Nombre del Integrante 5]** - [GitHub Profile Link] - *Lógica del Agente, Memoria Conversacional e Integración de LLMs*
* **[Nombre del Integrante 6]** - [GitHub Profile Link] - *Evaluación del Modelo (Ragas)*

*(Nota: Reemplaza los placeholders con los nombres y enlaces de tu equipo).*
````

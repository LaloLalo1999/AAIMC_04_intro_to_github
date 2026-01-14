**C4_M10_LAB**

**TÍTULO DEL LABORATORIO:** Proyecto Final - Construcción y Despliegue del Asistente de Investigación de IA

**MÓDULO:** 10. Proyecto Final - Aplicación Completa

**CURSO:** 4. Ingeniería de Software con IA

**OBJETIVO:**
Integrar todas las habilidades aprendidas en el curso para construir y desplegar una aplicación web full-stack de IA. El proyecto consistirá en un "Asistente de Investigación" que toma un tema, busca información en la web y genera un informe.

**REQUISITOS PREVIOS:**
*   Todos los conocimientos de los Módulos 1-9.
*   Cuentas en GitHub, Vercel y Render.
*   API Keys de OpenAI y Firecrawl (o similar).

**DURACIÓN ESTIMADA:** 4-6 horas

---

### PARTE 1: Configuración del Proyecto (Monorepo)

1.  Crea un directorio principal para el proyecto: `mkdir ai-research-assistant && cd ai-research-assistant`.
2.  Crea un repositorio de Git y súbelo a tu GitHub.
3.  Dentro del directorio, crea tres subdirectorios:
    *   `frontend`: Para la aplicación de React.
    *   `backend`: Para la API de FastAPI.
    *   `agents`: Para el servicio de Mastra.

### PARTE 2: El Servicio de Agentes (Mastra)

1.  Navega a la carpeta `agents` e inicializa un proyecto Mastra: `npx create-mastra@latest .`
2.  **Crea la Herramienta de Búsqueda:** Define una `Tool` que use `firecrawl-js` para buscar y extraer el contenido de las 3 URLs más relevantes para un tema dado.
3.  **Crea el Agente Investigador:** Define un `Agent` con un `system prompt` que le instruya a actuar como un analista experto. Su tarea es recibir un tema, usar la herramienta de búsqueda para obtener contexto, y luego generar un informe en Markdown con: Puntos Clave, Resumen Detallado y Fuentes.
4.  **Expón el Agente:** Crea un servidor simple (usando Express, que viene con Mastra) que exponga tu agente en un endpoint `POST /generate`.

### PARTE 3: El Backend (FastAPI)

1.  Navega a la carpeta `backend` y configura un entorno virtual de Python.
2.  Instala `fastapi`, `uvicorn`, `sqlalchemy`, `psycopg2-binary`, `requests`.
3.  **Define el Modelo de Datos:** Crea un modelo SQLAlchemy para guardar los informes (`ResearchReport` con `id`, `topic`, `content`, `created_at`).
4.  **Crea el Endpoint:** Implementa un endpoint `POST /research` que:
    a.  Reciba el tema del frontend.
    b.  Llame al servicio de Mastra (`http://localhost:3000/generate`).
    c.  Reciba el informe en Markdown.
    d.  Lo guarde en la base de datos PostgreSQL.
    e.  Lo devuelva al frontend.
5.  **Configura CORS:** Añade el middleware de CORS para permitir solicitudes desde tu frontend en `localhost`.

### PARTE 4: El Frontend (React + v0.dev)

1.  Navega a la carpeta `frontend` e inicializa un proyecto de React con Vite: `npm create vite@latest . -- --template react-ts`.
2.  **Genera Componentes con v0.dev:**
    a.  Usa v0.dev para generar un formulario de entrada con un `textarea` y un botón.
    b.  Genera un componente para mostrar el informe, que pueda renderizar Markdown (puedes pedirle que use `react-markdown`).
3.  **Integra los Componentes:** Añade los componentes a tu `App.tsx`.
4.  **Conecta con el Backend:**
    a.  Implementa la función `handleSubmit` que se activa al hacer clic en el botón.
    b.  Usa `fetch` para llamar a tu endpoint de FastAPI (`http://localhost:8000/research`).
    c.  Maneja el estado de la aplicación: `isLoading`, `error`, y el `report` recibido.
    d.  Muestra un spinner mientras se genera el informe y el resultado (o un error) cuando se complete.

### PARTE 5: Despliegue (Opcional, pero recomendado)

1.  **Backend en Render:**
    a.  Crea una nueva base de datos PostgreSQL en Render.
    b.  Crea un nuevo "Web Service" en Render y conéctalo a tu repositorio de GitHub. Especifica la carpeta `backend`.
    c.  Configura el comando de build (`pip install -r requirements.txt`) y el de inicio (`uvicorn main:app --host 0.0.0.0 --port $PORT`).
    d.  Añade las variables de entorno (URL de la DB, URL del servicio Mastra).
2.  **Frontend en Vercel:**
    a.  Crea un nuevo proyecto en Vercel y conéctalo a tu repositorio. Especifica la carpeta `frontend`.
    b.  Vercel detectará automáticamente que es un proyecto de Vite y lo desplegará.
    c.  Añade la URL de tu backend de Render como variable de entorno (`VITE_API_URL`).

### ENTREGABLE

Un enlace a tu repositorio de GitHub con el código completo. Si lo desplegaste, incluye también los enlaces a tu aplicación de Vercel y tu API de Render.

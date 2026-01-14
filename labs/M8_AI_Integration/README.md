# Laboratorio M8: Integración de IA con OpenAI SDK

**Módulo:** 8. Integración de IA en Aplicaciones  
**Curso:** 4. Ingeniería de Software con IA  
**Duración Estimada:** 45 minutos

## Objetivo

Construir un analizador de texto que utilice la API de OpenAI para extraer el sentimiento y las entidades clave de un texto, devolviendo los resultados en formato JSON estructurado.

## Requisitos Previos

*   Python 3.10+ instalado.
*   Cuenta de OpenAI con créditos (o API Key válida).
*   Librería `openai` instalada (`pip install openai`).
*   Librería `python-dotenv` instalada (`pip install python-dotenv`).

## Instrucciones

### Paso 1: Configuración del Entorno

1.  Crea una carpeta para tu proyecto:
    ```bash
    mkdir text_analyzer && cd text_analyzer
    ```

2.  Crea un archivo `.env` y añade tu API Key:
    ```
    OPENAI_API_KEY=sk-proj-...
    ```

3.  Crea un archivo `requirements.txt`:
    ```
    openai
    python-dotenv
    ```

4.  Instala las dependencias:
    ```bash
    pip install -r requirements.txt
    ```

### Paso 2: El Script de Análisis (`analyzer.py`)

Crea un archivo `analyzer.py` con el siguiente código base:

```python
import os
import json
from dotenv import load_dotenv
from openai import OpenAI

# Cargar variables de entorno
load_dotenv()

# Inicializar cliente
client = OpenAI()

def analyze_text(text: str) -> dict:
    """
    Analiza un texto y extrae sentimiento y entidades.
    
    Args:
        text: El texto a analizar.
    
    Returns:
        Diccionario con sentiment, summary, y entities.
    """
    print("Analizando texto...")
    
    system_prompt = """
    Eres un analizador de texto experto. Analiza el texto proporcionado y devuelve un JSON con:
    - "sentiment": "positive", "negative", o "neutral"
    - "summary": Un resumen de 1 frase del texto
    - "entities": Una lista de objetos con "name" y "type" (Person, Organization, Location)
    
    Responde SOLO con el JSON, sin explicaciones adicionales.
    """
    
    # TU CÓDIGO AQUÍ:
    # 1. Llama a client.chat.completions.create con response_format={"type": "json_object"}.
    # 2. Usa el modelo "gpt-4o-mini" o "gpt-3.5-turbo".
    # 3. Parsea y retorna el JSON.
    pass

if __name__ == "__main__":
    sample_text = """
    Hola, soy Carlos Pérez de la empresa TechSolutions. 
    Quería comentarles que el servicio que recibimos ayer en Madrid fue excelente. 
    El técnico llegó puntual y resolvió el problema del servidor en 10 minutos. 
    Definitivamente renovaremos el contrato el próximo año.
    """
    
    result = analyze_text(sample_text)
    if result:
        print(json.dumps(result, indent=2, ensure_ascii=False))
```

### Paso 3: Implementación

Completa la función `analyze_text` para que:
*   Haga una llamada a la API de OpenAI con el formato JSON activado.
*   Maneje errores de la API.
*   Retorne el diccionario parseado.

### Paso 4: Prueba con Diferentes Textos

Prueba tu script con estos textos y verifica si la IA acierta:

*   **Texto 1 (Queja):** "Estoy furioso. El paquete llegó roto y nadie me contesta en soporte. Exijo un reembolso inmediato." -> Debería ser `negative`.
*   **Texto 2 (Neutro):** "Adjunto la factura correspondiente al mes de marzo para su revisión." -> Debería ser `neutral`.

### Paso 5: Reto Extra (Opcional)

Añade la funcionalidad de streaming para mostrar la respuesta en tiempo real.

## Entregable

Un archivo comprimido `.zip` que contenga:
1.  `analyzer.py` completo y funcionando.
2.  `requirements.txt`.
3.  Una captura de pantalla de la terminal mostrando la ejecución exitosa con el JSON formateado.

## Criterios de Evaluación

| Criterio | Puntos |
|----------|--------|
| Llamada a la API correcta | 30 |
| Uso de JSON Mode | 20 |
| Manejo de errores | 20 |
| Código limpio y documentado | 15 |
| Pruebas con múltiples textos | 15 |
| **Total** | **100** |

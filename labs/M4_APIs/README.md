# Laboratorio M4: Consumo de APIs con Python

**Módulo:** 4. APIs y Backend  
**Curso:** 4. Ingeniería de Software con IA  
**Duración Estimada:** 45 minutos

## Objetivo

Construir un script de Python que consuma una API pública (OpenWeatherMap) para obtener el clima de una ciudad y mostrar los resultados de forma estructurada.

## Requisitos Previos

*   Python 3.10+ instalado.
*   Librería `requests` instalada (`pip install requests`).
*   Librería `python-dotenv` instalada (`pip install python-dotenv`).
*   API Key de OpenWeatherMap (gratuita): [https://openweathermap.org/api](https://openweathermap.org/api)

## Instrucciones

### Paso 1: Configuración del Entorno

1.  Crea una carpeta para tu proyecto:
    ```bash
    mkdir weather_app && cd weather_app
    ```

2.  Crea un archivo `.env` y añade tu API Key:
    ```
    OPENWEATHER_API_KEY=tu_api_key_aqui
    ```

3.  Crea un archivo `requirements.txt`:
    ```
    requests
    python-dotenv
    ```

4.  Instala las dependencias:
    ```bash
    pip install -r requirements.txt
    ```

### Paso 2: El Script Base (`weather.py`)

Crea un archivo `weather.py` con el siguiente código base:

```python
import os
import requests
from dotenv import load_dotenv

# Cargar variables de entorno
load_dotenv()

API_KEY = os.getenv("OPENWEATHER_API_KEY")
BASE_URL = "https://api.openweathermap.org/data/2.5/weather"

def get_weather(city: str) -> dict:
    """
    Obtiene el clima actual de una ciudad.
    
    Args:
        city: Nombre de la ciudad (ej: "Madrid", "Mexico City")
    
    Returns:
        Diccionario con la información del clima.
    """
    # TU CÓDIGO AQUÍ:
    # 1. Construye los parámetros de la petición (q, appid, units, lang).
    # 2. Realiza la petición GET a la API.
    # 3. Maneja errores (status code != 200).
    # 4. Retorna el JSON de la respuesta.
    pass

def display_weather(data: dict) -> None:
    """
    Muestra el clima de forma formateada.
    """
    # TU CÓDIGO AQUÍ:
    # Extrae y muestra: ciudad, país, temperatura, descripción, humedad.
    pass

if __name__ == "__main__":
    city = input("Ingresa el nombre de una ciudad: ")
    weather_data = get_weather(city)
    if weather_data:
        display_weather(weather_data)
```

### Paso 3: Implementación

Completa las funciones `get_weather` y `display_weather` para que:
*   `get_weather`: Haga una petición GET con los parámetros correctos y maneje errores.
*   `display_weather`: Muestre la información de forma legible.

**Pista:** Usa `units=metric` para obtener la temperatura en Celsius y `lang=es` para descripciones en español.

### Paso 4: Prueba

Ejecuta tu script y prueba con diferentes ciudades:
```bash
python weather.py
```

### Paso 5: Reto Extra (Opcional)

Añade la funcionalidad de guardar el historial de consultas en un archivo JSON.

## Entregable

Un archivo comprimido `.zip` que contenga:
1.  `weather.py` completo y funcionando.
2.  `requirements.txt`.
3.  Una captura de pantalla de la terminal mostrando la ejecución exitosa.

## Criterios de Evaluación

| Criterio | Puntos |
|----------|--------|
| Petición GET correcta | 30 |
| Manejo de errores | 20 |
| Formateo de salida | 20 |
| Uso de variables de entorno | 15 |
| Código limpio y documentado | 15 |
| **Total** | **100** |

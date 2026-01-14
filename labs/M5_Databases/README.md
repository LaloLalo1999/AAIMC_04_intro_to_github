# Laboratorio M5: Bases de Datos con SQLAlchemy

**Módulo:** 5. Bases de Datos y Persistencia  
**Curso:** 4. Ingeniería de Software con IA  
**Duración Estimada:** 60 minutos

## Objetivo

Construir una aplicación de gestión de tareas (To-Do) con persistencia en base de datos SQLite usando SQLAlchemy como ORM.

## Requisitos Previos

*   Python 3.10+ instalado.
*   Librería `sqlalchemy` instalada (`pip install sqlalchemy`).

## Instrucciones

### Paso 1: Configuración del Proyecto

1.  Crea una carpeta para tu proyecto:
    ```bash
    mkdir todo_app && cd todo_app
    ```

2.  Crea un archivo `requirements.txt`:
    ```
    sqlalchemy
    ```

3.  Instala las dependencias:
    ```bash
    pip install -r requirements.txt
    ```

### Paso 2: Definir el Modelo (`models.py`)

Crea un archivo `models.py` con el siguiente código base:

```python
from sqlalchemy import create_engine, Column, Integer, String, Boolean, DateTime
from sqlalchemy.orm import declarative_base, sessionmaker
from datetime import datetime

# Crear la base
Base = declarative_base()

class Task(Base):
    """
    Modelo para representar una tarea.
    """
    __tablename__ = "tasks"
    
    id = Column(Integer, primary_key=True, autoincrement=True)
    title = Column(String(100), nullable=False)
    description = Column(String(500), nullable=True)
    completed = Column(Boolean, default=False)
    created_at = Column(DateTime, default=datetime.utcnow)
    
    def __repr__(self):
        status = "✓" if self.completed else "○"
        return f"[{status}] {self.id}: {self.title}"

# Crear el motor y la sesión
engine = create_engine("sqlite:///todo.db", echo=False)
Session = sessionmaker(bind=engine)

def init_db():
    """Crea las tablas en la base de datos."""
    Base.metadata.create_all(engine)
```

### Paso 3: Implementar las Operaciones CRUD (`crud.py`)

Crea un archivo `crud.py` con las siguientes funciones:

```python
from models import Session, Task, init_db

def create_task(title: str, description: str = None) -> Task:
    """Crea una nueva tarea."""
    # TU CÓDIGO AQUÍ
    pass

def get_all_tasks() -> list:
    """Obtiene todas las tareas."""
    # TU CÓDIGO AQUÍ
    pass

def get_task_by_id(task_id: int) -> Task:
    """Obtiene una tarea por su ID."""
    # TU CÓDIGO AQUÍ
    pass

def update_task(task_id: int, title: str = None, description: str = None, completed: bool = None) -> Task:
    """Actualiza una tarea existente."""
    # TU CÓDIGO AQUÍ
    pass

def delete_task(task_id: int) -> bool:
    """Elimina una tarea por su ID."""
    # TU CÓDIGO AQUÍ
    pass

def toggle_complete(task_id: int) -> Task:
    """Marca una tarea como completada o pendiente."""
    # TU CÓDIGO AQUÍ
    pass
```

### Paso 4: Crear la Interfaz de Línea de Comandos (`main.py`)

Crea un archivo `main.py` que permita al usuario:
*   Listar todas las tareas.
*   Añadir una nueva tarea.
*   Marcar una tarea como completada.
*   Eliminar una tarea.

### Paso 5: Prueba

Ejecuta tu aplicación y prueba todas las operaciones CRUD:
```bash
python main.py
```

## Entregable

Un archivo comprimido `.zip` que contenga:
1.  `models.py` completo.
2.  `crud.py` completo y funcionando.
3.  `main.py` con la interfaz de usuario.
4.  `requirements.txt`.
5.  Una captura de pantalla de la terminal mostrando la ejecución exitosa.

## Criterios de Evaluación

| Criterio | Puntos |
|----------|--------|
| Modelo definido correctamente | 20 |
| Operaciones CRUD funcionando | 40 |
| Interfaz de usuario funcional | 20 |
| Código limpio y documentado | 10 |
| Manejo de errores | 10 |
| **Total** | **100** |

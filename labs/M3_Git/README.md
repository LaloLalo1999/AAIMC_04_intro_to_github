# Laboratorio M3: Flujo de Trabajo Git Profesional

**Módulo:** 3. Git y Control de Versiones  
**Curso:** 4. Ingeniería de Software con IA  
**Duración Estimada:** 45 minutos

## Objetivo

Practicar el flujo de trabajo profesional de Git utilizando ramas, commits, y Pull Requests en un escenario realista de desarrollo colaborativo.

## Requisitos Previos

*   Git instalado en tu sistema.
*   Cuenta de GitHub.
*   Acceso a este repositorio.

## Instrucciones

### Parte 1: Configuración Inicial (5 min)

1.  Clona este repositorio si no lo has hecho:
    ```bash
    git clone https://github.com/LaloLalo1999/AAIMC_04_intro_to_github.git
    cd AAIMC_04_intro_to_github
    ```

2.  Configura tu identidad de Git (si no lo has hecho):
    ```bash
    git config --global user.name "Tu Nombre"
    git config --global user.email "tu@email.com"
    ```

3.  Asegúrate de estar en la rama `main` y actualizada:
    ```bash
    git checkout main
    git pull origin main
    ```

### Parte 2: Crear una Rama de Feature (10 min)

1.  Crea una nueva rama para tu trabajo:
    ```bash
    git checkout -b feature/lab-m3-[tu-nombre]
    ```

2.  Crea un archivo con tu nombre en la carpeta `labs/M3_Git/submissions/`:
    ```bash
    mkdir -p labs/M3_Git/submissions
    touch labs/M3_Git/submissions/[tu-nombre].md
    ```

3.  Edita el archivo y añade:
    *   Tu nombre completo.
    *   Fecha de completación.
    *   Una breve reflexión sobre lo que aprendiste en el Módulo 3.

### Parte 3: Commits Atómicos (10 min)

1.  Realiza tu primer commit:
    ```bash
    git add labs/M3_Git/submissions/[tu-nombre].md
    git commit -m "feat(lab-m3): add initial submission file"
    ```

2.  Añade más contenido a tu archivo (por ejemplo, respuestas a las preguntas del quiz).

3.  Realiza un segundo commit:
    ```bash
    git add .
    git commit -m "feat(lab-m3): complete lab reflection"
    ```

### Parte 4: Push y Pull Request (15 min)

1.  Sube tu rama al repositorio remoto:
    ```bash
    git push origin feature/lab-m3-[tu-nombre]
    ```

2.  Ve a GitHub y crea un **Pull Request** desde tu rama hacia `main`.

3.  En la descripción del PR, incluye:
    *   Un resumen de lo que hiciste.
    *   Cualquier dificultad que encontraste.

### Parte 5: Revisión y Merge (5 min)

1.  Espera la aprobación del instructor o de un compañero.
2.  Una vez aprobado, realiza el **Merge** del PR.
3.  Elimina tu rama remota después del merge.

## Entregable

*   Un Pull Request completado y mergeado en este repositorio.
*   Tu archivo de submission en `labs/M3_Git/submissions/[tu-nombre].md`.

## Criterios de Evaluación

| Criterio | Puntos |
|----------|--------|
| Rama creada correctamente | 20 |
| Commits atómicos y descriptivos | 30 |
| Pull Request con descripción completa | 30 |
| Archivo de submission completo | 20 |
| **Total** | **100** |

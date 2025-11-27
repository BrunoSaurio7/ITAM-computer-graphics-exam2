# Gráfica por Computadora: Iluminación y Transformaciones (Parcial 2)

Este repositorio contiene la implementación práctica para el Segundo Examen Parcial del curso de Gráfica por Computadora. La solución utiliza C++ y OpenGL 3.3 para demostrar modelos avanzados de iluminación, atenuación de reflectores (spotlights) y propiedades de reflexión especular.

**Realizado por:**
- Bruno Daniel Pérez Vargas
- Fernando Villalobos Betancourt

## Tecnologías Utilizadas

* **IDE:** Visual Studio 2022
* **Lenguaje:** C++
* **API:** OpenGL 3.3 Core Profile
* **Dependencias:**
    * GLFW (Ventanas y Entradas)
    * GLAD (Carga de funciones OpenGL)
    * GLM (Matemáticas para OpenGL)
    * stb_image (Carga de Texturas)

## Resumen de Proyectos

La solución se divide en dos proyectos distintos:

### 1. Pregunta 1: Análisis de Atenuación de Reflector (Spotlight)

**Objetivo:** Implementar un reflector fijo apuntando a un objeto específico en la escena y analizar el efecto de la atenuación lineal en la suavidad de los bordes de la luz.

**Detalles Clave de Implementación:**
* **Apuntado:** La dirección del reflector se calcula dinámicamente para seguir estrictamente al cubo más profundo en la escena (Z = -15.0f).
* **Atenuación:** Se manipula el coeficiente de atenuación lineal (`light.linear`) para alterar la dureza visual del borde del reflector.

**Explicación Técnica:**
Para lograr que el borde de la luz se desvanezca suavemente en lugar de cortarse abruptamente, se modificó el coeficiente de atenuación lineal. Al aumentar este valor, incrementamos la rapidez con la que la luz pierde intensidad conforme viaja. Esto causa que la intensidad luminosa llegue a cero antes de alcanzar el límite físico angular del reflector. Al no haber luz visible llegando al borde del cono, el corte duro desaparece visualmente, creando un gradiente natural hacia la oscuridad.

**Pasos para Reproducir:**
Para replicar los requerimientos del examen, modifique la variable `linearAttenuation` en `main.cpp` (Línea ~45):

1.  **Transición de Borde Duro:**
    * Configurar: `float linearAttenuation = 0.09f;`
    * *Resultado:* El reflector proyecta un círculo claro y definido sobre el objeto.
    * **Evidencia:**
      > *[Inserta aquí tu captura de pantalla, ej: ![Borde Duro](img/duro.png)]*

2.  **Transición de Borde Suave:**
    * Configurar: `float linearAttenuation = 0.7f;`
    * *Resultado:* La intensidad de la luz decae rápidamente antes de llegar al ángulo de corte, creando un efecto de desvanecimiento suave.
    * **Evidencia:**
      > *[Inserta aquí tu captura de pantalla, ej: ![Borde Suave](img/suave.png)]*

---

### 2. Pregunta 2: Saturación Especular y Animación

**Objetivo:** Renderizar una escena con múltiples fuentes de luz y objetos rotando para demostrar el impacto del coeficiente de brillo (*shininess*) en la saturación del color.

**Detalles Clave de Implementación:**
* **Animación:** Los cubos rotan continuamente basándose en `glfwGetTime()`.
* **Reflexión Especular:** La propiedad de brillo (*shininess*) del material se manipula para simular una intensidad especular extrema, resultando en pérdida de color (blanqueamiento).

**Explicación Técnica:**
Para lograr que el efecto de reflexión especular causara una máxima pérdida de color, se redujo drásticamente el coeficiente `material.shininess` a un valor de 0.04f. En el modelo de iluminación Phong, al usar un exponente cercano a cero, el resultado de la potencia se acerca a 1.0 incluso para ángulos de reflexión amplios. Esto provoca que la luz especular no se concentre en un punto, sino que se distribuya con máxima intensidad sobre casi toda la superficie del cubo orientada a la luz. Al sumarse este blanco intenso al color difuso del objeto, el color original se satura y el objeto parece perder su color, viéndose mayormente blanco o metálico brillante.

**Pasos para Reproducir:**
Para replicar los requerimientos de video, modifique la variable `shininessValue` en `main.cpp` (Línea ~40):

1.  **Iluminación Estándar:**
    * Configurar: `float shininessValue = 32.0f;`
    * *Resultado:* Brillos especulares estándar, típicos de materiales plásticos o semipulidos.
    * **Evidencia:**
      > *[Inserta aquí el enlace a tu video, ej: [Ver en YouTube](https://youtube.com/...)]*

2.  **Saturación Especular (Pérdida de Color):**
    * Configurar: `float shininessValue = 0.04f;`
    * *Resultado:* El componente especular se expande para cubrir la mayoría de la superficie, dominando sobre el color difuso.
    * **Evidencia:**
      > *[Inserta aquí el enlace a tu video, ej: [Ver en YouTube](https://youtube.com/...)]*

---

## Instrucciones de Construcción (Build)

### Visual Studio 2022
1. Abrir la solución `ITAM-ComputerGraphics-Exam2.sln`.
2. Asegurarse de que ambos proyectos estén configurados para **x64**.
3. Verificar directorios de inclusión y librerías (GLFW, GLAD, GLM).
4. Establecer el proyecto deseado como "Startup Project" y ejecutar.

### MSYS2 (MinGW64)
Navegar a la carpeta del proyecto específico vía terminal y ejecutar:
```bash
g++ main.cpp glad.c -o main -I. -lglfw3 -lopengl32 -lgdi32
./main.exe

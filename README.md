# Computer Graphics: Lighting and Transformations (Exam 2)

This repository contains the practical implementation for the Second Partial Exam of the Computer Graphics course. The solution utilizes C++ and OpenGL 3.3 to demonstrate advanced lighting models, spotlight attenuation, and specular reflection properties.

## Technologies Used

* **IDE:** Visual Studio 2022
* **Language:** C++
* **API:** OpenGL 3.3 Core Profile
* **Dependencies:**
    * GLFW (Windowing and Input)
    * GLAD (OpenGL Loading Library)
    * GLM (OpenGL Mathematics)
    * stb_image (Texture Loading)

## Projects Overview

The solution is divided into two distinct projects:

### 1. Question1: Spotlight Attenuation Analysis

**Objective:** Implement a fixed spotlight targeting a specific object in the scene and analyze the effect of linear attenuation on light edge softness.

**Key Implementation Details:**
* **Targeting:** The spotlight direction is dynamically calculated to strictly follow the deepest cube in the scene (Z = -15.0f).
* **Attenuation:** The linear attenuation coefficient (`light.linear`) is manipulated to alter the visual hardness of the spotlight's edge.

**Reproduction Steps:**
To replicate the exam requirements, modify the `linearAttenuation` variable in `main.cpp` (Line ~45):

1.  **Hard Edge Transition:**
    * Set `float linearAttenuation = 0.09f;`
    * *Result:* The spotlight projects a clear, defined circle on the object.
2.  **Soft Edge Transition:**
    * Set `float linearAttenuation = 0.7f;`
    * *Result:* The light intensity decays rapidly before reaching the cut-off angle, creating a smooth fade-out effect.

---

### 2. Question2: Specular Saturation and Animation

**Objective:** Render a scene with multiple light sources and rotating objects to demonstrate the impact of the shininess coefficient on color saturation.

**Key Implementation Details:**
* **Animation:** Cubes rotate continuously based on `glfwGetTime()`.
* **Specular Reflection:** The material's shininess property is manipulated to simulate extreme specular intensity, resulting in color loss (whitening).

**Reproduction Steps:**
To replicate the video requirements, modify the `shininessValue` variable in `main.cpp` (Line ~40):

1.  **Standard Lighting:**
    * Set `float shininessValue = 32.0f;`
    * *Result:* Standard specular highlights typical of plastic or semi-polished materials.
2.  **Specular Saturation (Color Loss):**
    * Set `float shininessValue = 0.04f;`
    * *Result:* The specular component expands to cover the majority of the surface, overpowering the diffuse color and causing the object to appear bright white/metallic.

---

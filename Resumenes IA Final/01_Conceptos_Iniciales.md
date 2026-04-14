# 01 — Conceptos Iniciales de IA

> **Playlist:** Conceptos Iniciales  
> **Objetivo:** Entender qué es la IA, qué son los Sistemas Inteligentes, y cómo funciona el Machine Learning básico.

---

## 1. ¿Qué es la Inteligencia Artificial?

**Definición:** Rama de las ciencias computacionales que estudia modelos de cómputo (tecnologías, arquitecturas) para desarrollar software capaz de realizar actividades propias de los seres humanos relacionadas con:
- Razonamiento
- Conducta
- Aprendizaje

**Disciplinas que comprende:**
- IA Tradicional
- Inteligencia Computacional
- Machine Learning (Aprendizaje Automático)
- Visión Artificial
- Procesamiento del Lenguaje Natural
- Big Data & Data Mining

---

## 2. Sistemas Inteligentes (SI)

Son artefactos con **comportamiento inteligente**. Un comportamiento inteligente implica:
- **Racional:** toma decisiones consistentes con su objetivo
- **No omnisciente:** no posee todos los conocimientos ni datos
- **No infalible:** no siempre es exitoso
- **Puede aprender:** mejora durante su uso
- **Flexible y robusto:** soporta cambios del dominio

**Se usan en dominios complejos** donde:
- El problema no se entiende completamente
- No se pueden anticipar todas las situaciones futuras
- Las posibles soluciones son demasiado numerosas para búsqueda exhaustiva
- Un modelo tradicional requeriría simplificación que lo vuelve inútil

---

## 3. Tipos de Sistemas Inteligentes

### Por fuente de conocimiento:
| Fuente | Tipo |
|--------|------|
| Pública (libros, manuales, datos digitales) | Sistema Inteligente |
| Privada (mente del experto) | Sistema Experto |

> **Regla clave:** Un SI no siempre es un SE, pero un SE **siempre** es un SI.

### Por tecnología:
| Tecnología | Ejemplos |
|-----------|---------|
| IA Tradicional | SBC, SET, Lógica Difusa |
| Machine Learning | Inducción, Regresión, RNA, Lógica Difusa |
| Inteligencia Computacional | RNA, Algoritmos Genéticos |

---

## 4. IA Tradicional vs Inteligencia Computacional

### Sistema Basado en Conocimientos (SBC)
- Fuentes **públicas**
- Componentes: Base de conocimientos (hechos + reglas) → Motor de inferencias → Interface E/S

### Sistema Experto Tradicional (SET)
- Fuentes **privadas** (+ puede usar públicas)
- Componentes adicionales:
  - **Base de datos:** almacena datos del problema actual (temporal)
  - **Memoria de trabajo:** registra la traza del razonamiento
  - **Trazador de explicaciones:** justifica el resultado al usuario
  - **Trazador de consultas:** pide información adicional al usuario
  - **Manejador de comunicaciones:** interfaz de E/S

### Inteligencia Computacional
Inspiración biológica: RNA, computación evolutiva, inteligencia de enjambre, sistemas inmunológicos artificiales.

---

## 5. Machine Learning (ML)

**Definición:** Genera software capaz, de forma automática, de adquirir capacidades y adaptarse a su entorno.  
Flujo: **Datos → Algoritmo → Modelo**

### Estrategias de aprendizaje:
| Estrategia | Descripción |
|-----------|-------------|
| **Supervisado** | Se dan ejemplos + salida deseada. El algoritmo aprende la relación. |
| **No supervisado** | Solo ejemplos de entrada. El algoritmo agrupa por similitud. |

### Tipos de entrenamiento:
| Tipo | Descripción |
|------|-------------|
| **Offline (estático)** | Aprende en fase de entrenamiento; en producción no aprende más. |
| **Online (dinámico)** | Sigue aprendiendo en producción (requiere monitoreo). |

### Tipos de algoritmos de ML:
- Clustering
- **Inducción** ← importante para el final
- **Regresión** ← importante para el final
- Basados en Bayes
- Redes Neuronales Artificiales

---

## 6. Algoritmos de Inducción (TDIDT)

**Supervisado + Offline.** Identifica reglas de clasificación a partir de una tabla de ejemplos.

**Estructura de datos:** tabla donde:
- **Filas** = ejemplos
- **Columnas** = atributos
- **Atributo objetivo** = lo que quiero predecir (único, siempre al final)

**Las reglas tienen:**
- **Antecedente:** condiciones sobre atributos de entrada
- **Consecuente:** valor del atributo objetivo

### Algoritmo TDIDT (Top Down Induction Decision Trees)
Genera árboles de decisión con **divide y vencerás**:

```
A partir de un conjunto T:
1. Si T está vacío → finalizar
2. Si T tiene un único valor en atributo objetivo → generar hoja
3. Sino:
   a. Seleccionar atributo con mayor GANANCIA DE INFORMACIÓN en T
   b. Particionar T por cada valor del atributo seleccionado
   c. Aplicar recursivamente a cada partición
```

**Resultado:** árbol de decisión → conjunto de reglas IF-THEN-ELSE

---

## 7. Algoritmos de Regresión

**Supervisado.** A partir de una tabla identifica una **fórmula** que describe la relación entre atributos de entrada y el atributo objetivo.  
**Requisito:** todos los atributos deben tener valores **numéricos** (continuos). Si no, se deben transformar previamente.

---

## 8. Procesos de construcción de modelos ML

| Proceso | Descripción |
|---------|-------------|
| **Entrenamiento** | Aprende los valores del modelo a partir de ejemplos |
| **Validación** | Evalúa distintos parámetros para optimizar el modelo (en paralelo al entrenamiento) |
| **Prueba** | Evalúa la capacidad de **generalización** del modelo final |

**Tres conjuntos de datos distintos:** entrenamiento / validación / prueba

---

## 9. Métricas de evaluación

### Para salidas discretas (clasificación):
| Métrica | Fórmula | Qué mide |
|---------|---------|---------|
| **Exactitud (Accuracy)** | (VP+VN)/(VP+FP+VN+FN) | Proporción de identificaciones correctas |
| **Precisión** | VP/(FP+VP) | De los que dije que eran positivos, ¿cuántos lo eran? |
| **Recuperación (Recall)** | VP/(VP+FN) | De los positivos reales, ¿cuántos identifiqué? |
| **F1 Score** | 2*(P*R)/(P+R) | Combina precisión y recuperación |
| **Matriz de confusión** | — | Muestra VP, VN, FP, FN → mide convergencia |

> **Atención:** Buena exactitud ≠ modelo confiable (especialmente con clases desbalanceadas). Mejorar precisión suele perjudicar recall y viceversa.

### Para salidas continuas (regresión):
| Métrica | Fórmula |
|---------|---------|
| **Error absoluto** | \|real - estimado\| |
| **Error relativo** | \|real - estimado\| / real |

Cuanto menores los errores → mejor el modelo.

---

## Resumen clave para el final

1. **IA** estudia cómo construir software que razone, actúe y aprenda.
2. **SI** es cualquier artefacto con comportamiento inteligente; **SE** es un SI que emula a un experto humano con conocimiento privado.
3. **ML** = Datos → Algoritmo → Modelo. Puede ser supervisado/no supervisado y offline/online.
4. **TDIDT** genera árboles de decisión por ganancia de información (divide y vencerás).
5. **Regresión** = encontrar fórmula numérica; **Inducción** = encontrar reglas de clasificación.
6. Siempre se necesitan 3 conjuntos de datos: entrenamiento, validación y prueba.
7. **F1 Score** balancea precisión y recall cuando hay clases desbalanceadas.

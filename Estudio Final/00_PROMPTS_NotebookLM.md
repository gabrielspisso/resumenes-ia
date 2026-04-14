# Prompts para NotebookLM — IA Final

> Copiá y pegá el prompt en el campo "Customize" antes de generar el audio.  
> Objetivo: que el video se quede en el tema puntual, sin irse por las ramas.

---

## 01 — Conceptos Iniciales

```
Quiero un resumen oral enfocado exclusivamente en los conceptos fundamentales de Inteligencia Artificial para un examen universitario. Cubrí estos puntos en orden:
1. Qué es un Sistema Inteligente y qué lo diferencia de un sistema experto (SE) y un sistema basado en conocimientos (SBC).
2. Las tres formas de desarrollo: IA Tradicional, Inteligencia Computacional y Machine Learning. Qué incluye cada una y un ejemplo concreto.
3. Estrategias de aprendizaje: supervisado vs no supervisado, y tipos de entrenamiento offline vs online.
4. Algoritmo TDIDT: qué hace, cómo genera el árbol y qué resultado produce.
5. Las métricas de evaluación: exactitud, precisión, recall y F1. Cuándo usar cada una.

No menciones algoritmos genéticos, redes neuronales, búsqueda heurística ni ningún otro tema. Solo conceptos iniciales y métricas básicas de ML.
```

---

## 02 — Análisis de Protocolos

```
Quiero un resumen oral sobre la técnica de Análisis de Protocolos (AP) para un examen universitario de Inteligencia Artificial. Cubrí estos puntos en orden:
1. Qué es el AP, para qué sirve y quién lo lleva a cabo.
2. Las 4 etapas en orden: Grabación → Transcripción → Codificación → Interpretación. Qué se hace en cada una.
3. En la etapa de Codificación: qué son Concepto, Característica, Valor, Relación y Operador. Diferencia entre estados como conceptos vs estados como valores.
4. Qué son los sinónimos, metacomentarios e incertidumbres. Cómo se identifican.
5. Cómo se escribe una regla de razonamiento en la etapa de Interpretación (formato SI-ENTONCES).
6. Qué tipo de conocimiento se extrae: procedimental vs declarativo, y en qué etapa se encuentra cada uno.

No hables de emparrillado, redes neuronales, algoritmos genéticos ni ningún otro tema. Solo Análisis de Protocolos.
```

---

## 03 — Algoritmos Genéticos

```
Quiero un resumen oral sobre Algoritmos Genéticos para un examen universitario de Inteligencia Artificial. Cubrí estos puntos en orden:
1. Qué son los AG, para qué se usan y cuándo conviene aplicarlos (vs Machine Learning vs IA Tradicional).
2. La analogía con la evolución: cromosoma, genotipo, fenotipo, fitness.
3. El flujo completo del algoritmo: GPI → Selección → Cruzamiento → Mutación → Criterio de paro. Diferencia entre vuelta y corrida.
4. Los 3 métodos de selección: Torneo, Ranking y Ruleta. Para la Ruleta, explicar también la versión con control sobre número esperado (parte entera + mantisa).
5. Los métodos de cruzamiento: Simple, Multipunto y Binomial (máscara complemento, doble y al azar).
6. La mutación: cuándo ocurre, cómo funciona, y los 3 tipos (simple, adaptativa por convergencia, adaptativa por temperatura).
7. Criterio de paro: las 4 formas posibles.

No hables de redes neuronales, búsqueda heurística, emparrillado ni ningún otro tema. Solo Algoritmos Genéticos.
```

---

## 04 — Redes Neuronales Artificiales

```
Quiero un resumen oral sobre Redes Neuronales Artificiales para un examen universitario de Inteligencia Artificial. El tema es extenso, así que priorizá la profundidad sobre la amplitud. Cubrí estos puntos en orden:
1. Qué es una neurona artificial: entradas, pesos (excitador/inhibidor/neutro), función de activación y función de salida.
2. Los parámetros que definen un modelo RNA: tipo de información, tipo de asociación (heteroasociativa vs autoasociativa), topología y reglas de aprendizaje.
3. Modelo Perceptrón: arquitectura, proceso de entrenamiento, el rol del alfa, y su limitación (solo funciones lineales).
4. Modelo Backpropagation: cómo supera al Perceptrón, proceso de entrenamiento con gradiente decreciente, diseño de capas (entrada, ocultas, salida) y qué hacer si no aprende.
5. Modelo Hopfield: arquitectura autoasociativa, entrenamiento con producto vectorial, criterio de convergencia y limitaciones (ortogonalidad de patrones).
6. CNN: por qué se necesita para imágenes, cómo funcionan los filtros, las 3 etapas de una capa convolucional (convolución + ReLU + pooling) y la arquitectura completa.
7. Preparación de datos: normalización (Standard Scaler, MinMax, Robust), separación entrenamiento/validación/prueba, y data augmentation.
8. Parámetros de entrenamiento: mini-batch, épocas, overfitting/underfitting, early stopping, fórmulas de error (MSE vs CrossEntropy) y optimizadores (Adam es el más recomendado).

No hables de algoritmos genéticos, búsqueda heurística, emparrillado ni ningún otro tema. Solo Redes Neuronales.
```

---

## 05 — Emparrillado

```
Quiero un resumen oral sobre la técnica de Emparrillado (Repertory Grid) para un examen universitario de Inteligencia Artificial. Cubrí estos puntos en orden:
1. Qué es el emparrillado, para qué sirve y cuáles son sus ventajas y limitaciones (especialmente que por sí solo no sirve para construir una base de conocimientos).
2. Las 5 etapas: identificación de elementos → identificación de características → diseño de parrilla → formalización → interpretación.
3. Los 3 tipos de parrilla: dicotómica, clasificatoria y evaluativa. Diferencias clave (escala, empates).
4. La formalización de elementos: cómo calcular la matriz de distancias, cómo fusionar el par con mínima distancia, y cómo armar el árbol de elementos.
5. La formalización de características: cómo construir la parrilla opuesta, calcular D1 (diagonal superior) y D2 (diagonal inferior), y construir la matriz final.
6. La interpretación: cómo leer el árbol de elementos (distancia = nivel) y los 4 tipos de relaciones entre características: paralela, recíproca, ortogonal y ambigua.

No hables de Análisis de Protocolos, redes neuronales ni ningún otro tema. Solo Emparrillado.
```

---

## 06 — Métodos de Búsqueda

```
Quiero un resumen oral sobre los Métodos de Búsqueda para resolución de problemas, para un examen universitario de Inteligencia Artificial. Cubrí estos puntos en orden:
1. Cómo se representa un problema: estado, estado inicial, estados intermedios, estados finales y operadores.
2. Métodos sin información de dominio (búsqueda ciega): Primero en Amplitud (BFS), Primero en Profundidad (DFS), Generación y Prueba, y Bidireccional. Para cada uno: estructura de datos, cómo recorre, si garantiza solución y cuándo termina.
3. Métodos con heurística: Escalada Simple, Escalada Máxima Pendiente, Primero el Mejor, Beam Search y A*. Para cada uno: si tiene retroceso, si garantiza solución, y cuál es el criterio para elegir el siguiente nodo.
4. La diferencia clave entre Escalada (sin retroceso, puede quedar en máximo local) y Primero el Mejor (con LNA y LNC, siempre encuentra solución).
5. Cómo funciona A*: la fórmula f(n) = g(n) + h(n) y por qué garantiza la solución óptima.

No hables de redes neuronales, algoritmos genéticos, lógica difusa ni ningún otro tema. Solo Métodos de Búsqueda.
```

---

## 07 — Lógica Difusa

```
Quiero un resumen oral sobre Lógica Difusa y Razonamiento Aproximado para un examen universitario de Inteligencia Artificial. Cubrí estos puntos en orden:
1. Por qué se necesita razonamiento aproximado: diferencia entre incertidumbre e imprecisión, y sus fuentes.
2. Diferencia entre lógica tradicional (V/F), lógica polivalente y lógica difusa (valores continuos [0,1]).
3. Qué es un conjunto difuso y qué es la función de pertenencia μ. Aclarar que NO es una probabilidad.
4. Los 3 operadores de lógica difusa: negación (1-μ), conjunción/AND (mínimo), disyunción/OR (máximo).
5. Cómo funciona la implicación difusa (SI A → ENTONCES B): los 3 pasos.
6. Sistemas difusos: arquitectura general con fuzzificación y defuzzificación.
7. Modelo Mamdani vs Takagi-Sugeno: diferencias en complejidad, cantidad de reglas y forma del consecuente.
8. Las 3 críticas a los sistemas difusos y por qué existen los sistemas neurodifusos.

No hables de redes neuronales, algoritmos genéticos, búsqueda heurística ni ningún otro tema. Solo Lógica Difusa.
```

---

## 08 — Implementación de Sistemas Inteligentes

```
Quiero un resumen oral sobre el proceso de Implementación de Sistemas Inteligentes para un examen universitario de Inteligencia Artificial. Cubrí estos puntos en orden:
1. Diferencias entre software tradicional y sistema inteligente: tareas, implementación (algorítmica vs declarativa), stakeholders, y tipo de mantenimiento (perfectivo).
2. Las 6 fases de implementación en orden: Definición del problema → Datos → Selección de tecnología → Construcción del modelo → Aplicación → Instalación y mantenimiento.
3. Fase 1 (Definición): fuentes de información (recursos propios, externos, stakeholders), técnicas de recolección (extracción vs educción), y las técnicas de análisis conceptual (abstraer, descomponer, proyectar, modularizar).
4. Fase 2 (Datos): recolección, estudio, integración, limpieza y selección.
5. Fase 3 (Selección de tecnología): cuándo usar ML, cuándo usar IA Tradicional y cuándo usar Algoritmos Genéticos.
6. Fase 5 (Aplicación): qué son los pipelines y para qué sirven.

No te vayas a los detalles de cada tecnología (eso ya está en otros resúmenes). Enfocate en el proceso de implementación como metodología.
```

---

## 09 — PNL: Procesamiento del Lenguaje Natural

```
Quiero un resumen oral sobre Procesamiento del Lenguaje Natural (PNL) para un examen universitario de Inteligencia Artificial. Cubrí estos puntos en orden:
1. Qué es el PNL y por qué el lenguaje natural requiere IA (a diferencia del lenguaje artificial).
2. Las 4 áreas de lingüística relevantes: fonología, morfología, sintaxis y semántica.
3. NLU vs NLG: qué hace cada una y ejemplos concretos de aplicación.
4. El pipeline de procesamiento: Tokenización → Normalización → Segmentación. Qué hace cada paso y para qué sirve.
5. Normalización: diferencia entre Lematización (forma base semántica) y Stemming (raíz morfológica). Ejemplos concretos.
6. Categorización gramatical (PoS): diferencia entre Open Classes (cambian con el tiempo) y Closed Classes (fijas).
7. Autocorrección: cómo funciona con distancia de edición (Levenshtein).
8. Autocompletado: cómo funciona con modelos n-gram.
9. NLP tradicional vs NLP con ML: ventajas, limitaciones, y técnicas de representación de texto (TF-IDF y GloVe).

No hables de redes neuronales en detalle, algoritmos genéticos ni ningún otro tema. Solo PNL.
```

---

## Tips generales para usar en NotebookLM

- **Subí solo el archivo de ese tema** (no todos a la vez) para que no mezcle información
- Si el audio se va por las ramas igual, agregá al final del prompt: *"No incluyas introducción general ni comparaciones con otras tecnologías de IA. Ve directo al contenido."*
- Para que sea más corto: agregá *"Hacé el resumen en no más de 8 minutos. Priorizá los puntos más difíciles de recordar."*
- Para que incluya ejemplos: agregá *"Incluí al menos un ejemplo concreto por cada concepto principal."*

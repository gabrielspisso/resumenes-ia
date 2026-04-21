# Resumen Final IA — Temas 04, 06, 08, 09

> Combinación de: Redes Neuronales (v3) · Métodos de Búsqueda · Implementación de SI · PNL

---

# 04 v3 — Redes Neuronales Artificiales (Versión Final para el Examen)

> **Base:** resumen v1 + temas de clases del prof. Pitel que faltaban (CNN, entrenamiento avanzado)

---

## ¿Qué son?

Sistema de cómputo inspirado en el cerebro biológico formado por **neuronas artificiales interconectadas** que aprenden de ejemplos. **No poseen base de conocimientos** — el conocimiento queda codificado en los **valores de los pesos**.

**Relación con otras ramas:**
- **Inteligencia Computacional:** inspiración biológica
- **Machine Learning:** aprenden automáticamente de ejemplos

**Ventajas:** Aprendizaje adaptativo · Autoorganización · Tolerancia a fallos · Operación en tiempo real · Fácil inserción en tecnología existente

---

## La Neurona Artificial

**Proceso:**
1. Entradas `Xj` (valores numéricos)
2. × Pesos `Wji` (sinapsis: positivo = excitadora, 0 = neutra, negativo = inhibitoria)
3. **Entrada neta:** `Net_i = Σ(Wji × Xj)`
4. **Función de activación** A(Net_i): determina si la neurona se activa (usa el umbral)
5. **Función de salida/transferencia** S[A(Net_i)] = Yi → en la práctica: `F(Net_i) = Yi`

> **Lo único que cambia durante el entrenamiento son los pesos W** (nunca la función ni la estructura).

---

## Componentes de una RNA

| Componente | Descripción |
|-----------|-------------|
| **Capas** | Entrada / Ocultas (procesamiento) / Salida |
| **Conexión Wij** | >0 excitadora, =0 neutra, <0 inhibitoria |

**Funciones de activación comunes:** Escalón, Identidad, Lineal mixta, ReLU  
**Funciones de salida comunes:** Escalón, **Sigmoidal** (la más usada), Gaussiana, tanh

---

## Parámetros del Modelo RNA

### Tipo de información:
- **Discreta:** binarios (0/1) &nbsp;&nbsp; **Continua:** reales

### Tipo de asociación:
| Tipo | Aprendizaje | Descripción |
|------|------------|-------------|
| **Heteroasociativa** | Supervisado | Se da patrón de entrada + salida deseada |
| **Autoasociativa** | No supervisado | La red aprende sola a identificar la salida |

### Topología: Monocapa o multicapa · Conectividad total o parcial · Feedforward o retroalimentación

### Reglas de aprendizaje:
| Combinación | Método | Uso |
|------------|-------|-----|
| Supervisado offline | Corrección de error | Clasificar / predecir |
| Supervisado online | Por refuerzo | Solo valoración de la salida |
| No supervisado | Hebbiano | — |
| No supervisado | Competitivo/cooperativo | Clustering |

---

## Modelo 1: Perceptrón

**Tipo:** Heteroasociativa · Supervisado · **Offline** · Corrección de errores · **Monocapa (1 neurona)**

**Algoritmo:** Para cada patrón calcula Net_i → función escalón → si Yi ≠ Yd → `ΔWj = α × (Yd - Yi) × Xj` → repite hasta error 0.

**Recomendaciones:**
- Umbral: mantenerlo constante · Valores de entrada: normalizar en [0;1]
- **Alfa:** entre 0.05 y 0.30 (pequeño = lento pero no olvida; grande = rápido pero puede olvidar)
- Pesos iniciales: entre 0.00 y 0.50

**Desventaja:** Solo aprende funciones **linealmente separables**. No puede aprender XOR ni funciones no lineales.

---

## Modelo 2: Backpropagation (Multi-Perceptrón)

**Tipo:** Heteroasociativa · Supervisado · **Offline** · Corrección de errores · **Multicapa (≥2 capas)**

**Aplicaciones:** Clasificación, estimación y predicción. Puede aprender funciones **lineales y no lineales**.

**Entrenamiento (Gradiente Decreciente + Backprop):**
1. Propagación hacia adelante → calcula salida capa por capa
2. Calcula error (Salida deseada − Salida generada)
3. Calcula gradiente δ en capa de salida
4. Propaga δ hacia atrás ponderado por la magnitud de las conexiones
5. Ajusta pesos: `W_nuevo = W_viejo + α × δ × entrada`
6. Repite hasta error aceptable

**Requiere funciones derivables → se usa Sigmoidal** (continua 0 a 1). Para salida real → Gaussiana o tanh.

**Capa de salida y función de error:**
| Función de salida | Función de error |
|------------------|-----------------|
| Identidad (salida continua) | **MSE** |
| Sigmoidal (salida binaria) | **CrossEntropy** |
| Softmax (múltiples clases) | **CrossEntropy** |

**Topología (neuronas ocultas):**
- **Teorema de Aproximación Universal:** existe una red suficientemente grande para aprender cualquier conjunto de datos con el grado de precisión deseado, pero **no indica cuántas capas ni neuronas** hacen falta
- 1 capa oculta: suficiente para la mayoría · 2 capas: aprende más rápido
- **Más de 3 capas puede dificultar el ajuste de pesos en las capas más profundas**
- No hay regla general → prueba y corrección, o usar AG

**Pesos iniciales:** entre 0 y 0.5, **inicializados al azar y distintos entre neuronas de la misma capa** para "romper simetrías" y evitar que aprendan lo mismo.

**Si la red no aprende → en orden:**
1. Normalizar datos · 2. Modificar alfa · 3. Cambiar pesos iniciales · 4. Cambiar orden de patrones · 5. Agregar neuronas/capas · 6. Revisar los datos de los patrones de entrenamiento

**Ciclos de entrenamiento:**
- Pocos → **underfitting** (no terminó de aprender) · Demasiados → **overfitting** (memoriza, no generaliza)
- **Early Stopping:** detiene el entrenamiento cuando el error de validación empieza a subir

---

## Modelo 3: Hopfield

**Tipo:** Autoasociativa · **No supervisado** · Offline · Hebbiano · **Monocapa con conexiones laterales**

**Uso:** Completar patrones incompletos a partir de patrones ya aprendidos.

**Entrenamiento:**
1. Para cada patrón `p`: calcular `M_p = p^T × p` (vector × transpuesto)
2. Tachar la diagonal → matriz de pesos del patrón
3. Sumar todas las matrices → matriz de pesos total de la red

**Convergencia:** La red terminó cuando en **2 ciclos seguidos** se obtiene el mismo resultado.

**Limitaciones:**
- Patrones deben ser **ortogonales** (diferentes en al menos N/2 componentes)
- Capacidad de almacenamiento limitada (aprox. 0.15 × N patrones)

---

## Modelo 4: Redes Convolucionales (CNN)

**Tipo:** Heteroasociativa · Supervisada · Offline · Backpropagation  
**Uso principal:** Reconocimiento y clasificación de **imágenes**  
**Inspiración:** Cortex Visual Primario del cerebro humano

**¿Por qué no usar Backprop directamente para imágenes?**  
Una imagen 200×200 px = 40.000 entradas. Con 4.000 neuronas ocultas → **160 millones de pesos** → inviable.

**Solución CNN:** reducir parámetros con:
- **Conectividad escasa (sparse):** cada neurona oculta procesa solo una región de la imagen
- **Pesos compartidos (filtros):** todas las regiones usan los mismos pesos

### Estructura de una capa convolucional (3 etapas):

| Etapa | Qué hace |
|-------|---------|
| **1. Convolución** | Filtro F×F se desliza por la imagen (stride) → genera el feature map. Con k filtros: solo `k × F × F` pesos |
| **2. Detector (activación)** | Aplica función no lineal al feature map → sigmoidal, tanh o **ReLU** (la más recomendada actualmente) |
| **3. Pooling (reducción)** | Reduce dimensiones. **Max Pooling** (toma el máximo de cada región 2×2) — el más usado |

> Los valores de los filtros **se aprenden durante el entrenamiento** (son los pesos que ajusta backprop).

### Arquitectura completa:
```
Imagen → [Conv + Detector + Pooling] × n → Flatten → [Capas Lineales] × m → Softmax
```

**Recomendaciones:** Preferir muchos filtros pequeños (3×3) sobre pocos grandes · Equilibrar ancho (filtros) y profundidad (capas).

---

## Preparación de datos

### Normalización:
| Método | Cuándo usar |
|--------|-------------|
| **Standard Scaler** `(x - media) / desv_std` | Caso general |
| **MinMax Scaler** `(x - min) / (max - min)` | Cuando el rango es conocido → resultado en [0,1] |
| **Robust Scaler** | Cuando hay outliers |

> **Regla de oro:** Aplicar la **misma fórmula y mismos parámetros** a entrenamiento, validación, prueba Y producción.

### Separación de datos:
- 70% entrenamiento+validación / 30% prueba (o 80/20 con muchos datos)
- Dentro del 70%: 80% entrenamiento / 20% validación
- **Muestreo estratificado:** mantiene la proporción de clases en cada conjunto (recomendado)

### Procesamiento por lotes:
| Método | Ajusta pesos | Recomendado |
|--------|------------|------------|
| Ejemplo por ejemplo | Por cada ejemplo | No (lento) |
| Full Batch | Al final de cada época | No (mucha RAM) |
| **Mini-Batch** | Por cada lote de N ejemplos | ✓ **Sí** |

---

## Algoritmos de optimización (variantes del Gradiente Decreciente)

| Algoritmo | Alfa | Descripción |
|-----------|------|-------------|
| **SGD** | Constante | Base; converge bien en clasificación de imágenes |
| **Momentum** | Constante | Considera gradientes anteriores; evita oscilaciones |
| **AdaGrad** | Adaptativo | Alfa distinto por parámetro |
| **RMSProp** | Adaptativo | Media móvil; bueno para no convexos |
| **Adam** | Adaptativo | Combina Momentum + RMSProp; **funciona bien en la mayoría de casos** |

---

## Comparación de Modelos RNA

| Característica | Perceptrón | Backpropagation | Hopfield | CNN |
|---------------|-----------|----------------|---------|-----|
| **Entrenamiento** | Supervisado | Supervisado | No supervisado | Supervisado |
| **Estrategia** | Corrección de error (delta) | Delta generalizada + backprop | Hebbiano | Backprop |
| **Modo** | Offline | Offline | Offline | Offline |
| **Arquitectura** | 1 capa, 1 neurona | 2+ capas | 1 capa + conexiones laterales | Conv + Lineal |
| **Tipo** | Heteroasociativa | Heteroasociativa | Autoasociativa | Heteroasociativa |
| **Salida** | Discreta | Discreta o continua | Vector | Discreta (generalmente) |
| **Aplicación** | Funciones lineales | Lineales y no lineales | Completar patrones | Reconocimiento de imágenes |

---

## Resumen clave — RNA

1. RNA = neuronas artificiales interconectadas que aprenden de ejemplos. **Solo se modifican los pesos.**
2. **Perceptrón:** monocapa, solo lineal, supervisado offline. Alfa 0.05–0.30. `ΔWj = α × (Yd - Yi) × Xj`.
3. **Backpropagation:** multicapa, lineal y no lineal, supervisado offline. Propaga error hacia atrás con gradiente. Requiere Sigmoidal.
4. **Hopfield:** autoasociativa, no supervisada. Aprende con `M = p^T × p` (tachar diagonal). Converge con 2 ciclos iguales.
5. **CNN:** para imágenes. Usa filtros (pesos compartidos). Etapas: convolución → ReLU → Max Pooling → capas lineales → softmax.
6. **Underfitting** = pocas épocas. **Overfitting** = demasiadas épocas. **Early stopping** detiene cuando sube el error de validación.
7. **Función de error:** MSE para identidad · CrossEntropy para sigmoidal/softmax.
8. **Adam** funciona bien en la mayoría de casos. **Mini-batch** es el procesamiento más eficiente.

---

---

# 06 — Métodos de Búsqueda

> **Objetivo:** Resolver problemas formalizándolos como búsqueda en un espacio de estados.

---

## Modelar el Problema

Todo problema se formaliza como **búsqueda en un espacio de estados**:
- **Estado:** "foto" del sistema en un momento dado
- **Estado inicial:** punto de partida · **Estados finales / solución:** lo que queremos alcanzar
- **Operadores / reglas:** vinculan un estado padre con un estado hijo

---

## Métodos SIN información del dominio (Búsqueda Ciega)

### Primero en Amplitud (BFS)
- Estructura: **cola FIFO** · Recorre nivel a nivel
- **Garantiza encontrar la solución** · Problema: usa mucha memoria

### Primero en Profundidad (DFS)
- Estructura: **pila LIFO** · Explora una rama hasta el fondo antes de retroceder
- Usa poca memoria · Problema: **no garantiza solución óptima**

### Generación y Prueba
- Recorre todos los nodos por ramas · Permite encontrar **todos** los estados solución
- Problema: muy lento en problemas complejos

### Bidireccional
- Dos búsquedas simultáneas: top-bottom (desde inicial) + bottom-up (desde solución)
- Al menos una debe ser en **amplitud** · Para cuando se encuentran en un estado intermedio común

---

## Métodos CON información del dominio (Búsqueda Heurística)

Se usa **función heurística h(n)**: a mayor valor → nodo más deseable.

### Escalada Simple (Hill Climbing Simple)
- Genera el primer hijo y lo compara con el actual; si es mejor → avanza
- Sin retroceso → puede quedar en **máximo local**

### Escalada Máxima Pendiente (Steepest Ascent)
- Genera **todos** los hijos y avanza al **mejor**
- Sin retroceso → también puede quedar en máximo local

### Primero el Mejor (Best First Search)
- Usa **LNA** (nodos abiertos ordenados por heurística) y **LNC** (nodos cerrados)
- **Tiene retroceso** → puede escapar de máximos locales · **Garantiza encontrar solución**

### Beam Search
- Como Primero el Mejor pero con **LNA limitada a N nodos** (memoria acotada)
- No garantiza solución (depende de N)

### A* (A Estrella)
- Como Primero el Mejor pero con `f(n) = g(n) + h(n)` (costo acumulado + heurística)
- **Garantiza la solución óptima** si la heurística es admisible

---

## Tabla Comparativa

| Método | ¿Retroceso? | ¿Garantiza solución? | Criterio |
|--------|------------|---------------------|---------|
| BFS | — | Sí | Por niveles (FIFO) |
| DFS | — | No (óptima) | Por ramas (LIFO) |
| Gen & Prueba | — | Sí (todas) | Por ramas |
| Bidireccional | — | Sí | Dos frentes |
| Escalada Simple | No | No | Primer hijo mejor |
| Escalada Máx. Pendiente | No | No | Mejor de todos los hijos |
| Primero el Mejor | Sí | Sí | Mejor nodo en LNA |
| Beam Search | Depende | No | Mejor en LNA limitada |
| A* | Sí | Sí (óptima) | Mejor f(n) = g(n) + h(n) |

---

## Resumen clave — Búsqueda

1. **Sin heurística:** BFS (amplitud), DFS (profundidad), Gen & Prueba, Bidireccional.
2. **Con heurística:** Escalada Simple/Máxima Pendiente, Primero el Mejor, Beam Search, A*.
3. **Escalada:** sin retroceso → máximo local.
4. **Primero el Mejor:** con retroceso (LNA) → garantiza solución.
5. **A*:** = Primero el Mejor + costo acumulado → solución óptima.
6. **Beam Search:** Primero el Mejor con LNA limitada a N nodos.

---

---

# 08 — Implementación de Sistemas Inteligentes

> **Objetivo:** Proceso completo para construir e implementar un Sistema Inteligente en la práctica.

---

## SW Tradicional vs Sistema Inteligente

| Aspecto | SW Tradicional | Sistema Inteligente |
|---------|---------------|-------------------|
| **Implementación** | Algorítmica (procedural) | **Declarativa** |
| **Stakeholders** | Directivos, gerentes, usuarios | + **Expertos** |
| **Mantenimiento** | Correctivo, Adaptativo | **Perfectivo** |

---

## Fases de la Implementación de un SI

```
Definición del problema → Identificación y transformación de datos → Selección de la tecnología → Construcción del modelo → Aplicación del sistema inteligente
```

### Fase 1: Definición del Problema
- **Elicitar:** identificar fuentes (propias, externas, stakeholders) y recolectar hechos
- Técnicas de educción: entrevistas, emparrillado, análisis de protocolos, prototipado, observación
- **Comprender:** abstraer, descomponer, proyectar, modularizar

### Fase 2: Identificación y Transformación de Datos
- **Integración:** unificar datos en una única tabla
- **Limpieza:** corregir nulos, incompletos, con ruido → asignar valor / eliminar fila / eliminar atributo
- **Formateo:** discretizar continuos; codificar alfanuméricos con código numérico o atributo binario por valor; fechas → separar o calcular días desde fecha fija
- **Normalización:** usando promedio y varianza. Regla de oro: misma normalización en dev y producción.

### Fase 3: Selección de la Tecnología
| Situación | Tecnología |
|-----------|-----------|
| Datos disponibles | **ML** |
| Reglas sin datos | IA Tradicional / IC |
| Solo heurísticas | **AG (IC)** |

### Fase 4: Construcción del Modelo
- **ML:** Datos → Algoritmo → Modelo → Entrenamiento → Validación → Prueba
- **IA Tradicional:** Reglas y hechos → Base de Conocimientos
- **AG:** definir cromosoma + función de aptitud

### Fase 5: Aplicación del SI
- **Pipeline:** recolección → preparación → ejecución del modelo → ajuste de resultados
- Regla de oro: **mismas acciones** de recolección y preparación que durante el desarrollo
- Integrar con sistemas externos → instalación → monitoreo → mantenimiento perfectivo

---

## Resumen clave — Implementación SI

1. Las fases: **Definir → Transformar datos → Elegir tecnología → Construir modelo → Aplicar**.
2. Emparrillado y análisis de protocolos son técnicas de **educción** (fase 1).
3. Datos disponibles → ML · Reglas sin datos → IA Trad. / IC · Solo heurísticas → AG.
4. La regla de oro: **mismas transformaciones en dev que en producción**.
5. Mantenimiento de SI = **perfectivo**.

---

---

# 09 — PNL: Procesamiento del Lenguaje Natural

> **Objetivo:** Permitir a las máquinas comprender, interpretar y generar lenguaje humano.

---

## ¿Qué es el PNL?

Rama de la IA que se enfoca en la **interacción entre computadoras y el lenguaje humano**. Comparte territorio con ML y Deep Learning.

**Aplicaciones:** análisis de sentimientos, traducción automática, extracción de información, generación de texto, clasificación de textos.

---

## Tipos de Lenguaje

| Tipo | Descripción | ¿Requiere SI? |
|------|-------------|--------------|
| **Artificial** (prog., técnico, científico) | Normas estrictas, sintaxis predecible | **No** |
| **Natural** (humano, hablado/escrito) | Ambiguo, dependiente del contexto | **Sí** |

---

## Orientaciones del PNL

| Orientación | Sigla | Qué hace |
|------------|-------|---------|
| **Comprensión del lenguaje natural** | NLU | Analiza sintaxis y semántica para entender el significado |
| **Generación del lenguaje natural** | NLG | Genera texto completo a partir de una entrada |

---

## Pipeline de Procesamiento de Texto

### 1. Tokenización
Divide el texto en unidades básicas llamadas **tokens** (palabras, frases, caracteres).

### 2. Normalización
| Técnica | Descripción | Ejemplo |
|---------|-------------|---------|
| **Lematización** | Reduce al lema (forma base en el diccionario) | "corriendo" → "correr" |
| **Stemming** | Reduce a la raíz (núcleo morfológico) | "corriendo" → "corr" |
| **Minúsculas** | Todo a minúsculas | "Hola" → "hola" |
| **Eliminar puntuación** | Quitar símbolos irrelevantes | "hola!" → "hola" |

### 3. Segmentación
Agrupa tokens en oraciones o párrafos para facilitar el procesamiento por unidades completas.

---

## Técnicas Complementarias

### Categorización (Part-of-Speech Tagging)
Asigna etiquetas gramaticales a cada token: sustantivos, verbos, adjetivos (**open classes**) · pronombres, preposiciones, conjunciones (**closed classes**).

### Autocorrección
Identifica palabras fuera del vocabulario → busca palabras cercanas con **distancia de edición (Levenshtein)** → selecciona la de mayor probabilidad según el contexto.

### Autocompletado
Aprende probabilidades de secuencias de palabras → dado el contexto (últimas n palabras) predice la siguiente. Modelo básico: **n-gram**.

---

## NLP Tradicional vs NLP con ML

| | NLP Tradicional | NLP con ML |
|--|----------------|-----------|
| **Ventajas** | Simple, pocos datos, fácil de mantener | Más potente, maneja ambigüedad y contexto |
| **Limitaciones** | Ambigüedad léxica, dependencia entre palabras, falta de contexto | Requiere más datos y recursos |
| **Representación de texto** | — | TF-IDF (importancia en corpus), GloVe (relaciones semánticas) |
| **Modelos** | Reglas + estadística | Regresión, árboles de decisión, Random Forest, K-Means |

---

## Resumen clave — PNL

1. **Lenguaje artificial** no necesita IA; **lenguaje natural** sí (ambiguo, depende del contexto).
2. Pipeline: **Tokenización → Normalización → Segmentación**.
3. **Lematización** → forma base semántica · **Stemming** → raíz morfológica.
4. **NLU:** comprende texto · **NLG:** genera texto.
5. **Autocorrección** usa distancia de edición (Levenshtein) · **Autocompletado** usa modelos n-gram.
6. NLP con ML: vectoriza con TF-IDF/GloVe → aplica regresión, árboles o clustering.

# 04 — Redes Neuronales Artificiales (RNA)

> **Playlist:** Redes Neuronales Artificiales (15 videos)  
> Fuente: Clase 5, Videos 1-15, Para el Coloquio

---

## ¿Qué son?

Evolución de un sistema de cómputo basado en modelo biológico. Formada por **elementos simples de proceso (neuronas) interconectados** que operan en paralelo para cumplir un objetivo.

**Relación con otras ramas de IA:**
- **Inteligencia Computacional:** inspiración biológica (el cerebro)
- **Machine Learning:** aprenden automáticamente de ejemplos

**Una RNA NO posee base de conocimientos.** El conocimiento queda codificado implícitamente en los **valores de los pesos** de las conexiones.

**Pueden usarse** con fuentes públicas (SI) o con fuentes privadas de un experto (SE).

**Ventajas:**
- **Aprendizaje adaptativo:** aprenden casi cualquier tipo de problema
- **Autoorganización:** modifican sus conexiones solas durante el entrenamiento
- **Tolerancia a fallos:** cierta flexibilidad para datos no vistos
- **Tiempo real:** una vez entrenada, es muy rápida en producción
- **Portabilidad:** funciona en cualquier hardware/lenguaje

---

## Neurona Artificial

**Modelo biológico → artificial:**

| Biología | Artificial |
|----------|-----------|
| Dendritas | Entradas Xj |
| Sinapsis excitadora (+) | Peso Wji > 0 |
| Sinapsis inhibidora (-) | Peso Wji < 0 |
| Sinapsis neutra (0) | Peso Wji = 0 |
| Axón | Salida Yi |

**Proceso de cálculo:**

```
Entradas X0...Xn
    × Pesos W0i...Wni
    ↓
Net_i = Σ(Wji × Xj)   ← Entrada neta
    ↓
A(Net_i)               ← Función de activación (con umbral)
    ↓
S[A(Net_i)] = Yi       ← Función de salida/transferencia
```

En la práctica se usan combinadas: `F(Net_i) = Yi`

**La salida es única** pero puede ir a múltiples neuronas.

**Funciones de activación comunes:** Escalón, Identidad, Lineal mixta, ReLU

**Funciones de salida comunes:** Escalón, Mixta, **Sigmoidal** (la más usada), Gaussiana, Softmax

---

## Parámetros que definen un Modelo RNA

### 1. Tipo de información de E/S
- **Discreta:** binarios (0/1)
- **Continua:** valores reales

### 2. Tipo de asociación

| Tipo | Aprendizaje | Descripción |
|------|------------|-------------|
| **Heteroasociativa** | Supervisado | Se da patrón de entrada + salida deseada |
| **Autoasociativa** | No supervisado | La red aprende sola a identificar la salida |

### 3. Topología
- **Capas:** monocapa o multicapa
- **Conectividad:** total o parcial
- **Conexiones:** hacia adelante (feedforward) o hacia atrás (retroalimentación)

### 4. Reglas de aprendizaje

| Estrategia | Modo | Método | Uso |
|-----------|------|--------|-----|
| Supervisado | Offline | Corrección de error | Clasificar / predecir |
| Supervisado | Online | Por refuerzo | Solo valoración de la salida |
| No supervisado | Off/Online | Hebbiano | — |
| No supervisado | Off/Online | Competitivo/cooperativo | Clustering |

> **Solo se modifican los pesos W de las conexiones** durante el entrenamiento.

---

## Modelo 1: Perceptrón

**Tipo:** Heteroasociativa · Supervisado · **Offline** · Corrección de error · **Monocapa (1 neurona)**

**Creado por:** Rosenblatt, 1958

**Proceso de entrenamiento (por patrón):**
```
1. Presentar patrón de entrada
2. Calcular la salida de la neurona
3. Comparar con la salida deseada
4. Si hay error → ajustar pesos:
   W_nuevo = W_viejo + α × error × entrada
5. Repetir para todos los patrones → ciclos hasta convergencia
```

**El coeficiente alfa (α):**
- Evita que olvide lo aprendido (aprendizaje más lento pero más estable)
- Valor recomendado: **0.05 a 0.30**
- Muy grande → inestabilidad; muy pequeño → muy lento

**Recomendaciones:**
- Umbral: mantenerlo constante para mayor estabilidad
- Trabajar con valores binarios o normalizados en [0;1]
- Pesos iniciales: entre 0.00 y 0.50

**Limitación:** Solo aprende funciones **lineales**. No puede resolver el problema XOR.

---

## Modelo 2: Multi-Perceptrón (Backpropagation)

**Nombre completo:** RNA con Regla Delta Generalizada / Gradiente Decreciente / Retropropagación del Error.

**Tipo:** Heteroasociativa · Supervisado · **Offline** · Corrección de error · **Multicapa (≥2 capas)**

**Superación del Perceptrón:** combina múltiples neuronas → puede aprender funciones **lineales y no lineales**.

**Aplicaciones:** Clasificación de datos, estimación y predicción.

**Requiere:** funciones **derivables** → se usa **Sigmoidal** para salida binaria.

### Proceso de entrenamiento

```
Para cada patrón:
1. Propagación hacia adelante:
   → calcular salida de cada neurona, capa por capa
2. Calcular error:
   → Error = Salida deseada - Salida generada
3. Calcular gradiente para la neurona de salida:
   → δ_salida = derivada_función × error
4. Propagar gradiente hacia atrás (backpropagation):
   → δ_oculta = derivada_función × Σ(δ_siguiente × W_conexión)
5. Ajustar todos los pesos:
   → W_nuevo = W_viejo + α × δ_neurona × entrada_conexión
6. Repetir hasta que el error sea aceptable
```

### Diseño de la red

#### Capa de entrada
- Valores reales: una neurona por atributo, función identidad
- Valores binarios: una neurona por bit, o una por valor posible (one-hot encoding)

#### Capas ocultas
- No hay regla general; se determina por prueba y corrección o mediante AG
- **1 capa oculta:** suficiente para la mayoría de problemas
- **2 capas ocultas:** aprende más rápido para la misma cantidad de neuronas
- Funciones: Sigmoidal para binarios, ReLU (muy usada hoy), tanh para reales

#### Capa de salida
- Una neurona por salida requerida
- Identidad → salida continua → usar **MSE** para calcular error
- Sigmoidal → salida binaria → usar **CrossEntropy**
- Softmax → múltiples clases → usar **CrossEntropy**

#### Pesos iniciales: entre 0 y 0.5 (al azar)

#### Si la red no aprende → probar en este orden:
1. Normalizar datos de entrada y salida
2. Modificar alfa
3. Cambiar pesos iniciales
4. Cambiar el orden de los patrones
5. Agregar neuronas ocultas y/o capas

---

## Modelo 3: RNA Hopfield

**Tipo:** Autoasociativa · **No supervisada** · Offline · **Hebbiano** · Monocapa con **conexiones laterales**

**Uso:** Completar patrones incompletos a partir de patrones ya aprendidos (memoria asociativa).

### Entrenamiento

Para cada patrón p (vector fila):
1. Calcular `M_p = p^T × p` (producto del vector columna por el vector fila)
2. Tachar la diagonal principal (poner en 0)
3. Matriz de pesos total = suma de todas las matrices M_p de cada patrón

### Operación / Producción

1. Ingresar el patrón incompleto
2. La red itera actualizando cada neurona con los pesos aprendidos
3. **Criterio de convergencia:** 2 ciclos consecutivos con el mismo resultado → completó el patrón

### Limitaciones

- Los patrones deben ser **ortogonales** entre sí: diferir en al menos N/2 componentes (donde N = número de neuronas)
- Capacidad de almacenamiento: aprox. **0.15 × N patrones**

---

## Modelo 4: Redes Convolucionales (CNN)

**Tipo:** Heteroasociativa · Supervisada · Offline · Corrección de error (Backpropagation)

**Inspiración:** Cortex Visual Primario del cerebro humano

**Uso principal:** Reconocimiento y clasificación de **imágenes**

**¿Por qué no usar Backprop directamente para imágenes?**  
Una imagen de 200×200 px = 40.000 neuronas de entrada. Con 4.000 neuronas ocultas → 160 millones de pesos → inviable.

**Solución CNN:** usar **filtros** (pesos compartidos + conectividad escasa).

### Estructura de una capa convolucional (3 etapas)

#### Etapa 1: Convolución (filtros)
- Se define un filtro F×F (ej: 3×3) que se desliza por la imagen
- En cada posición: multiplica píxeles × pesos del filtro → suma → genera **feature map**
- Con k filtros de F×F → solo `k × F × F` pesos (en vez de millones)
- **Los valores de los filtros se aprenden durante el entrenamiento (son los pesos)**

#### Etapa 2: Detector (función de activación)
- Se aplica una función no lineal al feature map
- Generalmente **ReLU** (devuelve 0 si negativo, el valor si positivo)

#### Etapa 3: Pooling (reducción)
- Reduce dimensiones preservando lo importante
- **Max Pooling:** toma el valor máximo de cada región (más usado)
- **Average Pooling:** toma el promedio de cada región
- El pooling es fijo (no se aprende)

### Arquitectura completa de una CNN

```
Entrada (imagen)
    → [Convolución + ReLU + Pooling] × n capas conv.
    → Flatten (matriz → vector)
    → [Capas Lineales (Backpropagation)] × m
    → Capa de Salida (Softmax)
```

### Recomendaciones de diseño CNN
- Filtros reducen en potencias de 2 a medida que la red se hace más profunda
- Preferir muchos filtros pequeños (3×3) sobre pocos grandes (5×5)
- Equilibrar ancho (cantidad de filtros) y profundidad (capas)

---

## Preparación de Datos

### Normalización

**Por qué:** atributos con escalas distintas dificultan el aprendizaje.

| Método | Fórmula | Cuándo usar |
|--------|---------|-------------|
| **Standard Scaler** | `(x - media) / desv_estándar` | Caso general |
| **MinMax Scaler** | `(x - min) / (max - min)` → [0,1] | Cuando el rango es conocido |
| **Robust Scaler** | Ignora outliers | Cuando hay valores extremos |

> **Regla de oro:** Aplicar la **misma fórmula y parámetros** al entrenamiento, validación, prueba Y producción.

### Separación de datos

- 70% entrenamiento+validación / 30% prueba (o 80/20, 90/10 con muchos datos)
- Dentro del 70%: 80% entrenamiento / 20% validación

**Técnicas de muestreo:**
- **Estratificado (recomendado):** mantiene la proporción de clases en cada conjunto
- **Simple:** aleatorio, puede generar desbalance

**Data Augmentation (imágenes):** volteo, rotación, zoom, cambios de brillo/ruido → cuando hay pocos datos.

---

## Parámetros de Entrenamiento

### Procesamiento de datos

| Método | Ajusta pesos | Ventaja/Desventaja |
|--------|-------------|-------------------|
| Ejemplo por ejemplo | Por ejemplo | Lento con muchos datos |
| Full Batch | Una vez por época | Menos preciso |
| Estocástico | Por ejemplo aleatorio | Necesita muchas épocas |
| **Mini-Batch** ✓ | Por lote N | **El más recomendado** — equilibra velocidad y calidad |

- **Step/Paso:** procesar un mini-batch → calcular error → ajustar pesos
- **Época:** completar todo el conjunto de entrenamiento

### Overfitting y Underfitting

| Situación | Síntoma | Solución |
|----------|---------|---------|
| **Underfitting** | Error de entrenamiento alto | Más épocas, más neuronas |
| **Overfitting** | Error entrenamiento bajo, error validación/prueba alto | Menos épocas, regularización |
| **Early Stopping** | Detener cuando error de validación sube mientras el de entrenamiento baja | Automático |

### Fórmulas de error (Loss functions)

| Capa de salida | Loss recomendado |
|---------------|-----------------|
| Identidad (salida continua) | **MSE** (Error Cuadrático Medio) |
| Sigmoidal (salida binaria) | **CrossEntropy** (Entropía Cruzada) |
| Softmax (múltiples clases) | **CrossEntropy** |

### Tasa de aprendizaje alfa

- Rango recomendado: **0.01 a 0.40**
- Alfa muy grande → inestabilidad / esquiva el óptimo
- Alfa muy pequeño → aprendizaje extremadamente lento

### Optimizadores (variantes del Gradiente Decreciente)

| Algoritmo | Alfa | Descripción |
|-----------|------|-------------|
| **SGD** | Constante | Base; más lento pero predecible |
| **Momentum** | Constante | Considera gradientes anteriores; puede sobrepasar el óptimo |
| **NAG (Nesterov)** | Constante | Variante de Momentum; frena antes del óptimo |
| **AdaGrad** | Adaptativo | Alfa distinto por parámetro; puede volverse muy pequeño |
| **RMSProp** | Adaptativo | Media móvil; bueno para situaciones no convexas |
| **Adam** | Adaptativo | Momentum + AdaDelta; **el mejor para la mayoría de casos** |
| **NAdam** | Adaptativo | Adam + Nesterov; versión mejorada |

---

## Tabla Comparativa de Modelos RNA

| | Perceptrón | Backpropagation | Hopfield | CNN |
|--|-----------|----------------|---------|-----|
| **Tipo** | Heteroasociativa | Heteroasociativa | Autoasociativa | Heteroasociativa |
| **Aprendizaje** | Supervisado | Supervisado | No supervisado | Supervisado |
| **Modo** | Offline | Offline | Offline | Offline |
| **Estrategia** | Corrección de error | Delta generalizada + backprop | Hebbiano | Backprop con filtros |
| **Arquitectura** | 1 neurona | 2+ capas | 1 capa | Conv + Lineal |
| **Conexiones** | Hacia adelante | Hacia adelante | Laterales | Hacia adelante (filtros) |
| **Funciones** | Solo lineales | Lineales y no lineales | — | No lineales |
| **Aplicación** | Clasificación simple | Clasificación, predicción | Completar patrones | Imágenes |

---

## Trampas del examen

- Lo único que cambia durante el entrenamiento son los **pesos W** (no funciones, no estructura)
- La RNA **no tiene base de conocimientos** → no es SBC ni SET en el sentido tradicional
- Perceptrón: solo funciones **lineales** (no puede aprender XOR)
- Backprop: requiere funciones **derivables** (usa Sigmoidal)
- Hopfield: **autoasociativa** y **no supervisada** (las otras dos son heteroasociativas y supervisadas)
- Hopfield converge con **2 ciclos iguales consecutivos**
- Los patrones de Hopfield deben ser **ortogonales** (diferir en al menos N/2 componentes)
- CNN: los filtros **se aprenden** durante el entrenamiento (no son fijos)
- El **Pooling NO se aprende** (es fijo, lo elige el diseñador)
- Usar **CrossEntropy** con sigmoidal/softmax; **MSE** con identidad
- La normalización debe aplicarse con los **mismos parámetros** en entrenamiento y producción
- **Mini-Batch** es el método de procesamiento más recomendado
- **Adam** es el optimizador más recomendado para la mayoría de casos

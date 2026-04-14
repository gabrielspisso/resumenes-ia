# 04 v2 — Redes Neuronales Artificiales (desde clases del profesor)

> **Fuente:** Transcripciones de las 15 clases del prof. Pablo Pitel  
> **Cubre:** Introducción → Perceptrón → Backpropagation → Hopfield → CNN → Entrenamiento avanzado

---

## 1. Introducción y ubicación en IA

Las RNA se relacionan con **dos disciplinas de la IA**:
- **Inteligencia Computacional:** por su inspiración biológica (el cerebro)
- **Machine Learning:** por su capacidad de aprender automáticamente de ejemplos

**Una RNA NO posee base de conocimientos** → no tiene relación con los Sistemas Basados en Conocimiento (SBC).  
Todo el conocimiento queda codificado implícitamente en los **valores de los pesos** de las conexiones.

Pueden usarse con fuentes públicas (SI normal) o privadas de un experto (SE).

**Ventajas:**
- **Aprendizaje adaptativo:** aprende casi cualquier tipo de problema
- **Autoorganización:** modifica sus conexiones sola durante el entrenamiento
- **Tolerancia a fallos:** cierta flexibilidad para datos no vistos (con límite)
- **Tiempo real:** una vez entrenada, es muy rápida en producción
- **Portabilidad:** funciona en cualquier hardware/lenguaje

---

## 2. Modelo biológico → Neurona Artificial

### Neurona biológica
- **Dendritas** → interfaz de **entrada**
- **Axón** → interfaz de **salida** (único, se multiplexa en botones opie)
- **Sinapsis:** conexión entre botón opie de una neurona y dendrita de otra
  - **Excitadora (+):** tiende a cargar (activar) la neurona receptora
  - **Inhibidora (-):** tiende a descargar (inhibir) la neurona receptora
  - **Neutra (0):** no afecta el estado de la neurona receptora

Al aprender, lo que se modifica son las **sinapsis** (se vuelven más excitadoras, inhibidoras o neutras).

### Neurona artificial — estructura

```
X0 ──W0──┐
X1 ──W1──┤
...      ├─→ Net_i → A(Net_i) → S[A(Net_i)] = Yi
Xn ──Wn──┘
```

| Elemento | Descripción |
|---------|-------------|
| **Xj** | Valores de entrada (numéricos) |
| **Wji** | Pesos de conexiones (sinapsis); >0 excitadora, =0 neutra, <0 inhibitoria |
| **Entrada neta** | `Net_i = Σ(Wji × Xj)` |
| **Función de activación A()** | Usa Net_i y el umbral θ para determinar si la neurona se activa |
| **Función de salida/transferencia S()** | Determina el valor de salida Yi a partir de A() |
| **Salida Yi** | Única (puede multiplexarse hacia muchas otras neuronas) |

En la práctica se combinan en una única función: `F(Net_i) = Yi`

> **Lo único que cambia durante el entrenamiento son los pesos W. Nunca la función, el umbral (en general) ni la estructura.**

---

## 3. Componentes y estructura de una RNA

### Capas
| Capa | Descripción |
|------|-------------|
| **Entrada** | Recibe información del exterior |
| **Ocultas** (0, 1 o más) | Procesamiento interno; opcionales o no según el modelo |
| **Salida** | Envía resultado al exterior |

> Cantidad de neuronas de entrada y salida = determinado por el problema.  
> Cantidad de neuronas ocultas = depende de la complejidad del problema.

### Tipos de información
| Tipo | Descripción |
|------|-------------|
| **Discreta (binaria)** | Valores 0 o 1 |
| **Continua (real)** | Cualquier valor numérico en algún rango |

### Funciones comunes
- **Activación:** escalón, identidad, lineal mixta, ReLU
- **Salida:** escalón, sigmoidal, gaussiana, tangente hiperbólica (tanh)
- **ReLU:** muy usada actualmente por simplicidad y eficiencia computacional

### Tipo de asociación
| Tipo | Aprendizaje | Uso típico |
|------|------------|-----------|
| **Heteroasociativa** | **Supervisado** — se da entrada + salida deseada | Clasificación, predicción |
| **Autoasociativa** | **No supervisado** — solo entradas | Clustering, completar patrones |

### Topología
| Parámetro | Opciones |
|-----------|---------|
| Cantidad de capas | Monocapa / bicapa / multicapa |
| Neuronas por capa | Depende del problema |
| **Conectividad** | **Total** (cada neurona → todas de la siguiente capa) o **Parcial** (cuando la RAM no alcanza) |
| **Forma de conexión** | Hacia adelante (feedforward) / hacia atrás (retroalimentación, recursiva, lateral) |

> Las conexiones **hacia atrás** generan ciclos que finalizan cuando se cumple un criterio de estabilización.

---

## 4. Reglas de aprendizaje (Estrategias de entrenamiento)

### Clasificación
```
                    ┌── Offline
      Supervisado ──┤   ├── Por corrección de error ← lo que se ve en materia
                    │   ├── Estocástico (al azar, poco usado)
                    │   └── Online → Por refuerzo
                    │
                    └── Offline
    No supervisado ──┤   ├── Hebbiano
                    │   └── Competitivo/cooperativo → Clustering
                    └── Online → Hebbiano / Competitivo
```

| Estrategia | Descripción |
|-----------|-------------|
| **Por corrección de error** | Minimiza el error usando fórmula; ajusta pesos con precisión |
| **Estocástico** | Ajusta pesos al azar; hoy en desuso |
| **Por refuerzo** | Como corrección de error pero en lugar de salida deseada, recibe una valoración (bueno/malo/regular) de la salida |
| **Hebbiano** | Inspirado en cómo aprende el cerebro biológico |
| **Competitivo/cooperativo** | Etapa 1: ordenación global (cooperación); Etapa 2: ajuste fino (competencia) → clustering |

---

## 5. Modelo 1: Perceptrón (1958, Rosenblatt)

**Tipo:** Heteroasociativa · Supervisada · **Offline** · Corrección de error · **Monocapa (1 neurona)**

**Función:** escalón (si activación > 0 → 1, sino → 0)

### Algoritmo de entrenamiento

```
Para cada patrón de entrenamiento:
1. Calcular Net_i = Σ(Wji × Xj)
2. Aplicar función de activación: A = Net_i - umbral
3. Aplicar función escalón → salida generada Yi
4. Comparar Yi con salida deseada Yd
5. Si Yi ≠ Yd → ajustar pesos:
   ΔWj = α × (Yd - Yi) × Xj
   Wj_nuevo = Wj + ΔWj
6. Si se modificaron pesos → volver a probar TODOS los patrones anteriores
7. Repetir hasta que el error sea 0 o aceptable
```

**El coeficiente alfa (α) — tasa de aprendizaje:**
- Valor recomendado: **0.05 a 0.30**
- Alfa pequeño → aprende lento pero no olvida lo anterior
- Alfa grande → aprende rápido pero puede olvidar patrones ya aprendidos

**Otras recomendaciones:**
- Umbral θ: mantenerlo constante (más estable); puede ajustarse como peso si se desea
- Valores de entrada: normalizar en [0, 1]
- Pesos iniciales: entre 0.00 y 0.50

**Limitación crítica:** Solo aprende funciones **linealmente separables**.  
→ No puede aprender la función OR-exclusivo (requeriría 2 rectas).  
→ Por esto fue abandonado hasta los años 80.

---

## 6. Modelo 2: Backpropagation (Multi-Perceptrón)

**Tipo:** Heteroasociativa · Supervisada · **Offline** · Corrección de error · **Multicapa (≥2 capas)**

**Nombre completo:** RNA Multi-Perceptrón con Regla Delta Generalizada o Aprendizaje por Retropropagación del Error.

**Superación del Perceptrón:** combina múltiples neuronas perceptrón → puede aprender funciones **lineales y no lineales**.

**Aplicaciones:** Clasificación de datos, estimación y predicción de resultados.

### Función requerida
Las funciones de cada neurona deben ser **derivables** → se usa **Sigmoidal**.

**Función sigmoidal:** devuelve valores continuos entre 0 y 1.  
Si la salida debe ser discreta → se aplica un **umbral de clasificación** (ej: si salida > 0.5 → 1, sino → 0).

Para valores reales → usar **Gaussiana** o **tangente hiperbólica (tanh)**.

### Entrenamiento: Gradiente Decreciente + Backpropagation

El problema: necesitamos encontrar los valores de pesos que minimicen el error total, pero hay muchos pesos y no sabemos hacia dónde ajustarlos.

**Solución:** el **gradiente negativo** (calculado con la derivada) indica la dirección en que debemos modificar cada peso para acercarnos al óptimo.

```
Para cada patrón:
1. Propagación hacia adelante:
   - Calcular salida de cada neurona (capa por capa, de entrada a salida)
2. Calcular el error:
   - Error = Salida deseada - Salida generada
3. Calcular el gradiente para la neurona de salida:
   δ_salida = derivada_de_la_función × error
4. Propagar el gradiente hacia atrás (backpropagation):
   δ_oculta = derivada_de_la_función × Σ(δ_siguiente × W_conexión)
5. Ajustar todos los pesos:
   W_nuevo = W_viejo + α × δ_neurona × entrada_de_la_conexión
6. Repetir hasta que el error sea aceptable
```

> El gradiente propaga el error hacia atrás **ponderado por la magnitud de las conexiones** → neuronas que contribuyeron más al error reciben un ajuste mayor.

### Recomendaciones de diseño

#### Capa de entrada
- **Valores reales:** una neurona por atributo, función identidad
- **Valores binarios:** una neurona por cada bit; o una neurona por cada valor posible del atributo (one-hot encoding)

#### Capas ocultas
- No hay regla general para cantidad de neuronas ni capas
- **1 capa oculta:** suficiente para la mayoría de problemas
- **2 capas ocultas:** aprende más rápido para la misma cantidad de neuronas
- Más neuronas y capas → mayor capacidad, mayor complejidad, más tiempo de entrenamiento
- Para determinarlas: prueba y corrección manual, o usar Algoritmos Genéticos
- **Funciones:** Sigmoidal para binarios; ReLU es muy usada actualmente; tanh para valores reales

#### Capa de salida
- Neuronas según la cantidad de salidas requeridas
- **Función identidad:** si la salida es un valor real continuo → usar **MSE** para calcular error
- **Función sigmoidal:** si la salida es binaria (0/1) → usar **CrossEntropy** para calcular error
- **Función softmax:** si hay múltiples clases y quiero probabilidades → usar **CrossEntropy**

#### Pesos iniciales
- Recomendados: entre **0 y 0.5** (inicializar al azar dentro de ese rango)

#### Si la red no aprende → probar en este orden:
1. Normalizar datos de entrada y salida
2. Modificar parámetros de aprendizaje (alfa)
3. Cambiar pesos iniciales
4. Cambiar el orden en que se ingresan los patrones
5. Agregar neuronas ocultas y/o capas

---

## 7. Modelo 3: Hopfield

**Tipo:** Autoasociativa · **No supervisada** · Offline · Hebbiano · **Monocapa con conexiones laterales**

**Uso:** Completar valores faltantes de patrones de entrada a partir de patrones ya aprendidos.

### Entrenamiento
1. Para cada patrón `p` (vector fila):  
   `M_p = p^T × p` (producto del vector por su traspuesto)
2. Tachar la diagonal principal (ponerse en 0)
3. La **matriz de pesos total** = suma de todas las matrices `M_p`

### Operación (producción)
1. Ingresar el patrón incompleto
2. La red itera actualizando los valores de cada neurona usando los pesos de la matriz
3. **Criterio de convergencia:** cuando en 2 ciclos consecutivos el resultado es el mismo → la red aprendió / completó el patrón

### Limitaciones
- Los patrones deben ser **ortogonales** entre sí (diferir en al menos N/2 componentes, donde N = número de neuronas)
- Capacidad de almacenamiento limitada (aprox. 0.15 × N patrones)

---

## 8. Modelo 4: Redes Convolucionales (CNN)

> **Tema que NO estaba en el resumen anterior.**

**Tipo:** Heteroasociativa · Supervisada · Offline · Corrección de error (Backpropagation)  
**Inspiración:** Cortex Visual Primario del cerebro humano  
**Uso principal:** Reconocimiento y clasificación de **imágenes**

**Historia:** Surgieron en los 80 pero necesitaban hardware que no existía. Recién en 2012 tomaron notoriedad al ganar el concurso ImageNet con error del 16.4%. Google las usó en 2014 para Google Imágenes.

### ¿Por qué no usar Backpropagation directamente para imágenes?

Una imagen de 200×200 px = 40.000 neuronas de entrada.  
Con 4.000 neuronas ocultas → **160 millones de pesos** → inviable.

**Solución CNN:** reducir parámetros usando:
1. **Conectividad escasa (sparse):** cada neurona oculta solo procesa una región de la imagen
2. **Pesos compartidos (filtros):** todas las regiones usan los **mismos pesos** → los filtros

### Estructura de una capa convolucional

Cada capa convolucional tiene **3 etapas:**

#### Etapa 1: Convolucional (filtros)
- Se define un filtro de tamaño `F×F` (ej: 3×3) — son los pesos de la capa
- El filtro se desliza por la imagen con un paso (**stride**)
- En cada posición: multiplica los píxeles de la región por los pesos → calcula la suma → genera el **feature map**
- Con `k` filtros de `F×F`: la red tiene solo `k × F × F` pesos en esa capa (en vez de millones)

> **Los valores de los filtros se aprenden durante el entrenamiento** (son los pesos que se ajustan con backprop).

#### Etapa 2: Detector (función de activación)
- Se aplica una función no lineal al feature map
- Generalmente se usa **ReLU** (devuelve 0 si negativo, el valor si positivo)
- Permite aprender patrones no lineales

#### Etapa 3: Pooling (reducción)
- Reduce las dimensiones del feature map → simplifica preservando lo importante
- **Max Pooling:** toma el valor máximo de cada región (ej: de un bloque 2×2 → 1 valor)
- **Average Pooling:** toma el valor promedio de cada región
- El pooling es fijo (no se aprende), el ingeniero decide cuál usar
- **En general se usa Max Pooling**

### Arquitectura completa de una CNN

```
Entrada (imagen) 
    → [Capa Convolucional (conv + detector + pooling)] × n
    → Flatten/Reshape (matriz → vector)
    → [Capas Lineales (neuronas tipo backpropagation)] × m
    → Capa de Salida (identidad / sigmoidal / softmax)
```

- **Capas convolucionales:** extraen características de la imagen
- **Flatten:** convierte la salida matricial en vector para las capas lineales
- **Capas lineales:** aprenden a clasificar a partir de las características extraídas
- **Capa de salida con Softmax:** da probabilidad por cada clase posible

### Recomendaciones de diseño CNN
- Los filtros deben **reducirse** a medida que la red se hace más profunda (en potencias de 2 para evitar cuellos de botella)
- Preferir **muchos filtros pequeños** (3×3) sobre pocos filtros grandes (5×5) → aprende más rápido
- Equilibrar ancho (cantidad de filtros) y profundidad (cantidad de capas): más profundidad → menos ancho

---

## 9. Preparación de datos para entrenamiento

### Normalización de datos

**Por qué:** diferentes atributos con escalas muy distintas dificultan el aprendizaje.  
**Objetivo:** llevar todos los atributos a una escala similar (entre [-1,1] o [0,1]).

| Método | Fórmula | Resultado | Cuándo usar |
|--------|---------|-----------|-------------|
| **Standard Scaler** | `(x - media) / desviación_estándar` | Centrado en 0, rango variable | Caso general |
| **MinMax Scaler** | `(x - min) / (max - min)` | Entre 0 y 1 (o -1 y 1 si hay negativos) | Cuando el rango es conocido |
| **Robust Scaler** | Ignora outliers al calcular estadísticas | Más robusto ante valores extremos | Cuando hay outliers |

> **Regla de oro:** Aplicar la **misma fórmula y los mismos parámetros** a los datos de entrenamiento, validación, prueba Y producción. Si no, la red dará resultados incorrectos en producción.

### Separación de datos

**Proporciones recomendadas:**
- 70% entrenamiento + validación / 30% prueba
- 80% / 20% (con muchos datos)
- 90% / 10% (con millones de registros)

**Dentro del 70% de entrenamiento+validación:**
- 80% / 20% para entrenamiento vs validación
- O 90% / 10% cuando hay pocos datos

**Técnicas de muestreo:**
- **Muestreo estratificado (recomendado):** mantiene la proporción de clases en cada conjunto
- **Muestreo simple:** aleatorio; puede generar desbalance de clases

**Dejar una afuera (leave-one-out):** cuando se tiene muy poca cantidad de datos — cada época usa un ejemplo distinto como validación.

### Data Augmentation (para imágenes)

Cuando hay pocos datos de imagen → generar variantes artificiales:
- Volteo horizontal (y vertical si tiene sentido)
- Rotación, zoom, recorte
- Traslación (mover el objeto en la imagen)
- Cambios de brillo/contraste
- Agregar ruido gaussiano

> Se hace **una vez** antes del entrenamiento; luego se usan todos los datos aumentados.

### Preparación de imágenes
- Normalizar tamaño a un estándar fijo (ej: 200×200)
- Color (3 canales RGB) o escala de grises (1 canal)
- Normalizar valores de píxeles: dividir por 255 → rango [0,1]

---

## 10. Parámetros de entrenamiento

### Tipos de procesamiento de datos

| Método | Descripción | Cuándo ajusta pesos | Problema |
|--------|-------------|---------------------|---------|
| **Ejemplo por ejemplo** | Procesa un ejemplo → ajusta pesos → siguiente | En cada ejemplo | Lento con muchos datos |
| **Full Batch** | Procesa todos los ejemplos → calcula error promedio → ajusta | Una vez por época | Mucha memoria; ajuste poco preciso |
| **Estocástico** | Elige 1 ejemplo al azar por época → ajusta | En cada ejemplo elegido | Necesita muchas épocas para converger |
| **Mini-Batch** ✓ **Recomendado** | Procesa un lote pequeño de N ejemplos → calcula error del lote → ajusta | Por cada lote | Equilibra velocidad y calidad |

**Términos:**
- **Step/Paso:** procesar un ejemplo (o un mini-batch) → calcular error → ajustar pesos
- **Época:** completar el procesamiento de todo el conjunto de datos de entrenamiento

### Épocas y over/underfitting

| Situación | Descripción |
|----------|-------------|
| **Underfitting** | Pocas épocas → la red no terminó de aprender → error de entrenamiento alto |
| **Overfitting** | Demasiadas épocas → la red memoriza los datos → error de entrenamiento bajo pero error de validación/prueba alto |
| **Early Stopping** | Finalización automática cuando el error de validación empieza a subir mientras el de entrenamiento sigue bajando |

> **Early stopping** es útil pero no perfecto: puede finalizar demasiado pronto. Siempre verificar con datos de prueba.

### Fórmulas de error (Loss function)

| Capa de salida | Fórmula de error recomendada |
|---------------|------------------------------|
| **Identidad** (salida continua) | **MSE** (Error Cuadrático Medio) |
| **Sigmoidal** (salida binaria) | **CrossEntropy** (Entropía Cruzada) |
| **Softmax** (múltiples clases) | **CrossEntropy** (Entropía Cruzada) |

> Si usás la fórmula incorrecta, el error puede quedar constante y la red no aprende.

### Tasa de aprendizaje (alfa / learning rate)

- Rango recomendado: **0.01 a 0.40**
- Alfa muy grande → inestabilidad, esquiva el óptimo
- Alfa muy pequeño → aprendizaje extremadamente lento
- Se puede usar **alfa adaptativo** (que va cambiando durante el entrenamiento)

### Algoritmos de optimización

Todos son variaciones del **Gradiente Decreciente (SGD)**:

| Algoritmo | Alfa | Descripción |
|-----------|------|-------------|
| **SGD** (Stochastic Gradient Descent) | Constante | Base; más lento pero converge bien |
| **Momentum** | Constante | Considera gradientes anteriores; evita oscilaciones; puede sobrepasar el óptimo |
| **NAG** (Nesterov) | Constante | Variante de Momentum; frena antes de llegar al óptimo |
| **AdaGrad** | Adaptativo | Alfa distinto por parámetro; puede volverse demasiado pequeño |
| **AdaDelta** | Adaptativo | Soluciona el problema de AdaGrad con promedio ponderado de gradientes anteriores |
| **RMSProp** | Adaptativo | Similar a AdaDelta con media móvil; funciona bien para situaciones no convexas |
| **Adam** | Adaptativo | Combina Momentum + AdaDelta + RMSProp; **funciona bien en la mayoría de casos** |
| **NAdam** | Adaptativo | Adam + Nesterov; versión mejorada de Adam |

> **En general Adam es la mejor opción**, pero a veces para clasificación de imágenes SGD puro converge mejor.

---

## 11. Tabla comparativa de modelos RNA

| Característica | Perceptrón | Backpropagation | Hopfield | CNN |
|---------------|-----------|----------------|---------|-----|
| **Tipo** | Heteroasociativa | Heteroasociativa | Autoasociativa | Heteroasociativa |
| **Aprendizaje** | Supervisado | Supervisado | No supervisado | Supervisado |
| **Modo** | Offline | Offline | Offline | Offline |
| **Estrategia** | Corrección de error | Corrección de error (delta generalizada + backprop) | Hebbiano | Corrección de error (backprop) |
| **Arquitectura** | 1 neurona | 2+ capas | 1 capa + conexiones laterales | Conv + Lineal |
| **Conexiones** | Hacia adelante | Hacia adelante | Laterales | Hacia adelante (con filtros) |
| **Iteraciones** | Varias por patrón | Varias por patrón | 1 por patrón (hasta convergencia) | Varias por patrón |
| **Salida** | Discreta | Discreta o continua | Vector | Discreta (generalmente) |
| **Funciona con** | Solo funciones lineales | Lineales y no lineales | Completar patrones | Imágenes y datos matriciales |
| **Aplicación típica** | Clasificación simple | Clasificación, predicción | Memoria asociativa | Reconocimiento de imágenes |

---

## Resumen clave para el final

1. **Lo único que cambia durante el entrenamiento son los pesos W** (no funciones, no estructura).
2. **Perceptrón:** 1 neurona, solo lineal, 1958. Alfa 0.05–0.30. Ajuste por `α × error × entrada`.
3. **Backpropagation:** multicapa, lineal y no lineal. Usa gradiente decreciente + error propagado hacia atrás. Función sigmoidal (derivable).
4. **Hopfield:** autoasociativa, aprende con `M = p^T × p` (tachar diagonal), converge cuando 2 ciclos iguales.
5. **CNN:** para imágenes. Usa filtros (pesos compartidos) → reduce parámetros de millones a decenas. Etapas: convolución + detector (ReLU) + pooling. Luego capas lineales.
6. **Normalización:** misma fórmula y parámetros en entrenamiento, validación, prueba Y producción.
7. **Mini-batch:** el método de procesamiento más eficiente para grandes volúmenes de datos.
8. **Underfitting:** pocas épocas. **Overfitting:** demasiadas épocas. **Early stopping** ayuda a controlarlo.
9. **Fórmula de error:** MSE para salida continua (identidad); CrossEntropy para sigmoidal/softmax.
10. **Algoritmo de optimización:** Adam funciona bien en la mayoría de casos.

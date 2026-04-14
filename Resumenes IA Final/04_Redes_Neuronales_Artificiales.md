# 04 — Redes Neuronales Artificiales (RNA)

> **Playlist:** Redes Neuronales Artificiales  
> **Objetivo:** Sistemas de cómputo inspirados en el cerebro biológico que aprenden de ejemplos.

---

## ¿Qué son?

Evolución de un sistema de cómputo basado en modelo biológico. Formada por **elementos simples de proceso (neuronas) interconectados** que operan en paralelo.

**Relación con otras ramas:**
- **Inteligencia Computacional:** inspiración biológica
- **Machine Learning:** aprenden automáticamente de ejemplos

**Ventajas:**
- **Aprendizaje adaptativo:** aprenden casi cualquier tipo de problema
- **Autoorganización:** cambian las conexiones durante el entrenamiento
- **Tolerancia a fallos:** cierta flexibilidad ante datos nuevos
- **Operación en tiempo real**

---

## La Neurona Artificial

**Proceso:**
1. Entradas `Xj` (valores numéricos)
2. × Pesos `Wji` (sinapsis: positivo = excitadora, 0 = neutra, negativo = inhibitoria)
3. **Entrada neta:** `Net_i = Σ(Wji × Xj)`
4. **Función de activación** A(Net_i): determina si la neurona se activa (usa el umbral)
5. **Función de salida/transferencia** S[A(Net_i)] = Yi

En la práctica se combina: `F(Net_i) = Yi` (función única)

**La salida es única** pero puede ir a múltiples neuronas.

---

## Componentes de una RNA

| Componente | Descripción |
|-----------|-------------|
| **Capas** | Entrada / Ocultas (procesamiento) / Salida |
| **Conexión Wij** | >0 excitadora, =0 neutra, <0 inhibitoria |

### Funciones de activación comunes:
- Escalón, Identidad, Lineal mixta, ReLU

### Funciones de salida comunes:
- Escalón, Mixta, **Sigmoidal** (la más usada), Gaussiana

---

## Parámetros del Modelo RNA

### Tipo de información:
- **Discreta:** binarios (0/1)
- **Continua:** reales

### Tipo de asociación:
| Tipo | Aprendizaje | Descripción |
|------|------------|-------------|
| **Heteroasociativa** | Supervisado | Se da patrón de entrada + salida deseada |
| **Autoasociativa** | No supervisado | La red aprende sola a identificar la salida |

### Topología:
- **Capas:** monocapa o multicapa
- **Conectividad:** total o parcial
- **Conexiones:** hacia adelante (feedforward) / hacia atrás (retroalimentación)

### Reglas de aprendizaje:
| Combinación | Método | Uso |
|------------|-------|-----|
| Supervisado offline | Corrección de error | Clasificar / predecir |
| Supervisado offline | Estocástico | Ajuste al azar (poco usado hoy) |
| Supervisado online | Por refuerzo | Solo valoración de la salida |
| No supervisado off/online | Hebbiano | — |
| No supervisado off/online | Competitivo/cooperativo | Clustering (ordenación global + ajuste fino) |

> **En RNA solo se modifican los pesos de las conexiones**

---

## Modelo 1: Perceptrón

**Tipo:** Heteroasociativa, supervisado, **offline**, corrección de errores. **Monocapa** (1 sola neurona).

**Proceso de entrenamiento:**
- Se repite (aprendizaje por repetición)
- El coeficiente **alfa** evita que olvide lo aprendido (aprendizaje más lento pero más estable)

**Recomendaciones:**
- Umbral: mantenerlo constante para mayor estabilidad
- Valores: trabajar solo con binarios, normalizar en [0;1]
- **Alfa:** entre 0.05 y 0.30
- Pesos iniciales: entre 0.00 y 0.50

**Desventaja:** Solo aprende funciones **lineales**. No puede aprender funciones no lineales.

---

## Modelo 2: Multi-Perceptrón (Backpropagation)

**Nombre completo:** RNA con regla delta generalizada / gradiente decreciente / retropropagación del error.

**Tipo:** Heteroasociativa, supervisado, **offline**, corrección de errores. **Multicapa** (≥2 capas).

**Aplicaciones:** Clasificación de datos, estimación/predicción.

**Entrenamiento:**
- Si hay error, se propaga hacia atrás (**backpropagation**)
- Usa el gradiente del error (delta_e)
- Requiere funciones **derivables** → se usa Sigmoidal

**Parámetros:**
- Función de salida (Sigmoidal para binarios, Gaussiana o tanh para reales)
- Factor de aprendizaje **alfa**
- Umbrales de neuronas
- Pesos iniciales

**Recomendaciones:**
- Alfa entre 0.05 y 0.30 (más grande → parálisis/inestabilidad; más pequeño → muy lento)
- Usar tasa **adaptativa decreciente** para evitar máximos locales
- Pesos iniciales entre 0 y 0.5
- Si no aprende → intentar: normalizar datos, modificar parámetros, cambiar pesos iniciales, cambiar orden de patrones, agregar neuronas/capas

**Topología (neuronas ocultas):**
- 1 capa oculta: suficiente para la mayoría de problemas
- 2 capas ocultas: aprende más rápido
- No hay regla general → prueba y corrección, o usar AG

**Ciclos de entrenamiento:**
- Pocos → aprendizaje incompleto
- Demasiados → **sobreaprendizaje**
- Mejor: adaptativo según error de entrenamiento y validación

---

## Modelo 3: RNA Hopfield

**Tipo:** Autoasociativa, **no supervisado**, offline, hebbiano. **Monocapa** con **conexiones laterales**.

**Uso:** Completar patrones incompletos a partir de patrones ya aprendidos.

**Entrenamiento:**
1. Para cada patrón: calcular `vector × vector_transpuesto` → tachar diagonal → matriz de pesos del patrón
2. Sumar todas las matrices de pesos de cada patrón → matriz de pesos total de la red

**Convergencia:** La red aprendió cuando en **2 ciclos seguidos** se obtiene el mismo resultado.

**Limitaciones:**
- Los patrones a memorizar deben ser **ortogonales** (diferentes en al menos N/2 componentes)
- Para N neuronas, capacidad limitada de almacenamiento

---

## Comparación de Modelos RNA

| Característica | Perceptrón | Backpropagation | Hopfield |
|---------------|-----------|----------------|---------|
| **Entrenamiento** | Supervisado | Supervisado | No supervisado |
| **Estrategia** | Corrección de error (delta) | Corrección de error (delta generalizada) | Hebbiano |
| **Modo** | Offline | Offline | Offline |
| **Arquitectura** | 1 capa, 1 neurona | 2+ capas | 1 capa |
| **Tipo** | Heteroasociativa | Heteroasociativa | Autoasociativa |
| **Conexiones** | Hacia adelante | Hacia adelante | Laterales |
| **Iteraciones** | Varias (por patrón) | Varias (por patrón) | Una (por patrón) |
| **Salida** | Discreta | Discreta o continua | Vector |
| **Aplicación** | Funciones lineales | Lineales y no lineales | Completar patrones |

---

## Métricas para Evaluar RNA

- **Matriz de confusión:** medir convergencia (VP, VN, FP, FN)
- **Exactitud, Precisión, Recuperación, F1 Score** (ver tema 01)

---

## Resumen clave para el final

1. RNA = neuronas artificiales interconectadas que aprenden de ejemplos.
2. **Perceptrón:** monocapa, lineal, supervisado offline.
3. **Backpropagation:** multicapa, lineal y no lineal, supervisado offline, propaga error hacia atrás.
4. **Hopfield:** autoasociativa, no supervisada, completa patrones incompletos.
5. Solo se modifican los **pesos** de las conexiones durante el entrenamiento.
6. **Sobreaprendizaje** = demasiados ciclos → el modelo memoriza en vez de generalizar.
7. Alfa muy alto → parálisis/inestabilidad; muy bajo → lentitud.

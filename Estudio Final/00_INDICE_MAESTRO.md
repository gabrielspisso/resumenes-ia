# Inteligencia Artificial — Índice Maestro para el Final

> **9 archivos**, uno por playlist de YouTube. Cada archivo tiene el contenido condensado sin información innecesaria.  
> Todo lo que necesitás saber para aprobar el final, sin humo.

---

## Archivos de estudio

| # | Tema | Archivo | Conceptos clave |
|---|------|---------|----------------|
| 01 | Conceptos Iniciales | `01_Conceptos_Iniciales.md` | IA, SI, SE, SBC, ML, TDIDT, métricas |
| 02 | Análisis de Protocolos | `02_Analisis_de_Protocolos.md` | Educción, CCV, reglas SI-ENTONCES, 4 etapas |
| 03 | Algoritmos Genéticos | `03_Algoritmos_Geneticos.md` | Cromosoma, fitness, GPI, selección, cruzamiento, mutación |
| 04 | Redes Neuronales | `04_Redes_Neuronales.md` | Perceptrón, Backprop, Hopfield, CNN, normalización, overfitting |
| 05 | Emparrillado | `05_Emparrillado.md` | Parrilla, distancias, árboles, relaciones |
| 06 | Métodos de Búsqueda | `06_Metodos_de_Busqueda.md` | BFS, DFS, heurísticas, A*, Beam Search |
| 07 | Lógica Difusa | `07_Logica_Difusa.md` | Conjuntos difusos, operadores, Mamdani, Takagi-Sugeno |
| 08 | Implementación de SI | `08_Implementacion_SI.md` | Fases, educción, selección tecnología, pipelines |
| 09 | PNL | `09_PNL.md` | Tokenización, normalización, NLU, NLG, n-gram |

---

## Mapa de tecnologías de IA

```
IA
├── IA Tradicional
│   ├── SBC (Sistema Basado en Conocimientos)  ← fuentes públicas
│   └── SET (Sistema Experto Tradicional)       ← fuentes privadas (+públicas)
│
├── Machine Learning
│   ├── Algoritmos de inducción (TDIDT) → reglas de clasificación
│   ├── Algoritmos de regresión → fórmula numérica
│   └── RNA (también en IC)
│
└── Inteligencia Computacional (IC)
    ├── Algoritmos Genéticos → optimización
    ├── RNA (Perceptrón, Backpropagation, Hopfield, CNN)
    └── Lógica Difusa (también en ML y IA Trad.)
```

---

## Qué tecnología usar según el problema

| Tengo... | Uso... |
|----------|--------|
| Datos + quiero clasificar | Inducción (TDIDT) o RNA supervisada |
| Datos + quiero predecir número | Regresión o RNA supervisada |
| Datos sin etiquetas + quiero agrupar | Clustering / RNA no supervisada / Hopfield |
| Reglas de un experto, sin datos | SBC / SET (IA Tradicional) |
| Solo heurísticas, sin datos ni reglas | Algoritmos Genéticos |
| Datos imprecisos / vagos | Lógica Difusa |
| Texto en lenguaje natural | PNL |

---

## Técnicas de Educción del Conocimiento

| Técnica | Cuándo usarla | Qué extrae |
|---------|--------------|-----------|
| **Análisis de Protocolos** | Conocimiento implícito del experto | Reglas de razonamiento (SI-ENTONCES) + declarativo |
| **Emparrillado** | Cómo el experto clasifica elementos | Similitudes/diferencias entre elementos y sus características |
| **Entrevistas / Brainstorming** | Conocimiento explícito general | Requerimientos y contexto del dominio |

---

## Comparativa Completa de RNA

| | Perceptrón | Backpropagation | Hopfield | CNN |
|-|-----------|----------------|---------|-----|
| **Tipo** | Heteroasociativa | Heteroasociativa | **Autoasociativa** | Heteroasociativa |
| **Aprendizaje** | Supervisado | Supervisado | **No supervisado** | Supervisado |
| **Modo** | Offline | Offline | Offline | Offline |
| **Estrategia** | Corrección de error | Delta generalizada + backprop | **Hebbiano** | Backprop con filtros |
| **Arquitectura** | 1 neurona | 2+ capas | 1 capa + lat. | Conv + Lineal |
| **Conexiones** | → Adelante | → Adelante | ↔ Laterales | → Adelante (filtros) |
| **Funciones** | **Solo lineales** | Lineales + no lineales | — | No lineales |
| **Aplicación** | Clasificación simple | Clasificación, predicción | Completar patrones | Imágenes |
| **Año** | 1958 | — | — | 2012 (popularización) |

---

## Comparativa Métodos de Búsqueda

### Sin heurística

| Método | Estructura | Garantiza solución | Encuentra todas | Memoria |
|--------|-----------|-------------------|----------------|---------|
| Amplitud (BFS) | Cola FIFO | **Sí** | Sí | Alta |
| Profundidad (DFS) | Pila LIFO | **No óptima** | No | Baja |
| Generación y Prueba | Pila LIFO | **Sí (todas)** | Sí | Baja |
| Bidireccional | Cola (al menos 1) | Sí | No | Media |

### Con heurística

| Método | Retroceso | Garantiza solución | Criterio |
|--------|----------|--------------------|---------|
| Escalada simple | **No** | **No** | Primer hijo > padre |
| Escalada máx. pendiente | **No** | **No** | Mejor hijo > padre |
| Primero el mejor | **Sí** | **Sí** | Mejor nodo de LNA |
| Beam Search | Depende de N | **No** | Mejor N nodos de LNA |
| A* | **Sí** | **Sí (óptima)** | h(n) + g(n) en LNA |

---

## Comparativa Modelos Difusos

| Aspecto | Mamdani | Takagi-Sugeno |
|---------|---------|--------------|
| **Complejidad** | Más simple | Más complejo |
| **Reglas** | Más reglas necesarias | Menos reglas |
| **Consecuente** | Conjunto difuso | Función lineal |
| **Defuzzificación** | Centro de masa / Promedio del máximo | Media ponderada directa |
| **Mejor para** | Problemas simples | Problemas no lineales |

---

## Métricas de Evaluación ML

| Métrica | Fórmula | Qué mide |
|---------|---------|---------|
| **Exactitud** | (VP+VN)/(VP+FP+VN+FN) | % correctos total |
| **Precisión** | VP/(VP+FP) | De los que predije positivos, ¿cuántos lo son? |
| **Recall** | VP/(VP+FN) | De los positivos reales, ¿cuántos encontré? |
| **F1** | 2×P×R/(P+R) | Balance precisión/recall |
| **Error absoluto** | \|real - estimado\| | Para regresión |
| **Error relativo** | \|real - estimado\|/real | Para regresión (%) |

**Cuándo usar:** Precisión cuando FP es costoso (spam). Recall cuando FN es costoso (enfermedades). F1 cuando se necesita balance.

---

## Operadores de Selección AG

| Método | Ventaja | Desventaja |
|--------|---------|-----------|
| Torneo | Buena solución garantizada | Puede perder al 2do mejor |
| Ranking | Simple | Convergencia prematura |
| Ruleta simple | Todos tienen chance | Puede seleccionar solo malos |
| Ruleta s/nro. esperado | Más equitativa y completa | Más compleja |

---

## Comparativa Procesamiento de Datos de RNA

| Método | Ajuste de pesos | Recomendado |
|--------|----------------|-------------|
| Ejemplo por ejemplo | Por ejemplo | No (lento) |
| Full Batch | Por época | No (poco preciso) |
| Estocástico | Por ejemplo aleatorio | No (necesita muchas épocas) |
| **Mini-Batch** | Por lote N | **Sí** |

---

## Optimizadores RNA

| Algoritmo | Alfa | Cuándo usar |
|-----------|------|------------|
| SGD | Constante | Base, predecible |
| Momentum | Constante | Evitar oscilaciones |
| NAG | Constante | Mejor que Momentum |
| AdaGrad | Adaptativo | Cuidado: puede volverse muy pequeño |
| RMSProp | Adaptativo | Bueno para no-convexos |
| **Adam** | Adaptativo | **La mayoría de casos** |
| NAdam | Adaptativo | Adam + Nesterov (mejorado) |

---

## Fórmulas de Error RNA

| Capa de salida | Loss | Cuándo |
|---------------|------|--------|
| **Identidad** | MSE | Salida continua / regresión |
| **Sigmoidal** | CrossEntropy | Salida binaria (0/1) |
| **Softmax** | CrossEntropy | Múltiples clases |

---

## Etapas del Análisis de Protocolos

| Etapa | Qué se hace | Resultado |
|-------|-------------|-----------|
| **1. Grabación** | Experto piensa en voz alta | Audio/video |
| **2. Transcripción** | Segmentar en frases numeradas | Protocolo escrito |
| **3. Codificación** | Tabla CCV + búsqueda + sinónimos/metacom./incertidumbres | Tabla CCV, estados, operadores |
| **4. Interpretación** | Reglas SI-ENTONCES en pseudocódigo | Reglas del sistema |

---

## Etapas del Emparrillado

| Etapa | Resultado |
|-------|-----------|
| 1. Identificar elementos | Lista de elementos homogéneos |
| 2. Identificar características | Características bipolares |
| 3. Diseñar parrilla | Matriz elementos × características |
| 4. Formalizar | Árbol de elementos + árbol de características |
| 5. Interpretar | Red de relaciones entre características |

---

## Tipos de Parrilla

| Tipo | Escala | Empates |
|------|--------|---------|
| Dicotómica | {0,1} | N/A |
| Clasificatoria | [1,n] n=elementos | **No** |
| Evaluativa | [1,n] n=definida por experto | **Sí** |

---

## Fases de Implementación de un SI

| Fase | Actividades clave |
|------|-----------------|
| 1. Definición del problema | Elicitar, comprender, formalizar requerimientos |
| 2. Datos | Recolección, estudio, integración, limpieza, selección |
| 3. Selección de tecnología | ML / IA Tradicional / IC según el problema |
| 4. Construcción del modelo | Específica a cada tecnología |
| 5. Aplicación | Pipelines, integración con SW tradicional |
| 6. Instalación y mantenimiento | Monitoreo, mantenimiento perfectivo |

---

## Normalización en RNA

| Método | Fórmula | Cuándo |
|--------|---------|--------|
| Standard Scaler | (x - media) / desv_estándar | Caso general |
| MinMax Scaler | (x - min) / (max - min) → [0,1] | Rango conocido |
| Robust Scaler | Ignora outliers | Con valores extremos |

> **Regla de oro:** misma fórmula y mismos parámetros en entrenamiento, validación, prueba Y producción.

---

## Trampas frecuentes del examen

- RNA **no tiene base de conocimientos** → no es SBC
- Hopfield es la única RNA **autoasociativa** y **no supervisada**
- Los filtros de CNN **se aprenden**; el pooling **no se aprende**
- La mutación en AG puede **activarse pero no ejecutarse**
- Los sinónimos en AP **no tienen características** ni **relaciones** entre sí
- En el emparrillado, solo se relacionan características **del mismo grupo**
- La función de pertenencia difusa **no es una probabilidad**
- Escalada (simple y máxima pendiente) **no tiene retroceso** → puede quedar en máximo local
- Primero el Mejor y A* **siempre encuentran solución** (si existe)
- SW Inteligente se implementa de forma **declarativa** (no algorítmica)
- El mantenimiento de un SI es **perfectivo**
- La lematización da palabras semánticas válidas ("correr"); el stemming da raíces ("corr")

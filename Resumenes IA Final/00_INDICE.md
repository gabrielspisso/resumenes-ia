# Inteligencia Artificial — Índice de Estudio para el Final

> **9 archivos**, uno por playlist de YouTube. Cada archivo tiene el contenido condensado sin información innecesaria.

---

## Archivos de estudio

| # | Tema | Archivo | Conceptos clave |
|---|------|---------|----------------|
| 01 | Conceptos Iniciales | `01_Conceptos_Iniciales.md` | IA, SI, SE, ML, TDIDT, métricas |
| 02 | Análisis de Protocolos | `02_Analisis_de_Protocolos.md` | Educción, CCV, reglas SI-ENTONCES |
| 03 | Algoritmos Genéticos | `03_Algoritmos_Geneticos.md` | Cromosoma, fitness, GPI, selección, cruzamiento, mutación |
| 04 | Redes Neuronales | `04_Redes_Neuronales_Artificiales.md` | Perceptrón, Backpropagation, Hopfield |
| 05 | Emparrillado | `05_Emparrillado.md` | Parrilla, distancias, árboles, relaciones |
| 06 | Métodos de Búsqueda | `06_Metodos_de_Busqueda.md` | BFS, DFS, heurísticas, A*, Beam Search |
| 07 | Lógica Difusa | `07_Logica_Difusa.md` | Conjuntos difusos, operadores, Mamdani, Takagi-Sugeno |
| 08 | Implementación de SI | `08_Implementacion_SI.md` | Fases, educción, selección tecnología, pipeline |
| 09 | PNL | `09_PNL_Procesamiento_Lenguaje_Natural.md` | Tokenización, normalización, NLU, NLG, ML en NLP |

---

## Mapa de tecnologías de IA

```
IA
├── IA Tradicional
│   ├── SBC (Sistema Basado en Conocimientos)  ← fuentes públicas
│   └── SET (Sistema Experto Tradicional)       ← fuentes privadas
│
├── Machine Learning
│   ├── Algoritmos de inducción (TDIDT) → reglas de clasificación
│   ├── Algoritmos de regresión → fórmula numérica
│   └── Redes Neuronales (también en IC)
│
└── Inteligencia Computacional
    ├── Algoritmos Genéticos → optimización
    ├── RNA (Perceptrón, Backpropagation, Hopfield)
    └── Lógica Difusa (también en ML y IA Trad.)
```

---

## Qué técnica usar según la situación

| Tengo... | Uso... |
|----------|--------|
| Datos + quiero clasificar | Inducción (TDIDT) o RNA supervisada |
| Datos + quiero predecir número | Regresión o RNA |
| Datos sin etiquetas + quiero agrupar | Clustering / RNA no supervisada / Hopfield |
| Reglas de un experto, sin datos | SBC / SET (IA Tradicional) |
| Solo heurísticas, sin datos ni reglas | Algoritmos Genéticos |
| Datos imprecisos / vagos | Lógica Difusa |
| Texto en lenguaje natural | PNL (NLU / NLG) |

---

## Técnicas de educción del conocimiento

| Técnica | Cuándo usarla | Qué extrae |
|---------|--------------|-----------|
| **Análisis de Protocolos** | Conocimiento implícito del experto | Reglas de razonamiento (SI-ENTONCES) |
| **Emparrillado** | Cómo el experto clasifica elementos | Similitudes/diferencias entre elementos, relaciones entre características |

---

## Resumen de métricas ML

| Métrica | Fórmula | Qué mide |
|---------|---------|---------|
| Exactitud | (VP+VN)/(VP+FP+VN+FN) | % correctos total |
| Precisión | VP/(VP+FP) | De los que predije positivos, ¿cuántos lo son? |
| Recall | VP/(VP+FN) | De los positivos reales, ¿cuántos encontré? |
| F1 | 2×P×R/(P+R) | Balance precisión/recall |
| Error absoluto | \|real-estimado\| | Para regresión |
| Error relativo | \|real-estimado\|/real | Para regresión |

---

## Comparativa RNA

| | Perceptrón | Backpropagation | Hopfield |
|-|-----------|----------------|---------|
| Capas | 1 neurona | 2+ capas | 1 capa |
| Tipo | Heteroasociativa | Heteroasociativa | Autoasociativa |
| Aprendizaje | Supervisado | Supervisado | No supervisado |
| Modo | Offline | Offline | Offline |
| Estrategia | Corrección de error | Retropropagación (delta generalizada) | Hebbiano |
| Funciones | Solo lineales | Lineales y no lineales | Completar patrones |

---

## Comparativa Métodos de Búsqueda

| Método | Heurística | Retroceso | Garantiza solución |
|--------|-----------|----------|--------------------|
| BFS (amplitud) | No | Sí | Sí |
| DFS (profundidad) | No | Parcial | No (no óptima) |
| Generación y prueba | No | Sí | Sí (todos) |
| Escalada simple | Sí | No | No |
| Escalada máx. pendiente | Sí | No | No |
| Primero el mejor | Sí | Sí | Sí |
| Beam Search | Sí | Depende | No |
| A* | Sí | Sí | Sí (óptima) |

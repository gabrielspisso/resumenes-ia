# 01 — Conceptos Iniciales de IA

> **Playlist:** Conceptos Iniciales  
> Fuente: Clase 1, Clase 2, Para el Coloquio

---

## Inteligencia Artificial

**Definición:** Rama de las ciencias computacionales que estudia modelos de cómputo (tecnologías, arquitecturas) para desarrollar software capaz de realizar actividades propias de los seres humanos: razonamiento, conducta y aprendizaje.

**Disciplinas:** IA Tradicional, Inteligencia Computacional, Machine Learning, Visión Artificial, PNL, Big Data & Data Mining.

**Historia clave:**
- 1956: Conferencia de Dartmouth — primera presentación formal del término "IA"
- 1970-1980: Primer invierno de la IA
- 1980-1990: Ingeniería del Conocimiento (INCO), sistemas basados en conocimiento
- 1990-Mid 1990: Segundo invierno
- 1996: Deep Blue vence a Kasparov en ajedrez
- 1996-presente: Redes neuronales, Big Data, Deep Learning

**Enseñanzas de los inviernos:** La IA requiere equipamiento convencional, debe soportar datos erróneos, y los algoritmos deben estar en lenguajes flexibles.

---

## Sistemas Inteligentes (SI)

**Definición:** Artefacto con comportamiento inteligente que resulta de combinar disciplinas de IA para resolver problemas de dominios complejos.

**Comportamiento inteligente:**
- Racional: toma decisiones consistentes con su objetivo
- No omnisciente: no tiene todos los conocimientos ni datos
- No infalible: no siempre es exitoso
- Puede aprender: mejora durante su uso
- Flexible y robusto: soporta cambios del dominio

**Dominio complejo:** al menos una de estas condiciones:
- El problema no se entiende completamente
- No se pueden anticipar todas las situaciones futuras
- Las posibles soluciones son demasiado numerosas para búsqueda exhaustiva
- Un modelo tradicional requeriría simplificación que lo vuelve inútil

**Diferencia clave:** SW Tradicional: dato → noticia. Sistema Inteligente: dato → conocimiento (significado + utilidad dentro del dominio).

---

## Tipos de SI según fuente de conocimiento

| Fuente | Tipo |
|--------|------|
| Pública (libros, manuales) | Sistema Basado en Conocimientos (SBC) |
| Privada (mente del experto) | Sistema Experto (SE) |
| Ambas | SE puede usar ambas |

> **Regla:** Un SI no siempre es un SE, pero un SE **siempre** es un SI.

---

## Sistema Experto Tradicional (SET)

Intenta emular parte del comportamiento de un experto para resolver tareas en un dominio acotado.

**Arquitectura:**
- **Base de conocimientos:** hechos + reglas del dominio
- **Base de datos:** almacena datos del problema actual (temporal)
- **Motor de inferencias:** activa reglas según BD y Memoria de Trabajo
- **Memoria de trabajo:** registro de lo que va aplicando el motor
- **Trazador de consultas:** pide información adicional al usuario
- **Trazador de explicaciones:** justifica el resultado al usuario
- **Manejador de comunicaciones:** interfaz E/S

---

## Sistema Basado en Conocimientos (SBC)

- Conocimiento explícito en Base de Conocimientos
- Fuentes públicas (+ puede usar privadas)
- Arquitectura simplificada: Base de conocimientos + Motor de inferencias + Interfaz E/S

---

## IA Tradicional vs Inteligencia Computacional

| | IA Tradicional (SBC/SET) | Inteligencia Computacional |
|--|--------------------------|---------------------------|
| Conocimiento | Explícito (visible) | Implícito (en pesos/estructura) |
| Base de conocimientos | Sí | No |
| Ejemplos | SET, SBC, Lógica Difusa | RNA, Algoritmos Genéticos |
| Inspiración | Razonamiento simbólico | Biológica |

**IC incluye:** RNA (neuronas), Computación Evolutiva (Darwin), Inteligencia de Enjambre (insectos buscando alimento), Sistemas Inmunológicos Artificiales.

---

## Machine Learning

**Definición:** Subcampo que busca algoritmos capaces de generar conocimiento a partir de información no estructurada suministrada en forma de ejemplos.

**Flujo:** Datos → Algoritmo → Modelo (Sistema Inteligente)

**Estrategias de aprendizaje:**

| Estrategia | Qué recibe | Para qué |
|-----------|-----------|---------|
| **Supervisado** | Ejemplos + salida deseada | Identificar dentro de un grupo acotado de salidas |
| **No supervisado** | Solo ejemplos | Agrupar por categorías que el algoritmo detecta |

**Tipos de entrenamiento:**

| Tipo | Descripción |
|------|-------------|
| **Offline (estático)** | Fase de entrenamiento; luego en producción no aprende más |
| **Online (dinámico)** | Puede seguir aprendiendo en producción (necesita monitoreo) |

**Algoritmos de ML:** Clustering, Inducción, Regresión, Bayes, RNA.

---

## Algoritmos de Inducción (TDIDT)

**TDIDT = Top Down Induction Decision Trees**

- Supervisado y Offline
- Genera un árbol de decisión a partir de datos tabulares
- **Atributo objetivo:** columna que queremos predecir
- **Resultado:** árbol → reglas SI-ENTONCES

**Procedimiento:**
1. Si T está vacío → finalizar
2. Si T tiene un único valor en atributo objetivo → generar Hoja
3. Seleccionar atributo con **mayor ganancia de información**
4. Particionar T por cada valor de ese atributo
5. Aplicar recursividad a cada partición

**Resultado:** reglas del tipo: `SI atrib_entrada = valor ENTONCES atrib_objetivo = resultado`

---

## Métricas de Evaluación ML

### Matriz de Confusión

|  | Predijo Positivo | Predijo Negativo |
|--|-----------------|-----------------|
| **Real Positivo** | VP (Verdadero Positivo) | FN (Falso Negativo) |
| **Real Negativo** | FP (Falso Positivo) | VN (Verdadero Negativo) |

### Métricas

| Métrica | Fórmula | Qué mide |
|---------|---------|---------|
| **Exactitud** | (VP+VN)/(VP+FP+VN+FN) | % de predicciones correctas total |
| **Precisión** | VP/(VP+FP) | De los que predije positivos, ¿cuántos lo son realmente? |
| **Recall (Sensibilidad)** | VP/(VP+FN) | De los positivos reales, ¿cuántos encontré? |
| **F1 Score** | 2×Precisión×Recall/(Precisión+Recall) | Balance entre precisión y recall |
| **Error absoluto** | \|real − estimado\| | Para regresión |
| **Error relativo** | \|real − estimado\| / real | Para regresión (en %) |

### Cuándo usar cada métrica

- **Exactitud:** cuando las clases están balanceadas
- **Precisión:** cuando el costo de los FP es alto (ej: spam)
- **Recall:** cuando el costo de los FN es alto (ej: enfermedades)
- **F1:** cuando se necesita balance entre ambas

---

## Mapa general de tecnologías

```
IA
├── IA Tradicional
│   ├── SBC → fuentes públicas
│   └── SET → fuentes privadas (puede usar públicas también)
│
├── Machine Learning
│   ├── Algoritmos de inducción (TDIDT) → reglas de clasificación
│   ├── Algoritmos de regresión → fórmula numérica
│   └── RNA (también en IC)
│
└── Inteligencia Computacional
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

## Trampas del examen

- "Los conocimientos públicos son siempre declarativos" → **FALSO** — pueden ser procedimentales también
- "Los conocimientos privados se educen" → **VERDADERO**
- Un SE puede usar fuentes públicas además de privadas → **VERDADERO**
- La IC no posee base de conocimientos → **VERDADERO**
- RNA ∈ Machine Learning Y ∈ Inteligencia Computacional → **ambas son correctas**
- TDIDT es supervisado y offline → **VERDADERO**

# 05 — Emparrillado (Repertory Grid)

> **Playlist:** Emparrillado  
> **Objetivo:** Técnica de educción del conocimiento que clasifica elementos del dominio según características bipolares.

---

## ¿Qué es?

**Técnica de educción del conocimiento** que trabaja sobre un área de interés.

**Definición:** Test de clasificación que vincula una lista de **elementos homogéneos y representativos** con un conjunto **bipolar de características**, para extraer similitudes y diferencias entre los elementos desde el punto de vista del experto.

- Cada individuo ve al mundo de manera diferente
- **Describe** elementos del dominio
- **Los ubica** en el imaginario del experto
- **Tiene en cuenta** los aspectos importantes para el experto

**Ventajas:** reflexión sobre el tema, representación gráfica, asociaciones, refina el problema.

**Inconvenientes:** valores subjetivos, solo captura conocimiento superficial, complejo con muchos elementos, **solo no es útil para construir una Base de Conocimiento** (necesita complementarse).

---

## Etapas

1. Identificación de los elementos
2. Identificación de las características
3. Diseño de la parrilla
4. Formalización
5. Interpretación / Análisis de resultados

---

### Etapa 1: Identificación de los Elementos

Los elementos deben ser:
- **Representativos** del dominio
- **Homogéneos** (todos del mismo tipo)
- **Separables** (distinguibles entre sí)
- **No solapados**

*Ejemplo: E1=COVID-19, E2=MERS-CoV, E3=SARS-CoV, E4=229E*

---

### Etapa 2: Identificación de las Características

Cualidad atribuida a un elemento. Los valores son siempre **bipolares** (alto/bajo, intenso/leve, etc.)

*Ejemplo: C1=Frecuencia respiratoria (alta/baja), C2=Fiebre (alta/baja)*

---

### Etapa 3: Diseño de la Parrilla

Matriz bidimensional que cruza elementos × características.

**Tipos de parrilla:**

| Tipo | Escala | Descripción |
|------|--------|-------------|
| **Dicotómica** | {0, 1} | El elemento posee o no la característica |
| **Clasificatoria** | [1, n] (n = nro. de elementos) | Asigna posición/orden al elemento en el rango (sin empates) |
| **Evaluativa** | [1, n] (n no fijo) | Grado de satisfacción del elemento con la característica |

*Ejemplo con parrilla evaluativa [1,4]:*

|    | E1 | E2 | E3 | E4 |
|----|----|----|----|----|
| C1 | 2  | 4  | 3  | 2  |
| C2 | 3  | 2  | 2  | 3  |
| C3 | 1  | 3  | 4  | 1  |
| C4 | 4  | 1  | 2  | 2  |

---

### Etapa 4: Formalización

Se divide en dos partes: clasificación de elementos y clasificación de características.

#### A. Clasificación de Elementos

**Paso 1: Calcular la Matriz de Distancias de Elementos** (triangular superior)

Distancia entre dos elementos = suma de diferencias absolutas por característica:
```
d(E1, E2) = |2-4| + |3-2| + |1-3| + |4-1| = 2+1+2+3 = 8
```

|    | E1 | E2 | E3 | E4 |
|----|----|----|----|----|
| E1 |    | 8  | 7  | 2  |
| E2 |    |    | 3  | 6  |
| E3 |    |    |    | 5  |

**Paso 2: Fusionar el par con mínima distancia** (o máxima, según criterio elegido)

→ El mínimo es d(E1,E4) = 2 → fusionar [E1,E4]

**Paso 3: Recalcular distancias del grupo fusionado** con los demás elementos

Usando criterio **mínimo:**
```
d([E1,E4], E2) = min(d(E1,E2), d(E4,E2)) = min(8, 6) = 6
d([E1,E4], E3) = min(d(E1,E3), d(E4,E3)) = min(7, 5) = 5
```

|           | E2 | E3 |
|-----------|----|----|
| [E1, E4]  | 6  | 5  |
| E2        |    | 3  |

→ Siguiente mínimo: d(E2,E3) = 3 → fusionar [E2,E3]

→ d([E1,E4], [E2,E3]) = min(5,6,5,3) = 3 → fusionar todo

**Árbol resultante (dendrograma de elementos):**
```
Distancia:
    2       E1 ─┐
                ├── [E1,E4] ─┐
            E4 ─┘            ├── todos
    3       E2 ─┐            │
                ├── [E2,E3] ─┘
            E3 ─┘
```

---

#### B. Clasificación de Características

**Proceso más complejo — usa DOS parrillas:**

**Paso 1: Matriz de distancias d1** (distancia entre características usando la parrilla original, comparando por filas)
```
d1(C1, C2) = |2-3| + |4-2| + |3-2| + |2-3| = 1+2+1+1 = 5
```

Genera la triangular **superior**.

**Paso 2: Parrilla opuesta** (invertir la escala: 1→4, 2→3, 3→2, 4→1)

**Paso 3: Matriz de distancias d2** (comparar un elemento de la parrilla original con el correspondiente de la parrilla opuesta)
```
d2(C1, C2) = |2-2| + |4-3| + |3-2| + |2-2| = 0+1+0+0 = 1
```

Genera la triangular **inferior**.

**Paso 4: Matriz final de características** — para cada par de características, tomar el **mínimo** entre d1 y d2 (la diagonal queda vacía)

**Paso 5:** Igual que con elementos → fusionar el par con menor distancia → recalcular → construir árbol

---

### Etapa 5: Interpretación / Análisis de Resultados

#### Análisis de árboles
- Identificar grupos de elementos similares y distancias entre ellos
- Explicar qué significa que dos elementos estén en el mismo grupo desde el punto de vista del experto
- Ídem para grupos de características

#### Red de relaciones entre características

Solo se relacionan características que pertenecen al mismo grupo.

**Tipos de relaciones:**

| Relación | Descripción |
|----------|-------------|
| **Paralela** | Cuando C1 es alta, C2 también es alta (y viceversa) |
| **Recíproca** | Cuando C1 es alta, C2 es baja (y viceversa) |
| **Ortogonal** | C1 y C2 son independientes, no se afectan entre sí |
| **Ambigua** | No se puede determinar una relación clara |

---

## Resumen clave para el final

1. El emparrillado captura cómo el experto **clasifica y diferencia** elementos del dominio.
2. **No sirve solo** para construir una BdC; necesita combinarse con otras técnicas.
3. Las 5 etapas: **Elementos → Características → Parrilla → Formalización → Interpretación**.
4. La parrilla puede ser dicotómica, clasificatoria o **evaluativa**.
5. **Formalización:** calcular matrices de distancias y construir dendrogramas para elementos y características.
6. Para características: necesitás la parrilla original **y** la opuesta (d1 y d2 → tomar mínimo).
7. **Relaciones entre características:** paralela / recíproca / ortogonal / ambigua.

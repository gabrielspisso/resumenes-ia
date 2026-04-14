# 05 — Emparrillado (Repertory Grid)

> **Playlist:** Emparrillado  
> Fuente: Clase 7, Para el Coloquio, Tips ejercicios

---

## ¿Qué es?

**Técnica de educción del conocimiento** que clasifica elementos del dominio según características bipolares.

**Definición:** Test de clasificación que vincula una lista de **elementos homogéneos y representativos** con un conjunto **bipolar de características**, para extraer similitudes y diferencias entre los elementos desde el punto de vista del experto.

**Principios:**
- Cada individuo ve al mundo de manera diferente
- Trabaja sobre un área de interés
- Tiene en cuenta solo lo que el experto considera importante

**Ventajas:** reflexión sobre el tema, representación gráfica, produce asociaciones elemento-característica, refina el conocimiento.

**Limitaciones:**
- Los valores son subjetivos (dependen del experto)
- Solo captura conocimiento superficial
- Se vuelve complejo con muchos elementos/características
- **Por sí solo no es útil para construir una base de conocimientos** (necesita complementarse con AP u otras técnicas)

---

## Las 5 Etapas del Emparrillado

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
- **No solapados** (no puede haber dos al mismo tiempo)

*Ejemplo: E1=COVID-19, E2=MERS-CoV, E3=SARS-CoV, E4=229E*

---

### Etapa 2: Identificación de las Características

Cualidad atribuida a un elemento o concepto del dominio. Los valores son siempre **bipolares** (alto/bajo, intenso/leve, etc.).

*Ejemplo: C1=Frecuencia respiratoria, C2=Fiebre, C3=Contagiosidad, C4=Mortalidad*

---

### Etapa 3: Diseño de la Parrilla

Matriz bidimensional que cruza **elementos × características**.

**Tipos de parrilla:**

| Tipo | Escala | Descripción |
|------|--------|-------------|
| **Dicotómica** | {0, 1} | El elemento posee (1) o no (0) la característica |
| **Clasificatoria** | [1, n] donde n = cantidad de elementos | Posición/rango sin empates; cada relación posee un valor único |
| **Evaluativa** | [1, n] donde n lo define el experto | Grado de satisfacción; pueden repetirse valores |

*Ejemplo de parrilla evaluativa (escala 1-4):*

|    | E1 | E2 | E3 | E4 |
|----|----|----|----|----|
| C1 | 2  | 4  | 3  | 2  |
| C2 | 3  | 2  | 2  | 3  |
| C3 | 1  | 3  | 4  | 1  |
| C4 | 4  | 1  | 2  | 2  |

---

### Etapa 4: Formalización

Se divide en dos partes: **clasificación de elementos** y **clasificación de características**.

#### Parte A: Clasificación de Elementos

**Objetivo:** construir un árbol que muestre qué elementos son más similares entre sí.

**Paso 1: Calcular la Matriz de Distancias de Elementos**

Para cada par de elementos: sumar las diferencias absolutas por cada característica.

```
d(E1, E2) = |C1_E1 - C1_E2| + |C2_E1 - C2_E2| + ... 
d(E1, E2) = |2-4| + |3-2| + |1-3| + |4-1| = 2+1+2+3 = 8
```

La matriz es **simétrica** (d(E1,E2) = d(E2,E1)) con la **diagonal en cero**.

|    | E1 | E2 | E3 | E4 |
|----|----|----|----|----|
| E1 | 0  | 8  | 7  | 2  |
| E2 |    | 0  | 3  | 6  |
| E3 |    |    | 0  | 5  |
| E4 |    |    |    | 0  |

**Paso 2: Fusionar el par con mínima distancia**

→ Mínimo = d(E1,E4) = 2 → fusionar [E1,E4]

**Paso 3: Recalcular distancias con el nuevo grupo**

```
d([E1,E4], E2) = MIN(d(E1,E2), d(E4,E2)) = MIN(8, 6) = 6
d([E1,E4], E3) = MIN(d(E1,E3), d(E4,E3)) = MIN(7, 5) = 5
```

Nueva matriz:

|         | [E1,E4] | E2 | E3 |
|---------|---------|----|----|
| [E1,E4] | 0       | 6  | 5  |
| E2      |         | 0  | 3  |
| E3      |         |    | 0  |

→ Mínimo = d(E2,E3) = 3 → fusionar [E2,E3]

→ d([E1,E4], [E2,E3]) = MIN(5,6) = 5 → fusionar todo → árbol completo.

**Árbol de elementos:**

```
Nivel 5: [E1,E4,E2,E3]
Nivel 3: [E2,E3]
Nivel 2: [E1,E4]

E1 ─┐ (nivel 2)
E4 ─┘
        ┬ (nivel 5)
E2 ─┐ (nivel 3)
E3 ─┘
```

**Interpretación:** cuanto **más bajo** el nivel de unión → **más similares** son los elementos.

---

#### Parte B: Clasificación de Características

**Objetivo:** construir un árbol que muestre qué características son más similares (o más opuestas) entre sí.

**Paso 1: Construir la Parrilla Opuesta**

Invertir la escala de valores de la parrilla original.

*Escala original [1,4]: si en la original hay un 2 → en la opuesta hay un 3 (4+1-2=3)*

**Paso 2: Calcular la Distancia D1 (Diagonal Superior)**

Recorrer la parrilla original horizontalmente, comparando características dos a dos:
```
D1(C1, C2) = |C1_E1 - C2_E1| + |C1_E2 - C2_E2| + ... 
```
*(se pone en la diagonal superior: C1 con C2, C1 con C3, etc.)*

**Paso 3: Calcular la Distancia D2 (Diagonal Inferior)**

Tomar el primer valor de la parrilla **original** y el segundo de la parrilla **opuesta**:
```
D2(C1, C2): usar C1 de original y C2 de opuesta (o viceversa)
```
*(se pone en la diagonal inferior)*

**Paso 4: Construir la Matriz Final**

Para cada par de características, comparar el valor de D1 (diagonal superior) con D2 (diagonal inferior):
- Tomar el **menor** de los dos valores

Con esta matriz final, se aplica el mismo proceso de fusión que con los elementos.

---

### Etapa 5: Interpretación / Análisis de Resultados

#### Árbol de elementos
- **Distancia entre elementos = nivel** en el árbol
- Nivel bajo = elementos muy similares
- Nivel alto = elementos muy diferentes

#### Árbol de características: Red de relaciones

Se identifican relaciones entre características del mismo grupo. Solo se pueden relacionar características **del mismo grupo**.

**Tipos de relaciones:**

| Relación | Descripción | Símbolo |
|----------|-------------|---------|
| **Paralela** | Las dos características siempre se dan juntas (2 a 2, ambas) | → ← |
| **Recíproca** | Una característica implica a la otra en ambas direcciones (2 a 2, ida y vuelta) | ⇄ |
| **Ortogonal** | Solo 1 a 1, o llegan 2 flechas a 1 característica | ↑ |
| **Ambigua** | Salen 2 flechas de 1 a las otras dos, o variantes | ↗↘ |
| **No tipificada** | No entra en ninguna de las anteriores | — |

---

## Comparación AP vs Emparrillado

| Aspecto | Análisis de Protocolos | Emparrillado |
|---------|----------------------|-------------|
| **Qué captura** | Procedimientos implícitos | Similitudes/diferencias entre elementos |
| **Cómo** | Experto piensa en voz alta | Experto clasifica elementos según características |
| **Resultado** | Reglas SI-ENTONCES | Árboles de similitud y relaciones entre características |
| **Conocimiento** | Procedimental + Declarativo | Declarativo (superficial) |

---

## Trampas del examen (Tips del docente)

**Matriz de distancia de elementos:**
- Bajar de forma vertical, restando E1 con E2 y sacando módulo → sumar
- Se arman subgrupos con la **mínima distancia**
- Al calcular distancia de un grupo con un elemento: `MIN(dist(X,Z), dist(Y,Z))`

**Clasificación de características:**
1. Parrilla original → invertir intervalo → parrilla opuesta
2. D1 coloca diagonal superior (recorrer original horizontal: C1 y C2)
3. D2 coloca diagonal inferior (C1 de original + C2 de opuesta, horizontal)
4. Matriz final: tomar el menor de cada par (superior vs inferior)

**Relaciones (trampas comunes):**
- **Paralela:** 2 a 2, sí o sí ambas características
- **Recíproca:** 2 a 2, ida y vuelta (A implica B y B implica A)
- **Ortogonal:** solo 1 a 1 o llega 2 flechas a 1 característica
- **Ambigua:** salen 2 flechas de 1 a las otras dos (múltiples formas)
- Solo se relacionan características **del mismo grupo** en el árbol

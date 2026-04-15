# 05 — Emparrillado (Repertory Grid)

> **Playlist:** Emparrillado  
> **Objetivo:** Técnica de educción del conocimiento que clasifica elementos del dominio según características bipolares para extraer similitudes y diferencias desde la perspectiva del experto.

---

## ¿Qué es?

**Técnica de educción del conocimiento** que trabaja sobre un área de interés específica para extraer conocimiento privado del experto.

**Definición:** Test de clasificación que vincula una lista de **elementos homogéneos y representativos** con un conjunto **bipolar de características**, para extraer similitudes y diferencias entre los elementos desde el punto de vista del experto.

### Fundamentos

- Cada individuo ve al mundo de manera diferente
- **Describe** elementos del dominio
- **Los ubica** en el imaginario del experto
- **Tiene en cuenta** los aspectos más importantes y representativos para el experto

**Origen histórico:** Presentada en 1955 como "técnica del constructo personal", originalmente se utilizó en psicología para trabajar con pacientes con trastornos mentales, buscando obtener un mapa del dominio que el paciente podía percibir.

### Características principales

La técnica se basa en la construcción de un **modelo mental** del experto, identificando:
- **Elementos** del dominio
- **Características bipolares** (con dos polos opuestos)
- **Relaciones** entre estas características

---

## Ventajas e Inconvenientes

### Ventajas

1. **Reflexión sobre el tema:** Permite que el experto reflexione a través del diálogo con el ingeniero de conocimiento
2. **Representación gráfica:** Proporciona visualización clara mediante árboles (dendrogramas) y matrices
3. **Asociación elementos-características:** Facilita la comprensión de relaciones en la matriz
4. **Refinamiento del problema:** Ayuda al experto a identificar mejor los elementos y aspectos clave
5. **Formalización del conocimiento:** Transforma el conocimiento tácito en una representación más estructurada
6. **Comparación entre expertos:** Permite analizar diferentes perspectivas si se aplica a múltiples expertos del mismo dominio

### Inconvenientes

1. **Valores subjetivos:** Los valores de la matriz dependen del experto; diferentes expertos pueden dar valores diferentes para los mismos elementos y características
2. **Conocimiento superficial:** Solo captura lo que el experto considera más importante y representativo
3. **Complejidad con muchos elementos:** Cuando hay gran cantidad de elementos o características, los árboles se vuelven gráficos muy complejos y con información probablemente superficial
4. **Técnica intrusiva:** Aborda directamente el pensamiento del experto, lo que puede hacer que se sienta invadido
5. **Incompleta:** **No es útil por sí sola para construir una Base de Conocimiento** (necesita complementarse con otras técnicas)
6. **Resultados requieren validación:** Las conclusiones extraídas deben validarse posteriormente con el experto

---

## Etapas de la Técnica

1. **Diálogo inicial:** Identificación del dominio y establecimiento de una primera aproximación
2. **Identificación de elementos**
3. **Identificación de características**
4. **Diseño de la parrilla** (sesión de valoración donde el experto asigna valores)
5. **Formalización** (cálculos realizados por el ingeniero de conocimiento)
6. **Interpretación y análisis de resultados** (validación con el experto)

---

## Etapa 1: Identificación de los Elementos

Los elementos deben cumplir con estos requisitos:

- **Representativos:** deben ser significativos y relevantes del dominio
- **Homogéneos:** todos del mismo tipo, pertenecientes al mismo dominio
- **Separables:** distinguibles entre sí, sin solapamiento
- **No solapados:** no pueden compartirse (el elemento 1 y el elemento 2 no pueden ser simultáneamente presentes)

**Ejemplo:** Para un dominio médico de virus respiratorios:
- E1 = COVID-19
- E2 = MERS-CoV
- E3 = SARS-CoV
- E4 = Coronavirus 229E

---

## Etapa 2: Identificación de las Características

Una **característica** es una cualidad que se puede atribuir a un elemento. Los valores son siempre **bipolares** (dos polos opuestos que definen un continuo).

**Ejemplos de características bipolares:**
- Alta / Baja
- Intenso / Leve
- Presente / Ausente

**Ejemplo del dominio médico:**
- C1 = Frecuencia respiratoria (alta / baja)
- C2 = Fiebre (alta / baja)
- C3 = Intensidad del dolor de garganta (intenso / leve)
- C4 = Intensidad del dolor de cabeza (intenso / leve)

---

## Etapa 3: Diseño de la Parrilla

Una **parrilla** es una matriz bidimensional que cruza **elementos × características**, mostrando cómo cada elemento se relaciona con cada característica.

### Tipos de Parrilla

| Tipo | Escala | Descripción |
|------|--------|-------------|
| **Dicotómica** | {0, 1} | El elemento posee (1) o no (0) la característica |
| **Clasificatoria** | [1, n] (n = nro. de elementos) | Asigna posición/orden al elemento en un ranking sin empates |
| **Evaluativa** | [1, n] (n no fijo) | Grado de satisfacción/intensidad del elemento con la característica |

#### Parrilla Dicotómica (Ejemplo)
```
    | E1 | E2 | E3 | E4 |
----|----|----|----|----|
C1  | 1  | 0  | 1  | 1  |
C2  | 1  | 1  | 0  | 0  |
C3  | 0  | 1  | 1  | 0  |
C4  | 1  | 0  | 1  | 1  |
```

#### Parrilla Clasificatoria (Ejemplo)
```
    | E1 | E2 | E3 | E4 |
----|----|----|----|----|
C1  | 2  | 4  | 3  | 1  |
C2  | 1  | 3  | 2  | 4  |
C3  | 4  | 2  | 1  | 3  |
C4  | 3  | 1  | 4  | 2  |
```
*Nota: Cada fila contiene los números del 1 al 4 sin repetir (ranking sin empates)*

#### Parrilla Evaluativa (Ejemplo - Escala [1,4])
```
    | E1 | E2 | E3 | E4 |
----|----|----|----|----|
C1  | 2  | 4  | 3  | 2  |
C2  | 3  | 2  | 2  | 3  |
C3  | 1  | 3  | 4  | 1  |
C4  | 4  | 1  | 2  | 2  |
```
*Nota: Los valores pueden repetirse, indican grado de satisfacción o intensidad*

---

## Etapa 4: Formalización

Esta es la etapa más compleja. Se realiza en dos partes: clasificación de elementos y clasificación de características.

### Parte A: Clasificación de Elementos

#### Paso 1: Calcular la Matriz de Distancias entre Elementos

La **distancia entre dos elementos** se calcula como la suma de las diferencias absolutas en todas las características:

```
d(Ei, Ej) = Σ |valor(Ei,Ck) - valor(Ej,Ck)|
```

**Ejemplo de cálculo** (usando la parrilla evaluativa anterior):
```
d(E1, E2) = |2-4| + |3-2| + |1-3| + |4-1| = 2+1+2+3 = 8
d(E1, E3) = |2-3| + |3-2| + |1-4| + |4-2| = 1+1+3+2 = 7
d(E1, E4) = |2-2| + |3-3| + |1-1| + |4-2| = 0+0+0+2 = 2
d(E2, E3) = |4-3| + |2-2| + |3-4| + |1-2| = 1+0+1+1 = 3
d(E2, E4) = |4-2| + |2-3| + |3-1| + |1-2| = 2+1+2+1 = 6
d(E3, E4) = |3-2| + |2-3| + |4-1| + |2-2| = 1+1+3+0 = 5
```

**Matriz de distancias** (triangular superior):
```
    | E1 | E2 | E3 | E4 |
----|----|----|----|----|
E1  |    | 8  | 7  | 2  |
E2  |    |    | 3  | 6  |
E3  |    |    |    | 5  |
E4  |    |    |    |    |
```

*Nota: La diagonal principal no se calcula porque la distancia de un elemento consigo mismo es 0*

#### Paso 2: Fusionar el par con mínima (o máxima) distancia

En nuestro ejemplo, tomamos el **criterio de mínima distancia**:

→ El mínimo es d(E1,E4) = 2 → **fusionar [E1,E4]**

#### Paso 3: Recalcular distancias del nuevo grupo

Cuando fusionamos [E1,E4], necesitamos recalcular sus distancias con los elementos restantes usando el **criterio mínimo**:

```
d([E1,E4], E2) = min(d(E1,E2), d(E4,E2)) = min(8, 6) = 6
d([E1,E4], E3) = min(d(E1,E3), d(E4,E3)) = min(7, 5) = 5
d(E2, E3) = 3 (ya calculado)
```

**Nueva matriz**:
```
           | E2 | E3 |
-----------|----|----|
[E1, E4]   | 6  | 5  |
E2         |    | 3  |
E3         |    |    |
```

→ Siguiente mínimo: d(E2,E3) = 3 → **fusionar [E2,E3]**

#### Paso 4: Siguiente fusión

```
d([E1,E4], [E2,E3]) = min(6, 5) = 5
```

→ **Fusionar todos en distancia 5**

#### Árbol resultante (dendrograma de elementos)

```
Distancia:
    2       E1 ─┐
                ├── [E1,E4] ─┐
            E4 ─┘            ├── todos
    3       E2 ─┐            │
                ├── [E2,E3] ─┘
            E3 ─┘     5
```

**Interpretación:** El árbol muestra que E1 y E4 son muy similares (distancia 2), E2 y E3 son similares (distancia 3), y los dos grupos se unen a distancia 5.

---

### Parte B: Clasificación de Características

Este proceso es **más complejo** porque utiliza **DOS parrillas**: la original y una parrilla opuesta.

#### Paso 1: Parrilla Opuesta

Se invierte la escala de valores. Para una escala [1,4]:
- 1 → 4
- 2 → 3
- 3 → 2
- 4 → 1

**Ejemplo** (parrilla original vs. opuesta):

Parrilla Original:
```
    | E1 | E2 | E3 | E4 |
----|----|----|----|----|
C1  | 2  | 4  | 3  | 2  |
C2  | 3  | 2  | 2  | 3  |
C3  | 1  | 3  | 4  | 1  |
C4  | 4  | 1  | 2  | 2  |
```

Parrilla Opuesta:
```
    | E1 | E2 | E3 | E4 |
----|----|----|----|----|
C1  | 3  | 1  | 2  | 3  |
C2  | 2  | 3  | 3  | 2  |
C3  | 4  | 2  | 1  | 4  |
C4  | 1  | 4  | 3  | 3  |
```

#### Paso 2: Matriz de Distancias d1 (triangular superior)

Se calcula de la misma forma que con elementos, pero comparando características por filas en la parrilla original:

```
d1(C1, C2) = |2-3| + |4-2| + |3-2| + |2-3| = 1+2+1+1 = 5
d1(C1, C3) = |2-1| + |4-3| + |3-4| + |2-1| = 1+1+1+1 = 4
d1(C1, C4) = |2-4| + |4-1| + |3-2| + |2-2| = 2+3+1+0 = 6
d1(C2, C3) = |3-1| + |2-3| + |2-4| + |3-1| = 2+1+2+2 = 7
d1(C2, C4) = |3-4| + |2-1| + |2-2| + |3-2| = 1+1+0+1 = 3
d1(C3, C4) = |1-4| + |3-1| + |4-2| + |1-2| = 3+2+2+1 = 8
```

#### Paso 3: Matriz de Distancias d2 (triangular inferior)

Se calcula tomando **un elemento de cada parrilla** (original y opuesta):

```
d2(C1, C2) = |2-2| + |4-3| + |3-3| + |2-2| = 0+1+0+0 = 1
d2(C1, C3) = |2-4| + |4-2| + |3-1| + |2-4| = 2+2+2+2 = 8
d2(C1, C4) = |2-1| + |4-4| + |3-3| + |2-3| = 1+0+0+1 = 2
d2(C2, C3) = |3-4| + |2-2| + |2-1| + |3-4| = 1+0+1+1 = 3
d2(C2, C4) = |3-1| + |2-4| + |2-3| + |3-3| = 2+2+1+0 = 5
d2(C3, C4) = |1-1| + |3-4| + |4-3| + |1-3| = 0+1+1+2 = 4
```

#### Paso 4: Matriz final de características

Para cada par de características, tomar el **mínimo entre d1 y d2**:

```
           | C1 | C2 | C3 | C4 |
-----------|----|----|----|----|
C1         |    | 1  | 4  | 2  |
C2         |    |    | 3  | 3  |
C3         |    |    |    | 4  |
C4         |    |    |    |    |
```

*Explicación: mín(5,1)=1, mín(4,8)=4, mín(6,2)=2, mín(7,3)=3, mín(3,5)=3, mín(8,4)=4*

#### Paso 5: Construir el dendrograma de características

Se sigue el mismo proceso que con elementos: fusionar el par con menor distancia, recalcular distancias del nuevo grupo, etc.

Tomando el mínimo valor (1, entre C1 y C2):
→ **Fusionar [C1,C2]**

Siguiente: d(C2,C4) = 3 y d(C2,C3) = 3
→ **Fusionar [C2,C4]** (o C2,C3, según el orden)

Finalmente:
→ **Fusionar todos los grupos**

**Árbol resultante de características**:
```
Distancia:
    1       C1 ─┐
                ├── [C1,C2] ─┐
            C2 ─┘            ├── todos
    2       C4 ─┐            │
                ├── [C4,?] ──┘
            C3 ─┘     3
```

---

## Etapa 5: Interpretación y Análisis de Resultados

Esta es la última etapa y tiene dos subetapas principales.

### Subetapa 5.1: Análisis de los Árboles

#### Análisis del árbol de elementos

1. Identificar **grupos de elementos similares**
2. Observar las **distancias de conexión** dentro de cada grupo
3. Explicar desde el punto de vista del experto por qué los elementos están agrupados

**Ejemplo:**
- El árbol muestra **dos grupos principales**: [E1,E4] y [E2,E3]
- E1 y E4 son similares a distancia 2 (muy próximos)
- E2 y E3 son similares a distancia 3
- Los grupos se unen a distancia 5 (menos similares entre grupos)

#### Análisis del árbol de características

1. Identificar **grupos de características relacionadas**
2. Observar qué características el experto considera que **varían juntas**
3. Explicar las relaciones entre características

**Ejemplo:**
- El árbol muestra que C1 y C2 están fuertemente relacionadas (distancia 1)
- Estas características varían de manera similar según los elementos

### Subetapa 5.2: Red de Relaciones entre Características

Una vez identificados los grupos de características, se analizan los **tipos de relaciones** entre ellas.

#### Reglas importantes

- **Solo se pueden relacionar características que pertenecen al mismo grupo** (que aparecen juntas en el árbol)
- Si el texto menciona relaciones entre características de grupos diferentes, esa relación no es válida

#### Tipos de Relaciones

| Relación | Gráfico | Descripción |
|----------|---------|-------------|
| **Paralela** | →↑→↑ | Cuando C1 aumenta, C2 también aumenta (y viceversa). Los dos polos positivos se relacionan y los negativos también. |
| **Recíproca** | →↑→↓ | Cuando C1 aumenta, C2 disminuye (y viceversa). Un polo positivo se relaciona con uno negativo. |
| **Ortogonal** | ⊥ | C1 y C2 son independientes; no se afectan entre sí. Un polo de C1 se relaciona con ambos de C2. |
| **Ambigua** | ? | No se puede determinar una relación clara o el texto proporciona información incompleta. |
| **No tipificada** | ~ | La relación no corresponde a ninguna de las anteriores. |

#### Ejemplo de análisis de relaciones

**Texto del enunciado:**
"En las observaciones realizadas a diferentes pacientes se puede apreciar que aquellos coronavirus que se manifiestan con frecuencia respiratoria alta, se caracterizan por presentarse con fiebre alta también, mientras que en aquellos casos que se manifiestan con frecuencia respiratoria baja, poseen fiebre baja también."

**Análisis:**
- Se menciona: frecuencia respiratoria **alta** ↔ fiebre **alta**
- Se menciona: frecuencia respiratoria **baja** ↔ fiebre **baja**
- Esto coincide con el gráfico de relación **paralela**
- C1 (frecuencia respiratoria) y C2 (fiebre) están en el mismo grupo → relación válida

**Conclusión:** Existe una **relación paralela entre C1 y C2**

---

## Resumen clave para el final

1. **Propósito:** El emparrillado captura cómo el experto **clasifica y diferencia** elementos del dominio mediante características bipolares.

2. **No es suficiente por sí sola:** No sirve para construir una Base de Conocimiento de manera independiente; necesita complementarse con otras técnicas de adquisición de conocimiento.

3. **Las 6 etapas:** 
   - Diálogo inicial
   - Identificación de elementos
   - Identificación de características
   - Diseño de la parrilla
   - **Formalización** (cálculos de distancias y dendrogramas)
   - **Interpretación** (análisis de árboles y relaciones)

4. **Tipos de parrilla:** Dicotómica, clasificatoria o evaluativa.

5. **Formalización:** Calcular matrices de distancias y construir dendrogramas para elementos y características usando el criterio de mínima (o máxima) distancia.

6. **Características especiales:** Para características, necesitas la parrilla original **y** la opuesta (d1 y d2 → tomar mínimo de cada par).

7. **Relaciones entre características:** Paralela / recíproca / ortogonal / ambigua / no tipificada (solo entre características del mismo grupo).

8. **Validación:** Los resultados deben discutirse y validarse con el experto.

---

## 📝 Cambios respecto al original

### Información agregada:

1. **Origen histórico:** Añadido contexto sobre la presentación en 1955 y uso original en psicología clínica
2. **Naturaleza intrusiva:** Clarificado que es una técnica un tanto invasiva del pensamiento del experto
3. **Ejemplo concreto:** Integrado el dominio médico con virus específicos (COVID-19, MERS-CoV, SARS-CoV, 229E) y síntomas (frecuencia respiratoria, fiebre, dolor de garganta, dolor de cabeza)
4. **Proceso iterativo:** Enfatizado el rol del diálogo inicial, la sesión de valoración y la validación final con el experto
5. **Ampliación de ventajas:** Agregada la ventaja de poder comparar perspectivas entre múltiples expertos
6. **Mayor detalle en formalización:** 
   - Explicación paso a paso del cálculo de la matriz de distancias
   - Ejemplo numérico completo con cálculos
   - Clarificación del criterio de mínima/máxima distancia
   - Ejemplo visual de parrilla opuesta (inversión de escala)
   - Explicación de por qué se necesitan dos matrices (d1 y d2) para características
7. **Dendrogramas mejorados:** Representación visual más clara de los árboles resultantes
8. **Relaciones entre características:** 
   - Agregado tipo "No tipificada"
   - Ejemplo completo de análisis de texto para identificar relaciones
   - Énfasis en que solo se pueden relacionar características del mismo grupo
9. **Análisis de ejemplo:** Desarrollado el análisis completo del ejemplo médico incluyendo interpretación de grupos y distancias
10. **Mayor claridad:** Mejorado el lenguaje en secciones técnicas y agregados más detalles sobre limitaciones prácticas

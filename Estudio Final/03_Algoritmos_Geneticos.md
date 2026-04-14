# 03 — Algoritmos Genéticos

> **Playlist:** Algoritmos Genéticos  
> Fuente: Clase 4, Para el Coloquio

---

## ¿Qué son?

Algoritmos matemáticos de **optimización de propósito general** basados en mecanismos naturales de selección y genética.

**Características:**
- Dan excelentes soluciones en problemas complejos con muchos parámetros
- "Saltan" entre distintos resultados buscando máximos locales y comparando para encontrar el máximo absoluto
- **Estable:** la cantidad de individuos se mantiene constante a lo largo de toda la ejecución
- No necesitan datos históricos (a diferencia de ML)

**Cuándo usar AG:** cuando hay heurísticas disponibles sobre el problema pero no datos suficientes para ML.

---

## Analogía con la evolución

| Biología | AG |
|----------|----|
| Ecosistema / Ambiente | El problema a resolver |
| Individuo | Posible solución |
| **Cromosoma / Genotipo** | Descripción de la solución (cadena de bits o estructura) |
| Gen | Característica o atributo (porción del cromosoma) |
| **Fenotipo** | Resultado de aplicar la función de aptitud al cromosoma |
| Selección natural | Operador de selección |
| Herencia | Operador de cruzamiento |
| Mutación | Operador de mutación |

---

## Estructura del Cromosoma

- Cadena de bits o valores que representa **una posible solución**
- Dividido en **genes** (cada gen = una característica del problema)
- Los genes no tienen por qué tener la misma longitud
- El cromosoma debe ser: completo, coherente, uniforme y sencillo

---

## Función de Aptitud (Fitness)

Determina qué tan buena es la solución representada por un cromosoma. Devuelve un número: **mayor valor = mejor solución**.

**Pasos para diseñarla:**
1. Analizar pistas: qué condiciones debe cumplir la solución (aumenta fitness) y qué restricciones no puede cumplir (disminuye fitness)
2. Analizar la estructura del cromosoma: identificar combinaciones inválidas de genes (penaliza fitness)
3. Definir la operatoria para interpretar el cromosoma y calcular el valor

**Formas de penalizar soluciones inválidas:**
- Pena de muerte (aptitud = 0)
- Penas constantes por nivel
- Penas adaptativas por aptitud de la población
- Penas adaptativas por temperatura (según vueltas)

---

## Flujo del Algoritmo

```
1. Generar Población Inicial (GPI)
         ↓
2. Selección
         ↓
3. Cruzamiento
         ↓
4. Mutación
         ↓
5. ¿Criterio de paro cumplido?
   ├── SÍ → Población final → identificar mejor individuo → SOLUCIÓN
   └── NO → La población mutada = nueva población → volver a (2)
```

**Términos:**
- **Vuelta / Ciclo:** cada iteración del bucle (2)→(3)→(4)→(5)
- **Corrida:** ejecución completa del algoritmo hasta cumplir el criterio de paro

---

## Operador 1: Generar Población Inicial (GPI)

**Métodos:**
- **Al azar:** completamente aleatorio (random)
- **Ad-hoc:** con conocimiento previo del dominio para generar individuos válidos

**Parámetros:**
- Cantidad de individuos en la población
- Varianza (constante o variable)

---

## Operador 2: Selección

Objetivo: seleccionar un subconjunto de individuos para que participen en el cruzamiento.

### Torneo
- Se comparan de a pares según la función de aptitud
- El ganador pasa; un mismo individuo puede ganar varias veces
- **Ventaja:** garantiza una excelente solución
- **Desventaja:** puede perder al 2do mejor si enfrenta al 1ro en primera ronda

### Ranking
- Se ordena la población por fitness y se seleccionan los mejores según un criterio
- **Desventaja:** convergencia prematura (los de menor fitness nunca participan)

### Ruleta (Proporcional al fitness)

Proceso completo:
1. Calcular el **total de aptitud** (suma de todos los fitness)
2. Calcular el **porcentaje de participación** de cada individuo: `f(Ix) / total`
3. Calcular la **probabilidad acumulada** de cada individuo
4. Tirar un número aleatorio → el individuo cuya probabilidad acumulada lo incluye es seleccionado

**Mayor fitness = mayor probabilidad, pero todos tienen chance.**

### Ruleta con Control s/Número Esperado (más completa)

Evita seleccionar solo individuos malos en una tirada de ruleta:
1. Calcular el **promedio** de la aptitud total: `promedio = total / cantidad`
2. Para cada individuo: `relación = f(Ix) / promedio`
3. La **parte entera** de la relación = cuántas veces ese individuo es seleccionado garantizadamente
4. Con la **mantisa** (parte decimal) de cada individuo → hacer ruleta clásica para los puestos restantes

---

## Operador 3: Cruzamiento

Opera **de a pares** (2 padres → 2 hijos). Los padres son eliminados.

### Cruzamiento Simple (1 punto de corte)
- Se define un punto de corte (sin partir genes)
- Hijo 1: parte del padre 1 hasta el corte + parte del padre 2 desde el corte
- Hijo 2: lo inverso

### Cruzamiento Multipunto
- Dos o más puntos de corte
- Los segmentos se alternan entre padres

### Binomial – Máscara Complemento
- Se define una máscara (ej: 10110)
- Donde la máscara = 1: Hijo 1 toma del padre 1, Hijo 2 del padre 2
- Donde la máscara = 0: al revés
- **Hijo 2 es el complemento exacto del Hijo 1** (no se repiten genes)

### Binomial – Máscara Doble
- Una máscara distinta para cada hijo
- **Los genes pueden repetirse** en ambos hijos

### Binomial – Al Azar
- Para cada posición: generar random R
  - Si R ≤ umbral M → tomar gen del padre 1
  - Si R > umbral M → tomar gen del padre 2
- Para Hijo 2: usar complemento del Hijo 1, o volver a tirar al azar (puede repetir genes)

---

## Operador 4: Mutación

Simula alteraciones cromosómicas por agentes externos. Ocurre **después** del cruzamiento.

**Proceso:**
1. Generar random → ¿activa la mutación? (ej: random ≤ probabilidad de mutación)
2. Si se activa → generar random de posición → ese gen cambia de valor
3. Si no se activa → la población cruzada = población mutada (sin cambios)

> La mutación **puede activarse pero no ejecutarse** si el random de posición no genera cambio real.

**Métodos de probabilidad de mutación:**

| Método | Descripción |
|--------|-------------|
| **Simple** | Probabilidad constante durante toda la corrida |
| **Adaptativa por convergencia** | Varía según el promedio de aptitud de la población |
| **Adaptativa por temperatura** | Varía según la cantidad de vueltas (ascendente o descendente) |

---

## Operador 5: Criterio de Paro (opcional)

Se deja de iterar cuando:
- Se alcanza una cantidad de **vueltas** determinada
- Se supera un **tiempo límite**
- `f(Ix) > valor objetivo` (algún individuo supera el umbral)
- `promedio[f(Ix)] > valor objetivo`

> **Cuidado:** los dos últimos pueden generar bucles infinitos si el valor nunca se alcanza.

---

## Identificar la Solución

**Teóricamente:** al finalizar, calcular fitness a todos los individuos de la última población → tomar el mejor → decodificar el cromosoma.

**En la práctica:** guardar **logs de distintas corridas** → buscar el mejor individuo entre todas las corridas.

---

## Comparativa de métodos de selección

| Método | Ventaja | Desventaja |
|--------|---------|------------|
| Torneo | Garantiza buena solución | Puede perder al 2do mejor |
| Ranking | Simple | Convergencia prematura |
| Ruleta simple | Todos tienen chance | Puede seleccionar solo malos |
| Ruleta s/nro. esperado | La más completa y equitativa | Más compleja de implementar |

---

## Trampas del examen

- El AG es para **optimización**, no para clasificación/predicción con datos
- El cromosoma es la **descripción** de la solución (genotipo), no la solución en sí
- La mutación **siempre va después del cruzamiento**
- La cantidad de individuos es **estable** (se mantiene constante)
- La mutación puede activarse pero no ejecutarse
- En la ruleta, **todos tienen probabilidad** de ser seleccionados (≠ ranking)
- La ruleta con control s/nro. esperado usa parte entera (garantizada) + mantisa (ruleta) 
- El AG siempre termina en corrida, no en vuelta

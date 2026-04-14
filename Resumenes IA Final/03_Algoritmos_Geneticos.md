# 03 — Algoritmos Genéticos

> **Playlist:** Algoritmos Genéticos  
> **Objetivo:** Algoritmos de optimización basados en la evolución natural. Se usan cuando no hay datos disponibles pero hay heurísticas.

---

## ¿Qué son?

Algoritmos matemáticos de **optimización de propósito general** basados en mecanismos naturales de selección y genética. Dan excelentes soluciones en problemas complejos con muchos parámetros.

## Analogía con la evolución

| Teoría de la Evolución | Algoritmos Genéticos |
|----------------------|---------------------|
| Ecosistema / Ambiente | Problema |
| Individuo | Posible solución |
| Genotipo / Cromosoma | Descripción de la solución (cadena de bits) |
| Gen | Característica o atributo (porción del cromosoma) |
| Fenotipo | Función de aptitud (qué tan buena es la solución) |

---

## Estructura del Cromosoma

- Es una **cadena de bits**
- Se divide en **genes** (cada gen = una característica del problema)
- Los genes no tienen por qué tener la misma longitud

## Función de Aptitud (Fitness)

- `f(x) → R` — determina qué tan apto es el cromosoma como solución
- Cuanto mayor el valor, mejor la solución

---

## Flujo del Algoritmo

```
1. Generar Población Inicial
2. Selección
3. Cruzamiento
4. Mutación
5. ¿Criterio de paro cumplido?
   → SÍ: población final (identificar el mejor individuo)
   → NO: volver a Selección (la población mutada es la nueva población inicial)
```

**Términos:**
- **Vuelta / Ciclo:** cada iteración del bucle Selección → Cruzamiento → Mutación
- **Corrida:** la ejecución completa del algoritmo

---

## Operadores

### 1. Generar Población Inicial (GPI)

**Métodos:**
- **Al azar:** completamente aleatorio
- **Ad-hoc:** con conocimiento previo del dominio

**Parámetros de la población:**
- Cantidad de individuos
- Varianza (constante o variable)

---

### 2. Selección

Se seleccionan individuos para reproducirse. Métodos:

#### Torneo
- Se comparan de a pares usando la función fitness
- El ganador pasa. Un mismo individuo puede ganar varias veces
- **Desventaja:** si el mejor pelea contra el 2do mejor, puedo perder al 2do mejor

#### Ranking
- Se ordena la población por fitness y se seleccionan los mejores
- **Desventaja:** convergencia prematura (quedo atrapado en un máximo local)

#### Ruleta
- A cada individuo se le asigna un **porcentaje proporcional** a su fitness
- Se calcula la **probabilidad acumulada**
- Se tiran números aleatorios para seleccionar (mayor fitness = mayor probabilidad, pero todos tienen chance)

#### Control s/nro. esperado (Ruleta mejorada)
Evita que en una ruleta salgan todos malos:
1. **Preselección:** calcular promedio del fitness → `relación = f(Ix)/promedio`  
   La **parte entera** = cuántas veces tomo ese individuo (garantizado)
2. **Selección por ruleta:** usar la **mantisa** de esa relación como nueva función fitness para la ruleta

---

### 3. Cruzamiento

Se realiza sobre los individuos seleccionados. Opera **de a pares** (2 padres → 2 hijos).

#### Simple (1 punto de corte)
Se define un punto de corte; cada mitad va a un hijo diferente.  
**Regla:** no cortar por la mitad de un gen.

#### Multipunto
Más de un punto de corte.

#### Binomial – Máscara Complemento
Se define una máscara; las posiciones en 1 de la máscara van a un hijo y el complemento al otro.

#### Binomial – Máscara Doble
Una máscara distinta para cada hijo. Los genes pueden repetirse.

#### Binomial – Azar
Para cada posición se genera un random R y un umbral M:
- Si R ≤ M → tomo el gen del padre X
- Si R > M → tomo el gen del padre Y

Para el 2do hijo: complemento del resultado anterior, o nuevamente al azar.

---

### 4. Mutación

- Ocurre **después** del cruzamiento
- Simula alteraciones cromosómicas por agentes exógenos
- **Se activa pero no necesariamente se ejecuta** (depende de la probabilidad)

**Proceso:**
1. Generar random → ¿es ≤ probabilidad de mutación? → Si SÍ: mutar
2. Generar random de posición → esa posición del cromosoma cambia de valor

**Métodos de mutación:**

| Método | Descripción |
|--------|-------------|
| **Simple** | Probabilidad constante a lo largo de toda la corrida |
| **Adaptativa por convergencia** | `P_m = G(promedio[f(Ix)])` — cambia según la aptitud promedio |
| **Adaptativa por temperatura** | `P_m = G(cantidad de vueltas)` — ascendente o descendente |

---

### 5. Criterio de Paro

Se deja de iterar cuando:
- Se alcanza cierta cantidad de vueltas
- Se supera un tiempo límite
- `f(Ix) > Valor_objetivo`
- `Promedio[f(Ix)] ≈ Valor_objetivo`

> **Cuidado:** los últimos dos criterios pueden generar bucles infinitos si el valor nunca se alcanza.

---

## Identificar la Solución

**Teoría:** ejecutar fitness a todos los individuos de la última población → tomar el mejor → decodificar el cromosoma.

**Práctica:** guardar logs de distintas corridas → buscar el mejor individuo entre todas las corridas.

---

## Cromosoma y Función de Aptitud — Buenas Prácticas (para implementación)

**Cromosoma:**
- Tamaño fijo y longitud mínima
- Debe representar todas las posibles soluciones (**completitud**)
- No representar soluciones inválidas (**coherencia**)
- Todas las soluciones con misma probabilidad de ser generadas (**uniformidad**)
- Fácil de interpretar (**sencillez**)

**Función de aptitud:**
- Usar bien la heurística del problema
- Ser consistente con el cromosoma
- Pequeños cambios en características → pequeños cambios en valoración (**causalidad fuerte**)
- Manejar bien la penalización de soluciones inválidas:
  - Pena de muerte
  - Niveles de pena constantes
  - Penas adaptativas en el tiempo
  - Penas adaptativas por la aptitud de la población

---

## Resumen clave para el final

1. Los AG son para **optimización** con muchos parámetros, sin necesidad de datos históricos.
2. El **cromosoma** codifica una solución; el **fitness** la evalúa.
3. Flujo: **GPI → Selección → Cruzamiento → Mutación → ¿Paro?**
4. **Ruleta con control s/nro. esperado** = más completo (parte entera = selección garantizada; mantisa = ruleta).
5. La **mutación** evita la convergencia prematura.
6. En producción: múltiples corridas, tomar el mejor individuo de todos los logs.

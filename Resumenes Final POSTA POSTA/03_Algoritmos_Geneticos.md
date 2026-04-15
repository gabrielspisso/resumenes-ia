# 03 — Algoritmos Genéticos

> **Playlist:** Algoritmos Genéticos  
> **Objetivo:** Algoritmos de optimización basados en la evolución natural. Se usan cuando no hay datos disponibles pero hay heurísticas.

---

## ¿Qué son?

Algoritmos matemáticos de **optimización de propósito general** basados en mecanismos naturales de selección y genética. Dan excelentes soluciones en problemas complejos con muchos parámetros.

### Cuando usarlos vs otros métodos
- Se aplican en problemas donde **no se pueden usar métodos matemáticos tradicionales** que garantizan óptimos
- Son ideales para universos de búsqueda **exponencialmente grandes** (combinaciones más allá de lo computable)
- Ejemplo: para un equipo de 10 personas con guardias mensuales, hay más combinaciones que átomos en el universo
- El algoritmo **no garantiza la mejor solución, sino una solución suficientemente buena** rápidamente

---

## Analogía con la Evolución

### Teoría de la evolución (Darwin, 1859)
La teoría de evolución por **selección natural** establece postulados clave:

1. **Las formas de vida evolucionan** — cambios graduales y lentos a través de generaciones
2. **Selección natural** — hay una competencia por la supervivencia
3. **Ecosistema/Ambiente** — establece requisitos para sobrevivir
4. **Población** — conjunto de individuos que compiten
5. **Herencia** — los genes se heredan (cromosomas contienen genes)
6. **Supervivencia del más apto** — quienes están mejor adaptados tienen más probabilidades de reproducirse

### Mapeo a Algoritmos Genéticos

| Teoría de la Evolución | Algoritmos Genéticos |
|----------------------|---------------------|
| Ecosistema / Ambiente | Problema a resolver |
| Individuo | Posible solución |
| Genotipo / Cromosoma | Descripción de la solución (cadena de bits) |
| Gen | Característica o atributo (porción del cromosoma) |
| Fenotipo | Función de aptitud (evaluación de qué tan buena es) |
| Supervivencia del más apto | Selección para reproducción |

---

## Estructura del Cromosoma

- Es una **cadena de bits** (generalmente binaria)
- Se divide en **genes** (cada gen = una característica del problema)
- Los genes **no tienen por qué tener la misma longitud**, depende de cuántos valores pueda tomar esa característica
  - Ejemplo: característica binaria (0 o 1) = 1 posición; característica con 3 estados = 2 posiciones
- Se pueden trabajar con **cromosomas compuestos** para problemas más complejos
  - Ejemplo: problema del pesecito (zebra puzzle) — cromosoma compuesto donde cada persona tiene su propio conjunto de genes

### Característica vs Gen
- **Gen**: una característica o atributo
- **Posición**: cada 0 o 1 en el cromosoma
- Importante: no confundir posición con gen (un gen puede ocupar varias posiciones)

## Función de Aptitud (Fitness)

- `f(x) → R` — determina qué tan apto es el cromosoma como solución
- Cuanto mayor el valor, mejor la solución (maximización)
- Es una **función compleja** que depende del problema
- Debe ser **consistente** con la estructura del cromosoma
- Debe **penalizar soluciones inválidas** adecuadamente

### Aspectos importantes de la Función de Aptitud
- Debe capturar la heurística del problema correctamente
- Pequeños cambios en características → pequeños cambios en valoración (**causalidad fuerte**)
- Manejo de **penalizaciones** para soluciones inválidas:
  - Pena de muerte (valor muy bajo)
  - Niveles de pena constantes
  - Penas adaptativas en el tiempo
  - Penas adaptativas por la aptitud de la población

---

## Terminología Clave

- **Vuelta / Ciclo**: cada iteración del bucle Selección → Cruzamiento → Mutación
- **Corrida**: la ejecución completa del algoritmo (desde población inicial hasta criterio de paro)
  - Una corrida **contiene muchas vueltas**
  - Aclaración importante para los exámenes: "vueltas" ≠ "corridas"

---

## Flujo del Algoritmo

```
1. Generar Población Inicial (GPI)
2. Selección
3. Cruzamiento
4. Mutación
5. ¿Criterio de paro cumplido?
   → SÍ: población final (identificar el mejor individuo)
   → NO: volver a Selección (la población mutada es la nueva población)
```

### Concepto de "Navegación en la Sabana de Soluciones"
El algoritmo genético "navega en una sabana de soluciones":
- Todas las combinaciones posibles = universo de soluciones
- El AG no recorre exhaustivamente; **salta** de un punto a otro
- Puede quedar atrapado en un **máximo local** (buena solución, pero no la mejor)
- Las múltiples corridas y operadores permiten escapar de máximos locales
- **En distintas corridas obtiene distintos valores**, la solución final es el mejor entre todas

---

## Operadores

### 1. Generar Población Inicial (GPI)

**Métodos:**
- **Al azar**: completamente aleatorio (simple pero puede generar inválidos)
  - Si la función fitness está bien diseñada, los inválidos serán penalizados
- **Ad-hoc**: con conocimiento previo del dominio (valores válidos seleccionados)

**Parámetros de la población:**
- Cantidad de individuos
- Varianza (constante o variable)
  - Generalmente se trabaja con **población constante** en toda la ejecución

---

### 2. Selección

Se seleccionan individuos para reproducirse (crear padres). Métodos:

#### Torneo
- Se comparan de a **pares** usando la función fitness
- El ganador pasa al siguiente ciclo
- Un mismo individuo puede ganar varias veces
- **Ventaja**: simple, el mejor siempre gana
- **Desventaja**: si el mejor pelea contra el 2do mejor, se pierde al 2do mejor
  - Ejemplo: si 1 (f=100) pelea con 5 (f=95), gana 1; pero si 5 no participa de nuevo, se pierde esa buena solución

#### Ranking
- Se ordena la población por fitness y se seleccionan los mejores (ej: 1°, 2°, 3°, 4°...)
- **Ventaja**: garantiza quedarse con los mejores
- **Desventaja**: **convergencia prematura** (máximo local)
  - Si todos los seleccionados tienen características similares, la población pierde heterogeneidad
  - Esto limita la exploración del espacio de soluciones

#### Ruleta
- A cada individuo se le asigna una **porción proporcional a su fitness**
- Se calcula la **probabilidad acumulada** (acumulativa)
- Se tiran números aleatorios para seleccionar
- **Mayor fitness = mayor probabilidad, pero todos tienen chance**
- **Desventaja**: puede salir una mala selección (muchos individuos malos)
- **Ventaja**: mantiene heterogeneidad en la población

#### Control s/nro. Esperado (Ruleta Mejorada)
Evita que en una ruleta salgan todos malos, combinando lo mejor de ambas estrategias:

1. **Preselección garantizada:** 
   - Calcular promedio del fitness → `relación = f(Ix)/promedio`  
   - La **parte entera** = cuántas veces se toma ese individuo (garantizado)
   - Ejemplo: si relación = 2,8 → se toma 2 veces ese individuo

2. **Selección complementaria por ruleta:** 
   - Usar la **mantisa** (parte decimal) como nueva función fitness para ruleta
   - Llenar los lugares que faltan usando ruleta sobre las mantisas
   - **Resultado**: se garantizan los buenos, después se usan probabilidades para llenar

**Resumen de métodos:**
- **Torneo**: simple, puede perder buenos elementos
- **Ranking**: garantiza los mejores, pero riesgo de convergencia prematura
- **Ruleta**: permite variedad, pero puede salir mala selección
- **Control s/nro. esperado**: combina ventajas de ranking (garantía) y ruleta (variedad)

---

### 3. Cruzamiento

Se realiza sobre los individuos seleccionados. Opera **de a pares** (2 padres → generalmente 2 hijos).

**Regla importante**: no cortar por la mitad de un gen, sino respetando los límites de cada característica.

#### Simple (1 punto de corte)
Se define un punto de corte; cada mitad va a un hijo diferente.  
```
Padre 1: [1 0 1 0 | 1 1 0 1]  →  Hijo 1: [1 0 1 0 | 1 1 0 1] (de Padre 2)
Padre 2: [0 1 0 1 | 0 0 1 0]  →  Hijo 2: [0 1 0 1 | 1 1 0 1] (de Padre 1)
```

#### Multipunto
Más de un punto de corte. Las características pueden alternarse entre más puntos.

#### Binomial – Máscara Complemento
Se define una máscara; las posiciones en 1 van a un hijo y el complemento al otro.
- **Ventaja/Característica**: es equivalente a una cruza multipunto con puntos de corte variables

#### Binomial – Máscara Doble
Una máscara distinta para cada hijo. **Los genes pueden repetirse** (característica única).
- Ejemplo: Padre X puede contribuir la misma característica 2 veces

#### Binomial – Azar
Para cada posición se genera un `random R` y un umbral `M`:
- Si `R ≤ M` → tomo el gen del padre X
- Si `R > M` → tomo el gen del padre Y

Para el 2do hijo: 
- **Opción 1**: complemento del resultado anterior (las características no repetidas van al otro)
- **Opción 2**: nuevamente al azar (permite repetición)

---

### 4. Mutación

- Ocurre **después** del cruzamiento
- Simula alteraciones cromosómicas por agentes exógenos
- **Se activa pero no necesariamente se ejecuta** (depende de la probabilidad)

**Proceso:**
1. **Activación**: se evalúa probabilidad de mutación
2. **Ejecución** (si se activa y tira favorable):
   - Generar random de posición → esa posición del cromosoma cambia de valor
   - Ejemplo: si es binario, 0 → 1 o 1 → 0

**Importante**: 
- Cada ciclo el operador se **activa** (verifica si ejecutar)
- Pero puede no **ejecutarse** (si el random no cumple la condición)
- Si no se ejecuta, la población mutada = población cruzada

**Métodos de mutación:**

| Método | Descripción | Fórmula/Característica |
|--------|-------------|----------------------|
| **Simple** | Probabilidad constante | Misma Pm en toda la corrida |
| **Adaptativa por convergencia** | Aumenta cuando hay convergencia | `P_m = G(promedio[f(Ix)])` — cambia según aptitud promedio |
| **Adaptativa por temperatura (Ascendente)** | Aumenta con el tiempo | `P_m = G(cantidad de vueltas)` — Pm baja al inicio, sube al final |
| **Adaptativa por temperatura (Descendente)** | Decrece con el tiempo | Lo opuesto a ascendente — Pm alta al inicio, baja al final |
| **Adaptativa por desvío estándar** | Aumenta si la población es homogénea | Cuanto más parecidos son los fitness, más alta la Pm |

### Propósito de la Mutación
- **Evita la convergencia prematura** (quedarse en máximo local)
- Introduce variabilidad incluso cuando la población es muy similar
- Si Pm es muy baja: riesgo de convergencia prematura
- Si Pm es muy alta: el algoritmo se comporta como búsqueda aleatoria

---

### 5. Criterio de Paro

Se deja de iterar cuando se cumple **alguno** de:
- Se alcanza cierta cantidad de vueltas (ciclos máximos)
- Se supera un tiempo límite
- `f(Ix) > Valor_objetivo` (para maximización)
- `Promedio[f(Ix)] ≈ Valor_objetivo`

> **Cuidado:** los últimos dos criterios pueden generar bucles infinitos si el valor nunca se alcanza.
> **Buena práctica**: combinar criterios (ej: máximo de vueltas + aptitud target)

---

## Identificar la Solución

### Teoría
Ejecutar fitness a todos los individuos de la última población → tomar el mejor → decodificar el cromosoma

### Práctica (Lo que realmente funciona)
**Importante**: la mejor solución **no siempre está en la población final**
- Guardar **logs de distintas corridas** (múltiples ejecuciones)
- En cada ciclo, registrar el mejor individuo encontrado
- Buscar el mejor individuo **entre todos los logs y ciclos**
- Decodificar ese cromosoma para obtener la solución final

**Motivo**: a veces la convergencia elimina buenos individuos en ciclos posteriores. Por eso se hacen **múltiples corridas** con los mismos parámetros

---

## Cromosoma y Función de Aptitud — Buenas Prácticas

### Diseño del Cromosoma

**Debe tener:**
- **Tamaño fijo** y longitud mínima
- **Completitud**: debe representar todas las posibles soluciones
- **Coherencia**: no representar soluciones inválidas (o penalizarlas bien)
- **Uniformidad**: todas las soluciones con igual probabilidad de ser generadas
- **Sencillez**: fácil de interpretar y decodificar

### Diseño de la Función de Aptitud

- **Usar bien la heurística** del problema
- **Ser consistente** con el cromosoma
- **Causalidad fuerte**: pequeños cambios en características → pequeños cambios en valoración
- **Manejo de penalizaciones**:
  - Pena de muerte (valores muy bajos)
  - Niveles de pena constantes
  - Penas adaptativas en el tiempo
  - Penas adaptativas por la aptitud de la población

---

## Ejemplo Práctico: Problema del Pesecito (Zebra Puzzle)

### Enunciado
- 5 casas de 5 colores diferentes
- 5 personas de nacionalidades diferentes
- Cada persona: una bebida, marca de cigarrillo, mascota
- Múltiples pistas (el británico vive en casa roja, etc.)
- **Pregunta**: ¿Quién es dueño del pesecito?

### Modelado con Algoritmo Genético

**Cromosoma compuesto** (porque hay múltiples dimensiones):
- Cada "bloque" representa a una persona (británico, sueco, danés, alemán, noruego)
- Dentro de cada bloque: características codificadas (número de casa, color, bebida, cigarrillo, mascota)
- Cada gen es una posición binaria que se decodifica

**Función de Aptitud**:
- **Aumenta** si se cumplen las pistas
- **Disminuye** si hay inconsistencias (valores inválidos, combinaciones prohibidas)
- Valida combinaciones válidas (ej: un gen con valor 111 puede ser inválido)

**Resultado**: el algoritmo evoluciona hacia soluciones que cumplen más pistas, hasta encontrar la solución completa

---

## Ejemplo Práctico: Sistema de Guardias Médicas

### Contexto del Problema
- Servicio médico con N participantes
- Necesidad de organizar guardias mensuales
- Trabajo actual: manual, varias horas de coordinación
- Combinaciones posibles: para 10 personas con 8 guardias cada una = **más combinaciones que átomos en el universo**
- **Imposible evaluar exhaustivamente** todas las opciones

### Solución con Algoritmo Genético

**Mapeo del problema:**
- **Individuos**: calendarios posibles de guardias
- **Ambiente**: reglas y restricciones del servicio
- **Fitness negativo inicialmente**: número de violaciones de reglas

**Reglas del modelo:**
- Cantidad de días de guardia por persona
- Días prohibidos (francos obligatorios)
- Días asignados (debe estar de guardia)
- Distancia mínima entre guardias (ej: no 2 días seguidos)
- Particularidades por residencias (distancia mínima de 2 o 3 días)

**Parámetros de ejecución:**
- 100 individuos en población
- 1000 iteraciones máximas
- Fitness target: 0 (sin errores)
- Selección: ranking truncado
- Salto generacional: 0.5 (50% de renovación por ciclo)
- Cruzamiento: binomial
- Mutación: por desvío estándar (evita convergencia prematura)

**Resultados**:
- **Tiempo**: 7-93 segundos (depende de parámetros)
- **Convergencia**: se ve clara evolución (ej: -200 → -4 → 0 errores)
- **Éxito**: obtiene calendarios que respetan todas las restricciones
- **Nota**: si hay reglas contradictorias, el algoritmo puede quedar atrapado en mínimo local

---

## Patrones de Implementación (Orientado a Objetos)

### Enfoque Imperativo/Declarativo
El usuario especifica **qué** quiere, no **cómo**:
1. Instancia un objeto `GeneticAlgorithm`
2. Define propiedades: selección, cruzamiento, mutación, población
3. Llama a `start()` y `run()`

### Componentes Clave
- **Algoritmo de Selección**: implementa interfaz con `fitnessBlock`
- **Algoritmo de Cruzamiento**: recibe 2 individuos, devuelve vector de hijos
- **Algoritmo de Mutación**: evalúa si mutar, ejecuta cambios
- **Población**: no necesita ser de clase específica, solo debe entender mensajes

### Ventaja del Diseño
- **No limita tipos**: cualquier objeto que implemente la interfaz funciona
- **Flexible**: permite combinar distintos operadores
- **Reutilizable**: mismo framework para distintos problemas

---

## Resumen Clave para el Final

1. **Los AG son para optimización** con muchos parámetros, sin necesidad de datos históricos, cuando el espacio de soluciones es exponencialmente grande.

2. **El cromosoma codifica una solución**; el **fitness la evalúa**.

3. **Flujo**: **GPI → Selección → Cruzamiento → Mutación → ¿Paro?**

4. **Ruleta con control s/nro. esperado** = más completo (garantiza los buenos + variedad probabilística).

5. **La mutación evita la convergencia prematura** (máximos locales).

6. **En producción**:
   - Múltiples corridas con los mismos parámetros
   - Guardar logs de cada ciclo
   - Tomar el mejor individuo de todos los logs
   - Decodificar esa solución

7. **El algoritmo busca soluciones suficientemente buenas**, no necesariamente la mejor, lo que lo hace útil en espacios de búsqueda exponenciales.

8. **Importante**: distinguir entre **vueltas** (ciclos individuales) y **corridas** (ejecución completa).

---

## 📝 Cambios respecto al original

### Información Agregada

**Conceptos y Contexto:**
- Historia y teoría de la evolución (Darwin, postulados, herencia genética)
- Explicación clara de cuándo usar AG vs métodos tradicionales
- Concepto de "navegación en sabana de soluciones" y máximos locales
- Distinción entre vueltas y corridas

**Métodos de Selección:**
- Ventajas y desventajas específicas de cada método
- Explicación detallada de la "convergencia prematura"
- Pasos concretos del método de Control s/nro. Esperado con valores numéricos

**Mutación:**
- Explicación de que se "activa pero no se ejecuta"
- Método adaptativo por desvío estándar (no estaba en original)
- Ejemplos de cómo afecta Pm a la búsqueda

**Cruzamiento:**
- Ejemplos visuales de cómo funciona cada tipo
- Aclaración sobre cuándo se pueden repetir genes

**Nuevas Secciones:**
- Ejemplos prácticos: Problema del Pesecito y Sistema de Guardias Médicas
- Patrones de Implementación (orientado a objetos)
- Mejora en la sección de "Identificar la Solución" con énfasis en logs y múltiples corridas
- Terminología Clave mejorada y contextualizada

**Detalles Técnicos:**
- Parámetros específicos en ejemplos (1000 iteraciones, 0.5 salto generacional, etc.)
- Números reales de convergencia (ej: -200 → -4 → 0)
- Tiempos de ejecución (7-93 segundos)
- Cómo funciona la decodificación del cromosoma

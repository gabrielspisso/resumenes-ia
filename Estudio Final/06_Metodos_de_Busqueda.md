# 06 — Métodos de Búsqueda

> **Playlist:** Métodos de Búsqueda  
> Fuente: Clase 2 (Métodos de Búsqueda), Para el Coloquio, Tips ejercicios

---

## Representación del Problema

Todo problema se formaliza como **búsqueda en un espacio de estados**:

| Elemento | Descripción |
|---------|-------------|
| **Estado** | "Foto" del sistema en un momento dado; contiene toda la información que define la situación |
| **Estado inicial** | Punto de partida |
| **Estados intermedios** | Se transitan para alcanzar los objetivos |
| **Estados finales / solución** | Los que queremos alcanzar |
| **Operadores / reglas** | Acciones que vinculan un estado padre con un estado hijo |

**Proceso de solución:** partiendo del estado inicial, se aplican operadores para transitar entre estados hasta llegar a un estado solución, usando una **estrategia de control**.

---

## Métodos SIN información del dominio (Búsqueda Ciega)

No hay información que diga si un estado es mejor que otro. Solo se conocen los estados y cuáles son solución.

---

### Primero en Amplitud (BFS — Breadth First Search)

- Estructura: **cola FIFO** (primero en entrar, primero en salir)
- Recorre **todo un nivel** antes de bajar al siguiente
- **Garantiza encontrar la solución** (si existe y el espacio es finito)
- Útil: cuando existen pocos nodos finales cercanos a la raíz
- **Problema:** usa mucha memoria
- **Finaliza cuando:** recorre todo el árbol

---

### Primero en Profundidad (DFS — Depth First Search)

- Estructura: **pila LIFO** (último en entrar, primero en salir)
- Explora **toda una rama** hasta el fondo antes de retroceder
- Usa **poca memoria**
- Útil: cuando hay muchos nodos solución alejados de la raíz
- **Problema:** no recorre todo el árbol → **no garantiza la solución óptima**
- **Finaliza cuando:** encuentra el primer estado final

---

### Generación y Prueba

- Variante de Primero en Profundidad
- Explora ramas pero **continúa hasta recorrer TODOS los nodos**
- Permite encontrar **todos** los estados solución
- Útil: en problemas sencillos
- **Problema:** en problemas complejos puede consumir mucho tiempo
- **Finaliza cuando:** encuentra el primer estado final (o todos, según enunciado)

---

### Bidireccional

- Dos búsquedas simultáneas: **top-bottom** (desde inicial) y **bottom-up** (desde solución)
- Al menos una de ellas debe ser en **amplitud**
- Se debe conocer el estado inicial **y** el estado final
- Para cuando ambas búsquedas se encuentran en un estado intermedio común
- **Complejidad ≈** dos búsquedas unidireccionales

---

## Métodos CON información del dominio (Búsqueda Heurística)

Se usa una **función heurística h(n)** que indica qué tan prometedor es un nodo.  
**Mayor valor heurístico → nodo más deseable.**

Más eficientes, pero no exhaustivos (no recorren todo el árbol).

---

### Escalada Simple (Hill Climbing)

- Genera el **primer hijo** y lo compara con el nodo actual
- Si el hijo tiene **mayor heurística** → pasa a ser el nodo actual
- Si ningún hijo es mejor → **se detiene** (puede quedarse en máximo local)
- **Sin retroceso** → puede quedar atrapado
- Memoria: media
- **NO garantiza solución**

---

### Escalada Máxima Pendiente (Steepest Ascent)

- Genera **todos los hijos** y se queda con el **mejor**
- Compara el mejor hijo con el nodo actual; si no supera → se detiene
- También **sin retroceso** → también puede quedar en máximo local
- Memoria: media-alta
- **NO garantiza solución**

---

### Primero el Mejor (Best First Search)

- Usa dos listas:
  - **LNA (Nodos Abiertos):** generados pero no recorridos, ordenados por heurística ↓
  - **LNC (Nodos Cerrados):** ya recorridos
- Siempre selecciona el **mejor nodo de LNA** (sin importar la profundidad)
- **Tiene retroceso** → puede escapar de máximos locales
- **Siempre encuentra solución** si existe
- Puede usar mucha memoria (mantiene muchos nodos abiertos)

**Pasos:**
1. LNA = {estado inicial}, LNC = {}
2. Tomar el mejor de LNA → mover a LNC
3. Si es solución → fin. Si no → generar hijos, agregarlos a LNA (ordenados)
4. Repetir

---

### Beam Search (N)

- Como Primero el Mejor pero con **memoria limitada**
- Solo se guardan los **N mejores nodos** en LNA (N = parámetro del algoritmo)
- Los nodos descartados **no vuelven** a la lista
- No necesita que el hijo supere al padre para visitarlo (≠ escalada)
- Comportamiento similar a Escalada Máxima Pendiente pero sin requerir que supere al padre
- **No garantiza solución** (depende de N)
- Mejora mucho el uso de memoria respecto a Primero el Mejor

---

### A* (A Estrella)

- Como Primero el Mejor pero incluye **costo acumulado del camino**
- Valor para ordenar LNA: `f(n) = g(n) + h(n)` donde:
  - `g(n)` = costo acumulado del camino hasta n (penaliza caminos largos)
  - `h(n)` = heurística (estimación del beneficio/costo restante)
- Cuanto más largo el camino, más penalizado
- **Garantiza encontrar la solución óptima** si la heurística es admisible

---

## Tabla Comparativa

### Sin información de dominio

| Método | Estructura | Recorre por | Garantiza solución | Finaliza cuando |
|--------|-----------|-------------|-------------------|----------------|
| Primero en Amplitud | Cola FIFO | Niveles | Sí | Recorre todo el árbol |
| Primero en Profundidad | Pila LIFO | Ramas | No (no óptima) | Primer estado final |
| Generación y Prueba | Pila LIFO | Ramas | Sí (todas) | Recorre todos los nodos |
| Bidireccional | Cola (al menos 1) | Niveles/Ramas | Sí | Estado intermedio común |

### Con información de dominio

| Método | Heurística | Retroceso | Garantiza solución | Criterio siguiente |
|--------|-----------|----------|--------------------|-------------------|
| Escalada simple | Sí | No | No | Primer hijo > padre |
| Escalada máx. pendiente | Sí | No | No | Mejor hijo > padre |
| Primero el mejor | Sí | Sí (LNA) | Sí | Mejor nodo de LNA |
| Beam Search | Sí | Depende de N | No | Mejor nodo de LNA (limitada a N) |
| A* | Sí (+ costo) | Sí (LNA) | Sí (óptima) | Mejor nodo: h(n) + g(n) |

---

## Tips para resolver ejercicios

**Primero en Amplitud:**
- Si existe solución, siempre la encuentra
- Recorre todo un nivel y luego baja al siguiente
- Termina cuando recorre todo el árbol

**Primero en Profundidad:**
- Puede encontrar solución pero no garantiza la óptima
- Recorre toda una rama; si no hay solución, vuelve al último nodo con otro hijo

**Generación y Prueba:**
- Igual que profundidad pero continúa hasta recorrer todos los nodos

**Escalada Simple:**
- Puedo NO encontrar solución (si la función no es estrictamente creciente)
- El valor del nodo hijo > padre → lo visito. Si no hay ningún hijo mayor → termina

**Escalada Máxima Pendiente:**
- Igual al anterior pero genera todos los hijos y elige el más adecuado

**Primero el Mejor:**
- Siempre encuentra solución
- Acomodar los nodos abiertos siempre por valor heurístico

**Beam Search N=n:**
- Igual al Primero el Mejor pero limita los nodos abiertos a n
- Los que quedaron fuera en un paso no vuelven más

**A*:**
- Siempre encuentra solución
- Igual al Primero el Mejor pero con **costos en las aristas** (se descuenta del heurístico)

---

## Trampas del examen

- **Escalada simple y máxima pendiente:** sin retroceso → pueden quedar en máximo local → NO garantizan solución
- **Primero el Mejor:** tiene retroceso (LNA), garantiza encontrar solución
- **Beam Search:** como Primero el Mejor pero limitado → puede no encontrar solución
- **A*:** igual que Primero el Mejor + costos en aristas → garantiza solución óptima
- En Escalada, solo seleccionan hijos **estrictamente mejores** que el padre (no igual)
- Bidireccional: al menos **una** de las dos búsquedas debe ser en amplitud
- La función heurística evalúa nodos (beneficio); el costo va en las aristas (penalización)

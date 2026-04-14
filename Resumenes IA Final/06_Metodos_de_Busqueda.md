# 06 — Métodos de Búsqueda

> **Playlist:** Métodos de Búsqueda  
> **Objetivo:** Resolver problemas formalizándolos como búsqueda en un espacio de estados.

---

## Modelar el Problema

Todo problema se formaliza como **búsqueda en un espacio de estados**:
- **Estado:** "foto" del sistema en un momento dado
- **Estado inicial:** punto de partida
- **Estados intermedios:** caminos posibles
- **Estados finales / solución:** lo que queremos alcanzar
- **Operadores / reglas:** vinculan un estado padre con un estado hijo

**Proceso de solución:** partiendo del estado inicial, se aplican reglas para transitar entre estados hasta llegar a un estado solución, usando una **estrategia de control**.

---

## Métodos SIN información del dominio (Búsqueda Ciega)

No hay información que diga si un estado es mejor que otro. Solo se conocen los estados y cuáles son solución.

### Primero en Amplitud (BFS)
- Estructura: **cola FIFO** (primero en entrar, primero en salir)
- Recorre nodo por nodo nivel a nivel
- **Garantiza encontrar la solución** (si existe y el espacio es finito)
- Útil: pocos nodos finales, cercanos a la raíz
- **Problema:** usa mucha memoria

### Primero en Profundidad (DFS)
- Estructura: **pila LIFO** (último en entrar, primero en salir)
- Explora una rama hasta el fondo antes de retroceder
- Usa poca memoria
- Útil: muchos nodos solución alejados de la raíz
- **Problema:** no recorre todo → **no garantiza solución óptima**

### Generación y Prueba
- Recorre todos los nodos (como BFS pero por ramas)
- Permite encontrar **todos** los estados solución
- Adecuado para problemas sencillos
- **Problema:** en problemas complejos puede ser muy lento

### Bidireccional
- Dos búsquedas simultáneas: **top-bottom** (desde inicial) y **bottom-up** (desde solución)
- Al menos una debe ser en **amplitud**
- Para cuando se encuentran en un estado intermedio común
- Complejidad ≈ dos búsquedas unidireccionales sobre un grafo de la mitad del tamaño

---

## Métodos CON información del dominio (Búsqueda Heurística)

Se usa una **función heurística h(n)** que indica qué tan prometedor es un nodo.  
**A mayor valor heurístico → nodo más deseable**

Aumenta la eficiencia, sacrificando exhaustividad.

### Escalada Simple (Hill Climbing Simple)
- Se genera el primer hijo y se compara con el nodo actual
- Si el hijo tiene **mayor** heurística → pasa a ser el nodo actual
- Si ningún hijo es mejor → se detiene
- **Ventajas:** poca memoria
- **Problemas:**
  - Puede perderse nodos mejores (solo mira el primer hijo)
  - **No tiene retroceso** → puede quedar atrapado en un **máximo local**

### Escalada Máxima Pendiente (Steepest Ascent)
- Genera **todos** los hijos y se queda con el **mejor**
- Compara el mejor hijo con el nodo actual
- Si el mejor hijo no supera al actual → se detiene
- **Problema:** sin retroceso → también puede quedar en máximo local

### Primero el Mejor (Best First Search)
- Usa dos listas:
  - **LNA (Nodos Abiertos):** generados pero no recorridos, ordenados por heurística
  - **LNC (Nodos Cerrados):** ya recorridos
- Siempre selecciona el mejor nodo de LNA (sin importar la profundidad)
- **Tiene retroceso** → puede escapar de máximos locales
- **Garantiza encontrar solución** si existe

**Pasos:**
1. Inicializar LNA con el estado inicial, LNC vacía
2. Tomar el mejor nodo de LNA → mover a LNC
3. Si es solución → fin. Si no → generar hijos, agregarlos a LNA (ordenados)
4. Repetir

### Beam Search (N=1)
- Como Primero el Mejor pero con **memoria limitada**
- Solo se guardan los **N mejores nodos** en LNA (N = parámetro)
- Comportamiento similar a Escalada Máxima Pendiente pero **sin necesidad de que supere al nodo actual**
- No garantiza solución (depende de N)

### A* (A Estrella)
- Como Primero el Mejor pero incluye **costo acumulado del camino**
- Valor para ordenar LNA: `f(n) = g(n) + h(n)` donde:
  - `g(n)` = costo acumulado del camino hasta n
  - `h(n)` = heurística (estimación del costo restante)
- Cuanto más largo el camino, más penalizado
- **Garantiza encontrar la solución óptima** (si la heurística es admisible)

---

## Tabla Comparativa

### Sin información de dominio

| Método | Recorre por… | Finaliza cuando… |
|--------|-------------|-----------------|
| Primero en amplitud | Niveles | Recorre todo el árbol |
| Generación y prueba | Ramas | Encuentra el primer estado final |
| Primero en profundidad | Ramas | Encuentra el primer estado final |
| Bidireccional | Niveles (al menos 1) | Encuentra estado intermedio común |

### Con información de dominio

| Método | ¿Retroceso? | ¿Garantiza solución? | Criterio siguiente estado |
|--------|------------|---------------------|--------------------------|
| Escalada simple | No | No | Primer hijo mejor que actual |
| Escalada máx. pendiente | No | No | Mejor de todos los hijos |
| Primero el mejor | Sí | Sí | Mejor nodo abierto (LNA) |
| Beam Search | Depende | No | Mejor nodo abierto (LNA limitada) |
| A* | Sí | Sí | Mejor nodo abierto + costo acumulado |

> **Escalada simple y máxima pendiente:** solo seleccionan hijos con heurística **estrictamente mejor** que el padre (nunca igual).

---

## Resumen clave para el final

1. Todo problema se modela como estados + operadores + estado inicial + estados solución.
2. **Sin heurística:** BFS (amplitud), DFS (profundidad), Gen & Prueba, Bidireccional.
3. **Con heurística:** Escalada Simple/Máxima Pendiente, Primero el Mejor, Beam Search, A*.
4. **Escalada:** sin retroceso, puede quedar en máximo local.
5. **Primero el Mejor:** tiene retroceso (LNA), garantiza encontrar solución.
6. **A*:** = Primero el Mejor + costo acumulado. Óptimo si la heurística es admisible.
7. **Beam Search:** Primero el Mejor con LNA limitada a N nodos.

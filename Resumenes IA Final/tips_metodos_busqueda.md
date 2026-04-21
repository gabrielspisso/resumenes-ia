# Tips — Métodos de Búsqueda (para el examen)

---

## Sin heurística (Búsqueda Ciega)

**BFS — Primero en Amplitud**
Cola FIFO. Recorre nivel por nivel. Garantiza encontrar la solución, pero usa mucha memoria.

> Ejemplo: simplemente escribís la secuencia de nodos visitados nivel por nivel. El nodo solución va en **negrita**.
> ```
> A, B, C, D, E, F, H, K, L, G, I, J, M
> ```

---

**DFS — Primero en Profundidad**
Pila LIFO. Baja por una rama hasta el fondo antes de retroceder. Usa poca memoria, pero no garantiza solución óptima.

> Ejemplo: cuando retrocede, el nodo anterior aparece de nuevo en la secuencia — eso es correcto, no es un error.
> ```
> A, B, E, G, E, B, F, B, H, I
> ```

---

**Generación y Prueba**
Recorre todos los nodos por ramas. Sirve para encontrar todas las soluciones. Muy lento en problemas complejos.

> Ejemplo: igual que DFS pero **no para** al encontrar la primera solución, sigue hasta recorrer todo el árbol.
> ```
> A, B, E, G, E, B, F, B, H, I, H, J, H, C, K, M, K, C, A, D, L, M
> ```

---

**Bidireccional**
Lanza dos búsquedas al mismo tiempo: una desde el inicio y otra desde la solución. Termina cuando se encuentran en el medio. Al menos una debe ser en amplitud (BFS).

> Ejemplo: dos columnas, una desde el inicio (top-down) y otra desde la solución (bottom-up). Parás cuando el mismo nodo aparece en las dos.
>
> | Top-down (desde inicio) | Bottom-up (desde solución) |
> |------------------------|---------------------------|
> | A | M |
> | B | K |
> | E | C |
> | **D** | **D** ← se encuentran acá |

---

## Con heurística (Búsqueda Informada)

**Escalada Simple**
Toma el primer hijo que supere al nodo actual y avanza. Sin retroceso → puede quedar atrapado en un máximo local.

> Ejemplo: 3 columnas. Generás UN solo hijo por fila. Si generado ≤ actual → Fin. Solo avanza si es **estrictamente mayor**.
>
> | Nodo actual | Nodo generado | ¿Generado > actual? |
> |-------------|--------------|---------------------|
> | A (h=50) | B (h=80) | S |
> | B (h=80) | E (h=90) | S |
> | E (h=90) | G (h=70) | N → Fin, sin solución |

---

**Escalada Máxima Pendiente**
Evalúa todos los hijos y avanza al mejor. Sin retroceso igual → mismo problema de máximos locales.

> Ejemplo: mismas 3 columnas, pero en "Nodo generado" ponés **todos** los hijos y elegís el mejor. Si el mejor no supera al actual → Fin.
>
> | Nodo actual | Nodo generado (todos) | ¿Mejor > actual? |
> |-------------|----------------------|-----------------|
> | A (h=50) | B(80), C(70), D(100) → mejor: D | S |
> | D (h=100) | L(80) → mejor: L | N → Fin |

---

**Primero el Mejor**
Mantiene una lista de nodos abiertos (LNA) ordenados por heurística. Tiene retroceso, garantiza encontrar la solución.

> Ejemplo: 4 columnas. LNA siempre ordenada de mayor a menor heurística. Cuando encontrás la solución, igual completás los nodos abiertos en esa última fila.
>
> | Nodo actual | ¿Es solución? | Nodos cerrados | Nodos abiertos (LNA) |
> |-------------|--------------|----------------|----------------------|
> | A | N | A | D(100), C(90), B(80) |
> | D | N | A, D | C(90), B(80), L(80) |
> | C | N | A, D, C | K(185), H(150), B(80), L(80) |
> | K | N | A, D, C, K | M(200), H(150), B(80), L(80) |
> | M | **S** | A, D, C, K, M | H(150), B(80), L(80) |
> | FIN | | | |

---

**Beam Search (N = lo que diga el ejercicio)**
Igual que Primero el Mejor pero la LNA tiene un límite de N nodos. Más eficiente en memoria, no garantiza solución.

> Ejemplo con N=1: al generar los hijos solo conservás el mejor y **tachás los demás**. Los descartados desaparecen para siempre.
>
> | Nodo actual | ¿Es solución? | Nodos cerrados | Nodos abiertos (LNA, máx N=1) |
> |-------------|--------------|----------------|-------------------------------|
> | A | N | A | D(100), ~~C(90), B(80)~~ |
> | D | N | A, D | L(80) |
> | L | N | A, D, L | M(200) |
> | M | **S** | A, D, L, M | — |
> | FIN | | | |

---

**A\***
Igual que Primero el Mejor pero ordena por `f(n) = g(n) + h(n)` (costo acumulado del camino + heurística). Garantiza la solución óptima.

> Ejemplo: igual que Primero el Mejor pero los valores en LNA son f(n) = g(n) + h(n). Los valores cambian entre iteraciones porque g(n) crece con la profundidad — puede pasar que un nodo que antes parecía bueno ahora quede más abajo en la lista.
>
> | Nodo actual | ¿Es solución? | Nodos cerrados | Nodos abiertos (f = g + h) |
> |-------------|--------------|----------------|---------------------------|
> | A | N | A | D(90), C(70), B(50) |
> | D | N | A, D | C(70), B(50), L(40) |
> | C | N | A, D, C | K(125), H(90), B(50), L(40) |
> | K | N | A, D, C, K | H(110), M(80), B(50), L(50) |
> | H | N | A, D, C, K, H | I(200), J(150), M(80), B(50), L(50) |
> | I | **S** | A, D, C, K, H, I | — |
> | FIN | | | |

---

## Cosas importantes que te pueden salvar mañana

- En **Escalada** (ambas): si el nodo generado tiene la **misma heurística** que el actual → **NO**, termina. Solo avanza si es **estrictamente mayor**.

- En **Primero el Mejor y Beam Search**: cuando encontrás la solución **igual completás los nodos abiertos** en esa última fila, no los dejás vacíos.

- **Primero el Mejor, Beam Search y A\* pueden encontrar soluciones distintas** para el mismo problema — eso es correcto.

- **Beam Search** no garantiza solución: si los N nodos que sobreviven no llevan a ninguna solución, el algoritmo termina sin encontrar nada.

- En **Bidireccional**, al menos una de las dos búsquedas debe ser en **amplitud** (BFS).

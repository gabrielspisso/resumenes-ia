# 06 — Métodos de Búsqueda

> **Playlist:** Métodos de Búsqueda  
> **Objetivo:** Resolver problemas formalizándolos como búsqueda en un espacio de estados.

---

## Modelar el Problema

Todo problema se formaliza como **búsqueda en un espacio de estados**:
- **Estado:** "foto" del sistema en un momento dado. Conjunto de información que describe la situación completa del sistema en un instante específico.
- **Estado inicial:** punto de partida del sistema
- **Estados intermedios:** caminos posibles por los que se transita
- **Estados finales / solución:** lo que queremos alcanzar (puede haber múltiples estados solución)
- **Operadores / reglas:** vínculos entre un estado padre y un estado hijo. Representan las transiciones posibles entre estados.

### Espacio de estados
El conjunto de todos los estados posibles se denomina **espacio de estados** o **dominio**. Puede ser:
- **Finito:** se pueden conocer todos los estados posibles
- **Infinito:** no es posible numerar todos los estados posibles

**Proceso de solución:** partiendo del estado inicial, se aplican reglas para transitar entre estados hasta llegar a un estado solución, usando una **estrategia de control**. La estrategia de control es el conjunto de técnicas que nos permite elegir qué reglas aplicar en cada momento.

---

## Métodos SIN información del dominio (Búsqueda Ciega)

No hay información complementaria del dominio que indique si un estado es mejor que otro. Solo se conocen los estados posibles y cuáles son estados solución.

**Característica común:** estos métodos aplican una **búsqueda exhaustiva**, buscando el camino sin contar con información a priori sobre el mejor camino posible.

### Primero en Amplitud (BFS - Breadth First Search)
- **Estructura:** cola **FIFO** (primero en entrar, primero en salir)
- **Recorrido:** nodo por nodo, nivel a nivel. Se generan todos los nodos de un nivel antes de pasar al siguiente.
- **Garantiza encontrar la solución** si existe y el espacio es finito
- **Encontrará la solución óptima** si existen múltiples soluciones (enumera todas)
- **Útil cuando:** pocos nodos finales cercanos a la raíz
- **Problemas:** 
  - **Usa mucha memoria:** recorre todo el árbol de manera exhaustiva
  - Ejemplo: con nodos de 100 bytes cada uno y 4 hijos por nodo, en nivel 14 necesita ~25 GB de memoria

### Primero en Profundidad (DFS - Depth First Search)
- **Estructura:** pila **LIFO** (último en entrar, primero en salir)
- **Recorrido:** explora una rama completamente hasta el fondo antes de retroceder. El último nodo generado es el primero en ser analizado.
- **Usa poca memoria:** no genera todo el árbol, solo la rama actual
- **Útil cuando:** muchos nodos solución alejados de la raíz
- **Problemas:** 
  - **No recorre todo** → **no garantiza solución óptima**
  - Puede encontrar una solución subóptima si hay varias
  - Requiere especificar límite de profundidad para evitar ciclos infinitos

### Generación y Prueba
- **Recorrido:** combina profundidad y amplitud. Recorre de una rama por vez (como DFS) pero luego genera nuevas ramas hasta recorrer todo el árbol (como BFS).
- **Permite encontrar TODOS los estados solución**, no solo el primero
- **Adecuado para:** problemas sencillos
- **Problemas:** 
  - En problemas complejos puede ser muy lento
  - Consume más memoria que DFS pero menos que BFS (para algunos casos)
  - Permite identificar la mejor solución comparando todas

### Primero en Profundidad Iterativa
- Variante que combina BFS y DFS
- Realiza búsquedas en profundidad iterativas con límites crecientes
- Garantiza solución óptima con memoria similar a DFS

### Bidireccional
- **Estrategia:** dos búsquedas simultáneas
  - **Top-bottom:** desde el estado inicial hacia la solución
  - **Bottom-up:** desde el estado solución hacia el inicial
- **Requisito:** al menos una búsqueda debe usar amplitud
- **Se detiene cuando:** se encuentran en un estado intermedio común, permitiendo recrear el camino
- **Ventaja:** complejidad ≈ dos búsquedas unidireccionales sobre un grafo de la mitad del tamaño
- **Requisito de conocimiento:** necesita conocer tanto estado inicial como estado final

---

## Métodos CON información del dominio (Búsqueda Heurística)

Se usa una **función heurística h(n)** que proporciona información del dominio indicando qué tan prometedor/deseable es un nodo.

**Palabra origen:** del griego "eureka" (descubrir)

### Ventajas y desventajas de las heurísticas

**Ventajas:**
- Aumentan significativamente la **eficiencia** del proceso de búsqueda
- Reducen drásticamente memoria y tiempo requeridos
- Permiten resolver problemas con espacios de búsqueda exponenciales

**Desventajas:**
- Sacrifican la **exhaustividad:** no garantizan encontrar la solución óptima
- Pueden obtener soluciones "suficientemente buenas" pero no necesariamente las mejores
- Dependen de la calidad de la heurística: si la función heurística es pobre, los resultados pueden serlo también

**Aplicaciones comunes:**
- Búsqueda de rutas de viaje (exponencial en distancia)
- Verificación automática de software (SAGE - dinámicamente genera el árbol de ejecución)
- Sistemas expertos tradicionales
- Problemas de optimización (batería en celulares, etc.)

### Representación de la función heurística

La información heurística puede incluirse en:

1. **Nodos:** función que evalúa el estado, asignando un número que representa la deseabilidad
   - Mayor valor → más deseable
   - Menor valor → más deseable
   - Depende de cómo representes el problema

2. **Transiciones/Aristas:** costo de pasar de un estado a otro
   - Representa el costo del camino aplicable
   - Penaliza el costo total acumulado

### Métodos de Escalada (Hill Climbing)

Métodos que buscan ascender hacia el mejor valor según la heurística.

#### Escalada Simple
- **Proceso:**
  1. Se genera el primer hijo en el orden especificado (ej: izquierda a derecha)
  2. Se compara su heurística con la del nodo actual
  3. Si el hijo tiene **mayor** heurística → pasa a ser nodo actual
  4. Si no es mejor → continúa con el siguiente hijo
  5. Si ningún hijo es mejor → se detiene
  
- **Ventajas:** 
  - Poca memoria (no almacena todo el árbol)

- **Problemas:**
  - Puede perder nodos mejores (solo evalúa hijos en orden)
  - **No tiene retroceso** → puede quedar atrapado en un **máximo local**
  - Requiere que la función heurística sea monotonamente creciente
  - **No garantiza encontrar solución** a menos que exista un camino monotonamente creciente

#### Escalada de Máxima Pendiente (Steepest Ascent)
- **Proceso:**
  1. Se generan **todos** los hijos
  2. Se selecciona el hijo con **mejor** heurística
  3. Se compara con el nodo actual
  4. Si el mejor hijo supera al actual en heurística → pasa a ser nodo actual
  5. Si no → se detiene

- **Problema:** 
  - **Sin retroceso** → también puede quedar en máximo local
  - Requiere que la función heurística sea monotonamente creciente

- **Diferencia con Escalada Simple:** ambas requieren que el hijo tenga heurística **estrictamente mayor** que el padre (nunca igual)

### Primero el Mejor (Best First Search)

Mejora sobre los métodos de escalada incorporando la capacidad de cambiar de camino cuando aparece otro más prometedor.

- **Estructura de datos:** utiliza dos listas
  - **LNA (Nodos Abiertos):** generados pero no recorridos, ordenados por heurística (mayor a menor deseabilidad)
  - **LNC (Nodos Cerrados):** ya recorridos

- **Proceso:**
  1. Inicializar LNA con el estado inicial, LNC vacía
  2. Seleccionar el mejor nodo de LNA (más deseable)
  3. Mover a LNC y verificar si es solución
  4. Si es solución → fin
  5. Si no → generar hijos, agregar a LNA (ordenados), repetir

- **Características:**
  - **Tiene retroceso** → puede escapar de máximos locales
  - No necesita que la función sea monotonamente creciente
  - **Garantiza encontrar solución** si existe (siempre que no haya restricción de memoria)
  - Puede seleccionar el mejor estado disponible **incluso si tiene menor heurística que el nodo actual**
  - Nunca queda atrapado en máximo o mínimo local

### Beam Search (búsqueda de haz)

Variante de Primero el Mejor con **memoria limitada**.

- **Parámetro N:** número máximo de nodos que se guardan en LNA
- **Proceso:** similar a Primero el Mejor pero solo se conservan los **N mejores nodos** en LNA
- **Comportamiento:** similar a Escalada de Máxima Pendiente pero sin requerir que el nodo sea mejor que el actual
- **Diferencia con Escalada Máxima Pendiente:** no necesita comparar con el estado actual; el nodo puede tener menor heurística que su padre y aún ser seleccionado
- **Ventaja:** consume menos memoria que Primero el Mejor
- **Desventaja:** **no garantiza solución** (depende de N)

**Caso especial: Beam Search con N=1**
- Se convierte en un algoritmo similar a Escalada Máxima Pendiente
- Pero sin necesidad de que la heurística sea monotonamente creciente

### A* (A Estrella)

Extensión de Primero el Mejor que incluye **costo acumulado del camino**.

- **Función de evaluación:** `f(n) = g(n) + h(n)`
  - **g(n)** = costo acumulado del camino hasta n desde el inicio
  - **h(n)** = heurística (estimación del costo restante hasta la solución)

- **Ordenamiento:** los nodos en LNA se ordenan por f(n), penalizando caminos largos

- **Características:**
  - Cuanto más largo el camino, más penalizado
  - Incorpora información en transiciones (costo de los caminos aplicables)
  - **Garantiza encontrar la solución óptima** si:
    - La heurística es **admisible** (nunca sobrestima el costo real)
    - No hay restricción de memoria

- **Relación con otros métodos:** 
  - Es Primero el Mejor + costo acumulado
  - Generalización de algoritmos como Dijkstra (cuando h(n) = 0)

---

## Tabla Comparativa

### Sin información de dominio

| Método | Recorre por… | Finaliza cuando… | Garantiza solución óptima | Memoria |
|--------|-------------|-----------------|--------------------------|---------|
| Primero en amplitud | Niveles | Recorre todo el árbol | Sí | Mucha |
| Primero en profundidad | Ramas | Encuentra primer estado final | No | Poca |
| Generación y prueba | Ramas (luego niveles) | Encuentra todos los estados finales | Sí (comparando todas) | Media |
| Bidireccional | Niveles (al menos 1) | Encuentra estado intermedio común | Sí | Media |

### Con información de dominio

| Método | ¿Retroceso? | ¿Garantiza solución? | ¿Óptima? | Criterio siguiente estado | Especial |
|--------|------------|---------------------|----------|--------------------------|----------|
| Escalada simple | No | No | No | Primer hijo mejor que actual | Requiere heurística monótona |
| Escalada máx. pendiente | No | No | No | Mejor de todos los hijos | Requiere heurística monótona |
| Primero el mejor | Sí | Sí | No* | Mejor nodo abierto (LNA) | Puede seleccionar peor que actual |
| Beam Search | Sí* | No | No* | Mejor nodo abierto (LNA limitada) | Con N=1 similar a escalada |
| A* | Sí | Sí | Sí** | Mejor por f(n) = g(n)+h(n) | Incluye costo acumulado |

**Notas sobre la tabla:**
- Escalada simple y máxima pendiente requieren heurística **estrictamente mejor** (nunca igual)
- Primero el Mejor garantiza solución pero no necesariamente óptima (puede haber soluciones mejores más adelante)
- A* garantiza óptima si heurística es admisible
- Beam Search tiene retroceso solo si N > 1

---

## Análisis de Complejidad

Impacto del crecimiento exponencial del árbol de búsqueda:

Ejemplo con nodos de 100 bytes y 4 hijos por nodo:
- Nivel 9: ~20 MB
- Nivel 14: ~25 GB
- Nivel 15: ~100 GB

Esto justifica la necesidad de usar heurísticas para reducir la exploración del espacio de búsqueda.

---

## Resumen clave para el final

1. **Formalización:** todo problema se modela como estados + operadores + estado inicial + estados solución.

2. **Sin heurística (búsqueda ciega):** 
   - BFS (amplitud): garantiza solución óptima, usa mucha memoria
   - DFS (profundidad): usa poca memoria, no garantiza óptima
   - Generación y Prueba: encuentra todas las soluciones
   - Bidireccional: búsquedas simultáneas desde inicio y fin

3. **Con heurística (búsqueda informada):**
   - Escalada: sin retroceso, puede quedar en máximo local
   - Primero el Mejor: tiene retroceso, garantiza solución (no necesariamente óptima)
   - Beam Search: Primero el Mejor con LNA limitada a N nodos
   - A*: Primero el Mejor + costo acumulado. Óptima si heurística admisible

4. **Trade-off memoria-tiempo:** métodos heurísticos sacrifican exhaustividad (no garantizan óptima) para reducir memoria y tiempo dramáticamente.

5. **Función heurística:** crítica para el desempeño. Debe ser:
   - **Admisible** (para A*, no sobrestima)
   - **Informativa** (discrimina bien entre estados)
   - **Eficiente** de calcular

6. **Escalada:** sin retroceso, puede quedar en máximo local si función no es monotonamente creciente.

7. **Primero el Mejor:** tiene retroceso (LNA), garantiza encontrar solución, no requiere monotonía.

8. **A*:** equivalencia f(n) = g(n) + h(n). Óptimo si la heurística es admisible. Combina mejor lo mejor de información del dominio con costo del camino.

---

## 📝 Cambios respecto al original

**Se agregó:**
- Explicación detallada del concepto de "estado" como foto del sistema
- Diferenciación entre espacios de búsqueda finitos e infinitos
- Descripción del crecimiento exponencial de la memoria requerida con ejemplos concretos (20 MB, 25 GB)
- Contextualización histórica: origen del término "heurística" (griego "eureka")
- Aplicaciones prácticas de búsqueda heurística: rutas de viaje, verificación de software (SAGE), sistemas expertos, optimización
- Explicación de cómo se representa la información heurística en nodos vs. transiciones
- Detalles sobre penalización de costos en transiciones (resta vs. suma según deseabilidad)
- Procesos paso-a-paso de Primero en Amplitud, Primero en Profundidad, Generación y Prueba, Primero el Mejor, Beam Search y A*
- Primero en Profundidad Iterativa como variante de DFS
- Búsqueda Bidireccional con mayor profundidad en requisitos y funcionamiento
- Distinción clave: Escalada Simple requiere primero hijo mejor, Escalada Máxima Pendiente requiere mejor de todos, Primero el Mejor selecciona mejor disponible sin importar padre
- Tabla mejorada con columna de "Especial" detallando requisitos de cada método
- Explicación de exhaustividad vs. eficiencia en métodos heurísticos
- Función de evaluación A*: f(n) = g(n) + h(n) con desglose detallado
- Garantía de optimalidad en A* condicionada a heurística admisible
- Requisitos prácticos para función heurística: admisibilidad, informativeness, eficiencia computacional
- Ejemplos de recorrido en diferentes órdenes (izquierda-derecha, derecha-izquierda) para visualizar diferencias


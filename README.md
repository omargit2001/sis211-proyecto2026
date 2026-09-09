# SIS-211 · Proyecto de curso (2/2026)

Un mismo software que **crece**: v1 (estructuras simples) → v2 (jerárquicas) → v3 (grafos).

**Hoy solo existe la branch `v1`.** No creen `v2` ni `v3`.

| | |
| --- | --- |
| **Estudiante** |Omar Jose Torrez Moscoso |
| **Dominio** |Transacciones Bancarias (procesamiento, historial y auditoría) |
| **Repo** |https://github.com/omargit2001/sis211-proyecto2026.git |

## Mapa v1 (mínimo tres familias distintas)

Familias: arreglo, lista, pila, cola, tabla hash.  
`dict` y `set` son **la misma** familia (hash). Sin árboles ni grafos en v1.

| Flujo del dominio | Qué llega / sale / se busca | Familia | La uso porque… |
| --- | --- | --- | --- |
| Búsqueda directa de cuentas| Se busca una cuenta por su número o ID único para consultar saldo o titular.|Tabla Hash (dict) |Permite un acceso de tiempo constante $O(1)$ a la información de las cuentas sin necesidad de recorrer todo el registro. |
|Procesamiento de transferencias | Llegan solicitudes de transferencia entre cuentas en tiempo real para ser procesadas en orden de llegada.| Cola (collections.deque o lista como FIFO)| Garantiza el principio FIFO (First In, First Out), asegurando equidad e integridad procesando primero las transacciones que entraron primero.|
|Historial de transacciones de un usuario |Se registran los movimientos financieros para poder deshacer/revertir la última operación realizada en la sesión. |Pila (Lista como LIFO) | Funciona bajo el principio LIFO (Last In, First Out), lo que facilita implementar la función de deshacer (undo) la transacción más reciente.|
| Registro de transacciones sospechosas|Se almacenan los IDs de transacciones marcadas por fraude para auditoría continua.|Lista de tamaño variable (list)|Permite la inserción dinámica de nuevos registros de auditoría y su posterior iteración secuencial para generar reportes.|

Cómo probar un caso límite (vacío, no encontrado o duplicado):Se verificará que al intentar procesar una transferencia cuando la Cola está vacía, el sistema devuelva un mensaje de estado seguro sin lanzar una excepción no controlada (IndexError). Asimismo, al buscar un número de cuenta inexistente en la Tabla Hash, se manejará el caso de "cuenta no encontrada" retornando None o una alerta descriptiva, evitando que la aplicación se colapse.

>Se verificará que al intentar procesar una transferencia cuando la Cola está vacía, el sistema devuelva un mensaje de estado seguro sin lanzar una excepción no controlada (IndexError). Asimismo, al buscar un número de cuenta inexistente en la Tabla Hash, se manejará el caso de "cuenta no encontrada" retornando None o una alerta descriptiva, evitando que la aplicación se colapse.

## Carpetas

- `src/` — clases del dominio (POO). Hoy no codeen.
- `tests/` — un caso límite, cuando implementen.

## Alcance

- v1: clases en `.py` (POO). Entrega Moodle: **2026-10-07 23:59**.
- Este README **no** sustituye la tarea de Moodle.
- v2 y v3: otras branches, más adelante, a partir de `v1`.

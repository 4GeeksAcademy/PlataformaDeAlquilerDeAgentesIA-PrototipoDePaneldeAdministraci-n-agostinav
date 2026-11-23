# AgentHub - Tareas SDD

Cada tarea indica dependencias, archivos y un criterio de finalizacion comprobable. `SPECS.md`, `DESIGN.MD` y `stitch-reference/*.html` son fuentes de solo lectura.

| ID | Tarea | Depende de | Archivos afectados | Criterio de finalizacion |
|---|---|---|---|---|
| D01 | Auditar SPECS, DESIGN y las cinco exportaciones; registrar sus patrones e incompatibilidades. | - | Ninguno (lectura) | `plan.md` identifica las seis vistas, el shell compartido, el tema y las restricciones por archivo. |
| D02 | Completar el plan de fases y arquitectura singleton. | D01 | `specs/agenthub/plan.md` | Incluye componentes, dependencias, puertas de aprobacion, riesgos de datos y validacion. |
| D03 | Consolidar la especificacion funcional y tecnica en el unico archivo `SPECS.md` de la raiz. | D01 | `SPECS.md` | Conserva el contenido funcional y el complemento tecnico, incluidos los criterios 1-53. No existe `specs/agenthub/SPEC.md` ni `specs/agenthub/spec.md`. |
| D04 | Crear tareas ordenadas y mapa de cobertura de aceptación. | D02, D03 | `specs/agenthub/tasks.md` | Cada tarea tiene dependencias, archivos y una definicion de terminado; criterios 1-53 quedan asignados. |
| D05 | Revisar en conjunto los tres documentos y obtener aprobacion antes de implementar. | D02-D04 | Los tres documentos SDD | Sin contradicciones abiertas sobre alcance; aprobacion explicita del usuario registrada. |
| I01 | Crear el shell semantico de una sola pagina y navegacion de seis secciones. | D05 | `index.html` | Contiene aside/nav/header/main, seis vistas, Dashboard inicial, solo una vista visible, titulo y `aria-current` sincronizados. |
| I02 | Definir datos ficticios normalizados y renderizado de Dashboard. | I01 | `index.html` | Usuarios/agentes/skills/contratos/errores tienen IDs relacionados; ingresos `$48.750`, perdidas `$3.240`, actividad semanal HTML y conteos de agentes derivados. |
| I03 | Implementar tabla, detalle y eliminacion local de usuarios. | I02 | `index.html` | Cinco usuarios de SPECS; columnas y detalles requeridos; menu compartido; eliminar fila solo durante sesion. |
| I04 | Implementar tarjetas, acordeones, menu y configuracion de agentes. | I02 | `index.html` | Al menos cuatro agentes; todos los acordeones inician cerrados; detalle de skills, prompt por agente, guardar/cancelar local y eliminacion visible actualizan relaciones/metricas. |
| I05 | Implementar catalogo y detalle/eliminacion de skills. | I02, I04 | `index.html` | Cinco skills de SPECS; conteos derivados; detalle muestra agentes asociados; quitar skill la oculta del catalogo sin invalidar lineas contractuales historicas. |
| I06 | Implementar tabla y detalle economico de contratos. | I02, I05 | `index.html` | Cuatro contratos con cliente/agente validos, fechas, estado, skills y total; el total es exactamente la suma de precios individuales mostrados en el mismo modal. |
| I07 | Implementar log, detalle de traza y resolucion local. | I02, I04 | `index.html` | Seis errores con timestamp/agente/tipo/severidad/descripcion/traza; referencias validas; resolver cambia solo el estado del error. |
| I08 | Implementar modal singleton para los cinco casos de uso. | I03-I07 | `index.html` | La misma instancia cambia titulo/contenido/acciones; cierre por boton/backdrop/Escape; foco entra y vuelve al disparador; acciones de prompt Guardar/Cancelar verificadas. |
| I09 | Implementar dropdown singleton y despacho de acciones. | I03-I07 | `index.html` | Una instancia contextual; un menu visible; clic exterior/Escape; foco restaurado; las acciones requeridas por cada tipo se ejecutan y cierran el menu. |
| I10 | Consolidar badges, sidebar, toggle y patron de acordeon. | I01, I04, I08, I09 | `index.html` | Una implementacion compartida de cada patron; estados textuales accesibles y controles semanticos/teclado. |
| I11 | Integrar identidad Stitch con temas claro/oscuro y responsive. | I01-I10 | `index.html` | Usa tokens/jerarquia de DESIGN; clases `dark:` efectivas en shell, tablas, badges y modales; claro inicial sin persistencia; desktop/tablet sin solapamientos y tablas con scroll necesario. |
| I12 | Validar criterios funcionales, tecnicos, accesibilidad y reinicio. | I01-I11 | `index.html` | Matriz 1-53 marcada con evidencia; navegacion, acciones, relaciones, tema, teclado, recarga y restricciones tecnicas verificados manualmente; app servida con `python3 server.py`. |
| I13 | Revisar entrega y publicar cambios. | I12 | Solo archivos aprobados de la implementacion | Diff y estado revisados; commit y push solo con autorizacion de entrega y remoto/credenciales disponibles. No forma parte de esta fase documental. |

## Mapa de cobertura de `SPECS.md`

| Criterios | Tareas que los cubren |
|---|---|
| 1-8: producto, shell semantico, stack, restricciones y coherencia de datos | D01-D05, I01-I02, I11-I12 |
| 9-12: Dashboard, cuatro metricas y placeholder | I02, I10-I12 |
| 13-18: usuarios, tabla, badges, acciones y modal | I03, I08-I09, I12 |
| 19-26: agentes, estados, acordeones, prompt y eliminacion | I04, I08-I10, I12 |
| 27-32: skills, relaciones, detalle y eliminacion | I05, I08-I10, I12 |
| 33-38: contratos y desglose que suma el total | I06, I08-I09, I12 |
| 39-42: errores, traza y resolucion | I07-I09, I12 |
| 43-53: navegacion global, tema, menus, modal, transiciones, responsive, foco, contraste y recarga | I01, I08-I12 |

## Puertas de aprobacion

- No comenzar I01 ni crear `index.html` hasta que el usuario apruebe `plan.md`, `SPECS.md` y `tasks.md`.
- El criterio 1 se interpreta como una sola pagina HTML de producto; las cinco referencias existentes se conservan. Si se exige literalmente que no exista ningun HTML en el repositorio, resolver esa incompatibilidad con el usuario antes de I01.
- No modificar los archivos fuente de solo lectura ni crear `spec.md` en minusculas.
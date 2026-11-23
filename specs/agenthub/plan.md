# AgentHub - Plan tecnico de implementacion

## Estado y alcance

Este paquete documenta la implementacion y validacion de AgentHub. `SPECS.md` en la raiz es la unica especificacion del proyecto e incluye la especificacion funcional y el complemento tecnico. El prototipo ya esta implementado en el unico `index.html`; el orden de tareas y las puertas de aprobacion quedan como registro del proceso seguido.

La futura entrega de producto sera un solo `index.html`, con HTML5, Tailwind CSS por CDN y JavaScript vanilla. No se modificaran `SPECS.md`, `DESIGN.MD` ni los cinco HTML de referencia. No habra backend, API, `fetch`, persistencia, frameworks, CSS personalizado ni build.

## Auditoria de las referencias Stitch

Tamanos en bytes medidos con `wc -c`; lineas logicas verificadas por archivo. Las cinco referencias comparten un shell exportado con marca AgentHub, sidebar persistente de seis enlaces, header fijo, estado activo y boton global que alterna la clase `dark`. Tambien repiten la configuracion de Tailwind, tokens, tipografias, iconografia y superficies.

| Archivo | Bytes | Lineas | Pantalla y patrones relevantes |
|---|---:|---:|---|
| `stitch-reference/contratacionesdeagentes.html` | 33913 | 455 | KPI, tabla ancha con scroll, skills como badges, menu de fila y modal de detalle/desglose; incluye sparklines SVG. |
| `stitch-reference/gestiondeagentes.html` | 46804 | 684 | KPI, cinco tarjetas de agente, estados, listas de skills expandibles, menu y editor de prompt en modal. Muestra 3 activos, 1 inactivo y 1 fallando. |
| `stitch-reference/gestiondeusuarios.html` | 35256 | 505 | Resumen, busqueda/filtros, tabla de cinco usuarios, badges, menu de acciones y modal de detalle. |
| `stitch-reference/logdeerrores.html` | 37130 | 496 | KPI, franja de tendencia SVG, tabla de seis incidentes con severidad/estado y modal de traza. |
| `stitch-reference/skills.html` | 35423 | 460 | Banner explicativo, filtros, grilla de cinco skills, asignaciones, precio de catalogo y modal de detalle. |

### Patrones y diferencias que guian la integracion

- Reutilizar la composicion compartida del shell, sidebar, header, toggle, superficies, jerarquia tipografica, KPI, tablas, badges, menus y dialogs de Stitch. Las cinco pantallas son referencias separadas; la implementacion las unifica bajo un shell y seis secciones, incluida la vista Dashboard definida por `SPECS.md`.
- Las exportaciones configuran `darkMode: "class"` y el toggle modifica la clase raiz, pero no aplican variantes `dark:` a las superficies de las vistas. `DESIGN.MD` si define las superficies slate oscuras y colores semanticos. La implementacion aplicara esas variantes a todos los componentes y conservara tema claro inicial, sin persistencia.
- Las cinco exportaciones contienen un bloque `<style>`, cargan Inter, JetBrains Mono y Material Symbols desde Google Fonts, y repiten mucho `tailwind.config`. Contratos y errores tienen `style` inline en barras; usuarios modifica `row.style.display`; hay manejadores `onclick`. Son incompatibles con las restricciones de la entrega y no se copiaran como codigo. Se preservara la apariencia con utilidades Tailwind permitidas, sin estilos inline ni dependencia de fuentes/iconos remotos.
- Los estados preabiertos de menus/modal y el primer acordeon expandido en Agentes son solo composicion de referencia. La interfaz funcional inicia menus y modal cerrados y todos los acordeones colapsados, segun `SPECS.md`.
- Hay controles sin comportamiento o de demostracion: algunos menus no funcionan, busquedas/filtros son estaticos, eliminar puede mostrar `alert`, y resolver un error solo cierra un modal. El prototipo implementara las acciones locales especificadas y no mantendra afirmaciones de sincronizacion/API/tiempo real.
- Contrataciones muestra `$48.750` como KPI, pero las etiquetas de su grafico suman `$48.700`; ese total no se tomara como fuente de contratos. Skills tiene precios mensuales de catalogo distintos de los precios por linea de contrato. No se asumira una tarifa global comun. Cada total de contrato se calculara exclusivamente con los precios de sus skills contratadas.
- El texto de tokens de `DESIGN.MD` asigna `#3525cd` a `primary` y `#4f46e5` a `primary-container`, mientras su narrativa describe `#4f46e5` como ancla primaria. Se conservara el mapeo concreto de tokens Stitch y se registrara esta diferencia, sin inventar una tercera paleta.

## Arquitectura prevista

### Shell y vistas

Un solo documento con `<aside>`, `<nav>`, `<header>`, `<main>` y seis `<section>` identificables. La sidebar persistente mantiene los seis enlaces y `aria-current="page"`; en tablet se compacta sin perder nombres accesibles. El header actualiza titulo y contiene el unico toggle global. Solo la vista seleccionada queda visible.

### Componentes compartidos

- **Modal unico:** un dialog/backdrop en el HTML y un controlador `openModal(type, id, trigger)` / `closeModal()`. Un renderizador cambia titulo, contenido y acciones para detalle de usuario, configurar agente, detalle de skill, contrato y error. Maneja foco inicial, cierre por boton/backdrop/Escape y retorno al disparador. Configurar agente conserva el prompt original hasta Guardar; Cancelar descarta el borrador.
- **Dropdown unico:** un controlador con una instancia de menu contextual; recibe tipo e ID de entidad y produce las acciones permitidas. Solo puede quedar abierto uno; clic exterior o Escape lo cierra y Escape devuelve foco al disparador. Las acciones se despachan localmente.
- **Badges compartidas:** una funcion/template mapea estado o severidad a etiqueta y clases Tailwind de tema claro/oscuro. El texto comunica siempre el estado; el color no es el unico indicador.
- **Acordeon generico:** un disparador semantico por agente, con `aria-expanded` y `aria-controls`, controla solo su propio bloque. Inicio colapsado, teclado Enter/Espacio y transicion mediante clases Tailwind, sin atributos `style`.
- **Metricas y tablas:** plantillas visuales uniformes; tablas semanticas con scroll horizontal cuando el ancho lo requiera. Las metricas derivables leen los datos del estado actual.
- **Tema global:** un control alterna `dark` en el elemento raiz y actualiza su etiqueta accesible. Variantes `dark:` de `DESIGN.MD`, sin `localStorage`; recargar restablece tema claro.
- **Datos y eventos:** constantes JavaScript con IDs y referencias; renderizado vanilla y listeners delegados. Los avisos de exito describen un cambio local de sesion, nunca persistencia en servidor.

## Invariantes de datos y estado

- Mantener los valores expresos de `SPECS.md`: ingresos del mes `$48.750` y perdidas por descuentos/cupones `$3.240`. Son valores ficticios fijados por la especificacion, no una suma deducida de los contratos.
- Agentes activos y fallando se cuentan desde el inventario actual, no se hardcodean en las tarjetas. La distribucion Stitch de cinco agentes (3 activos, 1 inactivo, 1 fallando) puede usarse como fixture inicial: Dashboard mostraria 3 activos y 1 fallando. Si se usa otra distribucion, ambas metricas deben seguir derivadas y el error asociado al agente fallando debe concordar.
- Mantener los cinco nombres de usuario, cinco agentes y cinco skills indicados por `SPECS.md`, al menos cuatro contratos y seis errores. Contratos y errores referencian IDs existentes. Las skills asignadas y los conteos de adopcion se derivan de las relaciones.
- Fijar una sola moneda para catalogo y contratos; se propone USD por la identidad de las referencias. No fijar importes de lineas en este paquete: al definir fixtures, cada total contractual sera exactamente la suma visible de sus precios individuales.
- Eliminar usuario/agente/skill cambia la presentacion local hasta recargar. Para conservar integridad de referencias historicas, el registro base puede mantenerse oculto; quitar un agente actualiza las metricas derivadas del inventario visible y quita sus relaciones activas visibles. Ocultar una skill la quita del catalogo y de nuevas asociaciones; contratos existentes conservan el desglose historico.
- Marcar un error resuelto cambia solo `resuelto` y desactiva/oculta su accion repetida. No implica recuperar automaticamente el agente: `SPECS.md` no define esa transicion.
- Guardar prompt modifica solo el objeto en memoria de sesion; Cancelar no modifica el objeto. Recargar restaura fixtures, prompts y tema.

## Fases y puertas de aprobacion

1. **Documentacion SDD (esta fase):** inspeccionar fuentes, completar `plan.md`, conservar la especificacion consolidada `SPECS.md` y ordenar `tasks.md`. Termina cuando el usuario aprueba los tres documentos.
2. **Shell y modelo:** crear `index.html`, integrar Tailwind CDN/tokens, shell, seis vistas y datos ficticios relacionados. Depende de la aprobacion de Fase 1.
3. **Componentes e interacciones:** conectar modal, dropdown, badges, acordeones, toggle, acciones locales y renderizadores. Depende de shell y datos.
4. **Integracion visual/accesible:** adaptar patrones Stitch, variantes claras/oscuras de DESIGN, responsive, foco, semantica y teclado; corregir diferencias sin alterar `SPECS.md` ni las referencias.
5. **Verificacion:** mapear criterios 1-53, ejecutar validacion manual en escritorio/tablet y probar el servidor Flask. Corregir solo hallazgos del alcance.
6. **Entrega:** revisar cambios; commit/push solo despues de validar y con autorizacion de entrega, remoto y credenciales disponibles.

## Cobertura de criterios de aceptacion

La matriz de `tasks.md` asigna todos los criterios 1-53: restricciones/coherencia 1-8; Dashboard 9-12; Usuarios 13-18; Agentes 19-26; Skills 27-32; Contrataciones 33-38; Errores 39-42; navegacion, tema, controles globales, accesibilidad, responsive y recarga 43-53.

**Ambiguedad a resolver antes de implementacion:** el criterio 1 de `SPECS.md` dice que no habia HTML antes del primer commit de especificaciones, pero el repositorio ya contiene cinco HTML de Stitch que deben conservarse. Para no violar la instruccion de no modificarlos, se interpreta como una unica pagina HTML de producto (`index.html`) y referencias de diseño excluidas de ese conteo. Si se interpreta literalmente como ausencia de cualquier HTML, el criterio es incompatible con el estado del repositorio y requiere decision del usuario.

## Archivos

- Documentacion SDD: `specs/agenthub/plan.md`, `SPECS.md`, `specs/agenthub/tasks.md`.
- Unico artefacto de producto futuro: `index.html`.
- Fuentes de solo lectura: `SPECS.md`, `DESIGN.MD`, `server.py` y `stitch-reference/*.html`.
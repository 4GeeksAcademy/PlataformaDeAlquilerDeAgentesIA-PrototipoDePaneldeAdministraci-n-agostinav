# AGENTHUB - Especificacion del panel administrativo

## 1. Indice

1. [Descripcion del producto](#2-descripcion-del-producto)
2. [Usuario administrador y objetivos](#3-usuario-administrador-y-objetivos)
3. [Alcance y restricciones tecnicas](#4-alcance-y-restricciones-tecnicas)
4. [Arquitectura de navegacion](#5-arquitectura-de-navegacion)
5. [Especificaciones por seccion](#6-especificaciones-por-seccion)
   - [5.1 Dashboard](#61-dashboard)
   - [5.2 Gestion de usuarios](#62-gestion-de-usuarios)
   - [5.3 Gestion de agentes](#63-gestion-de-agentes)
   - [5.4 Skills](#64-skills)
   - [5.5 Contrataciones de agentes](#65-contrataciones-de-agentes)
   - [5.6 Log de errores](#66-log-de-errores)
6. [Inventario de componentes reutilizables](#7-inventario-de-componentes-reutilizables)
7. [Modelo de datos ficticios](#8-modelo-de-datos-ficticios)
8. [Interacciones JavaScript y comportamiento local](#9-interacciones-javascript-y-comportamiento-local)
9. [Diseno responsive y tema](#10-diseno-responsive-y-tema)
10. [Accesibilidad y semantica](#11-accesibilidad-y-semantica)
11. [Criterios de aceptacion](#12-criterios-de-aceptacion)
12. [Validacion manual](#13-validacion-manual)

## 2. Descripcion del producto

AgentHub es una plataforma SaaS que permite a las empresas alquilar agentes de inteligencia artificial preconfigurados y equiparlos con skills para realizar tareas empresariales.

El objetivo de este ejercicio es construir el prototipo visual e interactivo del panel de administracion interno de AgentHub. El sistema operativo sera representado de forma fiel mediante datos y estados ficticios, pero no establecera conexion con el backend existente ni con servicios externos.

El prototipo debe servir como referencia visual y funcional para futuros desarrolladores. Todas las pantallas, tablas, modales, menus y controles deben parecer parte del mismo producto, con datos coherentes entre todas las vistas.

## 3. Usuario administrador y objetivos

El usuario principal es un administrador interno de AgentHub que supervisa clientes, agentes, skills, contrataciones e incidentes operativos.

Sus objetivos principales son:

- Revisar rapidamente la actividad comercial y el estado operativo.
- Consultar y administrar usuarios registrados.
- Supervisar agentes, propietarios, estados y configuracion de prompts.
- Revisar el catalogo de skills disponible y su adopcion.
- Consultar contratos y el detalle economico de cada contratacion.
- Detectar errores, examinar trazas y marcar incidentes resueltos.

El usuario necesita una interfaz densa pero ordenada, visualmente clara en escritorio y tablet, con acciones predecibles y sin confirmaciones falsas de persistencia en servidor.

## 4. Alcance y restricciones tecnicas

### 4.1 Stack obligatorio

- HTML5 semantico.
- Tailwind CSS exclusivamente mediante CDN.
- JavaScript vanilla sin frameworks, librerias ni jQuery.
- Un unico `index.html` como resultado de la fase de implementacion.
- Datos ficticios hardcodeados dentro del documento o definidos en constantes JavaScript.
- Sin backend, base de datos, APIs, fetch, XMLHttpRequest o persistencia remota.
- Sin herramientas de compilacion, bundlers ni procesos de build.
- Sin archivos CSS personalizados.
- Sin atributos `style` inline.
- Sin React, Vue, Angular ni otros frameworks.

### 4.2 Alcance del prototipo

- Solo se implementaran las seis secciones especificadas.
- Los datos iniciales deben relacionarse entre si.
- Las acciones locales deben tener efecto visible durante la sesion.
- No se debe afirmar ni simular que un cambio fue enviado a un servidor.
- La recarga puede restablecer los datos ficticios iniciales.

## 5. Arquitectura de navegacion

Se utilizara una pantalla con sidebar persistente en escritorio y tablet. El sidebar contendra seis enlaces identificados por icono y etiqueta:

1. Dashboard.
2. Usuarios.
3. Agentes.
4. Skills.
5. Contrataciones.
6. Log de errores.

Cada enlace sera un boton o enlace semantico que cambia la vista visible. Solo una seccion sera visible a la vez. La seccion activa debera mostrar estado visual claro y `aria-current="page"`.

El header superior permanecera visible y mostrara el titulo de la seccion activa, una descripcion breve opcional y el toggle global de tema. En tablet, el sidebar podra reducir su ancho a iconos o transformarse en navegacion compacta siempre que conserve etiquetas accesibles y permita recorrer las seis secciones.

## 6. Especificaciones por seccion

### 6.1 Dashboard

**Especificacion visual:**

- Presentar un encabezado con el titulo Dashboard y una descripcion breve.
- Mostrar exactamente o al menos cuatro tarjetas de metricas en una cuadricula responsive.
- Las cuatro metricas son ingresos totales del mes, perdida por descuentos y cupones, agentes activos y agentes fallando.
- Cada tarjeta tendra icono, etiqueta y valor ficticio claramente legible.
- Debajo de las tarjetas existira un contenedor de ancho completo para un placeholder visual de grafico de actividad semanal.

**Especificaciones concretas:**

1. Tarjeta Ingresos: etiqueta “Ingresos totales”; valor de ejemplo `$48.750` y variacion opcional coherente con el mes.
2. Tarjeta Perdidas: etiqueta “Perdidas por descuentos” o equivalente; valor de ejemplo `$3.240`.
3. Tarjeta Agentes activos: valor derivado del inventario ficticio de agentes; por ejemplo `5` si existen cinco activos.
4. Tarjeta Agentes fallando: valor derivado del inventario; por ejemplo `1` si existe un agente con estado fallando.
5. El grafico sera un placeholder construido con Tailwind y elementos HTML, sin libreria ni canvas obligatorio. Podra representar barras, rejilla o linea CSS, pero no afirmara datos reales ni incorporara graficos externos.

### 6.2 Gestion de usuarios

**Especificacion visual:**

- Mostrar una tabla con al menos cinco usuarios ficticios.
- Las columnas obligatorias seran nombre, email, plan y estado.
- Cada estado sera una badge visual: activo, inactivo o pendiente.
- Cada fila tendra un boton de tres puntos para abrir un dropdown de acciones.

**Especificaciones concretas:**

1. Usuarios iniciales coherentes con los clientes de contrataciones: Sofia Ramirez, Daniel Ortega, Martina Torres, Nicolas Vega y Lucia Fernandez.
2. Cada usuario tendra plan, estado, empresa, fecha de registro y telefono opcional, visibles en su detalle.
3. La accion “Ver detalle” abrira un modal con nombre, email, plan, estado, empresa y fecha de registro.
4. La accion “Eliminar” removera visualmente la fila durante la sesion y cerrara el dropdown.
5. El modal se cerrara con el boton de cierre y con un clic en el backdrop.

### 6.3 Gestion de agentes

**Especificacion visual:**

- Mostrar al menos cuatro tarjetas o filas de agentes.
- Cada elemento mostrara nombre, propietario y estado activo, inactivo o fallando.
- Cada estado tendra una badge visual diferenciada.
- Las skills asignadas apareceran inicialmente colapsadas.
- Cada agente tendra un dropdown con “Configurar” y “Eliminar”.

**Especificaciones concretas:**

1. Inventario inicial: CustomerAgent, SalesCopilot, DataAnalyst, SupportBot y HealthAgent como catalogo posible; al menos cuatro deben estar visibles.
2. Al pulsar el encabezado o el boton de skills, el bloque expandira con transicion suave y mostrara las skills asignadas.
3. Al volver a pulsar el mismo control, el bloque colapsara con transicion suave. Solo el agente interactuado cambiara.
4. “Configurar” abrira un modal cuyo campo principal sera un textarea editable con el prompt de sistema ficticio del agente.
5. “Guardar” actualizara el prompt visible o informado como guardado localmente y cerrara el modal; “Cancelar” descartara cambios en la sesion del modal.
6. “Eliminar” removera visualmente el agente durante la sesion y actualizara metricas derivadas solo si esa derivacion se implementa localmente.

### 6.4 Skills

**Especificacion visual:**

- Incluir una explicacion breve de que es una skill dentro de AgentHub.
- Mostrar un catalogo de al menos cuatro skills en tarjetas o una grilla.
- Cada skill mostrara nombre, descripcion y numero de agentes que la utilizan.
- Cada skill tendra un dropdown con “Ver detalle” y “Eliminar”.

**Especificaciones concretas:**

1. Skills iniciales: Consultas CRM, Analisis de datos, Respuestas multicanal, Generacion de reportes y Automatizacion de soporte.
2. Los conteos de agentes serán derivados de las relaciones ficticias definidas en el modelo de datos.
3. “Ver detalle” abrira un modal con descripcion completa y lista de agentes asociados.
4. “Eliminar” removera visualmente la skill durante la sesion y cerrara el dropdown.
5. La explicacion indicara que una skill es una capacidad preconfigurada que amplía las tareas que puede realizar un agente.

### 6.5 Contrataciones de agentes

**Especificacion visual:**

- Mostrar una tabla con al menos cuatro contratos ficticios.
- Mostrar cliente, agente contratado, skills incluidas, fecha de inicio, fecha de finalizacion e importe total pagado.
- Cada contrato tendra un dropdown de acciones con “Ver detalle”.

**Especificaciones concretas:**

1. Los contratos referenciaran los nombres existentes de usuarios/clientes y agentes del catalogo ficticio.
2. Cada fila mostrara las skills asignadas como texto compacto o badges.
3. “Ver detalle” abrira un modal con cliente, agente, fechas, estado de contratacion e importe total.
4. El modal incluira un desglose de las skills contratadas y su precio individual.
5. El importe total sera la suma visible de los precios individuales del contrato.

### 6.6 Log de errores

**Especificacion visual:**

- Mostrar al menos seis registros ficticios.
- Mostrar timestamp, agente, tipo de error y descripcion breve.
- Clasificar visualmente los errores mediante badges de severidad o tipo.
- Cada registro tendra un dropdown con “Ver detalle” y “Marcar como resuelto”.

**Especificaciones concretas:**

1. Los registros referenciaran agentes existentes y conservaran consistencia con su estado, por ejemplo, un agente fallando asociado a incidentes.
2. “Ver detalle” abrira un modal con timestamp, agente, tipo, severidad, descripcion y traza completa ficticia.
3. “Marcar como resuelto” cambiara visualmente el registro a estado resuelto y cerrara el dropdown.
4. La traza mostrara un bloque legible con mensaje, modulo, identificador y pasos, sin ejecutar ni sugerir codigo real.
5. El timestamp seguira un formato uniforme, por ejemplo `2026-11-20 09:42:15`, y sera visible en la tabla y el detalle.

## 7. Inventario de componentes reutilizables

### 7.1 Sidebar

- Contendra la marca, navegacion y toggle de tema si se diseña dentro de ella.
- Debe persistir mientras cambia de seccion.
- El enlace activo mostrara fondo, icono y/o borde distinto y `aria-current="page"`.

### 7.2 Header

- Contendra el titulo de la seccion activa y el toggle global de tema.
- El titulo cambiara al navegar entre secciones.
- Debe compartir espaciado, tipografia y jerarquia visual en todas las vistas.

### 7.3 Tarjetas de metricas

- Tendran icono decorativo con nombre accesible, etiqueta y valor destacado.
- El layout sera uniforme y responsive.
- Los valores derivados podran calcularse desde los datos ficticios al iniciar el prototipo.

### 7.4 Tablas

- Usaran HTML semantico con `<table>`, `<thead>`, `<tbody>`, `<th>` y `<td>`.
- Tendran cabeceras asociadas a columnas y contenedor con scroll horizontal en espacios estrechos.
- Las tablas no deben perder el contexto de las acciones en la ultima columna.

### 7.5 Badges de estado

- Estados disponibles: activo, inactivo, fallando, pendiente, resuelto y severidades de error.
- Cada badge tendra color y texto; el color nunca sera la unica informacion.
- Las combinaciones claro/oscuro deben mantener contraste legible.

### 7.6 Dropdown de acciones

- Se implementara con un boton visible mediante tres puntos y un menu asociado.
- Solo un dropdown debera estar abierto a la vez.
- Al hacer clic fuera de un dropdown se cerrara.
- Al seleccionar una accion se ejecutara la accion local y se cerrara el menu.
- Pulsar Escape debera cerrar el menu y devolver el foco al boton disparador.

### 7.7 Modales

- Se implementaran con estructura semantica y una unica instancia reusable cuando sea suficiente.
- Tendran titulo, contenido dinamico, boton de cierre, foco inicial y boton o control primario segun aplique.
- Se abriran para detalle de usuario, configuracion de agente, detalle de skill, detalle de contrato y detalle de error.
- Cerrar el modal restablecera el foco al elemento que lo abrió.

### 7.8 Backdrop

- Cubrira el area restante alrededor del modal.
- Un clic directo sobre el backdrop cerrara el modal.
- Un clic dentro del panel del modal no debera propagarse al cierre del backdrop.
- Debe impedir visualmente el acceso a controles inferiores mientras esta abierto.

### 7.9 Listas colapsables

- Tendran un disparador con `aria-expanded` y un contenedor asociado con `aria-controls`.
- El estado inicial sera colapsado.
- La expansion y el colapso tendran transición suave basada en max-height, grid rows, opacidad o la tecnica equivalente de Tailwind.
- El cambio sera accesible mediante teclado con Enter o Espacio.

### 7.10 Toggle de tema

- El control sera global y cambiara toda la interfaz entre tema claro y oscuro.
- Usara las utilidades `dark:` de Tailwind al habilitar la clase `dark` en el elemento raiz.
- Tendra etiqueta accesible que indique la accion o el tema activo.
- La decision aprobada es no persistir el tema en localStorage. El estado se reiniciara al recargar.

### 7.11 Textarea editable

- Existira dentro del modal de configuracion de agente.
- Permitira seleccionar, editar y guardar texto sin validacion compleja.
- “Guardar” conservara el prompt del agente en memoria JavaScript durante la sesion.
- “Cancelar” no alterara el prompt almacenado.
- Al recargar, volvera al prompt ficticio inicial.

### 7.12 Placeholder de graficos

- Se construira con HTML y Tailwind exclusivamente.
- Tendra ejes o rejilla visuales y una leyenda breve si aporta claridad.
- No requerira libreria, API ni dato remoto.

## 8. Modelo de datos ficticios

### 8.1 Convenciones

- Los datos se definiran como constantes JavaScript con IDs unicos y nombres legibles.
- Los agentes, usuarios, skills, contratos y errores compartiran identificadores para mantener relaciones coherentes.
- Los precios se representaran como numeros en euros o dolares segun una moneda fijada visualmente; no se mezclarán monedas dentro del prototipo.
- Las fechas iniciales perteneceran al periodo mostrado en el prototipo.

### 8.2 Entidades

**Usuarios:**

- `id`, `nombre`, `email`, `plan`, `estado`, `empresa`, `fechaRegistro` y datos opcionales.
- Deben existir al menos cinco usuarios.

**Agentes:**

- `id`, `nombre`, `propietario`, `estado`, `skills`, `prompt` y datos opcionales.
- Deben existir al menos cuatro agentes.
- Estados permitidos: activo, inactivo y fallando.

**Skills:**

- `id`, `nombre`, `descripcion`, `agentesAsignados` o referencia por IDs de agentes.
- Deben existir al menos cuatro skills.
- El conteo mostrado sera derivado de las relaciones del array.

**Contratos:**

- `id`, `usuarioId`, `agenteId`, `skillsContratadas`, `fechaInicio`, `fechaFin`, `totalPagado`, `estado`.
- Deben existir al menos cuatro contratos.
- `skillsContratadas` tendra referencia al ID y precio individual de cada skill.
- El total sera la suma de los precios individuales para cada contrato.

**Errores:**

- `id`, `timestamp`, `agenteId`, `tipo`, `severidad`, `descripcion`, `traza`, `resuelto`.
- Deben existir al menos seis registros.
- Los agentes referenciados deben existir en el inventario.

### 8.3 Relaciones necesarias

- Cada contrato referencia un usuario existente y un agente existente.
- Las skills contratadas existen en el catalogo de skills.
- Los agents de los errores existen en el inventario de agentes.
- Los usuarios cliente pueden tener uno o varios contratos ficticios.
- Un agente puede tener varias skills y aparecer en varios contratos.
- Los conteos de skills se calculan a partir de agentes asignados.
- La actividad y los agentes fallando deben ser coherentes con los datos operativos mostrados.

## 9. Interacciones JavaScript y comportamiento local

### 9.1 Navegacion

- Los enlaces del sidebar escucharan clic mediante delegacion o listeners individuales.
- Al cambiar de vista se ocultaran todas las secciones y se mostrara solo la seleccionada.
- Se actualizaran titulo del header y estado activo.
- No se navegara mediante recarga ni se llamara a rutas externas.

### 9.2 Dropdowns

- Abrir uno cerrara cualquier otro dropdown abierto.
- Clic fuera cerrara el menu activo.
- Escape cerrara el menu activo y devolvera foco al disparador.
- Las acciones dispararan una funcion local segun el tipo de entidad.

### 9.3 Modales

- Los modales compartiran una instancia o estructura y cambiaran su contenido segun la accion.
- Guardar y cerrar deberan actualizar la interfaz solo en memoria.
- El backdrop recibira el evento de cierre.
- El panel interno detendra la propagacion del clic para no cerrar accidentalmente.
- El foco volvera al elemento que abrió el modal al cerrarse.

### 9.4 Acciones sin backend

- Eliminar usuario: removera visualmente la fila sin confirmar persistencia remota.
- Eliminar agente: removera visualmente el agente y sus relaciones mostradas en la misma sesion.
- Eliminar skill: removera visualmente la skill del catalogo y evitara mostrarla en detalles nuevos.
- Resolver error: cambiara el registro a estado resuelto y ocultara o desactivara la accion repetida segun el diseño final.
- Configurar agente: editara el prompt almacenado en memoria y mostrara confirmacion local visible.
- Ninguna accion usara peticiones HTTP ni escribira en almacenamiento permanente.
- La recarga restablecera todos los datos y acciones locales a su estado inicial.

### 9.5 Tema

- El toggle agregara o removera la clase `dark` en el elemento raiz.
- Todas las superficies necesitaran variantes claras y oscuras mediante clases `dark:`.
- El estado no sera persistido entre recargas segun la decision aprobada.

### 9.6 Navegacion por teclado

- Los controles principales seran botones o enlaces reales.
- Tabs, Enter y Escape deberan permitir operar enlaces, dropdowns, modales y acordeones.
- No se usaran `div` o `span` clicables sin semantica y gestion de teclado.

## 10. Diseno responsive y tema

- Desktop tendra sidebar persistente y vistas con cuadriculas que aprovechen el ancho.
- Tablet tendra sidebar reducida o compacta y tablas con contenedor horizontal si fueran mas anchas que el viewport.
- Las tarjetas del dashboard se adaptaran a dos columnas en tablet y una columna en viewport pequeno.
- Las vistas no deberan superponerse ni ocultar acciones principales.
- Los dropdown y modales deberan caber dentro del viewport con margen suficiente.
- Mobile no es obligatorio en el briefing, pero la interfaz debe evitar desbordes graves y podra adoptar una sidebar compacta o offcanvas.
- El modo claro sera el tema inicial hasta que se implemente otro comportamiento aprobado.
- El tema oscuro utilizara exclusivamente variantes Tailwind `dark:` y el sistema de clases de Tailwind CDN.
- No se usaran estilos inline para controlar tema, layout o transiciones.

## 11. Accesibilidad y semantica

- Utilizar HTML5 semantico: `<aside>`, `<header>`, `<main>`, `<nav>`, `<section>`, `<table>` y encabezados jerarquicos.
- Cada formulario o control tendra nombre accesible mediante `<label>`, `aria-label` o texto visible.
- Los iconos decorativos llevaran `aria-hidden="true"` y los iconos funcionales tendran texto o etiqueta accesible.
- Los modales tendran `role="dialog"`, `aria-modal="true"` y titulo asociado mediante `aria-labelledby`.
- Los dropdown tendran `aria-haspopup="menu"`, `aria-expanded` y cierre por Escape.
- Los acordeones tendran `aria-expanded` y `aria-controls` asociados al contenido.
- El foco sera visible con clases Tailwind de anillo o borde.
- Las badges incluiran texto, no dependeran solo de color.
- El contenido de las tablas tendra cabeceras programaticamente asociadas.
- Al abrir modales se movera el foco al primer elemento util y al cerrar se restaurara.
- Se evitara texto demasiado pequeno o contraste insuficiente en estados claros y oscuros.

## 12. Criterios de aceptacion

### Producto y restricciones

1. El repositorio contiene una interfaz basada en una sola pagina HTML para el panel AgentHub y no contiene HTML previo al primer commit de especificaciones.
2. El producto se presenta como un panel administrativo interno, sin afirmaciones de conexion real al backend.
3. HTML5 semantico define la estructura principal: aside, nav, header, main y secciones.
4. Tailwind CSS se carga mediante CDN y no se incluyen archivos CSS personalizados.
5. JavaScript vanilla gestiona todas las interacciones sin React, Vue, Angular, jQuery ni otra libreria.
6. No existen llamadas a APIs, bases de datos, fetch, almacenamiento remoto ni herramientas de build.
7. No existe ningun atributo `style` inline ni CSS incrustado para maquetacion personalizada.
8. Los datos mostrados son ficticios y son coherentes entre usuarios, agentes, skills, contratos y errores.

### Dashboard

9. La vista Dashboard incluye cuatro tarjetas de metricas obligatorias.
10. Las tarjetas muestran icono, etiqueta y valor para ingresos, perdidas, agentes activos y agentes fallando.
11. Debajo de las metricas existe un placeholder visual de grafico de actividad semanal de ancho completo.
12. El placeholder funciona sin librerias ni servicios externos.

### Usuarios

13. La tabla de usuarios contiene al menos cinco filas ficticias y las columnas nombre, email, plan y estado.
14. Los estados de usuarios se representan mediante badges con texto visible.
15. Cada fila incluye un boton de tres puntos que abre un menu de acciones.
16. El menu contiene “Ver detalle” y “Eliminar”.
17. “Ver detalle” abre un modal con la informacion completa del usuario seleccionado.
18. El modal de usuario se cierra mediante el boton de cierre y mediante clic directo sobre el backdrop.

### Agentes

19. El listado muestra al menos cuatro agentes con nombre, propietario y estado activo, inactivo o fallando.
20. Los estados de agentes se representan mediante badges diferenciadas y legibles.
21. Las listas de skills de todos los agentes aparecen inicialmente colapsadas.
22. Al hacer clic una primera vez, la lista se expande con transicion suave; al hacer clic nuevamente, se colapsa.
23. Cada agente tiene un dropdown con “Configurar” y “Eliminar”.
24. “Configurar” abre un modal con el prompt de sistema del agente dentro de un textarea editable.
25. El cambio de prompt puede guardarse localmente durante la sesion y no genera llamadas al servidor.
26. “Eliminar” retira visualmente el agente seleccionado hasta recargar o reiniciar el prototipo.

### Skills

27. El catalogo incluye al menos cuatro skills con nombre, descripcion y numero de agentes que usan cada una.
28. La seccion contiene una explicacion comprensible de que es una skill dentro de AgentHub.
29. Los conteos se derivan de relaciones existentes entre las skills y los agentes ficticios.
30. Cada skill incluye un dropdown con “Ver detalle” y “Eliminar”.
31. “Ver detalle” abre un modal con informacion ampliada y agentes asociados.
32. “Eliminar” retira visualmente la skill seleccionada durante la sesion.

### Contrataciones

33. La tabla contiene al menos cuatro contratos ficticios con cliente, agente contratado, skills, fecha de inicio, fecha de fin e importe.
34. Las referencias de clientes y agentes existen en sus respectivas entidades ficticias.
35. Cada contrato incluye un dropdown de acciones con “Ver detalle”.
36. “Ver detalle” abre un modal con el desglose completo del contrato.
37. El modal muestra las skills contratadas y el precio individual de cada una.
38. El importe total coincide con la suma de los precios individuales mostrados.

### Log de errores

39. El log contiene al menos seis registros con timestamp, agente, tipo de error y descripcion breve.
40. Los errores muestran badges de severidad o tipo con texto visible.
41. Cada registro incluye “Ver detalle” y “Marcar como resuelto” dentro de su dropdown.
42. “Ver detalle” abre un modal con la traza completa, y “Marcar como resuelto” cambia localmente el estado del registro.

### Interacciones globales y accesibilidad

Los criterios anteriores cubren los 42 requisitos numerados de la consigna principal. Las validaciones siguientes complementan la cobertura global y no sustituye ni modifica esos 42 criterios:

43. La navegacion lateral permite alternar entre las seis secciones y marca visual y semanticamente la seccion activa.
44. Solo una seccion se muestra a la vez al navegar.
45. El toggle global cambia entre modo claro y oscuro mediante la clase `dark` y utilidades `dark:`.
46. Abrir un dropdown cierra cualquier otro dropdown activo y tambien se cierra al hacer clic fuera.
47. Los modales tienen boton de cierre y cierran mediante backdrop.
48. Los dropdown y modales contienen acciones locales sin persistencia ni llamadas al servidor.
49. Las transiciones de acordeones y otros controles son suaves y no cambian el layout de forma abrupta.
50. El diseño es utilizable en escritorio y tablet sin solapamientos ni desbordes significativos.
51. Los controles principales tienen semantica HTML y gestion accesible de foco y teclado.
52. Los estados no dependen solo del color y mantienen contraste suficiente en ambos temas.
53. Al recargar, los datos vuelven al estado inicial ficticio y las acciones locales no afirman persistencia real.

## 13. Validacion manual

### Navegacion y tema

1. Abrir la pagina y confirmar que Dashboard aparece inicialmente como seccion activa.
2. Pulsar las seis entradas del sidebar y verificar que cambia la vista y el titulo del header.
3. Activar y desactivar el modo oscuro y revisar todas las vistas, tablas y modales.
4. Recargar y confirmar que el tema vuelve al estado inicial definido por el prototipo.

### Dropdown y cierre exterior

1. Abrir un dropdown y abrir otro distinto: el primero debe cerrarse.
2. Pulsar fuera de los menus y verificar que el menu activo desaparece.
3. Pulsar Escape en un dropdown y confirmar que el foco vuelve al disparador.

### Modales

1. Abrir y cerrar cada tipo de modal con el boton de cierre.
2. Abrir cada tipo de modal y cerrar haciendo clic directamente sobre el backdrop.
3. Confirmar que el foco inicial entra al dialogo y vuelve al disparador al cerrarlo.
4. Editar un prompt, cancelar y comprobar que el prompt almacenado no cambia.
5. Editar un prompt, guardar y comprobar que el nuevo texto permanece en la sesion del prototipo.

### Datos y acciones locales

1. Comparar nombres de clientes y agentes en Usuarios, Contrataciones y Errores.
2. Comparar conteos de skills con las asignaciones de agentes.
3. Eliminar un usuario, un agente y una skill y verificar el efecto visual local.
4. Resolver un error y verificar el cambio de estado sin recargar.
5. Recargar y confirmar que los elementos eliminados y cambios locales vuelven al inventario inicial.

### Responsive y accesibilidad

1. Revisar el prototipo en un viewport de escritorio amplio y en uno de tablet.
2. Verificar que las tablas tienen scroll horizontal si hace falta y que no se superponen controles.
3. Recorrer con teclado sidebar, dropdown, acordeones y modales.
4. Comprobar que el foco es visible y que los textos mantienen contraste en ambos temas.
5. Confirmar que los badges, aunque tengan color, incluyen texto comprensible.

---

# Complemento tecnico AgentHub

Este complemento extiende la especificacion funcional anterior; no la reemplaza ni crea un `spec.md` paralelo. Los criterios 1-53 y sus valores fuente permanecen sin cambios. `SPECS.md`, en la raiz, es la unica especificacion del proyecto y conserva la especificacion funcional aprobada junto con este complemento tecnico.

## 14. Integracion visual de Stitch y DESIGN.MD

Las cinco referencias (`contratacionesdeagentes.html`, `gestiondeagentes.html`, `gestiondeusuarios.html`, `logdeerrores.html` y `skills.html`) contienen el mismo shell AgentHub: sidebar con seis enlaces, header fijo, estado activo y control que alterna la clase `dark`. Tambien repiten tokens de superficie, configuracion Tailwind, tipografia y patrones de KPI, tablas, badges, menus y dialogs. La implementacion consolidara el shell y renderizara seis vistas; Dashboard se construye a partir de `SPECS.md`, porque no hay una referencia HTML separada para el.

Los HTML exportados configuran `darkMode: "class"` y cambian la clase raiz, pero no aplican clases `dark:` a las superficies de sus pantallas. Para que el toggle tenga efecto visual real, todas las superficies, textos, bordes, badges, menus y dialogos recibiran variantes claras/oscuras segun `DESIGN.MD`. El tema inicial sera claro y no se guardara entre recargas.

Se conserva la composicion, jerarquia, densidad y lenguaje visual reconocible de Stitch, usando tokens y utilidades Tailwind. No se copiaran bloques CSS `<style>`, atributos `style`, mutaciones visuales con `element.style`, manejadores `onclick`, configuraciones duplicadas ni recursos remotos de Google Fonts/Material Symbols: no cumplen las restricciones de CSS/estilos inline y ausencia de servicios externos. La funcionalidad se implementara con listeners vanilla; los iconos tendran alternativa local accesible. Los menus/modal inician cerrados y los acordeones colapsados aunque la referencia los muestre abiertos.

### Diferencias encontradas en las referencias

- Contrataciones presenta `$48.750` como KPI mientras los cuatro segmentos rotulados suman `$48.700`; no se reutilizara ese grafico como calculo de contratos. Cada total de contrato se obtiene de sus propios precios de skills.
- El catalogo de Skills muestra precios mensuales que no son iguales a algunos precios unitarios de contratos. `SPECS.md` exige sumar los precios del contrato, no igualarlos a una tarifa global del catalogo.
- Agentes muestra cinco agentes: tres activos, uno inactivo y uno fallando. Esta distribucion es un fixture compatible; el Dashboard debe derivar los conteos desde los agentes existentes y visibles.
- Usuarios y errores tienen controles de demo incompletos; errores presenta texto “Live Stream” y accion de resolver que no cambia la fila. La implementacion usara datos ficticios y mutaciones locales, sin afirmar conexion o actividad real.
- `DESIGN.MD` documenta paletas/tokens con `primary: #3525cd` y `primary-container: #4f46e5`, mientras su narrativa llama a `#4f46e5` ancla primaria. Se conserva el mapeo de tokens Stitch y no se redefine la identidad cromatica.

## 15. Contratos de componentes

### Modal singleton

Una unica estructura de dialogo y backdrop recibe un tipo de vista, un ID de entidad y el elemento disparador. El contenido define titulo, cuerpo y acciones para: detalle de usuario, configuracion de prompt, detalle de skill, detalle de contrato y detalle de error. Cierre por boton, clic directo en backdrop y Escape; el panel evita que un clic interno cierre el dialogo. Al abrir, el foco entra al control util inicial; al cerrar vuelve al disparador. Configurar agente mantiene un borrador hasta Guardar; Cancelar descarta el borrador.

### Controlador unico de dropdowns

Los botones de tres puntos informan tipo/ID de entidad. Un controlador cierra el menu anterior y muestra las acciones aplicables: usuarios (detalle/eliminar), agentes (configurar/eliminar), skills (detalle/eliminar), contratos (detalle) y errores (detalle/resolver). Clic exterior cierra; Escape cierra y devuelve el foco. La seleccion ejecuta la accion local y cierra el menu.

### Componentes compartidos

- **Badge:** estado/severidad traducidos a texto visible y clases semanticas con contraste en ambos temas.
- **Sidebar y header:** una sola instancia persistente para las seis vistas; navegacion cambia seccion, titulo y `aria-current`.
- **Toggle de tema:** un control global modifica la clase `dark` del elemento raiz y no usa almacenamiento persistente.
- **Lista colapsable:** un patron por agente con estado independiente, `aria-expanded`, `aria-controls`, teclado y transicion Tailwind; estado inicial cerrado.
- **Tablas, tarjetas KPI y acciones:** patrones de marcado/estilos compartidos; las tablas usan contenedor `overflow-x-auto` donde lo requiera el viewport.

## 16. Reglas tecnicas y de datos

- Entrega de producto: solo `index.html`; HTML5 semantico, Tailwind CSS CDN y JavaScript vanilla. Sin CSS personalizado, atributos `style`, frameworks, librerias, APIs, red, almacenamiento o build.
- Ingresos del Dashboard: valor ficticio fijo `$48.750`. Perdidas por descuentos/cupones: `$3.240`. No se deducen de los contratos.
- Conteos de agentes activos/fallando: derivados del inventario vigente, nunca de valores escritos por separado. La distribucion Stitch de 3 activos, 1 inactivo y 1 fallando es compatible y, si se conserva, produce 3 y 1 en Dashboard.
- Mantener los cinco usuarios indicados, el catalogo de agentes/skills de `SPECS.md`, al menos cuatro contratos y seis errores. Los IDs referenciados deben existir y los conteos de skills derivarse de las asignaciones.
- Los importes se expresan en una unica moneda (USD es la opcion alineada a Stitch). No fijar un precio de contrato a partir de un KPI: cada total se calcula como suma de sus lineas de skills y el modal muestra esos mismos importes.
- Eliminar es una mutacion solo visual/local hasta recargar. Se pueden conservar entidades base ocultas para no romper referencias historicas; las relaciones activas mostradas se actualizan. Al eliminar agente, los conteos operativos se recalculan. Al eliminar skill, se oculta del catalogo y de nuevas asociaciones, manteniendo desglose historico de contratos.
- “Marcar como resuelto” actualiza el registro de error local y no modifica por si solo el estado del agente. Guardar prompt cambia el valor en memoria de sesion; Cancelar no lo cambia.
- Errores y contratos mantienen nombres/IDs validos durante la sesion. No mostrar mensajes de sincronizacion, persistencia remota ni actividad en tiempo real.

## 17. Trazabilidad de aceptacion

La lista normativa es la de los criterios 1-53 inmediatamente anteriores. En `tasks.md` se asigna cobertura asi: 1-8 producto y restricciones; 9-12 Dashboard; 13-18 Usuarios; 19-26 Agentes; 27-32 Skills; 33-38 Contrataciones; 39-42 Errores; 43-53 integracion global, accesibilidad, responsive y reinicio local. No se omite ni altera ningun criterio.

El criterio 1 menciona que no habia HTML antes del primer commit de especificaciones, pero el repositorio contiene cinco referencias Stitch que deben preservarse. Se interpreta como una sola pagina HTML de producto (`index.html`) y las referencias como material de diseño, no como paginas de producto. Una lectura literal de “ningun HTML” seria incompatible con ese estado y requiere resolucion antes de implementacion.

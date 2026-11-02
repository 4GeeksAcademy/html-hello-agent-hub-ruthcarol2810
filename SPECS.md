# Especificaciones: AgentHub

## Objetivo

Crear un prototipo HTML completamente diseñado de un panel de administración para AgentHub, una plataforma SaaS donde las empresas alquilan agentes de IA preconfigurados y los equipan con *skills* —capacidades como navegar por la web, leer documentos o gestionar calendarios— para realizar tareas de negocio. El panel está dirigido a la persona administradora de la plataforma, que necesita supervisar usuarios, agentes, skills, contratos y errores desde una única interfaz.

## Stack y restricciones

- HTML5 semántico, con `index.html` como página principal. Usar correctamente elementos como `header`, `nav`, `main`, `section` y `table`.
- Diseño adaptable a escritorio, tablet y móvil.
- Tailwind CSS mediante CDN; no crear archivos CSS personalizados ni usar atributos `style` en línea.
- JavaScript vanilla para la navegación, las interacciones y los datos simulados; sin frameworks, bibliotecas adicionales ni herramientas de build.
- Los datos de ejemplo se mantienen localmente en JavaScript o JSON. Las operaciones simulan peticiones al backend: no se requiere servidor, persistencia real ni conexiones a una API.
- Mantener consistencia entre secciones: un mismo agente debe conservar el mismo nombre en Gestión de agentes, Contrataciones y Log de errores.
- Diseño limpio y minimalista, basado en un sistema visual plano (*flat design*).

## Navegación y comportamiento global

- El panel incluye seis secciones accesibles desde una barra lateral persistente: Dashboard, Gestión de usuarios, Gestión de agentes, Skills, Contrataciones de agentes y Log de errores. La barra muestra el nombre **AgentHub** y destaca la sección activa.
- Al seleccionar una sección, se muestra su contenido y se actualiza el indicador de sección activa en la barra lateral.
- Una barra superior incluye un control para alternar entre modo claro y oscuro. El cambio afecta a todo el panel mediante las utilidades `dark:` de Tailwind y se conserva al navegar entre secciones.
- Todos los menús desplegables de acciones se cierran al hacer clic fuera de su área.
- Los modales se cierran con su botón de cierre y al hacer clic en el *backdrop*.

## Secciones

### Dashboard

1. Mostrar cuatro tarjetas de métricas: ingresos generados este mes, pérdida total por descuentos y cupones, agentes activos y agentes marcados como fallando. Cada tarjeta incluye un icono, una etiqueta y un valor de ejemplo.
2. Organizar las tarjetas en una cuadrícula responsive 2×2. Usar colores de acento distintos según el tipo de métrica y una sombra sutil.
3. Debajo de las tarjetas, incluir un área de ancho completo con borde discontinuo y una etiqueta centrada que represente un marcador de posición para el gráfico de actividad semanal.

### Gestión de usuarios

1. Mostrar una tabla con al menos cinco usuarios de ejemplo y las columnas nombre, email, plan y estado. El estado se presenta mediante un badge.
2. Incluir en cada fila un menú de acciones activado por un botón `⋮`, con las opciones **Ver detalle** y **Eliminar**.
3. Al seleccionar **Ver detalle**, abrir un modal con el registro completo del usuario. El modal se cierra con su botón de cierre o al hacer clic en el *backdrop*.

### Gestión de agentes

1. Mostrar al menos cuatro agentes de ejemplo. Cada registro incluye el nombre del agente, el propietario, un badge de estado y un control para desplegar sus skills.
2. Representar los estados **Activo** en verde, **Inactivo** en gris y **Fallando** en rojo. 
3. Las skills están ocultas inicialmente; al activar el control se muestran con una transición suave y se vuelven a ocultar al activarlo de nuevo.
4. Incluir en cada registro un menú de acciones `⋮` con **Configurar** y **Eliminar**.
5. Al seleccionar **Configurar**, abrir un modal que muestre el prompt de sistema del agente en un `<textarea>` editable.

### Skills

1. Mostrar un catálogo de al menos cuatro skills, cada una con nombre, descripción breve y cantidad de agentes que la tienen habilitada.
2. Incluir dentro de la sección una explicación breve de qué es una skill en AgentHub. Una capacidad que se puede añadir a un agente para ampliar las tareas que puede realizar.
3. Cada skill tiene un menú `⋮` con las opciones **Ver detalle** y **Eliminar**. **Ver detalle** abre un modal con la información de la skill.

### Contrataciones de agentes

1. Mostrar una tabla con al menos cuatro contratos activos o pasados. Cada fila incluye cliente, agente alquilado, skills contratadas, fechas de inicio y fin, e importe pagado.
2. Incluir en cada fila un menú de acciones `⋮` con la opción **Ver detalle**.
3. Al seleccionar **Ver detalle**, abrir un modal con el desglose del contrato, incluidas las skills contratadas y el precio individual de cada una.

### Log de errores

1. Mostrar al menos seis errores de ejemplo, cada uno con timestamp, nombre del agente, tipo de error, descripción breve y estado (Pendiente/Resuelto).
2. Identificar visualmente el tipo o la gravedad de cada error mediante badges con código de color.
3. Incluir en cada entrada un menú `⋮` con **Ver detalle** y **Marcar como resuelto**. **Ver detalle** abre un modal con la traza completa del error; al marcarlo como resuelto, actualizar su estado visualmente.

## Inventario de componentes

| Componente | Función |
| --- | --- |
| Barra lateral (*sidebar*) | Navegar entre las seis secciones y destacar la vista activa. |
| Tarjeta de métrica | Mostrar las principales métricas de la plataforma. |
| Tabla y fila de datos | Presentar registros y sus acciones. |
| Menú desplegable | Mostrar las acciones disponibles para cada registro. |
| Modal | Mostrar detalles o configuración del registro seleccionado. |
| Badge | Identificar estados de usuarios, agentes y errores. |
| Lista de skills colapsable | Mostrar u ocultar las skills de un agente. |
| Control de tema | Alternar entre los modos claro y oscuro. |
| Gestor de vistas | Mostrar la sección seleccionada y sincronizarla con la barra lateral. |

## Criterios de aceptación

1. Las seis secciones se pueden abrir desde la barra lateral y la sección activa queda resaltada.
2. El Dashboard muestra las cuatro tarjetas de métricas y el marcador de posición para el gráfico semanal.
3. Gestión de usuarios muestra al menos cinco filas. El menú `⋮` ofrece **Ver detalle** y **Eliminar**, y **Ver detalle** abre el registro correspondiente en un modal.
4. Gestión de agentes muestra al menos cuatro agentes con badges de estado correctos. El control de skills las expande y colapsa; **Configurar** abre el prompt de sistema en un `<textarea>` editable.
5. Skills muestra al menos cuatro entradas, su descripción y la cantidad de agentes que las usan. El menú de acciones ofrece **Ver detalle** y **Eliminar**.
6. Contrataciones de agentes muestra al menos cuatro contratos y permite abrir un modal con el desglose de skills y sus precios individuales.
7. Log de errores muestra al menos seis entradas con badges codificados por color; permite abrir la traza completa y marcar una entrada como resuelta.
8. Los modales se cierran tanto con el botón de cierre como al hacer clic en el *backdrop*.
9. Todos los menús de acciones se cierran al hacer clic fuera de ellos.
10. El control de tema alterna entre modo claro y oscuro en todo el panel; la selección se mantiene al navegar entre secciones.
11. La interfaz es usable en viewports de escritorio, tablet y móvil, y los datos de los mismos agentes son consistentes entre las secciones.

## Referencia

Especificaciones adaptadas de [AgentHub UI Specs and Prompts](https://github.com/4GeeksAcademy/ai-engineering-syllabus/blob/main/content/projects/agent-hub-ui-specs-and-prompts/README.es.md).
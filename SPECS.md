# Especificación de Requisitos: Panel de Administración "AgentHub"

## 1. Descripción del Producto
**AgentHub** es una plataforma SaaS B2B que permite a las empresas alquilar "Agentes de IA" preconfigurados y equiparlos con diferentes "skills" (habilidades como navegación web, manejo de bases de datos, etc.) para tareas de negocio específicas. 
**Usuario objetivo:** El administrador interno de AgentHub, quien usará este panel para monitorizar métricas de ingresos, gestionar el catálogo de agentes y skills, supervisar los contratos activos de los clientes y auditar errores del sistema en tiempo real.

## 2. Stack Tecnológico y Restricciones
*   **HTML:** HTML5 semántico (`<nav>`, `<main>`, `<section>`, `<header>`, etc.). Estructurado en un único `index.html` (o varios enlazados).
*   **Estilos:** Tailwind CSS implementado **exclusivamente vía CDN**. 
    *   No se permiten archivos CSS externos.
    *   No se permiten atributos `style` en línea.
*   **Interactividad:** JavaScript Vanilla únicamente. 
    *   Cero frameworks o librerías externas (Ni React, Vue, jQuery, etc.).
*   **Datos:** 100% hardcodeados (ficticios), pero consistentes entre vistas. Sin conexiones a backend ni APIs.

## 3. Especificaciones por Sección

### 3.1. Dashboard
1. **Tarjetas de Métricas:** Cuatro tarjetas dispuestas en una cuadrícula responsive (2x2 en tablet/escritorio). Muestran: ingresos totales, pérdidas por descuentos, agentes activos y agentes fallando. Cada tarjeta incluye un icono representativo, una etiqueta descriptiva y un valor hardcodeado.
2. **Estilo de Tarjetas:** Las tarjetas usan colores de acento distintos dependiendo del tipo de métrica (ej. rojo para pérdidas o agentes fallando, verde/azul para ingresos/activos) e incluyen una sombra sutil para destacar sobre el fondo.
3. **Gráfico de Actividad:** Justo debajo de las tarjetas, un elemento `div` de ancho completo con un borde discontinuo, un alto predefinido y una etiqueta de texto centrada que sirve como "marcador de posición" (placeholder) para el futuro gráfico de actividad semanal.

### 3.2. Gestión de Usuarios
1. **Tabla de Datos:** Una tabla con al menos 5 filas de usuarios hardcodeados. Las columnas deben ser: Nombre, Email, Plan (ej. Pro, Enterprise) y un Badge visual indicando el Estado (Activo, Inactivo).
2. **Dropdown de Acciones:** Cada fila tiene una celda final con un botón de tres puntos verticales (`⋮`). Al hacer clic, despliega un menú flotante con las opciones "Ver detalle" y "Eliminar".
3. **Interacción del Modal:** Al hacer clic en "Ver detalle", se abre un Modal (overlay oscuro) con el registro completo del usuario. El modal se cierra haciendo clic en un botón de cierre interno o haciendo clic fuera del contenido (en el backdrop).

### 3.3. Gestión de Agentes
1. **Listado de Agentes:** Una tabla o listado de al menos 4 agentes. Muestra: Nombre del Agente, Propietario (Cliente), un Badge de estado (activo/inactivo/fallando) y una sección para skills.
2. **Lista de Skills Colapsable:** Las skills de cada agente están ocultas por defecto. Existe un control (botón/icono de flecha) que, al hacer clic, revela la lista de skills con una transición visual suave (CSS transition). Al hacer clic nuevamente, se colapsa.
3. **Configuración de Prompts:** El menú de acciones (`⋮`) incluye "Configurar" y "Eliminar". Al elegir "Configurar", se abre un Modal que muestra el "System Prompt" del agente dentro de una etiqueta `<textarea>` editable.

### 3.4. Skills
1. **Explicación Contextual:** En la parte superior de la sección, existe un bloque de texto o banner que ofrece una breve explicación sobre qué es una "skill" en el contexto específico de AgentHub.
2. **Catálogo de Skills:** Un listado de al menos 4 skills disponibles, mostrando el Nombre de la skill, una descripción breve de lo que hace, y un contador que indica cuántos agentes la tienen habilitada actualmente.
3. **Opciones de Skill:** Cada skill listada posee un dropdown de acciones (`⋮`) con las opciones "Ver detalle" y "Eliminar".

### 3.5. Contrataciones de Agentes
1. **Tabla de Contratos:** Una tabla detallada con al menos 4 registros de alquileres mostrando: Nombre del cliente, Agente alquilado, cantidad de Skills contratadas, Fechas de inicio/fin y el Importe total pagado.
2. **Desglose de Contrato:** Cada fila tiene el menú de acciones (`⋮`). 
3. **Modal de Facturación:** La opción "Ver detalle" abre un Modal de desglose completo del contrato. Este modal debe contener una lista desglosada que muestre cada skill contratada y su precio individual, sumando al total.

### 3.6. Log de Errores
1. **Registro de Fallos:** Una tabla/lista de al menos 6 entradas de error hardcodeadas, mostrando: Timestamp (fecha/hora), Nombre del agente afectado, un Badge de tipo de error, y una descripción breve.
2. **Categorización Visual:** Los Badges de tipo de error deben estar diferenciados por un código de color representativo de su gravedad (ej. Rojo = Crítico, Naranja = Warning, Azul = Info).
3. **Resolución de Errores:** El dropdown de acciones (`⋮`) incluye las opciones "Ver detalle" (que abre un modal con el código simulado del error) y una acción directa de "Marcar como resuelto".

## 4. Inventario de Componentes UI Reutilizables
Para mantener la coherencia y modularidad en Tailwind, el diseño se basa en los siguientes componentes recurrentes:
1.  **Sidebar (Barra Lateral):** Menú de navegación principal persistente con indicador de vista activa.
2.  **Toggle de Modo Oscuro:** Botón en la barra superior para cambiar el esquema de color.
3.  **Tarjeta de Métrica (Metric Card):** Contenedor con sombra, icono, título y valor grande.
4.  **Dropdown de Acciones (`⋮`):** Menú flotante posicionado de forma relativa a su disparador.
5.  **Modal Overlay:** Contenedor de pantalla completa con un backdrop oscuro semitransparente, panel central de contenido y botón de cierre.
6.  **Badge de Estado:** Etiqueta pequeña con bordes redondeados y colores de fondo/texto específicos.
7.  **Lista Colapsable (Accordion):** Contenedor que expande/contrae su altura mediante interacciones.

## 5. Criterios de Aceptación
Para que el prototipo se considere completado y listo, debe cumplir obligatoriamente lo siguiente:
1.  **Layout y Semántica:** El HTML usa etiquetas semánticas (`section`, `table`, `nav`, `header`, `main`) y el layout es perfectamente funcional tanto en viewports de escritorio como de tablet.
2.  **Estricto Tailwind CSS:** Se emplean las clases utilitarias de Tailwind de forma consistente en todo el proyecto vía CDN. No hay archivos `.css` externos ni atributos `style=""`.
3.  **Funcionamiento del Modo Oscuro:** El Toggle de modo oscuro/claro cambia exitosamente el esquema de color de *todo* el panel usando las utilidades `dark:` de Tailwind.
4.  **Funcionamiento de Dropdowns:** Todos los Dropdowns de acciones (`⋮`) se abren al hacer clic en ellos, se cierran al elegir una opción y **se cierran al hacer clic en cualquier lugar fuera de su área**.
5.  **Funcionamiento de Modales:** La acción "Ver detalle" abre con éxito un Modal en al menos cuatro secciones distintas. Todos los modales se cierran usando el botón interno ("X" o "Cerrar") Y al hacer clic en el backdrop oscuro.
6.  **Funcionamiento Colapsable:** La lista de skills en la vista de Agentes permanece colapsada por defecto y se expande/colapsa al hacer clic en su respectivo botón, mostrando una transición visual suave.
7.  **Coherencia de Datos:** Los nombres e información hardcodeada son lógicos (por ejemplo, los nombres de agentes que aparecen en "Gestión de agentes" son los mismos que aparecen fallando en el "Log de errores").
8.  **Puro JavaScript:** No existe ninguna dependencia de frameworks para la interactividad, validado directamente en las etiquetas `<script>`.
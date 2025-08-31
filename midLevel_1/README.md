# 🎨 Módulo 4: CSS Grid y Flexbox Avanzado

## 🧭 Navegación del Curso

- **⬅️ Anterior**: [Módulo 3: Responsive Design](../junior_3/README.md)
- **➡️ Siguiente**: [Módulo 5: Animaciones y Transiciones](../midLevel_2/README.md)
- **📚 [Índice Completo](../INDICE_COMPLETO.md)** | **[🧭 Navegación Rápida](../NAVEGACION_RAPIDA.md)**

---

## 📚 Descripción del Módulo

En este módulo avanzarás significativamente en tus habilidades de layout CSS. Aprenderás CSS Grid completo, desde conceptos básicos hasta técnicas avanzadas, y profundizarás en Flexbox para crear layouts complejos y profesionales. Este módulo te dará el poder de crear cualquier tipo de layout que puedas imaginar, con control total sobre la disposición de elementos en la página.

## 🎯 Objetivos de Aprendizaje

Al completar este módulo, serás capaz de:

- ✅ Dominar CSS Grid completo con todas sus propiedades
- ✅ Crear layouts complejos usando Grid y Flexbox combinados
- ✅ Implementar auto-fit y auto-fill para layouts responsivos
- ✅ Usar Subgrid (CSS Grid Level 2) para layouts anidados
- ✅ Crear masonry layouts y galerías avanzadas
- ✅ Optimizar layouts para diferentes dispositivos y contenidos

## 📖 Contenido del Módulo

### 4.1 CSS Grid Completo - Fundamentos

#### ¿Qué es CSS Grid y por qué es tan poderoso?

CSS Grid es un sistema de layout bidimensional que te permite crear layouts complejos con filas y columnas. Es como tener una cuadrícula invisible donde puedes colocar elementos exactamente donde quieras.

**Ventajas de CSS Grid:**
- **Control bidimensional**: Puedes controlar tanto filas como columnas
- **Layouts complejos**: Crea layouts que antes eran imposibles
- **Responsive nativo**: Se adapta automáticamente al contenido
- **Menos código**: Logra más con menos CSS

#### Configuración Básica del Grid

```css
/* Paso 1: Convertir un contenedor en grid */
.grid-container {
    display: grid;
    /* Ahora todos los hijos directos se convierten en grid items */
}

/* Paso 2: Definir la estructura de columnas */
.grid-container {
    display: grid;
    grid-template-columns: 200px 200px 200px;
    /* Crea 3 columnas de 200px cada una */
}

/* Paso 3: Definir la estructura de filas */
.grid-container {
    display: grid;
    grid-template-columns: 200px 200px 200px;
    grid-template-rows: 100px 100px;
    /* Crea 2 filas de 100px cada una */
}
```

#### Unidades de Grid - Explicación Detallada

**fr (Fracción) - La unidad más poderosa del Grid:**
```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    /* 
    Explicación paso a paso:
    - 1fr = toma 1 parte del espacio disponible
    - 2fr = toma 2 partes del espacio disponible  
    - 1fr = toma 1 parte del espacio disponible
    - Total: 4 partes
    - Si el contenedor tiene 400px de ancho:
      * Primera columna: 100px (1/4 de 400px)
      * Segunda columna: 200px (2/4 de 400px)
      * Tercera columna: 100px (1/4 de 400px)
    */
}
```

**minmax() - Controla el tamaño mínimo y máximo:**
```css
.grid-container {
    display: grid;
    grid-template-columns: minmax(200px, 1fr) minmax(300px, 2fr);
    /* 
    Explicación:
    - Primera columna: mínimo 200px, máximo 1fr
    - Segunda columna: mínimo 300px, máximo 2fr
    - Esto garantiza que las columnas nunca sean muy pequeñas
    */
}
```

**repeat() - Repite patrones automáticamente:**
```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    /* Equivale a: 1fr 1fr 1fr */
    
    grid-template-columns: repeat(4, minmax(200px, 1fr));
    /* Equivale a: minmax(200px, 1fr) minmax(200px, 1fr) minmax(200px, 1fr) minmax(200px, 1fr) */
}
```

### 4.2 Propiedades Avanzadas de Grid Template

#### Grid Template Areas - Layouts Visuales

Grid Template Areas te permite crear layouts visuales dibujándolos con texto. Es como hacer un boceto de tu layout directamente en CSS.

```css
/* Paso 1: Define las áreas con nombres descriptivos */
.grid-container {
    display: grid;
    grid-template-areas: 
        "header header header"
        "sidebar content content"
        "footer footer footer";
    /* 
    Explicación visual:
    ┌─────────┬─────────┬─────────┐
    │ header  │ header  │ header  │
    ├─────────┼─────────┼─────────┤
    │ sidebar │ content │ content │
    ├─────────┼─────────┼─────────┤
    │ footer  │ footer  │ footer  │
    └─────────┴─────────┴─────────┘
    */
}

/* Paso 2: Asigna elementos a las áreas */
.header {
    grid-area: header;
    /* Este elemento ocupará toda la primera fila */
}

.sidebar {
    grid-area: sidebar;
    /* Este elemento ocupará la primera columna de la segunda fila */
}

.content {
    grid-area: content;
    /* Este elemento ocupará las columnas 2 y 3 de la segunda fila */
}

.footer {
    grid-area: footer;
    /* Este elemento ocupará toda la tercera fila */
}
```

#### Grid Template Rows y Columns Avanzados

**Crear filas de diferentes alturas:**
```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    grid-template-rows: 80px 200px 100px 60px;
    /* 
    Explicación:
    - Primera fila: 80px (header)
    - Segunda fila: 200px (contenido principal)
    - Tercera fila: 100px (contenido secundario)
    - Cuarta fila: 60px (footer)
    */
}
```

**Usar auto para filas que se ajusten al contenido:**
```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    grid-template-rows: 80px auto 100px 60px;
    /* 
    Explicación:
    - Primera fila: 80px (altura fija)
    - Segunda fila: auto (se ajusta al contenido más alto)
    - Tercera fila: 100px (altura fija)
    - Cuarta fila: 60px (altura fija)
    */
}
```

### 4.3 Gap y Espaciado en Grid

#### Grid Gap - Espaciado entre elementos

Grid Gap es la forma moderna y limpia de crear espaciado entre elementos del grid. Es más simple y eficiente que usar margin.

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    
    /* Gap básico - mismo espaciado en filas y columnas */
    gap: 20px;
    
    /* Gap específico - diferente para filas y columnas */
    gap: 20px 30px; /* row-gap column-gap */
    
    /* Gap individual */
    row-gap: 20px;      /* Espaciado entre filas */
    column-gap: 30px;   /* Espaciado entre columnas */
}
```

**Ejemplo práctico con gap:**
```css
.photo-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 20px;
    padding: 20px;
    /* 
    Explicación:
    - Las imágenes se organizan en columnas de mínimo 250px
    - Hay 20px de espacio entre cada imagen
    - El padding exterior es de 20px
    - Resultado: galería limpia y organizada
    */
}
```

### 4.4 Posicionamiento de Elementos en Grid

#### Grid Column y Grid Row - Control preciso

Estas propiedades te permiten controlar exactamente dónde se coloca cada elemento en el grid.

```css
.grid-item {
    /* Posicionamiento básico */
    grid-column: 1 / 3;  /* Desde la línea 1 hasta la línea 3 */
    grid-row: 2 / 4;     /* Desde la línea 2 hasta la línea 4 */
    
    /* Posicionamiento con span */
    grid-column: 1 / span 2;  /* Desde la línea 1, ocupando 2 columnas */
    grid-row: 2 / span 2;     /* Desde la línea 2, ocupando 2 filas */
    
    /* Posicionamiento con nombres de área */
    grid-column: sidebar;
    grid-row: content;
}
```

**Ejemplo práctico - Layout de blog:**
```css
.blog-layout {
    display: grid;
    grid-template-columns: 250px 1fr 300px;
    grid-template-rows: auto auto 1fr auto;
    gap: 20px;
}

.header {
    grid-column: 1 / -1;  /* Desde la primera línea hasta la última */
    grid-row: 1;
}

.sidebar {
    grid-column: 1;
    grid-row: 2 / 4;  /* Desde la fila 2 hasta la 4 */
}

.main-content {
    grid-column: 2;
    grid-row: 2 / 4;
}

.advertisement {
    grid-column: 3;
    grid-row: 2 / 4;
}

.footer {
    grid-column: 1 / -1;
    grid-row: 4;
}
```

### 4.5 Flexbox Avanzado - Profundizando en el Control

#### Flex Grow, Shrink y Basis - El trío poderoso

Estas tres propiedades controlan cómo los elementos flex crecen, se encogen y establecen su tamaño base.

**Flex Grow - Control del crecimiento:**
```css
.flex-item {
    flex-grow: 0;    /* No crece (valor por defecto) */
    flex-grow: 1;    /* Crece para llenar el espacio disponible */
    flex-grow: 2;    /* Crece el doble que un elemento con flex-grow: 1 */
}

/* Ejemplo práctico - Layout de navegación */
.nav-container {
    display: flex;
    gap: 20px;
}

.nav-item {
    flex-grow: 0;  /* Mantiene su tamaño natural */
}

.nav-item.active {
    flex-grow: 1;  /* El elemento activo crece para llenar espacio */
}
```

**Flex Shrink - Control del encogimiento:**
```css
.flex-item {
    flex-shrink: 1;  /* Se encoge si es necesario (valor por defecto) */
    flex-shrink: 0;  /* No se encoge, mantiene su tamaño */
    flex-shrink: 2;  /* Se encoge el doble que un elemento normal */
}

/* Ejemplo práctico - Sidebar que no se encoge */
.layout {
    display: flex;
}

.sidebar {
    flex: 0 0 250px;  /* grow: 0, shrink: 0, basis: 250px */
    /* La sidebar mantiene siempre 250px de ancho */
}

.content {
    flex: 1;  /* grow: 1, shrink: 1, basis: 0% */
    /* El contenido crece y se encoge según el espacio disponible */
}
```

**Flex Basis - Tamaño base del elemento:**
```css
.flex-item {
    flex-basis: auto;     /* Tamaño basado en el contenido */
    flex-basis: 200px;    /* Tamaño fijo de 200px */
    flex-basis: 50%;      /* 50% del contenedor padre */
    flex-basis: 0;        /* Tamaño mínimo, solo el contenido */
}

/* Ejemplo práctico - Cards de igual tamaño */
.card-container {
    display: flex;
    gap: 20px;
}

.card {
    flex: 1 1 300px;  /* grow: 1, shrink: 1, basis: 300px */
    /* 
    Explicación:
    - grow: 1 = crece para llenar espacio
    - shrink: 1 = se encoge si es necesario
    - basis: 300px = tamaño ideal de 300px
    - Resultado: cards que se adaptan pero mantienen proporciones
    */
}
```

### 4.6 Auto-fit y Auto-fill - Grids Inteligentes

#### Auto-fit vs Auto-fill - Diferencias clave

Estas dos funciones crean columnas automáticamente, pero se comportan de manera diferente.

**Auto-fit - Se adapta al contenido:**
```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    /* 
    Explicación paso a paso:
    1. repeat(auto-fit, ...) = crea tantas columnas como quepan
    2. minmax(250px, 1fr) = cada columna tiene mínimo 250px, máximo 1fr
    3. auto-fit = las columnas vacías se colapsan y las demás se expanden
    4. Resultado: layout que se adapta perfectamente al contenido
    */
}
```

**Auto-fill - Mantiene la estructura:**
```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    /* 
    Explicación paso a paso:
    1. repeat(auto-fill, ...) = crea tantas columnas como quepan
    2. minmax(250px, 1fr) = cada columna tiene mínimo 250px, máximo 1fr
    3. auto-fill = mantiene todas las columnas, incluso las vacías
    4. Resultado: estructura consistente pero puede dejar espacios vacíos
    */
}
```

**Comparación práctica:**
```css
/* Auto-fit - Ideal para galerías de imágenes */
.photo-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    /* 
    Ventajas:
    - Las imágenes se distribuyen uniformemente
    - No hay espacios vacíos
    - Se adapta perfectamente al número de imágenes
    */
}

/* Auto-fill - Ideal para layouts de dashboard */
.dashboard-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    /* 
    Ventajas:
    - Mantiene la estructura visual
    - Espacios vacíos para futuros widgets
    - Layout consistente independientemente del contenido
    */
}
```

### 4.7 Subgrid - CSS Grid Level 2

#### ¿Qué es Subgrid y por qué es revolucionario?

Subgrid permite que los elementos hijos de un grid item también se comporten como un grid, creando layouts anidados perfectamente alineados.

**Problema sin Subgrid:**
```css
/* Sin subgrid - los elementos internos no se alinean */
.card-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

.card {
    /* Cada card es un grid item, pero su contenido interno no se alinea */
    display: grid;
    grid-template-columns: 1fr 1fr;
    /* Los elementos internos no se alinean con las otras cards */
}
```

**Solución con Subgrid:**
```css
.card-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}

.card {
    display: grid;
    grid-template-columns: subgrid;  /* Hereda las columnas del padre */
    /* 
    Explicación:
    1. subgrid = hereda la estructura de columnas del grid padre
    2. Los elementos internos se alinean perfectamente con otras cards
    3. Cambios en el grid padre se reflejan automáticamente en las cards
    4. Resultado: alineación perfecta sin código adicional
    */
}
```

**Ejemplo práctico - Timeline con subgrid:**
```css
.timeline {
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 30px;
}

.timeline-item {
    display: grid;
    grid-template-columns: subgrid;  /* Hereda las 2 columnas del padre */
    align-items: center;
}

.timeline-date {
    grid-column: 1;  /* Primera columna (200px) */
    text-align: right;
}

.timeline-content {
    grid-column: 2;  /* Segunda columna (1fr) */
    padding-left: 20px;
}
```

### 4.8 Masonry Layouts - Galerías Avanzadas

#### ¿Qué es un Masonry Layout?

Un Masonry Layout es un tipo de galería donde las imágenes se organizan de manera que llenan espacios vacíos, creando un patrón visual atractivo.

**Implementación con CSS Grid:**
```css
.masonry-gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    grid-auto-rows: 20px;  /* Altura base de cada fila */
    gap: 10px;
}

.masonry-item {
    /* Cada item puede ocupar múltiples filas */
    grid-row: span var(--row-span);
    /* 
    Explicación:
    1. grid-auto-rows: 20px = crea filas de 20px
    2. grid-row: span var(--row-span) = cada item ocupa múltiples filas
    3. --row-span se calcula con JavaScript basado en la altura de la imagen
    4. Resultado: layout que se adapta al contenido
    */
}
```

**JavaScript para calcular el span:**
```javascript
// Función para calcular cuántas filas debe ocupar cada imagen
function calculateMasonryLayout() {
    const items = document.querySelectorAll('.masonry-item');
    const rowHeight = 20; // Debe coincidir con grid-auto-rows
    
    items.forEach(item => {
        const height = item.offsetHeight;
        const rowSpan = Math.ceil(height / rowHeight);
        item.style.setProperty('--row-span', rowSpan);
    });
}

// Ejecutar cuando las imágenes se cargan
window.addEventListener('load', calculateMasonryLayout);
```

### 4.9 Layouts Complejos Combinando Grid y Flexbox

#### Estrategia: Grid para la estructura, Flexbox para el contenido

Esta es la estrategia más poderosa: usar CSS Grid para crear la estructura general y Flexbox para organizar el contenido dentro de cada sección.

**Ejemplo: Dashboard empresarial:**
```css
.dashboard {
    display: grid;
    grid-template-areas: 
        "header header header"
        "sidebar main widgets"
        "sidebar charts charts"
        "footer footer footer";
    grid-template-columns: 250px 1fr 300px;
    grid-template-rows: 80px 1fr 300px 60px;
    gap: 20px;
    height: 100vh;
}

/* Header con Flexbox para navegación */
.header {
    grid-area: header;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 20px;
    background: #2c3e50;
    color: white;
}

/* Sidebar con Flexbox para menú vertical */
.sidebar {
    grid-area: sidebar;
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 20px;
    background: #34495e;
    color: white;
}

/* Área principal con Grid para widgets */
.main {
    grid-area: main;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 20px;
    padding: 20px;
}

/* Widgets con Flexbox para contenido */
.widget {
    display: flex;
    flex-direction: column;
    gap: 15px;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

/* Área de gráficos con Grid para diferentes tipos */
.charts {
    grid-area: charts;
    display: grid;
    grid-template-columns: 2fr 1fr;
    gap: 20px;
    padding: 20px;
}

/* Footer con Flexbox para distribución */
.footer {
    grid-area: footer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 20px;
    background: #2c3e50;
    color: white;
}
```

## 🧪 Ejercicios Prácticos

### **Ejercicio 1: Grid Básico con Explicaciones**
Crea un grid de 3x3 con explicaciones detalladas de cada propiedad.

**Instrucciones paso a paso:**
1. **Crea el HTML**: 9 divs con clases descriptivas
2. **Configura el Grid**: Usa `display: grid`
3. **Define columnas**: Usa `grid-template-columns: repeat(3, 1fr)`
4. **Define filas**: Usa `grid-template-rows: repeat(3, 100px)`
5. **Añade gap**: Usa `gap: 20px`
6. **Explica cada propiedad**: Comenta qué hace cada línea de CSS

**Requisitos:**
- Usa colores diferentes para cada celda
- Añade texto explicativo en cada celda
- Comenta cada propiedad CSS explicando su función

### **Ejercicio 2: Layout de Blog con Grid Areas**
Crea un layout de blog usando grid-template-areas.

**Instrucciones paso a paso:**
1. **Planifica el layout**: Dibuja un boceto de tu blog
2. **Define las áreas**: Usa nombres descriptivos como "header", "nav", "main", "sidebar"
3. **Crea el grid**: Usa `grid-template-areas` para definir la estructura
4. **Asigna elementos**: Usa `grid-area` para posicionar cada sección
5. **Hazlo responsive**: Usa media queries para cambiar el layout en móvil

**Requisitos:**
- Header que ocupa todo el ancho
- Navegación horizontal debajo del header
- Contenido principal y sidebar en dos columnas
- Footer que ocupa todo el ancho
- Layout que se adapte a móvil

### **Ejercicio 3: Galería de Imágenes Responsiva**
Implementa una galería que se adapte automáticamente al número de imágenes.

**Instrucciones paso a paso:**
1. **Crea el contenedor**: Usa `display: grid`
2. **Configura auto-fit**: Usa `repeat(auto-fit, minmax(250px, 1fr))`
3. **Añade gap**: Usa `gap: 20px`
4. **Haz las imágenes responsivas**: Usa `width: 100%` y `height: auto`
5. **Añade hover effects**: Usa `transform: scale()` y `transition`

**Requisitos:**
- Las columnas se ajustan automáticamente al ancho de pantalla
- Las imágenes mantienen su proporción
- Efectos hover suaves y atractivos
- Funciona en todos los tamaños de pantalla

### **Ejercicio 4: Dashboard con Grid y Flexbox**
Construye un dashboard que combine Grid para la estructura y Flexbox para el contenido.

**Instrucciones paso a paso:**
1. **Crea la estructura con Grid**: Define áreas para header, sidebar, main, widgets
2. **Usa Flexbox en el header**: Para navegación horizontal
3. **Usa Flexbox en la sidebar**: Para menú vertical
4. **Organiza widgets con Grid**: Para diferentes tamaños de widgets
5. **Haz el footer con Flexbox**: Para distribución de elementos

**Requisitos:**
- Header con navegación y perfil de usuario
- Sidebar con menú de navegación
- Área principal con widgets organizados
- Widgets de diferentes tamaños
- Footer con información y enlaces

### **Ejercicio 5: Sistema de Cards con Subgrid**
Implementa un sistema de cards usando subgrid para alineación perfecta.

**Instrucciones paso a paso:**
1. **Crea el contenedor principal**: Usa Grid con columnas definidas
2. **Configura las cards**: Usa `display: grid` en cada card
3. **Implementa subgrid**: Usa `grid-template-columns: subgrid`
4. **Organiza el contenido interno**: Usa `grid-column` para posicionar elementos
5. **Añade estilos**: Usa colores, sombras y espaciado consistente

**Requisitos:**
- Cards de igual ancho pero altura variable
- Contenido interno perfectamente alineado
- Imagen, título, descripción y botón en cada card
- Hover effects y transiciones suaves

### **Ejercicio 6: Timeline con Grid Avanzado**
Crea una timeline vertical usando técnicas avanzadas de Grid.

**Instrucciones paso a paso:**
1. **Crea la estructura**: Usa Grid con 2 columnas (fecha y contenido)
2. **Posiciona elementos**: Usa `grid-row` para controlar la altura
3. **Añade líneas conectoras**: Usa pseudo-elementos `::before` o `::after`
4. **Haz la timeline responsive**: Usa media queries para cambiar el layout
5. **Añade animaciones**: Usa `@keyframes` para efectos de entrada

**Requisitos:**
- Fechas alineadas a la izquierda
- Contenido alineado a la derecha
- Líneas conectoras entre elementos
- Responsive design
- Animaciones de entrada

### **Ejercicio 7: Masonry Layout con JavaScript**
Implementa un masonry layout que se calcule dinámicamente.

**Instrucciones paso a paso:**
1. **Crea el contenedor**: Usa Grid con `grid-auto-rows: 20px`
2. **Configura las columnas**: Usa `repeat(auto-fill, minmax(200px, 1fr))`
3. **Escribe el JavaScript**: Calcula el `row-span` basado en la altura real
4. **Aplica el span**: Usa `grid-row: span var(--row-span)`
5. **Optimiza el rendimiento**: Usa `ResizeObserver` para cambios dinámicos

**Requisitos:**
- Las imágenes se organizan automáticamente
- No hay espacios vacíos
- Se adapta a diferentes tamaños de imagen
- Funciona con contenido dinámico
- Performance optimizada

### **Ejercicio 8: Sistema de Grid de 12 Columnas**
Desarrolla un sistema de grid profesional como Bootstrap.

**Instrucciones paso a paso:**
1. **Define las variables CSS**: Usa `:root` para breakpoints y gutters
2. **Crea las clases base**: `.row`, `.col`, `.container`
3. **Implementa las columnas**: Usa `grid-template-columns: repeat(12, 1fr)`
4. **Crea clases utilitarias**: `.col-1`, `.col-2`, hasta `.col-12`
5. **Añade responsive**: Usa media queries para diferentes breakpoints

**Requisitos:**
- Sistema de 12 columnas
- Clases utilitarias para diferentes tamaños
- Responsive breakpoints
- Gutter configurable
- Compatible con diferentes navegadores

### **Ejercicio 9: Layout de E-commerce**
Crea un layout completo para una tienda online.

**Instrucciones paso a paso:**
1. **Planifica las secciones**: Header, navegación, filtros, productos, paginación
2. **Usa Grid para la estructura**: Define áreas principales
3. **Implementa filtros con Flexbox**: Para opciones de búsqueda
4. **Crea la grilla de productos**: Usa Grid con auto-fit
5. **Añade paginación**: Usa Flexbox para los controles

**Requisitos:**
- Header con logo, búsqueda y carrito
- Sidebar con filtros y categorías
- Grid de productos responsivo
- Paginación funcional
- Layout que se adapte a móvil

### **Ejercicio 10: Portfolio con Grid Avanzado**
Desarrolla un portfolio que demuestre todas las técnicas aprendidas.

**Instrucciones paso a paso:**
1. **Crea la estructura principal**: Usa Grid para el layout general
2. **Implementa hero section**: Usa Grid para organizar contenido
3. **Crea galería de proyectos**: Usa auto-fit y masonry
4. **Añade sección de habilidades**: Usa Grid para organizar iconos
5. **Implementa contacto**: Usa Flexbox para formularios

**Requisitos:**
- Hero section impactante
- Galería de proyectos con filtros
- Sección de habilidades organizada
- Formulario de contacto funcional
- Diseño moderno y profesional

## 🎯 Proyecto Integrador: Dashboard Administrativo con Layout Complejo

### Descripción del Proyecto
Crea un dashboard administrativo completo que demuestre dominio de CSS Grid y Flexbox avanzado. Este proyecto debe ser funcional, responsive y visualmente atractivo.

### Requisitos del Proyecto

#### **Estructura HTML (25%)**
- Header con navegación y perfil de usuario
- Sidebar con menú de navegación expandible
- Área principal con widgets organizados
- Sección de gráficos y estadísticas
- Footer con información y enlaces

#### **Layout CSS (40%)**
- Uso de CSS Grid para la estructura principal
- Implementación de grid-template-areas
- Uso de Flexbox para contenido interno
- Sistema de grid responsivo
- Implementación de subgrid donde sea apropiado

#### **Componentes Avanzados (20%)**
- Widgets de diferentes tamaños y tipos
- Sistema de navegación con estados
- Gráficos y visualizaciones de datos
- Tablas responsivas con scroll horizontal
- Modales y overlays

#### **Responsive Design (15%)**
- Layout que se adapte a móvil, tablet y desktop
- Sidebar colapsable en móvil
- Widgets que se reorganizan según el dispositivo
- Navegación adaptativa
- Touch-friendly en dispositivos móviles

### Entregables
1. **Archivo HTML** (`index.html`)
2. **Archivo CSS** (`styles.css`)
3. **JavaScript** (`script.js`) - Para funcionalidad básica
4. **README** explicando las decisiones de layout y técnicas utilizadas
5. **Capturas de pantalla** en diferentes dispositivos
6. **Demo funcional** con datos de ejemplo

### Criterios de Evaluación
- **Layout**: Estructura sólida y bien organizada usando Grid y Flexbox
- **Responsive**: Funciona perfectamente en todos los dispositivos
- **Componentes**: Widgets bien diseñados y funcionales
- **Código**: CSS limpio, organizado y bien comentado
- **UX**: Experiencia de usuario intuitiva y atractiva

## 📚 Recursos Adicionales

### Documentación
- [MDN CSS Grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)
- [MDN Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)
- [CSS Grid Level 2](https://www.w3.org/TR/css-grid-2/)

### Herramientas
- [CSS Grid Generator](https://cssgrid-generator.netlify.app/)
- [Flexbox Playground](https://codepen.io/enxaneta/full/adLPwv/)
- [Grid by Example](https://gridbyexample.com/)

### Práctica
- [CSS Grid Garden](https://cssgridgarden.com/) - Aprende CSS Grid jugando
- [Flexbox Froggy](https://flexboxfroggy.com/) - Aprende Flexbox jugando
- [Grid Critters](https://gridcritters.com/) - Juego avanzado de CSS Grid

## 🔍 Preguntas de Repaso

1. **¿Cuál es la diferencia entre CSS Grid y Flexbox?**
2. **¿Qué hace la propiedad `grid-template-areas`?**
3. **¿Cómo funciona `auto-fit` vs `auto-fill`?**
4. **¿Qué es subgrid y cuándo se usa?**
5. **¿Cómo se crea un masonry layout con CSS Grid?**
6. **¿Cuál es la diferencia entre `fr` y `%` en Grid?**
7. **¿Cómo se combinan Grid y Flexbox efectivamente?**
8. **¿Qué hace `minmax()` y cuándo es útil?**
9. **¿Cómo se hace un grid responsive sin media queries?**
10. **¿Cuáles son las mejores prácticas para layouts complejos?**

## 🚀 Siguiente Paso

Una vez que hayas completado este módulo y el proyecto integrador, estarás listo para continuar con el **Módulo 5: Animaciones y Transiciones**, donde aprenderás a crear experiencias web dinámicas y atractivas con CSS.

---

## 🧭 Navegación del Curso

- **⬅️ Anterior**: [Módulo 3: Responsive Design](../junior_3/README.md)
- **➡️ Siguiente**: [Módulo 5: Animaciones y Transiciones](../midLevel_2/README.md)
- **📚 [Índice Completo](../INDICE_COMPLETO.md)** | **[🧭 Navegación Rápida](../NAVEGACION_RAPIDA.md)**

---

**¡Excelente trabajo! Ahora tienes el poder de crear cualquier tipo de layout que puedas imaginar con CSS Grid y Flexbox.** 🎉

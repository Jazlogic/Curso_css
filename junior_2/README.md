# 🎨 Módulo 2: Layout y Box Model

## 📚 Descripción del Módulo

En este módulo profundizarás en el corazón del layout CSS: el Box Model. Aprenderás cómo los elementos se comportan en el flujo del documento, cómo controlar su tamaño y posición, y cómo crear layouts básicos usando diferentes técnicas de posicionamiento. También te introducirás a Flexbox, una herramienta poderosa para crear layouts flexibles y responsivos.

## 🎯 Objetivos de Aprendizaje

Al completar este módulo, serás capaz de:

- ✅ Comprender completamente el Box Model CSS
- ✅ Controlar el comportamiento de elementos con propiedades display
- ✅ Implementar diferentes tipos de posicionamiento
- ✅ Trabajar con float y clear para layouts tradicionales
- ✅ Crear layouts básicos con Flexbox
- ✅ Manejar overflow y z-index efectivamente

## 📖 Contenido del Módulo

### 2.1 Box Model Completo

#### ¿Qué es el Box Model?
El Box Model es el modelo que define cómo se calcula el tamaño y espacio de cada elemento HTML. Cada elemento se trata como una caja rectangular con las siguientes propiedades:

```css
/* Box Model completo */
.element {
    /* Contenido */
    width: 200px;
    height: 100px;
    
    /* Padding - espacio interno */
    padding: 20px;
    
    /* Border - borde */
    border: 2px solid #333;
    
    /* Margin - espacio externo */
    margin: 10px;
    
    /* Box-sizing */
    box-sizing: border-box;
}
```

#### Propiedades del Box Model

**Width y Height**
```css
/* Dimensiones del contenido */
.square {
    width: 100px;
    height: 100px;
}

/* Dimensiones con unidades relativas */
.responsive {
    width: 50%;
    height: 50vh;
}

/* Dimensiones mínimas y máximas */
.constrained {
    min-width: 200px;
    max-width: 800px;
    min-height: 100px;
    max-height: 400px;
}
```

**Padding (Espaciado Interno)**
```css
/* Padding individual por lado */
.element {
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 15px;
    padding-left: 25px;
}

/* Padding con shorthand */
.padding-shorthand {
    padding: 10px;                    /* Todos los lados */
    padding: 10px 20px;               /* Vertical | Horizontal */
    padding: 10px 20px 15px;          /* Top | Horizontal | Bottom */
    padding: 10px 20px 15px 25px;     /* Top | Right | Bottom | Left */
}
```

**Border (Borde)**
```css
/* Bordes individuales */
.border-example {
    border-top: 2px solid red;
    border-right: 1px dashed blue;
    border-bottom: 3px dotted green;
    border-left: 1px double orange;
}

/* Bordes con shorthand */
.border-shorthand {
    border: 2px solid #333;           /* Ancho | Estilo | Color */
    border-radius: 8px;               /* Bordes redondeados */
    border-radius: 10px 20px 30px 40px; /* Top-left | Top-right | Bottom-right | Bottom-left */
}

/* Estilos de borde */
.border-styles {
    border-style: solid;      /* Línea sólida */
    border-style: dashed;     /* Línea punteada */
    border-style: dotted;     /* Línea de puntos */
    border-style: double;     /* Línea doble */
    border-style: groove;     /* Borde 3D hundido */
    border-style: ridge;      /* Borde 3D elevado */
    border-style: inset;      /* Borde 3D interno */
    border-style: outset;     /* Borde 3D externo */
}
```

**Margin (Espaciado Externo)**
```css
/* Margin individual por lado */
.element {
    margin-top: 10px;
    margin-right: 20px;
    margin-bottom: 15px;
    margin-left: 25px;
}

/* Margin con shorthand */
.margin-shorthand {
    margin: 10px;                     /* Todos los lados */
    margin: 10px 20px;                /* Vertical | Horizontal */
    margin: 10px 20px 15px;           /* Top | Horizontal | Bottom */
    margin: 10px 20px 15px 25px;      /* Top | Right | Bottom | Left */
}

/* Margin negativo */
.negative-margin {
    margin-top: -10px;                /* Mueve el elemento hacia arriba */
}
```

#### Box-Sizing
La propiedad `box-sizing` determina cómo se calculan las dimensiones:

```css
/* Box-sizing: content-box (por defecto) */
.content-box {
    box-sizing: content-box;
    width: 200px;                     /* Solo el contenido */
    padding: 20px;                    /* Se añade al ancho */
    border: 2px solid black;          /* Se añade al ancho */
    /* Ancho total: 200 + 40 + 4 = 244px */
}

/* Box-sizing: border-box */
.border-box {
    box-sizing: border-box;
    width: 200px;                     /* Incluye padding y border */
    padding: 20px;                    /* Incluido en el ancho */
    border: 2px solid black;          /* Incluido en el ancho */
    /* Ancho total: 200px */
}

/* Aplicar border-box globalmente */
* {
    box-sizing: border-box;
}
```

### 2.2 Propiedades Display

#### Tipos de Display Básicos

**Block (Bloque)**
```css
.block-element {
    display: block;
    /* Características:
       - Ocupa todo el ancho disponible
       - Comienza en una nueva línea
       - Respeta width, height, margin, padding */
}

/* Elementos block por defecto */
div, p, h1, h2, h3, h4, h5, h6, 
section, article, aside, header, footer {
    display: block;
}
```

**Inline (En Línea)**
```css
.inline-element {
    display: inline;
    /* Características:
       - Solo ocupa el espacio necesario
       - No comienza en nueva línea
       - No respeta width, height, margin-top, margin-bottom */
}

/* Elementos inline por defecto */
span, a, strong, em, i, b, small, 
label, input, button {
    display: inline;
}
```

**Inline-Block**
```css
.inline-block-element {
    display: inline-block;
    /* Características:
       - Se comporta como inline pero respeta width, height, margin */
}

/* Ejemplo práctico */
.nav-item {
    display: inline-block;
    width: 120px;
    height: 40px;
    margin: 5px;
    text-align: center;
    line-height: 40px;
}
```

#### Display Especiales

**None**
```css
.hidden {
    display: none;
    /* Características:
       - Elemento completamente oculto
       - No ocupa espacio en el layout
       - No es accesible para lectores de pantalla */
}

/* Alternativa: visibility */
.invisible {
    visibility: hidden;
    /* Características:
       - Elemento invisible pero ocupa espacio
       - Mantiene el layout intacto */
}
```

**Flex (Introducción Básica)**
```css
.flex-container {
    display: flex;
    /* Características:
       - Los hijos se comportan como flex items
       - Layout flexible y responsivo */
}

.flex-item {
    /* Los hijos heredan propiedades flex automáticamente */
}
```

### 2.3 Positioning (Posicionamiento)

#### Tipos de Posicionamiento

**Static (Por Defecto)**
```css
.static-element {
    position: static;
    /* Características:
       - Posición normal en el flujo del documento
       - No se puede mover con top, right, bottom, left
       - No crea un nuevo contexto de apilamiento */
}
```

**Relative (Relativo)**
```css
.relative-element {
    position: relative;
    top: 20px;           /* Mueve 20px hacia abajo desde su posición original */
    left: 30px;          /* Mueve 30px hacia la derecha desde su posición original */
    
    /* Características:
       - Se mueve desde su posición original
       - Mantiene su espacio en el flujo
       - Crea un nuevo contexto de apilamiento */
}

/* Ejemplo práctico */
.tooltip {
    position: relative;
    top: -10px;
    left: 50%;
    transform: translateX(-50%);
}
```

**Absolute (Absoluto)**
```css
.absolute-element {
    position: absolute;
    top: 0;
    right: 0;
    
    /* Características:
       - Se posiciona relativo al ancestro posicionado más cercano
       - Se remueve del flujo normal del documento
       - Si no hay ancestro posicionado, se posiciona relativo al viewport */
}

/* Ejemplo: Modal overlay */
.modal-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
}
```

**Fixed (Fijo)**
```css
.fixed-element {
    position: fixed;
    top: 20px;
    right: 20px;
    
    /* Características:
       - Se posiciona relativo al viewport
       - Se mantiene fijo durante el scroll
       - Se remueve del flujo normal */
}

/* Ejemplo: Botón flotante */
.floating-button {
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: #007bff;
    color: white;
    border: none;
    cursor: pointer;
}
```

**Sticky (Pegajoso)**
```css
.sticky-element {
    position: sticky;
    top: 0;
    
    /* Características:
       - Se comporta como relative hasta que alcanza el threshold
       - Luego se comporta como fixed
       - Requiere un ancestro con scroll */
}

/* Ejemplo: Header sticky */
.sticky-header {
    position: sticky;
    top: 0;
    background-color: white;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    z-index: 100;
}
```

#### Z-Index y Apilamiento
```css
/* Z-index controla el orden de apilamiento */
.lowest { z-index: 1; }
.middle { z-index: 10; }
.highest { z-index: 100; }

/* Solo funciona en elementos posicionados */
.positioned-element {
    position: relative; /* o absolute, fixed, sticky */
    z-index: 10;
}
```

### 2.4 Float y Clear

#### Float Básico
```css
/* Float left */
.float-left {
    float: left;
    margin-right: 20px;
}

/* Float right */
.float-right {
    float: right;
    margin-left: 20px;
}

/* Clear para evitar problemas de float */
.clearfix::after {
    content: "";
    display: table;
    clear: both;
}
```

#### Problemas Comunes del Float
```css
/* Problema: El contenedor no se expande */
.float-container {
    border: 2px solid red;
    /* Los hijos float no expanden el contenedor */
}

/* Solución 1: Clearfix */
.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

/* Solución 2: Overflow hidden */
.overflow-fix {
    overflow: hidden;
}

/* Solución 3: Display flow-root (moderno) */
.flow-root {
    display: flow-root;
}
```

### 2.5 Flexbox Básico

#### Conceptos Fundamentales

**Container (Contenedor)**
```css
.flex-container {
    display: flex;
    
    /* Dirección del eje principal */
    flex-direction: row;              /* Por defecto: horizontal */
    flex-direction: row-reverse;      /* Horizontal invertido */
    flex-direction: column;           /* Vertical */
    flex-direction: column-reverse;   /* Vertical invertido */
    
    /* Wrap de elementos */
    flex-wrap: nowrap;                /* Por defecto: no wrap */
    flex-wrap: wrap;                  /* Wrap a nueva línea */
    flex-wrap: wrap-reverse;          /* Wrap invertido */
    
    /* Shorthand */
    flex-flow: row wrap;              /* direction + wrap */
}
```

**Items (Elementos)**
```css
.flex-item {
    /* Crecimiento */
    flex-grow: 0;                     /* Por defecto: no crece */
    flex-grow: 1;                     /* Crece para llenar espacio disponible */
    
    /* Encogimiento */
    flex-shrink: 1;                   /* Por defecto: se encoge */
    flex-shrink: 0;                   /* No se encoge */
    
    /* Tamaño base */
    flex-basis: auto;                 /* Por defecto: tamaño del contenido */
    flex-basis: 200px;                /* Tamaño fijo */
    
    /* Shorthand */
    flex: 1;                          /* grow: 1, shrink: 1, basis: 0% */
    flex: 0 0 200px;                  /* grow: 0, shrink: 0, basis: 200px */
}
```

#### Alineación Básica

**Justify Content (Eje Principal)**
```css
.flex-container {
    justify-content: flex-start;      /* Por defecto: inicio */
    justify-content: flex-end;        /* Final */
    justify-content: center;          /* Centro */
    justify-content: space-between;   /* Espacio entre elementos */
    justify-content: space-around;    /* Espacio alrededor de elementos */
    justify-content: space-evenly;    /* Espacio uniforme */
}
```

**Align Items (Eje Secundario)**
```css
.flex-container {
    align-items: stretch;             /* Por defecto: estirar */
    align-items: flex-start;          /* Inicio */
    align-items: flex-end;            /* Final */
    align-items: center;              /* Centro */
    align-items: baseline;            /* Línea base del texto */
}
```

### 2.6 Overflow y Z-Index

#### Overflow
```css
/* Overflow visible (por defecto) */
.overflow-visible {
    overflow: visible;
    /* El contenido se desborda */
}

/* Overflow hidden */
.overflow-hidden {
    overflow: hidden;
    /* El contenido se corta */
}

/* Overflow scroll */
.overflow-scroll {
    overflow: scroll;
    /* Siempre muestra barras de scroll */
}

/* Overflow auto */
.overflow-auto {
    overflow: auto;
    /* Muestra barras solo cuando es necesario */
}

/* Overflow específico por eje */
.overflow-x-hidden {
    overflow-x: hidden;               /* Solo horizontal */
    overflow-y: auto;                 /* Solo vertical */
}
```

#### Z-Index Avanzado
```css
/* Contextos de apilamiento */
.stacking-context-1 {
    position: relative;
    z-index: 1;
}

.stacking-context-2 {
    position: relative;
    z-index: 2;
}

/* Elementos dentro de contextos */
.child-1 {
    position: absolute;
    z-index: 10;                      /* Solo afecta a su contexto padre */
}

.child-2 {
    position: absolute;
    z-index: 100;                     /* Solo afecta a su contexto padre */
}
```

## 🧪 Ejercicios Prácticos

### **Ejercicio 1: Box Model Visual**
Crea una página que demuestre visualmente el Box Model con diferentes configuraciones.

**Requisitos:**
- Muestra elementos con diferentes padding, border y margin
- Usa colores diferentes para cada parte del box
- Compara content-box vs border-box

### **Ejercicio 2: Layout con Display**
Crea un layout usando diferentes tipos de display (block, inline, inline-block).

**Requisitos:**
- Header con navegación horizontal
- Sidebar y contenido principal
- Footer con múltiples columnas
- Usa solo propiedades display básicas

### **Ejercicio 3: Sistema de Posicionamiento**
Implementa diferentes tipos de posicionamiento en una página.

**Requisitos:**
- Header sticky
- Botón flotante fijo
- Tooltips posicionados absolutamente
- Elementos relativos para ajustes finos

### **Ejercicio 4: Layout con Float**
Crea un layout tradicional usando float y clear.

**Requisitos:**
- Galería de imágenes con float
- Sidebar flotante
- Soluciona problemas de clearfix
- Layout responsivo básico

### **Ejercicio 5: Flexbox Básico**
Construye un layout usando Flexbox fundamental.

**Requisitos:**
- Navegación horizontal centrada
- Cards en fila con flex
- Footer con elementos distribuidos
- Responsive con flex-wrap

### **Ejercicio 6: Sistema de Grid Simple**
Crea un sistema de grid básico usando Flexbox.

**Requisitos:**
- Grid de 12 columnas
- Diferentes tamaños de columna
- Responsive breakpoints
- Gutter entre columnas

### **Ejercicio 7: Componentes con Box Model**
Desarrolla componentes reutilizables usando el Box Model.

**Requisitos:**
- Botones con diferentes tamaños
- Cards con padding y margin consistentes
- Inputs con estados visuales
- Sistema de espaciado uniforme

### **Ejercicio 8: Layout de Blog**
Implementa un layout de blog completo.

**Requisitos:**
- Header con navegación
- Sidebar con widgets
- Contenido principal con artículos
- Footer con información
- Usa diferentes técnicas de layout

### **Ejercicio 9: Galería de Imágenes**
Crea una galería de imágenes responsiva.

**Requisitos:**
- Grid de imágenes con flexbox
- Hover effects
- Lightbox básico
- Responsive breakpoints

### **Ejercicio 10: Dashboard Básico**
Construye un dashboard administrativo simple.

**Requisitos:**
- Header sticky
- Sidebar de navegación
- Área de contenido principal
- Widgets organizados en grid
- Responsive design

## 🎯 Proyecto Integrador: Layout de Blog con Sidebar

### Descripción del Proyecto
Crea un blog completo con layout de dos columnas que demuestre todos los conceptos de layout aprendidos en este módulo.

### Requisitos del Proyecto

#### **Estructura HTML (25%)**
- Header con navegación principal
- Sidebar con widgets (búsqueda, categorías, posts recientes)
- Área de contenido principal con artículos
- Footer con información adicional

#### **Layout CSS (40%)**
- Uso apropiado del Box Model
- Diferentes tipos de display
- Posicionamiento para elementos específicos
- Float o Flexbox para el layout principal
- Manejo correcto de overflow

#### **Responsive Design (20%)**
- Layout que se adapta a móvil y desktop
- Sidebar que se colapsa en móvil
- Navegación adaptativa
- Imágenes responsivas

#### **Componentes (15%)**
- Sistema de botones consistente
- Cards de artículos bien estructuradas
- Formularios estilizados
- Navegación funcional

### Entregables
1. **Archivo HTML** (`index.html`)
2. **Archivo CSS** (`styles.css`)
3. **Página de artículo individual** (`article.html`)
4. **README** explicando las decisiones de layout
5. **Capturas de pantalla** en diferentes dispositivos

### Criterios de Evaluación
- **Layout**: Estructura sólida y bien organizada
- **Box Model**: Uso correcto de padding, margin y border
- **Posicionamiento**: Implementación apropiada de diferentes tipos
- **Responsive**: Funciona bien en todos los dispositivos
- **Código**: CSS limpio y bien estructurado

## 📚 Recursos Adicionales

### Documentación
- [MDN Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model)
- [MDN Position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
- [MDN Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)

### Herramientas
- [CSS Box Model Visualizer](https://www.w3schools.com/css/css_boxmodel.asp)
- [Flexbox Playground](https://codepen.io/enxaneta/full/adLPwv/)
- [CSS Position Visualizer](https://www.w3schools.com/css/css_positioning.asp)

### Práctica
- [Flexbox Froggy](https://flexboxfroggy.com/) - Aprende Flexbox jugando
- [CSS Grid Garden](https://cssgridgarden.com/) - Aprende CSS Grid jugando
- [CSS Diner](https://flukeout.github.io/) - Juego de selectores CSS

## 🔍 Preguntas de Repaso

1. **¿Qué es el Box Model y cuáles son sus componentes principales?**
2. **¿Cuál es la diferencia entre content-box y border-box?**
3. **¿Cómo funciona el posicionamiento absolute vs relative?**
4. **¿Qué problemas causa el float y cómo se solucionan?**
5. **¿Cuáles son las propiedades principales de Flexbox?**
6. **¿Cómo se controla el orden de apilamiento con z-index?**
7. **¿Qué tipos de overflow existen y cuándo usar cada uno?**
8. **¿Cómo se crea un contexto de apilamiento?**
9. **¿Cuál es la diferencia entre display: none y visibility: hidden?**
10. **¿Cómo se implementa un layout responsive con Flexbox?**

## 🚀 Siguiente Paso

Una vez que hayas completado este módulo y el proyecto integrador, estarás listo para continuar con el **Módulo 3: Responsive Design**, donde aprenderás sobre media queries, mobile-first approach y técnicas de diseño responsivo.

---

**¡Excelente trabajo! Ahora entiendes cómo controlar el layout y posicionamiento de elementos en CSS.** 🎉

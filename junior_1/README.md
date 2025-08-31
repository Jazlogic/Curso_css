# 🎨 Módulo 1: Fundamentos de CSS

## 📚 Descripción del Módulo

Este módulo te introduce a los fundamentos esenciales de CSS (Cascading Style Sheets). Aprenderás qué es CSS, cómo funciona, y los conceptos básicos que forman la base de todo el diseño web moderno. Desde selectores simples hasta la comprensión de la cascada y herencia, este módulo establece las bases sólidas para tu viaje en CSS.

## 🎯 Objetivos de Aprendizaje

Al completar este módulo, serás capaz de:

- ✅ Comprender qué es CSS y su evolución histórica
- ✅ Utilizar selectores básicos y avanzados efectivamente
- ✅ Aplicar estilos de texto y tipografía
- ✅ Trabajar con colores y fondos
- ✅ Entender la cascada, especificidad e herencia
- ✅ Usar unidades de medida apropiadas
- ✅ Implementar pseudo-clases y pseudo-elementos básicos

## 📖 Contenido del Módulo

### 1.1 Introducción a CSS y su Evolución

#### ¿Qué es CSS?
CSS (Cascading Style Sheets) es un lenguaje de hojas de estilo utilizado para describir la presentación de documentos HTML. CSS describe cómo deben mostrarse los elementos HTML en pantalla, en papel, en el habla o en otros medios.

#### Evolución de CSS
- **CSS1 (1996)**: Primera especificación con estilos básicos
- **CSS2 (1998)**: Posicionamiento y media types
- **CSS3 (2001-presente)**: Módulos independientes (Grid, Flexbox, Animaciones)
- **CSS4**: En desarrollo con nuevas características

#### ¿Por qué CSS?
```css
/* Sin CSS - HTML básico */
<h1 style="color: blue; font-size: 24px; text-align: center;">Título</h1>

/* Con CSS - Separación de responsabilidades */
h1 {
    color: blue;
    font-size: 24px;
    text-align: center;
}
```

### 1.2 Selectores Básicos y Avanzados

#### Selectores de Tipo
```css
/* Selector de elemento */
p {
    color: #333;
}

/* Selector de clase */
.highlight {
    background-color: yellow;
}

/* Selector de ID */
#header {
    background-color: #f0f0f0;
}
```

#### Selectores de Atributos
```css
/* Elementos con atributo específico */
input[type="text"] {
    border: 1px solid #ccc;
}

/* Elementos que contienen texto en atributo */
a[href*="google"] {
    color: blue;
}

/* Elementos que empiezan con texto */
a[href^="https"] {
    color: green;
}
```

#### Selectores Combinados
```css
/* Descendiente */
div p {
    margin: 10px 0;
}

/* Hijo directo */
div > p {
    padding: 5px;
}

/* Hermano adyacente */
h1 + p {
    font-size: 18px;
}

/* Hermano general */
h1 ~ p {
    line-height: 1.6;
}
```

#### Selectores de Pseudo-clases
```css
/* Estados de enlaces */
a:link { color: blue; }
a:visited { color: purple; }
a:hover { color: red; }
a:active { color: orange; }

/* Estados de formularios */
input:focus {
    outline: 2px solid blue;
}

input:disabled {
    background-color: #f0f0f0;
}

/* Selectores de posición */
li:first-child { font-weight: bold; }
li:last-child { border-bottom: none; }
li:nth-child(odd) { background-color: #f9f9f9; }
```

### 1.3 Propiedades de Texto y Tipografía

#### Propiedades de Fuente
```css
/* Familia de fuente */
body {
    font-family: 'Arial', 'Helvetica', sans-serif;
}

/* Tamaño de fuente */
h1 { font-size: 2.5rem; }
h2 { font-size: 2rem; }
p { font-size: 1rem; }

/* Peso de fuente */
.light { font-weight: 300; }
.normal { font-weight: 400; }
.bold { font-weight: 700; }
.extra-bold { font-weight: 900; }

/* Estilo de fuente */
.italic { font-style: italic; }
.oblique { font-style: oblique; }
```

#### Propiedades de Texto
```css
/* Alineación de texto */
.text-left { text-align: left; }
.text-center { text-align: center; }
.text-right { text-align: right; }
.text-justify { text-align: justify; }

/* Decoración de texto */
.underline { text-decoration: underline; }
.line-through { text-decoration: line-through; }
.no-decoration { text-decoration: none; }

/* Transformación de texto */
.uppercase { text-transform: uppercase; }
.lowercase { text-transform: lowercase; }
.capitalize { text-transform: capitalize; }

/* Espaciado de letras y palabras */
.letter-spacing { letter-spacing: 2px; }
.word-spacing { word-spacing: 5px; }
```

#### Propiedades de Línea
```css
/* Altura de línea */
.single-line { line-height: 1; }
.double-line { line-height: 2; }
.comfortable { line-height: 1.6; }

/* Indentación */
.indented { text-indent: 2em; }

/* Espaciado vertical */
.paragraph {
    margin-top: 1em;
    margin-bottom: 1em;
}
```

### 1.4 Colores y Fondos

#### Colores en CSS
```css
/* Nombres de colores */
.red { color: red; }
.blue { color: blue; }
.green { color: green; }

/* Valores hexadecimales */
.primary { color: #007bff; }
.secondary { color: #6c757d; }
.success { color: #28a745; }

/* Valores RGB */
.rgb-color { color: rgb(255, 0, 0); }
.rgba-color { color: rgba(255, 0, 0, 0.5); }

/* Valores HSL */
.hsl-color { color: hsl(0, 100%, 50%); }
.hsla-color { color: hsla(0, 100%, 50%, 0.5); }
```

#### Propiedades de Fondo
```css
/* Color de fondo */
.bg-primary { background-color: #007bff; }
.bg-secondary { background-color: #6c757d; }

/* Imagen de fondo */
.bg-image {
    background-image: url('image.jpg');
    background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
}

/* Fondo con gradiente */
.gradient-bg {
    background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
}

.radial-gradient {
    background: radial-gradient(circle, #ff6b6b, #4ecdc4);
}
```

#### Propiedades de Fondo Avanzadas
```css
/* Múltiples fondos */
.layered-bg {
    background-image: 
        url('overlay.png'),
        url('background.jpg');
    background-size: 
        contain,
        cover;
    background-position: 
        center,
        center;
}

/* Fondo con attachment */
.parallax-bg {
    background-image: url('parallax.jpg');
    background-attachment: fixed;
    background-size: cover;
}
```

### 1.5 Cascada, Especificidad e Herencia

#### Cascada CSS
La cascada determina qué reglas CSS se aplican cuando hay conflictos. El orden de importancia es:

1. **!important** (mayor prioridad)
2. **Estilos inline**
3. **Especificidad del selector**
4. **Orden en el archivo CSS**

```css
/* Ejemplo de cascada */
p { color: blue; }        /* Regla 1 */
p { color: red; }         /* Regla 2 - sobrescribe la 1 */
p { color: green !important; } /* Regla 3 - mayor prioridad */
```

#### Especificidad
La especificidad determina qué selector tiene mayor peso:

```css
/* Orden de especificidad (de menor a mayor) */
* { }                     /* 0,0,0,0 */
p { }                     /* 0,0,0,1 */
.class { }                /* 0,0,1,0 */
#id { }                   /* 0,1,0,0 */
style="color: red"        /* 1,0,0,0 */
!important                /* Mayor prioridad */
```

#### Herencia
Algunas propiedades se heredan automáticamente:

```css
/* Propiedades que se heredan */
body {
    font-family: Arial, sans-serif;
    color: #333;
    line-height: 1.6;
}

/* Todos los elementos hijos heredan estas propiedades */
h1, p, div, span {
    /* Heredan font-family, color, line-height */
}

/* Propiedades que NO se heredan */
body {
    border: 1px solid black;    /* No se hereda */
    margin: 20px;               /* No se hereda */
    padding: 10px;              /* No se hereda */
}
```

### 1.6 Unidades de Medida

#### Unidades Absolutas
```css
/* Píxeles - unidad más común */
.pixel { font-size: 16px; }

/* Puntos - para impresión */
.print { font-size: 12pt; }

/* Pulgadas y centímetros */
.inches { margin: 0.5in; }
.centimeters { padding: 1cm; }
```

#### Unidades Relativas
```css
/* Em - relativo al tamaño de fuente del elemento padre */
.parent { font-size: 16px; }
.child { font-size: 1.5em; } /* 24px */

/* Rem - relativo al tamaño de fuente del elemento raíz (html) */
html { font-size: 16px; }
.element { font-size: 1.5rem; } /* 24px */

/* Porcentaje - relativo al elemento padre */
.container { width: 100%; }
.half { width: 50%; }

/* Viewport units */
.full-height { height: 100vh; }
.full-width { width: 100vw; }
```

#### Unidades Modernas
```css
/* Container queries (CSS moderno) */
@container (min-width: 400px) {
    .card {
        grid-template-columns: 1fr 1fr;
    }
}

/* Aspect ratio */
.video {
    aspect-ratio: 16 / 9;
}

/* Clamp - tamaño responsivo */
.responsive-text {
    font-size: clamp(1rem, 4vw, 2rem);
}
```

### 1.7 Pseudo-clases y Pseudo-elementos Básicos

#### Pseudo-clases de Estado
```css
/* Estados de formularios */
input:required { border-color: red; }
input:optional { border-color: green; }
input:valid { border-color: blue; }
input:invalid { border-color: red; }

/* Estados de elementos */
.element:empty { display: none; }
.element:target { background-color: yellow; }

/* Estados de navegación */
:root { /* Elemento raíz */ }
:host { /* En Shadow DOM */ }
```

#### Pseudo-elementos
```css
/* ::before y ::after */
.quote::before {
    content: '"';
    font-size: 2em;
    color: #ccc;
}

.quote::after {
    content: '"';
    font-size: 2em;
    color: #ccc;
}

/* ::first-line y ::first-letter */
p::first-line {
    font-weight: bold;
    color: #333;
}

p::first-letter {
    font-size: 3em;
    float: left;
    margin-right: 0.1em;
}

/* ::selection */
::selection {
    background-color: yellow;
    color: black;
}
```

## 🧪 Ejercicios Prácticos

### **Ejercicio 1: Selectores Básicos**
Crea un archivo HTML con diferentes elementos y aplica estilos usando selectores de tipo, clase e ID.

**Requisitos:**
- Usa al menos 5 selectores diferentes
- Aplica colores, fuentes y espaciado
- Demuestra la diferencia entre selectores

### **Ejercicio 2: Tipografía Responsiva**
Crea un sistema de tipografía que se adapte a diferentes tamaños de pantalla.

**Requisitos:**
- Usa unidades rem y em
- Implementa una escala tipográfica
- Aplica diferentes tamaños para móvil y desktop

### **Ejercicio 3: Paleta de Colores**
Desarrolla una paleta de colores coherente usando diferentes formatos de color.

**Requisitos:**
- Define colores primarios, secundarios y acentos
- Usa hexadecimal, RGB y HSL
- Crea variaciones de opacidad

### **Ejercicio 4: Sistema de Espaciado**
Implementa un sistema de espaciado consistente usando variables CSS.

**Requisitos:**
- Define variables para márgenes y padding
- Usa diferentes unidades de medida
- Aplica el sistema a varios elementos

### **Ejercicio 5: Estados de Elementos**
Crea elementos interactivos con diferentes estados visuales.

**Requisitos:**
- Implementa estados hover, focus y active
- Usa pseudo-clases apropiadas
- Crea transiciones suaves

### **Ejercicio 6: Layout Básico con CSS**
Construye un layout simple usando solo propiedades básicas de CSS.

**Requisitos:**
- Crea un header, main y footer
- Usa diferentes tipos de display
- Implementa espaciado consistente

### **Ejercicio 7: Sistema de Botones**
Desarrolla un sistema de botones con diferentes variantes.

**Requisitos:**
- Crea botones primarios, secundarios y de texto
- Usa pseudo-clases para estados
- Implementa diferentes tamaños

### **Ejercicio 8: Tarjetas de Contenido**
Diseña tarjetas de contenido con diferentes estilos.

**Requisitos:**
- Usa sombras y bordes
- Implementa diferentes variantes de color
- Aplica espaciado consistente

### **Ejercicio 9: Navegación Básica**
Crea una navegación horizontal con estilos apropiados.

**Requisitos:**
- Usa display flexbox básico
- Implementa estados hover
- Aplica espaciado uniforme

### **Ejercicio 10: Formulario Estilizado**
Diseña un formulario con estilos modernos y accesibles.

**Requisitos:**
- Usa diferentes tipos de input
- Implementa estados de validación
- Aplica estilos consistentes

## 🎯 Proyecto Integrador: Página Web Personal

### Descripción del Proyecto
Crea una página web personal completa que demuestre todos los conceptos aprendidos en este módulo.

### Requisitos del Proyecto

#### **Estructura HTML (20%)**
- Header con navegación
- Sección de presentación personal
- Sección de habilidades
- Sección de proyectos
- Footer con información de contacto

#### **Estilos CSS (40%)**
- Uso de selectores apropiados
- Sistema de colores coherente
- Tipografía bien estructurada
- Espaciado consistente
- Estados interactivos

#### **Responsive Design (20%)**
- Adaptación a diferentes tamaños de pantalla
- Uso apropiado de unidades relativas
- Media queries básicas

#### **Código Limpio (20%)**
- CSS bien organizado y comentado
- Uso de variables CSS
- Nomenclatura consistente
- Estructura lógica

### Entregables
1. **Archivo HTML** (`index.html`)
2. **Archivo CSS** (`styles.css`)
3. **README** explicando las decisiones de diseño
4. **Capturas de pantalla** en diferentes dispositivos

### Criterios de Evaluación
- **Funcionalidad**: La página se ve correctamente en diferentes navegadores
- **Diseño**: Estética atractiva y profesional
- **Código**: CSS limpio, organizado y bien estructurado
- **Responsive**: Funciona bien en móvil y desktop
- **Accesibilidad**: Uso apropiado de colores y contraste

## 📚 Recursos Adicionales

### Documentación
- [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [CSS Values and Units](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Values_and_Units)

### Herramientas
- [CSS Validator](https://jigsaw.w3.org/css-validator/)
- [Color Picker](https://htmlcolorcodes.com/)
- [CSS Grid Generator](https://cssgrid-generator.netlify.app/)

### Práctica
- [CSS Diner](https://flukeout.github.io/) - Juego de selectores CSS
- [Flexbox Froggy](https://flexboxfroggy.com/) - Aprende Flexbox jugando
- [Grid Garden](https://cssgridgarden.com/) - Aprende CSS Grid jugando

## 🔍 Preguntas de Repaso

1. **¿Qué significa CSS y cuál es su propósito principal?**
2. **¿Cuál es la diferencia entre un selector de clase y un selector de ID?**
3. **¿Cómo funciona la cascada en CSS?**
4. **¿Qué propiedades CSS se heredan automáticamente?**
5. **¿Cuál es la diferencia entre em y rem?**
6. **¿Cómo se calcula la especificidad de un selector?**
7. **¿Qué son las pseudo-clases y pseudo-elementos?**
8. **¿Cuáles son las ventajas de usar variables CSS?**
9. **¿Cómo se aplican colores en CSS?**
10. **¿Qué es el box model en CSS?**

## 🚀 Siguiente Paso

Una vez que hayas completado este módulo y el proyecto integrador, estarás listo para continuar con el **Módulo 2: Layout y Box Model**, donde aprenderás sobre el modelo de caja, posicionamiento y Flexbox básico.

---

**¡Felicitaciones por completar el primer módulo! Has establecido una base sólida en CSS.** 🎉

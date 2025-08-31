# 🎨 Módulo 6: CSS Moderno y Avanzado

## 📚 Descripción del Módulo

En este módulo explorarás las características más modernas y avanzadas de CSS. Aprenderás sobre variables CSS (Custom Properties), funciones matemáticas, pseudo-elementos avanzados, CSS Houdini y técnicas que están definiendo el futuro del diseño web. Este conocimiento te pondrá a la vanguardia del desarrollo CSS.

## 🎯 Objetivos de Aprendizaje

Al completar este módulo, serás capaz de:

- ✅ Implementar variables CSS para sistemas de diseño dinámicos
- ✅ Usar funciones CSS modernas como calc(), min(), max(), clamp()
- ✅ Crear pseudo-elementos avanzados y selectores complejos
- ✅ Entender CSS Houdini y sus capacidades futuras
- ✅ Implementar CSS Containment para optimización
- ✅ Usar aspect-ratio y container queries para layouts modernos

## 📖 Contenido del Módulo

### 6.1 Variables CSS (Custom Properties) - El Poder de la Reutilización

#### ¿Qué son las Variables CSS?

Las variables CSS (Custom Properties) te permiten definir valores reutilizables en tu CSS. Es como crear tu propio sistema de constantes que puedes usar en todo tu código, facilitando el mantenimiento y la consistencia.

#### Sintaxis Básica de Variables CSS

```css
/* Paso 1: Definir variables en :root (scope global) */
:root {
    --primary-color: #007bff;
    --secondary-color: #6c757d;
    --font-size-base: 16px;
    --spacing-unit: 8px;
    --border-radius: 4px;
    /* 
    Explicación paso a paso:
    1. :root = selector para el elemento raíz (html)
    2. --nombre-variable = sintaxis para definir variables CSS
    3. valor = el valor que se almacenará en la variable
    4. Estas variables están disponibles en todo el documento
    */
}

/* Paso 2: Usar las variables */
.button {
    background-color: var(--primary-color);
    font-size: var(--font-size-base);
    padding: calc(var(--spacing-unit) * 2);
    border-radius: var(--border-radius);
    /* 
    Explicación:
    - var(--nombre-variable) = obtiene el valor de la variable
    - calc() = permite hacer cálculos matemáticos
    - var(--spacing-unit) * 2 = duplica el valor de spacing
    */
}
```

#### Variables CSS con Fallbacks

```css
.element {
    /* Variable con valor de respaldo */
    color: var(--text-color, #333);
    /* 
    Explicación:
    - Si --text-color no está definida, usa #333
    - Los fallbacks son importantes para compatibilidad
    */
    
    /* Múltiples fallbacks */
    background-color: var(--bg-color, var(--fallback-bg, white));
    /* 
    Explicación:
    - Primero intenta usar --bg-color
    - Si no existe, usa --fallback-bg
    - Si ninguna existe, usa white
    */
}
```

#### Variables CSS en Diferentes Scopes

```css
/* Variables globales */
:root {
    --global-spacing: 20px;
    --global-radius: 8px;
}

/* Variables específicas del componente */
.card {
    --card-padding: 16px;
    --card-shadow: 0 2px 8px rgba(0,0,0,0.1);
    
    padding: var(--card-padding);
    box-shadow: var(--card-shadow);
    border-radius: var(--global-radius);
    /* 
    Explicación:
    - --card-padding solo está disponible dentro de .card
    - --global-radius está disponible en todo el documento
    - Las variables locales pueden sobrescribir las globales
    */
}

/* Variables que cambian según el estado */
.button {
    --button-bg: var(--primary-color);
    --button-text: white;
    
    background-color: var(--button-bg);
    color: var(--button-text);
}

.button:hover {
    --button-bg: var(--primary-dark);
    /* 
    Explicación:
    - Al hacer hover, la variable cambia
    - El botón se re-renderiza automáticamente
    - No necesitas redefinir background-color
    */
}
```

### 6.2 Funciones CSS Modernas - Matemáticas en CSS

#### calc() - Calculadora CSS

La función `calc()` te permite hacer cálculos matemáticos directamente en CSS, combinando diferentes unidades.

```css
.element {
    /* Cálculos básicos */
    width: calc(100% - 40px);        /* Ancho total menos 40px */
    height: calc(100vh - 80px);      /* Altura del viewport menos 80px */
    margin: calc(20px + 2rem);       /* 20px más 2rem */
    
    /* Cálculos complejos */
    padding: calc(var(--spacing) * 2 + 10px);
    /* 
    Explicación paso a paso:
    1. var(--spacing) = obtiene el valor de la variable
    2. * 2 = multiplica por 2
    3. + 10px = suma 10px al resultado
    4. El resultado se convierte en padding
    */
}

/* Ejemplo práctico - Layout con sidebar */
.layout {
    display: grid;
    grid-template-columns: 250px calc(100% - 250px);
    /* 
    Explicación:
    - Primera columna: 250px (sidebar fija)
    - Segunda columna: 100% - 250px (contenido que se adapta)
    - Resultado: layout que siempre usa todo el ancho disponible
    */
}
```

#### min(), max() y clamp() - Valores Responsivos

Estas funciones te permiten establecer valores que se adaptan automáticamente según el contexto.

**min() - El valor más pequeño:**
```css
.element {
    width: min(300px, 50%);
    /* 
    Explicación:
    - Si 300px es menor que 50%, usa 300px
    - Si 50% es menor que 300px, usa 50%
    - Resultado: el elemento nunca será más ancho que 300px
    */
    
    font-size: min(4vw, 24px);
    /* 
    Explicación:
    - En pantallas pequeñas: usa 4vw (responsive)
    - En pantallas grandes: usa 24px (máximo legible)
    - Resultado: texto que se adapta pero no es demasiado grande
    */
}
```

**max() - El valor más grande:**
```css
.element {
    width: max(200px, 30%);
    /* 
    Explicación:
    - Si 200px es mayor que 30%, usa 200px
    - Si 30% es mayor que 200px, usa 30%
    - Resultado: el elemento nunca será más estrecho que 200px
    */
    
    padding: max(20px, 5%);
    /* 
    Explicación:
    - Padding mínimo de 20px
    - En pantallas grandes puede ser 5%
    - Resultado: espaciado que nunca es muy pequeño
    */
}
```

**clamp() - Rango con mínimo, preferido y máximo:**
```css
.element {
    font-size: clamp(16px, 4vw, 32px);
    /* 
    Explicación paso a paso:
    1. 16px = tamaño mínimo (nunca más pequeño)
    2. 4vw = tamaño preferido (responsive)
    3. 32px = tamaño máximo (nunca más grande)
    4. Resultado: texto que se adapta pero está dentro de límites seguros
    */
    
    width: clamp(300px, 50%, 800px);
    /* 
    Explicación:
    - Mínimo: 300px (nunca muy estrecho)
    - Preferido: 50% (responsive)
    - Máximo: 800px (nunca muy ancho)
    - Resultado: ancho que se adapta pero mantiene proporciones
    */
}
```

### 6.3 Pseudo-elementos Avanzados - Más Allá de ::before y ::after

#### Pseudo-elementos de Selección y Contenido

**::selection - Estilo del texto seleccionado:**
```css
::selection {
    background-color: #ffeb3b;
    color: #000;
    text-shadow: none;
    /* 
    Explicación:
    - ::selection afecta todo el texto seleccionado
    - Solo funciona con color, background-color y text-shadow
    - Útil para mejorar la legibilidad del texto seleccionado
    */
}

/* Selección específica en elementos */
.code-block::selection {
    background-color: #e3f2fd;
    color: #1565c0;
    /* 
    Explicación:
    - Solo afecta al texto seleccionado dentro de .code-block
    - Permite diferentes estilos para diferentes tipos de contenido
    */
}
```

**::placeholder - Estilo de placeholders:**
```css
.input-field::placeholder {
    color: #999;
    font-style: italic;
    opacity: 0.8;
    /* 
    Explicación:
    - ::placeholder estiliza el texto de placeholder
    - Solo funciona con propiedades de texto y color
    - Útil para hacer formularios más atractivos
    */
}

/* Placeholder con transición */
.input-field::placeholder {
    transition: opacity 0.3s ease;
}

.input-field:focus::placeholder {
    opacity: 0.5;
    /* 
    Explicación:
    - Al hacer focus, el placeholder se desvanece
    - Transición suave para mejor UX
    */
}
```

#### Pseudo-elementos de Lista y Contenido

**::marker - Estilo de marcadores de lista:**
```css
.list-item::marker {
    color: var(--primary-color);
    font-weight: bold;
    font-size: 1.2em;
    /* 
    Explicación:
    - ::marker estiliza los bullets de las listas
    - Solo funciona con propiedades de texto y color
    - Útil para personalizar listas
    */
}

/* Marcadores personalizados */
.custom-list {
    list-style: none;
}

.custom-list li::before {
    content: "→";
    color: var(--accent-color);
    margin-right: 8px;
    font-weight: bold;
    /* 
    Explicación:
    - ::before crea contenido antes de cada elemento
    - content: "→" = inserta una flecha
    - Resultado: lista con flechas personalizadas
    */
}
```

**::first-letter y ::first-line - Estilo de texto específico:**
```css
.article::first-letter {
    font-size: 3.5em;
    float: left;
    line-height: 1;
    margin-right: 0.1em;
    color: var(--primary-color);
    font-family: serif;
    /* 
    Explicación:
    - ::first-letter estiliza solo la primera letra
    - float: left = la letra flota a la izquierda
    - Resultado: efecto de letra capital (drop cap)
    */
}

.article::first-line {
    font-weight: bold;
    color: var(--text-dark);
    text-transform: uppercase;
    letter-spacing: 0.05em;
    /* 
    Explicación:
    - ::first-line estiliza solo la primera línea
    - Útil para destacar el inicio de párrafos
    - Se adapta automáticamente al ancho del contenedor
    */
}
```

### 6.4 Selectores de Atributos Avanzados - Poder de Selección

#### Selectores de Atributos Básicos

```css
/* Elementos con atributo específico */
input[type="text"] {
    border: 2px solid var(--primary-color);
    /* Solo inputs de tipo texto */
}

/* Elementos que contienen texto en atributo */
a[href*="google"] {
    color: #4285f4;
    /* Enlaces que contengan "google" en la URL */
}

/* Elementos que empiezan con texto */
a[href^="https"] {
    color: #28a745;
    /* Enlaces que empiecen con "https" */
}

/* Elementos que terminan con texto */
img[src$=".jpg"] {
    border: 3px solid #ffc107;
    /* Imágenes que terminen en ".jpg" */
}
```

#### Selectores de Atributos Avanzados

```css
/* Elementos con múltiples condiciones */
input[type="text"][required] {
    border-color: var(--error-color);
    /* Inputs de texto que sean requeridos */
}

/* Elementos con atributo que contiene palabra específica */
a[class*="btn"] {
    display: inline-block;
    padding: 10px 20px;
    /* Enlaces que contengan "btn" en su clase */
}

/* Elementos con atributo que no contiene texto */
div:not([class*="hidden"]) {
    display: block;
    /* Divs que NO contengan "hidden" en su clase */
}

/* Selectores con valores que empiezan con guión */
[class^="icon-"] {
    font-family: "FontAwesome";
    /* Elementos con clase que empiece con "icon-" */
}
```

### 6.5 CSS Houdini - El Futuro de CSS

#### ¿Qué es CSS Houdini?

CSS Houdini es un conjunto de APIs que te permite extender CSS con JavaScript, creando propiedades y valores personalizados. Es como tener superpoderes para CSS.

#### Custom Properties y Values API

```javascript
// Registrar una propiedad personalizada
CSS.registerProperty({
    name: '--my-color',
    syntax: '<color>',
    inherits: false,
    initialValue: 'black'
});

// Usar la propiedad en CSS
.element {
    --my-color: red;
    background-color: var(--my-color);
}
```

#### Paint Worklet - Crear Funciones de Pintura Personalizadas

```javascript
// paint-worklet.js
class MyPaintWorklet {
    paint(ctx, size, properties) {
        // ctx = contexto de canvas
        // size = tamaño del elemento
        // properties = propiedades CSS
        
        const color = properties.get('--accent-color');
        ctx.fillStyle = color;
        ctx.fillRect(0, 0, size.width, size.height);
    }
}

registerPaint('my-paint', MyPaintWorklet);
```

```css
/* Usar el paint worklet */
.element {
    background: paint(my-paint);
    --accent-color: #ff6b6b;
}
```

### 6.6 CSS Containment - Optimización de Rendimiento

#### ¿Qué es CSS Containment?

CSS Containment permite que el navegador optimice el renderizado aislando partes del DOM. Es como decirle al navegador: "Esta sección es independiente, optimízala por separado".

#### Tipos de Containment

```css
/* Layout containment - aísla el layout */
.layout-section {
    contain: layout;
    /* 
    Explicación:
    - Los cambios en este elemento no afectan el layout de otros
    - El navegador puede optimizar el renderizado
    - Útil para secciones que cambian frecuentemente
    */
}

/* Style containment - aísla los estilos */
.widget {
    contain: style;
    /* 
    Explicación:
    - Los estilos de este elemento no se propagan
    - Mejora la especificidad y evita conflictos
    - Útil para componentes reutilizables
    */
}

/* Paint containment - aísla el pintado */
.animated-element {
    contain: paint;
    /* 
    Explicación:
    - Los cambios no requieren repintar elementos externos
    - Mejora el rendimiento de animaciones
    - Útil para elementos que se animan frecuentemente
    */
}

/* Containment completo */
.isolated-component {
    contain: strict;
    /* 
    Explicación:
    - strict = layout + style + paint
    - Máxima optimización y aislamiento
    - Útil para componentes completamente independientes
    */
}
```

### 6.7 Aspect-Ratio y Container Queries

#### Aspect-Ratio - Control de Proporciones

```css
/* Aspect-ratio básico */
.video-container {
    aspect-ratio: 16 / 9;
    /* 
    Explicación:
    - Mantiene proporción 16:9 (formato de video)
    - Se adapta automáticamente al ancho
    - No necesitas calcular height manualmente
    */
}

/* Aspect-ratio con diferentes valores */
.square {
    aspect-ratio: 1 / 1;  /* Cuadrado perfecto */
}

.portrait {
    aspect-ratio: 3 / 4;  /* Formato retrato */
}

.landscape {
    aspect-ratio: 4 / 3;  /* Formato paisaje */
}

/* Aspect-ratio responsivo */
.responsive-image {
    width: 100%;
    aspect-ratio: var(--image-ratio, 16 / 9);
    /* 
    Explicación:
    - Usa variable CSS para ratio configurable
    - Fallback a 16:9 si no se define la variable
    - Útil para galerías con diferentes proporciones
    */
}
```

#### Container Queries - Responsive Basado en el Contenedor

```css
/* Definir contenedor */
.card-container {
    container-type: inline-size;
    /* 
    Explicación:
    - inline-size = el contenedor responde a cambios de ancho
    - block-size = el contenedor responde a cambios de altura
    - size = responde a ambos
    */
}

/* Query basado en el contenedor */
.card {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
}

@container (min-width: 400px) {
    .card {
        grid-template-columns: 1fr 1fr;
        /* 
        Explicación:
        - Cuando el contenedor tenga al menos 400px de ancho
        - La card cambia a layout de 2 columnas
        - No depende del viewport, solo del contenedor
        */
    }
}

@container (min-width: 600px) {
    .card {
        grid-template-columns: 1fr 1fr 1fr;
        /* Layout de 3 columnas en contenedores más anchos */
    }
}
```

## 🧪 Ejercicios Prácticos

### **Ejercicio 1: Sistema de Variables CSS**
Crea un sistema de diseño completo usando variables CSS.

**Instrucciones paso a paso:**
1. **Define variables globales** en :root para colores, espaciado, tipografía
2. **Crea variables de componente** para botones, cards, formularios
3. **Implementa un tema oscuro** que cambie las variables
4. **Usa calc()** para derivar valores de otras variables

**Requisitos:**
- Sistema de colores coherente
- Espaciado consistente
- Tema claro/oscuro funcional
- Variables bien organizadas

### **Ejercicio 2: Layout Responsivo con Funciones CSS**
Implementa un layout que use min(), max() y clamp().

**Instrucciones paso a paso:**
1. **Crea contenedor principal** con ancho responsivo
2. **Implementa sidebar** que nunca sea muy estrecha
3. **Usa clamp()** para tipografía responsiva
4. **Aplica min() y max()** para espaciado adaptativo

**Requisitos:**
- Layout que se adapta a diferentes pantallas
- Tipografía que nunca es muy pequeña o grande
- Espaciado que se mantiene proporcional
- Performance optimizada

### **Ejercicio 3: Pseudo-elementos Avanzados**
Crea componentes usando pseudo-elementos complejos.

**Instrucciones paso a paso:**
1. **Implementa drop cap** con ::first-letter
2. **Crea indicadores de estado** con ::before
3. **Estiliza selección de texto** con ::selection
4. **Añade decoraciones** con ::after

**Requisitos:**
- Drop cap funcional y atractivo
- Indicadores visuales claros
- Selección de texto estilizada
- Decoraciones consistentes

### **Ejercicio 4: Selectores de Atributos**
Desarrolla un sistema de estilos basado en atributos.

**Instrucciones paso a paso:**
1. **Crea estilos para inputs** basados en type y required
2. **Implementa estilos para enlaces** basados en href
3. **Añade estilos para imágenes** basados en src
4. **Crea clases utilitarias** basadas en atributos

**Requisitos:**
- Estilos automáticos para diferentes tipos de input
- Enlaces con estilos contextuales
- Imágenes con estilos basados en formato
- Sistema de clases utilitarias

### **Ejercicio 5: CSS Containment**
Optimiza el rendimiento usando CSS Containment.

**Instrucciones paso a paso:**
1. **Identifica componentes** que pueden usar containment
2. **Aplica layout containment** en secciones independientes
3. **Usa style containment** en widgets reutilizables
4. **Implementa paint containment** en elementos animados

**Requisitos:**
- Containment apropiado para cada componente
- Performance mejorada
- Componentes bien aislados
- Código optimizado

### **Ejercicio 6: Aspect-Ratio Responsivo**
Crea layouts que mantengan proporciones consistentes.

**Instrucciones paso a paso:**
1. **Implementa galería de imágenes** con aspect-ratio
2. **Crea cards** que mantengan proporciones
3. **Añade videos** con aspect-ratio 16:9
4. **Usa variables CSS** para ratios configurables

**Requisitos:**
- Imágenes que mantienen proporciones
- Cards con layout consistente
- Videos responsivos
- Ratios configurables

### **Ejercicio 7: Container Queries**
Implementa responsive design basado en contenedores.

**Instrucciones paso a paso:**
1. **Crea contenedores** con container-type definido
2. **Implementa queries** para diferentes tamaños de contenedor
3. **Crea layouts adaptativos** que no dependan del viewport
4. **Prueba en diferentes contextos** de layout

**Requisitos:**
- Layouts que se adaptan al contenedor
- No dependencia del viewport
- Componentes reutilizables
- Responsive design avanzado

### **Ejercicio 8: Sistema de Componentes con Variables**
Desarrolla un sistema de componentes usando técnicas modernas.

**Instrucciones paso a paso:**
1. **Define variables base** para el sistema de diseño
2. **Crea componentes** que usen las variables
3. **Implementa variantes** usando variables locales
4. **Añade temas** que cambien las variables

**Requisitos:**
- Sistema de componentes coherente
- Variantes bien definidas
- Temas funcionales
- Código mantenible

### **Ejercicio 9: Optimización Avanzada**
Combina múltiples técnicas de optimización.

**Instrucciones paso a paso:**
1. **Implementa CSS Containment** en componentes
2. **Usa variables CSS** para valores dinámicos
3. **Aplica aspect-ratio** para proporciones
4. **Optimiza con funciones CSS** modernas

**Requisitos:**
- Performance optimizada
- Código moderno y eficiente
- Componentes bien estructurados
- Técnicas avanzadas implementadas

### **Ejercicio 10: Proyecto Integrador Moderno**
Crea un proyecto que demuestre todas las técnicas aprendidas.

**Instrucciones paso a paso:**
1. **Planifica la arquitectura** usando variables CSS
2. **Implementa componentes** con containment
3. **Crea layouts responsivos** con container queries
4. **Optimiza performance** con técnicas modernas

**Requisitos:**
- Arquitectura CSS moderna
- Componentes optimizados
- Layouts responsivos avanzados
- Performance excelente

## 🎯 Proyecto Integrador: Sistema de Componentes Reutilizables

### Descripción del Proyecto
Crea un sistema de componentes completo que demuestre dominio de CSS moderno, variables, containment y técnicas avanzadas.

### Requisitos del Proyecto

#### **Arquitectura CSS (30%)**
- Sistema de variables CSS bien organizado
- Uso de funciones CSS modernas
- CSS Containment implementado
- Estructura modular y escalable

#### **Componentes (35%)**
- Botones con variantes y estados
- Cards con layouts adaptativos
- Formularios con validación visual
- Navegación responsive
- Modales y overlays

#### **Técnicas Modernas (25%)**
- Container queries implementados
- Aspect-ratio para proporciones
- Pseudo-elementos avanzados
- Selectores de atributos

#### **Performance (10%)**
- CSS optimizado
- Containment apropiado
- Variables eficientes
- Código mantenible

### Entregables
1. **Sistema de componentes** completo
2. **Documentación** de variables y uso
3. **Ejemplos** de implementación
4. **README** explicando la arquitectura
5. **Demo funcional** con todos los componentes

### Criterios de Evaluación
- **Arquitectura**: Sistema bien estructurado y escalable
- **Componentes**: Funcionales, atractivos y reutilizables
- **Técnicas**: Uso apropiado de CSS moderno
- **Performance**: Código optimizado y eficiente
- **Mantenibilidad**: Fácil de modificar y extender

## 📚 Recursos Adicionales

### Documentación
- [MDN CSS Custom Properties](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)
- [MDN CSS Functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions)
- [CSS Houdini](https://web.dev/css-houdini/)
- [Container Queries](https://web.dev/container-queries/)

### Herramientas
- [CSS Variable Generator](https://css-variables-generator.vercel.app/)
- [CSS Container Queries Polyfill](https://github.com/GoogleChromeLabs/container-query-polyfill)
- [CSS Houdini Playground](https://houdini.glitch.me/)

### Práctica
- [CSS Custom Properties](https://css-tricks.com/guides/css-custom-properties/)
- [Container Queries Examples](https://codepen.io/collection/nLLqyx)
- [Modern CSS Techniques](https://web.dev/learn/css/)

## 🔍 Preguntas de Repaso

1. **¿Cuál es la diferencia entre variables CSS y preprocesadores?**
2. **¿Cómo funciona calc() y cuándo es útil?**
3. **¿Qué ventajas tienen min(), max() y clamp()?**
4. **¿Cómo se implementan container queries?**
5. **¿Qué es CSS Houdini y cuándo usarlo?**
6. **¿Cómo optimiza CSS Containment el rendimiento?**
7. **¿Cuál es la diferencia entre aspect-ratio y height fijo?**
8. **¿Cómo se organizan las variables CSS en un proyecto grande?**
9. **¿Qué pseudo-elementos son más útiles para componentes?**
10. **¿Cómo se combinan múltiples técnicas modernas?**

## 🚀 Siguiente Paso

Una vez que hayas completado este módulo y el proyecto integrador, estarás listo para continuar con el **Módulo 7: Arquitectura CSS y Metodologías**, donde aprenderás sobre BEM, SMACSS, ITCSS y cómo organizar CSS a gran escala.

---

**¡Excelente trabajo! Ahora dominas las técnicas más modernas y avanzadas de CSS.** 🎉

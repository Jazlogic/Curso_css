# 🎨 Módulo 3: Responsive Design

## 🧭 Navegación del Curso

- **⬅️ Anterior**: [Módulo 2: Layout y Box Model](junior_2/README.md)
- **➡️ Siguiente**: [Módulo 4: CSS Grid y Flexbox Avanzado](midLevel_1/README.md)
- **📚 [Índice Completo](../INDICE_COMPLETO.md)** | **[🧭 Navegación Rápida](../NAVEGACION_RAPIDA.md)**

---

## 📚 Descripción del Módulo

En este módulo aprenderás los fundamentos del diseño responsivo, una habilidad esencial en el desarrollo web moderno. Aprenderás cómo crear sitios web que se adapten perfectamente a cualquier dispositivo, desde móviles hasta pantallas de escritorio. Cubriremos media queries, mobile-first approach, unidades responsivas y técnicas para crear experiencias web consistentes en todos los dispositivos.

## 🎯 Objetivos de Aprendizaje

Al completar este módulo, serás capaz de:

- ✅ Implementar media queries efectivamente
- ✅ Aplicar el enfoque mobile-first
- ✅ Usar unidades responsivas apropiadas
- ✅ Crear imágenes y contenido responsivo
- ✅ Definir breakpoints estratégicos
- ✅ Implementar viewport meta tag correctamente

## 📖 Contenido del Módulo

### 3.1 Media Queries Básicas

#### ¿Qué son las Media Queries?
Las Media Queries son una característica de CSS que permite aplicar estilos diferentes basados en características del dispositivo, como el ancho de pantalla, orientación, resolución y más.

```css
/* Sintaxis básica */
@media media-type and (media-feature: value) {
    /* Estilos CSS */
}

/* Ejemplo básico */
@media screen and (max-width: 768px) {
    .container {
        padding: 10px;
    }
}
```

#### Tipos de Media
```css
/* Media types */
@media screen { }           /* Pantallas de computadora */
@media print { }            /* Impresión */
@media speech { }           /* Lectores de pantalla */
@media all { }              /* Todos los dispositivos */

/* Media features más comunes */
@media (max-width: 768px) { }           /* Ancho máximo */
@media (min-width: 1024px) { }         /* Ancho mínimo */
@media (orientation: landscape) { }     /* Orientación horizontal */
@media (orientation: portrait) { }      /* Orientación vertical */
```

#### Media Queries Básicas por Ancho
```css
/* Mobile first - comienza con estilos para móvil */
.container {
    padding: 10px;
    font-size: 14px;
}

/* Tablet */
@media (min-width: 768px) {
    .container {
        padding: 20px;
        font-size: 16px;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .container {
        padding: 30px;
        font-size: 18px;
    }
}

/* Large desktop */
@media (min-width: 1200px) {
    .container {
        padding: 40px;
        font-size: 20px;
    }
}
```

#### Media Queries Avanzadas
```css
/* Rango de ancho */
@media (min-width: 768px) and (max-width: 1023px) {
    /* Solo tablet */
}

/* Múltiples condiciones */
@media (min-width: 768px) and (orientation: landscape) {
    /* Tablet en orientación horizontal */
}

/* Condiciones OR */
@media (max-width: 480px), (orientation: portrait) {
    /* Móvil O orientación vertical */
}

/* Negación */
@media not (max-width: 768px) {
    /* No móvil */
}
```

### 3.2 Mobile-First Approach

#### Filosofía Mobile-First
El enfoque mobile-first significa diseñar primero para dispositivos móviles y luego escalar hacia pantallas más grandes. Esto es más eficiente y mejora el rendimiento.

#### Implementación Práctica
```css
/* Base styles - Mobile first */
.container {
    width: 100%;
    padding: 15px;
    margin: 0 auto;
}

.nav {
    flex-direction: column;
    gap: 10px;
}

.grid {
    grid-template-columns: 1fr;
    gap: 20px;
}

/* Tablet */
@media (min-width: 768px) {
    .container {
        max-width: 720px;
        padding: 20px;
    }
    
    .nav {
        flex-direction: row;
        gap: 20px;
    }
    
    .grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 30px;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .container {
        max-width: 960px;
        padding: 30px;
    }
    
    .grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 40px;
    }
}
```

#### Ventajas del Mobile-First
- **Mejor rendimiento**: CSS más ligero para móviles
- **Mejor UX**: Enfoque en contenido esencial
- **Mejor SEO**: Google prioriza mobile-first
- **Mantenimiento**: Más fácil escalar que reducir

### 3.3 Unidades Relativas

#### Unidades de Viewport
```css
/* Viewport Width (vw) */
.full-width {
    width: 100vw;          /* 100% del ancho del viewport */
}

.half-width {
    width: 50vw;           /* 50% del ancho del viewport */
}

/* Viewport Height (vh) */
.full-height {
    height: 100vh;         /* 100% de la altura del viewport */
}

.half-height {
    height: 50vh;          /* 50% de la altura del viewport */
}

/* Viewport Min/Max */
.responsive-element {
    width: 90vw;           /* 90% del viewport */
    max-width: 1200px;     /* Pero no más de 1200px */
    min-width: 300px;      /* Y no menos de 300px */
}
```

#### Unidades Relativas a la Fuente
```css
/* Em - relativo al tamaño de fuente del elemento padre */
.parent {
    font-size: 16px;
}

.child {
    font-size: 1.5em;      /* 24px (1.5 × 16px) */
    margin: 1em;           /* 24px (1 × 24px) */
}

/* Rem - relativo al tamaño de fuente del elemento raíz */
html {
    font-size: 16px;
}

.element {
    font-size: 1.5rem;     /* 24px (1.5 × 16px) */
    margin: 1rem;          /* 16px (1 × 16px) */
}

/* Ejemplo práctico */
.responsive-text {
    font-size: clamp(1rem, 4vw, 2rem);
    line-height: 1.6;
    margin: 1rem 0;
}
```

#### Unidades de Porcentaje
```css
/* Porcentaje del elemento padre */
.container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
}

.sidebar {
    width: 25%;            /* 25% del ancho del contenedor */
}

.content {
    width: 75%;            /* 75% del ancho del contenedor */
}

/* Porcentaje en padding y margin */
.element {
    padding: 5% 10%;       /* 5% vertical, 10% horizontal */
    margin: 2% 0;          /* 2% vertical, 0 horizontal */
}
```

### 3.4 Imágenes Responsivas

#### Imágenes Básicas Responsivas
```css
/* Imagen que se adapta al contenedor */
.responsive-image {
    max-width: 100%;
    height: auto;
    display: block;
}

/* Imagen con aspect ratio */
.aspect-ratio-image {
    width: 100%;
    aspect-ratio: 16 / 9;
    object-fit: cover;
}
```

#### HTML para Imágenes Responsivas
```html
<!-- Imagen básica responsiva -->
<img src="image.jpg" alt="Descripción" class="responsive-image">

<!-- Imagen con srcset para diferentes resoluciones -->
<img src="image-small.jpg" 
     srcset="image-small.jpg 300w,
             image-medium.jpg 600w,
             image-large.jpg 900w"
     sizes="(max-width: 600px) 300px,
            (max-width: 900px) 600px,
            900px"
     alt="Descripción">

<!-- Imagen con picture element -->
<picture>
    <source media="(max-width: 600px)" srcset="image-mobile.jpg">
    <source media="(max-width: 1024px)" srcset="image-tablet.jpg">
    <img src="image-desktop.jpg" alt="Descripción">
</picture>
```

#### CSS para Diferentes Tamaños de Imagen
```css
/* Imágenes responsivas con CSS */
.hero-image {
    width: 100%;
    height: 300px;
    object-fit: cover;
}

@media (min-width: 768px) {
    .hero-image {
        height: 400px;
    }
}

@media (min-width: 1024px) {
    .hero-image {
        height: 500px;
    }
}

/* Galería de imágenes responsiva */
.gallery {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
}

@media (min-width: 768px) {
    .gallery {
        grid-template-columns: repeat(2, 1fr);
        gap: 30px;
    }
}

@media (min-width: 1024px) {
    .gallery {
        grid-template-columns: repeat(3, 1fr);
        gap: 40px;
    }
}
```

### 3.5 Breakpoints y Estrategias

#### Breakpoints Comunes
```css
/* Breakpoints estándar de la industria */
/* Mobile: 0px - 767px */
/* Tablet: 768px - 1023px */
/* Desktop: 1024px - 1439px */
/* Large Desktop: 1440px+ */

/* Sistema de breakpoints */
:root {
    --mobile: 480px;
    --tablet: 768px;
    --desktop: 1024px;
    --large: 1200px;
    --xl: 1440px;
}

/* Uso de variables CSS */
@media (min-width: var(--tablet)) {
    .container {
        max-width: 720px;
    }
}
```

#### Estrategias de Breakpoints
```css
/* Estrategia 1: Breakpoints basados en contenido */
.container {
    width: 100%;
    padding: 20px;
}

/* Cuando el contenido se ve mal */
@media (min-width: 600px) {
    .container {
        max-width: 600px;
        margin: 0 auto;
    }
}

/* Estrategia 2: Breakpoints basados en dispositivos */
/* iPhone SE y similares */
@media (max-width: 375px) {
    .container {
        padding: 10px;
    }
}

/* iPhone 12/13/14 */
@media (min-width: 376px) and (max-width: 428px) {
    .container {
        padding: 15px;
    }
}

/* iPad */
@media (min-width: 768px) and (max-width: 1024px) {
    .container {
        padding: 30px;
    }
}
```

#### Container Queries (CSS Moderno)
```css
/* Container queries - responsive basado en el contenedor */
.card-container {
    container-type: inline-size;
}

.card {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
}

@container (min-width: 400px) {
    .card {
        grid-template-columns: 1fr 1fr;
    }
}

@container (min-width: 600px) {
    .card {
        grid-template-columns: 1fr 1fr 1fr;
    }
}
```

### 3.6 Viewport Meta Tag

#### Configuración Básica
```html
<!-- Meta tag esencial para responsive design -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

#### Configuraciones Avanzadas
```html
<!-- Configuración completa -->
<meta name="viewport" content="
    width=device-width,
    initial-scale=1.0,
    maximum-scale=5.0,
    minimum-scale=0.5,
    user-scalable=yes,
    viewport-fit=cover
">

<!-- Para dispositivos con notch -->
<meta name="viewport" content="
    width=device-width,
    initial-scale=1.0,
    viewport-fit=cover
">
```

#### CSS para Safe Areas
```css
/* CSS para dispositivos con notch */
.safe-area {
    padding-top: env(safe-area-inset-top);
    padding-bottom: env(safe-area-inset-bottom);
    padding-left: env(safe-area-inset-left);
    padding-right: env(safe-area-inset-right);
}

/* Shorthand */
.safe-area {
    padding: env(safe-area-inset-top) 
             env(safe-area-inset-right) 
             env(safe-area-inset-bottom) 
             env(safe-area-inset-left);
}
```

### 3.7 Técnicas de Layout Responsivo

#### Grid Responsivo
```css
/* Grid responsivo básico */
.grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    padding: 20px;
}

/* Tablet */
@media (min-width: 768px) {
    .grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 30px;
        padding: 30px;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 40px;
        padding: 40px;
    }
}

/* Large desktop */
@media (min-width: 1200px) {
    .grid {
        grid-template-columns: repeat(4, 1fr);
        gap: 50px;
        padding: 50px;
    }
}
```

#### Flexbox Responsivo
```css
/* Flexbox responsivo */
.flex-container {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.flex-item {
    flex: 1;
}

/* Tablet */
@media (min-width: 768px) {
    .flex-container {
        flex-direction: row;
        gap: 30px;
    }
    
    .flex-item {
        flex: 0 0 calc(50% - 15px);
    }
}

/* Desktop */
@media (min-width: 1024px) {
    .flex-container {
        gap: 40px;
    }
    
    .flex-item {
        flex: 0 0 calc(33.333% - 26.667px);
    }
}
```

#### Navegación Responsiva
```css
/* Navegación mobile-first */
.nav {
    display: flex;
    flex-direction: column;
    gap: 10px;
    padding: 20px;
}

.nav-item {
    padding: 10px;
    border-bottom: 1px solid #eee;
}

/* Tablet y desktop */
@media (min-width: 768px) {
    .nav {
        flex-direction: row;
        gap: 20px;
        padding: 0;
        border-bottom: none;
    }
    
    .nav-item {
        border-bottom: none;
        padding: 15px 20px;
    }
}

/* Menú hamburguesa para móvil */
.menu-toggle {
    display: block;
}

@media (min-width: 768px) {
    .menu-toggle {
        display: none;
    }
}
```

## 🧪 Ejercicios Prácticos

### **Ejercicio 1: Media Queries Básicas**
Crea una página que cambie completamente su layout en diferentes breakpoints.

**Requisitos:**
- Usa al menos 3 breakpoints diferentes
- Cambia colores, layout y tipografía
- Implementa mobile-first approach

### **Ejercicio 2: Sistema de Grid Responsivo**
Desarrolla un sistema de grid que se adapte a diferentes tamaños de pantalla.

**Requisitos:**
- Grid de 12 columnas
- Breakpoints para móvil, tablet y desktop
- Gutter responsivo
- Uso de unidades relativas

### **Ejercicio 3: Navegación Responsiva**
Crea una navegación que se adapte a diferentes dispositivos.

**Requisitos:**
- Menú hamburguesa para móvil
- Navegación horizontal para desktop
- Transiciones suaves
- Mobile-first approach

### **Ejercicio 4: Galería de Imágenes Responsiva**
Implementa una galería que se adapte a diferentes tamaños de pantalla.

**Requisitos:**
- Grid responsivo de imágenes
- Diferentes layouts por breakpoint
- Imágenes optimizadas
- Hover effects

### **Ejercicio 5: Tipografía Responsiva**
Crea un sistema de tipografía que se adapte a diferentes dispositivos.

**Requisitos:**
- Escala tipográfica responsiva
- Uso de unidades rem y vw
- Diferentes tamaños por breakpoint
- Legibilidad optimizada

### **Ejercicio 6: Formularios Responsivos**
Diseña formularios que funcionen bien en todos los dispositivos.

**Requisitos:**
- Layout adaptativo
- Tamaños de input apropiados
- Validación visual
- Accesibilidad mejorada

### **Ejercicio 7: Cards Responsivas**
Desarrolla un sistema de cards que se adapte a diferentes layouts.

**Requisitos:**
- Cards que cambian de layout
- Imágenes responsivas
- Contenido adaptativo
- Hover effects

### **Ejercicio 8: Sidebar Responsiva**
Crea una sidebar que se comporte diferente en móvil y desktop.

**Requisitos:**
- Sidebar fija en desktop
- Sidebar colapsable en móvil
- Overlay para móvil
- Transiciones suaves

### **Ejercicio 9: Hero Section Responsiva**
Implementa una sección hero que se adapte a diferentes dispositivos.

**Requisitos:**
- Imagen de fondo responsiva
- Texto que se adapte
- CTA buttons responsivos
- Performance optimizada

### **Ejercicio 10: Footer Responsivo**
Diseña un footer que se reorganice en diferentes dispositivos.

**Requisitos:**
- Layout adaptativo
- Información organizada
- Enlaces funcionales
- Responsive design completo

## 🎯 Proyecto Integrador: Sitio Web Responsivo para Restaurante

### Descripción del Proyecto
Crea un sitio web completo para un restaurante que se adapte perfectamente a todos los dispositivos, desde móviles hasta pantallas de escritorio.

### Requisitos del Proyecto

#### **Estructura HTML (25%)**
- Header con navegación responsiva
- Hero section con imagen de fondo
- Sección de menú con grid responsivo
- Sección "Sobre nosotros"
- Formulario de reservas
- Footer con información de contacto

#### **Responsive Design (40%)**
- Mobile-first approach
- Media queries efectivas
- Breakpoints estratégicos
- Layouts adaptativos
- Imágenes responsivas

#### **Navegación (20%)**
- Menú hamburguesa para móvil
- Navegación horizontal para desktop
- Transiciones suaves
- Estados interactivos

#### **Performance (15%)**
- Imágenes optimizadas
- CSS eficiente
- Transiciones suaves
- Carga rápida

### Entregables
1. **Archivo HTML** (`index.html`)
2. **Archivo CSS** (`styles.css`)
3. **Página de menú** (`menu.html`)
4. **Página de reservas** (`reservations.html`)
5. **README** explicando las decisiones de responsive design
6. **Capturas de pantalla** en diferentes dispositivos

### Criterios de Evaluación
- **Responsive**: Funciona perfectamente en todos los dispositivos
- **Mobile-first**: Implementación correcta del enfoque
- **Media Queries**: Uso efectivo de breakpoints
- **Performance**: Carga rápida y optimizada
- **UX**: Experiencia consistente en todos los dispositivos

## 📚 Recursos Adicionales

### Documentación
- [MDN Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries)
- [MDN Responsive Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [CSS Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Container_Queries)

### Herramientas
- [Responsive Design Checker](https://responsivedesignchecker.com/)
- [Mobile-Friendly Test](https://search.google.com/test/mobile-friendly)
- [Browser DevTools](https://developer.chrome.com/docs/devtools/)

### Práctica
- [Responsive Web Design](https://www.freecodecamp.org/learn/responsive-web-design/)
- [CSS Grid Garden](https://cssgridgarden.com/)
- [Flexbox Froggy](https://flexboxfroggy.com/)

## 🔍 Preguntas de Repaso

1. **¿Qué son las media queries y cuándo se usan?**
2. **¿Cuál es la diferencia entre mobile-first y desktop-first?**
3. **¿Cuáles son las ventajas de usar unidades relativas?**
4. **¿Cómo funciona el viewport meta tag?**
5. **¿Qué son los breakpoints y cómo se eligen?**
6. **¿Cómo se implementan imágenes responsivas?**
7. **¿Qué son las container queries?**
8. **¿Cómo se crea un grid responsivo?**
9. **¿Cuál es la importancia del mobile-first approach?**
10. **¿Cómo se optimiza el performance en responsive design?**

## 🚀 Siguiente Paso

Una vez que hayas completado este módulo y el proyecto integrador, estarás listo para continuar con el **Módulo 4: CSS Grid y Flexbox Avanzado**, donde aprenderás técnicas avanzadas de layout y cómo crear layouts complejos y profesionales.

---

## 🧭 Navegación del Curso

- **⬅️ Anterior**: [Módulo 2: Layout y Box Model](junior_2/README.md)
- **➡️ Siguiente**: [Módulo 4: CSS Grid y Flexbox Avanzado](midLevel_1/README.md)
- **📚 [Índice Completo](../INDICE_COMPLETO.md)** | **[🧭 Navegación Rápida](../NAVEGACION_RAPIDA.md)**

---

**¡Excelente trabajo! Ahora puedes crear sitios web que se adapten perfectamente a cualquier dispositivo.** 🎉

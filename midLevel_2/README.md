# 🎨 Módulo 5: Animaciones y Transiciones

## 🧭 Navegación del Curso

- **⬅️ Anterior**: [Módulo 4: CSS Grid y Flexbox Avanzado](midLevel_1/README.md)
- **➡️ Siguiente**: [Módulo 6: CSS Moderno y Avanzado](midLevel_3/README.md)
- **📚 [Índice Completo](../INDICE_COMPLETO.md)** | **[🧭 Navegación Rápida](../NAVEGACION_RAPIDA.md)**

---

## 📚 Descripción del Módulo

En este módulo aprenderás a dar vida a tus sitios web con CSS. Las animaciones y transiciones transforman sitios estáticos en experiencias dinámicas y atractivas. Aprenderás desde transiciones simples hasta animaciones complejas con keyframes, optimización de performance y técnicas avanzadas.

## 🎯 Objetivos de Aprendizaje

Al completar este módulo, serás capaz de:

- ✅ Implementar transiciones CSS suaves y atractivas
- ✅ Crear animaciones complejas con @keyframes
- ✅ Optimizar animaciones para mejor performance
- ✅ Usar timing functions y easing para movimientos naturales
- ✅ Crear animaciones de entrada y salida
- ✅ Combinar CSS y JavaScript para animaciones interactivas

## 📖 Contenido del Módulo

### 5.1 Transiciones CSS - El Primer Paso

#### ¿Qué son las Transiciones CSS?

Las transiciones CSS permiten que las propiedades cambien suavemente de un valor a otro durante un período de tiempo específico. Es como decirle al navegador: "No cambies este valor de golpe, hazlo gradualmente".

#### Propiedades Básicas de Transición

```css
/* Propiedad básica - transición de color */
.button {
    background-color: blue;
    transition: background-color 0.3s ease;
    /* 
    Explicación paso a paso:
    1. transition = activa la transición
    2. background-color = qué propiedad se anima
    3. 0.3s = duración de la transición (300 milisegundos)
    4. ease = función de timing (aceleración natural)
    */
}

.button:hover {
    background-color: red;
    /* Al hacer hover, el color cambia suavemente de azul a rojo */
}
```

#### Propiedades de Transición Completas

```css
.element {
    /* Shorthand - todas las propiedades en una línea */
    transition: all 0.5s ease-in-out;
    
    /* Propiedades individuales para control preciso */
    transition-property: transform, opacity, background-color;
    transition-duration: 0.3s, 0.5s, 0.2s;
    transition-timing-function: ease, linear, ease-out;
    transition-delay: 0s, 0.1s, 0.2s;
    
    /* 
    Explicación detallada:
    - transform: se anima en 0.3s con ease
    - opacity: se anima en 0.5s con linear
    - background-color: se anima en 0.2s con ease-out
    - Los delays crean un efecto escalonado
    */
}
```

### 5.2 Timing Functions - Haciendo Movimientos Naturales

#### ¿Qué son las Timing Functions?

Las timing functions controlan cómo se acelera y desacelera una animación. Son como las leyes de la física para tus animaciones CSS.

#### Tipos de Timing Functions

```css
.element {
    /* Easing básico */
    transition: all 0.5s ease;        /* Aceleración natural */
    transition: all 0.5s linear;      /* Velocidad constante */
    transition: all 0.5s ease-in;     /* Lento al inicio, rápido al final */
    transition: all 0.5s ease-out;    /* Rápido al inicio, lento al final */
    transition: all 0.5s ease-in-out; /* Lento al inicio y al final */
    
    /* Easing personalizado con cubic-bezier */
    transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    /* 
    Explicación de cubic-bezier:
    - 0.68, -0.55, 0.265, 1.55 = crea un efecto "bounce"
    - Los números controlan la curva de aceleración
    - Resultado: animación que rebota al final
    */
}
```

#### Ejemplos Prácticos de Timing Functions

```css
/* Botón con efecto de rebote */
.bounce-button {
    transition: transform 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
}

.bounce-button:hover {
    transform: scale(1.1);
    /* El botón crece con un efecto de rebote */
}

/* Card con efecto de entrada suave */
.card {
    transition: all 0.4s ease-out;
    opacity: 0;
    transform: translateY(20px);
}

.card.visible {
    opacity: 1;
    transform: translateY(0);
    /* La card aparece deslizándose hacia arriba */
}
```

### 5.3 Transformaciones - Moviendo y Cambiando Elementos

#### ¿Qué son las Transformaciones?

Las transformaciones CSS permiten mover, rotar, escalar y sesgar elementos sin afectar el layout de otros elementos. Es como tener un control total sobre la posición y forma de cada elemento.

#### Transformaciones Básicas

```css
.element {
    /* Translate - mover elementos */
    transform: translateX(50px);      /* Mover 50px a la derecha */
    transform: translateY(-20px);     /* Mover 20px hacia arriba */
    transform: translate(30px, 40px); /* Mover 30px derecha, 40px abajo */
    
    /* Scale - cambiar tamaño */
    transform: scale(1.5);            /* Aumentar 50% */
    transform: scaleX(2);             /* Duplicar solo el ancho */
    transform: scaleY(0.5);           /* Reducir altura a la mitad */
    
    /* Rotate - girar elementos */
    transform: rotate(45deg);         /* Girar 45 grados */
    transform: rotateX(90deg);        /* Girar en eje X (3D) */
    transform: rotateY(180deg);       /* Girar en eje Y (3D) */
}
```

#### Combinando Múltiples Transformaciones

```css
.element {
    /* Múltiples transformaciones en una línea */
    transform: translateX(50px) scale(1.2) rotate(15deg);
    /* 
    Orden de aplicación:
    1. translateX(50px) - mueve el elemento
    2. scale(1.2) - lo agranda
    3. rotate(15deg) - lo gira
    */
}

/* Ejemplo práctico - Botón con hover complejo */
.complex-button {
    transition: transform 0.3s ease;
}

.complex-button:hover {
    transform: translateY(-5px) scale(1.05) rotate(2deg);
    /* 
    Al hacer hover:
    - Se mueve 5px hacia arriba
    - Crece 5%
    - Gira ligeramente 2 grados
    */
}
```

### 5.4 Animaciones con @keyframes - Control Total

#### ¿Qué son las @keyframes?

@keyframes te permiten crear animaciones complejas definiendo exactamente qué debe pasar en cada momento de la animación. Es como crear una película frame por frame.

#### Sintaxis Básica de @keyframes

```css
/* Definir la animación */
@keyframes slideIn {
    /* Estado inicial (0%) */
    0% {
        opacity: 0;
        transform: translateX(-100px);
    }
    
    /* Estado intermedio (50%) */
    50% {
        opacity: 0.5;
        transform: translateX(-50px);
    }
    
    /* Estado final (100%) */
    100% {
        opacity: 1;
        transform: translateX(0);
    }
}

/* Aplicar la animación */
.sliding-element {
    animation: slideIn 1s ease-out;
    /* 
    Explicación:
    - slideIn = nombre de la animación
    - 1s = duración
    - ease-out = función de timing
    */
}
```

#### Propiedades de Animación Avanzadas

```css
.animated-element {
    /* Propiedades básicas */
    animation-name: slideIn;
    animation-duration: 1s;
    animation-timing-function: ease-out;
    
    /* Propiedades avanzadas */
    animation-delay: 0.5s;           /* Esperar 0.5s antes de empezar */
    animation-iteration-count: 3;    /* Repetir 3 veces */
    animation-direction: alternate;   /* Alternar dirección */
    animation-fill-mode: forwards;    /* Mantener estado final */
    
    /* Shorthand completo */
    animation: slideIn 1s ease-out 0.5s 3 alternate forwards;
    /* nombre duración timing delay iteraciones dirección fill-mode */
}
```

### 5.5 Animaciones de Entrada y Salida

#### Animaciones de Entrada - Haciendo Elementos Visibles

```css
/* Fade In - Aparecer gradualmente */
@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

.fade-in {
    animation: fadeIn 0.8s ease-in;
}

/* Slide In desde arriba */
@keyframes slideInFromTop {
    from {
        opacity: 0;
        transform: translateY(-50px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.slide-in-top {
    animation: slideInFromTop 0.6s ease-out;
}

/* Zoom In - Aparecer agrandándose */
@keyframes zoomIn {
    from {
        opacity: 0;
        transform: scale(0.3);
    }
    to {
        opacity: 1;
        transform: scale(1);
    }
}

.zoom-in {
    animation: zoomIn 0.5s ease-out;
}
```

#### Animaciones de Salida - Haciendo Elementos Invisibles

```css
/* Fade Out - Desaparecer gradualmente */
@keyframes fadeOut {
    from {
        opacity: 1;
    }
    to {
        opacity: 0;
    }
}

.fade-out {
    animation: fadeOut 0.5s ease-in;
}

/* Slide Out hacia la derecha */
@keyframes slideOutToRight {
    from {
        opacity: 1;
        transform: translateX(0);
    }
    to {
        opacity: 0;
        transform: translateX(100px);
    }
}

.slide-out-right {
    animation: slideOutToRight 0.4s ease-in;
}
```

### 5.6 Performance y Optimización

#### ¿Por qué es Importante la Performance?

Las animaciones mal optimizadas pueden hacer que tu sitio web se sienta lento y poco responsivo. Aprender a optimizar es crucial para una experiencia de usuario fluida.

#### Propiedades que se Animan Mejor

```css
/* ✅ BUENAS - Se animan suavemente */
.element {
    /* Transformaciones */
    transform: translateX(100px);
    transform: scale(1.2);
    transform: rotate(45deg);
    
    /* Opacidad */
    opacity: 0.5;
    
    /* Filtros (con cuidado) */
    filter: blur(2px);
}

/* ❌ MALAS - Pueden causar lag */
.element {
    /* Cambios de layout */
    width: 200px;
    height: 100px;
    margin: 20px;
    padding: 10px;
    
    /* Posicionamiento */
    top: 100px;
    left: 50px;
}
```

#### Usando will-change para Optimización

```css
.element {
    /* Indicar al navegador que este elemento cambiará */
    will-change: transform, opacity;
    
    /* 
    Explicación:
    - will-change le dice al navegador que prepare recursos
    - Solo usar en elementos que realmente cambiarán
    - No usar en exceso - consume memoria
    */
}

/* Ejemplo práctico - Botón que se anima frecuentemente */
.animated-button {
    will-change: transform;
    transition: transform 0.2s ease;
}

.animated-button:hover {
    transform: scale(1.1);
}
```

### 5.7 Animaciones con JavaScript

#### ¿Cuándo Usar JavaScript para Animaciones?

JavaScript es útil para:
- Animaciones basadas en eventos del usuario
- Animaciones que dependen de datos dinámicos
- Control preciso del timing y estado

#### Ejemplo Básico - Animación con JavaScript

```javascript
// Función para animar entrada de elementos
function animateElement(element, animationClass) {
    // Añadir la clase de animación
    element.classList.add(animationClass);
    
    // Escuchar cuando termine la animación
    element.addEventListener('animationend', function() {
        // Remover la clase después de la animación
        element.classList.remove(animationClass);
    });
}

// Usar la función
const button = document.querySelector('.my-button');
animateElement(button, 'bounce');
```

#### CSS para las Animaciones

```css
/* Animación de rebote */
@keyframes bounce {
    0%, 20%, 53%, 80%, 100% {
        transform: translateY(0);
    }
    40%, 43% {
        transform: translateY(-30px);
    }
    70% {
        transform: translateY(-15px);
    }
    90% {
        transform: translateY(-4px);
    }
}

.bounce {
    animation: bounce 1s ease-in-out;
}
```

## 🧪 Ejercicios Prácticos

### **Ejercicio 1: Botones con Transiciones**
Crea botones con diferentes tipos de transiciones.

**Instrucciones paso a paso:**
1. **Crea 3 botones** con diferentes estilos
2. **Añade transiciones** para diferentes propiedades
3. **Experimenta con timing functions** (ease, ease-in, ease-out)
4. **Prueba diferentes duraciones** (0.2s, 0.5s, 1s)

**Requisitos:**
- Botón que cambia color suavemente
- Botón que se agranda al hacer hover
- Botón que se mueve ligeramente

### **Ejercicio 2: Cards con Animaciones de Entrada**
Implementa cards que aparecen con diferentes animaciones.

**Instrucciones paso a paso:**
1. **Crea un contenedor** con display: grid
2. **Añade 6 cards** con contenido
3. **Implementa animaciones** de fadeIn, slideIn, zoomIn
4. **Usa delays escalonados** para efecto cascada

**Requisitos:**
- Cards aparecen una por una
- Diferentes tipos de animación
- Efecto visual atractivo

### **Ejercicio 3: Menú de Navegación Animado**
Crea un menú con animaciones suaves.

**Instrucciones paso a paso:**
1. **Crea navegación horizontal** con Flexbox
2. **Añade indicador activo** que se mueve
3. **Implementa transiciones** para cambios de estado
4. **Añade hover effects** en los enlaces

**Requisitos:**
- Indicador que se mueve suavemente
- Enlaces con efectos hover
- Transiciones fluidas

### **Ejercicio 4: Galería con Animaciones**
Crea una galería de imágenes con efectos animados.

**Instrucciones paso a paso:**
1. **Organiza imágenes** en grid responsivo
2. **Añade overlay** que aparece al hacer hover
3. **Implementa zoom** en las imágenes
4. **Usa transformaciones** para efectos 3D

**Requisitos:**
- Imágenes que se agrandan suavemente
- Overlay con fade in/out
- Efectos 3D sutiles

### **Ejercicio 5: Loading Spinner**
Crea un spinner de carga animado.

**Instrucciones paso a paso:**
1. **Crea círculo base** con border-radius
2. **Implementa rotación** con @keyframes
3. **Añade gradiente** para efecto visual
4. **Optimiza con will-change**

**Requisitos:**
- Rotación continua y suave
- Efecto visual atractivo
- Performance optimizada

### **Ejercicio 6: Modal con Animaciones**
Desarrolla un modal que aparece y desaparece suavemente.

**Instrucciones paso a paso:**
1. **Crea overlay** con fondo semi-transparente
2. **Implementa modal** con contenido
3. **Añade animaciones** de entrada y salida
4. **Usa JavaScript** para controlar estados

**Requisitos:**
- Aparece con fade in y slide
- Desaparece con fade out
- Overlay animado

### **Ejercicio 7: Timeline Animado**
Crea una timeline con elementos que aparecen secuencialmente.

**Instrucciones paso a paso:**
1. **Estructura timeline** con Grid o Flexbox
2. **Añade elementos** con contenido
3. **Implementa animaciones** escalonadas
4. **Usa scroll trigger** para activar animaciones

**Requisitos:**
- Elementos aparecen al hacer scroll
- Animaciones secuenciales
- Efecto visual coherente

### **Ejercicio 8: Formulario con Validación Animada**
Crea un formulario con feedback visual animado.

**Instrucciones paso a paso:**
1. **Implementa formulario** con inputs
2. **Añade validación** con JavaScript
3. **Crea animaciones** para estados válidos/inválidos
4. **Usa shake** para errores

**Requisitos:**
- Feedback visual inmediato
- Animaciones para diferentes estados
- UX mejorada

### **Ejercicio 9: Parallax Scrolling**
Implementa efecto parallax con CSS y JavaScript.

**Instrucciones paso a paso:**
1. **Crea secciones** con diferentes velocidades
2. **Implementa scroll listener** en JavaScript
3. **Aplica transformaciones** basadas en scroll
4. **Optimiza performance** con requestAnimationFrame

**Requisitos:**
- Efecto parallax suave
- Performance optimizada
- Responsive design

### **Ejercicio 10: Dashboard con Animaciones**
Crea un dashboard con widgets animados.

**Instrucciones paso a paso:**
1. **Estructura dashboard** con Grid
2. **Implementa widgets** con contenido
3. **Añade animaciones** de entrada
4. **Crea interacciones** hover y click

**Requisitos:**
- Widgets aparecen secuencialmente
- Interacciones animadas
- Layout responsive

## 🎯 Proyecto Integrador: Galería Interactiva con Animaciones

### Descripción del Proyecto
Crea una galería de imágenes completa con animaciones avanzadas, efectos de hover, lightbox y transiciones suaves.

### Requisitos del Proyecto

#### **Estructura HTML (25%)**
- Grid responsivo de imágenes
- Lightbox para vista ampliada
- Navegación entre imágenes
- Filtros por categorías

#### **Animaciones CSS (40%)**
- Transiciones suaves en hover
- Animaciones de entrada para imágenes
- Efectos de zoom y overlay
- Transiciones entre estados

#### **Interactividad (20%)**
- Lightbox funcional
- Navegación con teclado
- Filtros animados
- Loading states

#### **Performance (15%)**
- Optimización de animaciones
- Lazy loading de imágenes
- Uso apropiado de will-change
- Transiciones hardware-accelerated

### Entregables
1. **Archivo HTML** (`index.html`)
2. **Archivo CSS** (`styles.css`)
3. **JavaScript** (`script.js`)
4. **README** explicando las técnicas de animación
5. **Demo funcional** con imágenes de ejemplo

### Criterios de Evaluación
- **Animaciones**: Suaves, atractivas y funcionales
- **Performance**: Sin lag o saltos
- **UX**: Experiencia intuitiva y agradable
- **Código**: CSS y JS limpios y optimizados
- **Responsive**: Funciona en todos los dispositivos

## 📚 Recursos Adicionales

### Documentación
- [MDN CSS Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions)
- [MDN CSS Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)
- [MDN CSS Transforms](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)

### Herramientas
- [CSS Animation Libraries](https://animate.style/)
- [Cubic Bezier Generator](https://cubic-bezier.com/)
- [CSS Animation Examples](https://codepen.io/collection/nLLqyx)

### Práctica
- [CSS Animation Playground](https://cssanimation.rocks/)
- [Animation Performance](https://web.dev/animations/)
- [CSS Animation Best Practices](https://css-tricks.com/tips-for-writing-animation-code-efficiently/)

## 🔍 Preguntas de Repaso

1. **¿Cuál es la diferencia entre transition y animation?**
2. **¿Qué hace cubic-bezier y cuándo usarlo?**
3. **¿Por qué es importante optimizar las animaciones?**
4. **¿Cuáles son las mejores propiedades para animar?**
5. **¿Cómo se crea una animación infinita?**
6. **¿Qué es will-change y cuándo usarlo?**
7. **¿Cómo se combinan múltiples transformaciones?**
8. **¿Cuál es la diferencia entre ease-in y ease-out?**
9. **¿Cómo se crea un efecto parallax?**
10. **¿Cuáles son las mejores prácticas para animaciones?**

## 🚀 Siguiente Paso

Una vez que hayas completado este módulo y el proyecto integrador, estarás listo para continuar con el **Módulo 6: CSS Moderno y Avanzado**, donde aprenderás sobre variables CSS, funciones modernas y técnicas avanzadas.

---

## 🧭 Navegación del Curso

- **⬅️ Anterior**: [Módulo 4: CSS Grid y Flexbox Avanzado](midLevel_1/README.md)
- **➡️ Siguiente**: [Módulo 6: CSS Moderno y Avanzado](midLevel_3/README.md)
- **📚 [Índice Completo](../INDICE_COMPLETO.md)** | **[🧭 Navegación Rápida](../NAVEGACION_RAPIDA.md)**

---

**¡Excelente trabajo! Ahora puedes crear experiencias web dinámicas y atractivas con CSS.** 🎉

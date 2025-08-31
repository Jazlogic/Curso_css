# 🎨 Módulo 9: Testing y Debugging CSS

## 📚 Descripción del Módulo

En este módulo aprenderás técnicas avanzadas para probar y depurar CSS en diferentes entornos. Desde testing automatizado hasta debugging en navegadores, pasando por herramientas de análisis visual y testing de accesibilidad, dominarás todo lo necesario para crear CSS robusto y confiable.

## 🎯 Objetivos de Aprendizaje

Al completar este módulo, serás capaz de:

- ✅ Implementar testing automatizado para CSS
- ✅ Usar herramientas avanzadas de debugging
- ✅ Crear tests de accesibilidad y cross-browser
- ✅ Implementar visual regression testing
- ✅ Debuggear problemas complejos de CSS
- ✅ Crear estrategias de testing para proyectos grandes

## 📖 Contenido del Módulo

### 9.1 Testing Automatizado de CSS - Garantizando Calidad

#### ¿Por qué Testing CSS es Importante?

El CSS puede tener bugs sutiles que afectan la experiencia del usuario. Testing automatizado te permite detectar problemas antes de que lleguen a producción.

#### Jest con CSS Testing

```javascript
// css-testing.test.js
import { render } from '@testing-library/react';
import '@testing-library/jest-dom';

describe('CSS Component Testing', () => {
    test('button tiene estilos correctos', () => {
        const { getByRole } = render(
            <button className="btn btn--primary">Test Button</button>
        );
        
        const button = getByRole('button');
        
        // Verificar clases CSS
        expect(button).toHaveClass('btn');
        expect(button).toHaveClass('btn--primary');
        
        // Verificar estilos computados
        const styles = window.getComputedStyle(button);
        expect(styles.backgroundColor).toBe('rgb(0, 123, 255)');
        expect(styles.color).toBe('rgb(255, 255, 255)');
    });
    
    test('card tiene layout correcto', () => {
        const { getByTestId } = render(
            <div data-testid="card" className="card">
                <h3>Card Title</h3>
                <p>Card content</p>
            </div>
        );
        
        const card = getByTestId('card');
        const styles = window.getComputedStyle(card);
        
        // Verificar propiedades de layout
        expect(styles.display).toBe('block');
        expect(styles.padding).toBe('20px');
        expect(styles.borderRadius).toBe('8px');
    });
});

/* 
Explicación paso a paso:
1. @testing-library/react = librería para testing de React
2. @testing-library/jest-dom = matchers adicionales para Jest
3. getComputedStyle = obtiene estilos computados del elemento
4. Verificamos tanto clases como estilos aplicados
5. Resultado = tests que verifican CSS real
*/
```

#### Testing de Responsive Design

```javascript
// responsive-testing.test.js
describe('Responsive CSS Testing', () => {
    beforeEach(() => {
        // Simular diferentes viewports
        Object.defineProperty(window, 'innerWidth', {
            writable: true,
            configurable: true,
            value: 1200
        });
        
        // Disparar evento resize
        window.dispatchEvent(new Event('resize'));
    });
    
    test('layout se adapta a desktop', () => {
        const { getByTestId } = render(
            <div data-testid="container" className="responsive-container">
                <div className="sidebar">Sidebar</div>
                <div className="content">Content</div>
            </div>
        );
        
        const container = getByTestId('container');
        const styles = window.getComputedStyle(container);
        
        // Verificar layout de desktop
        expect(styles.gridTemplateColumns).toBe('250px 1fr');
    });
    
    test('layout se adapta a mobile', () => {
        // Cambiar a viewport móvil
        Object.defineProperty(window, 'innerWidth', {
            writable: true,
            configurable: true,
            value: 768
        });
        
        window.dispatchEvent(new Event('resize'));
        
        const { getByTestId } = render(
            <div data-testid="container" className="responsive-container">
                <div className="sidebar">Sidebar</div>
                <div className="content">Content</div>
            </div>
        );
        
        const container = getByTestId('container');
        const styles = window.getComputedStyle(container);
        
        // Verificar layout móvil
        expect(styles.gridTemplateColumns).toBe('1fr');
    });
});

/* 
Explicación:
- Simulamos diferentes viewports para testing
- Disparamos eventos resize para activar media queries
- Verificamos que el layout se adapte correctamente
- Testing de responsive design automatizado
*/
```

### 9.2 Visual Regression Testing - Detectando Cambios Visuales

#### ¿Qué es Visual Regression Testing?

Visual regression testing compara capturas de pantalla de tu aplicación para detectar cambios visuales no intencionales. Es como tener un ojo que nunca se cansa revisando tu UI.

#### BackstopJS para Visual Testing

```javascript
// backstop.config.js
module.exports = {
    id: 'css-visual-tests',
    viewports: [
        {
            label: 'desktop',
            width: 1200,
            height: 800
        },
        {
            label: 'tablet',
            width: 768,
            height: 1024
        },
        {
            label: 'mobile',
            width: 375,
            height: 667
        }
    ],
    scenarios: [
        {
            label: 'Button Components',
            url: 'http://localhost:3000/components/buttons',
            selectors: ['.btn', '.btn--primary', '.btn--secondary'],
            delay: 1000
        },
        {
            label: 'Card Layout',
            url: 'http://localhost:3000/components/cards',
            selectors: ['.card', '.card--featured'],
            delay: 1000
        },
        {
            label: 'Navigation',
            url: 'http://localhost:3000/components/navigation',
            selectors: ['.nav', '.nav__item'],
            delay: 1000
        }
    ],
    paths: {
        bitmaps_reference: 'backstop_data/bitmaps_reference',
        bitmaps_test: 'backstop_data/bitmaps_test',
        html_report: 'backstop_data/html_report',
        ci_report: 'backstop_data/ci_report'
    }
};

/* 
Explicación paso a paso:
1. viewports = diferentes tamaños de pantalla para testing
2. scenarios = páginas y componentes a testear
3. selectors = elementos específicos a capturar
4. delay = tiempo de espera para que CSS se aplique
5. paths = directorios para reportes y capturas
*/
```

#### Implementación con Puppeteer

```javascript
// visual-testing.js
const puppeteer = require('puppeteer');
const fs = require('fs').promises;

class VisualTester {
    constructor() {
        this.browser = null;
        this.page = null;
    }
    
    async init() {
        this.browser = await puppeteer.launch();
        this.page = await this.browser.newPage();
    }
    
    async captureComponent(url, selector, name) {
        await this.page.goto(url);
        await this.page.waitForSelector(selector);
        
        // Esperar a que CSS se aplique
        await this.page.waitForTimeout(1000);
        
        const element = await this.page.$(selector);
        const screenshot = await element.screenshot({
            path: `screenshots/${name}.png`
        });
        
        return screenshot;
    }
    
    async compareScreenshots(baseline, current) {
        // Comparar screenshots pixel por pixel
        // Implementar lógica de comparación
        const diff = await this.calculateDiff(baseline, current);
        return diff;
    }
    
    async close() {
        if (this.browser) {
            await this.browser.close();
        }
    }
}

/* 
Explicación:
- Puppeteer = controla navegador Chrome/Chromium
- captureComponent = captura screenshot de componente específico
- compareScreenshots = compara versiones para detectar cambios
- Resultado = testing visual automatizado
*/
```

### 9.3 Testing de Accesibilidad CSS - Inclusión para Todos

#### ¿Por qué Testing de Accesibilidad CSS?

El CSS puede afectar la accesibilidad de tu aplicación. Testing de accesibilidad asegura que todos los usuarios puedan usar tu sitio web.

#### Testing con jest-axe

```javascript
// accessibility-testing.test.js
import { render } from '@testing-library/react';
import { axe, toHaveNoViolations } from 'jest-axe';

expect.extend(toHaveNoViolations);

describe('CSS Accessibility Testing', () => {
    test('button tiene contraste suficiente', async () => {
        const { container } = render(
            <button className="btn btn--primary">
                Accessible Button
            </button>
        );
        
        const results = await axe(container);
        expect(results).toHaveNoViolations();
    });
    
    test('form tiene labels accesibles', async () => {
        const { container } = render(
            <form className="form">
                <label htmlFor="email" className="form__label">
                    Email
                </label>
                <input
                    id="email"
                    type="email"
                    className="form__input"
                    required
                />
            </form>
        );
        
        const results = await axe(container);
        expect(results).toHaveNoViolations();
    });
    
    test('focus visible en elementos interactivos', async () => {
        const { container } = render(
            <div className="interactive-elements">
                <button className="btn">Button 1</button>
                <a href="#" className="link">Link 1</a>
                <input type="text" className="input" />
            </div>
        );
        
        const results = await axe(container);
        expect(results).toHaveNoViolations();
    });
});

/* 
Explicación:
- jest-axe = integra axe-core con Jest
- toHaveNoViolations = verifica que no hay violaciones de accesibilidad
- Testing de contraste, labels, focus visible
- Resultado = CSS accesible para todos los usuarios
*/
```

#### Testing de Contraste de Colores

```javascript
// contrast-testing.js
import { getContrast } from 'polished';

describe('Color Contrast Testing', () => {
    test('texto tiene contraste suficiente', () => {
        const colorPairs = [
            { background: '#ffffff', text: '#000000' },
            { background: '#007bff', text: '#ffffff' },
            { background: '#28a745', text: '#ffffff' }
        ];
        
        colorPairs.forEach(({ background, text }) => {
            const contrast = getContrast(background, text);
            
            // WCAG AA requiere 4.5:1 para texto normal
            expect(contrast).toBeGreaterThanOrEqual(4.5);
        });
    });
    
    test('texto grande tiene contraste adecuado', () => {
        const colorPairs = [
            { background: '#f8f9fa', text: '#6c757d' },
            { background: '#e9ecef', text: '#495057' }
        ];
        
        colorPairs.forEach(({ background, text }) => {
            const contrast = getContrast(background, text);
            
            // WCAG AA requiere 3:1 para texto grande
            expect(contrast).toBeGreaterThanOrEqual(3.0);
        });
    });
});

/* 
Explicación:
- polished = librería para manipulación de colores
- getContrast = calcula ratio de contraste entre colores
- WCAG AA = estándar de accesibilidad web
- Testing automático de contraste de colores
*/
```

### 9.4 Cross-Browser Testing - Compatibilidad Universal

#### ¿Por qué Cross-Browser Testing?

Diferentes navegadores pueden interpretar CSS de manera diferente. Testing cross-browser asegura que tu aplicación se vea bien en todos los navegadores.

#### BrowserStack para Testing Automatizado

```javascript
// cross-browser-testing.js
const webdriver = require('selenium-webdriver');
const { Builder, By, until } = webdriver;

class CrossBrowserTester {
    constructor() {
        this.drivers = new Map();
    }
    
    async createDriver(browser, version, platform) {
        const capabilities = {
            'bstack:options': {
                os: platform,
                osVersion: '10',
                browserVersion: version,
                projectName: 'CSS Cross Browser Testing',
                buildName: 'CSS Tests Build'
            },
            browserName: browser
        };
        
        const driver = await new Builder()
            .usingServer('https://hub-cloud.browserstack.com/wd/hub')
            .withCapabilities(capabilities)
            .build();
            
        this.drivers.set(`${browser}-${version}`, driver);
        return driver;
    }
    
    async testCSSProperty(url, selector, property, expectedValue) {
        const results = {};
        
        for (const [browserKey, driver] of this.drivers) {
            try {
                await driver.get(url);
                await driver.wait(until.elementLocated(By.css(selector)), 5000);
                
                const element = await driver.findElement(By.css(selector));
                const actualValue = await element.getCssValue(property);
                
                results[browserKey] = {
                    expected: expectedValue,
                    actual: actualValue,
                    passed: actualValue === expectedValue
                };
            } catch (error) {
                results[browserKey] = {
                    error: error.message,
                    passed: false
                };
            }
        }
        
        return results;
    }
    
    async closeAll() {
        for (const driver of this.drivers.values()) {
            await driver.quit();
        }
    }
}

/* 
Explicación:
- BrowserStack = plataforma de testing cross-browser
- Selenium WebDriver = automatiza navegadores
- testCSSProperty = verifica propiedad CSS en múltiples navegadores
- Resultado = testing de compatibilidad automatizado
*/
```

#### Testing de CSS Grid y Flexbox

```javascript
// layout-testing.js
describe('CSS Layout Cross-Browser Testing', () => {
    let tester;
    
    beforeAll(async () => {
        tester = new CrossBrowserTester();
        
        // Crear drivers para diferentes navegadores
        await tester.createDriver('Chrome', 'latest', 'Windows');
        await tester.createDriver('Firefox', 'latest', 'Windows');
        await tester.createDriver('Safari', 'latest', 'OS X');
    });
    
    afterAll(async () => {
        await tester.closeAll();
    });
    
    test('CSS Grid funciona en todos los navegadores', async () => {
        const results = await tester.testCSSProperty(
            'http://localhost:3000/grid-test',
            '.grid-container',
            'display',
            'grid'
        );
        
        // Verificar que todos los navegadores soporten Grid
        Object.entries(results).forEach(([browser, result]) => {
            expect(result.passed).toBe(true);
        });
    });
    
    test('Flexbox funciona en todos los navegadores', async () => {
        const results = await tester.testCSSProperty(
            'http://localhost:3000/flexbox-test',
            '.flex-container',
            'display',
            'flex'
        );
        
        // Verificar que todos los navegadores soporten Flexbox
        Object.entries(results).forEach(([browser, result]) => {
            expect(result.passed).toBe(true);
        });
    });
});

/* 
Explicación:
- Testing de CSS Grid y Flexbox en múltiples navegadores
- Verificación de propiedades CSS críticas
- Detección de problemas de compatibilidad
- Testing automatizado de layouts
*/
```

### 9.5 Debugging Avanzado de CSS - Resolviendo Problemas Complejos

#### Chrome DevTools - Inspector Avanzado

```javascript
// debugging-tools.js
class CSSDebugger {
    constructor() {
        this.breakpoints = new Set();
        this.observers = new Map();
    }
    
    // Agregar breakpoint en CSS
    addCSSBreakpoint(selector, property) {
        const style = document.createElement('style');
        style.textContent = `
            ${selector} {
                ${property}: breakpoint !important;
            }
        `;
        
        document.head.appendChild(style);
        this.breakpoints.add(style);
        
        console.log(`CSS Breakpoint agregado: ${selector} { ${property} }`);
    }
    
    // Remover breakpoint
    removeCSSBreakpoint(style) {
        if (this.breakpoints.has(style)) {
            document.head.removeChild(style);
            this.breakpoints.delete(style);
            console.log('CSS Breakpoint removido');
        }
    }
    
    // Observar cambios en propiedades CSS
    observeCSSProperty(element, property, callback) {
        const observer = new MutationObserver((mutations) => {
            mutations.forEach((mutation) => {
                if (mutation.type === 'attributes' && 
                    mutation.attributeName === 'style') {
                    const newValue = element.style[property];
                    callback(newValue, element);
                }
            });
        });
        
        observer.observe(element, {
            attributes: true,
            attributeFilter: ['style']
        });
        
        this.observers.set(element, observer);
    }
    
    // Detener observación
    stopObserving(element) {
        const observer = this.observers.get(element);
        if (observer) {
            observer.disconnect();
            this.observers.delete(element);
        }
    }
}

/* 
Explicación:
- addCSSBreakpoint = agrega breakpoint visual en CSS
- observeCSSProperty = observa cambios en propiedades CSS
- MutationObserver = detecta cambios en atributos del DOM
- Herramientas para debugging avanzado de CSS
*/
```

#### Debugging de Layout Issues

```javascript
// layout-debugging.js
class LayoutDebugger {
    constructor() {
        this.debugMode = false;
        this.debugStyles = null;
    }
    
    // Activar modo debug de layout
    enableLayoutDebug() {
        if (this.debugMode) return;
        
        this.debugStyles = document.createElement('style');
        this.debugStyles.textContent = `
            * {
                outline: 1px solid red !important;
                background-color: rgba(255, 0, 0, 0.1) !important;
            }
            
            *:hover {
                outline: 2px solid blue !important;
                background-color: rgba(0, 0, 255, 0.2) !important;
            }
            
            .grid-container * {
                outline: 1px solid green !important;
                background-color: rgba(0, 255, 0, 0.1) !important;
            }
            
            .flex-container * {
                outline: 1px solid orange !important;
                background-color: rgba(255, 165, 0, 0.1) !important;
            }
        `;
        
        document.head.appendChild(this.debugStyles);
        this.debugMode = true;
        
        console.log('Layout Debug Mode activado');
    }
    
    // Desactivar modo debug
    disableLayoutDebug() {
        if (!this.debugMode) return;
        
        if (this.debugStyles) {
            document.head.removeChild(this.debugStyles);
            this.debugStyles = null;
        }
        
        this.debugMode = false;
        console.log('Layout Debug Mode desactivado');
    }
    
    // Mostrar información de layout
    showLayoutInfo(element) {
        const styles = window.getComputedStyle(element);
        const rect = element.getBoundingClientRect();
        
        const layoutInfo = {
            display: styles.display,
            position: styles.position,
            top: styles.top,
            left: styles.left,
            width: rect.width,
            height: rect.height,
            margin: styles.margin,
            padding: styles.padding,
            border: styles.border
        };
        
        console.log('Layout Info:', layoutInfo);
        return layoutInfo;
    }
}

/* 
Explicación:
- enableLayoutDebug = activa visualización de layout
- Colores diferentes para Grid, Flexbox y elementos normales
- showLayoutInfo = muestra información detallada de layout
- Herramientas para debugging visual de CSS
*/
```

### 9.6 Testing de Performance CSS - Métricas de Rendimiento

#### Testing de Core Web Vitals

```javascript
// performance-testing.js
class CSSPerformanceTester {
    constructor() {
        this.metrics = {};
    }
    
    // Medir Largest Contentful Paint (LCP)
    async measureLCP() {
        return new Promise((resolve) => {
            const observer = new PerformanceObserver((list) => {
                const entries = list.getEntries();
                const lastEntry = entries[entries.length - 1];
                
                this.metrics.lcp = lastEntry.startTime;
                resolve(lastEntry.startTime);
            });
            
            observer.observe({ entryTypes: ['largest-contentful-paint'] });
        });
    }
    
    // Medir First Input Delay (FID)
    async measureFID() {
        return new Promise((resolve) => {
            const observer = new PerformanceObserver((list) => {
                const entries = list.getEntries();
                const firstEntry = entries[0];
                
                this.metrics.fid = firstEntry.processingStart - firstEntry.startTime;
                resolve(this.metrics.fid);
            });
            
            observer.observe({ entryTypes: ['first-input'] });
        });
    }
    
    // Medir Cumulative Layout Shift (CLS)
    async measureCLS() {
        return new Promise((resolve) => {
            let clsValue = 0;
            let clsEntries = [];
            
            const observer = new PerformanceObserver((list) => {
                for (const entry of list.getEntries()) {
                    if (!entry.hadRecentInput) {
                        clsValue += entry.value;
                        clsEntries.push(entry);
                    }
                }
                
                this.metrics.cls = clsValue;
                resolve(clsValue);
            });
            
            observer.observe({ entryTypes: ['layout-shift'] });
        });
    }
    
    // Medir CSS parsing time
    measureCSSParsingTime() {
        const navigation = performance.getEntriesByType('navigation')[0];
        const cssStart = navigation.responseStart;
        const cssEnd = navigation.loadEventEnd;
        
        this.metrics.cssParsingTime = cssEnd - cssStart;
        return this.metrics.cssParsingTime;
    }
    
    // Obtener métricas completas
    getMetrics() {
        return this.metrics;
    }
}

/* 
Explicación:
- Core Web Vitals = métricas de performance web de Google
- LCP = tiempo para renderizar contenido principal
- FID = tiempo de respuesta a primera interacción
- CLS = estabilidad visual del layout
- Testing automatizado de performance CSS
*/
```

### 9.7 Testing de Animaciones CSS - Suavidad y Performance

#### Testing de Frame Rate

```javascript
// animation-testing.js
class AnimationTester {
    constructor() {
        this.frameCount = 0;
        this.lastTime = performance.now();
        this.fps = 0;
    }
    
    // Medir FPS de animaciones
    startFPSCounter() {
        const measureFPS = () => {
            this.frameCount++;
            const currentTime = performance.now();
            
            if (currentTime - this.lastTime >= 1000) {
                this.fps = this.frameCount;
                this.frameCount = 0;
                this.lastTime = currentTime;
                
                console.log(`FPS: ${this.fps}`);
                
                // Verificar que FPS sea aceptable
                if (this.fps < 30) {
                    console.warn('FPS bajo detectado. Considera optimizar animaciones.');
                }
            }
            
            requestAnimationFrame(measureFPS);
        };
        
        requestAnimationFrame(measureFPS);
    }
    
    // Test de animación específica
    testAnimation(element, animationClass) {
        return new Promise((resolve) => {
            const startTime = performance.now();
            let animationEnd = false;
            
            element.classList.add(animationClass);
            
            const checkAnimationEnd = () => {
                if (!animationEnd) {
                    const computedStyle = window.getComputedStyle(element);
                    const animationState = computedStyle.animationPlayState;
                    
                    if (animationState === 'running') {
                        requestAnimationFrame(checkAnimationEnd);
                    } else {
                        animationEnd = true;
                        const endTime = performance.now();
                        const duration = endTime - startTime;
                        
                        resolve({
                            duration,
                            success: true
                        });
                    }
                }
            };
            
            requestAnimationFrame(checkAnimationEnd);
        });
    }
    
    // Test de performance de transformaciones
    testTransformPerformance(element, iterations = 1000) {
        const startTime = performance.now();
        
        for (let i = 0; i < iterations; i++) {
            element.style.transform = `translateX(${i}px) rotate(${i}deg)`;
        }
        
        const endTime = performance.now();
        const totalTime = endTime - startTime;
        const avgTime = totalTime / iterations;
        
        return {
            totalTime,
            avgTime,
            iterations
        };
    }
}

/* 
Explicación:
- startFPSCounter = mide frames por segundo en tiempo real
- testAnimation = testea animación específica
- testTransformPerformance = mide performance de transformaciones
- Testing de animaciones CSS para performance
*/
```

## 🧪 Ejercicios Prácticos

### **Ejercicio 1: Testing Automatizado de Componentes**
Implementa testing automatizado para componentes CSS.

**Instrucciones paso a paso:**
1. **Configura Jest** con testing-library
2. **Crea tests** para botones, cards, formularios
3. **Verifica estilos** computados y clases
4. **Implementa testing** de responsive design
5. **Mide cobertura** de testing

**Requisitos:**
- Tests automatizados funcionando
- Verificación de estilos CSS
- Testing de responsive design
- Cobertura de testing medida

### **Ejercicio 2: Visual Regression Testing**
Implementa visual regression testing con BackstopJS.

**Instrucciones paso a paso:**
1. **Configura BackstopJS** en tu proyecto
2. **Define escenarios** para componentes clave
3. **Configura viewports** para responsive testing
4. **Ejecuta tests** y analiza resultados
5. **Integra en CI/CD** pipeline

**Requisitos:**
- BackstopJS configurado
- Escenarios de testing definidos
- Testing responsive implementado
- Integración CI/CD configurada

### **Ejercicio 3: Testing de Accesibilidad**
Implementa testing de accesibilidad para CSS.

**Instrucciones paso a paso:**
1. **Configura jest-axe** para testing
2. **Crea tests** para contraste de colores
3. **Verifica focus** visible y navegación
4. **Testea labels** y formularios
5. **Mide compliance** de accesibilidad

**Requisitos:**
- jest-axe configurado
- Tests de accesibilidad implementados
- Verificación de contraste
- Compliance de accesibilidad medido

### **Ejercicio 4: Cross-Browser Testing**
Implementa testing cross-browser para CSS.

**Instrucciones paso a paso:**
1. **Configura BrowserStack** o similar
2. **Crea tests** para diferentes navegadores
3. **Verifica compatibilidad** de CSS Grid/Flexbox
4. **Testea media queries** y responsive
5. **Documenta diferencias** entre navegadores

**Requisitos:**
- Cross-browser testing configurado
- Tests en múltiples navegadores
- Compatibilidad verificada
- Diferencias documentadas

### **Ejercicio 5: Debugging Avanzado**
Implementa herramientas de debugging CSS.

**Instrucciones paso a paso:**
1. **Crea CSSDebugger** personalizado
2. **Implementa breakpoints** CSS
3. **Crea LayoutDebugger** visual
4. **Implementa observadores** de propiedades
5. **Documenta herramientas** de debugging

**Requisitos:**
- Herramientas de debugging implementadas
- Breakpoints CSS funcionales
- Debugging visual de layout
- Observadores de propiedades CSS

### **Ejercicio 6: Testing de Performance**
Implementa testing de performance CSS.

**Instrucciones paso a paso:**
1. **Configura CSSPerformanceTester**
2. **Mide Core Web Vitals**
3. **Implementa testing** de FPS
4. **Testea performance** de animaciones
5. **Optimiza basado** en métricas

**Requisitos:**
- Testing de performance implementado
- Core Web Vitals medidos
- FPS y animaciones testeados
- Optimizaciones implementadas

### **Ejercicio 7: Testing de Animaciones**
Implementa testing específico para animaciones CSS.

**Instrucciones paso a paso:**
1. **Configura AnimationTester**
2. **Mide FPS** en tiempo real
3. **Testea animaciones** específicas
4. **Mide performance** de transformaciones
5. **Optimiza animaciones** problemáticas

**Requisitos:**
- Testing de animaciones implementado
- FPS medido en tiempo real
- Performance de transformaciones medida
- Animaciones optimizadas

### **Ejercicio 8: Testing de Layout**
Implementa testing específico para layouts CSS.

**Instrucciones paso a paso:**
1. **Crea tests** para CSS Grid
2. **Implementa testing** para Flexbox
3. **Verifica responsive** breakpoints
4. **Testea container queries**
5. **Mide estabilidad** de layout

**Requisitos:**
- Testing de Grid implementado
- Testing de Flexbox implementado
- Responsive testing funcional
- Estabilidad de layout medida

### **Ejercicio 9: Testing de Variables CSS**
Implementa testing para variables CSS.

**Instrucciones paso a paso:**
1. **Crea tests** para variables CSS
2. **Verifica fallbacks** y valores por defecto
3. **Testea temas** claro/oscuro
4. **Verifica cascada** de variables
5. **Mide performance** de variables

**Requisitos:**
- Testing de variables implementado
- Fallbacks verificados
- Temas testeados
- Performance de variables medida

### **Ejercicio 10: Proyecto de Testing Completo**
Crea un proyecto que demuestre todas las técnicas de testing.

**Instrucciones paso a paso:**
1. **Planifica estrategia** de testing
2. **Implementa testing** automatizado
3. **Configura visual regression** testing
4. **Implementa testing** de accesibilidad
5. **Configura testing** cross-browser

**Requisitos:**
- Todas las técnicas implementadas
- Testing automatizado funcional
- Cobertura de testing alta
- CI/CD configurado

## 🎯 Proyecto Integrador: Sistema de Testing CSS Completo

### Descripción del Proyecto
Crea un sistema de testing CSS completo que demuestre dominio de todas las técnicas de testing y debugging aprendidas.

### Requisitos del Proyecto

#### **Testing Automatizado (25%)**
- Jest configurado con testing-library
- Tests para componentes CSS
- Testing de responsive design
- Cobertura de testing alta

#### **Visual Regression Testing (20%)**
- BackstopJS configurado
- Escenarios de testing definidos
- Testing responsive implementado
- Reportes automáticos

#### **Testing de Accesibilidad (20%)**
- jest-axe implementado
- Tests de contraste y focus
- Compliance de accesibilidad
- Reportes de accesibilidad

#### **Cross-Browser Testing (20%)**
- Testing en múltiples navegadores
- Compatibilidad verificada
- Diferencias documentadas
- Testing automatizado

#### **Herramientas de Debugging (15%)**
- CSSDebugger implementado
- LayoutDebugger funcional
- Observadores de propiedades
- Herramientas documentadas

### Entregables
1. **Sistema de testing completo** implementado
2. **Tests automatizados** para todos los componentes
3. **Visual regression testing** configurado
4. **Testing de accesibilidad** implementado
5. **Herramientas de debugging** funcionales

### Criterios de Evaluación
- **Testing**: Sistema completo y funcional
- **Cobertura**: Alta cobertura de testing
- **Accesibilidad**: Compliance verificado
- **Cross-browser**: Compatibilidad asegurada
- **Debugging**: Herramientas útiles y funcionales

## 📚 Recursos Adicionales

### Documentación
- [Jest CSS Testing](https://jestjs.io/docs/getting-started)
- [BackstopJS](https://github.com/garris/BackstopJS)
- [jest-axe](https://github.com/nickcolley/jest-axe)
- [CSS Testing Best Practices](https://css-tricks.com/testing-css/)

### Herramientas
- [Jest](https://jestjs.io/) - Framework de testing
- [BackstopJS](https://backstopjs.com/) - Visual regression testing
- [BrowserStack](https://www.browserstack.com/) - Cross-browser testing
- [axe-core](https://github.com/dequelabs/axe-core) - Testing de accesibilidad

### Práctica
- [CSS Testing Strategies](https://web.dev/css-testing/)
- [Visual Regression Testing](https://css-tricks.com/visual-regression-testing/)
- [CSS Performance Testing](https://web.dev/css-performance-testing/)
- [Cross-Browser CSS Testing](https://css-tricks.com/cross-browser-css-testing/)

## 🔍 Preguntas de Repaso

1. **¿Por qué es importante testing CSS automatizado?**
2. **¿Cómo funciona visual regression testing?**
3. **¿Qué métricas de accesibilidad son importantes?**
4. **¿Cómo implementar testing cross-browser?**
5. **¿Qué herramientas usar para debugging CSS?**
6. **¿Cómo medir performance de CSS?**
7. **¿Qué son Core Web Vitals?**
8. **¿Cómo testear animaciones CSS?**
9. **¿Qué es testing de layout?**
10. **¿Cómo crear un sistema de testing completo?**

## 🚀 Siguiente Paso

Una vez que hayas completado este módulo y el proyecto integrador, estarás listo para continuar con el **Módulo 10: DevOps y Deployment CSS**, donde aprenderás técnicas de CI/CD, deployment y mantenimiento de CSS en producción.

---

**¡Excelente trabajo! Ahora dominas las técnicas de testing y debugging CSS más avanzadas.** 🎉

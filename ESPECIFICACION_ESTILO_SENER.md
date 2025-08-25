# 📋 Especificación de Estilo - Geovisor SENER

## Guía de Diseño Institucional para Homologación de Prototipos

---

## 🎨 **PALETA DE COLORES INSTITUCIONAL**

### Colores Primarios

```css
--color-burdeos-oscuro: #35031B;     /* Texto principal */
--color-burdeos-medio: #601623;      /* Elementos destacados */
--color-verde-profundo: #20705B;     /* Acciones primarias */
--color-verde-marino: #1F7A62;       /* Gradientes */
--color-magenta-oscuro: #7E1D37;     /* Elementos críticos */
```

### Colores Secundarios

```css
--color-rosa-palido: #EFD2DC;        /* Fondos suaves */
--color-aqua-claro: #95E5E0;         /* Acentos claros */
--color-mostaza-amarillo: #C69A04;   /* Advertencias */
--color-rojo-vivo: #E24849;          /* Errores/Cerrar */
--color-amarillo-claro: #FEC747;     /* Hover states */
```

### Colores de Estado

```css
--estado-operativo: #20705B;         /* Verde profundo */
--estado-mantenimiento: #C69A04;     /* Mostaza */
--estado-fuera-servicio: #E24849;    /* Rojo vivo */
--estado-construccion: #1F7A62;      /* Verde marino */
```

---

## 🔤 **TIPOGRAFÍA**

### Fuente Principal

```css
font-family: 'Montserrat', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
```

### Jerarquía Tipográfica

```css
/* Títulos Principales */
h1: font-size: 2.25rem; font-weight: 700; (Desktop)
h1: font-size: 1.1rem; font-weight: 700; (Mobile)

/* Subtítulos */
h2: font-size: 1.5rem; font-weight: 600;
h3: font-size: 1.25rem; font-weight: 600;

/* Texto Cuerpo */
body: font-size: 1rem; font-weight: 400; line-height: 1.6;
small: font-size: 0.875rem; font-weight: 400;

/* Elementos UI */
.btn: font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px;
.navbar-title: text-transform: uppercase; letter-spacing: 0.5px;
```

---

## 🏛️ **HEADER/NAVBAR INSTITUCIONAL**

### Estructura Desktop

```html
<nav class="institutional-navbar">
  <div class="container-fluid">
    <div class="row align-items-center w-100">
      <div class="col-md-3"><!-- Logo SENER --></div>
      <div class="col-md-6"><!-- Título Central --></div>
      <div class="col-md-3"><!-- Logo Gobierno --></div>
    </div>
  </div>
</nav>
```

### Estilos del Navbar

```css
.institutional-navbar {
  background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
  border-bottom: 4px solid var(--color-burdeos-medio);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  padding: 1rem 0;
  position: sticky;
  top: 0;
  z-index: 1030;
}

/* Logos */
.sener-logo, .gob-logo {
  height: 60px; /* Desktop */
  height: 40px; /* Tablet */
  display: none; /* Mobile */
  transition: transform 0.3s ease;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.1));
}

/* Títulos */
.navbar-title {
  font-size: 1.5rem; /* Desktop */
  font-size: 1.1rem; /* Mobile */
  font-weight: 700;
  color: var(--color-burdeos-oscuro);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.navbar-subtitle {
  font-size: 0.9rem; /* Desktop */
  font-size: 0.8rem; /* Mobile */
  font-weight: 500;
  color: var(--color-verde-profundo);
  text-transform: capitalize;
}
```

### Responsive Behavior

- **Desktop (>768px)**: Logo + Título + Logo
- **Tablet (≤768px)**: logo + Título + logo (reducidos)
- **Mobile (≤576px)**: Título centrado (logos ocultos)

---

## ⏳ **PRELOADER**

### Estructura

```html
<div id="preloader" class="d-flex flex-column align-items-center justify-content-center">
  <div class="text-center">
    <img src="img/mujer.png" alt="SENER" style="max-width: 10rem;">
    <h3 class="fw-bold">Subsecretaría de Planeación y Transición Energética</h3>
    <p class="text-muted fs-5">Cargando datos y capas...</p>
    <div class="spinner-border text-main-color"></div>
    <div class="progress">
      <div id="preProgressBar" class="progress-bar"></div>
    </div>
  </div>
</div>
```

### Estilos del Preloader

```css
#preloader {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100vh;
  background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
  z-index: 10000;
  backdrop-filter: blur(10px);
}

#preloader img {
  animation: pulse 2s ease-in-out infinite;
}

#preloader h3 {
  font-weight: 700;
  color: var(--color-burdeos-oscuro);
  margin-bottom: 0.5rem;
}

#preloader p {
  color: var(--color-verde-profundo);
  font-weight: 500;
}

.progress-bar {
  background: linear-gradient(90deg, 
    var(--color-verde-profundo) 0%, 
    var(--color-verde-marino) 50%, 
    var(--color-aqua-medio) 100%);
  border-radius: 10px;
  transition: width 0.3s ease;
}
```

---

## 🗺️ **MAPAS Y CONTROLES**

### Configuración de Mapas Base

```javascript
const baseMaps = {
  'SENER Azul': MapaPersonalizado,
  'SENER Light': MapaClaro,
  'SENER Oscuro': MapaOscuro
};
```

### Uso de `mapa.js` (para ejemplos)

Si quieres una forma simple y reutilizable de añadir un mapa de ejemplo en las páginas, usa el archivo `mapa.js` incluido en la plantilla. `mapa.js` expone una API global `MAPA` con funciones:

**API Principal:**
- `MAPA.init(options)` -> inicializa y devuelve un objeto `L.Map` con basemaps personalizados de SENER.
  - **options**: { container, center, zoom, includeBasemapControl, restrictToMexico }
- `MAPA.addGeoJson(map, geojson, options)` -> añade y retorna una capa GeoJSON al mapa.
- `MAPA.centerToMexico(map)` -> centra el mapa en los límites de México.

**Basemaps incluidos (automáticos):**
- 'SENER Azul' - Mapa personalizado con style ID `0198a42c-5e08-77a1-9773-763ee4e12b32`
- 'SENER Light' - Mapa claro con style ID `0198a9af-dc7c-79d3-8316-a80767ad1d0f`
- 'SENER Oscuro' - Mapa oscuro con style ID `0198a9f0-f135-7991-aaec-bea71681556e`
- 'Satelital' - Google Satellite como fallback

**Configuración automática:**
- **Límites de México**: Restringe navegación a coordenadas [14.0, -118.0] a [33.5, -86.0]
- **Zoom máximo**: 18 (100% de detalle)
- **Zoom mínimo**: 4 (evita alejarse demasiado de México)
- **Control de basemaps**: Selector en esquina superior derecha

**Ejemplo completo para IA/agentes:**

```html
<!-- 1. Incluir dependencias en el HEAD -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
    integrity="sha256-p4NxAoJBhIIN+hmNHrzRCf9tD/miZyoHS5obTRR9BMY=" crossorigin="" />
<!-- MapTiler SDK CSS (Opcional pero recomendado para mapas vectoriales) -->
<link href="https://cdn.maptiler.com/leaflet-maptilersdk/v2.0.3/leaflet-maptilersdk.css" rel="stylesheet" />

<!-- 2. Contenedor del mapa -->
<div class="position-relative" style="height: 400px;">
    <div id="map" style="height:100%; border:1px solid #ddd; border-radius:8px;"></div>
    <button id="center-map-btn" class="btn btn-light" style="position:absolute; left:12px; bottom:12px; z-index:999">Centrar</button>
</div>

<!-- 3. Scripts al final del BODY -->
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"
    integrity="sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=" crossorigin=""></script>
<!-- MapTiler SDK JS (Opcional pero recomendado para mapas vectoriales) -->
<script src="https://cdn.maptiler.com/leaflet-maptilersdk/v2.0.3/leaflet-maptilersdk.js"></script>
<script src="mapa.js"></script>
<script>
document.addEventListener('DOMContentLoaded', function () {
    setTimeout(function() {
        // Inicializar mapa con configuración completa
        const map = MAPA.init({ 
            container: 'map', 
            center: [23.6, -102.5], 
            zoom: 5,
            includeBasemapControl: true,  // Control de basemaps
            restrictToMexico: true        // Límites de México
        });
        
        // Conectar botón de centrar
        const centerBtn = document.getElementById('center-map-btn');
        if (centerBtn && map) {
            centerBtn.addEventListener('click', () => {
                MAPA.centerToMexico(map);
            });
        }

        // Verificar si el SDK de MapTiler se cargó correctamente
        if (typeof L.maptiler === 'undefined') {
            console.warn('Advertencia: El SDK de MapTiler no se cargó. Los mapas se mostrarán como imágenes (raster) en lugar de vectores.');
        }

    }, 100);
});
</script>
```

**Variables importantes para IA:**
- **API Keys**: Configuradas en `mapa.js` (líneas 3-6)
- **Style IDs**: Configurados en `createBasemaps()` en `mapa.js`
- **Límites México**: `[14.0, -118.0]` a `[33.5, -86.0]` (en `mapa.js`)

**Recomendación**: En proyectos reales centraliza las keys en variables de entorno o en un sistema de secretos. `mapa.js` está pensado para ejemplos y prototipos con configuración consistente de SENER.

### Estilos de Controles de Leaflet

```css
/* Control de Capas */
.leaflet-control-layers {
  background: rgba(255, 255, 255, 0.98);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.4);
  border-radius: 16px;
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
  padding: 20px;
  min-width: 280px;
}

/* Control de Zoom */
.leaflet-control-zoom a {
  background: rgba(255, 255, 255, 0.98);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.4);
  color: var(--color-verde-profundo);
  font-weight: bold;
  width: 44px; height: 44px;
  border-radius: 12px;
  transition: all 0.3s ease;
}

.leaflet-control-zoom a:hover {
  background: var(--color-verde-profundo);
  color: white;
  transform: scale(1.05);
}

/* Botón Centrar Mapa */
#center-map-btn {
  position: absolute;
  bottom: 30px; left: 10px;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(32, 112, 91, 0.3);
  color: var(--color-verde-profundo);
  border-radius: 8px;
  padding: 8px 12px;
  font-weight: 600;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  transition: all 0.3s ease;
}
```

### Popups Elegantes

```css
.leaflet-popup-content-wrapper {
  background: white;
  backdrop-filter: blur(15px);
  border: 1px solid rgba(32, 112, 91, 0.3);
  border-radius: 12px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12), 
              0 2px 8px rgba(32, 112, 91, 0.08);
  overflow: hidden;
}

/* Encabezado del Popup */
.leaflet-popup-content h6 {
  background: linear-gradient(135deg, var(--color-verde-profundo), var(--color-verde-marino));
  color: white;
  margin: -20px -20px 15px -20px;
  padding: 15px 20px;
  border-radius: 12px 12px 0 0;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

/* Botón Cerrar */
.leaflet-popup-close-button {
  background: rgba(220, 53, 69, 0.85);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.4);
  border-radius: 50%;
  width: 28px; height: 28px;
  transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
}

.leaflet-popup-close-button:hover {
  background: rgba(220, 53, 69, 1);
  transform: scale(1.1) rotate(90deg);
  box-shadow: 0 4px 16px rgba(220, 53, 69, 0.5);
}
```

---

## 📊 **CARDS Y COMPONENTES**

### Cards de Totales

```css
#total-cards-container .card {
  border: 1px solid rgba(0, 0, 0, 0.08);
  border-radius: 16px;
  box-shadow: 0 8px 24px -8px rgba(0, 0, 0, 0.15);
  background: white;
  transition: all 0.3s ease;
  overflow: hidden;
}

#total-cards-container .card:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 32px -8px rgba(0, 0, 0, 0.2);
}

/* Títulos de Cards */
.card-title {
  font-weight: 700;
  font-size: 0.65rem;
  letter-spacing: 0.8px;
  text-transform: uppercase;
  line-height: 1.2;
}

/* Números de Cards */
.card-text {
  font-weight: 800;
  font-size: 1.4rem;
  font-variant-numeric: tabular-nums;
}
```

### Switches de Capas

```css
.form-check-input:checked {
  background-color: var(--color-verde-profundo);
  border-color: var(--color-verde-profundo);
  box-shadow: 0 0 0 0.2rem rgba(32, 112, 91, 0.25);
}

.form-check-input:focus {
  border-color: var(--color-verde-marino);
  box-shadow: 0 0 0 0.2rem rgba(32, 112, 91, 0.25);
}
```

---

## 🦶 **FOOTER INSTITUCIONAL**

### Estructura

```html
<footer class="main-footer">
  <div class="container">
    <div class="row">
      <div class="col-lg-8">
        <!-- Enlaces y contenido -->
      </div>
      <div class="col-lg-4">
        <img src="img/logo_gob.png" alt="Gobierno de México" class="footer-logo">
      </div>
    </div>
  </div>
</footer>
```

### Estilos del Footer

```css
.main-footer {
  background: linear-gradient(45deg, var(--color-verde-profundo-oscuro), var(--color-verde-petroleo));
  color: var(--color-rosa-palido);
  padding: 3rem 0;
  font-size: 0.9rem;
  margin-top: 3rem;
  border-top: 4px solid var(--color-verde-profundo);
}

.main-footer h5 {
  font-weight: 700;
  font-size: 1.1rem;
  color: var(--color-aqua-claro);
}

.main-footer a {
  color: var(--color-rosa-palido);
  text-decoration: none;
  transition: color 0.3s ease;
}

.main-footer a:hover {
  color: var(--color-amarillo-claro);
}

/* Logo del Footer */
.main-footer img {
  filter: brightness(0) invert(1);
  transition: filter 0.3s ease;
}

.main-footer img:hover {
  filter: brightness(0) invert(1) drop-shadow(0 0 8px rgba(255, 255, 255, 0.3));
}
```

---

## 📱 **RESPONSIVE DESIGN**

### Breakpoints

```css
/* Mobile First Approach */
/* Mobile: 0-576px */
/* Tablet: 577-768px */
/* Desktop: 769px+ */

@media (max-width: 576px) {
  /* Ocultar logos */
  .sener-logo, .gob-logo { display: none !important; }
  
  /* Títulos centrados */
  .navbar-title { font-size: 1.1rem; text-align: center; }
  
  /* Cards en scroll horizontal */
  #total-cards-container { 
    flex-wrap: nowrap !important;
    overflow-x: auto;
  }
  
  /* Popups más pequeños */
  .leaflet-popup-content { max-width: 280px !important; }
}

@media (max-width: 768px) {
  /* Logos reducidos */
  .sener-logo, .gob-logo { height: 40px; opacity: 0.8; }
  
  /* Footer centrado */
  .main-footer { text-align: center; }
}
```

### Principios Mobile

1. **Logos ocultos** en pantallas pequeñas
2. **Contenido centrado** y legible
3. **Botones táctiles** mínimo 44px
4. **Scroll horizontal** para cards cuando sea necesario
5. **Popups adaptados** a pantalla disponible

---

## 🎨 **EFECTOS VISUALES**

### Glassmorphism

```css
.glass-effect {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  border: 1px solid rgba(255, 255, 255, 0.4);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}
```

### Transiciones Estándar

```css
.smooth-transition {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.hover-scale:hover {
  transform: scale(1.05);
}

.hover-lift:hover {
  transform: translateY(-2px);
}
```

### Animaciones

```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.7; transform: scale(1.05); }
}

.fade-in { animation: fadeInUp 0.5s ease-out; }
.pulse-effect { animation: pulse 2s infinite; }
```

---

## 🔧 **COMPONENTES REUTILIZABLES**

### Botones Institucionales

```css
.btn-sener-primary {
  background: var(--color-verde-profundo);
  border-color: var(--color-verde-profundo);
  color: white;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  border-radius: 8px;
  padding: 8px 16px;
  transition: all 0.3s ease;
}

.btn-sener-primary:hover {
  background: var(--color-verde-marino);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(32, 112, 91, 0.3);
}
```

### Notificaciones

```css
.notification {
  position: fixed;
  top: 20px; right: 20px;
  z-index: 2000;
  max-width: 350px;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.3);
  border-radius: 8px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  animation: slideInRight 0.3s ease-out;
}
```

---

## 📋 **CHECKLIST DE IMPLEMENTACIÓN**

### ✅ Elementos Obligatorios

- [ ] Paleta de colores institucional implementada
- [ ] Fuente Montserrat cargada
- [ ] Navbar con logos y responsive
- [ ] Preloader con imagen institucional
- [ ] Footer estilo gob.mx
- [ ] Controles de mapa con glassmorphism
- [ ] Popups elegantes con encabezado verde
- [ ] Cards con hover effects
- [ ] Responsive mobile-first

### ✅ Elementos Opcionales

- [X] Animaciones de entrada
- [X] Efectos de hover avanzados
- [X] Notificaciones toast
- [X] Clusters personalizados
- [X] Sincronización bidireccional

---

## 🎯 **NOTAS DE IMPLEMENTACIÓN**

1. **Siempre usar variables CSS** para colores institucionales
2. **Mobile-first approach** en todos los componentes
3. **Glassmorphism** para elementos flotantes (controles, popups)
4. **Transiciones suaves** en todas las interacciones
5. **Logos ocultos en móvil** para mejor UX
6. **Colores de estado** consistentes en toda la aplicación
7. **Tipografía jerárquica** clara y legible
8. **Accesibilidad** con tamaños táctiles apropiados

---

*Esta especificación debe ser la base para todos los prototipos de SENER, garantizando consistencia visual y funcional en todos los proyectos.*

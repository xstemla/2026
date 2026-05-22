Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: Colectivo-Tracker

## FUNCIONALIDAD PRINCIPAL

Detectar automáticamente cuando una persona sube a un colectivo (GPS + IA) y mostrar su ubicación en un mapa para que sus compañeros la vean en tiempo real.

---
## RESTRICCIONES (OBLIGATORIO RESPETAR)
- NO usar backend propio
- NO usar Firebase
- NO usar Redux, NO usar Zustand
- NO agregar autenticación real
- NO agregar funcionalidades fuera del MVP
- Mantener arquitectura simple
- Priorizar estabilidad sobre features
---
## ARQUITECTURA (DESACOPLADO)
- `useGPS`: toda la lógica de geolocalización
- `useColectivoMachine`: toda la máquina de estados
- `useSimulacion`: toda la lógica de simulación
- Los componentes (Speedometer, EventLog, Mapa) deben ser presentacionales
- Recibir datos por props, no tener lógica interna compleja
---
## DEFINICIONES EXACTAS
- **QUIETO**: promedio últimas 3 lecturas GPS < 1 km/h
- **MOVIMIENTO**: promedio últimas 3 lecturas GPS > 5 km/h
- **ARRANQUE SOSTENIDO**: MOVIMIENTO durante 10 segundos consecutivos
- **SEMÁFORO**: quieto en VIAJE_ACTIVO por menos de 90 segundos
- **BAJADA**: quieto por más de 120 segundos consecutivos
---
## LOGS OBLIGATORIOS (para debugging)
Cada uno de estos eventos debe registrarse en el EventLog con timestamp:
- 📍 GPS recibido: X km/h
- 🔄 Cambio de estado: ESPERANDO → ALERTA
- 🤖 Consultando IA...
- 🤖 IA respondió: COLECTIVO / SEMAFORO
- 💾 Supabase: insert / update / error
- 🧪 Simulación activada / desactivada
- ⚠️ Error: (descripción)
- 🚦 Semáforo detectado
- 🔁 Reset por bajada
---
## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Login, Tracker, Mapa)

### FASE 2 - Login
- Campos: nombre, código (validar "COLECTIVO2024")
- Guardar en localStorage

### FASE 3 - GPS + Velocímetro
- `useGPS` con watchPosition (enableHighAccuracy: true)
- Promediar últimas 3 lecturas
- **FALLBACK**: si coords.speed es null, calcular velocidad con distancia entre coordenadas / tiempo
- Velocímetro circular SVG (componente presentacional)

### FASE 4 - Máquina de estados
- ESPERANDO → ALERTA (quieto >3s) → VERIFICANDO (arranque 10s) → VIAJE_ACTIVO
- VIAJE_ACTIVO → SEMAFORO (quieto >5s, espera 90s)
- SEMAFORO → RESETEANDO (quieto 90s)
- RESETEANDO → ESPERANDO

### FASE 5 - Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Prompt: "¿COLECTIVO o SEMAFORO?" (responder solo una palabra)
- Timeout 3 segundos

### FASE 6 - Supabase + Realtime
- Tabla "viajes": id, nombre, lat, lng, velocidad, estado (activo/inactivo), updated_at
- VIAJE_ACTIVO → INSERT con estado='activo'
- Actualizar cada 10 segundos → UPDATE
- RESETEANDO → UPDATE estado='inactivo'
- Mapa SOLO muestra: estado='activo' AND updated_at > NOW() - INTERVAL '60 seconds'

### FASE 7 - Mapa con Leaflet
- Importar CSS de Leaflet
- Altura del mapa: h-[70vh]
- Suscribirse a Realtime
- Popup con nombre, velocidad, última actualización

### FASE 8 - Modo simulación
- 5 taps en el título activa panel
- Slider de velocidad manual
- Badge rojo "SIMULACIÓN"
- Ignorar GPS real cuando activo
---
## SUPABASE (esquema)
```sql
CREATE TABLE viajes (
 id SERIAL PRIMARY KEY,
 nombre_usuario TEXT NOT NULL,
 lat FLOAT NOT NULL,
 lng FLOAT NOT NULL,
 velocidad FLOAT NOT NULL,
 estado TEXT DEFAULT 'activo',
 created_at TIMESTAMP DEFAULT NOW(),
 updated_at TIMESTAMP DEFAULT NOW()
);
ALTER TABLE viajes REPLICA IDENTITY FULL;
```
----------

## MAPA (requisitos técnicos)

-   Leaflet con CSS importado correctamente
-   Altura: h-[70vh]
-   Suscribirse a Realtime para actualizaciones en vivo
-   Popup con nombre, velocidad y tiempo desde última actualización
    

----------

## GPS + MÁQUINA DE ESTADOS (detalles específicos)

-   **watchPosition** con enableHighAccuracy: true
-   **Promedio móvil** de últimas 3 lecturas para suavizar
-   **FALLBACK de velocidad**: calcular distancia entre coordenadas / tiempo transcurrido   
-   **Page Visibility API**: pausar GPS cuando pestaña no está visible    
-   **cleanup**: clearWatch() al desmontar
    
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### GPS denegado

-   Mostrar pantalla con mensaje claro   
-   Botón "REINTENTAR" que vuelve a pedir permiso    
-   Botón "USAR SIMULACIÓN" (activa modo simulación automáticamente)
    

### Hugging Face falla o timeout

-   Continuar usando heurística local (solo velocidad, sin IA)  
-   Registrar en log: "⚠️ IA no disponible, usando detección básica"
    

### Supabase falla

-   Seguir funcionando localmente    
-   Mapa muestra mensaje: "📡 Modo offline - ubicación no compartida"   
-   Guardar intentos para reintentar después
    

----------

## LIMPIEZA DE RECURSOS (OBLIGATORIO)

-   Al desmontar Tracker: clearWatch()    
-   Al salir de VIAJE_ACTIVO: clearInterval()  
-   Page Visibility API: pausar GPS cuando pestaña no está visible   
-   Evitar múltiples watchPosition (usar ref booleano)
    

----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal (overflow-x-hidden en body)    
-   Compatible con iPhone SE (viewport meta correcto)    
-   Compatible con Android Chrome    
-   Drawer de simulación NO debe tapar navegación principal   
-   Botones tamaño mínimo 44x44px (accesibilidad táctil) 
-   Leaflet debe ser responsive: width 100%, altura definida en vh
    

----------

## VARIABLES DE ENTORNO (Secrets en Replit)

```text
VITE_HF_TOKEN = token_huggingface
VITE_SUPABASE_URL = https://proyecto.supabase.co
VITE_SUPABASE_ANON_KEY = clave_anonima
```
----------

## ESTRUCTURA DE ARCHIVOS

```text
src/
├── pages/
│   ├── Login.tsx
│   ├── Tracker.tsx
│   └── Mapa.tsx
├── components/
│   ├── Speedometer.tsx
│   ├── EventLog.tsx
│   ├── CompañerosMap.tsx
│   └── SimulationDrawer.tsx
├── hooks/
│   ├── useGPS.ts
│   ├── useColectivoMachine.ts
│   └── useSimulacion.ts
├── lib/
│   └── supabase.ts
├── contexts/
│   └── SimulationContext.tsx
└── types/
 └── index.ts
```
----------

## DEPENDENCIAS

```text
react, react-dom, typescript, vite, tailwindcss, wouter
@supabase/supabase-js, @huggingface/inference
react-leaflet, leaflet, framer-motion
```
----------

## CRITERIOS DE ACEPTACIÓN

-   Sin errores TypeScript 
-   Sin botones manuales de subida    
-   Hooks desacoplados de UI   
-   Logs completos de cada evento importante  
-   GPS fallback funciona si coords.speed es null  
-   Mapa solo muestra usuarios activos (último update < 60s)  
-   Al resetear, estado='inactivo' en Supabase    
-   Cleanup de watchPosition e intervals    
-   Manejo de errores GPS, IA y Supabase    
-   Modo simulación funciona    
-   Diseño mobile-first sin overflow horizontal    
-   Drawer no tapa navegación   
-   Funciona en iPhone SE y Android Chrome
    

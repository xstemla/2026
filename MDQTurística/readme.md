Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: MDQTurística

## FUNCIONALIDAD PRINCIPAL

Plataforma para potenciar el turismo en Mar del Plata durante todo el año. Tres perfiles: Turista (encuentra servicios en mapa), Ciudadano (reporta problemas), Emprendedor (registra negocio y promociones). Incluye chatbot con IA y sistema de reputación.

---
## RESTRICCIONES (OBLIGATORIO RESPETAR)

- NO usar backend propio
- NO usar Firebase
- NO usar Redux, NO usar Zustand
- NO agregar autenticación real (simular con localStorage)
- NO agregar funcionalidades fuera del MVP
- Mantener arquitectura simple

---

## ARQUITECTURA (DESACOPLADO)

- `useChatbot`: lógica de comunicación con Hugging Face
- `useMapa`: lógica de mapa y marcadores
- `useReportes`: lógica de reportes ciudadanos
- `useNegocios`: lógica de CRUD de negocios
- Componentes presentacionales (Mapa, Chatbot, TarjetaNegocio, FormularioReporte)

---

## DEFINICIONES EXACTAS

- **TURISTA**: puede ver mapa, buscar categorías, calificar negocios
- **CIUDADANO**: puede reportar problemas, ver actividades sociales
- **EMPRENDEDOR**: puede registrar negocio, subir promociones, ver reputación

---
## LOGS OBLIGATORIOS (para debugging)

- 🗺️ Mapa cargado
- 🤖 Chatbot: pregunta enviada / respuesta recibida
- 💾 Supabase: insert/update/error
- ⭐ Calificación registrada
- 📍 Reporte ciudadano creado
- 🏢 Negocio registrado
- 🎁 Promoción subida
- 🎪 Actividad social creada

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (SeleccionPerfil, MapaTurista, PanelCiudadano, PanelEmprendedor)
- 
### FASE 2 - Selección de perfil
- Tres botones: Turista, Ciudadano, Emprendedor
- Guardar perfil en localStorage
- Redirigir según perfil

### FASE 3 - Mapa para Turista (core)
- react-leaflet con OpenStreetMap
- Mostrar marcadores de negocios desde Supabase
- Filtros por categoría: entretenimiento, hospedaje, transporte, gastronomía, emergencias, compras, servicios
- Popup con: nombre, dirección, teléfono, horario, calificación, botón "Cómo llegar" (abre Google Maps)
-
### FASE 4 - Calificaciones y reputación
- Turista puede calificar negocio (1-5 estrellas)
- Guardar en Supabase tabla calificaciones
- Calcular promedio y actualizar reputación del negocio
- Los negocios con mejor reputación aparecen primeros

### FASE 5 - Panel Ciudadano
- Formulario para reportar: tipo (basura/luminaria/bache), ubicación (mapa o texto), foto (opcional)
- Guardar en Supabase tabla reportes
- Listado de reportes propios con estado (pendiente/en proceso/resuelto)
- Botón de emergencias: llama al 911 (tel:911)

### FASE 6 - Panel Emprendedor
- Formulario para registrar negocio: nombre, dirección, categoría, descripción, coordenadas
- Formulario para subir promociones: título, descripción, imagen, vigencia
- Ver reputación actual (puntaje promedio)
- Ver lista de promociones activas

### FASE 7 - Chatbot con IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Prompt contextual según perfil del usuario
- Mostrar historial de mensajes (solo sesión actual)

### FASE 8 - Ranking y actividades sociales
- Ranking de negocios por reputación
- Listado de actividades sociales (limpieza de playas, ferias, eventos) desde Supabase tabla `actividades`
- CRUD básico de actividades (admin simulado)

---

## SUPABASE (esquema)
```sql
-- Usuarios (simplificado, sin auth real)
CREATE TABLE usuarios (
 id SERIAL PRIMARY KEY,
 nombre TEXT DEFAULT 'Usuario',
 perfil TEXT NOT NULL,
 created_at TIMESTAMP DEFAULT NOW()
);
-- Negocios
CREATE TABLE negocios (
 id SERIAL PRIMARY KEY,
 nombre TEXT NOT NULL,
 direccion TEXT NOT NULL,
 categoria TEXT NOT NULL,
 telefono TEXT,
 horario TEXT,
 lat FLOAT NOT NULL,
 lng FLOAT NOT NULL,
 reputacion FLOAT DEFAULT 0,
 descripcion TEXT,
 creado_por INTEGER REFERENCES usuarios(id)
);
-- Calificaciones
CREATE TABLE calificaciones (
 id SERIAL PRIMARY KEY,
 negocio_id INTEGER REFERENCES negocios(id),
 usuario_id INTEGER REFERENCES usuarios(id),
 puntaje INTEGER CHECK (puntaje BETWEEN 1 AND 5),
 comentario TEXT,
 created_at TIMESTAMP DEFAULT NOW()
);
-- Reportes ciudadanos
CREATE TABLE reportes (
 id SERIAL PRIMARY KEY,
 usuario_id INTEGER REFERENCES usuarios(id),
 tipo TEXT NOT NULL,
 ubicacion TEXT NOT NULL,
 lat FLOAT,
 lng FLOAT,
 foto TEXT,
 estado TEXT DEFAULT 'pendiente',
 created_at TIMESTAMP DEFAULT NOW()
);
-- Promociones
CREATE TABLE promociones (
 id SERIAL PRIMARY KEY,
 negocio_id INTEGER REFERENCES negocios(id),
 titulo TEXT NOT NULL,
 descripcion TEXT,
 imagen TEXT,
 vigencia_hasta DATE,
 created_at TIMESTAMP DEFAULT NOW()
);
-- Actividades sociales
CREATE TABLE actividades (
 id SERIAL PRIMARY KEY,
 titulo TEXT NOT NULL,
 descripcion TEXT,
 ubicacion TEXT,
 fecha DATE,
 tipo TEXT CHECK (tipo IN ('limpieza', 'feria', 'evento'))
);
-- Habilitar Realtime
ALTER TABLE negocios REPLICA IDENTITY FULL;
ALTER TABLE reportes REPLICA IDENTITY FULL;
ALTER TABLE promociones REPLICA IDENTITY FULL;
ALTER TABLE actividades REPLICA IDENTITY FULL;
```
----------

## MAPA (requisitos técnicos)

-   Leaflet con CSS importado correctamente   
-   Altura: h-[70vh]  
-   Centrado en Mar del Plata: [-38.0055, -57.5426], zoom 12   
-   Marcadores personalizados por categoría (usar diferentes íconos)   
-   Botón "Cómo llegar" abre Google Maps con coordenadas
    
----------

## CHATBOT (detalles específicos)

-   Contexto en cada consulta: perfil, ubicación si está disponible    
-   Respuesta esperada: amigable, útil, específica para Mar del Plata    
-   Timeout 5 segundos    
-   Fallback local si Hugging Face falla: respuestas predefinidas para preguntas comunes
    
----------

## MANEJO DE ERRORES (OBLIGATORIO)

-   **Supabase falla**: modo offline con datos locales    
-   **GPS denegado**: usar ubicación manual o centrar en MDP por defecto    
-   **Chatbot timeout**: mostrar mensaje de error y sugerir reintentar
    
----------

## LIMPIEZA DE RECURSOS (OBLIGATORIO)

-   Al desmontar componente con mapa: limpiar marcadores si es necesario    
-   AbortController para peticiones fetch/chatbot al desmontar   
-   Evitar suscripciones duplicadas a Realtime    

----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE y Android Chrome    
-   Botones tamaño mínimo 44x44px   
-   Mapa táctil (zoom, pan)  
-   Formularios con inputs táctiles grandes
    
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
│   ├── SeleccionPerfil.tsx
│   ├── MapaTurista.tsx
│   ├── PanelCiudadano.tsx
│   └── PanelEmprendedor.tsx
├── components/
│   ├── Mapa.tsx
│   ├── Chatbot.tsx
│   ├── TarjetaNegocio.tsx
│   ├── FormularioReporte.tsx
│   ├── FormularioNegocio.tsx
│   ├── Ranking.tsx
│   └── ActividadesSociales.tsx
├── hooks/
│   ├── useChatbot.ts
│   ├── useMapa.ts
│   ├── useReportes.ts
│   └── useNegocios.ts
├── lib/
│   └── supabase.ts
├── contexts/
│   └── PerfilContext.tsx
└── types/
 └── index.ts
```
----------

## DEPENDENCIAS

```text
react, react-dom, typescript, vite, tailwindcss, wouter
@supabase/supabase-js, @huggingface/inference
react-leaflet, leaflet, lucide-react
```
----------

## CRITERIOS DE ACEPTACIÓN

-   Sin errores TypeScript
-   Tres perfiles funcionando con rutas separadas   
-   Mapa muestra negocios desde Supabase   
-   Turista puede calificar negocios y ver ranking    
-   Ciudadano puede reportar problemas y ver emergencias  
-   Emprendedor puede registrar negocio y subir promociones   
-   Chatbot responde preguntas contextuales
-   Datos persisten en Supabase    
-   Tabla `actividades` funciona con datos reales    
-   Diseño mobile-first con colores de Mar del Plata (azul mar, arena, celeste)

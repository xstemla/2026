Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: MascotasApp

## FUNCIONALIDAD PRINCIPAL

Ayudar a los habitantes de Mar del Plata a encontrar mascotas perdidas rápidamente. Permite publicar mascotas perdidas o encontradas, verlas en un mapa interactivo, recibir alertas por zona (simuladas) y usar IA para obtener consejos según la situación.

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
- `useMascotas`: toda la lógica de publicaciones (CRUD + localStorage)
- `useHuggingFace`: lógica de IA para consejos según situación
- `useMapa`: lógica de mapa y marcadores (Leaflet)
- `useAlertas`: lógica de suscripción por zona y notificaciones simuladas
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS
- **PUBLICACIÓN PERDIDA**: mascota que el dueño busca
- **PUBLICACIÓN ENCONTRADA**: mascota que alguien halló
- **ZONAS**: barrios de Mar del Plata (Centro, Playa Grande, Los Andes, etc.)
- **ESTADO**: activo (por defecto) o resuelto (cuando se encuentra)

---

## LOGS OBLIGATORIOS (para debugging)
- 🐾 Publicación creada: [tipo] - [especie] en [zona]
- 🗺️ Mapa cargado con [cantidad] marcadores
- 🔔 Alerta generada para zona: [zona]
- 🤖 Consultando Hugging Face para consejos...
- 🤖 IA respondió
- ✅ Publicación marcada como resuelta
- 🗑️ Publicación eliminada
- ⚠️ Error de Hugging Face

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, Publicar, Mapa, ConsejosIA)

### FASE 2 - Pantalla principal y navegación
- Dos botones grandes: "Perdí mi mascota" y "Encontré una mascota"
- Listado de publicaciones recientes (foto, especie, zona, fecha)

### FASE 3 - Publicar mascota (perdida o encontrada)
- Formulario dinámico según tipo:
 - Campos comunes: especie (perro/gato/otro), descripción, zona (selector: Centro, Playa Grande, Los Andes, etc.), foto (opcional), contacto
 - Campo "nombre" solo para perdidas
- Guardar en localStorage con:
 - id: Date.now(), tipo, fecha, estado: "activo"
- Coordenadas: asignar coordenadas fijas según zona seleccionada (para el mapa)

### FASE 4 - Mapa interactivo con Leaflet
- Importar CSS de Leaflet
- Altura: h-[70vh]
- Centrado en Mar del Plata: [-38.0055, -57.5426], zoom 13
- Mostrar marcadores para todas las publicaciones activas
- Al hacer click en marcador: popup con foto, especie, zona, contacto
- Marcadores diferenciados por tipo (perdida = rojo, encontrada = verde)

### FASE 5 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Función: consejos contextuales según:
 - Situación (perdida, encontrada, abandonada)
 - Especie (perro, gato, otro)
 - Zona y descripción adicional

### FASE 6 - Alertas por zona (simuladas)
- Usuario puede suscribirse a una o varias zonas (toggle)
- Al crear nueva publicación, verificar si hay suscriptores en esa zona
- Si hay, mostrar notificación simulada (toast o alert) en la próxima interacción
- Las alertas NO son push reales (solo dentro de la app)

### FASE 7 - Listado y gestión de publicaciones
- Mostrar todas las publicaciones en home (ordenadas por fecha descendente)
- Cada publicación tiene:
 - Foto miniatura, especie, zona, fecha, contacto
 - Botón "Marcar como resuelto" (cambia estado a inactivo)
 - Botón "Eliminar" (solo para pruebas)
- Los marcadores del mapa solo muestran publicaciones activas

### FASE 8 - Consejos IA (página o modal)
- Input para que el usuario describa su situación
- Ejemplos: "Se me perdió mi perro en Playa Grande", "Encontré un gato abandonado"
- IA responde con prioridad (Alta/Media/Baja) y lista de consejos
- Mostrar sugerencias de contacto (protectoras, zoonosis, veterinarias)
---
## LOCALSTORAGE (estructura de datos)
```json
{
 "publicaciones": [
 {
 "id": 1715678901234,
 "tipo": "perdida",
 "especie": "perro",
 "nombre": "Luna",
 "descripcion": "Blanca con mancha negra en la oreja",
 "zona": "Centro",
 "coordenadas": { "lat": -38.0055, "lng": -57.5426 },
 "foto": "data:image/jpeg;base64,...",
 "contacto": "222-555-1234",
 "fecha": "2025-05-20",
 "estado": "activo"
 }
 ],
 "suscripciones": ["Centro", "Playa Grande"]
}
```
----------

## MAPA (requisitos técnicos)

-   Leaflet con CSS importado correctamente    
-   Altura: h-[70vh], ancho: 100%    
-   Coordenadas de zonas predefinidas:    
    -   Centro: [-38.0055, -57.5426]        
    -   Playa Grande: [-38.0450, -57.5300]        
    -   Los Andes: [-37.9950, -57.5700]        
    -   (Agregar 3-4 zonas más)        
-   Marcadores personalizados: ícono rojo (perdida), verde (encontrada)    
-   Popup con: especie, zona, contacto, foto miniatura, botón "Ver más"
    
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para consejos:**
```javascript
const prompt = `
 Situación: ${situacion} (perdida/encontrada/abandonada)
 Especie: ${especie}
 Zona: ${zona}
 Descripción adicional: ${descripcion}
 Respondé EXACTAMENTE en este formato:
 Prioridad: [Alta/Media/Baja]
 Consejo 1: [texto corto]
 Consejo 2: [texto corto]
 Consejo 3: [texto corto]
 Contacto sugerido: [protectora, zoonosis o veterinaria de Mar del Plata]
`;
```

**Uso en la app:**

-   El usuario puede pedir consejos desde una pantalla específica o desde cada publicación    
-   Si la IA falla, mostrar consejos predefinidos (fallback local)
    
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable    
-   Usar respuestas predefinidas (fallback local) con consejos genéricos
    
### Leaflet o mapa no carga

-   Mostrar mensaje "No se pudo cargar el mapa"   
-   Seguir mostrando listado de publicaciones
    
### Foto muy grande

-   Al leer el archivo, limitar tamaño (redimensionar a max 500px)

### localStorage lleno o error

-   Limitar cantidad de publicaciones (mostrar advertencia al llegar a 30)    
-   Ofrecer opción de exportar/limpiar
    
----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE y Android Chrome   
-   Botones grandes (mínimo 44x44px) en home y formularios    
-   Mapa táctil (zoom, pan) bien responsive    
-   Formularios con campos que ocupan todo el ancho    
-   Input file con captura desde cámara en celular    
-   Alertas simuladas (toast o snackbar) visibles pero no invasivas
    

----------

## VARIABLES DE ENTORNO (Secrets en Replit)

```text
VITE_HF_TOKEN = token_huggingface
```
----------

## ESTRUCTURA DE ARCHIVOS

```text
src/
├── pages/
│   ├── Home.tsx
│   ├── Publicar.tsx
│   ├── Mapa.tsx
│   └── ConsejosIA.tsx
├── components/
│   ├── TarjetaPublicacion.tsx
│   ├── MapaInteractivo.tsx
│   ├── FormularioPublicacion.tsx
│   ├── SelectorZonas.tsx
│   ├── AlertaSimulada.tsx
│   └── ConsejosIA.tsx
├── hooks/
│   ├── useMascotas.ts
│   ├── useHuggingFace.ts
│   ├── useMapa.ts
│   └── useAlertas.ts
├── lib/
│   └── localStorage.ts
├── contexts/
│   └── MascotasContext.tsx
├── data/
│   └── zonasMarDelPlata.ts
└── types/
 └── index.ts
```

----------

## DEPENDENCIAS

```text
react, react-dom, typescript, vite, tailwindcss, wouter
@huggingface/inference
react-leaflet, leaflet
lucide-react
```
----------

## CRITERIOS DE ACEPTACIÓN

-   Sin errores TypeScript    
-   Usuario puede publicar mascota perdida o encontrada    
-   Las publicaciones se guardan en localStorage    
-   Mapa muestra marcadores en las coordenadas de cada zona  
-   Marcadores diferenciados por tipo (perdida/encontrada)    
-   Usuario puede suscribirse a zonas y recibe alertas simuladas    
-   IA da consejos según situación y especie    
-   Listado de publicaciones recientes en home    
-   Diseño mobile-first con colores cálidos (naranja, marrón, celeste)    
-   Fallback elegante si Hugging Face no responde

Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: SaludMayoresApp

## FUNCIONALIDAD PRINCIPAL
Ayudar a adultos mayores de Mar del Plata a conseguir medicamentos (mapa con farmacias cercanas que tengan stock) y turnos médicos (listado de especialistas con contacto). Incluye IA para corregir nombres de medicamentos, dar recordatorios de medicación y ofrecer consejos médicos simples. Diseño accesible: fuentes grandes, botones grandes, alto contraste.

---

## RESTRICCIONES (OBLIGATORIO RESPETAR)
- NO usar backend propio
- NO usar Firebase
- NO usar Redux, NO usar Zustand
- NO agregar autenticación real
- NO agregar funcionalidades fuera del MVP
- Mantener arquitectura simple
- Priorizar estabilidad sobre features
- **DISEÑO ACCESIBLE OBLIGATORIO**: fuente mínima 18px, botones mínimo 44x44px, colores de alto contraste

---

## ARQUITECTURA (DESACOPLADO)

- `useMedicamentos`: lógica de búsqueda de medicamentos y stock en farmacias
- `useTurnos`: lógica de listado de especialidades y profesionales
- `useMapa`: lógica de mapa y marcadores de farmacias (Leaflet)
- `useHuggingFace`: lógica de IA (corrección de nombres, recordatorios, consejos)
- `useAccesibilidad`: lógica de modo alto contraste y preferencias
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS

- **ADULTO MAYOR**: usuario objetivo (interfaz adaptada, sin asumir conocimientos técnicos)
- **STOCK**: disponibilidad de un medicamento en una farmacia (mock: sí/no)
- **RECORDATORIO**: alerta simulada (texto en pantalla) para horario de medicación

---

## LOGS OBLIGATORIOS (para debugging)
- 💊 Búsqueda de medicamento: [nombre]
- 🤖 IA corrigiendo nombre: [original] → [corregido]
- 🗺️ Mapa cargado con [cantidad] farmacias
- 📞 Llamada a farmacia: [nombre]
- 🏥 Búsqueda de turno en especialidad: [especialidad]
- ⏰ Recordatorio de medicación configurado: [medicamento] a las [hora]
- ⚠️ Error de Hugging Face

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, BuscarMedicamento, Turnos, Configuracion)

### FASE 2 - Pantalla principal accesible
- Dos botones grandes: "BUSCAR MEDICAMENTO" y "PEDIR TURNO MÉDICO"
- Fuente: 24px o más en títulos, 18px en texto
- Botones: tamaño mínimo 60x60px, colores contrastantes
- Opción de "Modo alto contraste" (toggle)

### FASE 3 - Buscar medicamento (con mapa)
- Input grande para escribir nombre del medicamento
- Botón "Buscar" y "Usar micrófono" (opcional, simulado con texto)
- Mapa Leaflet centrado en Mar del Plata [-38.0055, -57.5426]
- Marcadores de farmacias (mock) con:
 - Nombre, dirección, teléfono
 - Stock: SÍ/NO para el medicamento buscado
 - Botón "Llamar" (abre teléfono con número)
- Si no hay stock, mostrar mensaje claro

### FASE 4 - Pedir turno médico
- Listado de especialidades (botones grandes): Clínico, Oftalmólogo, Cardiólogo, Traumatólogo, Dermatólogo
- Al seleccionar, mostrar profesionales mock:
 - Nombre, dirección, teléfono
 - Botón "Llamar" o "Consultar"
- Opción de guardar profesional como favorito

### FASE 5 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Funciones:
 - Corrección de nombre de medicamento (si está mal escrito)
 - Recordatorios de medicación (configurar horario y mostrar mensaje)
 - Consejos médicos simples ("¿Qué preguntar al cardiólogo?")

### FASE 6 - Recordatorios de medicación (simulados)
- Pantalla o modal para agregar medicamento: nombre, hora, dosis
- Guardar en localStorage
- Cuando es la hora, mostrar notificación simulada (alert o toast en pantalla grande)
- Listado de recordatorios activos (con opción de eliminar)

### FASE 7 - Asistente IA simple (chat o guía)
- Botón "Consultar a la IA" en pantalla principal
- Input para pregunta: "¿Qué hago si me duele el pecho?", "¿Cómo tomar losartán?"
- IA responde con lenguaje simple, paso a paso, máximo 3 pasos
- Consejo adicional: "Si no entendés, pedile a un familiar que te ayude"

### FASE 8 - Accesibilidad y preferencias
- Toggle "Modo alto contraste" (fondo negro, texto blanco, botones amarillos)
- Guardar preferencia en localStorage
- Opción de aumentar fuente (18px, 22px, 26px) - extra
- Todas las pantallas deben pasar prueba de contraste y tamaño de botones

---

## LOCALSTORAGE (estructura de datos)
```json
{
 "recordatorios": [
 { "medicamento": "Losartán", "hora": "08:00", "dosis": "50mg" },
 { "medicamento": "Aspirina", "hora": "20:00", "dosis": "100mg" }
 ],
 "farmaciasFavoritas": [1, 3],
 "profesionalesContactados": [101, 102],
 "accesibilidad": {
 "altoContraste": false,
 "tamañoFuente": "grande"  // normal, grande, extragrande
 }
}
```
----------

## MAPA (requisitos técnicos)

-   Leaflet con CSS importado correctamente    
-   Altura: 60vh (un poco más pequeño para dejar espacio a botones)    
-   Centrado en Mar del Plata: [-38.0055, -57.5426], zoom 14    
-   Farmacias mock (5-6 puntos en la ciudad):    

```javascript
const farmaciasMock = [
 { id: 1, nombre: "Farmacia Centro", direccion: "Av. Luro 123", telefono: "223 555-1234", lat: -38.0055, lng: -57.5426, stock: { "losartán": true, "aspirina": false } },
 { id: 2, nombre: "Farmacia Playa Grande", direccion: "Av. del Mar 456", telefono: "223 555-5678", lat: -38.0450, lng: -57.5300, stock: { "losartán": false, "aspirina": true } }
];
```
-   Al buscar medicamento, solo mostrar farmacias con stock=true para ese medicamento    
-   Popup con nombre, dirección, teléfono y botón "Llamar" grande
    
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para corregir nombre de medicamento:**
```javascript
const prompt = `
 El usuario escribió: "${textoIngresado}"
 ¿Es un medicamento real o está mal escrito?
 Corregilo a un nombre de medicamento real (ej. "losartán", "aspirina", "paracetamol").
 Respondé SOLO con el nombre corregido en minúsculas.
`;
```

**Prompt para recordatorios (generar mensaje amigable):**

```javascript
const prompt = `
 Es la hora de tomar ${medicamento} (${dosis}).
 Generá un mensaje corto, claro y amigable para un adulto mayor.
 Usá un tono respetuoso y alentador.
`;
```

**Prompt para consejos médicos:**

```javascript
const prompt = `
 El usuario (adulto mayor) pregunta: "${pregunta}"
 Respondé de forma CLARA y SIMPLE:
 1. Respuesta simple (una oración)
 2. Paso a paso (máximo 3 pasos)
 3. Qué hacer si no entiende (sugerir pedir ayuda)
`;
```
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable: "No pude conectar con la IA. Reintentá más tarde."    
-   Para corrección de medicamentos: usar el texto original sin cambios    
-   Para recordatorios: mensaje genérico "Es hora de tomar tu medicamento"
    

### Mapa no carga

-   Mostrar mensaje claro "No se pudo cargar el mapa. Revisá tu conexión."    
-   Seguir mostrando lista de farmacias en texto (como fallback)
    
### GPS denegado (para farmacias cercanas)

-   Mostrar mensaje "No podemos ver tu ubicación. Mostramos todas las farmacias."    
-   Seguir funcionando sin geolocalización
    

### Input de texto vacío o inválido

-   Mostrar mensaje: "Escribí el nombre del medicamento, por favor"
    

----------

## ACCESIBILIDAD (OBLIGATORIO - chequeo final)

-   Fuente base mínima 18px en todo el texto    
-   Botones mínimo 44x44px, ideal 60x60px    
-   Contraste: texto sobre fondo (mínimo 4.5:1)    
-   Modo alto contraste opcional (toggle guardado)    
-   Inputs con borde grueso y label grande    
-   Mensajes de error claros y visibles    
-   Sin gestos complejos (solo tap)
    
----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE (pantalla chica) y Android   
-   Botones ocupan al menos 50% de ancho en pantallas pequeñas   
-   Mapa táctil (zoom, pan)    
-   Inputs grandes (padding 12px)
    
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
│   ├── BuscarMedicamento.tsx
│   ├── Turnos.tsx
│   ├── Recordatorios.tsx
│   └── Configuracion.tsx
├── components/
│   ├── BotonAccesible.tsx
│   ├── MapaFarmacias.tsx
│   ├── ListaFarmacias.tsx
│   ├── ListaEspecialidades.tsx
│   ├── ListaProfesionales.tsx
│   ├── RecordatorioItem.tsx
│   ├── AsistenteIA.tsx
│   └── ToggleAccesibilidad.tsx
├── hooks/
│   ├── useMedicamentos.ts
│   ├── useTurnos.ts
│   ├── useMapa.ts
│   ├── useHuggingFace.ts
│   └── useAccesibilidad.ts
├── lib/
│   └── localStorage.ts
├── contexts/
│   └── AccesibilidadContext.tsx
├── data/
│   ├── farmaciasMock.ts
│   └── profesionalesMock.ts
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
-   Diseño cumple accesibilidad: fuente 18px+, botones 44px+, contraste    
-   Usuario puede buscar medicamento y ver mapa con farmacias que tienen stock    
-   Botón "Llamar" abre el teléfono con número de la farmacia    
-   Usuario puede ver listado de especialidades y profesionales con contacto    
-   IA corrige nombres de medicamentos mal escritos    
-   IA puede configurar recordatorios y mostrar notificaciones simuladas    
-   IA responde preguntas médicas simples en lenguaje claro    
-   Datos persisten en localStorage (recordatorios, favoritos)    
-   Modo alto contraste funciona y se guarda    
-   Fallback elegante si Hugging Face no responde

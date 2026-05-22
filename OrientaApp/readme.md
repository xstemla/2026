Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.
## NOMBRE: OrientaApp
## FUNCIONALIDAD PRINCIPAL
Ayudar a adolescentes que no saben qué estudiar mediante un test vocacional con IA. El usuario responde preguntas sobre gustos, habilidades e intereses, y la IA analiza sus respuestas para recomendar carreras, explicar por qué coinciden con su perfil, y mostrar un mapa con universidades cercanas.

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
- `useTestVocacional`: lógica del test (preguntas, respuestas, progreso)
- `useHuggingFace`: lógica de IA para analizar respuestas y recomendar carreras
- `useMapa`: lógica de mapa y marcadores de universidades
- `useResultados`: lógica de guardado en localStorage y compartir
- Los componentes deben ser presentacionales
---
## DEFINICIONES EXACTAS
- **TEST CORTO**: 5 preguntas básicas (rápido, menos preciso)
- **TEST LARGO**: 15 preguntas (más preciso, más tiempo)
- **PERFIL DETECTADO**: etiqueta de 2-3 palabras que resume al usuario (ej. "Social y analítico")
- **TOP 3 CARRERAS**: las 3 carreras mejor rankeadas por la IA
---
## LOGS OBLIGATORIOS (para debugging)
- 📝 Test iniciado (modo: corto/largo)
- ❓ Pregunta respondida: [número]
- 🤖 Consultando Hugging Face para analizar respuestas...
- 🤖 IA respondió con recomendaciones
- 💾 Resultados guardados en localStorage
- 🗺️ Mapa cargado con [cantidad] universidades
- 📤 Resultados compartidos por WhatsApp
- ⚠️ Error de Hugging Face

---
## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, Test, Resultados, Mapa)

### FASE 2 - Pantalla inicial y selección de test
- Título "¿Qué puedo estudiar?" y breve explicación
- Botones: "Test corto (5 preguntas)" y "Test largo (15 preguntas)"
- Botón "Ver mi último resultado" (si existe en localStorage)

### FASE 3 - Test vocacional (preguntas)
- Array predefinido de preguntas (5 o 15 según modo)
- Cada pregunta: opciones múltiples (ej. "¿Qué disfrutás más?", "¿En qué sos bueno?")
- Barra de progreso (pregunta actual / total)
- Guardar respuestas en estado local

### FASE 4 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Función: al finalizar el test, enviar todas las respuestas a la IA
- La IA debe responder en formato estructurado (ver prompt)

### FASE 5 - Pantalla de resultados
- Mostrar "Perfil detectado" (ej. "Social y creativo")
- Mostrar Top 3 carreras recomendadas
- Por cada carrera, mostrar explicación personalizada de por qué coincide
- Consejo motivador adicional
- Botón "Ver en mapa" (lleva a la página del mapa con las universidades)

### FASE 6 - Mapa con universidades
- Leaflet con CSS importado
- Centrado en Mar del Plata (o coordenadas configurables)
- Marcadores para universidades que ofrecen las carreras recomendadas
- Popup: nombre de la universidad, carreras destacadas, dirección
- (Los datos de universidades pueden ser un array fijo en el código)

### FASE 7 - Guardar y compartir resultados
- Guardar en localStorage: respuestas, resultados, fecha
- Botón "Guardar este resultado" (si el usuario quiere conservarlo)
- Botón "Reiniciar test" (borra respuestas y empieza de nuevo)
- Botón "Compartir por WhatsApp": abre WhatsApp con mensaje predefinido que incluye las carreras recomendadas

### FASE 8 - Mejoras de experiencia
- Opción de ver resultado anterior (cargar desde localStorage)
- Animaciones suaves entre preguntas
- Diseño adaptativo: en celular, las opciones son botones grandes

---

## PREGUNTAS DEL TEST (mock para el prompt)
**Test corto (5 preguntas):**
1. ¿Qué actividad te suena más atractiva? (Ayudar a personas / Resolver problemas técnicos / Crear arte o contenido / Organizar y planificar)
2. ¿Cuál es tu materia favorita? (Lengua y comunicación / Matemáticas / Ciencias / Historia y sociales)
3. ¿Cómo te describirían tus amigos? (Empático / Analítico / Creativo / Líder)
4. ¿Qué entorno laboral preferís? (Oficina / Laboratorio o taller / Trabajo de campo / Remoto desde casa)
5. ¿Qué valorás más en un trabajo? (Ayudar a otros / Buen salario / Creatividad / Estabilidad)
**Test largo:** se pueden agregar más preguntas similares (especificar en el prompt que la IA debe usar las primeras 5 si el prompt es muy largo, o generar un array de 15 preguntas en el código).
---
## LOCALSTORAGE (estructura de datos)
```json
{
 "ultimoResultado": {
 "fecha": "2025-05-20",
 "modo": "corto",
 "respuestas": ["Ayudar a personas", "Lengua", "Empático", "Oficina", "Ayudar a otros"],
 "resultadosIA": {
 "perfil": "Social y empático",
 "carreras": ["Psicología", "Trabajo Social", "Recursos Humanos"],
 "explicaciones": {
 "Psicología": "Te gusta ayudar a personas y entender sus emociones...",
 "Trabajo Social": "Valorás el bienestar comunitario...",
 "Recursos Humanos": "Sos empático y te interesa el entorno laboral..."
 },
 "consejo": "Tu perfil es ideal para carreras donde el centro sea la persona."
 }
 }
}
```
----------

## MAPA (requisitos técnicos)

-   Leaflet con CSS importado correctamente
    
-   Altura: h-[70vh], ancho: 100%
    
-   Centro: [-38.0055, -57.5426] (Mar del Plata, pero puede configurarse)
    
-   Marcadores con ícono personalizado (ej. morado)
    
-   Datos de universidades (mock):
    

```javascript
const universidades = [
 { nombre: "UNMdP", carreras: ["Psicología", "Ingeniería", "Medicina"], lat: -38.0055, lng: -57.5426, direccion: "Peatonal Diagonal 123" },
 { nombre: "UTN", carreras: ["Ingeniería", "Tecnicaturas"], lat: -38.0100, lng: -57.5500, direccion: "Av. Colón 456" },
 { nombre: "Universidad FASTA", carreras: ["Psicología", "Nutrición"], lat: -38.0000, lng: -57.5350, direccion: "Av. Luro 789" }
];
```
-   El mapa filtra y solo muestra universidades que tengan ALGUNA de las carreras recomendadas por la IA.
    

----------

## HUGGING FACE IA (detalles específicos)

**Prompt para analizar respuestas (test corto como ejemplo):**

```javascript
const prompt = `
 El usuario respondió este test vocacional:
 Pregunta 1 (actividad atractiva): ${respuesta1}
 Pregunta 2 (materia favorita): ${respuesta2}
 Pregunta 3 (descripción de amigos): ${respuesta3}
 Pregunta 4 (entorno laboral): ${respuesta4}
 Pregunta 5 (valor en trabajo): ${respuesta5}
 Analizá las respuestas y respondé EXACTAMENTE en este formato:
 Perfil detectado: [2-3 palabras]
 Top 3 carreras: [carrera1, carrera2, carrera3]
 Explicación para carrera1: [texto corto]
 Explicación para carrera2: [texto corto]
 Explicación para carrera3: [texto corto]
 Consejo adicional: [frase motivadora]
`;
```

**Para test largo**, el prompt debe incluir las 15 respuestas en el mismo formato, pero puede truncarse o enviarse en partes (la app puede hacer dos llamadas a IA). Para simplificar el MVP, se recomienda implementar primero el test corto y luego extender.

----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable    
-   Usar recomendaciones predefinidas (fallback local) basadas en respuestas comunes:    
    -   Si muchas respuestas son "ayudar personas" → Psicología, Trabajo Social        
    -   Si son "resolver problemas" → Ingeniería, Sistemas        
    -   etc.
        

### Mapa no carga

-   Mostrar mensaje "No se pudo cargar el mapa"    
-   Seguir mostrando lista de universidades en texto
    
### LocalStorage lleno o error

-   Mostrar opción de borrar resultado anterior para guardar nuevo
    

----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE y Android Chrome    
-   Botones grandes (mínimo 44x44px) para respuestas del test    
-   Barra de progreso clara    
-   Mapa táctil (zoom, pan)    
-   Resultados con fuente legible y espaciado adecuado    
-   Botón de compartir por WhatsApp bien visible
    

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
│   ├── Test.tsx
│   ├── Resultados.tsx
│   └── MapaUniversidades.tsx
├── components/
│   ├── Pregunta.tsx
│   ├── BarraProgreso.tsx
│   ├── TarjetaCarrera.tsx
│   ├── MapaLeaflet.tsx
│   └── BotonCompartir.tsx
├── hooks/
│   ├── useTestVocacional.ts
│   ├── useHuggingFace.ts
│   ├── useMapa.ts
│   └── useResultados.ts
├── lib/
│   └── localStorage.ts
├── contexts/
│   └── TestContext.tsx
├── data/
│   ├── preguntasCorto.ts
│   ├── preguntasLargo.ts
│   └── universidades.ts
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
-   Usuario puede elegir test corto o largo    
-   Test muestra preguntas con barra de progreso    
-   Al finalizar, IA analiza respuestas y devuelve perfil + top 3 carreras + explicaciones    
-   Resultados se guardan en localStorage    
-   Mapa muestra universidades que ofrecen las carreras recomendadas    
-   Usuario puede compartir resultados por WhatsApp    
-   Diseño mobile-first con colores juveniles (celeste, naranja, violeta)  
-   Fallback elegante si Hugging Face no responde
    



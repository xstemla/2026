📝 PROMPT DEFINITIVO (con advertencias y soluciones reales)
markdown
Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: EstudIA

## FUNCIONALIDAD PRINCIPAL

Apoyo escolar gratuito para estudiantes de secundaria (13 a 18 años). Contenido organizado por materia y tema (currícula de Buenos Aires), videos educativos, asistente IA que responde preguntas y genera ejercicios, y seguimiento de progreso personalizado.

---

## ⚠️ ADVERTENCIA IMPORTANTE (LEER ANTES DE EMPEZAR)

**En el entorno de Replit, NO se puede llamar directamente a `api-inference.huggingface.co`.** 
El dominio está bloqueado (DNS no resuelve). Tampoco se puede usar `@huggingface/inference` con tokens básicos porque requiere permisos especiales.

### ✅ ÚNICA SOLUCIÓN QUE FUNCIONA EN REPLIT:

Usar **OpenRouter** a través de **Replit AI Integrations**. 
- No necesita API key propia
- No pasa por dominios bloqueados
- Soporta modelos como `microsoft/phi-3-mini-128k-instruct`
- Es una integración nativa de Replit

### Cómo configurarlo:

1. En Replit, abrir **Tools → AI Integrations**
2. Activar **OpenRouter**
3. Seleccionar el modelo `microsoft/phi-3-mini-128k-instruct`
4. El código generado automáticamente queda en `replit.nix` y usa `@replit/ai`

### Código que SÍ funciona en Replit:

```typescript
// Backend (Express) o frontend (React) - funciona igual
import { AI } from '@replit/ai'

const ai = new AI()

const respuesta = await ai.chatCompletion({
  model: 'microsoft/phi-3-mini-128k-instruct',
  messages: [
    { role: 'system', content: 'Sos un asistente de estudio para secundaria.' },
    { role: 'user', content: 'Explicame fracciones' }
  ]
})

console.log(respuesta.message.content)
❌ Lo que NO hay que hacer (no funciona en Replit):
fetch('https://api-inference.huggingface.co/...') → Dominio bloqueado

new HfInference(token).chatCompletion() → Token sin permisos

Cualquier llamada directa a *.huggingface.co desde el backend
```


RESTRICCIONES (OBLIGATORIO RESPETAR)
NO usar backend propio (salvo Express mínimo si se necesita)
NO usar Firebase
NO usar Redux, NO usar Zustand
NO agregar autenticación real
NO usar Hugging Face directamente (no funciona en Replit)

Mantener arquitectura simple
Priorizar estabilidad sobre features

ARQUITECTURA (DESACOPLADO)
useIA: lógica de comunicación con OpenRouter (usando @replit/ai)
useContenido: lógica de videos y temas por materia
useProgresoEstudio: lógica de videos vistos, puntaje, último tema
useAsistente: lógica del chat con IA contextual (MANTENER historial de conversación)

Los componentes deben ser presentacionales

DEFINICIONES EXACTAS
MATERIAS BASE: Matemática, Lengua, Ciencias (Biología/Química/Física), Historia
TEMAS: subcategorías dentro de cada materia (ej. Matemática → Fracciones, Ecuaciones)

PUNTAJE: +10 puntos por video visto, +5 por ejercicio completado

LOGS OBLIGATORIOS (para debugging)
📚 Materia/tema seleccionado

🎬 Video reproducido

📝 Ejercicio generado por IA

✅ Actividad completada

🤖 Consultando IA (OpenRouter)...

🤖 IA respondió

💾 Progreso guardado en localStorage

⚠️ Error de IA

IMPLEMENTACIÓN POR FASES
FASE 1 - Setup base
React + Vite + TypeScript + Tailwind

Configurar Replit AI Integrations (OpenRouter) en replit.nix

Routing con wouter (Home, Materias, VideoPlayer, Asistente, Progreso)

FASE 2 - Pantalla inicial
Selección de materia: Matemática, Lengua, Ciencias, Historia

Selección de tema (dinámico según materia)

FASE 3 - Contenido educativo (videos)
Grid de videos de ejemplo (YouTube embebido)

Reproductor que marca "visto" al finalizar

FASE 4 - Seguimiento de progreso
Guardar en localStorage: videos vistos, puntaje, último tema

Mostrar "Seguir estudiando"

FASE 5 - Integración con IA (OpenRouter)
Configuración inicial (única vez):

En Replit: Tools → AI Integrations → OpenRouter → Activar

Seleccionar modelo microsoft/phi-3-mini-128k-instruct

Código del hook useIA.ts:

typescript
import { AI } from '@replit/ai'

const ai = new AI()

export async function consultarIA(prompt: string) {
  try {
    const respuesta = await ai.chatCompletion({
      model: 'microsoft/phi-3-mini-128k-instruct',
      messages: [
        { role: 'system', content: 'Sos un asistente de estudio para secundaria (13 a 18 años). Respondé de forma clara, didáctica y con ejemplos de Argentina.' },
        { role: 'user', content: prompt }
      ]
    })
    return respuesta.message.content
  } catch (error) {
    console.error('Error en IA:', error)
    return null // Para usar fallback
  }
}
FASE 6 - Asistente IA (chat) - REQUISITOS CRÍTICOS
⚠️ OBLIGATORIO: El chat debe mantener historial de conversación.

typescript
// Estado del chat
const [mensajes, setMensajes] = useState([
  { role: 'system', content: 'Sos EstudIA, asistente de estudio para secundaria.' }
])

// Función para enviar mensaje
const enviarMensaje = async (texto: string) => {
  // 1. Agregar mensaje del usuario
  const nuevosMensajes = [...mensajes, { role: 'user', content: texto }]
  setMensajes(nuevosMensajes)
  
  // 2. Enviar TODO el historial a la IA
  const respuesta = await ai.chatCompletion({
    model: 'microsoft/phi-3-mini-128k-instruct',
    messages: nuevosMensajes  // ← Envía el historial completo
  })
  
  // 3. Guardar respuesta en el historial
  setMensajes([...nuevosMensajes, { role: 'assistant', content: respuesta.message.content }])
}
FASE 7 - Generación de ejercicios
Botón "Practicar" en cada tema

IA genera 3 ejercicios con solución (usando el mismo consultarIA)

Suma puntaje al completar

FASE 8 - Dashboard personal
Estadísticas y progreso visual

Recomendación IA personalizada

LOCALSTORAGE (estructura de datos)
json
{
  "usuarioId": "usuario_demo",
  "edad": 15,
  "progreso": {
    "matematica": {
      "fracciones": { "videoVisto": true, "ejerciciosCompletados": 3 }
    }
  },
  "ultimoTema": "matematica/fracciones",
  "puntajeTotal": 125
}
Nota: No guardar el historial del chat en localStorage (solo en memoria).

PROMPTS PARA LA IA (se arman según necesidad)
Explicar un tema:
text
Materia: ${materia}
Tema: ${tema}
Edad: ${edad} años

Explicá de forma clara con ejemplos de la vida cotidiana de Argentina.
Formato:
EXPLICACION: [texto]
PREGUNTA 1: [texto]
PREGUNTA 2: [texto]
Generar ejercicios:
text
Materia: ${materia}
Tema: ${tema}
Nivel: secundario (${edad} años)

Generá 3 ejercicios prácticos con sus soluciones.
Formato:
Ejercicio 1: [texto]
Ejercicio 2: [texto]
Ejercicio 3: [texto]
Soluciones: 1: [respuesta], 2: [respuesta], 3: [respuesta]
Recomendación personalizada:
text
Temas vistos: ${temasVistos}
Puntaje: ${puntaje}
Currícula Buenos Aires.

¿Qué tema debería ver a continuación?
Respondé:
MATERIA: [nombre]
TEMA: [nombre]
JUSTIFICACION: [una oración]
MANEJO DE ERRORES (OBLIGATORIO)
IA falla o timeout
Mostrar mensaje amigable: "La IA está teniendo problemas, intentá de nuevo"

Usar fallbacks locales:

Explicaciones básicas predefinidas (fracciones, ecuaciones, etc.)

Ejercicios genéricos

Videos de YouTube no cargan
Mostrar "Video no disponible temporalmente"

Ofrecer explicación por IA como alternativa

localStorage lleno
Limitar progreso a últimos 50 temas

Mostrar opción de reiniciar datos

MOBILE (OBLIGATORIO)
Evitar overflow horizontal

Compatible con iPhone SE y Android Chrome

Botones tamaño mínimo 44x44px

Reproductor de video responsivo (aspect-ratio 16/9)

Chat con scroll y input fijo abajo

VARIABLES DE ENTORNO
No necesita token externo. La integración de OpenRouter se configura en Replit:

Tools → AI Integrations → OpenRouter → Activar

ESTRUCTURA DE ARCHIVOS
text
src/
├── pages/
│   ├── Home.tsx
│   ├── Materias.tsx
│   ├── VideoPlayer.tsx
│   ├── Asistente.tsx
│   └── Progreso.tsx
├── components/
│   ├── TarjetaMateria.tsx
│   ├── ReproductorVideo.tsx
│   ├── ChatAsistente.tsx      # ← Mantiene historial de mensajes
│   └── BarraProgreso.tsx
├── hooks/
│   ├── useIA.ts               # ← Usa @replit/ai, NO Hugging Face
│   ├── useContenido.ts
│   └── useProgresoEstudio.ts
├── lib/
│   └── localStorage.ts
└── types/
    └── index.ts

replit.nix                      # Configura la integración de IA
DEPENDENCIAS
text
react, react-dom, typescript, vite, tailwindcss, wouter, lucide-react
@replit/ai                      # ← Para usar OpenRouter
CRITERIOS DE ACEPTACIÓN
Sin errores TypeScript

IA funcionando con OpenRouter (NO con Hugging Face directo)

Asistente IA mantiene historial de conversación

Selección de materia/tema funciona

Videos embebidos se reproducen

Progreso guarda en localStorage

Sin errores de CORS o "Failed to fetch"

Fallback elegante si la IA falla

Mobile-first

text

---

## 📊 Resumen de lo que aprendimos y pusimos en el prompt

| Problema detectado | Cómo lo resolvimos en el prompt |
|-------------------|--------------------------------|
| `api-inference.huggingface.co` bloqueado | ❌ Prohibido usarlo. Usar OpenRouter. |
| Token de HF sin permisos | ❌ No usar tokens de HF. Usar integración nativa. |
| CORS / DNS en Replit | ✅ Solución: `@replit/ai` + OpenRouter |
| Chat sin memoria | ✅ Requisito explícito de historial de mensajes |
| Pérdida de tiempo debuggeando | ✅ Advertencia inicial "LEER ANTES DE EMPEZAR" |
| Confusión sobre qué funciona | ✅ Código de ejemplo que SÍ funciona |

---

## 🎯 La frase que resume el prompt

> *"En Replit, NO uses Hugging Face directamente. Usá OpenRouter vía `@replit/ai`. Es la única forma que funciona sin bloqueos ni permisos especiales. Y el chat tiene que mandar TODO el historial cada vez."*

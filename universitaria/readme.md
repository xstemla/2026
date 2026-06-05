📝 PROMPT DEFINITIVO (con advertencias y soluciones reales)

Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

**NOMBRE:** Conectá (Consejería universitaria con IA)

**FUNCIONALIDAD PRINCIPAL**
Plataforma gratuita que conecta a jóvenes de 15 a 20 años (provincia de Buenos Aires) con consejeros universitarios (estudiantes avanzados o graduados) a través de foros de preguntas y respuestas. La IA recomienda foros según intereses y detecta preguntas duplicadas.

---

## ⚠️ ADVERTENCIA IMPORTANTE (LEER ANTES DE EMPEZAR)

En el entorno de Replit, **NO se puede llamar directamente a api-inference.huggingface.co**. El dominio está bloqueado (DNS no resuelve). Tampoco se puede usar `@huggingface/inference` con tokens básicos porque requiere permisos especiales.

**✅ ÚNICA SOLUCIÓN QUE FUNCIONA EN REPLIT:**
Usar **OpenRouter** a través de **Replit AI Integrations**.

- No necesita API key propia
- No pasa por dominios bloqueados
- Soporta modelos como `microsoft/phi-3-mini-128k-instruct`
- Es una integración nativa de Replit

**Cómo configurarlo:**
1. En Replit, abrir `Tools → AI Integrations`
2. Activar `OpenRouter`
3. Seleccionar el modelo `microsoft/phi-3-mini-128k-instruct`
4. El código generado automáticamente queda en `replit.nix` y usa `@replit/ai`

**Código que SÍ funciona en Replit:**
```typescript
// Frontend React - funciona igual
import { AI } from '@replit/ai'

const ai = new AI()

const respuesta = await ai.chatCompletion({
  model: 'microsoft/phi-3-mini-128k-instruct',
  messages: [
    { role: 'system', content: 'Sos un asistente que recomienda foros universitarios y detecta duplicados.' },
    { role: 'user', content: '¿Qué carreras tienen salida laboral en tecnología?' }
  ]
})

console.log(respuesta.message.content)
```

❌ Lo que NO hay que hacer (no funciona en Replit):
```
fetch('https://api-inference.huggingface.co/...') → Dominio bloqueado

new HfInference(token).chatCompletion() → Token sin permisos

Cualquier llamada directa a *.huggingface.co desde el backend
```
## RESTRICCIONES (OBLIGATORIO RESPETAR)
- ❌ NO usar backend propio (salvo Express mínimo si se necesita)
- ❌ NO usar Firebase
- ❌ NO usar Redux, NO usar Zustand
- ❌ NO agregar autenticación real
- ❌ NO usar Hugging Face directamente (no funciona en Replit)
- ✅ Mantener arquitectura simple
- ✅ Priorizar estabilidad sobre features

ARQUITECTURA (DESACOPLADO)
- useIA: lógica de comunicación con OpenRouter (usando @replit/ai)
- useForos: lógica de foros, preguntas y respuestas
- useRecomendacion: lógica de IA para recomendar foros según intereses
- useValidacion: validación de consejeros (simulada sin backend real)

Los componentes deben ser presentacionales.

## DEFINICIONES EXACTAS
- CARRERAS BASE: Medicina, Ingeniería, Derecho, Psicología, Ciencias de la Computación, Administración
- FOROS: cada foro pertenece a una carrera y contiene preguntas y respuestas de consejeros.

## PUNTAJE:
- Consejero: +10 puntos por respuesta útil, +5 por mejor respuesta
- Estudiante: +5 puntos por pregunta bien formulada (para incentivar participación)

## VALIDACIÓN CONSEJEROS (simulada):
- Subir foto de credencial o certificado
- En demo, se acepta manualmente (sin backend real)

LOGS OBLIGATORIOS (para debugging)
```text
📚 Carrera/foro seleccionado
🎓 Consejero registró respuesta
🤖 IA recomendando foros...
🤖 IA detectó posible duplicado
🗳️ Voto registrado para respuesta
✅ Consejero validado (simulado)
💾 Progreso guardado en localStorage
⚠️ Error de IA
🏆 Usuario sumó [X] puntos. Total: [Y]
```

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Configurar Replit AI Integrations (OpenRouter) en `replit.nix`
- Routing con `wouter` (Home, Foros, ForoDetalle, AsistenteIA, Perfil)

### FASE 2 - Pantalla inicial
- Selección de carrera: Medicina, Ingeniería, Derecho, Psicología, Computación, Administración
- Listado de foros populares de esa carrera

### FASE 3 - Foros y preguntas
- Cada foro tiene: título, carrera, preguntas, respuestas de consejeros
- Los estudiantes pueden hacer preguntas
- Los consejeros pueden responder

### FASE 4 - Votación y reputación
- Estudiantes votan respuestas útiles (+1)
- Consejeros acumulan puntaje y visibilidad
- Sistema anti-doble voto por usuario/respuesta

### FASE 5 - Integración con IA (OpenRouter) - CRÍTICO

**Configuración inicial (única vez):**
1. En Replit: `Tools → AI Integrations → OpenRouter → Activar`
2. Seleccionar modelo `microsoft/phi-3-mini-128k-instruct`

### Código del hook `useIA.ts`:

```typescript
import { AI } from '@replit/ai'

const ai = new AI()

export async function consultarIA(prompt: string, contexto?: string) {
  try {
    const respuesta = await ai.chatCompletion({
      model: 'microsoft/phi-3-mini-128k-instruct',
      messages: [
        { 
          role: 'system', 
          content: 'Sos un asistente para orientación vocacional universitaria. Ayudás a jóvenes de 15 a 20 años de la provincia de Buenos Aires a elegir carrera. Respondé de forma clara, con ejemplos reales y mencionando salida laboral en Argentina.' 
        },
        { role: 'user', content: prompt }
      ]
    })
    return respuesta.message.content
  } catch (error) {
    console.error('⚠️ Error de IA:', error)
    return null // Para usar fallback
  }
}

// Función específica para detectar preguntas duplicadas
export async function detectarDuplicado(preguntaNueva: string, preguntasExistentes: string[]) {
  const prompt = `
    ¿Esta nueva pregunta es esencialmente igual a alguna de las siguientes?
    Nueva: "${preguntaNueva}"
    Existentes: ${preguntasExistentes.join(' | ')}
    
    Respondé solo SI o NO.
  `
  const respuesta = await consultarIA(prompt)
  return respuesta?.includes('SI') ?? false
}

// Función para recomendar foros según intereses
export async function recomendarForos(intereses: string[], historial: string[]) {
  const prompt = `
    Intereses del usuario: ${intereses.join(', ')}
    Historial de foros vistos: ${historial.join(', ')}
    
    Recomendá 3 foros de carreras (de: Medicina, Ingeniería, Derecho, Psicología, Computación, Administración).
    Formato: 
    CARRERA 1: [nombre]
    FORO 1: [título]
    CARRERA 2: [nombre]
    FORO 2: [título]
    CARRERA 3: [nombre]
    FORO 3: [título]
  `
  return await consultarIA(prompt)
}
```

## FASE 6 - Asistente IA vocacional (chat con historial) - REQUISITOS CRÍTICOS
### ⚠️ OBLIGATORIO: El chat debe mantener historial de conversación.

```typescript
// Estado del chat
const [mensajes, setMensajes] = useState([
  { role: 'system', content: 'Sos Conectá, asistente de orientación universitaria para jóvenes de Buenos Aires. Ayudás a elegir carrera mostrando experiencias reales de consejeros.' }
])

// Función para enviar mensaje
const enviarMensaje = async (texto: string) => {
  // 1. Agregar mensaje del usuario
  const nuevosMensajes = [...mensajes, { role: 'user', content: texto }]
  setMensajes(nuevosMensajes)

  // 2. Enviar TODO el historial a la IA
  const respuesta = await ai.chatCompletion({
    model: 'microsoft/phi-3-mini-128k-instruct',
    messages: nuevosMensajes // ← Envía el historial completo
  })

  // 3. Guardar respuesta en el historial
  setMensajes([...nuevosMensajes, { role: 'assistant', content: respuesta.message.content }])
}
```

## FASE 7 - Validación de consejeros (simulada con IA)
- Botón "Quiero ser consejero"
- Subir foto de credencial (simulado, no se envía realmente)
- IA analiza si parece válido (fallback: aprobación automática en demo)

## FASE 8 - Dashboard personal
- Estadísticas: foros seguidos, preguntas hechas, votos recibidos (si es consejero)
- Recomendación IA personalizada de carreras según actividad

LOCALSTORAGE (estructura de datos)
```json
{
  "usuarioId": "estudiante_demo",
  "rol": "estudiante",
  "edad": 17,
  "intereses": ["tecnologia", "salud"],
  "forosSeguidos": ["medicina_1", "computacion_3"],
  "preguntasRealizadas": [],
  "votosRealizados": [],
  "puntajeTotal": 45,
  "ultimoForoVisto": "ingenieria/software"
}

// Consejero adicional
{
  "consejeroId": "consejero_demo",
  "nombre": "Carlos Gómez",
  "universidad": "UNLP",
  "carrera": "Ingeniería",
  "validado": true,
  "puntuacion": 4.7,
  "respuestasDadas": []
}
```
Nota: No guardar el historial del chat en localStorage (solo en memoria).

## PROMPTS PARA LA IA (se arman según necesidad)

### Detectar pregunta duplicada:
```text
¿Estas dos preguntas describen la misma duda sobre una carrera universitaria?
Pregunta 1: [texto]
Pregunta 2: [texto]
Respondé solo SI o NO.
```


### Recomendar carrera según intereses:
```text
- Edad: [edad]
- Intereses: [lista]
- Materias que le gustan: [lista]
- Respondé: CARRERA: [nombre] JUSTIFICACION: [una oración con salida laboral en Argentina]
```


### Responder pregunta vocacional:
```text
Un joven de [edad] años pregunta: "[pregunta]"
Respondé como consejero universitario con experiencia real. Mencioná cómo es estudiar esa carrera, dificultades y salida laboral en Buenos Aires.
```


---

## MANEJO DE ERRORES (OBLIGATORIO)

**IA falla o timeout:**
- Mostrar mensaje amigable: "La IA está teniendo problemas, intentá de nuevo"
- Usar fallbacks locales:
  - Recomendaciones básicas predefinidas (carreras más comunes)
  - Detección de duplicados por distancia de texto simple

**Foros sin respuestas:**
- Mostrar: "Todavía no hay respuestas, sé el primer consejero en ayudar"

**Validación de consejero falla:**
- Modo demo: aprobar automáticamente con mensaje "En la versión final se validaría con universidades"

**localStorage lleno:**
- Limitar a últimos 50 foros seguidos
- Mostrar opción de reiniciar datos

---

## MOBILE (OBLIGATORIO)

- Evitar overflow horizontal
- Compatible con iPhone SE y Android Chrome
- Botones tamaño mínimo 44x44px
- Chat con scroll y input fijo abajo
- Tarjetas de foros en grid responsivo

---

## VARIABLES DE ENTORNO

No necesita token externo. La integración de OpenRouter se configura en Replit:
`Tools → AI Integrations → OpenRouter → Activar`

---

## ESTRUCTURA DE ARCHIVOS
```text
src/
├── pages/
│ ├── Home.tsx
│ ├── ForosPorCarrera.tsx
│ ├── ForoDetalle.tsx
│ ├── AsistenteIA.tsx
│ └── Perfil.tsx
├── components/
│ ├── TarjetaForo.tsx
│ ├── ListaPreguntas.tsx
│ ├── RespuestaConsejero.tsx
│ ├── ChatAsistente.tsx # ← Mantiene historial de mensajes
│ └── ValidadorConsejero.tsx
├── hooks/
│ ├── useIA.ts # ← Usa @replit/ai, NO Hugging Face
│ ├── useForos.ts
│ ├── useRecomendacion.ts
│ └── useProgresoEstudiante.ts
├── lib/
│ └── localStorage.ts
├── data/
│ └── carrerasMock.ts # Datos de ejemplo de carreras y foros
└── types/
└── index.ts
```

**replit.nix** - Configura la integración de IA automáticamente.

---

## DEPENDENCIAS

```json
{
  "react", "react-dom", "typescript", "vite", "tailwindcss", "wouter", "lucide-react",
  "@replit/ai"  // ← Para usar OpenRouter
}
```


## CRITERIOS DE ACEPTACIÓN

- ✅ Sin errores TypeScript
- ✅ IA funcionando con OpenRouter (NO con Hugging Face directo)
- ✅ Asistente IA mantiene historial de conversación
- ✅ Selección de carrera y foros funciona
- ✅ Consejeros pueden responder preguntas
- ✅ Votación sin doble voto funciona
- ✅ Progreso guarda en localStorage
- ✅ Sin errores de CORS o "Failed to fetch"
- ✅ Fallback elegante si la IA falla
- ✅ Mobile-first

---

## 📊 RESUMEN DE LO QUE APRENDIMOS

| Problema detectado | Cómo lo resolvimos |
|---|---|
| `api-inference.huggingface.co` bloqueado | ❌ Prohibido usarlo. Usar OpenRouter. |
| Token de HF sin permisos | ❌ No usar tokens de HF. Usar integración nativa. |
| CORS / DNS en Replit | ✅ Solución: `@replit/ai` + OpenRouter |
| Chat sin memoria | ✅ Requisito explícito de historial de mensajes |
| Pérdida de tiempo debuggeando | ✅ Advertencia inicial "LEER ANTES DE EMPEZAR" |
| Confusión sobre qué funciona | ✅ Código de ejemplo que SÍ funciona |

---

## 🎯 FRASE CLAVE DEL PROYECTO

> **"En Replit, NO uses Hugging Face directamente. Usá OpenRouter vía @replit/ai. Es la única forma que funciona sin bloqueos ni permisos especiales. El chat tiene que mandar TODO el historial cada vez. Y la plataforma conecta jóvenes con consejeros universitarios mediante foros + IA."**

---




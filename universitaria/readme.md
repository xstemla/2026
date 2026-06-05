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

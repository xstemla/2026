Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: AlanApp
## FUNCIONALIDAD PRINCIPAL

Alan es un asistente de estudio con IA que ayuda a organizar tareas, dividir objetivos grandes en pasos pequeños, crear hábitos de estudio y motivar al usuario con un sistema de recompensas (rompecabezas) y vínculo emocional (mensajes de preocupación si abandona).

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

- `useHuggingFace`: lógica de comunicación con Hugging Face API
- `useAlanIA`: lógica específica del asistente (dividir tareas, plan de estudio)
- `useGamificacion`: lógica de rompecabezas y recompensas
- `useAbandono`: lógica de detección de inactividad y mensajes de preocupación
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS

- **TAREA GRANDE**: objetivo de estudio que el usuario necesita completar (ej. "estudiar 5 temas para el examen")
- **PASO PEQUEÑO**: subtarea generada por IA (ej. "resumir tema 1", "hacer 5 ejercicios")
- **PIEZA DE ROMPECABEZAS**: recompensa por cada paso completado
- **ABANDONO**: 3 días sin abrir la app

---

## LOGS OBLIGATORIOS (para debugging)
- 👋 Usuario registró nombre y materias
- 🧩 Tarea creada: [nombre]
- 🤖 IA generando pasos...
- 🤖 IA respondió
- ✅ Paso completado: [nombre]
- 🧩 Pieza de rompecabezas otorgada
- 🖼️ Rompecabezas completado
- 😟 Mensaje de preocupación enviado (abandono detectado)
- 💾 Progreso guardado en localStorage
- ⚠️ Error de Hugging Face

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Onboarding, Dashboard, Tareas, Logros)

### FASE 2 - Onboarding (primera vez)
- Pantalla inicial pide: nombre del usuario, materias/áreas de estudio
- Guardar en localStorage
- Alan (avatar/animación amigable) da la bienvenida

### FASE 3 - Dashboard principal
- Mostrar avatar de Alan (puede ser un emoji grande o ícono animado con CSS)
- Lista de tareas activas
- Progreso del rompecabezas actual (piezas obtenidas)
- Mensaje motivador del día

### FASE 4 - Crear y dividir tareas
- Input para que el usuario escriba una tarea grande (ej. "estudiar para el examen de matemáticas")
- Botón "Alan, ayudame a dividir"
- IA genera:
 - Lista de pasos pequeños
 - Tiempo estimado total
 - Mensaje motivador

### FASE 5 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Funciones:
 - Dividir tareas grandes en pasos lógicos
 - Sugerir plan de estudio según materias
 - Generar mensajes de preocupación personalizados

### FASE 6 - Sistema de recompensas (rompecabezas)
- Cada paso completado → +1 pieza de rompecabezas
- Rompecabezas completo (ej. 6 piezas) → imagen completa + recompensa
- Las recompensas son mensajes de Alan (ej. "¡Sos increíble! Desbloqueaste un nuevo logro")
- Progreso de múltiples rompecabezas (se reinicia al completar)

### FASE 7 - Detección de abandono y mensajes emocionales
- Registrar timestamp de última actividad
- Si pasan 3 días sin actividad:
 - Alan muestra mensaje de preocupación personalizado
 - Ejemplo: "¡Hola [nombre]! Te extrañé. ¿Cómo venís con [última tarea]? Podemos retomarla juntos."
- Los mensajes se generan con IA contextual

### FASE 8 - Personalización y hábitos
- Alan sugiere plan de estudio semanal según materias
- Opción de recordatorios (simulados con notificaciones del navegador)
- Estadísticas: racha de días activos, tareas completadas

---

## LOCALSTORAGE (estructura de datos)
```json
{
 "usuario": {
 "nombre": "Juan",
 "materias": ["Matemática", "Historia", "Lengua"],
 "fechaRegistro": "2025-05-20"
 },
 "tareas": [
 {
 "id": "1",
 "titulo": "Estudiar para examen de matemáticas",
 "pasos": [
 { "texto": "Repasar ecuaciones", "completado": true },
 { "texto": "Hacer 5 ejercicios de fracciones", "completado": false },
 { "texto": "Ver video de funciones", "completado": false }
 ],
 "tiempoEstimado": 90,
 "creada": "2025-05-20",
 "completada": false
 }
 ],
 "rompecabezasActual": {
 "id": 3,
 "totalPiezas": 6,
 "piezasObtenidas": 2,
 "imagenCompleta": "🌟 ¡Campeón! 🌟"
 },
 "estadisticas": {
 "diasActivos": 5,
 "tareasCompletadas": 3,
 "ultimaConexion": "2025-05-20"
 }
}
```
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para dividir tarea:**

```javascript
const prompt = `
 Tarea del usuario: ${tarea}
 Sus materias: ${materias}
 Dividí esta tarea en 3 a 5 pasos pequeños y alcanzables.
 Estimá el tiempo total en minutos.
 Agregá un mensaje motivador corto.
 Formato exacto:
 Pasos: [paso 1, paso 2, paso 3, ...]
 Tiempo: [número] minutos
 Motivación: [frase corta]
`;
```

**Prompt para mensaje de preocupación (abandono):**

```javascript
const prompt = `
 El usuario ${nombre} no usa la app hace ${diasInactivo} días.
 Su última tarea era: ${ultimaTarea}
 Sus materias son: ${materias}
 Generá un mensaje corto, cálido y preocupado.
 Demostrale que Alan se acuerda de él y quiere ayudarlo a retomar.
 Usá un tono amigable, como un amigo que se preocupa.
`;
```

**Prompt para plan de estudio semanal:**

```javascript
const prompt = `
 El usuario tiene estas materias: ${materias}
 Tiene disponible ${diasPorSemana} días por semana.
 Sugerí un plan de estudio simple.
 Formato:
 Lunes: [materia y tema]
 Martes: [materia y tema]
 ...
 Consejo: [texto corto]
`;
```

----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable
-   Usar respuestas predefinidas (fallback local) para:
    -   División de tareas comunes ("estudiar matemática" → pasos genéricos)
    -   Mensajes de preocupación simples
        
### LocalStorage lleno o error

-   Limitar historial a últimas 20 tareas
-   Mostrar opción de exportar/limpiar datos
    
### Abandono mal detectado

-   Usar fecha de última actividad, no solo cierre de app
-   Permitir al usuario "pausar" recordatorios si no quiere mensajes
    
----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal
-   Compatible con iPhone SE y Android Chrome
-   Botones tamaño mínimo 44x44px (especialmente para completar pasos)
-   Avatar de Alan debe ser visible pero no ocupar demasiado espacio
-   Lista de pasos con checkboxes grandes y táctiles
-   Progreso del rompecabezas visual (ej. 3/6 piezas)
    
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
│   ├── Onboarding.tsx
│   ├── Dashboard.tsx
│   ├── Tareas.tsx
│   ├── Logros.tsx
│   └── Configuracion.tsx
├── components/
│   ├── AvatarAlan.tsx
│   ├── TarjetaTarea.tsx
│   ├── ListaPasos.tsx
│   ├── Rompecabezas.tsx
│   ├── MensajePreocupacion.tsx
│   ├── PlanEstudio.tsx
│   └── Estadisticas.tsx
├── hooks/
│   ├── useHuggingFace.ts
│   ├── useAlanIA.ts
│   ├── useGamificacion.ts
│   └── useAbandono.ts
├── lib/
│   └── localStorage.ts
├── contexts/
│   └── UsuarioContext.tsx
└── types/
 └── index.ts
```
----------

## DEPENDENCIAS

```text
react, react-dom, typescript, vite, tailwindcss, wouter
@huggingface/inference
lucide-react
```
----------

## CRITERIOS DE ACEPTACIÓN

-   Sin errores TypeScript
-   Onboarding guarda nombre y materias
-   Usuario puede crear tarea grande y IA la divide en pasos
-   Completar pasos otorga piezas de rompecabezas
-   Al completar todas las piezas, muestra recompensa
-   Si pasa 3 días sin actividad, Alan muestra mensaje de preocupación
-   Datos persisten en localStorage
-   Diseño mobile-first con colores cálidos (naranja, amarillo, celeste)
-   Fallback elegante si Hugging Face no responde

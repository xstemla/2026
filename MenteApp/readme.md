
Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.
## NOMBRE: MenteApp

## FUNCIONALIDAD PRINCIPAL

App de apoyo emocional para adolescentes y jóvenes en situación vulnerable. Previene el suicidio y promueve la salud mental mediante un "modo urgente" que detecta cuando el usuario no está bien y lo acompaña en tiempo real, permitiendo avisar a alguien de confianza con un toque. Incluye chat guiado, seguimiento del estado de ánimo, espacios anónimos moderados y recursos de ayuda.

---
## RESTRICCIONES (OBLIGATORIO RESPETAR)
- NO usar backend propio
- NO usar Firebase
- NO usar Redux, NO usar Zustand
- NO agregar autenticación real (simulada)
- NO agregar funcionalidades fuera del MVP
- Mantener arquitectura simple
- Priorizar estabilidad sobre features
- **ADVERTENCIA**: Esta app NO reemplaza ayuda profesional. Incluir siempre enlace a líneas de emergencia (ej. 135, 911)

---
## ARQUITECTURA (DESACOPLADO)

- `useHuggingFace`: lógica de IA para chat guiado y análisis de estado de ánimo
- `useModoUrgente`: lógica de detección de crisis y acciones rápidas
- `useEstadoAnimo`: lógica de seguimiento emocional (registro diario)
- `useRedApoyo`: lógica de contactos de confianza y notificaciones simuladas
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS
- **MODO URGENTE**: estado especial de la app cuando el usuario indica que no está bien (botón "Estoy mal" o detección por respuesta negativa)
- **CONTACTO DE CONFIANZA**: persona que el usuario elige para recibir alerta (simulado)
- **CHAT GUIADO**: conversación con IA que sigue un protocolo de apoyo emocional (no terapéutico)
- **ESTADO DE ÁNIMO**: registro diario en escala (1-5) con opción de escribir

---

## LOGS OBLIGATORIOS (para debugging)

- 💚 Usuario registró estado de ánimo: [nivel]
- 🚨 Modo urgente activado
- 🤖 Chat guiado iniciado
- 📞 Alerta enviada a contacto de confianza (simulado)
- 🛡️ Espacio anónimo: nuevo post creado
- ⚠️ Error de Hugging Face (usar fallback)
- 💾 Datos guardados en localStorage

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, ModoUrgente, ChatIA, EstadoAnimo, RedApoyo, Recursos)

### FASE 2 - Onboarding (primera vez)
- Pedir nombre (opcional, puede ser anónimo)
- Configurar contacto de confianza (nombre y teléfono, solo en localStorage)
- Aceptar advertencia: "Esta app no reemplaza ayuda profesional. En caso de emergencia llamá al 135 o 911"

### FASE 3 - Pantalla principal (home)
- Botón grande destacado: "¿No estás bien? → Modo urgente" (rojo/llamativo)
- Botón "Registrar cómo me siento hoy" (seguimiento de ánimo)
- Botón "Charlar con IA" (chat guiado)
- Botón "Espacio seguro" (foro anónimo moderado - simulado)
- Botón "Mis contactos de confianza"
- Recursos: líneas de ayuda (135, 911, etc.)

### FASE 4 - Modo urgente (core)
- Al activarlo (botón o detección por respuesta negativa en chat):
 1. Mostrar mensaje de acompañamiento: "No estás solo/a. Vamos paso a paso."
 2. Ofrecer acciones simples:
 - "Hablar con alguien ahora" (chat IA guiado)
 - "Avisar a un contacto de confianza" (simular envío de alerta)
 - "Llamar a línea de emergencia 135" (abrir teléfono)
 - "Respirar conmigo" (animación de respiración guiada de 30s)
 3. Después de la crisis, ofrecer recursos y seguimiento

### FASE 5 - Chat guiado con IA (Hugging Face)
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN

- **Prompt especial para contenido sensible**:
```javascript
const prompt = `
 El usuario es un adolescente que busca apoyo emocional.
 Mensaje: "${mensaje}"
  
 IMPORTANTE: 
 - NO des consejos médicos ni diagnósticos.
 - Mostrá empatía y escucha activa.
 - Preguntá cómo se siente.
 - Si menciona autolesión o suicidio, respondé: "Lo que estás diciendo es muy importante. Por favor, hablá con un adulto de confianza o llamá al 135 (línea de prevención del suicidio). No estás solo/a."
 - Mantené un tono cálido, nunca juzgues.
 - Ofrecé recursos de ayuda.
`;
 ```
### FASE 6 - Seguimiento del estado de ánimo

-   Registro diario: seleccionar emoji (1-5) + texto opcional   
-   Guardar en localStorage    
-   Mostrar historial en calendario o gráfico simple   
-   Detectar tendencias negativas (ej. 3 días seguidos con nivel bajo) → sugerir activar modo urgente o contactar apoyo
    
### FASE 7 - Red de apoyo y alertas (simuladas)

-   Configurar hasta 3 contactos de confianza: nombre, teléfono (opcional)    
-   Botón "Avisar a mi contacto" → mostrar mensaje simulado: "Se enviaría un mensaje a [nombre] diciendo: 'Tu amigo/a [usuario] necesita que lo contactes. Por favor, hablá con él/ella.'"    
-   En versión real, se integraría con SMS o WhatsApp (fuera del MVP)
    

### FASE 8 - Espacio seguro (foro anónimo moderado)

-   Publicaciones anónimas (sin identificación)    
-   Moderación básica por IA: detectar palabras prohibidas o contenido peligroso   
-   Los usuarios pueden comentar con apoyo    
-   Guardar en localStorage (limitado a últimas 20 publicaciones)
    
----------

## LOCALSTORAGE (estructura de datos)

 ```json
{
 "usuario": {
 "nombre": "Ana",
 "anonimo": false,
 "contactos": [
 { "nombre": "Mamá", "telefono": "222-555-1234" }
 ]
 },
 "estadoAnimo": [
 { "fecha": "2025-05-20", "nivel": 2, "texto": "Me siento solo" },
 { "fecha": "2025-05-21", "nivel": 3, "texto": "Un poco mejor" }
 ],
 "alertasEnviadas": [
 { "fecha": "2025-05-20", "contacto": "Mamá", "simulado": true }
 ],
 "postsForo": [
 { "id": 1, "texto": "Hoy me siento triste", "comentarios": [], "fecha": "2025-05-20" }
 ]
}
 ```
----------

## HUGGING FACE IA (detalles específicos - CRÍTICO)

**Prompt para chat guiado (versión segura):**

 ```javascript
const prompt = `
 Eres un asistente de apoyo emocional para adolescentes.
 El usuario dice: "${mensaje}"
  
 REGLAS ESTRICTAS:
 1. No sos un profesional de la salud.
 2. Nunca recetes medicamentos ni diagnóstiques.
 3. Si hay riesgo de vida o autolesión, respondé ÚNICAMENTE: "Lo que decís es muy importante. Por favor, llamá al 135 (línea de prevención del suicidio) o hablá con un adulto de confianza. No estás solo/a."
 4. Si es una conversación general (tristeza, estrés, soledad), mostrá empatía, validá sus sentimientos, preguntá cómo podés ayudar.
 5. Ofrecé recursos: "¿Probaste respirar profundo? ¿Querés que hagamos un ejercicio juntos?"
 6. Respondé en español, tono cálido y adolescente (sin jerga forzada).
 7. Máximo 100 palabras.
`;
 ```
 
**Prompt para moderación de foro:**

 ```javascript
const prompt = `
 Analizá este mensaje de un foro anónimo de salud mental: "${texto}"
 ¿Contiene contenido peligroso (autolesión, suicidio, acoso)?
 Respondé SOLO "PELIGROSO" o "SEGURO".
`;
 ```
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable: "Estoy teniendo problemas de conexión, pero no estás solo/a. ¿Querés probar el modo urgente o contactar a un adulto de confianza?"  
-   Fallback: respuestas predefinidas empáticas ("Entiendo que te sientas así. ¿Querés hablar de eso?") y recursos de emergencia siempre visibles.
    

### Detección de crisis mal interpretada

-   Siemere priorizar la seguridad: si la IA no entiende, mostrar recursos de emergencia.
    

### localStorage lleno o error

-   Limpiar historial de estado de ánimo antiguo (más de 3 meses)   
-   Notificar al usuario que los datos muy antiguos se borran
    

----------

## DISEÑO (obligatorio para esta app)

-   Colores: tonos tranquilos (celeste suave, verde menta, blanco, gris claro)    
-   **Botón de modo urgente**: rojo vibrante, tamaño grande, en lugar destacado   
-   Tipografía: legible, cálida  
-   Espacios de respiro: animación de respiración, paisajes suaves   
-   Sin elementos que puedan abrumar (muchos textos, colores agresivos)
    
----------

## MOBILE (OBLIGATORIO)

-   Botón de modo urgente visible en todas las pantallas    
-   Acceso rápido a contacto de emergencia (135)    
-   Inputs grandes y fáciles de tocar    
-   Animación de respiración guiada (por si el usuario está en crisis)
    
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
│   ├── ModoUrgente.tsx
│   ├── ChatIA.tsx
│   ├── EstadoAnimo.tsx
│   ├── RedApoyo.tsx
│   └── EspacioSeguro.tsx
├── components/
│   ├── BotonUrgente.tsx
│   ├── AnimacionRespiracion.tsx
│   ├── RecursoEmergencia.tsx
│   ├── RegistroAnimo.tsx
│   ├── PublicacionForo.tsx
│   └── ContactoConfianza.tsx
├── hooks/
│   ├── useHuggingFace.ts
│   ├── useModoUrgente.ts
│   ├── useEstadoAnimo.ts
│   └── useRedApoyo.ts
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
-   Botón de modo urgente funciona y ofrece acciones claras (chat guiado, avisar contacto, emergencia, respirar)    
-   Chat IA con prompt de seguridad (sin consejos médicos, derivación a emergencia si hay riesgo)   
-   Usuario puede registrar estado de ánimo y ver historial   
-   Configurar contacto de confianza (simulado)   
-   Foro anónimo con moderación básica por IA    
-   Recursos de emergencia (135, 911) siempre visibles   
-   Fallback elegante si Hugging Face no responde   
-   Diseño calmado, sin elementos agresivos

Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: EntrenamientoApp


## FUNCIONALIDAD PRINCIPAL

Ayudar a jóvenes y adolescentes a aprender sobre entrenamiento y salud. Incluye categorías por nivel, videos educativos, seguimiento de progreso (gráficos y calendario), funciones sociales (ranking, compartir logros, desafíos) y un asistente IA que recomienda rutinas y responde preguntas.

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
- `useProgreso`: lógica de seguimiento (peso, entrenamientos, gráficos)
- `useSocial`: lógica de ranking, desafíos y compartir
- `useVideos`: lógica de reproducción de videos (con/sonido)
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS
- **NIVEL PRINCIPIANTE**: ejercicios básicos, sin peso, énfasis en técnica
- **NIVEL INTERMEDIO**: ejercicios con peso moderado, series de 8-12 repeticiones
- **NIVEL AVANZADO**: ejercicios complejos, alta intensidad
- **DESAFÍO SEMANAL**: objetivo medible (ej. "entrená 3 días", "hacé 100 sentadillas")

---

## LOGS OBLIGATORIOS (para debugging)

- 📹 Video reproducido / pausado
- 📊 Progreso guardado (peso, entrenamiento)
- 🏆 Desafío completado
- 🤖 Consultando Hugging Face para rutina...
- 🤖 IA respondió
- 👥 Logro compartido por WhatsApp
- ⚠️ Error de Hugging Face

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, Entrenamiento, Progreso, Social, AsistenteIA)

### FASE 2 - Pantalla principal y categorías
- Tarjetas con niveles: Principiante, Intermedio, Avanzado
- Tipos de entrenamiento: Cardio, Fuerza, Flexibilidad, Funcional
- Sección "Para qué sirve entrenar" (beneficios físicos y mentales)

### FASE 3 - Contenido educativo (videos e imágenes)
- Grid de ejercicios con:
 - Video de YouTube embebido (ejemplo para cada ejercicio)
 - Imagen ilustrativa (placeholder o URL)
 - Texto explicativo paso a paso
- Toggle "Sonido activado / silenciado" (muta el video si se puede)

### FASE 4 - Seguimiento de progreso
- Formulario para anotar: peso (kg), repeticiones, tiempo (min)
- Calendario visual (días entrenados se marcan en verde)
- Gráfico simple de progreso (línea para peso o barras para días entrenados)
- Guardar datos en localStorage

### FASE 5 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Funciones:
 - Recomendar rutina según nivel y objetivo
 - Responder preguntas sobre técnica y prevención de lesiones
 - Generar mensajes motivadores personalizados
 
### FASE 6 - Funcionalidades sociales
- Botón "Compartir logro" → abre WhatsApp con mensaje predefinido
- Ranking de amigos (simulado con datos de ejemplo: "Ana: 5 días", "Luis: 3 días")
- Desafíos semanales predefinidos (se marcan como completados)

### FASE 7 - Asistente IA (chat simple)
- Input para que el usuario haga preguntas
- Ejemplos: "¿cómo hago sentadillas?", "¿cómo evito lesiones?", "motivame"
- IA responde en formato texto amigable

### FASE 8 - Dashboard personal
- Mostrar estadísticas: días entrenados esta semana, progreso de peso, último desafío completado
- Recomendación de rutina semanal generada por IA (según nivel y objetivo guardado)

---

## LOCALSTORAGE (estructura de datos)
```json
{
 "usuarioId": "usuario_demo",
 "nivel": "principiante",
 "objetivo": "ganar fuerza",
 "progreso": {
 "peso": [70, 69.5, 69],
 "fechasPeso": ["2025-05-01", "2025-05-08", "2025-05-15"],
 "entrenamientos": [
 { "fecha": "2025-05-01", "tipo": "fuerza", "duracion": 30 },
 { "fecha": "2025-05-03", "tipo": "cardio", "duracion": 20 }
 ]
 },
 "desafiosCompletados": ["entrenar 3 dias", "100 sentadillas"],
 "anotaciones": ["me duele la espalda al hacer peso muerto"],
 "sonidoActivado": true
}
```
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para recomendar rutina:**

```javascript
const prompt = `
 Nivel: ${nivel} (principiante/intermedio/avanzado)
 Objetivo: ${objetivo} (ganar fuerza/bajar de peso/mejorar resistencia)
 Días disponibles por semana: ${dias}
 Respondé EXACTAMENTE en este formato:
 Rutina: [3-4 ejercicios con repeticiones o minutos]
 Técnica: [consejo corto]
 Motivación: [frase corta]
`;
```

**Prompt para asistente de preguntas:**

```javascript
const prompt = `
 Contexto: app de entrenamiento para jóvenes.
 Pregunta del usuario: ${pregunta}
 Respondé de forma clara, breve y útil.
 Si no sabés algo, sugerí consultar a un entrenador profesional.
`;
```

**Prompt para motivación personalizada:**

```javascript
const prompt = `
 El usuario ha entrenado ${diasEntrenados} días esta semana.
 Su mejor racha fue ${rachaMaxima} días seguidos.
 Generá un mensaje corto y motivador para alentarlo a seguir.
`;
```
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable
-   Usar respuestas predefinidas (fallback local) para:   
    -   Rutinas básicas por nivel        
    -   Consejos de técnica comunes        
    -   Frases motivadoras genéricas
        

### Videos de YouTube no cargan

-   Mostrar mensaje "Video no disponible"  
-   Ofrecer ver solo la explicación por texto
    

### LocalStorage lleno o error

-   Limitar historial a últimos 30 entrenamientos    
-   Mostrar opción de exportar/limpiar datos
   
----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE y Android Chrome    
-   Botones tamaño mínimo 44x44px   
-   Videos responsivos (aspect-ratio 16/9)    
-   Gráficos legibles en pantallas chicas    
-   Calendario táctil (fácil de tocar días)
    
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
│   ├── Entrenamiento.tsx
│   ├── Progreso.tsx
│   ├── Social.tsx
│   └── AsistenteIA.tsx
├── components/
│   ├── TarjetaNivel.tsx
│   ├── ReproductorVideo.tsx
│   ├── CalendarioProgreso.tsx
│   ├── GraficoProgreso.tsx
│   ├── TablaRanking.tsx
│   ├── DesafiosSemanales.tsx
│   └── ChatAsistente.tsx
├── hooks/
│   ├── useHuggingFace.ts
│   ├── useProgreso.ts
│   ├── useSocial.ts
│   └── useVideos.ts
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
lucide-react, recharts (para gráficos)
```

----------

## CRITERIOS DE ACEPTACIÓN

-   Sin errores TypeScript    
-   Categorías y niveles funcionan    
-   Videos educativos se reproducen (al menos embebidos de YouTube)    
-   Seguimiento de progreso guarda y muestra gráfico/calendario   
-   IA recomienda rutinas según nivel  
-   Ranking y compartir por WhatsApp funcionan (simulado)    
-   Datos persisten en localStorage    
-   Diseño mobile-first con colores energéticos (naranja, verde, azul)    
-   Fallback elegante si Hugging Face no responde

# 🏋️ EntrenamientoApp

Crear una aplicación web con **React 18 + TypeScript + Vite + Tailwind CSS**.

---

# 📌 NOMBRE

**EntrenamientoApp**

---

# 🎯 FUNCIONALIDAD PRINCIPAL

Ayudar a jóvenes y adolescentes a aprender sobre entrenamiento y salud.

La aplicación incluye:

* Categorías por nivel.
* Videos educativos.
* Seguimiento de progreso mediante gráficos y calendario.
* Funciones sociales (ranking, compartir logros y desafíos).
* Asistente IA que recomienda rutinas y responde preguntas.

---

# 🚫 RESTRICCIONES (OBLIGATORIO RESPETAR)

* NO usar backend propio.
* NO usar Firebase.
* NO usar Redux.
* NO usar Zustand.
* NO agregar autenticación real.
* NO agregar funcionalidades fuera del MVP.
* Mantener arquitectura simple.
* Priorizar estabilidad sobre features.

---

# 🏗️ ARQUITECTURA (DESACOPLADO)

## Hooks

### useIA

Lógica de comunicación con OpenRouter.

### useProgreso

Lógica de seguimiento:

* Peso.
* Entrenamientos.
* Gráficos.

### useSocial

Lógica de:

* Ranking.
* Desafíos.
* Compartir logros.

### useVideos

Lógica de reproducción:

* Reproducir.
* Pausar.
* Sonido activado/silenciado.

## Componentes

Los componentes deben ser únicamente presentacionales.

---

# 📚 DEFINICIONES EXACTAS

## Nivel Principiante

* Ejercicios básicos.
* Sin peso.
* Énfasis en técnica.

## Nivel Intermedio

* Peso moderado.
* Series de 8 a 12 repeticiones.

## Nivel Avanzado

* Ejercicios complejos.
* Alta intensidad.

## Desafío Semanal

Objetivo medible.

Ejemplos:

* Entrenar 3 días.
* Hacer 100 sentadillas.

---

# 📝 LOGS OBLIGATORIOS

```text
📹 Video reproducido / pausado
📊 Progreso guardado (peso, entrenamiento)
🏆 Desafío completado
🤖 Consultando IA (OpenRouter) para rutina...
🤖 IA respondió
👥 Logro compartido por WhatsApp
⚠️ Error de IA (OpenRouter)
```

---

# 🚀 IMPLEMENTACIÓN POR FASES

## FASE 1 — Setup Base

* React
* Vite
* TypeScript
* Tailwind CSS
* Routing con Wouter

Páginas:

* Home
* Entrenamiento
* Progreso
* Social
* AsistenteIA

---

## FASE 2 — Pantalla Principal y Categorías

### Niveles

* Principiante
* Intermedio
* Avanzado

### Tipos de entrenamiento

* Cardio
* Fuerza
* Flexibilidad
* Funcional

### Sección educativa

"Para qué sirve entrenar"

Beneficios:

* Físicos.
* Mentales.
* Hábitos saludables.

---

## FASE 3 — Contenido Educativo

Grid de ejercicios con:

* Video de YouTube embebido.
* Imagen ilustrativa.
* Explicación paso a paso.
* Toggle de sonido.

Opciones:

* Sonido activado.
* Sonido silenciado.

---

## FASE 4 — Seguimiento de Progreso

Formulario para registrar:

* Peso (kg).
* Repeticiones.
* Tiempo (minutos).

### Visualización

* Calendario de entrenamientos.
* Gráfico de progreso.

### Persistencia

Guardar en localStorage.

---

## FASE 5 — Integración IA con OpenRouter

### Importante

NO utilizar Hugging Face.

Usar OpenRouter.

### API

```text
https://openrouter.ai/api/v1/chat/completions
```

### Variable de entorno

```env
VITE_OPENROUTER_API_KEY=tu_api_key
```

### Modelo recomendado

```text
google/gemini-2.0-flash-exp:free
```

Alternativa:

```text
microsoft/phi-3-mini-128k-instruct
```

### Hook useIA.ts

```typescript
const response = await fetch(
  "https://openrouter.ai/api/v1/chat/completions",
  {
    method: "POST",
    headers: {
      Authorization: `Bearer ${import.meta.env.VITE_OPENROUTER_API_KEY}`,
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      model: "google/gemini-2.0-flash-exp:free",
      messages: [
        {
          role: "user",
          content: prompt,
        },
      ],
    }),
  }
);
```

### Funciones IA

* Recomendar rutinas.
* Responder preguntas.
* Generar motivación personalizada.

---

## FASE 6 — Funcionalidades Sociales

### Compartir Logro

Botón:

```text
Compartir por WhatsApp
```

### Ranking Simulado

```text
Ana: 5 días
Luis: 3 días
Pedro: 2 días
```

### Desafíos

* Entrenar 3 días.
* Hacer 100 sentadillas.
* Caminar 5 km.

---

## FASE 7 — Asistente IA

Chat simple.

Preguntas ejemplo:

```text
¿Cómo hago sentadillas?
¿Cómo evito lesiones?
Motivame.
```

Respuesta:

* Clara.
* Breve.
* Útil.

Utilizando OpenRouter.

---

## FASE 8 — Dashboard Personal

Mostrar:

* Días entrenados esta semana.
* Evolución del peso.
* Último desafío completado.

Además:

* Recomendación semanal generada por IA.

---

# 💾 ESTRUCTURA LOCALSTORAGE

```json
{
  "usuarioId": "usuario_demo",
  "nivel": "principiante",
  "objetivo": "ganar fuerza",
  "progreso": {
    "peso": [70, 69.5, 69],
    "fechasPeso": [
      "2025-05-01",
      "2025-05-08",
      "2025-05-15"
    ],
    "entrenamientos": [
      {
        "fecha": "2025-05-01",
        "tipo": "fuerza",
        "duracion": 30
      },
      {
        "fecha": "2025-05-03",
        "tipo": "cardio",
        "duracion": 20
      }
    ]
  },
  "desafiosCompletados": [
    "entrenar 3 dias",
    "100 sentadillas"
  ],
  "anotaciones": [
    "me duele la espalda al hacer peso muerto"
  ],
  "sonidoActivado": true
}
```

---

# 🤖 PROMPTS PARA OPENROUTER

## Recomendar Rutina

```text
Nivel: ${nivel}
Objetivo: ${objetivo}
Días disponibles por semana: ${dias}

Respondé EXACTAMENTE en este formato:

Rutina: [3-4 ejercicios con repeticiones o minutos]

Técnica: [consejo corto]

Motivación: [frase corta]
```

---

## Asistente de Preguntas

```text
Contexto: app de entrenamiento para jóvenes.

Pregunta del usuario: ${pregunta}

Respondé de forma clara, breve y útil.

Si no sabés algo, sugerí consultar a un entrenador profesional.
```

---

## Motivación Personalizada

```text
El usuario ha entrenado ${diasEntrenados} días esta semana.

Su mejor racha fue ${rachaMaxima} días seguidos.

Generá un mensaje corto y motivador para alentarlo a seguir.
```

---

# ⚠️ MANEJO DE ERRORES (OBLIGATORIO)

## Error de OpenRouter

Mostrar:

```text
El asistente IA está muy ocupado, pero te ayudo igualmente.
```

### Fallbacks locales

* Rutinas básicas.
* Consejos de técnica.
* Frases motivadoras.

---

## Error de YouTube

Mostrar:

```text
Video no disponible
```

Y ofrecer:

* Explicación en texto.

---

## Error de LocalStorage

* Mantener solo los últimos 30 entrenamientos.
* Permitir exportar datos.
* Permitir limpiar datos.

---

# 📱 MOBILE (OBLIGATORIO)

* Sin overflow horizontal.
* Compatible con iPhone SE.
* Compatible con Android Chrome.
* Botones mínimo 44x44 px.
* Videos responsivos.
* Aspect ratio 16:9.
* Gráficos legibles.
* Calendario táctil.

---

# 🔐 VARIABLES DE ENTORNO

```env
VITE_OPENROUTER_API_KEY=tu_api_key_de_openrouter
```

## Obtener API Key

1. Crear cuenta en OpenRouter.
2. Ir a Keys.
3. Generar una API Key.
4. Guardarla en Secrets de Replit.

---

# 📂 ESTRUCTURA DE ARCHIVOS

```text
src/
├── pages/
│   ├── Home.tsx
│   ├── Entrenamiento.tsx
│   ├── Progreso.tsx
│   ├── Social.tsx
│   └── AsistenteIA.tsx
│
├── components/
│   ├── TarjetaNivel.tsx
│   ├── ReproductorVideo.tsx
│   ├── CalendarioProgreso.tsx
│   ├── GraficoProgreso.tsx
│   ├── TablaRanking.tsx
│   ├── DesafiosSemanales.tsx
│   └── ChatAsistente.tsx
│
├── hooks/
│   ├── useIA.ts
│   ├── useProgreso.ts
│   ├── useSocial.ts
│   └── useVideos.ts
│
├── lib/
│   └── localStorage.ts
│
├── contexts/
│   └── UsuarioContext.tsx
│
└── types/
    └── index.ts
```

---

# 📦 DEPENDENCIAS

```json
{
  "react": "^18.2.0",
  "react-dom": "^18.2.0",
  "typescript": "^5.0.0",
  "vite": "^5.0.0",
  "tailwindcss": "^3.4.0",
  "wouter": "^3.0.0",
  "lucide-react": "^0.300.0",
  "recharts": "^2.10.0"
}
```

Nota:

No utilizar:

```text
@huggingface/inference
```

Usar únicamente OpenRouter mediante fetch.

---

# ✅ CRITERIOS DE ACEPTACIÓN

* Sin errores TypeScript.
* Categorías y niveles funcionales.
* Videos educativos reproducibles.
* Seguimiento de progreso funcional.
* Calendario y gráficos operativos.
* IA recomienda rutinas mediante OpenRouter.
* Ranking simulado funcional.
* Compartir por WhatsApp funcional.
* Persistencia en localStorage.
* Diseño mobile-first.
* Colores energéticos:

  * Naranja.
  * Verde.
  * Azul.
* Fallback elegante si OpenRouter no responde.

---

# 📋 RESUMEN DE CAMBIOS

| Antes                            | Ahora                            |
| -------------------------------- | -------------------------------- |
| useHuggingFace                   | useIA                            |
| @huggingface/inference           | Fetch + OpenRouter               |
| VITE_HF_TOKEN                    | VITE_OPENROUTER_API_KEY          |
| microsoft/Phi-3-mini-4k-instruct | google/gemini-2.0-flash-exp:free |
| Consultando Hugging Face         | Consultando IA (OpenRouter)      |
| Error de Hugging Face            | Error de IA (OpenRouter)         |
| api-inference.huggingface.co     | openrouter.ai/api/v1             |

```
```

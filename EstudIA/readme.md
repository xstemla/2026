Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.
## NOMBRE: EstudIA

## FUNCIONALIDAD PRINCIPAL

Apoyo escolar gratuito para estudiantes de secundaria (13 a 18 años). Contenido organizado por materia y tema (currícula de Buenos Aires), videos educativos, asistente IA que responde preguntas y genera ejercicios, y seguimiento de progreso personalizado.

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
- `useContenido`: lógica de videos y temas por materia
- `useProgresoEstudio`: lógica de videos vistos, puntaje, último tema
- `useAsistente`: lógica del chat con IA contextual
- Los componentes deben ser presentacionales
---
## DEFINICIONES EXACTAS
- **MATERIAS BASE**: Matemática, Lengua, Ciencias (Biología/Química/Física), Historia
- **TEMAS**: subcategorías dentro de cada materia (ej. Matemática → Fracciones, Ecuaciones)
- **PUNTAJE**: +10 puntos por video visto, +5 por ejercicio completado
---
## LOGS OBLIGATORIOS (para debugging)
- 📚 Materia/tema seleccionado
- 🎬 Video reproducido
- 📝 Ejercicio generado por IA
- ✅ Actividad completada
- 🤖 Consultando Hugging Face...
- 🤖 IA respondió
- 💾 Progreso guardado en localStorage
- ⚠️ Error de Hugging Face
---
## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, Materias, VideoPlayer, Asistente, Progreso)

### FASE 2 - Pantalla inicial
- Selección de región: Buenos Aires (fijo por ahora)
- Selección de materia: Matemática, Lengua, Ciencias, Historia
- Selección de tema (dinámico según materia)

### FASE 3 - Contenido educativo (videos)
- Grid de videos de ejemplo (YouTube embebido) con:
 - Título, descripción, duración, materia
 - Organizados por materia y tema
- Reproductor de video que marca "visto" al finalizar

### FASE 4 - Seguimiento de progreso
- Guardar en localStorage:
 - Videos vistos
 - Puntaje total
 - Último tema visto
- Mostrar "Seguir estudiando" en home (retoma último tema)

### FASE 5 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Funciones:
 - Explicar temas con ejemplos cotidianos
 - Generar ejercicios personalizados
 - Recomendar siguiente contenido según progreso

### FASE 6 - Asistente IA (chat)
- Input de texto para preguntas del usuario
- Contexto: materia, tema, edad del usuario
- Ejemplos: "¿cómo se resuelve una ecuación?", "explicame fracciones", "dame ejercicios de álgebra"
- La IA responde en formato amigable y didáctico

### FASE 7 - Generación de ejercicios
- Botón "Practicar" en cada tema
- IA genera 3 ejercicios con solución
- Usuario puede marcar completados (suma puntaje)

### FASE 8 - Dashboard personal
- Mostrar estadísticas: puntaje total, videos vistos por materia
- Recomendación IA: "Viste fracciones, te sugiero practicar con estos ejercicios"
- Progreso visual (barras o porcentaje por materia)

---

## LOCALSTORAGE (estructura de datos)
```json
{
 "usuarioId": "usuario_demo",
 "edad": 15,
 "provincia": "Buenos Aires",
 "progreso": {
 "matematica": {
 "fracciones": { "videoVisto": true, "ejerciciosCompletados": 3 },
 "ecuaciones": { "videoVisto": false, "ejerciciosCompletados": 0 }
 },
 "lengua": {
 "comprension-lectora": { "videoVisto": true, "ejerciciosCompletados": 2 }
 }
 },
 "ultimoTema": "matematica/fracciones",
 "puntajeTotal": 125
}
```
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para explicar un tema:**

```javascript
const prompt = `
 Materia: ${materia}
 Tema: ${tema}
 Edad del usuario: ${edad} (13 a 18 años)
 Explicá el tema de forma CLARA y SENCILLA.
 Usá ejemplos de la vida cotidiana de Argentina.
 Al final, hacé 2 preguntas cortas para que el usuario compruebe si entendió.
 Formato:
 EXPLICACION: [texto]
 PREGUNTA 1: [texto]
 PREGUNTA 2: [texto]
`;
```

**Prompt para generar ejercicios:**

```javascript
const prompt = `
 Materia: ${materia}
 Tema: ${tema}
 Nivel: secundario (${edad} años)
 Generá 3 ejercicios prácticos sobre este tema.
 Incluí las soluciones al final.
 Formato:
 Ejercicio 1: [texto]
 Ejercicio 2: [texto]
 Ejercicio 3: [texto]
 Soluciones: [1: respuesta, 2: respuesta, 3: respuesta]
`;
```

**Prompt para recomendación personalizada:**

```javascript
const prompt = `
 El usuario ha visto estos temas: ${temasVistos}
 Su puntaje total es: ${puntaje}
 Según la currícula de secundaria de Buenos Aires,
 ¿qué tema debería ver a continuación?
 Respondé con el nombre de materia y tema, y una breve justificación.
`;
```
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable  
-   Usar respuestas predefinidas (fallback local) para:    
    -   Explicaciones básicas de temas comunes (fracciones, ecuación, etc.)      
    -   Ejercicios genéricos
        

### Videos de YouTube no cargan

-   Mostrar mensaje "Video no disponible temporalmente"    
-   Ofrecer explicación por IA como alternativa
    
### LocalStorage lleno o error

-   Limitar progreso a últimos 50 temas    
-   Mostrar opción de reiniciar progreso
    
----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal
-   Compatible con iPhone SE y Android Chrome
-   Botones tamaño mínimo 44x44px
-   Reproductor de video responsivo (aspect-ratio 16/9)
-   Selección de materia/tema con botones grandes
-   Chat del asistente con scroll y input fijo abajo
    
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
│   ├── Materias.tsx
│   ├── Temas.tsx
│   ├── VideoPlayer.tsx
│   ├── Asistente.tsx
│   └── Progreso.tsx
├── components/
│   ├── TarjetaMateria.tsx
│   ├── TarjetaVideo.tsx
│   ├── ReproductorVideo.tsx
│   ├── ChatAsistente.tsx
│   ├── EjercicioGenerado.tsx
│   ├── BarraProgreso.tsx
│   └── RecomendacionIA.tsx
├── hooks/
│   ├── useHuggingFace.ts
│   ├── useContenido.ts
│   ├── useProgresoEstudio.ts
│   └── useAsistente.ts
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
-   Selección de materia y tema funciona
-   Videos educativos se reproducen (embebidos de YouTube)
-   Progreso guarda videos vistos y puntaje
-   Asistente IA responde preguntas sobre temas escolares
-   IA puede generar ejercicios personalizados
-   "Seguir estudiando" retoma último tema
-   Datos persisten en localStorage
-   Diseño mobile-first con colores juveniles (celeste, naranja, violeta)
-   Fallback elegante si Hugging Face no responde

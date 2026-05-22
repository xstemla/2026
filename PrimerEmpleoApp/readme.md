Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: PrimerEmpleoApp

## FUNCIONALIDAD PRINCIPAL
Conectar a jóvenes de 16 a 18 años (con autorización de padres) con oportunidades de primer empleo en Mar del Plata. Incluye registro de perfil, sistema de puntos e insignias, asistente IA para armar CV y recomendar trabajos, y muro de oportunidades laborales.

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
- `usePerfil`: lógica de registro, perfil de usuario y localStorage
- `useOfertas`: lógica de listado de trabajos y postulaciones
- `usePuntaje`: lógica de puntos, niveles e insignias
- `useHuggingFace`: lógica de IA para armar CV, recomendar trabajos y consejos
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS
- **USUARIO**: joven de 16 a 18 años, con nombre, edad, ciudad (Mar del Plata), intereses laborales
- **PUNTOS**: se suman al completar trabajos (ej. 50 puntos por trabajo)
- **NIVELES**: Principiante (0-100), Intermedio (101-300), Avanzado (301+)
- **INSIGNIAS**: logros automáticos (Primera aplicación, Primer trabajo, 3 trabajos completados, etc.)

---

## LOGS OBLIGATORIOS (para debugging)
- 📝 Usuario registrado: [nombre], [edad]
- 💼 Oferta visualizada: [título]
- 📩 Postulación a oferta: [id]
- ⭐ Puntos sumados: +[cantidad], nuevo nivel: [nivel]
- 🏆 Insignia desbloqueada: [nombre]
- 🤖 Consultando Hugging Face para CV...
- 🤖 Consultando Hugging Face para recomendación...
- 🤖 IA respondió
- ⚠️ Error de Hugging Face

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Registro, MuroOfertas, Perfil, AsistenteIA)

### FASE 2 - Registro de usuario
- Formulario con: nombre, edad (16-18), ciudad (Mar del Plata fijo o selector), intereses laborales (checkbox: atención al cliente, ventas, tecnología, etc.)
- Checkbox "Autorizo con autorización de mis padres" (obligatorio)
- Guardar perfil en localStorage

### FASE 3 - Muro de oportunidades laborales
- Array mock de ofertas (id, título, empresa, descripción, requisitos, paga estimada, horario)
- Cada oferta tiene botón "Aplicar"
- Al aplicar, registrar en localStorage (evitar postulaciones duplicadas)

### FASE 4 - Sistema de puntos, niveles e insignias
- Calcular puntos totales según trabajos completados (mock: al "aplicar" se simula completado para pruebas)
- Definir niveles: Principiante (0-100), Intermedio (101-300), Avanzado (301+)
- Insignias predefinidas:
 - "Primera aplicación" (al postular a primera oferta)
 - "Primer trabajo" (al primer trabajo completado)
 - "Trabajador constante" (3 trabajos completados)
 - "Experto local" (5 trabajos)
- Mostrar insignias en perfil

### FASE 5 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Funciones:
 - Asistente para armar CV paso a paso
 - Recomendador de trabajos según perfil
 - Consejos para entrevistas

### FASE 6 - Asistente IA para armar CV
- Interfaz de chat simple o guía paso a paso
- IA pregunta: "¿Cuáles son tus habilidades?", "¿Qué materias te gustan?", "¿Tuviste alguna experiencia escolar relevante?"
- Genera texto de CV personalizado
- Guardar CV generado en localStorage (opcional)

### FASE 7 - Recomendador de trabajos por IA
- Botón "Recomendarme trabajos" en el muro
- IA recibe perfil (edad, intereses) y sugiere qué tipo de ofertas buscar
- Puede filtrar el listado de ofertas mock mostrando primero las más compatibles

### FASE 8 - Perfil público y compartir
- Pantalla de perfil con: nombre, edad, nivel, puntos, insignias, CV generado
- Botón "Compartir perfil" → abre WhatsApp con mensaje predefinido y datos del perfil
- Botón "Editar perfil" (permite cambiar intereses)

---

## LOCALSTORAGE (estructura de datos)
```json
{
 "perfil": {
 "id": 1715678901234,
 "nombre": "Juan",
 "edad": 17,
 "ciudad": "Mar del Plata",
 "intereses": ["atencion al cliente", "ventas"],
 "autorizacionPadres": true,
 "fechaRegistro": "2025-05-20"
 },
 "postulaciones": [
 { "ofertaId": 1, "fecha": "2025-05-20", "completado": true },
 { "ofertaId": 2, "fecha": "2025-05-21", "completado": false }
 ],
 "puntaje": 150,
 "insignias": ["Primera aplicación"],
 "cvGenerado": "Mi nombre es Juan, tengo 17 años...",
 "ultimaRecomendacionIA": "Según tu perfil, podrías buscar trabajos de atención al cliente..."
}
```
----------

## OFERTAS LABORALES (mock)

```javascript
const ofertasMock = [
 { id: 1, titulo: "Cajero/a", empresa: "Supermercado La Anónima", descripcion: "Atención al público y manejo de caja.", requisitos: "Secundario en curso, responsable", paga: "$2000 por hora", horario: "4h diarias", zona: "Centro" },
 { id: 2, titulo: "Cadete", empresa: "Motorboy", descripcion: "Reparto en moto (no requiere moto propia).", requisitos: "Licencia de moto, secundario en curso", paga: "$1500 por hora + propinas", horario: "3h diarias", zona: "Playa Grande" },
 { id: 3, titulo: "Atención al cliente", empresa: "McDonald's", descripcion: "Atención en mostrador y armado de pedidos.", requisitos: "Secundario en curso, buena predisposición", paga: "$1800 por hora", horario: "Rotativo", zona: "Centro" }
];
```
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para armar CV:**
```javascript
const prompt = `
 El usuario es un joven de ${edad} años, vive en ${ciudad}, y tiene estos intereses: ${intereses}.
 Sus habilidades mencionadas: ${habilidades}.
 Ayudalo a armar su primer CV para buscar trabajo.
 Respondé en formato amigable y motivador con:
 1. Cómo presentarse (2 líneas)
 2. Qué habilidades destacar (lista corta)
 3. Qué decir si no tiene experiencia previa (1 párrafo)
`;
```

**Prompt para recomendar trabajos:**

```javascript
const prompt = `
 Perfil del usuario:
 - Edad: ${edad}
 - Intereses: ${intereses}
 - Ciudad: ${ciudad}
 Según su perfil, ¿qué tipo de trabajos de primer empleo le recomendarías?
 Respondé con 3 sugerencias específicas (ej. "atención al cliente en locales de comida rápida").
 Explicá brevemente por qué cada una es adecuada.
`;
```

**Prompt para consejos de entrevista:**

```javascript
const prompt = `
 El usuario va a tener su primera entrevista laboral.
 Edad: ${edad}, postula a trabajos de: ${intereses}.
 DALE 3 consejos prácticos y específicos para destacar en la entrevista.
 Respondé de forma directa y útil.
`;
```
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable
-   Usar respuestas predefinidas (fallback local) para:   
    -   CV genérico ("Presentate con tu nombre, destacá tus ganas de aprender...")        
    -   Recomendaciones basadas en intereses (ej. si intereses incluyen "ventas" → sugerir comercios)
        
### Registro incompleto o edad inválida

-   Validar que edad esté entre 16 y 18    
-   Forzar checkbox de autorización de padres
    
### localStorage lleno o error

-   Limitar historial de postulaciones (mostrar últimas 20)    
-   Mostrar opción de limpiar datos
    
----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE y Android Chrome   
-   Botones grandes (mínimo 44x44px) para aplicar a ofertas   
-   Tarjetas de ofertas con información legible    
-   Formularios con campos que ocupan todo el ancho    
-   Insignias visibles pero no abrumadoras en perfil
    
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
│   ├── Registro.tsx
│   ├── MuroOfertas.tsx
│   ├── Perfil.tsx
│   └── AsistenteIA.tsx
├── components/
│   ├── TarjetaOferta.tsx
│   ├── FormularioRegistro.tsx
│   ├── Insignias.tsx
│   ├── BarraPuntos.tsx
│   ├── AsistenteCV.tsx
│   └── RecomendadorTrabajos.tsx
├── hooks/
│   ├── usePerfil.ts
│   ├── useOfertas.ts
│   ├── usePuntaje.ts
│   └── useHuggingFace.ts
├── lib/
│   └── localStorage.ts
├── contexts/
│   └── PerfilContext.tsx
├── data/
│   └── ofertasMock.ts
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
-   Usuario puede registrarse con nombre, edad, intereses y autorización de padres   
-   Muro muestra ofertas mock y permite aplicar    
-   Al aplicar, suma puntos y desbloquea insignias    
-   Perfil muestra nivel, puntos e insignias obtenidas    
-   IA puede armar CV personalizado según perfil    
-   IA puede recomendar trabajos según intereses    
-   Datos persisten en localStorage    
-   Diseño mobile-first con colores profesionales juveniles (azul, celeste, blanco)    
-   Fallback elegante si Hugging Face no responde

Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: DesperdicioCero

## FUNCIONALIDAD PRINCIPAL

Ayudar a evitar el desperdicio de comida mediante IA: escanear productos (simulado), recibir recetas con ingredientes disponibles, tips para residuos orgánicos, y un foro comunitario con gamificación.

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

- `useHuggingFace`: toda la lógica de comunicación con Hugging Face API
- `useProductos`: lógica de productos escaneados (guardar en localStorage)
- `useGamificacion`: lógica de puntajes y ranking
- `useForo`: lógica de publicación de tips
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS

- **PRODUCTO PRÓXIMO A VENCER**: fecha de vencimiento < 3 días desde hoy
- **COMIDA SALVADA**: cuando el usuario marca que usó un producto antes de vencer
- **DINERO AHORRADO**: valor estimado por producto salvado (ej. $500 por comida)

---

## LOGS OBLIGATORIOS (para debugging)

- 📷 Producto escaneado / ingresado
- 🤖 Consultando Hugging Face...
- 🤖 IA respondió
- 💾 Producto guardado en localStorage
- ⭐ Puntaje actualizado: +X puntos
- 🗣️ Nuevo tip publicado en foro
- ⚠️ Error de Hugging Face

---
## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, Escanear, Recetas, Foro, Ranking)

### FASE 2 - Escaneo de productos (simulado)
- Input de texto para código de producto (simula QR)
- Botón para subir foto (reconocimiento con IA)
- Guardar producto en localStorage con fecha de escaneo y vencimiento estimado

### FASE 3 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: microsoft/Phi-3-mini-4k-instruct
- Variable: VITE_HF_TOKEN
- Funciones:
 - Identificar producto por nombre
 - Sugerir fecha de vencimiento aproximada
 - Recomendar recetas con productos próximos a vencer
 
### FASE 4 - Recetas inteligentes
- Input para que el usuario ingrese ingredientes disponibles
- IA genera recetas con esos ingredientes
- Mostrar recetas en formato amigable (nombre + pasos cortos)

### FASE 5 - Tips para residuos orgánicos
- Sección con ideas predefinidas (compostaje, reutilización de cáscaras)
- El usuario puede preguntar "¿qué hago con X?" y la IA responde

### FASE 6 - Comunidad / Foro con IA
- Publicar tips (texto + nombre de usuario)
- Guardar tips en localStorage
- Asistente IA que responde preguntas en el foro

### FASE 7 - Gamificación (Ranking)
- Sistema de puntuación:
 - +100 puntos por cada "comida salvada"
 - +50 puntos por publicar tip
 - +10 puntos por día sin desperdicio registrado
- Tabla de posiciones con datos simulados de otros usuarios

### FASE 8 - Dashboard personal
- Mostrar estadísticas: comidas salvadas, dinero ahorrado, puntos
- Lista de productos escaneados recientemente
- Botón para marcar producto como "usado" (suma puntos)

---

## LOCALSTORAGE (estructura de datos)
```json
{
 "usuarioId": "usuario_demo",
 "productos": [
 {
 "id": "123456",
 "nombre": "Leche",
 "fechaEscaneo": "2025-05-20",
 "fechaVencimiento": "2025-05-25",
 "usado": false
 }
 ],
 "estadisticas": {
 "comidasSalvadas": 3,
 "dineroAhorrado": 1500,
 "puntos": 350
 },
 "tips": [
 {
 "id": "1",
 "autor": "Usuario",
 "texto": "Cómo hacer compost en casa",
 "fecha": "2025-05-20"
 }
 ],
 "rankingUsuarios": [
 { "nombre": "Ana", "puntos": 1250 },
 { "nombre": "Luis", "puntos": 980 },
 { "nombre": "Usuario", "puntos": 350 }
 ]
}
```
----------

## HUGGING FACE IA (detalles específicos)

**Prompt para identificación de producto:**

```javascript
const prompt = `
 Producto: ${nombreProducto}
 Respondé solo en formato JSON:
 { "nombre": "nombre del producto", "vencimientoEstimadoDias": X }
 donde X es cantidad de días hasta vencimiento (default 7).
 Respondé solo el JSON, nada más.
`;
```

**Prompt para recetas:**
```javascript
const prompt = `
 Ingredientes disponibles: ${ingredientes}
 Productos próximos a vencer: ${productosProximos}
 Generá 2 recetas que usen estos ingredientes.
 Formato exacto:
 Receta 1: [nombre] - [pasos cortos]
 Receta 2: [nombre] - [pasos cortos]
 Consejo anti-desperdicio: [texto]
`;
```

**Prompt para residuos:**
```javascript
const prompt = `
 El usuario pregunta sobre residuos orgánicos: ${pregunta}
 Respondé con tips prácticos para reutilizar en casa.
 Sé breve, amigable y útil.
`;
```

**Prompt para asistente del foro:**
```javascript
const prompt = `
 El usuario pregunta en el foro: ${pregunta}
 Contexto: es una comunidad sobre evitar desperdicio de comida.
 Respondé de forma útil y alentadora.
`;
```
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Mostrar mensaje amigable    
-   Usar respuestas predefinidas (fallback local) para:   
    -   Recetas comunes (tortilla, pan francés, ensaladas)        
    -   Tips de compostaje básico       
    -   Identificación de productos comunes
        

### Cámara no disponible
-   Usar entrada de texto como alternativa principal  
-   Mostrar mensaje: "Podés escribir el nombre del producto"
    

### LocalStorage lleno o error

-   Limitar a últimos 50 productos   
-   Mostrar opción de limpiar datos viejos
    
----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal    
-   Compatible con iPhone SE y Android Chrome    
-   Botones tamaño mínimo 44x44px
-   Inputs grandes para facilitar escritura   
-   Tarjetas de recetas fáciles de leer en pantallas chicas
    
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
│   ├── Escanear.tsx
│   ├── Recetas.tsx
│   ├── Foro.tsx
│   └── Ranking.tsx
├── components/
│   ├── TarjetaProducto.tsx
│   ├── TarjetaReceta.tsx
│   ├── FormularioTip.tsx
│   ├── TablaRanking.tsx
│   └── Estadisticas.tsx
├── hooks/
│   ├── useHuggingFace.ts
│   ├── useProductos.ts
│   ├── useGamificacion.ts
│   └── useForo.ts
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
-   Escaneo de productos (simulado con texto) funciona    
-   IA genera recetas según ingredientes  
-   Foro permite publicar tips y verlos en lista   
-   Ranking acumula puntos por acciones  
-   Datos persisten en localStorage entre sesiones    
-   Diseño mobile-first con tonos verdes/naturales
-   Fallback elegante si Hugging Face no responde

Creá una aplicación web con React 18 + TypeScript + Vite + Tailwind CSS.

## NOMBRE: TubularApp

## FUNCIONALIDAD PRINCIPAL
App de animación con IA que permite a dibujantes y creadores generar animaciones a partir de secuencias de dibujos (fotogramas). El usuario sube una serie de dibujos en orden (ej. posición 1, 1.1, 2, etc.) y la IA genera una animación fluida. Incluye red social para conectar actores de doblaje con animadores, y exportación de audio para proyectos de actuación de voz.

---

## RESTRICCIONES (OBLIGATORIO RESPETAR)
- NO usar backend propio
- NO usar Firebase
- NO usar Redux, NO usar Zustand
- NO agregar autenticación real (simulada)
- NO agregar funcionalidades fuera del MVP
- Mantener arquitectura simple
- Priorizar estabilidad sobre features

---

## ARQUITECTURA (DESACOPLADO)

- `useHuggingFace`: lógica de IA para interpolación de fotogramas y generación de animación
- `useAnimacion`: lógica de secuencia de dibujos (subir, ordenar, previsualizar)
- `useRedSocial`: lógica de perfiles, publicaciones y conexión entre animadores y actores de doblaje
- `useAudio`: lógica de grabación y exportación de audio
- Los componentes deben ser presentacionales

---

## DEFINICIONES EXACTAS

- **FOTOGRAMA**: cada dibujo individual que el usuario sube (parte de una secuencia)
- **SECUENCIA**: conjunto ordenado de fotogramas (ej. 1, 1.1, 2, 2.1, 3...)
- **INTERPOLACIÓN**: proceso por el cual la IA genera fotogramas intermedios para suavizar la animación
- **ANIMACIÓN**: resultado final (video o GIF) generado por la IA
- **ACTOR DE DOBLAJE**: usuario que ofrece servicios de voz para animaciones
---

## LOGS OBLIGATORIOS (para debugging)
- 🎨 Usuario subió fotograma: [orden]
- 🤖 IA generando interpolación...
- 🎬 Animación generada exitosamente
- 📤 Animación exportada (formato: video/GIF)
- 🎙️ Audio exportado para doblaje
- 👥 Publicación en red social creada
- 💾 Proyecto guardado en localStorage
- ⚠️ Error de Hugging Face

---

## IMPLEMENTACIÓN POR FASES

### FASE 1 - Setup base
- React + Vite + TypeScript + Tailwind
- Routing con wouter (Home, Animacion, RedSocial, Audio, Perfil)

### FASE 2 - Onboarding y perfil
- Usuario elige rol: "Animador" o "Actor de doblaje" (o ambos)
- Completar perfil: nombre, experiencia, portafolio (enlaces o descripción)
- Guardar en localStorage

### FASE 3 - Estudio de animación (core)
- Interfaz para subir dibujos en secuencia (arrastrar o seleccionar archivos)
- Ordenar fotogramas (numerar: 1, 1.1, 2, 2.1, etc.)
- Previsualización de la secuencia
- Botón "Generar animación con IA"

### FASE 4 - Integración con Hugging Face IA
- SDK: @huggingface/inference
- Modelo: (para interpolación de imágenes o generación de video, se puede usar un modelo de código abierto como stabilityai/stable-diffusion o modelos de frame interpolation - alternativamente usar API de Hugging Face para video)
- Variable: VITE_HF_TOKEN
- **Nota**: La interpolación de fotogramas es compleja. Para el MVP, se puede simular con una interpolación lineal básica en el frontend (mostrar transición de opacidad entre imágenes) o usar un modelo de Hugging Face como `google/frame-interpolation` si está disponible. En el prompt se describe la funcionalidad deseada.
**Función de interpolación simulada (fallback):**
- Tomar dos imágenes (fotograma A y B)
- Generar N fotogramas intermedios combinando píxeles (simplificado)
- El resultado final es un GIF animado o video corto

### FASE 5 - Exportación de animación y audio
- Exportar animación como GIF o MP4 (simulado: mostrar vista previa y opción de "descargar" que genera un archivo mock)
- Grabar audio: botón "Grabar voz" (usar MediaRecorder API)
- Asociar audio a una animación o personaje
- Exportar audio como MP3/WAV (simulado)

### FASE 6 - Red social para creadores
- Muro de publicaciones:
 - Animadores muestran sus animaciones generadas
 - Actores de doblaje ofrecen sus servicios (suben muestras de voz)
- Buscar por rol, experiencia, tipo de proyecto
- Botón "Contactar" (simulado: muestra mensaje "Se enviaría un mensaje a [usuario]")
- Perfiles públicos con portafolio

### FASE 7 - Colaboración entre animadores y actores
- Animador publica un casting: "Busco actor de doblaje para personaje X"
- Actor responde con una muestra
- Sistema de mensajería interno (simulado)
- Guardar conversaciones en localStorage

### FASE 8 - Proyectos y portafolio
- Usuario puede guardar proyectos (secuencias de dibujos + animación generada)
- Mostrar portafolio público en el perfil
- Opción de "Compartir en redes" (WhatsApp, Twitter simulado)

---

## LOCALSTORAGE (estructura de datos)
```json
{
 "usuario": {
 "id": 123456,
 "nombre": "Ana",
 "rol": "animador",
 "experiencia": "2 años",
 "portafolio": ["animacion1", "animacion2"],
 "contacto": "animadora.ana@email.com"
 },
 "proyectos": [
 {
 "id": 1,
 "nombre": "Mi primera animación",
 "secuencia": ["img1_base64", "img2_base64", "img3_base64"],
 "orden": [1, 2, 3],
 "animacionGenerada": "gif_base64",
 "audioAsociado": "audio_base64",
 "fecha": "2025-05-22"
 }
 ],
 "publicaciones": [
 {
 "id": 1,
 "usuarioId": 123456,
 "tipo": "animacion",
 "contenido": "gif_base64",
 "descripcion": "Mi primera animación con IA",
 "fecha": "2025-05-22"
 }
 ],
 "castings": [
 {
 "id": 1,
 "animadorId": 123456,
 "descripcion": "Busco voz para personaje principal",
 "respuestas": []
 }
 ],
 "mensajes": [
 {
 "from": 123456,
 "to": 789012,
 "texto": "Hola, me interesa tu trabajo",
 "fecha": "2025-05-22"
 }
 ]
}
```
----------

## HUGGING FACE IA (detalles específicos)

**Para interpolación de fotogramas (ideal):**

```javascript
// Hugging Face tiene modelos de frame interpolation como "google/frame-interpolation"
// En el MVP se puede simular una interpolación básica en el frontend.
// El prompt describe la funcionalidad deseada.
```

**Prompt para describir la funcionalidad al Replit Agent:**
```javascript
// La app debe tener una función "generarAnimacion(secuenciaImagenes)" que:
// 1. Reciba un array de imágenes en orden (Base64)
// 2. Genere fotogramas intermedios (puede ser una interpolación simple de opacidad)
// 3. Devuelva un GIF animado o video corto
// 4. Si se integra con Hugging Face, usar modelo de interpolación de frames
```

**Para la red social y matching (simulado):**

```javascript
// No se usa IA compleja, solo búsqueda por etiquetas y roles
```
----------

## MANEJO DE ERRORES (OBLIGATORIO)

### Hugging Face falla o timeout

-   Usar interpolación básica en el frontend (transición lineal)   
-   Mostrar mensaje: "Usando modo offline. La animación será más básica."
    

### Imágenes muy grandes

-   Redimensionar a máximo 500x500px antes de guardar
    

### Audio no grabado

-   Usar librería de MediaRecorder con fallback a input de archivo de audio
    

### localStorage lleno o error

-   Limitar cantidad de proyectos guardados (últimos 5)  
-   Ofrecer exportar proyecto como JSON
    

----------

## MOBILE (OBLIGATORIO)

-   Evitar overflow horizontal   
-   Compatible con iPhone SE y Android Chrome   
-   Botones grandes (mínimo 44x44px) para subir dibujos y generar animación   
-   Galería de fotogramas con scroll horizontal    
-   Subida de imágenes: acceso a cámara y galería   
-   Grabación de audio: acceso a micrófono
    

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
│   ├── Animacion.tsx
│   ├── RedSocial.tsx
│   ├── Audio.tsx
│   └── Perfil.tsx
├── components/
│   ├── SubirFotogramas.tsx
│   ├── InterpoladorIA.tsx
│   ├── VisorAnimacion.tsx
│   ├── GrabadoraAudio.tsx
│   ├── PublicacionRedSocial.tsx
│   ├── CastingCard.tsx
│   └── Mensajeria.tsx
├── hooks/
│   ├── useHuggingFace.ts
│   ├── useAnimacion.ts
│   ├── useRedSocial.ts
│   └── useAudio.ts
├── lib/
│   ├── localStorage.ts
│   └── interpoladorBasico.ts
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
-   Usuario puede subir secuencia de dibujos (mínimo 3 fotogramas)   
-   La IA (o simulación) genera una animación fluida entre fotogramas    
-   Usuario puede exportar animación (GIF/MP4 simulado)    
-   Usuario puede grabar y exportar audio (asociado a animación)   
-   Red social: animadores publican animaciones, actores ofrecen servicios    
-   Sistema de castings y mensajería (simulado)    
-   Datos persisten en localStorage   
-   Diseño mobile-first con colores creativos (morado, rosa, celeste)   
-   Fallback elegante si Hugging Face no responde




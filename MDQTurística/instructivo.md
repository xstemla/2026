# 🌊 MDQTurística - App con IA para potenciar el turismo en Mar del Plata

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para el chatbot IA)
- [ ] Una cuenta en **Supabase** (gratis, para guardar negocios, reportes y calificaciones)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---
## 🎯 Qué hace esta app
Es una plataforma que busca convertir a **Mar del Plata** en la principal ciudad turística durante todo el año (no solo en verano). La app tiene **tres perfiles de usuario**:

| Perfil | Qué puede hacer |
| :--- | :--- |
| 🧳 **Turista** | Encontrar entretenimiento, hospedaje, transporte, gastronomía, emergencias, compras y servicios |
| 🏙️ **Ciudadano** | Reportar basura, coordinar limpieza, actividades sociales, llamar a emergencias |
| 💼 **Emprendedor** | Hacer publicidad, mejorar su reputación, recibir feedback, acceder a incentivos municipales |

Un **asistente de IA (chatbot)** ayuda a todos los usuarios en tiempo real.

---
## 🛠️ Herramientas (todo desde el navegador)

| Herramienta | Link | Para qué |
| :--- | :--- | :--- |
| **Replit** | replit.com | Escribir y ejecutar el código |
| **Hugging Face** | huggingface.co | IA gratuita para el chatbot |
| **Supabase** | supabase.com | Base de datos (negocios, reportes, calificaciones) |
| **Vercel** | vercel.com | Publicar la app gratis |
| **PWABuilder** | pwabuilder.com | Convertir la app en APK |

✅ **No se instala nada en la computadora.**

---
## 🚀 Paso a paso

### 1. Crear las cuentas gratuitas (5 minutos)

**A. Hugging Face** (el chatbot IA)
- Entrar a [huggingface.co](https://huggingface.co)
- Registrarse con email
- Ir a **Settings** → **Access Tokens** → **New token** → copiar el token
- 
**B. Supabase** (la base de datos)
- Entrar a [supabase.com](https://supabase.com)
- "Start your project" → crear nuevo proyecto
- En **SQL Editor**, ejecutar el código SQL que está en el archivo `readme.md` (sección SUPABASE)
- Ir a **Database** → **Replication** → habilitar las tablas: `negocios`, `reportes`, `promociones`, `actividades`
- Ir a **Project Settings** → **API** → copiar `URL` y `anon public key`
### 2. Crear el proyecto en Replit
- Entrar a [replit.com](https://replit.com/)
- Click en **"Create new Repl"** → **"Create with AI"**
### 3. Configurar los "Secretos" (Keys)
En Replit, ir a **Tools** → **Secrets** (🔒) y agregar:
| Secret | Valor |
|--|--|
| `VITE_HF_TOKEN` | El token que copiaste de Hugging Face |
| `VITE_SUPABASE_URL` | La URL de Supabase |
| `VITE_SUPABASE_ANON_KEY` | La clave anónima de Supabase |

### 4. Copiar el prompt
Abrir el archivo `readme.md` de este proyecto y **copiar TODO su contenido**.
En Replit, pegar el prompt en el chat del **"Replit Agent"** y esperar a que genere la app.

### 5. Ver la app funcionando
A la derecha de la pantalla aparece una vista previa. Probá los tres perfiles, el mapa y el chatbot.

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://mdq-turistica.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a usar la app según su perfil

---

## 📱 Cómo se usa en el día a día
| Perfil | El usuario hace... | La app hace... |
|--|--|--|
| 🧳 **Turista** | Busca "restaurantes cerca" | Mapa con opciones, calificaciones y cómo llegar |
| 🧳 **Turista** | Pregunta "¿Qué hacer hoy?" | IA sugiere eventos y lugares según clima/temporada |
| 🏙️ **Ciudadano** | Ve basura en la calle | Toma foto, reporta ubicación, el municipio recibe la alerta |
| 🏙️ **Ciudadano** | Quiere participar de una limpieza de playa | Ve actividades sociales y se suma |
| 💼 **Emprendedor** | Registra su negocio | Aparece en las búsquedas de turistas |
| 💼 **Emprendedor** | Sube una promoción | Los turistas la ven en su feed |
| Cualquiera | Pregunta al asistente IA | Chatbot responde al instante |

> 🌊 La app conecta a turistas, ciudadanos y emprendedores para mejorar Mar del Plata.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Asistente virtual (chatbot)** | Responde preguntas sobre turismo, eventos, transporte, emergencias |
| **Recomendación personalizada** | Según el perfil y búsquedas previas, sugiere lugares o actividades |
| **Moderación de reputación** | Analiza comentarios y calificaciones para detectar falsos o spam |
| **Ayuda a emprendedores** | Sugiere cómo mejorar su reputación según feedback negativo |
| **Emergencias** | Reconoce palabras clave ("robo", "accidente") y sugiere llamar al 911 |

**Prompt que usa la IA internamente (chatbot):**
```javascript
const prompt = `
 El usuario es: ${perfil} (Turista/Ciudadano/Emprendedor)
 Pregunta: ${pregunta}
 Ubicación aproximada: ${zona}
 Respondé de forma amigable, útil y específica para Mar del Plata.
 Si no sabés algo, sugerí llamar al 147 (municipio) o al 911 (emergencias).
`;
```
----------

## 💰 Costos

| Servicio | Costo |
|--|--|
| Replit | $0 |
| Hugging Face | $0 |
| Supabase | $0 |
| Vercel | $0 |
| PWABuilder | $0 |
| **TOTAL** | **$0** |


----------

## ❓ Problemas comunes

| Problema | Solución |
|--|--|
| **El mapa no carga** | Verificar que las coordenadas en la base de datos sean correctas |
| **Los reportes de basura no llegan a nadie** | En la versión inicial son simulados. Para versión real, conectar con API del municipio  | 
| **La reputación del emprendedor puede ser manipulada** | Agregar verificación de que quien califica haya visitado el negocio (por geolocalización) |
| **El chatbot no responde** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado |


----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face y Supabase, construimos una app para convertir a Mar del Plata en la principal ciudad turística durante todo el año. Turistas encuentran servicios, ciudadanos reportan problemas y emprendedores mejoran su reputación, todo con un asistente de IA que responde preguntas en tiempo real. Todo gratis, todo funciona, pensado para nuestra ciudad."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT

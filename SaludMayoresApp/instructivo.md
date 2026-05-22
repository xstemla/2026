# 👴 SaludMayoresApp - App con IA para adultos mayores en Mar del Plata

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace esta app
Ayuda a adultos mayores de Mar del Plata a conseguir medicamentos y turnos médicos de manera fácil, sin tener que recorrer muchas farmacias ni hacer largas filas. La app incluye:
- **Búsqueda de medicamentos**: mapa con farmacias cercanas que tienen stock del medicamento que necesitás
- **Contacto directo**: botón para llamar a la farmacia o al médico
- **Turnos médicos**: listado de especialidades y profesionales con contacto
- **IA amigable**: corrige nombres de medicamentos, da recordatorios de horarios y responde preguntas simples
- **Diseño accesible**: fuentes GRANDES, botones GRANDES, modo alto contraste

> 👴 La app fue pensada para que los adultos mayores puedan usarla sin ayuda.

---

## 🛠️ Herramientas (todo desde el navegador)
| Herramienta | Link | Para qué |
| :--- | :--- | :--- |
| **Replit** | replit.com | Escribir y ejecutar el código |
| **Hugging Face** | huggingface.co | IA gratuita |
| **Vercel** | vercel.com | Publicar la app gratis |
| **PWABuilder** | pwabuilder.com | Convertir la app en APK |

✅ **No se instala nada en la computadora.**

---
## 🚀 Paso a paso

### 1. Crear las cuentas gratuitas (5 minutos)

**A. Hugging Face** (la IA)
- Entrar a [huggingface.co](https://huggingface.co)
- Registrarse con email
- Ir a **Settings** → **Access Tokens** → **New token** → copiar el token

**B. Replit** (el editor de código)
- Entrar a [replit.com](https://replit.com/)
- Registrarse con Google o GitHub

> ⚠️ **SaludMayoresApp NO necesita Supabase**. Los recordatorios y preferencias se guardan en el celular (localStorage). El mapa usa Leaflet (OpenStreetMap), no requiere API key.

### 2. Crear el proyecto en Replit
- Click en **"Create new Repl"** → **"Create with AI"**

### 3. Configurar los "Secretos" (Keys)
En Replit, ir a **Tools** → **Secrets** (🔒) y agregar:
| Secret | Valor |
|--|--|
| `VITE_HF_TOKEN` | El token que copiaste de Hugging Face |

### 4. Copiar el prompt
Abrir el archivo `readme.md` de este proyecto y **copiar TODO su contenido**.
En Replit, pegar el prompt en el chat del **"Replit Agent"** y esperar a que genere la app.

### 5. Ver la app funcionando
A la derecha de la pantalla aparece una vista previa. Probá:
- **Buscar medicamento**: escribí "losartán" o "aspirina" (datos mock)
- Ver el mapa con farmacias que tienen stock
- Tocar "Llamar" (simulado, en celular real abriría el teléfono)
- **Pedir turno**: elegí una especialidad y llamá al profesional
- **Recordatorios**: agregá un medicamento con horario y probá la notificación
- **Consultar IA**: preguntá "¿qué hago si me duele el pecho?" o "¿cómo tomar losartán?"
- **Accesibilidad**: activá "Modo alto contraste" y aumentá el tamaño de fuente

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://salud-mayores-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Pueden ayudar a sus familiares mayores a usar la app

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| **Necesita un medicamento** | Toca "Buscar medicamento" y escribe el nombre | Muestra mapa con farmacias que tienen stock |
| **Quiere llamar a la farmacia** | Toca el botón de llamada | Abre el teléfono con el número listo |
| **Necesita un turno** | Toca "Pedir turno médico" y elige especialidad | Muestra especialistas con contacto |
| **Se olvida la medicación** | Configura recordatorio | La IA recuerda a qué hora tomar cada medicamento |
| **Tiene dudas** | Pregunta a la IA | Responde con consejos simples |

> 💡 La app fue pensada para que los adultos mayores puedan usarla sin ayuda.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Corrección de medicamentos** | Si el usuario escribe mal el nombre, sugiere la corrección |
| **Recordatorios de medicación** | "Son las 20 hs, es hora de tomar la pastilla" |
| **Consejos médicos** | "¿Qué preguntas hacerle al cardiólogo?" |
| **Simplificación de lenguaje** | Traduce términos médicos complejos a palabras simples |

**Prompt que usa la IA internamente (ejemplo para consejos):**
```javascript
const prompt = `
 El usuario (adulto mayor) pregunta: "${pregunta}"
 Respondé de forma CLARA y SIMPLE:
 1. Respuesta simple (una oración)
 2. Paso a paso (máximo 3 pasos)
 3. Qué hacer si no entiende
`;
```
----------

## 💰 Costos

| Servicio | Costo |
|--|--|
| Replit | $0 |
| Hugging Face | $0 |
| Vercel | $0 |
| PWABuilder | $0 |
| **TOTAL** | **$0** |

----------

## ❓ Problemas comunes

| Problema | Solución |
|--|--|
| **El usuario mayor no ve bien la pantalla** | La app tiene fuentes grandes (18px+) y modo alto contraste |
| **No sabe escribir el medicamento** | La IA corrige automáticamente el nombre |
| **El mapa no carga** | Verificar conexión a internet. Leaflet no requiere API key. |
| **Los recordatorios no se ven** | Son simulados (toast o alert en pantalla). Revisar que estén guardados. |
| **La IA no responde** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app accesible para adultos mayores en Mar del Plata. Les ayuda a encontrar medicamentos en farmacias cercanas, pedir turnos médicos, recordar horarios de medicación y resolver dudas con IA. Diseñada con fuentes grandes, botones simples y modo alto contraste. Todo gratis, pensado para ellos."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT

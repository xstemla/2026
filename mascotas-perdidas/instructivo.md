# 🐾 MascotasApp - App con IA para mascotas perdidas en Mar del Plata

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace esta app
Ayuda a los habitantes de Mar del Plata a encontrar mascotas perdidas rápidamente. La app permite:
- Publicar mascotas perdidas o encontradas (con foto, zona, contacto)
- Ver todas las publicaciones en un mapa interactivo
- Recibir alertas por zona (simuladas) cuando alguien publica en tu barrio
- Pedir consejos a la IA según la situación (qué hacer si se perdió o si encontraste un animal)

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

> ⚠️ **MascotasApp NO necesita Supabase**. Las publicaciones se guardan en el celular (localStorage). El mapa usa Leaflet (OpenStreetMap), no requiere API key.

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
- Publicar una mascota perdida (ej. "Perro llamado Luna en Centro")
- Ver cómo aparece en el mapa (marcador rojo)
- Publicar una mascota encontrada (ej. "Gato en Playa Grande") → marcador verde
- Suscribirte a una zona y crear una publicación en esa zona para ver la alerta
- Pedir consejos a la IA: "Se me perdió mi perro, ¿qué hago?"

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://mascotas-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a reportar mascotas perdidas o encontradas en Mar del Plata

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| **Se perdió su mascota** | Toca "Perdí mi mascota" y completa el formulario | Guarda la publicación y la muestra en el mapa |
| **Encuentra una mascota** | Toca "Encontré una mascota" y carga los datos | Publica y notifica a suscriptores de la zona |
| **Quiere ayudar** | Mira el mapa y ve publicaciones cercanas | Muestra marcadores con fotos y datos |
| **Recibe una alerta** | (Automático) | La app muestra un cartel: "Nueva mascota perdida en tu zona" |
| **Necesita consejos** | Toca "Consejos IA" y describe su situación | Gemini recomienda qué hacer |

> 🐕 La app conecta a toda la comunidad de Mar del Plata para encontrar mascotas más rápido.
---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Tips para mascotas perdidas** | Responde: "¿Qué hago si se perdió mi perro? Dame consejos paso a paso" |
| **Consejos al encontrar un animal** | "Encontré un gato abandonado, ¿qué debo hacer?" |
| **Recomendaciones según especie** | Si es perro, gato, conejo, etc., la IA da consejos específicos |
| **Análisis de urgencia** | Evalúa si el caso es prioritario (animal herido, cachorro, etc.) |

**Prompt que usa la IA internamente (consejos):**
```javascript
const prompt = `
 Situación: ${situacion} (perdida/encontrada/abandonada)
 Especie: ${especie}
 Zona: ${zona}
 Descripción adicional: ${descripcion}
 Respondé en este formato:
 Prioridad: [Alta/Media/Baja]
 Consejo 1: [texto corto]
 Consejo 2: [texto corto]
 Consejo 3: [texto corto]
 Contacto sugerido: [protectora, zoonosis o veterinaria de Mar del Plata]
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
| **El mapa no carga** | Verificar que Leaflet esté bien importado. No necesita API key. |
| **Las alertas por zona no funcionan** | En la versión actual son simuladas (carteles dentro de la app). Para alertas reales habría que usar Firebase. |
| **La IA da consejos genéricos** | Mejorar el prompt con más detalles de la situación |
| **Las publicaciones no se guardan** | Verificar que localStorage esté habilitado |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app local para Mar del Plata que ayuda a e ncontrar mascotas perdidas usando mapas, alertas por zona simuladas e IA que da consejos en cada situación. Todo gratis, sin necesidad de base de datos externa, pensado para nuestra comunidad."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT

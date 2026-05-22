# 🚌 ColectivoApp - App con IA para avisar el colectivo (y verlo en un mapa)

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)
- [ ] Una cuenta en **Supabase** (gratis, para el mapa en vivo)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.
---
## 🎯 Qué hace esta app

Detecta automáticamente cuando un estudiante **sube al colectivo** y:
1. Comparte su **ubicación en un mapa en vivo**
2. Sus compañeros pueden **ver dónde está el colectivo** en tiempo real
3. No hay que tocar ningún botón. Todo es automático.
---

## 🛠️ Herramientas (todo desde el navegador)

| Herramienta | Link | Para qué |
| :--- | :--- | :--- |
| **Replit** | replit.com | Escribir y ejecutar el código |
| **Hugging Face** | huggingface.co | IA gratuita |
| **Supabase** | supabase.com | Base de datos y mapa en vivo |
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
- 
**B. Supabase** (la base de datos)
- Entrar a [supabase.com](https://supabase.com)
- "Start your project" → crear nuevo proyecto
- En **SQL Editor**, ejecutar el código SQL que está en el archivo `readme.md` (sección SUPABASE)
- Ir a **Database** → **Replication** → habilitar la tabla `viajes`
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
A la derecha de la pantalla aparece una vista previa.
**Para probar la simulación (sin moverte):**
- Hacé 5 taps rápidos en el título "Colectivo Tracker"
- Se abre un panel donde podés controlar la velocidad manualmente
- 
### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://colectivo-app.vercel.app`)
- 
### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`
- 
### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Usar el código de grupo: **COLECTIVO2024**

---

## 📱 Cómo se usa en el día a día
| Momento | El estudiante hace... | La app hace... |
|--|--|--|
| **Primera vez** | Abre la app, pone nombre y código | Guarda los datos |
| **Va a la parada** | Nada (deja la app abierta) | Espera quieta |
| **Sube al colectivo** | Nada | Detecta que empezó a moverse |
| **El colectivo arranca** | Nada | IA confirma que es colectivo |
| **Alerta** | Nada (automático) | Comparte ubicación en el mapa |
| **Compañeros** | Abren el mapa | Ven dónde está el colectivo en tiempo real |
| **Llega al colegio** | Nada | Detecta 2 minutos quieto → resetea |

> 🗺️ **Los compañeros pueden ver el mapa aunque ellos no estén viajando.**

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| Clasificación de movimiento | Recibe datos de velocidad y decide si es un colectivo o un semáforo |
| Reducción de falsas alarmas | Evita que un semáforo largo active una alerta |
| Adaptabilidad | Si el colectivo acelera diferente por tráfico, la IA se adapta sola |
**Prompt que usa la IA internamente:**
```javascript
const prompt = `
 Velocidad actual: ${velocidad} km/h
 Tiempo quieto previo: ${tiempoQuieto} segundos
 ¿Es un COLECTIVO arrancando o un SEMÁFORO?
 Respondé solo "COLECTIVO" o "SEMAFORO".
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
| **No pide permiso de ubicación** | Ir a Configuración → Apps → ColectivoApp → Permisos → Ubicación → "Permitir todo el tiempo" |
| **La IA no responde** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado en los Secrets de Replit |
| **El mapa no muestra a los compañeros** | Verificar que Supabase Realtime esté habilitado en la tabla `viajes` |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) como alternativa |
| **La app no detecta el movimiento** | Asegurarse de que el GPS esté activo y la app abierta (no en segundo plano) |


----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face y un mapa en vivo con Supabase, construimos una app que detecta automáticamente cuando un estudiante sube al colectivo y permite a todo el grupo ver su ubicación en tiempo real. Todo gratis, funcionando completamente desde el navegador"_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT

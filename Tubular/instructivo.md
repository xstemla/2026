# 🎨 TubularApp - Animación con IA para creadores

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace esta app
TubularApp es un estudio de animación en tu celular que:
- **Anima tus dibujos con IA**: subí una secuencia de dibujos (fotogramas) y la IA genera una animación fluida
- **Red social para creadores**: conecta animadores con actores de doblaje
- **Exportación de audio**: grabá y exportá voces para tus personajes
- **Castings y colaboración**: publicá roles y encontrá talento

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

> ⚠️ **TubularApp NO necesita Supabase**. Los dibujos, animaciones y perfiles se guardan en el celular (localStorage).

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
- Completar tu perfil (elegí rol: animador o actor de doblaje)
- Subir 3 dibujos en secuencia (ej. persona en diferentes posiciones)
- Tocar "Generar animación" y ver el resultado
- Grabar un audio y exportarlo
- Publicar tu animación en la red social
- Explorar castings o crear uno nuevo

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://tubular-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a crear animaciones y conectar con otros artistas

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| **Quiere animar un dibujo** | Sube 3-5 fotogramas en orden | IA genera la animación |
| **Necesita voz para su personaje** | Publica un casting en la red social | Actores de doblaje responden |
| **Es actor de doblaje** | Sube muestras de voz | Animadores lo contactan |
| **Quiere compartir su trabajo** | Publica la animación | Otros usuarios la ven y comentan |
| **Quiere guardar un proyecto** | Toca "Guardar" | Se guarda en su portafolio |

> 🎬 La app ayuda a creadores a hacer realidad sus sueños de tener su propia serie.

---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Interpolación de fotogramas** | Genera dibujos intermedios para suavizar la animación |
| **Generación de animación** | Convierte secuencia de imágenes en video/GIF fluido |

**Funcionamiento (simulado en MVP):**
```javascript
// La IA toma la imagen 1 y la imagen 2
// Genera 3-5 fotogramas intermedios combinando posiciones
// El resultado es una animación suave
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

| Problema  | Solución |
|--|--|
| **La animación se ve entrecortada** | Subí más fotogramas intermedios (ej. 1, 1.5, 2) |
| **La IA no responde** | Verificar token. Usa el modo offline (interpolación básica) |
| **No puedo grabar audio** | Verificar permisos de micrófono en el navegador |
| **No encuentro actores de doblaje** | Publicá un casting con más detalles |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Usando Replit y Hugging Face, creamos TubularApp: un estudio de animación con IA en tu celular. Subí tus dibujos en secuencia, la IA genera la animación fluida, y nuestra red social conecta animadores con actores de doblaje. No reemplaza al artista, lo potencia."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT

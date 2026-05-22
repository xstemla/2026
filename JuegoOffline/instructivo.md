
# 🎮 JuegoOffline - Juego mobile sin wifi con IA integrada

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)
> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---

## 🎯 Qué hace este juego
Es un juego sin necesidad de internet (offline) para matar el tiempo libre. Está inspirado en Subway Surfers, pero con una mecánica única: **podés ver tu partida anterior mientras jugás la actual para corregir errores**. Además, una IA te da consejos personalizados cuando perdés y te propone desafíos cada 5 partidas.
- **Mecánica principal**: corré y esquivá obstáculos (tocá la pantalla para saltar)
- **Mecánica innovadora**: en una esquina se reproduce tu partida anterior, mostrando dónde fallaste
- **IA**: analiza tus errores y te da consejos para mejorar
- **Offline**: el juego funciona sin internet (la IA solo online)

---

## 🛠️ Herramientas (todo desde el navegador)
| Herramienta | Link | Para qué |
| :--- | :--- | :--- |
| **Replit** | replit.com | Escribir y ejecutar el código |
| **Hugging Face** | huggingface.co | IA gratuita |
| **Vercel** | vercel.com | Publicar el juego gratis |
| **PWABuilder** | pwabuilder.com | Convertir el juego en APK |

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

> ⚠️ **JuegoOffline NO necesita Supabase**. Los puntajes y partidas se guardan en el celular (localStorage). El juego funciona offline; la IA solo se usa si hay conexión.

### 2. Crear el proyecto en Replit

- Click en **"Create new Repl"** → **"Create with AI"**

### 3. Configurar los "Secretos" (Keys)

En Replit, ir a **Tools** → **Secrets** (🔒) y agregar:

| Secret | Valor |
|--|--|
| `VITE_HF_TOKEN` | El token que copiaste de Hugging Face |

### 4. Copiar el prompt
Abrir el archivo `readme.md` de este proyecto y **copiar TODO su contenido**.
En Replit, pegar el prompt en el chat del **"Replit Agent"** y esperar a que genere el juego.

### 5. Ver el juego funcionando

A la derecha de la pantalla aparece una vista previa. Probá:
- **Jugar**: tocá la pantalla (o espacio en PC) para saltar obstáculos
- **Replay**: después de perder, reiniciá y mirá la esquina superior derecha: se reproduce la partida anterior
- **Consejo IA**: al perder, mirá el mensaje de IA (si hay conexión)
- **Desafío**: cada 5 partidas, la IA propone un objetivo
- **Modo oscuro**: activalo desde el botón correspondiente

### 6. Publicar el juego (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://juego-offline.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a jugar sin necesidad de internet

---

## 📱 Cómo se juega en el día a día
| Momento | El usuario hace... | El juego hace... |
|--|--|--|
| **Tiene tiempo muerto** | Abre el juego | Carga la última partida guardada |
| **Juega** | Toca la pantalla para saltar | Muestra puntaje y partida anterior en miniatura |
| **Pierde** | (Automático) | IA analiza el error y da un consejo |
| **Quiere mejorar** | Sigue el consejo de la IA | Evita el mismo error la próxima vez |
| **Juega 5 partidas** | (Automático) | IA sugiere un desafío personalizado |

> 🎮 El juego funciona sin internet, perfecto para viajes en tren o subte.
---

## 🤖 ¿Dónde usamos IA?
| Ubicación | Qué hace la IA |
|--|--|
| **Análisis de errores** | Detecta en qué obstáculo falló y da un consejo específico |
| **Desafíos personalizados** | Cada 5 partidas, genera un objetivo (ej. "superá los 800 puntos sin chocar") |
| **Consejos motivadores** | "Fallaste por el tren amarillo, saltá más temprano" |

**Prompt que usa la IA internamente (análisis de error):**
```javascript
const prompt = `
 El jugador perdió con puntaje: ${puntaje} (récord: ${mejorPuntaje}).
 El obstáculo que lo mató fue: ${obstaculo}.
 DALE UN CONSEJO CORTO (máximo 15 palabras) y MOTIVADOR.
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
| **El juego no corre en celulares viejos** | El prompt incluye optimización para gama baja. Si sigue lento, reducir obstáculos. |
| **La partida anterior no se reproduce** | Verificar que localStorage esté guardando los datos correctamente |
| **La IA da consejos genéricos** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado. El juego funciona igual. |
| **No responde al tap en celular** | Asegurar que el Canvas tenga eventos `touchstart` (el prompt lo incluye) |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |

----------

## 🎯 Frase para la defensa

> _"Con Google AI Studio y un solo prompt, creamos un juego mobile offline inspirado en Subway Surfers pero con una mecánica única: podés ver tu partida anterior mientras jugás para aprender de tus errores. Además, una IA te da consejos personalizados y desafíos. Todo desde el navegador, sin instalar nada, y funciona sin internet."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT

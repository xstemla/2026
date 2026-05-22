# 🦎 FaunaApp - App para registrar avistajes de fauna

## 📌 Antes de empezar
Este archivo es la **guía para humanos**. 
Antes de seguir, asegurate de tener:
- [ ] Una cuenta en **Replit** (gratis, con Google o GitHub)
- [ ] Una cuenta en **Hugging Face** (gratis, para la IA)

> 💡 Todo es gratuito y no necesita instalación en tu computadora.

---
## 🎯 Qué hace esta app

Permite registrar avistajes de animales (especie, ubicación, fecha y foto) y ver un listado de todos los registros. Los datos se guardan automáticamente en el celular (localStorage). La IA sugiere automáticamente la categoría del animal (ave, mamífero, reptil, etc.) mientras escribís la especie.

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

> ⚠️ **FaunaApp NO necesita Supabase**. Los avistajes se guardan en el celular (localStorage).

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
- Completar especie: "Hornero"
- Ver cómo la IA sugiere "Ave" debajo del campo
- Agregar ubicación, fecha, foto (opcional)
- Guardar y ver el avistaje en el listado
- Eliminar un avistaje o todos

### 6. Publicar la app (para generar el APK)
- En Replit, hacer clic en el botón **"Deploy"** (ícono de Vercel)
- Conectar con GitHub y autorizar Vercel
- Vercel te da una URL pública (ej: `https://fauna-app.vercel.app`)

### 7. Generar el APK para instalar en el celular
- Entrar a [pwabuilder.com](https://pwabuilder.com/)
- Pegar la URL que te dio Vercel
- Click en **"Build"** → **"Android"**
- Descargar el archivo `.apk`

### 8. Compartir con los compañeros
- Enviar el `.apk` por WhatsApp o Google Drive
- Cada uno lo instala en su celular
- Empiezan a registrar sus propios avistajes

---

## 📱 Cómo se usa en el día a día
| Momento | El usuario hace... | La app hace... |
|--|--|--|
| **Primera vez** | Abre la app | Muestra formulario vacío |
| **Ve un animal** | Completa especie, ubicación, fecha, agrega foto | IA sugiere categoría automáticamente |
| **Toca "Guardar"** | Click en guardar | Almacena en localStorage y actualiza listado |
| **Ver registros** | Mira el listado debajo | Muestra todos los avistajes ordenados |
| **Eliminar un error** | Toca "Eliminar" | Borra ese avistaje |
| **Empezar de cero** | Toca "Eliminar todos" | Pide confirmación y borra todo |

> 🦜 Los datos no se pierden al cerrar la app.

---

## 🤖 ¿Dónde usamos IA?

| Ubicación | Qué hace la IA |
|--|--|
| **Sugerencia de categoría** | Mientras escribís la especie, IA sugiere si es Ave, Mamífero, Reptil, Insecto u Otro |
| **Clasificación automática** | Ayuda a organizar avistajes sin que el usuario tenga que pensar la categoría |

**Prompt que usa la IA internamente:**
```javascript
const prompt = `
 Especie de animal: ${especie}
 Clasificá en: Ave, Mamífero, Reptil, Insecto, Otro.
 Respondé SOLO la categoría.
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
| **Las fotos no se ven** | Usar fotos chicas (la app debería redimensionarlas automáticamente) |
| **Los datos desaparecen** | Verificar que localStorage esté habilitado en el navegador |
| **La app se ve mal en celular** | El prompt ya pide diseño responsive. Si algo falla, ajustar Tailwind |
| **La IA no sugiere categoría** | Verificar que el token `VITE_HF_TOKEN` esté bien copiado. La app sigue funcionando igual. |
| **No se genera el APK** | Probar con otra URL o usar [bubblewrap.dev](https://bubblewrap.dev/) |
|  |  |

----------

## 🎯 Frase para la defensa

> _"Usando solo Replit desde el navegador, con IA gratuita de Hugging Face, construimos una app de campo para registrar avistajes de fauna. La IA ayuda a clasificar las especies automáticamente. Los datos se guardan solos en el celular sin necesidad de base de datos externa. Todo gratis, pensado para usar en excursiones o salidas de campo."_

----------

## 👥 Autores

Proyecto estudiantil - [Nombre del curso/institución]

## 📄 Licencia

MIT

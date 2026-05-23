# 🧠 Conceptos Avanzados - Entendiendo más a fondo

Este documento es para **después de haber hecho 2 o 3 proyectos**. Ya sabés lo básico y querés entender por qué a veces las cosas no funcionan como esperabas.

---

## 🧠 Concepto 1: Estado (state) vs Variables normales

Esta es **la diferencia más importante** y la que más confusiones genera.

### Variable normal
```javascript
let likes = 0

function darLike() {
  likes = likes + 1   // Cambió el número
  // Pero la pantalla sigue mostrando 0 😢
}
Estado (state)
javascript
const [likes, setLikes] = useState(0)

function darLike() {
  setLikes(likes + 1)  // Cambia el número Y la pantalla se actualiza ✅
}
```


Tabla comparativa
| |Variable normal	|Estado|
|--|--|--|
|¿Si cambia, la pantalla se actualiza?	|❌ No	|✅ Sí|
|¿Cómo se crea?	|let nombre = "Ana"	|const [nombre, setNombre] = useState("Ana")|
|¿Cómo se cambia?	|nombre = "Luis"|	setNombre("Luis")|

Regla de oro
> Si algo en la pantalla tiene que cambiar cuando el usuario hace algo (contador, mensaje, lista) → tiene que ser estado, no variable normal.

En tus apps: Puntaje del usuario, menú abierto/cerrado, texto que el usuario está escribiendo.

Si la IA se equivoca: Usa variable normal en vez de estado (la pantalla no se actualiza), o escribe likes = likes + 1 en vez de setLikes(likes + 1).

## 🧱 Concepto 2: Componentes y Props
En React (la tecnología de estos proyectos) la pantalla se arma con componentes: pedazos reutilizables.

```javascript
// Un componente Botón que podés usar muchas veces
function Boton({ texto, color, alHacerClick }) {
  return (
    <button 
      style={{ backgroundColor: color }}
      onClick={alHacerClick}
    >
      {texto}
    </button>
  )
}

// Usarlo en diferentes lugares
<Boton texto="Guardar" color="azul" alHacerClick={guardar} />
<Boton texto="Eliminar" color="rojo" alHacerClick={borrar} />
```

**¿Por qué son útiles?**

- Escribís el código una sola vez
- Si necesitas cambiar algo, lo cambiás en un solo lugar
- El código es más fácil de entender

**Props (propiedades):** Son los datos que le pasás a un componente. Son de solo lectura: el componente hijo NO puede modificarlas.

**En tus apps:** Tarjeta de cada publicación, formulario de registro, mensaje de error.

**Si la IA se equivoca:** Crea componentes que no se usan, o el componente hijo intenta modificar una prop directamente.

## 🗄️ Concepto 3: localStorage (memoria que no se borra)
El localStorage guarda datos en tu navegador para siempre (hasta que los borrés manualmente).

```javascript
// Guardar algo
localStorage.setItem("nombre", "Sofia")
localStorage.setItem("puntajeMaximo", 1500)
localStorage.setItem("tareas", JSON.stringify(["estudiar", "correr"]))

// Recuperar (aunque cierres y abras la app)
let nombre = localStorage.getItem("nombre")           // "Sofia"
let tareas = JSON.parse(localStorage.getItem("tareas")) // ["estudiar", "correr"]

// Borrar algo
localStorage.removeItem("puntajeMaximo")

// Borrar TODO
localStorage.clear()
```

¿Qué se puede guardar? Solo texto. Por eso para guardar listas u objetos usás JSON.stringify() y JSON.parse().

Diferencia con el estado
| | Estado |localStorage |
|--|--|--|
|Se borra al cerrar la app	| ✅ Sí	| ❌ No |
|La pantalla se actualiza sola	| ✅ Sí	 | ❌ No (hay que cargarlo manualmente) |
|Sirve para...	| Cosas temporales (lo que pasa mientras usás la app)	 | Cosas permanentes (perfil, progreso guardado) |

> Regla de oro: Si algo tiene que seguir estando después de cerrar la app → guardalo en localStorage.

**En tus apps:** Perfil del usuario, lista de tareas, puntaje más alto, animaciones guardadas.

**Si la IA se equivoca:** Intenta guardar imágenes (ocupan mucho espacio), olvida usar JSON.stringify(), o no carga los datos al iniciar.

## 🌐 Concepto 4: APIs (la app habla con otro programa)
Una API es un mensajero: tu app le pide algo a otro programa (ej. Hugging Face) y espera la respuesta.

```javascript
async function identificarAnimal(imagen) {
  try {
    const respuesta = await fetch("https://api.huggingface.co/models/google/vit-base-patch16-224", {
      method: "POST",
      headers: {
        "Authorization": `Bearer ${token}`,
        "Content-Type": "application/json"
      },
      body: JSON.stringify({ inputs: imagen })
    })
    
    const datos = await respuesta.json()
    return datos[0].label  // "perro", "gato", etc.
  } catch (error) {
    console.error("Error:", error)
    return "No se pudo identificar"
  }
}
```

El await significa: "Esperá a que la API responda, después seguí". Las APIs pueden tardar unos segundos.

En tus apps: Cada vez que la IA genera algo (consejos, ejercicios, animaciones), y cuando usás Supabase.

Si la IA se equivoca: Olvida el await (la función sigue sin esperar), o no maneja el error (la app se rompe si la API falla).

## 🔄 Concepto 5: Bucles (para repetir cosas)
Hacen lo mismo varias veces sin escribir el mismo código 100 veces.

```javascript
// Versión clásica (for)
let nombres = ["Ana", "Luis", "Sofia", "Carlos"]
for (let i = 0; i < nombres.length; i++) {
  console.log("Hola " + nombres[i])
}

// Versión moderna (map) - la que más vas a ver en estos proyectos
nombres.map((nombre) => {
  return <Tarjeta nombre={nombre} />
})
```

El map hace dos cosas:

- Recorre toda la lista
- Por cada elemento, devuelve un componente (o lo que le pidas)

En tus apps: Mostrar una lista de mensajes, generar varios fotogramas de una animación, crear botones para cada opción.

Si la IA se equivoca: Puede hacer un bucle infinito (la app se traba). Si pasa, cerrá y volvé a abrir.

## 🐛 Errores comunes y cómo solucionarlos (versión completa)
|Lo que ves	|Qué significa	|Qué hacer |
|--|--|--|
|undefined is not an object	|Usaste algo que no existe	|Revisá que escribiste bien el nombre|
|Cannot read property 'x' of undefined	|Una variable no tiene valor todavía	|Fijate que esté inicializada antes de usarla|
|setLikes is not a function	|Usaste mal el estado	|Revisá: const [likes, setLikes] = useState(0)|
|Maximum call stack exceeded	|Bucle infinito o componente que se renderiza sin parar	|Copiale el error a la IA|
|La pantalla no se actualiza al cambiar algo	|Usaste variable normal en vez de estado	|Cambiá let por const [..., set...] = useState(...)|
|Los datos desaparecen al cerrar la app	|Necesitás localStorage	|Pedile a la IA: "Guardá esto en localStorage para que no se borre"|
|El botón no hace nada	|La función no está conectada	|Revisá onClick={nombreDeFuncion} (sin paréntesis)|
|Network error	|No conecta con Hugging Face	|Revisá el token en los Secretos de Replit|
|La página se recarga sola	|Un botón sin type="button" dentro de un formulario	|Agregá type="button" al botón|

## 🔧 Debugging con console.log
console.log es tu mejor amiga. Te permite ver qué valores tienen las variables en cada momento.

```javascript
function calcularPuntaje(respuestas) {
  console.log("Respuestas recibidas:", respuestas)
  
  let total = 0
  for (let i = 0; i < respuestas.length; i++) {
    console.log(`Respuesta ${i}:`, respuestas[i])
    total = total + respuestas[i]
  }
  
  console.log("Total calculado:", total)
  return total
}
```

Cómo usarlo:
- Abrí la consola del navegador (F12 o clic derecho → Inspeccionar → pestaña Console)
- Agregá console.log("Algo:", variable) en lugares clave
- Ejecutá la acción y fijate qué aparece

Frases para pedirle a la IA que agregue logs:

"Agregá un console.log cada vez que se ejecute la función guardarDatos, mostrando lo que se está guardando"

## 🎯 Lo más importante de este documento
1. Estado → para cosas que cambian la pantalla. localStorage → para cosas que no se borran al cerrar
2. Componentes son pedazos de pantalla reutilizables. Props son los datos que reciben
3. APIs son mensajeros. Usan await y pueden fallar (siempre manejá errores)
4. map sirve para recorrer listas y mostrar componentes
5. console.log es la forma más fácil de entender qué está pasando adentro

Con estos conceptos ya podés debuggear sola/o cuando algo no funciona como esperabas.

🚀 Seguí creando!



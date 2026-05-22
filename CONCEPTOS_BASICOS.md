# 🎓 Conceptos Básicos - Vibe Coding

Este documento es para **antes de tu primer proyecto**. Solo necesitas entender estas ideas para arrancar. El resto lo vas a aprender sobre la marcha.

---

## 🎵 ¿Qué es "vibe coding"?

Es programar **describiendo en español** lo que querés hacer, y la IA escribe el código por vos.

**Ejemplo:** Le decís a Replit Agent:

> "Hacé una app con un título que diga 'Mi primera app', un botón azul que diga 'Saludar', y cuando lo aprietes mostrá un mensaje que diga 'Hola'"

Y la IA hace todo. Vos no escribís una línea de código.

**Lo importante:** La IA hace lo que le **pediste**, no siempre lo que **querías decir**. Cuanto más claro seas, mejor resultado vas a tener.

---

## 📦 Concepto 1: Variables (cajitas con nombre)

Una variable guarda un dato para usarlo después.

```javascript
let nombre = "Sofia"
let edad = 15
let puntaje = 0
```

¿Qué significa cada parte?
let → "voy a crear una cajita"
nombre → el nombre de la cajita (lo inventás vos)
= → "guardá esto dentro"
"Sofia" → el valor que guardás

Las variables pueden cambiar:

```javascript
puntaje = 10           // el jugador suma puntos
puntaje = puntaje + 5  // ahora vale 15
nombre = "Maria"       // el usuario cambió su nombre
```
En tus apps: El nombre del usuario, la puntuación, si completó una tarea.

Si la IA se equivoca: Puede usar la variable antes de guardarle un valor, o escribir el nombre mal.

##  🧪 Concepto 2: Funciones (recetas)
Una función es un conjunto de pasos que podés ejecutar cuando querés.

```text
// La receta
function hacerTostada() {
  // Paso 1
  let pan = sacarPan()
  // Paso 2
  ponerEnTostadora(pan)
  // Paso 3
  esperar(30)
  // Paso 4
  return servir()
}

// Usar la receta (ejecutar la función)
hacerTostada()
```
Las funciones pueden recibir datos y devolver resultados:

```javascript
function sumar(a, b) {
  let resultado = a + b
  return resultado
}
```
let total = sumar(5, 3)  // total vale 8
En tus apps: "Al hacer clic en el botón Guardar, tomar lo que escribió el usuario y guardarlo"

Si la IA se equivoca: Puede crear funciones que no se usan, o usarlas en el momento incorrecto.

## 🚦 Concepto 3: Condicionales (preguntas)
Hacen una pregunta y actúan según la respuesta.

```javascript
if (edad >= 18) {
  mostrar("Podés votar")
} else {
  mostrar("Todavía no, faltan " + (18 - edad) + " años")
}
```

Operadores que vas a usar:
```javascript
== o === → igual
!= → distinto
> → mayor que
< → menor que
>= → mayor o igual
<= → menor o igual
&& → Y (las dos condiciones tienen que cumplirse)
|| → O (al menos una se cumple)
```

Ejemplo con dos condiciones:

```javascript
if (edad >= 18 && tieneDNI) {
  mostrar("Podés entrar")
} else {
  mostrar("No podés entrar")
}
```
En tus apps: Si el usuario escribió muy poco, mostrar error. Si ganó el juego, mostrar felicitaciones.

Si la IA se equivoca: Puede hacer la pregunta al revés (ej. if (edad < 18) cuando debería ser >=).

## 💡 Cómo pedirle ayuda a la IA (Replit Agent)
Cuando algo no funciona, escribile cosas claras:

Para errores:
"Hay un error que dice Cannot read property 'nombre' of undefined. Arreglalo"

Para funciones que no andan:
"El botón Guardar no guarda nada. Revisá la función que maneja el clic"

Para comportamiento raro:
"Cuando aprieto Enviar, la página se recarga sola. Debería mostrar un mensaje sin recargar"

Para entender qué pasa:

"Agregá un console.log cada vez que se ejecute la función calcularPuntaje"

##  🐛 Los 3 errores más comunes (y cómo arreglarlos)
Lo que ves	Qué significa	Qué hacer
undefined is not an object	Usaste algo que no existe	Revisá que escribiste bien el nombre
Network error	No conecta con Hugging Face	Revisá el token en los Secretos de Replit
El botón no hace nada	La función no está conectada	Fijate que el botón tenga onClick={nombreDeLaFuncion}

##  🎯 Lo más importante de este documento
Vibe coding = describís en español, la IA escribe el código
Variables = cajitas que guardan datos (nombre, puntaje, etc.)
Funciones = recetas que hacen cosas cuando las llamás
Condicionales = preguntas para decidir qué hacer

Saber pedirle ayuda a la IA es tan importante como entender código

Con esto ya podés hacer tu primer proyecto (AlanApp o JuegoOffline). El resto se aprende haciendo.

##  🚀 A crear!

¿Terminaste tu primer proyecto? Pasá al CONCEPTOS_AVANZADOS.md cuando quieras entender más.

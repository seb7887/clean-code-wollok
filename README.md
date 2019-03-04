# Clean Code Wollok

## Contenido
  1. [Introducción](#introducción)
  2. [Variables](#variables)
  3. [Funciones](#funciones)
  4. [Objetos y estructuras de data](#objetos-y-estructuras-de-data)
  5. [Clases](#clases)
  6. [SOLID](#solid)
  7. [Pruebas](#pruebas)
  8. [Concurrencia](#concurrencia)
  9. [Resolver los errores](#resolver-los-errores)
  10. [Formatear](#formatear)
  11. [Comentarios](#comentarios)

## Introducción

![Imagen de la estimación de la calidad de software como una cifra 
de cuantos expletivos que uno puede gritar al leer programas](http://www.osnews.com/images/comics/wtfm.jpg)

Los principios de la ingeniería de software, del libro de Robert C. Martin [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882), adaptado para **Wollok**. Esta no es una guía de estilo, en cambio, es una guía para crear software que sea reutilizable, comprensible y que se pueda mejorar con el tiempo.

No hay que seguir tan estrictamente todos los principios en este libro, y vale la pena mencionar que hacia muchos de ellos habrá controversia en cuanto al consentimiento. Estas son reflexiones hechas después de muchos años de experiencia colectiva de los autores de *Clean Code*.

Una cosa más: saber esto no te hará un mejor programador inmediatamente, y tampoco trabajar con estas herramientas durante muchos años garantiza que nunca te vas a equivocar. Cualquier código empieza primero como un borrador y, por último, arreglamos las imperfecciones cuando lo revisamos con nuestros compañeros de trabajo.

## **Variables**
### Usa nombres significativos y pronunciables para las variables

**Mal**
```javascript
const dmyyyy = new Date(22, 2, 2019)
```

**Bien**
```javascript
const fechaActual = new Date(22, 2, 2019)
```

**[⬆ volver hasta arriba](#contenido)**

### Usa el mismo vocabulario para las variables del mismo tipo

**Mal**
```javascript
getInfoDelUsuario()
getDataDelCliente()
```

**Bien**
```javascript
getUsuario()
```

**[⬆ volver hasta arriba](#contenido)**

### Usa nombres que se puedan buscar

Siempre vamos a leer mucho más código del que vamos a escribir. Por eso, es importante que lo que se escriba sea legible y buscable, sino terminaremos confundiendo a quien esté leyendo el código.

**Mal**
```javascript
// Para que sirve 1234??
method valorTotal(cantidad) = cantidad * 1234
```

**Bien**
```javascript
// Se declara las constantes aparte -> mas legible y modificable
const COSTO = 1234

method valorTotal(cantidad) = cantidad * COSTO
```

**[⬆ volver hasta arriba](#contenido)**

### Usa variables para volver más entendible el código

**Mal**
```javascript
guardarCodigoPostal('Calle Falsa 123', 1234)
```
**Bien**
```javascript
var direccion = 'Calle Falsa 123'
var codigoPostal = 1234
guardarCodigoPostal(direccion, codigoPostal)
```

**[⬆ volver hasta arriba](#contenido)**

### Evitar el mapeo mental
Ser explícito es mucho mejor que ser implícito.

**Mal**
```javascript
var ubicaciones = [buenosAires, cordoba, rosario]
ubicaciones.forEach { u => u.coordenadas() } // Que es u??
```

**Bien**
```javascript
var ubicaciones = [buenosAires, cordoba, rosario]
ubicaciones.forEach { ubicacion => ubicacion.coordenadas() } // Tu yo del futuro te lo va a agradecer
```

**[⬆ volver hasta arriba](#contenido)**

## No incluyas contexto innecesario
Si el nombre de tu clase/objeto te dice algo, no lo repitas en el nombre de tu variable también.

**Mal**
```javascript
class Coche {
  const property marcaCoche = 'Honda'
  const property modeloCoche = 'Accord'
  var property colorCoche = 'Azul'

  method pintar(nuevoColor) {
    this.colorCoche = nuevoColor
  }
}
```

**Bien**
```javascript
class Coche {
  const property marca = 'Honda'
  const property modelo = 'Accord'
  var property color = 'Azul'

  method pintar(nuevoColor) {
    this.color = nuevoColor
  }
}
```

**[⬆ volver hasta arriba](#contenido)**

## **Funciones**
### Argumentos de funciones (2 o menos idealmente)

Limitar la cantidad de parámetros de tus funciones es increíblemente importante, ya que hace que tus tests sean mucho más fáciles. Al pasar los 3 parámetros, vas a llegar a un escenario de explosión combinatoria en el que hay que comprobar con tests muchos casos únicos con un argumento separado.

Normalmente, si tu función tiene más de dos argumentos es porque realiza demasiadas tareas. En ese caso, es mejor refactorizar y extraer parte de la función en otra.

**Mal**
```javascript
method valorTotal(cantidad, costoUnitario, impuestos) = (cantidad * costoUnitario) + impuestos
```

**Bien**
```javascript
var property costoUnitario
var property impuestos

method valorTotal(cantidad) = (cantidad * this.costoUnitario) + this.impuestos
```

**[⬆ volver hasta arriba](#contenido)**

### Las funciones deben tener una sola responsabilidad

Esta regla es la más importante en la ingeniería del Software. Cuando las funciones sirven para hacer más de una sola cosa, se dificultan las pruebas, la composición y la comprensión. Cuando uno puede aislar una función hasta tener una sola acción, se puede mejorar mucho más fácil eventualmente y el código se vuelve más limpio.

**Mal**
```javascript
method guardarClientes(clientes) {
  clientes.forEach { cliente => {
    this.baseDeDatos.find { record => record.cliente == cliente }
  } }
}
```
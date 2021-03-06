# Clean Code Wollok

## Contenido
  1. [Introducción](#introducción)
  2. [Nombres](#nombres)
  3. [Métodos](#métodos)


## Introducción

TODO

## **Nombres**
### Usa nombres descriptivos y pronunciables para las variables
El nombre de una variable debe indicar a qué se refiere y/o la función que realiza. También debe ser pronunciable, ya que si uno no puede pronunciarlo, resultará complicado explicar a que se refiere

**Mal**
```javascript
const d = new Date(22, 2, 2019)
```

**Bien**
```javascript
const fechaActual = new Date(22, 2, 2019)
```

### Los nombres de los métodos deben ser verbos
TODO

**Mal**
```javascript
```

**Bien**
```javascript
```


### Los nombres de las clases deben ser sustantivos
Bajo ningún punto deberán ser verbos

TODO

**Mal**
```javascript
```

**Bien**
```javascript
```

**[⬆ volver hasta arriba](#contenido)**

### Usar nombres que se puedan buscar

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

### Evitar asignaciones mentales
Ser explícito es mucho mejor que ser implícito. El lector del código no tiene que traducir mentalmente a qué se refiere el nombre de una variable

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
    colorCoche = nuevoColor
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
    color = nuevoColor
  }
}
```

**[⬆ volver hasta arriba](#contenido)**

## **Métodos**
### Tamaño reducido
Los métodos deben ser de tamaño reducido, lo más pequeños que se puedan

**Mal**
```javascript
```

**Bien**
```javascript
```

### Argumentos de los métodos (2 o menos idealmente)

Limitar la cantidad de parámetros de tus métodos es increíblemente importante, ya que hace que tus tests sean mucho más fáciles de escribir. Al pasar los 3 parámetros, se tendrá que comprobar con tests muchos casos únicos con un argumento separado.

Normalmente, si tu método tiene más de dos argumentos es porque realiza demasiadas tareas. En ese caso, es mejor refactorizar y extraer parte de la funcionabilidad en otro método aparte.

**Mal**
```javascript
method valorTotal(cantidad, costoUnitario, impuestos) = (cantidad * costoUnitario) + impuestos
```

**Bien**
```javascript
var property costoUnitario
var property impuestos

method valorTotal(cantidad) = (cantidad * self.costoUnitario) + this.impuestos
```

**[⬆ volver hasta arriba](#contenido)**

### Deben tener una sola cosa, hacerlo bien y debe ser lo único que hagan

Cuando los métodos sirven para hacer más de una sola cosa, se dificultan las pruebas, la composición y la comprensión. Cuando uno puede aislar un método hasta tener una sola acción, se puede mejorar mucho más fácil eventualmente y el código se vuelve más limpio.

**Mal**
```javascript
method sonTodosVagonesLivianos() = vagones.filter { vagon => vagon.pesoMaximo() < PESO_MAXIMO }.size() === vagones.size()
```
**Bien**
```javascript
method cantidadDeVagonesLivianos() = vagones.filter { vagon => vagon.pesoMaximo() < PESO_MAXIMO }.size()

method sonTodosVagonesLivianos() = self.cantidadDeVagonesLivianos() === vagones.size()
```

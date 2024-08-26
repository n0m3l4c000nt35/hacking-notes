# Inyeccion de comandos
1. [Introduccion a la inyeccion de comandos](#introduccion-a-la-inyeccion-de-comandos)
	1. [Que son las inyecciones](#que-son-las-inyecciones)
	2. [Inyección de comandos de sistema operativo](#inyeccion-de-comandos-de-sistema-operativo)
2. [Detección](#deteccion)
	1. [Detección de inyección de comandos](#deteccion-de-inyeccion-de-comandos)
	2. [Métodos de inyección de comandos](#metodos-de-inyeccion-de-comandos)
## Introduccion a la inyeccion de comandos
- Una vulnerabilidad de inyección de comandos es uno de los tipos de vulnerabilidad más críticos.
- Permite ejecutar comandos del sistema directamente en el servidor que aloja el back-end, lo que podría llevar a comprometer toda la red.
- Si una aplicación web utiliza entradas controladas por el usuario para ejecutar comandos del sistema en el servidor back-end para recuperar o devolver una salida específica, es posible  inyectar un payload malicioso para alterar el comando esperado y ejecutar un comando que el servidor no espera ejecutar.
### Que son las inyecciones
- Las vulnerabilidades de inyección se consideran el riesgo número 3 en los 10 principales riesgos de aplicaciones web de OWASP, dado su alto impacto y lo comunes que son.
- La inyección ocurre cuando la entrada controlada por el usuario se malinterpreta como parte de la consulta web o el código que se está ejecutando, lo que puede llevar a alterar el resultado previsto de la consulta a un resultado diferente que sea útil para el atacante.
- Hay muchos tipos de inyecciones que se encuentran en las aplicaciones web, dependiendo del tipo de consulta web que se esté ejecutando.
- Los siguientes son algunos de los tipos de inyecciones más comunes:

| Inyección                                   | Descripción                                                                                                |
| ------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Inyección de comandos del sistema operativo | Ocurre cuando el input del usuario se utiliza directamente como parte de un comando del sistema operativo. |
| Inyección de código                         | Ocurre cuando el input del usuario está directamente dentro de una función que evalúa el código.           |
| Inyecciones SQL                             | Ocurre cuando el input del usuario se utiliza directamente como parte de una consulta SQL.                 |
| Cross-Site Scripting/Inyección HTML         | Ocurre cuando se muestra la entrada exacta en una página web.                                              |

- Hay otros tipos de inyecciones como:
	- Inyección LDAP
	- Inyección NoSQL
	- Inyección HTTP header
	- Inyección XPath
	- Inyección IMAP
	- Inyección ORM

- Siempre que la entrada del usuario se utiliza dentro de una consulta sin estar debidamente desinfectada, puede ser posible escapar de los límites de la cadena de texto de entrada del usuario a la consulta principal y manipularla para cambiar su propósito previsto.
- A medida que se introduzcan más tecnologías web en las aplicaciones web, se verán nuevos tipos de inyecciones introducidas en las aplicaciones web.
### Inyeccion de comandos de sistema operativo
- Cuando se trata de inyecciones de comandos del sistema operativo, la entrada del usuario que se controla debe ir directa o indirectamente a (o afectar de alguna manera) una consulta web que ejecuta comandos del sistema.
- Todos los lenguajes de programación web tienen diferentes funciones que permiten al desarrollador ejecutar comandos del sistema operativo directamente en el servidor back-end cuando lo necesite.
- Se puede usar para diversos propósitos, como instalar complementos o ejecutar ciertas aplicaciones.
#### Ejemplo PHP
- Una aplicación web escrita en PHP puede usar las funciones `exec`, `system`, `shell_exec`, `passthru` o `popen` para ejecutar comandos directamente en el servidor back-end, cada uno con un caso de uso ligeramente diferente.

```php
<?php
if (isset($_GET['filename'])) {
    system("touch /tmp/" . $_GET['filename'] . ".pdf");
}
?>
```

- Quizás una aplicación web en particular tenga una funcionalidad que permita a los usuarios crear un nuevo documento `.pdf` que se crea en el directorio `/tmp` con un nombre de archivo proporcionado por el usuario y luego puede ser utilizado por la aplicación web para fines de procesamiento de documentos.
- Como la entrada del usuario del parámetro `filename` en la solicitud `GET` se usa directamente con el comando `touch` (sin ser desinfectado o escapado primero), la aplicación web se vuelve vulnerable a la inyección de comandos del sistema operativo.
- Esta falla se puede aprovechar para ejecutar comandos de sistema arbitrarios en el servidor back-end.

#### Ejemplo NodeJS
- Puede ocurrir en cualquier framework o lenguaje de desarrollo web.
- Si se desarrolla una aplicación web en `NodeJS`, un desarrollador puede usar `child_process.exec` o `child_process.spawn` para el mismo propósito.

```javascript
app.get("/createfile", function(req, res){
    child_process.exec(`touch /tmp/${req.query.filename}.txt`);
})
```

- El código anterior también es vulnerable a una vulnerabilidad de inyección de comandos, ya que utiliza el parámetro `filename` de la solicitud `GET` como parte del comando sin desinfectarlo primero.
- Tanto las aplicaciones web `PHP` como las `NodeJS` pueden explotarse utilizando los mismos métodos de inyección de comandos.
- Otros lenguajes de programación de desarrollo web tienen funciones similares que se utilizan para los mismos fines y, si son vulnerables, pueden explotarse utilizando los mismos métodos de inyección de comandos.
- Las vulnerabilidades de inyección de comandos no son exclusivas de las aplicaciones web, sino que también pueden afectar a otros binarios y aplicaciones de escritorio ​​si pasan una entrada de usuario no sanitizada a una función que ejecuta comandos del sistema, que también pueden explotarse con los mismos métodos de inyección de comandos.
## Deteccion
- El proceso para detectar las vulnerabilidades básicas de inyección de comandos del sistema operativo es el mismo proceso que para explotar dichas vulnerabilidades.
- Agregar el comando inyectado mediante varios métodos de inyección.
- Si el resultado del comando cambia respecto del resultado habitual previsto, se ha explotado la vulnerabilidad con éxito.
- Esto puede no ser cierto para vulnerabilidades de inyección de comandos más avanzadas porque se pueden utilizar varios métodos de fuzzing o análisis de código para identificar posibles vulnerabilidades de inyección de comandos.
- Luego se puede ir construyendo gradualmente el payload hasta lograr la inyección de comandos.
### Deteccion de inyeccion de comandos
- Una aplicación web muestra el output de un comando de sistema.
- Si el input no está desinfectado y escapado antes de ser utilizado, es posible que se pueda inyectar otro comando arbitrario.
### Metodos de inyeccion de comandos
- Para inyectar un comando adicional al deseado, se puede utilizar cualquiera de los siguientes operadores:

| Operador       | Caracter | Caracter URL-encodeado | Comando ejecutado                                         |
| -------------- | -------- | ---------------------- | --------------------------------------------------------- |
| Punto y coma   | ;        | %3b                    | Ambos                                                     |
| Salto de línea | \n       | %0a                    | Ambos                                                     |
| Segundo plano  | &        | %26                    | Ambos (el segundo output generalmente se muestra primero) |
| Pipe           | \|       | %7c                    | Ambos (Solo se muestra el segundo output)                 |
| AND            | &&       | %26%26                 | Ambos (Solo si el primero es exitoso)                     |
| OR             | \|       | %7c%7c                 | Segundo (Solo si el primero falla)                        |
| Sub-shell      | ``       | %60%60                 | Ambos (Solo Linux)                                        |
| Sub-shell      | $()      | %24%28%29              | Ambos (Solo Linux)                                        |

- Se puede usar cualquiera de estos operadores para inyectar otro comando de manera que se ejecuten «ambos» o «cualquiera» de los comandos.
- Se escribe el input esperado y luego se usa cualquiera de los operadores anteriores y se escribe el comando inyectado.
- Hay algunos operadores exclusivos de Unix que funcionarían en Linux y macOS, pero no en Windows, como envolver el comando inyectado con comillas dobles invertidas (` `` `) o con un operador de sub-shell (`$()`).
- Para la inyección de comandos básicos, todos estos operadores se pueden usar para inyecciones de comandos independientemente del lenguaje de la aplicación web, el framework o el servidor back-end.
- Si se inyecta en una aplicación web `PHP` que se ejecuta en un servidor `Linux`, o una aplicación web `.Net` que se ejecuta en un servidor back-end `Windows`, o una aplicación web `NodeJS` que se ejecuta en un servidor back-end `macOS`, las inyecciones deberían funcionar independientemente.
- La única excepción puede ser el punto y coma `;`, que no funcionará si el comando se ejecuta con `Línea de comandos de Windows (CMD)`, pero sí funcionará si se ejecuta con `Windows PowerShell`.
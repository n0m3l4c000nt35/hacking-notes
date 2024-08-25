# Inyeccion de comandos
1. [Introduccion a la inyeccion de comandos](#introduccion-a-la-inyeccion-de-comandos)
	1. [Que son las inyecciones](#que-son-las-inyecciones)
	2. [Inyección de comandos de sistema operativo](#inyeccion-de-comandos-de-sistema-operativo)
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
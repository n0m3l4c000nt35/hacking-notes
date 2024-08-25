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
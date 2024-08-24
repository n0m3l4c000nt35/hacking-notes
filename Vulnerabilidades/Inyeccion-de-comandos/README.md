# Inyeccion de comandos
1. [Introduccion a la inyeccion de comandos](#introduccion-a-la-inyeccion-de-comandos)
	1. [Que son las inyecciones](#que-son-las-inyecciones)
	2. [Inyección de comandos de sistema operativo](#inyeccion-de-comandos-de-sistema-operativo)
## Introduccion a la inyeccion de comandos
Una vulnerabilidad de inyección de comandos es uno de los tipos de vulnerabilidad más críticos.

Permite ejecutar comandos del sistema directamente en el servidor que aloja el back-end, lo que podría llevar a comprometer toda la red.

Si una aplicación web utiliza entradas controladas por el usuario para ejecutar comandos del sistema en el servidor back-end para recuperar o devolver una salida específica, es posible  inyectar un payload malicioso para alterar el comando esperado y ejecutar un comando que el servidor no espera ejecutar.
### Inyeccion de comandos de sistema operativo
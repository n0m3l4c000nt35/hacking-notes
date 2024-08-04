## Qué es XSS?
🔹 Vulnerabilidades XSS aprovechan fallas en la sanitización del input del usuario para escribir código JavaScript en la página y ejecutarlo en el lado del cliente, generando oportunidad para realizar distintos ataques a través del código JavaScript del navegador.<br />
🔹 Una aplicación web típica funciona recibiendo el código HTML del servidor back-end y representándolo en el navegador del lado del cliente.<br />
🔹 Cuando una aplicación web vulnerable no desinfecta adecuadamente el input del usuario, un usuario malintencionado puede inyectar código JavaScript adicional en un campo de entrada (por ejemplo, comentario/respuesta), de modo que una vez que otro usuario vea la misma página, ejecute el código JavaScript malicioso sin saberlo.<br />
🔹 Las vulnerabilidad XSS se ejecutan únicamente en el lado del cliente.<br />
🔹 No afectan directamente al servidor back-end.<br />
### Ejemplos
🔹 El usuario objetivo envía su cookie de sesión al servidor web del atacante sin saber.<br />
🔹 El navegador del objetivo ejecuta llamadas a la API que conducen a una acción maliciosa, como cambiar la contraseña del usuario por una contraseña elegida por el atacante.<br />
## Ataques XSS
🔹 Los ataques están limitados al motor JS del navegador (V8 en Chrome) ya que se ejecutan dentro del navegador.<br />
🔹 No pueden ejecutar código a nivel de sistema.<br />
🔹 En navegadores modernos están limitados al mismo dominio del sitio web vulnerable.<br />
## Tipos de XSS
| Tipo                           | Descripción                                                                                                                                                                                                     |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stored (Persistent) XSS        | El tipo de XSS más crítido.<br>Ocurre cuando el input del usuario se guarda en la base de datos del back-end y se muestra al recuperar ese dato.                                                                |
| Reflected (Non-persistent) XSS | Ocurre cuando el input del usuario se muestra en la página después de ser procesado por el servidor back-end pero sin ser guardado (resultados de búsquedas o mensajes de error).                               |
| DOM-based XSS (Non-persistent) | Ocurre cuando el input del usuario se muestra directamente en el navegador y es completamente procesado en el lado del cliente sin alcanzar el servidor back-end (a través de parámetros HTTP o etiquetas <a>). |
### Stored XSS
🔹 Afecta a cualquier usuario que visita la página infectada ya que el payload inyectado se guarda en la base de datos en el back-end.<br />
🔹 No es fácil de eliminar ya que necesita ser eliminado de la base de datos.<br />

```html
<script>alert(window.origin)</script>
```

```html
<img src="" onerror=alert(window.origin)>
```

🔹 Se debería ejecutar el código una vez ingresado el payload o cuando se actualice la página.<br />
🔹 Se confirma mirando el código fuente, en el que debería verse el payload.<br />

> [!NOTE]
> Muchas aplicaciones web modernas usan **cross-domain IFrames** (el contenido de los inputs se cargan desde un dominio diferente) para manejar el input del usuario, entonces aunque el input sea vulnerable a XSS no va a ser vulnerable en la aplicación principal.

🔹 Obtener el origen desde donde se está ejecutando el código es una manera de ver cuál es la entrada vulnerable.<br />
🔹 Algunos navegadores modernos bloquean la función JavaScript `alert`.<br />
🔹 `<plaintext>` muestra el código que viene después de el como texto plano.<br />
🔹 Para ver si el payload es persistente y se guarda en la base de datos se recarga la página para ver si el código se vuelve a ejecutar.<br />
🔹 Cualquier usuario que recargue la página va a ver la ejecución del código inyectado.<br />
### Reflexted XSS
🔹 Es procesado por el servidor back-end a través de solicitudes HTTP.<br />
🔹 Son temporales y solo existen hasta que se refresca la página.<br />
🔹 Solo afectan al usuario objetivo y no afecta a otros usuarios que visitan la página.<br />
🔹 Ocurre cuando el input es procesado por el servidor y devuelto al cliente sin filtrarlo ni sanitizarlo.<br />
🔹 En el código fuente se debería ver el payload inyectado.<br />
🔹 Para atacar a un usuario, se le puede enviar la URL que contiene el payload. Una vez que la víctima visitar la URL, el payload se ejecuta.<br />
### DOM XSS
🔹 Se procesa completamente del lado del cliente a través de JavaScript.<br />
🔹 Ocurre cuando se usa JavaScript para modificar la página a través del DOM (Document Object Model).<br />
🔹 No se ve el payload inyectado en el código fuente.<br />
#### Source & Sink
🔹 El **source** es el objeto JavaScript que toma el input del usuario.<br />
🔹 El **sink** es la función que escribe el input del usuario en un objeto del DOM en la página.<br />
🔹 Si el sink no sanitiza el input del usuario podría ser vulnerable a un ataque XSS.<br />
🔹 Funciones JavaScript que escriben en objetos del DOM:
- `document.write()`
- `DOM.innerHTML()`
- `DOM.outerHTML()`
🔹 Funciones `JQuery` que escriben en objetos del DOM:
- `add()`
- `after()`
- `append()`
## Descubriendo XSS
### Descubrimiento automatizado
- [XSStrike](https://github.com/s0md3v/XSStrike)
- [BruteXSS](https://github.com/rajeshmajumdar/BruteXSS)
- [XSSer](https://github.com/epsylon/xsser)
### Descubrimiento manual
Payloads:
- [Cross Site Scripting](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/XSS%20Injection/README.md)
- [Cross Site Scripting ( XSS ) Vulnerability Payload List](https://github.com/payloadbox/xss-payload-list)

### Revisión de código
## Defacing
## Phishing
## Session Hijacking
## Prevención
### Front-end
### Back-end
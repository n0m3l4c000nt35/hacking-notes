## Qué son los web proxies
🔹Para capturar las solicitudes y tráfico que pasa entre las aplicaciones y servidores backend y manipularlas para testearlas necesitamos **web proxies**.<br />
🔹Web proxies son herramientas especializadas que se configuran entre un navegador o aplicación móvil y un servidor backend para capturar y ver las solicitudes que se transmiten entre ambos, actuando como una herramienta man-in-the-middle.<br />
🔹Mientas que otras aplicaciones de Network Sniffing como Wireshark operan analizando el tráfico local para que pasa a través de una red, los web proxies principalmente funcionan con puertos web tales como el HTTP/80 y HTTPS/443.<br />
🔹Una vez configurado el web proxie, podemos ver todas las solicitudes HTTP hechas por una aplicación y todas las respuestas enviadas por el servidor backend.<br />
🔹Además, podemos interceptar una solicitud específica para modificar su información y ver como el servidor la maneja.<br />

## Usos de web proxies
- Scaneo de vulnerabilidades web
- Fuzzing web
- Web crawling
- Mapeo de aplicaciones web
- Análisis de solicitudes web
- Testeo de configuración web
- Revisión de código

## Web proxies
- Burp Suite
- ZAP

### Burp Suite
[Página oficial](https://portswigger.net/burp)<br />
🔹Características pagas:<br />
- Scanner activo de aplicaciones web
- Burp Intrudes más rápido
- Capacidad de cargar extensiones Burp

### OWASP Zed Attack Proxy (ZAP)
[Página oficial](https://www.zaproxy.org/)<br />
🔹Es gratuita, de código abierto, mantenida por la comunidad y no tiene características pagas<br />
## Estructura del sistema operativo
| Directorio          | Función                                                                                                                                                                                   |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Perflogs            | Contiene registros del rendimiento de Windows.                                                                                                                                            |
| Program Files       | En sistemas de 32 bits, los programas de 16 y 32 bits se instalan ahí.                                                                                                                    |
| Program Files (x86) | En sistemas de 64 bits, los programas de 16 y 32 bits se instalan ahí.                                                                                                                    |
| ProgramData         | Directorio oculto que contiene información esencial para la ejecución de ciertos programas. La información es accesible por cualquier programa no importa que usuario lo está ejecutando. |
| Users               | Contiene perfiles de cada usuario que inicia sesión en el sistema y contiene los directorios **Public** y **Default**.                                                                    |
| Default             | Plantilla de perfil de usuario para los usuarios creados. Los perfiles de usuarios creados se basan en esta plantilla.                                                                    |
| Public              | Directorio destinado para recursos compartidos. Es accesible para todos los usuarios por defecto. Se comparte sobre la red por defecto pero requiere una cuenta de red válida.            |

Obtener información del sistema operativo:

```powershell
Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber
```
## Sistema de archivos
## Permisos
## Recursos compartidos
## Acceso remoto
### Remote Desktop Protocol (RDP)
### xfreerdp
```bash
xfreerdp /v:<direccion-ip> /u:<usuario> /p:<contraseña>
```
## Servicios
## Procesos
## Sesiones de Windows
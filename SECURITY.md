# Política de seguridad

Overedge transmite todo lo que escribes, contraseñas incluidas. Cualquier falla de seguridad es prioridad.

## Cómo reportar una falla

> [!CAUTION]
> **No la publiques como issue, discusión ni en redes.** Un reporte público pone en riesgo a todos los que usan la app mientras se corrige.

Repórtala en privado desde **[Security → Report a vulnerability](../../security/advisories/new)** en este repositorio. Solo el equipo de Overedge puede verla.

Ayuda mucho incluir:

- la versión de Overedge y de cada sistema operativo;
- los pasos para repetirlo (un script o una prueba de concepto es ideal);
- qué podría lograr un atacante y en qué condiciones (por ejemplo, "alguien en la misma red Wi-Fi");
- si ya lo comentaste con alguien más.

## Qué puedes esperar

| Paso | Tiempo |
|---|---|
| Confirmamos que recibimos tu reporte | máximo **72 horas** |
| Te decimos si lo pudimos reproducir y qué tan grave es | máximo **7 días** |
| Corrección publicada para fallas críticas o altas | lo antes posible; te mantenemos al tanto |

Si quieres, te damos crédito en las notas de la versión que lo arregla. Pedimos que no publiques los detalles hasta que la corrección esté disponible; lo acordamos contigo.

## Versiones con soporte

| Versión | Soporte |
|---|---|
| 0.5.x | ✅ Recibe correcciones de seguridad |
| < 0.5 | ❌ Actualiza a la versión más reciente |

## Qué cubre

- La conexión entre computadoras: TLS, vinculación con SPAKE2, tokens y huella del certificado.
- El descubrimiento en la red local.
- Cómo se guardan las llaves y los tokens en cada sistema.
- La app en Windows y en macOS, incluida su interfaz.
- Los instaladores y archivos publicados en [Releases](../../releases).

## Fuera de alcance

- Que alguien de tu misma red vea los puertos abiertos (**TCP 24800** y **UDP 24801**). Sin el código de vinculación o un token válido, la conexión se corta en el saludo cifrado.
- Ataques que requieren acceso de administrador o físico a una computadora ya vinculada.
- Ataques de denegación de servicio por volumen dentro de tu propia red.
- El sitio [overedgeapp.com](https://overedgeapp.com), salvo que permita afectar a la app o a sus descargas.

## Cómo está protegida la conexión

| Capa | Qué hace |
|---|---|
| **TLS 1.3** | Todo el tráfico va cifrado. Si algún lado solo soporta TLS 1.2, se permiten únicamente suites ECDHE con AES-GCM o ChaCha20. |
| **Vinculación SPAKE2** | El código de 6 dígitos nunca viaja por la red. Los dos lados prueban que lo conocen con un protocolo PAKE atado a la huella del certificado. |
| **Huella fijada** | La Mac recuerda la huella SHA-256 de la PC. Si cambia, no envía nada y se niega a conectar. |
| **Llave privada protegida** | Certificado EC P-256. La llave privada se guarda cifrada y la frase que la abre vive en el Administrador de credenciales de Windows. |
| **Un token por Mac** | Token aleatorio de 256 bits en el Llavero de macOS; Windows guarda solo su hash. Cada Mac se puede desvincular por separado. |
| **Vinculación bajo demanda** | Cerrada por defecto; se abre 2 minutos, se cierra al vincular o tras 3 códigos incorrectos. El código nunca se guarda en disco. |
| **Resistencia a abusos** | Límites de intentos por IP que nunca afectan a una Mac ya vinculada, máximo de conexiones sin autenticar, tiempo límite para el saludo y rechazo de mensajes malformados. |
| **Solo red local** | El servidor rechaza conexiones desde IPs públicas. |
| **Interfaz blindada** | Política CSP sin recursos externos; todo texto que llega de la red se pinta como texto, nunca como HTML. |

Gracias por ayudar a que Overedge sea seguro para todos.

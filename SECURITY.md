# Seguridad

Overedge transmite todo lo que escribes, contraseñas incluidas, así que tomamos en serio cualquier falla.

## Cómo reportar una falla

**No la publiques como issue.** Repórtala en privado desde la pestaña **Security → Report a vulnerability** de este repositorio. Solo el equipo de Overedge puede verla.

Ayuda mucho incluir:
- la versión de Overedge y de los sistemas;
- los pasos para repetirlo;
- qué podría lograr un atacante.

## Qué puedes esperar

- Respuesta en un máximo de **72 horas**.
- Te mantenemos al tanto mientras lo corregimos.
- Si quieres, te damos crédito en las notas de la versión que lo arregla.

## Qué cubre

- La conexión entre computadoras: TLS, vinculación con SPAKE2, tokens y huella del certificado.
- El descubrimiento en la red local.
- Cómo se guardan llaves y tokens en cada sistema.
- La app en Windows y en macOS.

Overedge solo acepta conexiones de la red local. Que alguien de tu misma red vea el puerto abierto no es una falla por sí misma: sin el código de vinculación o un token válido, la conexión se corta en el saludo cifrado.

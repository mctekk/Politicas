Proceso de actualización
========================

Migraciones
-----------

Para manejar migraciones tendremos un branch especifico para subir migraciones, Cualquier migración que se dirija a staging o master debe pasar por un pull request desde el branch migration. Esto para evitar conflictos entre migraciones del mismo numero.

Las migraciones no deben tener la base de datos completa, a menos que sea la primera migración o que se ayan alterado todas/la mayoría de las tablas.

Para hacer una migración a una tabla en especifica se debe agregar el tag table de la siguiente forma

```ssh
	phalcon migration generate --table=mi_tabla
```

Que debe cumplirse para subir a development
-------------------------------------------

Estas son algunas de las cosas que debe cumplir un branch para hacer merge con development

 - El código no debe de contener errores de sintaxis.
 - El código debe estar debidamente documentado.
 - El programador debe revisar el código y cerciorarse que funcione.
 - Si el código puede afectar el comportamiento de otras áreas del sistema, se debe hacer las pruebas pertinentes.
 - El branch debe de estar actualizado al dia con los cambios de staging y development.
 - No se pueden subir código incompleto.
 - Los comentarios de los commit deben ser claros y hacer referencia al task si este esta registrado en Jira.

Que debe cumplirse para subir a Staging
---------------------------------------

Lo cambios a staging se suben periódicamente mediante pull request desde el branch development

- Cumplir con todo lo mencionado en development.
- Ser revisado por el responsable del proyecto.
- Haber pasado por las pruebas pertinentes.

Que debe cumplirse para subir a Master
--------------------------------------

Los cambios a master se suben periódicamente mediante pull request desde el branch development.

- Cumplir con todo lo mencionado en staging.
- Contener la validación de los usuarios family y el cliente.

Procesos de los Pull Request
----------------------------

###Antes de:
- Se debe revisar que se tienen todos los cambios que se quieren agregar al branch
- El código no debe de contener errores de sintaxis.
- El código debe estar debidamente documentado.
###Después de:
- El pull request debe de ser validado por algún compañero, si hay cambios se deben hacer y volver a solicitar una revision.
- Si el branch es development, staging o master la persona que haga el merge debe de ser el encargado del proyecto. De lo contrario el merge lo hace el que solicito el pull request.



Practicas para programar
========================

Modelos
-------

Los modelos deben representar la estructura de datos de la aplicación Web. Así pues los modelos deberían contener:

- Propiedades para representar datos específicos.
- Lógica del negocio que nos permita asegurar que los datos representados cumplen los requisitos del diseño.
- Adicionalmente, podría contener código para realizar la manipulación de los datos. 
- En general los modelos no deberían contener lógica que trata directamente con el usuario final. Más específicamente, los modelos no deberían contener:
	- \$_GET o $_POST pues son variables de datos del usuario final.
	- Código HTML o cualquier tipo de lógica de presentación (pues esto debería ser realizado en las vistas)

Vistas
------

Las vistas son las encargadas de presentar los modelos en el formato que el usuario requiera. Algunas características importantes a tomar en cuenta son:

- La mayor parte del contenido será HTML, pudiendo contener partes de php, javascript o css.
- Puede acceder a datos de los controladores y modelos de manera directa pero debería ser solamente con propósitos de presentación.
- Se debe evitar el acceso a variables que representan alguna petición del usuario. (\$_POST ó $_GET).
- Se debe evitar cualquier código que realice alguna consulta a la Base de Datos.

Controladores
-------------

Los controladores son la unión entre las vistas, los modelos y cualquier otro componente. Son el componente que debe "comprender" las peticiones que realiza el usuario. Entonces:

- Pueden lidiar con variables de pedido de los usuarios (\$_POST, $_GET).
- Pueden instanciar los modelos.
- Se debe evitar el uso de peticiones SQL pues estas peticiones van en los modelos.
- Se debe evitar el uso de HTML pues es mejor mantener este código en las vistas.
- Se debe evitar procesos lógicos estos deben de ir en librerías

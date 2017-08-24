#Nombramiento de las Ramas

##Principales

Manejaremos 3 ramas principales
<table>
  <thead>
    <tr>
      <th>Rama</th>
      <th>Descripción</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>development</td>
      <td>Es la versión en la que vamos integrando los cambios la aplicación (Base de datos de desarrollo)</td>
    </tr>
    <tr>
      <td>staging</td>
      <td>Es la versión de prueba que tiene los mismos cambios que producción (Copia de Base de datos de Producción)</td>
    </tr>
    <tr>
      <td>production</td>
      <td>La versión de producción (Base de datos de Producción)</td>
    </tr>
   
  </tbody>
</table>

De ser necesario se agregaran más ramas dependiendo de las exigencias del proyecto

##Secundarios

Las ramas secundarias son aquellos que tienen una importancia para el proyecto y estos estarán dentro de los repositorios con un tiempo de vida de 1 mes luego de haberse terminado el feature, bug o hotfix. Las mismas deben ser borradas por su creador y reportárselo a su Project Manager antes de eliminarlos.

### Convenciones de nombramiento de las ramas


Ejemplos
- sprint1 (código correspondiente al sprint 1)
- feature-report (Feature de reportes)
- feature-login (auth de usuario)
- feature-site (landing page del proyecto)

##Temporales

Las ramas temporales serán nombrados con la acción que se realizan en él. Estos se deben trabajar local sin ser subidos al repositorio y es de entera responsabilidad del programador que lo creo de conservarlo o eliminarlo según crea necesario.

Ejemplos:

Corrección de errores en los reportes

- fix-report (correcciones generales)
- fix-report-sellers (correcciones a vendedores)
- fix-report-buyers (correcciones a compradores)

No se debe poner el nombre a una rama que no explique con claridad para que fue creado.

Ejemplos que no se deben usar:

- not-working
- bug-reported
- fixes

##Merge ramas Principales

Para la unión de las ramas principales se harán de la siguiente forma.

merge desde las ramas secundarios a development

ejemplo:
```sh
(development)$ git merge feature-report
```

Merge desde development a staging

ejemplo:
```sh
(staging)$ git merge development
```
Merge desde staging a production (Solo project manager)
```sh
(production)$ git merge staging
```

##Corrección de errores en staging

Los errores de staging son los descubiertos por los usuarios finales y deben de ser resueltos directos en el staging esta es una excepción dentro de los push online. Las ramas deben de comenzar con hotfix- para que sean fácilmente identificado como correcciones en staging.

Pasos:

1 - Crear una rama desde staging

```sh
(staging)$ git branch hotfix-something
```

2 -  Corregir y hacer merge desde la rama creada a staging

```sh
(staging)$ git merge hotfix-something
```

3 - merge desde development a staging ya corregido

```sh
(development)$ git merge staging 
```

##Cambios grandes

Si el sistema tendrá un cambio grande se debe crear una rama, este nueva rama se nombrara "rama-pre/post-cambio" para recuperar los cambios si es necesario.

ejemplos:
```
  development-pre-vueToPhalcon
  development-post-mandrill
```

##Mensajes de los commits

Al hacer commit agregar descripción detallada de los cambios realizados, si estos cambios están respaldados por un task en Jira colocar delante el KEY del task separando con un guión (-) de la descripción.

>Getting in the habit of creating quality commit messages makes using and collaborating with Git a lot easier. As a general rule, your messages should start with a single line that’s no more than about 50 characters and that describes the changeset concisely, followed by a blank line, followed by a more detailed explanation. The Git project requires that the more detailed explanation include your motivation for the change and contrast its implementation with previous behavior – this is a good guideline to follow. It’s also a good idea to use the imperative present tense in these messages. In other words, use commands. Instead of “I added tests for” or “Adding tests for,” use “Add tests for.” 

Fuente: [Contributing to a Project](https://git-scm.com/book/ch5-2.html)

Ejemplos

```
	(development)$ git commit -m 'OOD-151 - Correcting problems with login'
```

#Versión

MCTekk trabajara con el Versionado Semántico [semver](http://semver.org/lang/es/) (mayor.menor.parche)

- mayor: el software sufre grandes cambios y mejoras.
- menor: se agrega un nuevo feature.
- parche: se aplican correcciones de errores.

Estas serán trabajadas y asignadas conjuntas a los realeses de los proyectos.

ejemplo:
- 1.0.0 Primera salida del proyecto alpha
- 1.0.1 Cambio rápido/Corrección de errores
- 1.1.0 New feature
- 1.2.5 New feature y corrección de errores

Los realeses y las versiones saldrán al finalizar los sprint

#FAQ

**Quien pude subir los cambios a producción?**

Solos los project manager pueden subir cambios a producción o personas que se les asigne esta tarea. 

**Si tengo un cambio pequeño debo crear una rama?**

No es necesario, puedes trabajarlo en una rama (secundario) que tenga que ver con el feature que estés corrigiendo.

**Si tengo un cambio considerable debe crear una rama?**

Si, pero este solo debe de ser local y unido a uno que ya se encuentre online (secundarios). Esto es para evitar que la data de una rama secundario se vea comprometida directamente.

**Si hay un cambio de urgencia en la rama de producción y no esta el project manager puedo subir el cambio?**

- En producción nunca debe de llegar un cambio de urgencia, todos los cambios deben pasar por development y luego staging para evitar que esto pase.
- La responsabilidad es enteramente directa al project manager, en caso de que este no se encuentre buscar a otro compañero con la misma posición para buscar una solución.

**Tengo conflictos con una rama ya que alguien mas publicó uno con el mismo nombre, que hago?**

Cambia el nombre a la rama para mantener la misma línea nombra la rama con el mismo nombre agregando le bk(backend) o ft(frontend)

```sh
git branch -m feature-report feature-report-bk // git branch -m old_branch new_branch
```

**Qué pasa si subo una rama temporal?**

Este debe de ser eliminado para evitar tener una cantidad grande de ramas en los repositorios online.

#Nombrar los Branches

##Principales

Manejaremos 3 branches principales

- develop: Es la versión en la que vamos integrando los cambios estables de los branches secundarios. (Local)
- staging: Es la versión que se usará en las empresas "family" (Semi production)
- master: La versión en productivo actual (production).

De ser necesario se agregaran mas branch dependiendo de las exigencias del proyecto

##Secundarios

Los branches secundarios son aquellos que tienen una importancia para el proyecto y estos estarán dentro de los repositorios con un tiempo de vida de 1 mes. Estos deben ser borrados por su creador y reportados a su project manager antes y después de eliminarlos.

Ejemplos
- sprint1 (código correspondiente al sprint 1)
- feature-report (Feature de reportes)
- feature-login (auth de usuario)
- feature-site (landing page del proyecto)

##Temporales

Los branchs temporales serán nombrados con la acción que se realizan en el. estos se deben trabajar local sin ser subidos al repositorio y es de entera responsabilidad del programador que lo creo de conservarlo o eliminarlo según crea necesario.

Ejemplos:

Corrección de errores en los reportes

- fixed-report (correcciones generales)
- fixed-report-sellers (correcciones a vendedores)
- fixed-report-buyers (correcciones a compradores)

No se debe poner el nombre a un branch que no explique con claridad para que fue creado.

Ejemplos que no se deben usar:

- daniel
- oorden
- js

##Merge branches Principales

Para la unión de los branches principales se harán de la siguiente forma.

**Merge desde los branches secundarios a develop**

ejemplo:
```sh
(develop)$ git merge feature-report
```

**Merge desde develop a staging**

ejemplo:
```sh
(staging)$ git merge develop
```

**Merge desde staging a master (Solo project manager)**

ejemplo:
```sh
(master)$ git merge staging
```

##Corrección de errores en staging

Los errores de staging son los descubiertos por los usuarios finales y deben de ser resueltos directos en el staging esta es una exepcion dentro de los push online. Los branches deben de comenzar con hotfix- para que sean facilmente identificado como correcciones en staging.

Pasos:

1- crear un branch desde staging (leer nombrar branch)

```sh
(staging)$ git branch hotfix-something
```

2- Corregir y hacer merge desde el branch creado a staging

```sh
(staging)$ git merge hotfix-something
```

3- merge desde develop a staging ya corregido

```sh
(develop)$ git merge staging 
```

##Cambios grandes

Si el sistema tendrá un cambio grande se debe crear un branch, este nuevo branch se nombrara "branch-pre/post-cambio" para recuperar los cambios si es necesario.

ejemplos:
```
  develop-pre-vueToPhalcon
  develop-post-mandrill
```

##Forma correcta de hacer commits

Al hacer commit agregar descripción detallada de los cambios realizados, si estos cambios están respaldados por un task en Jira colocar delante el KEY del task separando con un guión (-) de la descripción.

Ejemplos

```
	(develop)$ git commit -m 'OOD-151 - Correcting problems with login'
```

#Versión

Mctekk trabajara con el versionamiento mayor.menor.micro

- mayor: el software sufre grandes cambios y mejoras.
- menor: se agrega un nuevo feature.
- micro: se aplican correcciones de errores.

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

**Si tengo un cambio pequeño debo crear un branch?**

No es necesario, puedes trabajarlo en un branch (secundario) que tenga que ver con el feature que estés corrigiendo.

**Si tengo un cambio considerable debe crear un branch?**

Si, pero este solo debe de ser local y unido a uno que ya se encuentre online (secundarios). Esto es para evitar que la data de un branch secundario se vea comprometida directamente.

**Si hay un cambio de urgencia en el branch de producción y no esta el project manager puedo subir el cambio?**

- En producción nunca debe de llegar un cambio de urgencia, todos los cambios deben pasar por develop y luego staging para evitar que esto pase.
- La responsabilidad es enteramente directa al project manager, en caso de que este no se encuentre buscar a otro compañero con la misma posición para buscar una solución.

**Tengo conflictos con un branch ya que alguien mas publico uno con el mismo nombre, que hago?**

Cambia el nombre al branch. para mantener la misma linea nombra el branch con el mismo nombre agregando le bk(backend) o ft(frontend)

```sh
git branch -m feature-report feature-report-bk // git branch -m old_branch new_branch
```

**Que pasa si subo un branch temporal?**

Este debe de ser eliminado para evitar tener una cantidad grande de branch en los repositorios online.

**Que son las empresas "family"?**

Son los usuarios del sistemas mas cercanos al administrador, estos prueban las nuevas funciones antes de que lleguen a produccion. Se pueden tambien describir como usuarios beta tester

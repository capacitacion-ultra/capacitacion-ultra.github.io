# Proceso de trabajo

Para la realización de cualquier actividad relacionada con el desarrollo o mantenimiento de una pieza de software, en totalmente indispensable que se sigan los lineamientos siguientes:

## Sección I

Todo requerimiento debe ser solicitado a través de un simple formato llamado "Orden de trabajo" (en lo sucesivo ODT) que contenga la información siguiente:

1. ID
2. Fecha
3. Solicitante
4. Descripción de la solicitud
5. Necesidad que será atendida o problema que será resuelto
6. Diagramas explicativos (si es que son necesarios)
7. Requerimientos de los que depende este
8. Requerimientos que dependen de este
9. Complejidad del requerimiento en una métrica relativa (como Story points, o cosmi points, por ejemplo)
10. Lista de criterios de aceptación
11. Estatus de atención "enviado" inicialmente y posteriormente: aceptado, rechazado, en progreso, en revisión, terminado, o abortado
12. Responsable asignado y fecha de asignación (si aplica)
13. Ciclo de aceptación (este dato se registra posteriormente)

Cada ODT será colocada en un repositorio (tipo stack, o pila) global al proyecto llamado ```Repositorio Global de Órdenes de Trabajo``` que en lo sucesivo llamaremos ```ReGOT``` y puede ser elaborada por cualquier rol involucrado en el proyecto y en cualquier momento del proceso de desarrollo.

> Eso no quiere decir que serán atendidas o procesadas en el instante en el que sean creadas. De hecho, como se verá próximamente, serán priorizadas y atendidas acorde a su importantcia y/o urgencia.

Cada inicio de un nuevo ciclo, el ```ReGOT``` es revisado por el equipo y por un representante del negocio. A continuación, es **priorizado** (o reorganizado) para colocar las ODT's mas importantes (o en su caso, más urgentes) en el "top" del ```ReGOT```. De esta manera, aseguramos que al inicio de cada ciclo tendremos un ```ReGOT``` priorizado cuyos primeros elementos son especialmente relevantes ya sea por su importancia o por su urgencia a criterio del equipo de trabajo.

Los elementos en el ```ReGOT``` serán permanentes y no habrá manera de removerlos durante el ciclo de vida del proyecto. Sólo pueden ser editados para modificar su estatus o incluir un mayor claridad en su descripción o en su detalles.

# Sección II

En cada inicio de ciclo, el equipo tomará del ```ReGOT``` las ODT's que en conjunto determinen que pueden ser realizadas en el tiempo destinado a la duración del ciclo y (1) se cambiará su estatus a **aceptado** y (2) se registrará el ciclo en el que fue aceptado. 

Adicionalmente, si no se ha elegido a un responsable de manera previa, se procede a elegir uno en acuerdo con el equipo y considerando (a) las capacidades técnicas y (b) la carga de trabajo de cada miembro. Finalmente, se deberá registrar al responsable en el formato de ODT.

Las ODT's en el ```ReGOT``` cuyo estatus es "aceptado" para el ciclo N, representan el Repositorio Órdenes de Trabajo para el Ciclo N, que en lo sucesivo denominaremos como ```ReCOT``` para el ciclo N.

# Sección III

Una vez que se realizó el compromiso de entrega de las actividades del ```ReCOT```, en un ciclo dado, cada responsable deberá:
1. Crear una rama derivada de la rama de desarrollo
2. Clonar la rama creada en su entorno local de desarrollo
3. Producir la pieza de software
4. Generar el conjunto de pruebas unitarias con la cobertura acordada (alineados a RIICAAA)
5. Realizar, de manera ordenada y sistemática, commits de unidades completas de trabajo
6. Verificar el cumplimiento del DoD
7. Solicitar un PR (un PR es una revisión por uno o varios miembros del equipo del trabajo realizado por otro miembro, con sugerencias de cambio o mejora que se da en una secuencia de interacciones hasta que se agotan las observaciones de los revisores)
8. Atender a las observaciones del PR y buscar la aceptación de las mismas
9. Unir su rama de trabajo con la rama de desarrollo
10. Destruir la rama de trabajo
11. Cambiar el estatus de la ODT a "terminado" 

Lo anterior aplica para cada uno de los responsables y las actividades en el ```ReCOT``` hasta cumplir cada compromiso en El.

# Sección IV

El DoD es un documento que especifica cuáles son las actividades **adicionales** a la generación del producto, pruebas unitarias, y cobertura que deben ser realizadas para que un desarrollador esté en posibilidades de enviar a su equipo un PR. A continuación se presenta una sugerencia de DoD que generalmente es empleada por múltiples equipos de desarrollo:

1. Apego a estándares de codificación (en el lenguaje, en la base de datos, en los scripts de SO, etc)
2. Acoplamiento y cohesión (y aquí, de ser posible, complejidad ciclomática)
3. Code smells (mala indentación, uso indebido de asignaciones y valores boleanos, exceso de parámetros, uso indebido de excepciones, etc)
4. Pruebas de seguridad (inyección de sql, buffer overflow, cross site scripting, information disclosure, encrpción adecuada, digestión adecuada, validadores coherentes y congruentes, canal seguro, fortalez de contraseñas, etc)
5. Registro frecuente de operaciones en el log de transacciones
6. Inclusión de documentación de diversos tipos (javadoc, doble barra, barra estrella)
7. Congruencia en el uso del lenguaje nativo (No caer en el error de hacer variables en español y métodos en inglés)

Muchos de los puntos anteriores se pueden verificar de manera automática empleando software gratuito, como Sonar Lint, por ejemplo. Durante una revisión manual (como ocurre en un PR) también se dedica esfuerzo a validar este tipo de aspectos, pero el foco de un PR revisa principalmente la lógica de negocio y el apego a la arquitectura base y al diseño de la solución a la ODT trabajada.

Incumplir con los DoD genera dos grandes problemas:
1. Deuda técnica
2. Baja calidad en el producto de software

> Es interesante mencionar que el incumplimiento del DoD refleja una baja calidad en el proceso de Software y, consecuentemente, ello provoca una baja calidad en el producto de software.

# Sección V

Con las medidas anteriores, se puede asegurar que la calidad del producto de software será **mayor** que la que se tendría si no se llevarán a cabo; sin embargo, no es posible proporcionar un indicador de cuánto mejor. Evidentemente, porcentajes mayores de cobertura o una cercanía del 100% al indicador de "apego a estándares" hacen suponer una calidad superior, pero aun alcanzando altos niveles en los indicadores de las prácticas anteriores (que representaría un costo económico muy alto, para el proceso de desarrollo) no existe garantía de que el producto final esté libre de defectos.

De lo anterior, se recomienda el siguiente perfil de calidad: 

- Cobertura de pruebas unitarias: 70% (y sólo para las clases de servicio)
- Apego a estándares: 90%
- Code smells: 0% (para la totalidad del código)
- Documentación equivalente a la de javadoc: 100% (para las interfases de servicio)
- Documentación en línea (//) 20% de la totalidad de código de las clases de servicio
- Registro de operaciones relevantes en el log de transacciones: mayor a 10 registros por cada 100 líneas de código
- Revisión de elementos básicos de programación segura: 100%

Finalmente, se recomienda a los revisores de los PR que se enfoquen en los siguientes detalles:

- Diseño de la solución
- Compatibilidad del diseño con la arquitectura base
- Código malicioso
- Portabilidad
- Escalabilidad
- Eficiencia de la solución
- Implementación adecuada

# Sección VI

Una vez que el incremento (o pieza de software) ha pasado por las fases de implementación (con DoD incluído) y por su correspondiente PR de manera exitosa, el código de la rama de trabajo se une con el de la rama de desarrollo y esto dispara, de manera automática el proceso de integración continua y, posteriormente, el de despliegue continuo, que en lo sucesivo nombraremos como CI/CD.

El proceso de CI/CD es un proceso prácticamente automático que nos ayuda a realizar ciertas actividades rutinarias y tediosas que son candidatos a ejecutar de manera robótica. La siguiente lista de actividades es un ejemplo común de estos procesos:

- Obtener el código fuente de desarrollo
- Compilar el código
- Ejecutar pruebas unitarias de el código recién integrado MÁS TODAS las otras pruebas unitarias que se ejecutaron en el pasado
- Revisar que la cobertura de las pruebas recién integradas sea, cuando menos el 70% (del código de las clases de servicio)
- Revisar apego a estándares de codificación
- Revisar Code Smells
- Calcular el % del registro al log de transacciones
- Generar el paquete de distribución (en java es el jar, o el war, o el ear)
- Crear el contenedor del paquete (generalmente es un contenedor docker)
- Guardar el contenedor en el registro de contenedores (usando actualmente github packages)
- Producir el evento de despliegue (ejecutar un pod en kubernetes o invocar un script en el ambiente de despliegue)

# 1.1 Encuadre: objetivo del curso, mapa de contenidos y alcance

## Objetivo de la formación

El objetivo de este curso es proporcionar una visión práctica y realista de OpenShift como plataforma de ejecución y operación de aplicaciones basadas en contenedores.

Durante las distintas sesiones aprenderemos los conceptos fundamentales sobre los que se construye la plataforma, entenderemos cómo se organiza un clúster OpenShift y adquiriremos los conocimientos necesarios para desplegar, operar y diagnosticar aplicaciones dentro de un entorno empresarial.

El enfoque del curso está orientado a comprender cómo funcionan las plataformas modernas basadas en Kubernetes y OpenShift, priorizando el entendimiento de los conceptos sobre la memorización de comandos o procedimientos.

Al finalizar la formación, el alumno deberá ser capaz de:

- Comprender la relación entre contenedores, Kubernetes y OpenShift.
- Identificar los principales componentes de una plataforma OpenShift.
- Interpretar el estado de una aplicación desplegada.
- Utilizar la consola web y la herramienta de línea de comandos (`oc`) para tareas habituales de consulta y operación.
- Entender los patrones de despliegue y operación utilizados en entornos corporativos.

---

## Mapa del curso

La formación se estructura en varias sesiones que siguen una progresión lógica, comenzando por los conceptos fundamentales y avanzando posteriormente hacia aspectos de operación, despliegue y arquitectura.

### Día 1. Fundamentos de OpenShift

Comenzaremos construyendo una visión de conjunto de la plataforma:

- Contenedores e imágenes.
- Kubernetes como plataforma de orquestación de contenedores.
- Deployment, ReplicaSet, Pod, Service y DNS interno.
- Capacidades que OpenShift añade sobre Kubernetes.
- Arquitectura general de un clúster OpenShift.
- Consola web y herramienta de línea de comandos (`oc`).

El objetivo de esta primera sesión es comprender cómo se ejecuta una aplicación dentro de OpenShift, desde la imagen de contenedor hasta los recursos que la mantienen disponible y accesible dentro del clúster.

### Día 2. Recursos de aplicación

Profundizaremos en los recursos más utilizados para desplegar aplicaciones:

- Deployments.
- Services.
- Routes.
- ConfigMaps.
- Secrets.
- Variables de entorno.
- Consumo de almacenamiento.

El foco estará en comprender cómo se define y configura una aplicación dentro de la plataforma.

### Día 3. Construcción y ciclo de vida

Analizaremos las distintas opciones para construir, versionar y promocionar aplicaciones:

- Imágenes de contenedor.
- Registros de imágenes.
- Pipelines.
- Estrategias de despliegue.
- Operadores.
- Automatización.

Se explicarán los patrones habituales utilizados en entornos corporativos para la gestión del ciclo de vida de las aplicaciones.

### Día 4. Operación y diagnóstico

Nos centraremos en la operación diaria de la plataforma:

- Observabilidad.
- Logs.
- Eventos.
- Diagnóstico de incidencias.
- Consumo de recursos.
- Resolución de problemas frecuentes.

El objetivo será adquirir una metodología básica para analizar incidentes y comprender el comportamiento de las aplicaciones desplegadas.

---

## Enfoque de la formación

La formación sigue una aproximación progresiva.

Primero entenderemos los conceptos sobre los que se construyen los contenedores, Kubernetes y OpenShift.

Después veremos cómo dichos conceptos aparecen y se materializan dentro de la plataforma.

Finalmente aprenderemos a utilizarlos y operarlos mediante la consola web y la herramienta de línea de comandos.

Siempre que sea posible se utilizarán ejemplos cercanos a situaciones reales de operación de plataformas empresariales.

El objetivo no es convertir al alumno en administrador experto de OpenShift al finalizar el curso, sino proporcionarle una base sólida que le permita comprender cómo funciona la plataforma y desenvolverse con seguridad en ella.

---

## Qué no cubre este curso

Es importante delimitar el alcance de la formación.

Este curso no pretende profundizar en:

- Administración avanzada de clústeres OpenShift.
- Instalación de OpenShift.
- Diseño de arquitecturas empresariales complejas.
- Desarrollo avanzado de operadores.
- Administración avanzada de Kubernetes.
- Automatización avanzada de pipelines o GitOps.

Estos temas requieren conocimientos previos y una dedicación específica que quedan fuera del alcance de esta formación introductoria.

---

## Una consideración importante

Los ejemplos, patrones y recomendaciones que aparecerán a lo largo del curso están inspirados en plataformas OpenShift desplegadas y operadas en entornos reales.

Sin embargo, el entorno utilizado durante las prácticas tiene fines formativos.

Por este motivo, algunas configuraciones, capacidades o procedimientos pueden simplificarse respecto a los existentes en una plataforma corporativa en producción.

El interés de la formación no está en conocer los detalles concretos del clúster del laboratorio, sino en comprender los principios y patrones que posteriormente encontraremos en cualquier plataforma OpenShift empresarial.

---

## Resumen

Antes de comenzar con OpenShift es importante entender el recorrido que seguiremos durante la formación.

Empezaremos por los contenedores y Kubernetes, estudiaremos cómo OpenShift amplía sus capacidades, aprenderemos a utilizar las herramientas de acceso y operación de la plataforma y, posteriormente, profundizaremos en los recursos y mecanismos necesarios para desplegar y operar aplicaciones en entornos corporativos.

Con este marco común podremos abordar el resto del curso desde una comprensión compartida de los conceptos fundamentales.

# 1.2 De servidor a contenedor

## Objetivos de aprendizaje

Al finalizar este apartado serás capaz de:

- Comprender la diferencia entre una aplicación instalada en un servidor tradicional y una aplicación ejecutada en un contenedor.
- Entender qué es una imagen de contenedor.
- Comprender qué es una imagen base.
- Comprender qué es un contenedor y su relación con una imagen.
- Comprender por qué los contenedores se consideran efímeros.
- Entender la filosofía de sustituir en lugar de parchear.
- Interpretar los elementos básicos de un Dockerfile.

---

## Del servidor tradicional al contenedor

Durante muchos años, el despliegue de aplicaciones siguió un modelo similar:

1. Se preparaba un servidor físico o una máquina virtual.
2. Se instalaba el sistema operativo.
3. Se instalaban librerías y dependencias.
4. Se desplegaba y configuraba la aplicación.
5. Se realizaban actualizaciones y cambios sobre ese mismo servidor.

Con el paso del tiempo, cada servidor acababa teniendo una configuración propia.

Era habitual escuchar frases como:

> "En mi servidor funciona perfectamente."

El problema es que reproducir exactamente el mismo entorno en otro servidor no siempre era sencillo. Una diferencia de versión, una librería instalada manualmente o una modificación realizada meses atrás podían provocar comportamientos distintos.

Los contenedores surgen precisamente para solucionar este problema.

La idea es sencilla:

> En lugar de transportar instrucciones para instalar una aplicación, transportamos la aplicación ya preparada para ejecutarse.

---

## Un cambio en la forma de desplegar, no en la forma de programar

Cuando se empieza a trabajar con plataformas de contenedores suele surgir una duda frecuente:

> ¿Tengo que aprender a programar para OpenShift?

La respuesta es no.

OpenShift no define cómo se desarrolla una aplicación. Una aplicación Java sigue desarrollándose en Java, una aplicación .NET sigue desarrollándose en .NET y una aplicación Python sigue desarrollándose en Python.

Lo que cambia es la forma en la que la aplicación se empaqueta, se despliega y se opera.

Podemos compararlo con el paso que muchas organizaciones dieron al migrar de servidores físicos a máquinas virtuales. El software seguía siendo el mismo, pero cambiaba la plataforma sobre la que se ejecutaba.

De forma simplificada, la evolución ha sido:

```text
Servidor físico
       ↓
Máquina virtual
       ↓
Contenedor
```

En este curso nos centraremos en comprender este último paso y en cómo OpenShift facilita la ejecución y operación de aplicaciones basadas en contenedores.

---

## ¿Qué es una imagen de contenedor?

Una imagen es un paquete que contiene todo lo necesario para ejecutar una aplicación.

Normalmente incluye:

- Un sistema operativo o parte de él.
- Librerías necesarias.
- Dependencias.
- Componentes de ejecución.
- Código de la aplicación.
- Configuración básica de arranque.

Podemos pensar en una imagen como una plantilla inmutable.

Una vez creada, la imagen no cambia.

Por ejemplo:

```text
empresa/web:v1
```

Esta imagen contiene una versión concreta de una aplicación web.

Si la copiamos a distintos entornos:

- Desarrollo
- Pruebas
- Producción

siempre será exactamente la misma.

Esto aporta consistencia y reduce errores.

---

## La imagen base: el punto de partida

Rara vez una imagen se construye desde cero.

Lo habitual es partir de una imagen base sobre la que se añade la aplicación.

Podemos pensar en ella como la capa de sistema operativo y componentes comunes que servirán de fundamento para nuestra aplicación.

Por ejemplo:

```text
Imagen base
(Red Hat UBI + Java)
          +
Código de la aplicación
          +
Configuración
          =
Imagen final
```

La imagen base suele contener:

- Un sistema operativo ligero.
- Librerías básicas.
- Componentes comunes.
- Un lenguaje o entorno de ejecución (Java, Python, Node.js, .NET, etc.).

El equipo de desarrollo se centra en la aplicación, mientras que otros componentes ya vienen preparados en la imagen base.

### ¿Quién mantiene la imagen base?

La responsabilidad de las imágenes base depende del modelo organizativo de cada empresa.

Habitualmente intervienen varios equipos:

- Equipo de plataforma o OpenShift.
- Equipo de infraestructura o sistemas.
- Equipo de seguridad.
- Equipo DevOps o CI/CD.
- Equipos de desarrollo.

Lo importante es que exista un proceso común para definir qué imágenes pueden utilizarse en la organización.

Por ejemplo:

```text
Fabricante (Red Hat)
          ↓
Imagen base aprobada
          ↓
Repositorio corporativo
          ↓
Equipos de desarrollo
```

En muchas organizaciones, el equipo responsable de la plataforma OpenShift participa en este proceso, pero no suele ser el único responsable.

Con frecuencia, la selección, validación y actualización de imágenes base se realiza de forma conjunta con los equipos de seguridad y arquitectura.

### Imágenes certificadas y homologadas

Una práctica habitual en entornos empresariales consiste en que los desarrolladores no utilicen directamente imágenes obtenidas de Internet.

En su lugar, la organización define un catálogo de imágenes aprobadas y mantenidas corporativamente.

```text
Red Hat UBI
      ↓
Validación corporativa
      ↓
Imagen base corporativa
      ↓
Aplicaciones de la organización
```

De esta forma:

- Los equipos de desarrollo utilizan componentes homologados.
- El equipo de seguridad puede validar los componentes incluidos.
- El equipo de plataforma puede controlar qué imágenes se distribuyen dentro del entorno OpenShift.
- Se simplifica la gestión de vulnerabilidades y actualizaciones.

En resumen, no se pierde el control. Al contrario, se centraliza y se gobierna de forma más eficiente.

---

## Lectura básica de un Dockerfile

Ya sabemos qué es una imagen y qué es una imagen base.

La siguiente pregunta es:

> ¿Cómo se construye una imagen?

La respuesta habitual es mediante un Dockerfile.

Un Dockerfile es un fichero de texto que describe las instrucciones necesarias para construir una imagen de contenedor.

Durante este curso no aprenderemos a escribir Dockerfiles complejos, pero sí es importante poder interpretar uno sencillo.

Ejemplo:

```dockerfile
FROM ubi9/openjdk-17

COPY app.jar /opt/app/app.jar

EXPOSE 8080

CMD ["java", "-jar", "/opt/app/app.jar"]
```

Veamos qué significa cada línea.

### FROM

```dockerfile
FROM ubi9/openjdk-17
```

Indica la imagen base.

Es el punto de partida sobre el que construiremos nuestra aplicación.

En este caso se utiliza una imagen con Java ya instalado.

### COPY

```dockerfile
COPY app.jar /opt/app/app.jar
```

Copia el fichero de la aplicación al interior de la imagen.

### EXPOSE

```dockerfile
EXPOSE 8080
```

Indica el puerto utilizado por la aplicación.

### CMD

```dockerfile
CMD ["java", "-jar", "/opt/app/app.jar"]
```

Define el comando que se ejecutará cuando arranque el contenedor.

De forma simplificada, el proceso sería:

```text
Imagen base
      +
Aplicación
      +
Instrucciones Dockerfile
      ↓
Imagen final
```

---

## ¿Qué es un contenedor?

Una imagen por sí sola no hace nada.

Cuando la ejecutamos obtenemos un contenedor.

Si ya has trabajado con virtualización, puedes pensar en una imagen de contenedor de forma parecida a una plantilla de máquina virtual.

```text
Plantilla VM
      ↓
Máquina Virtual

Imagen
   ↓
Contenedor
```

En ambos casos existe una definición reutilizable a partir de la cual se crean instancias de ejecución.

La diferencia es que una máquina virtual incluye un sistema operativo completo, mientras que una imagen de contenedor contiene únicamente lo necesario para ejecutar la aplicación.

Además, los contenedores son normalmente más ligeros y rápidos de crear que una máquina virtual tradicional.

Una única imagen puede utilizarse para crear múltiples contenedores.

```text
               Imagen
         empresa/web:v1
                    │
       ┌────────────┼────────────┐
       │            │            │
       ▼            ▼            ▼

 Contenedor-1  Contenedor-2  Contenedor-3

   Ejecutando   Ejecutando   Ejecutando
      APP          APP          APP
```

Todos parten de la misma definición inicial, pero cada contenedor se ejecuta como una instancia independiente.

Podemos resumir la relación de la siguiente manera:

```text
Imagen
   ↓
¿Qué obtenemos al ejecutarla?
   ↓
Contenedor
```

---

## El contenedor es efímero

Uno de los cambios de mentalidad más importantes al trabajar con contenedores es entender que el contenedor no está pensado para durar indefinidamente.

En un entorno tradicional era habitual:

- Conectarse al servidor.
- Modificar archivos manualmente.
- Instalar paquetes.
- Corregir configuraciones sobre la marcha.

Con contenedores la filosofía es diferente.

Si un contenedor falla:

```text
Contenedor antiguo
        ↓
 Se elimina
        ↓
Contenedor nuevo
```

Lo importante no es el contenedor concreto, sino la imagen desde la que se creó.

También podemos representarlo de esta manera:

```text
Imagen
empresa/web:v1
      │
      │ ejecutar
      ▼

Contenedor
empresa/web-abc123

      │
      │ eliminar
      ▼

Contenedor desaparece

      │
      │ volver a crear
      ▼

Nuevo contenedor
empresa/web-xyz789
```

Por ello, los cambios realizados manualmente dentro de un contenedor suelen considerarse temporales.

---

## Sustituir en lugar de parchear

Este principio es una de las bases de las plataformas cloud-native como OpenShift.

### Modelo tradicional

```text
Servidor existente
       ↓
Modificar
       ↓
Actualizar
       ↓
Corregir errores
```

Con el tiempo resulta difícil saber exactamente qué cambios se han realizado.

### Modelo basado en imágenes

```text
Crear nueva imagen
        ↓
Desplegar nuevo contenedor
        ↓
Retirar el anterior
```

De esta forma:

- Los cambios quedan controlados.
- Es más sencillo volver atrás.
- Los despliegues son más predecibles.
- Se reducen las diferencias entre entornos.

Cuando una aplicación necesita una nueva versión, normalmente no se modifica el contenedor existente.

Se genera una nueva imagen y se despliega una nueva instancia.

---

## ¿Qué ocurre cuando cambia la aplicación?

En un modelo tradicional era frecuente actualizar directamente el servidor donde se ejecutaba la aplicación.

En plataformas basadas en contenedores la aproximación es diferente.

Cuando una aplicación incorpora cambios en su código:

```text
Nuevo código
      ↓
Nueva imagen
      ↓
Nuevo contenedor
```

El contenedor que estaba ejecutándose no suele modificarse.

En su lugar, se genera una nueva imagen que incorpora los cambios y se despliega un nuevo contenedor a partir de ella.

Por ejemplo:

```text
empresa/web:v1
       ↓
Contenedor versión 1

Cambio en la aplicación

empresa/web:v2
       ↓
Contenedor versión 2
```

### ¿Y si el código no cambia?

Una nueva imagen no se crea únicamente cuando cambia la aplicación.

También puede ser necesario generar una nueva versión cuando cambia alguno de sus componentes.

Por ejemplo, si aparece una vulnerabilidad en la imagen base:

```text
Imagen v1

Base v1
+
Aplicación v1
```

Tras aplicar las correcciones necesarias:

```text
Imagen v2

Base v2
+
Aplicación v1
```

En este caso:

- El código de la aplicación no ha cambiado.
- La imagen sí ha cambiado.
- Debe desplegarse un nuevo contenedor.

Por tanto, una nueva imagen puede generarse por distintos motivos.

**Cambio en la aplicación**

```text
Base v1 + Aplicación v1
           ↓
Base v1 + Aplicación v2
```

**Cambio en la imagen base**

```text
Base v1 + Aplicación v1
           ↓
Base v2 + Aplicación v1
```

**Cambio en ambos**

```text
Base v1 + Aplicación v1
           ↓
Base v2 + Aplicación v2
```

En todos los casos:

```text
Nueva imagen
      ↓
Nuevo contenedor
```

---

## ¿Por qué es importante entender esto en OpenShift?

OpenShift trabaja continuamente con imágenes y contenedores.

Aunque muchas tareas estarán automatizadas, es fundamental comprender algunos conceptos básicos:

- Las aplicaciones se despliegan a partir de imágenes.
- Un mismo despliegue puede crear múltiples contenedores.
- Los contenedores pueden ser reemplazados automáticamente.
- Las modificaciones deben realizarse en el proceso de construcción de la imagen y no directamente sobre los contenedores en ejecución.

Comprender esta filosofía facilitará posteriormente el entendimiento de Kubernetes y OpenShift, donde los contenedores se crean, eliminan y sustituyen de forma continua como parte del funcionamiento normal de la plataforma.

# 1.3 Kubernetes: la capa de orquestación de contenedores

## Objetivos de aprendizaje

Al finalizar este apartado serás capaz de:

- Comprender qué problema resuelve Kubernetes.
- Entender cómo ayuda a desplegar, escalar y recuperar aplicaciones.
- Comprender los conceptos de estado deseado y estado real.
- Entender qué es el bucle de reconciliación.
- Identificar el papel de los Deployments, ReplicaSets y Pods.
- Comprender para qué sirven los Services.
- Entender el papel de las etiquetas y selectores.

---

# De los contenedores a la orquestación

En el apartado anterior vimos cómo los contenedores permiten empaquetar una aplicación junto con todas sus dependencias, facilitando que pueda ejecutarse de forma consistente en distintos entornos.

Sin embargo, los contenedores por sí solos no resuelven todos los problemas.

Ejecutar una única aplicación en un único contenedor es relativamente sencillo. El verdadero reto aparece cuando debemos gestionar decenas, cientos o incluso miles de contenedores distribuidos entre múltiples servidores.

Por ejemplo:

- ¿Qué ocurre si un contenedor se detiene inesperadamente?
- ¿Cómo ejecutamos varias copias de una aplicación?
- ¿Cómo repartimos la carga entre ellas?
- ¿Cómo actualizamos una aplicación sin interrumpir el servicio?
- ¿Cómo garantizamos que las aplicaciones sigan funcionando después de un fallo?

A medida que aumenta el número de aplicaciones, la gestión manual deja de ser viable.

Aquí es donde aparece Kubernetes.

---

# ¿Qué es Kubernetes?

Kubernetes es una plataforma de orquestación de contenedores.

Cuando hablamos de orquestación nos referimos a la capacidad de coordinar automáticamente la ejecución de aplicaciones basadas en contenedores.

Kubernetes no sustituye a los contenedores.

Los contenedores siguen siendo el mecanismo mediante el cual se ejecutan las aplicaciones.

Lo que aporta Kubernetes es la capacidad de gestionarlos de forma automática y a gran escala.

Podemos representarlo de forma simplificada así:

```text
Aplicación
     ↓
Contenedor
     ↓
Kubernetes
     ↓
Gestión automática
```

Por este motivo suele decirse que Kubernetes es la capa de orquestación situada por encima de los contenedores.

---

# Los tres problemas principales que resuelve Kubernetes

Aunque Kubernetes incorpora muchas capacidades, todas ellas giran alrededor de tres necesidades fundamentales:

- Despliegue.
- Escalado.
- Recuperación ante fallos.

## Despliegue

Kubernetes permite poner aplicaciones en funcionamiento de forma repetible y controlada.

En lugar de arrancar contenedores manualmente, describimos cómo queremos que sea la aplicación y la plataforma se encarga de crear los recursos necesarios.

La idea es similar a pedir un resultado, no una lista de pasos.

---

## Escalado

Las necesidades de una aplicación pueden cambiar con el tiempo.

Una aplicación que inicialmente necesita una única instancia puede requerir varias copias cuando aumenta la carga de trabajo.

Por ejemplo:

```text
1 Pod
 ↓
3 Pods
 ↓
5 Pods
```

Kubernetes facilita aumentar o reducir el número de instancias sin necesidad de gestionar manualmente cada contenedor.

---

## Recuperación ante fallos

En cualquier entorno real pueden producirse errores:

- Un proceso puede detenerse.
- Un contenedor puede finalizar inesperadamente.
- Un servidor puede sufrir una avería.

Kubernetes supervisa continuamente la situación del entorno.

Si detecta que una aplicación ha dejado de estar disponible, intentará restaurarla automáticamente.

Por ejemplo:

```text
Pod funcionando
       ↓
    Falla
       ↓
Kubernetes detecta el problema
       ↓
Se crea un nuevo Pod
```

Esta capacidad de recuperación automática es una de las características más importantes de la plataforma.

---

# La idea clave: estado deseado y estado real

Para comprender Kubernetes es necesario entender un concepto fundamental.

Normalmente no indicamos a Kubernetes los pasos exactos que debe realizar.

Lo que hacemos es describir el resultado que esperamos obtener.

Por ejemplo:

```text
Quiero 3 instancias de mi aplicación
```

Eso representa el **estado deseado**.

Por otro lado, la situación real existente en cada momento dentro del clúster representa el **estado real**.

Por ejemplo:

```text
Estado deseado: 3 Pods

Estado real: 2 Pods
```

En este caso existe una diferencia entre ambos estados.

Kubernetes detectará esa discrepancia y actuará para corregirla.

Su objetivo permanente consiste en hacer que el estado real coincida con el estado deseado.

---

# El bucle de reconciliación

El mecanismo mediante el cual Kubernetes mantiene alineados ambos estados se denomina **bucle de reconciliación**.

De forma simplificada, el proceso sigue continuamente este ciclo:

```text
Estado deseado
        ↓
   Comparación
        ↓
 Estado real
        ↓
   Corrección
        ↓
Nueva comprobación
```

Este proceso nunca se detiene.

Kubernetes está observando continuamente el sistema y corrigiendo cualquier desviación respecto a lo solicitado.

Por ejemplo:

```text
Deseado: 3 Pods
Real:    3 Pods
```

No es necesaria ninguna acción.

Si posteriormente uno de ellos desaparece:

```text
Deseado: 3 Pods
Real:    2 Pods
```

Kubernetes detectará la diferencia y creará automáticamente un nuevo Pod.

Una vez completada la corrección:

```text
Deseado: 3 Pods
Real:    3 Pods
```

La situación vuelve a coincidir con lo solicitado.

Este comportamiento está presente en prácticamente todos los componentes de Kubernetes y OpenShift.

---

# Cómo mantiene Kubernetes una aplicación

Cuando trabajamos con Kubernetes normalmente no creamos Pods individuales.

Lo habitual es trabajar con un recurso denominado **Deployment**.

Un Deployment describe cómo debe ejecutarse una aplicación:

- Qué imagen debe utilizar.
- Cuántas instancias deben existir.
- Cómo deben aplicarse las actualizaciones.

Internamente Kubernetes utiliza varios componentes para mantener ese estado deseado.

La relación habitual puede representarse así:

```text
Deployment
      ↓
ReplicaSet
      ↓
Pod
```

Cada elemento tiene una responsabilidad diferente:

- **Deployment**: define cómo debe ejecutarse la aplicación.
- **ReplicaSet**: garantiza que exista el número correcto de Pods.
- **Pod**: es donde realmente se ejecutan los contenedores de la aplicación.

Sin embargo, desde el punto de vista del usuario, normalmente se trabaja con Deployments y no directamente con ReplicaSets.

Si alguno de los Pods desaparece, Kubernetes detectará la diferencia respecto al estado deseado y creará automáticamente uno nuevo para recuperar la situación esperada.

---

# Etiquetas y selectores

Kubernetes relaciona muchos de sus recursos mediante etiquetas.

Las etiquetas permiten identificar y clasificar recursos mediante pares clave-valor.

Por ejemplo:

```text
app=web
entorno=desarrollo
```

Los **selectores** permiten localizar recursos a partir de esas etiquetas.

Por ejemplo:

```text
app=web
```

puede utilizarse para localizar todos los recursos asociados a una determinada aplicación.

Muchos componentes de Kubernetes utilizan etiquetas y selectores para relacionarse entre sí.

Por este motivo suele decirse que constituyen el pegamento que conecta los distintos recursos de la plataforma.

Más adelante veremos ejemplos prácticos de este mecanismo cuando estudiemos otros componentes de OpenShift.

---

# Service: un punto de acceso estable

Los Pods son recursos efímeros.

Pueden desaparecer y volver a crearse en cualquier momento.

Cuando eso ocurre, también puede cambiar su dirección IP.

Para evitar depender de direcciones IP concretas, Kubernetes utiliza un recurso denominado **Service**.

Un Service proporciona un punto de acceso estable para acceder a una aplicación, independientemente de los Pods concretos que existan en cada momento.

```text
              Service
                  │
                  ▼
       ┌──────┬──────┬──────┐
       ▼      ▼      ▼
     Pod    Pod    Pod
```

De esta forma las aplicaciones acceden al Service y Kubernetes se encarga de dirigir las peticiones hacia los Pods disponibles.

Además, Kubernetes registra automáticamente un nombre DNS interno asociado al Service.

Esto permite que otras aplicaciones del clúster puedan comunicarse utilizando un nombre estable, sin necesidad de conocer las direcciones IP concretas de los Pods que están ejecutándose en cada momento.

---

# Ideas clave para recordar

- Kubernetes es una plataforma de orquestación de contenedores.
- Su función principal es automatizar la operación de aplicaciones basadas en contenedores.
- Resuelve tres necesidades fundamentales: despliegue, escalado y recuperación ante fallos.
- Kubernetes trabaja continuamente para hacer coincidir el estado real con el estado deseado.
- Este comportamiento se implementa mediante el bucle de reconciliación.
- Los usuarios trabajan habitualmente con Deployments para definir cómo debe ejecutarse una aplicación.
- Kubernetes utiliza ReplicaSets para mantener el número de Pods solicitado.
- Los Pods son la unidad donde realmente se ejecutan los contenedores.
- Muchos recursos de Kubernetes se relacionan mediante etiquetas y selectores.
- Los Services proporcionan un punto de acceso estable a las aplicaciones.
- Kubernetes asigna automáticamente nombres DNS internos a los Services para facilitar la comunicación entre aplicaciones.
- OpenShift utiliza Kubernetes como motor de orquestación y amplía sus capacidades.




# 1.4 Qué añade OpenShift

## Objetivos de aprendizaje

Al finalizar este apartado serás capaz de:

- Comprender que OpenShift se construye sobre Kubernetes y añade capacidades adicionales.
- Identificar algunos de los recursos más característicos de OpenShift.
- Comprender la diferencia entre Project y Namespace.
- Entender el propósito de las Routes.
- Comprender el objetivo de las Security Context Constraints (SCC).
- Reconocer la existencia de BuildConfig como mecanismo de construcción de imágenes.
- Entender qué es un operador y por qué es un concepto fundamental en OpenShift.
- Comprender el papel de OperatorHub como mecanismo de extensión de la plataforma.

---

# Kubernetes y OpenShift: relación entre ambos

En el apartado anterior hemos estudiado Kubernetes como plataforma de orquestación de contenedores.

OpenShift no sustituye Kubernetes.

OpenShift utiliza Kubernetes como base y añade un conjunto de componentes y funcionalidades orientadas a facilitar la construcción, operación y administración de plataformas empresariales.

Podemos representarlo de forma simplificada de la siguiente manera:

```text
Aplicaciones
      ↓
OpenShift
      ↓
Kubernetes
      ↓
Contenedores
      ↓
Sistema operativo
```

Todos los conceptos fundamentales que hemos visto hasta ahora siguen existiendo:

- Pods.
- Deployments.
- Services.
- Namespaces.
- ConfigMaps.
- Secrets.

Sin embargo, OpenShift incorpora además recursos y capacidades adicionales que simplifican tareas habituales relacionadas con la seguridad, el ciclo de vida de las aplicaciones y la operación de la plataforma.

A continuación veremos algunas de las más representativas.

---

# Projects: el espacio de trabajo habitual

En Kubernetes existe el concepto de Namespace.

Un namespace permite organizar y separar recursos dentro de un clúster.

OpenShift introduce el concepto de **Project**.

Desde el punto de vista técnico, un Project se apoya sobre un namespace de Kubernetes, pero añade funcionalidades relacionadas con la gestión de usuarios, permisos y experiencia de uso.

De forma simplificada:

```text
OpenShift
 Project
    ↓
Kubernetes
 Namespace
```

Por este motivo, cuando trabajamos en OpenShift normalmente hablamos de proyectos y no de namespaces.

Por ejemplo:

```text
equipo-a-dev
equipo-a-test
equipo-a-prod
```

Cada proyecto contiene sus propios recursos:

- Pods.
- Deployments.
- Services.
- Routes.
- ConfigMaps.
- Secrets.

Esto permite separar aplicaciones, equipos y entornos dentro de una misma plataforma.

Durante las prácticas del curso cada alumno trabajará habitualmente dentro de su propio proyecto.

---

# Routes: publicar aplicaciones fuera del clúster

En el apartado anterior vimos que un Service proporciona acceso estable a una aplicación dentro del clúster.

Sin embargo, normalmente también necesitamos acceder desde el exterior.

Para resolver esta necesidad OpenShift incorpora el recurso **Route**.

Podemos visualizarlo así:

```text
Usuario
    ↓
Route
    ↓
Service
    ↓
Pods
```

La Route proporciona un nombre DNS accesible desde fuera de la plataforma y dirige las peticiones hacia el Service correspondiente.

Por ejemplo:

```text
https://mi-aplicacion.apps.empresa.com
```

Gracias a las Routes, las aplicaciones pueden publicarse de forma sencilla para ser utilizadas por otros usuarios o sistemas.

Más adelante veremos este mecanismo con mayor detalle.

Por ahora basta con recordar una idea:

**Service resuelve el acceso interno.**

**Route resuelve el acceso externo.**

---

# BuildConfig: construcción de imágenes en OpenShift

OpenShift incorpora mecanismos para construir imágenes dentro de la propia plataforma.

Uno de los recursos asociados a esta capacidad es **BuildConfig**.

De forma simplificada:

```text
Código fuente
      +
 Dockerfile
      ↓
 BuildConfig
      ↓
 Construcción
      ↓
 Imagen
      ↓
 Registro de imágenes
```

Un BuildConfig define cómo debe realizarse una construcción de imagen dentro de OpenShift.

Habitualmente describe aspectos como:

- El origen del código fuente.
- La estrategia de construcción utilizada.
- El destino de la imagen resultante.

BuildConfig no sustituye al Dockerfile. El Dockerfile sigue describiendo cómo se construye la imagen, mientras que BuildConfig define y coordina el proceso de construcción dentro de la plataforma.

Más adelante veremos este mecanismo con mayor detalle cuando estudiemos la construcción y despliegue de aplicaciones.

Por ahora basta con recordar una idea:

> BuildConfig es un mecanismo de construcción de imágenes proporcionado por OpenShift.

---

# SCC: una capa adicional de seguridad

Uno de los aspectos donde OpenShift más se diferencia de una instalación básica de Kubernetes es la seguridad.

Para ello incorpora un mecanismo denominado **Security Context Constraints (SCC)**.

Las SCC definen qué puede hacer un contenedor cuando se ejecuta.

Por ejemplo:

- Qué usuario puede utilizar.
- Qué privilegios están permitidos.
- Qué capacidades del sistema puede solicitar.
- Qué configuraciones se consideran aceptables.

Podemos visualizarlo de la siguiente manera:

```text
Pod solicitado
       ↓
 Validación SCC
       ↓
Permitido o rechazado
```

Las SCC constituyen una capa adicional de protección que ayuda a reducir riesgos y a mantener políticas de seguridad homogéneas dentro de la plataforma.

Durante el segundo día del curso veremos este mecanismo con más detalle.

Por ahora es suficiente recordar que OpenShift incorpora controles de seguridad adicionales sobre las cargas de trabajo que se ejecutan en el clúster.

---

# El concepto de operador

Hasta ahora hemos hablado de recursos utilizados para desplegar aplicaciones.

Sin embargo, OpenShift utiliza también un concepto fundamental: los **operadores**.

Un operador es un componente software, basado en capacidades nativas de Kubernetes, encargado de instalar, configurar, mantener y actualizar otro componente software.

Podemos pensar en él como un administrador automatizado.

Tradicionalmente muchas tareas requerían intervención manual:

- Instalar un producto.
- Configurarlo.
- Actualizarlo.
- Supervisarlo.
- Resolver incidencias habituales.

Con un operador gran parte de estas tareas quedan automatizadas.

```text
Administrador humano
         ↓
     Operador
         ↓
 Componente gestionado
```

Los operadores utilizan el mismo principio de reconciliación que hemos visto anteriormente en Kubernetes.

El operador conoce cómo debe ser un componente y trabaja continuamente para mantenerlo en el estado deseado.

---

# El clúster está hecho de operadores

Esta es una de las ideas más importantes de todo el curso.

Cuando observamos OpenShift desde fuera podemos pensar que estamos utilizando una única plataforma.

Sin embargo, internamente OpenShift está formado por numerosos componentes especializados.

Por ejemplo:

- Consola web.
- Red de clúster.
- Acceso externo.
- Registro interno de imágenes.
- Monitorización.
- Gestión de certificados.
- Autenticación.
- Almacenamiento.
- Y muchos otros.

Gran parte de estos componentes están gestionados mediante operadores.

De forma simplificada:

```text
OpenShift
    │
    ├─ Operador
    ├─ Operador
    ├─ Operador
    ├─ Operador
    └─ ...
```

Por este motivo suele decirse que:

> OpenShift es una plataforma construida sobre operadores.

Más adelante veremos que incluso el estado de salud de la plataforma está estrechamente relacionado con el estado de sus operadores.

---

# OperatorHub: ampliar la plataforma

Si los operadores gestionan componentes, surge una pregunta natural:

¿Cómo se incorporan nuevos operadores a la plataforma?

OpenShift proporciona un catálogo denominado **OperatorHub**.

OperatorHub permite localizar e instalar operadores adicionales que amplían las capacidades del clúster.

De forma conceptual:

```text
OperatorHub
      ↓
Seleccionar operador
      ↓
Instalar
      ↓
Nueva funcionalidad disponible
```

Gracias a este mecanismo es posible incorporar nuevos servicios y herramientas sin realizar instalaciones complejas de forma manual.

Más adelante dedicaremos un apartado específico a comprender con detalle cómo funcionan los operadores y cómo se gestionan.

---

# Demostración: instalación del operador Web Terminal

Para ilustrar el funcionamiento de OperatorHub veremos una demostración sencilla realizada por el instructor.

El objetivo de la demostración no es aprender los pasos de instalación ni memorizar opciones de configuración.

Lo importante es comprender el mecanismo general:

```text
OperatorHub
      ↓
Instalación de un operador
      ↓
Despliegue automático
      ↓
Nueva funcionalidad disponible
```

Como ejemplo se instalará el operador **Web Terminal**.

Tras la instalación aparecerá una nueva capacidad integrada en la plataforma que permitirá abrir terminales directamente desde la consola web.

No es necesario memorizar los pasos de instalación. Lo importante es comprender que OpenShift puede ampliarse mediante operadores.

La idea fundamental que debemos recordar es la siguiente:

> Muchas funcionalidades de OpenShift se incorporan y mantienen mediante operadores.

---

# Ideas clave para recordar

- OpenShift utiliza Kubernetes como base y añade funcionalidades adicionales.
- Un Project es la forma habitual de trabajar con namespaces en OpenShift.
- Las Routes permiten publicar aplicaciones fuera del clúster.
- BuildConfig es un mecanismo de construcción de imágenes proporcionado por OpenShift.
- BuildConfig no sustituye al Dockerfile; ambos colaboran en el proceso de construcción.
- Las SCC añaden controles de seguridad sobre las cargas de trabajo.
- Un operador automatiza la instalación, configuración, mantenimiento y actualización de otros componentes.
- Los operadores se apoyan en capacidades nativas de Kubernetes.
- Gran parte de OpenShift está construida mediante operadores.
- OperatorHub permite ampliar la plataforma mediante la instalación de operadores.
- El operador Web Terminal es un ejemplo de extensión de OpenShift mediante OperatorHub.
- Comprender los operadores es fundamental para entender cómo funciona OpenShift internamente.



# 1.5 Arquitectura de un clúster OpenShift 4.x

## Objetivos de aprendizaje

Al finalizar este apartado serás capaz de:

- Identificar los principales componentes de un clúster OpenShift.
- Comprender la diferencia entre control plane, nodos worker y nodos de infraestructura.
- Entender el papel del API Server dentro del clúster.
- Entender el papel de etcd dentro del clúster.
- Comprender cómo OpenShift utiliza operadores para gestionar la plataforma.
- Entender qué es el Cluster Version Operator (CVO).
- Seguir de forma conceptual el recorrido de una petición hasta una aplicación.
- Comprender que OpenShift incorpora mecanismos propios de actualización.
- Conocer, a nivel básico, cómo influye la arquitectura del clúster en el licenciamiento.

---

# Del concepto a la plataforma real

Hasta ahora hemos visto:

- Contenedores.
- Kubernetes.
- OpenShift y sus capacidades adicionales.

La siguiente pregunta es natural:

**¿Cómo está construido realmente un clúster OpenShift?**

Aunque desde el punto de vista del usuario vemos una única plataforma, internamente OpenShift está formado por varios servidores que colaboran entre sí para ofrecer un entorno común de ejecución.

De forma simplificada, un clúster OpenShift está formado por:

- Control Plane.
- Nodos Worker.
- Nodos de Infraestructura (opcionales).

No todos los clústeres disponen necesariamente de nodos de infraestructura dedicados. En entornos pequeños o de laboratorio es habitual que determinados servicios de plataforma se ejecuten sobre los propios workers.

Para trabajar con OpenShift no es necesario conocer todos los detalles internos, pero sí entender el papel de cada uno de estos elementos.

---

# Qué es un nodo

Un nodo es una máquina que forma parte del clúster.

Dependiendo del entorno, puede tratarse de:

- Un servidor físico.
- Una máquina virtual.
- Una instancia en una nube pública.

Desde la perspectiva de OpenShift, todos ellos son simplemente nodos que colaboran para ejecutar y administrar la plataforma.

Todos los nodos de un clúster no tienen necesariamente el mismo papel.

Dependiendo de su función, podemos encontrar:

- Nodos de control (*control plane*).
- Nodos de trabajo (*workers*).
- Nodos de infraestructura (*infra*).

---

# El control plane

El control plane puede considerarse el cerebro del clúster.

Su función es coordinar y gobernar la plataforma.

Entre sus responsabilidades se encuentran:

- Mantener el estado del clúster.
- Procesar las peticiones realizadas por usuarios y herramientas.
- Decidir dónde se ejecutarán los Pods.
- Coordinar los diferentes componentes del sistema.
- Aplicar el estado deseado definido por Kubernetes.

Las aplicaciones de usuario normalmente no se ejecutan en los nodos del control plane.

Su función principal es gestionar el clúster.

---

# El API Server: la puerta de entrada al clúster

Uno de los componentes más importantes del control plane es el **API Server**.

El API Server actúa como puerta de entrada al clúster.

Todas las operaciones realizadas por los usuarios y las herramientas pasan por él.

Por ejemplo:

- Cuando ejecutamos un `oc login`.
- Cuando creamos un Deployment.
- Cuando consultamos un Pod.
- Cuando utilizamos la consola web.
- Cuando una herramienta automatizada interactúa con OpenShift.

Todas estas acciones terminan convirtiéndose en llamadas al API Server.

De forma simplificada:

```text
Usuario
  ↓
oc / Consola Web
  ↓
API Server
  ↓
Componentes del clúster
```

Esto significa que tanto la consola web como el cliente `oc` utilizan la misma API y trabajan sobre los mismos recursos.

Cuando un usuario crea una aplicación, la petición llega primero al control plane a través del API Server.

```text
Usuario
  ↓
API Server
  ↓
Control Plane
  ↓
Worker seleccionado
```

---

# Los nodos worker

Los nodos worker son los encargados de ejecutar las cargas de trabajo de los usuarios.

Aquí encontraremos habitualmente:

- Pods.
- Deployments.
- Aplicaciones corporativas.
- Procesos de construcción.
- Tareas programadas.

Podemos resumirlo de una forma sencilla:

```text
Control Plane = coordina

Workers = ejecutan
```

Cuando desplegamos una aplicación en OpenShift, los contenedores acaban ejecutándose sobre uno o varios nodos worker.

---

# Los nodos de infraestructura

En algunos entornos existen nodos dedicados específicamente a ejecutar componentes de la propia plataforma OpenShift.

Estos nodos se conocen habitualmente como **nodos de infraestructura**.

Algunos ejemplos habituales son:

- Router o Ingress Controller.
- Registro interno de imágenes.
- Monitorización.
- Logging.
- Componentes de observabilidad.
- Servicios compartidos de la propia plataforma.

Es importante entender que estos componentes también se ejecutan como contenedores, igual que las aplicaciones de usuario.

La diferencia es que prestan servicio al conjunto del clúster y no a un proyecto concreto.

De forma simplificada:

```text
Aplicaciones de negocio
  ↓
Workers

Servicios de plataforma
  ↓
Infraestructura
```

No todos los clústeres disponen de nodos de infraestructura dedicados.

Su uso es más habitual en entornos empresariales donde se desea separar las aplicaciones de negocio de los servicios necesarios para operar la plataforma.

---

# Consideración básica sobre licenciamiento

Los detalles completos de licenciamiento quedan fuera del alcance de este curso, pero conviene conocer una idea general.

En OpenShift, las suscripciones están asociadas principalmente a la capacidad de cómputo utilizada para ejecutar cargas de trabajo de usuario.

Por este motivo, cuando se dimensiona un clúster suele prestarse especial atención a los nodos worker y a la capacidad de CPU disponible en ellos.

Los nodos de control forman parte de la infraestructura necesaria para operar el clúster.

De forma similar, los nodos dedicados exclusivamente a funciones de infraestructura pueden tener un tratamiento específico de licenciamiento cuando se utilizan para alojar únicamente componentes de plataforma y no aplicaciones de usuario.

Para este curso basta con recordar una idea sencilla:

```text
Aplicaciones de usuario
  ↓
Workers
  ↓
Principal impacto en
capacidad y licenciamiento
```

---

# etcd: la memoria del clúster

Existe un componente especialmente importante dentro de Kubernetes y OpenShift: **etcd**.

Podemos imaginarlo como la base de datos del clúster.

En él se almacena información crítica como:

- Configuración del clúster.
- Recursos creados.
- Estado de los objetos.
- Definiciones de aplicaciones.
- Información necesaria para la operación de la plataforma.

De forma simplificada:

```text
Usuario crea un Deployment
  ↓
API Server
  ↓
etcd
```

Cuando Kubernetes necesita conocer el estado deseado del sistema, utiliza la información almacenada en etcd.

Por este motivo, etcd es uno de los componentes más importantes y sensibles de todo el clúster.

Más adelante estudiaremos las copias de seguridad de etcd y comprenderemos por qué son un elemento fundamental en cualquier estrategia de recuperación ante desastres.

---

# Una plataforma construida mediante operadores

En el apartado anterior vimos que OpenShift utiliza operadores para instalar, configurar y mantener componentes software.

Ahora podemos completar esa idea.

Buena parte de OpenShift está gestionada mediante operadores.

Por ejemplo:

- Red del clúster.
- Consola web.
- Monitorización.
- Autenticación.
- Certificados.
- Registro interno.
- Ingreso de tráfico.

De forma simplificada:

```text
OpenShift
 ├─ Operador de red
 ├─ Operador de consola
 ├─ Operador de monitorización
 ├─ Operador de autenticación
 └─ ...
```

Por este motivo, el estado de los operadores es uno de los principales indicadores de salud de la plataforma.

Posteriormente aprenderemos a localizar los **Cluster Operators** desde la consola web y a interpretar su estado.

---

# Un clúster gestionado

Una de las características más importantes de OpenShift 4 es que gran parte de la propia plataforma se encuentra autogestionada.

Muchos componentes internos son desplegados, configurados, supervisados y actualizados mediante operadores.

Esto significa que el administrador no tiene que instalar o actualizar manualmente cada componente por separado. En su lugar, OpenShift utiliza operadores para mantener el estado esperado de la plataforma y corregir automáticamente determinadas desviaciones cuando se producen.

De forma simplificada:

- El administrador define lo que necesita.
- OpenShift supervisa el estado del clúster.
- Los operadores realizan las acciones necesarias para mantener ese estado.

Este modelo reduce las tareas operativas y ayuda a mantener una plataforma más consistente.

---

# El Cluster Version Operator (CVO)

Entre todos los operadores existe uno especialmente importante: el **Cluster Version Operator (CVO)**.

Su responsabilidad es coordinar la versión global de OpenShift.

Podemos verlo como el componente encargado de dirigir las actualizaciones de la plataforma.

De forma simplificada:

```text
Nueva versión disponible
  ↓
CVO
  ↓
Actualización coordinada
  ↓
Clúster actualizado
```

El administrador no necesita actualizar manualmente cada componente por separado.

El CVO se encarga de coordinar el proceso para mantener la coherencia de la plataforma.

---

# Recorrido de una petición

Hasta ahora hemos visto que una aplicación suele estar formada por Pods, Services y Routes.

Cuando un usuario accede a una aplicación desde su navegador, la petición atraviesa varios componentes antes de llegar al contenedor que ejecuta la aplicación.

De forma simplificada:

```text
Usuario
  ↓
Route
  ↓
Service
  ↓
Pod
```

Recordemos:

- La Route publica la aplicación al exterior.
- El Service proporciona un punto de acceso estable.
- El Pod ejecuta realmente la aplicación.

Aunque internamente intervienen más componentes, esta visión es suficiente para comprender el flujo general de una petición.

---

# El clúster también se actualiza

Cuando se empieza a trabajar con OpenShift es habitual pensar únicamente en la actualización de las aplicaciones.

Sin embargo, la propia plataforma también evoluciona.

OpenShift publica periódicamente nuevas versiones que incorporan:

- Correcciones de errores.
- Mejoras funcionales.
- Actualizaciones de seguridad.
- Compatibilidad con nuevas capacidades.

Por tanto, un clúster OpenShift no es un sistema estático.

También forma parte de su operación habitual mantener la plataforma actualizada.

---

# Canales de actualización

OpenShift permite configurar canales de actualización que determinan qué versiones aparecerán como candidatas para actualizar el clúster.

Conceptualmente:

```text
Canal de actualización
  ↓
Versiones disponibles
  ↓
Proceso gestionado por OpenShift
```

No estudiaremos los procedimientos de actualización en este curso.

Lo importante es comprender que OpenShift incorpora mecanismos nativos para gestionar su propio ciclo de vida.

---

# Compatibilidad de operadores

Existe una última idea que conviene recordar.

Si OpenShift está compuesto por numerosos operadores, al actualizar la plataforma también debemos tener en cuenta dichos operadores.

Antes de una actualización es habitual verificar:

- El estado del clúster.
- La versión actual.
- La versión objetivo.
- Los operadores instalados.
- La compatibilidad de esos operadores con la nueva versión.

No profundizaremos en este proceso, pero es importante conocer que forma parte de la administración habitual de una plataforma OpenShift.

---

# Ideas clave para recordar

- Un clúster OpenShift está formado por múltiples nodos que trabajan de forma coordinada.
- El control plane gobierna y coordina la plataforma.
- El API Server es la puerta de entrada al clúster.
- Tanto la consola web como el cliente `oc` utilizan la API del clúster.
- Los nodos worker ejecutan las aplicaciones de usuario.
- Los nodos de infraestructura pueden alojar componentes propios de la plataforma.
- etcd almacena la información crítica del clúster.
- Las copias de seguridad de etcd son fundamentales para la recuperación de la plataforma.
- OpenShift está compuesto por numerosos operadores.
- Los Cluster Operators son un indicador importante de la salud del clúster.
- OpenShift 4 incorpora capacidades de autogestión mediante operadores.
- El Cluster Version Operator coordina las actualizaciones de la plataforma.
- Una petición suele recorrer la cadena Route → Service → Pod.
- OpenShift incorpora mecanismos integrados de actualización.
- Los workers son habitualmente el elemento más relevante desde el punto de vista de capacidad y licenciamiento.
- La compatibilidad de los operadores debe considerarse durante el ciclo de vida del clúster.

# 1.6 La consola web de OpenShift

## Objetivos de aprendizaje

Al finalizar este apartado serás capaz de:

- Comprender el papel de la consola web dentro de OpenShift.
- Diferenciar la perspectiva de administración y la perspectiva de desarrollo.
- Identificar qué tipo de información muestra cada una.
- Entender qué tareas suelen realizarse desde cada perspectiva.
- Reconocer cuándo resulta más adecuada una u otra vista.

---

# La puerta de entrada a OpenShift

Una de las características más valoradas de OpenShift es su consola web.

Aunque muchas tareas pueden realizarse desde línea de comandos mediante la herramienta `oc`, la consola proporciona una interfaz gráfica que facilita enormemente la visualización y gestión de los recursos de la plataforma.

Para un usuario que se inicia en OpenShift, la consola permite comprender mejor cómo se organizan las aplicaciones y cómo se relacionan entre sí los distintos componentes.

Sin embargo, al acceder por primera vez puede surgir una duda:

¿Por qué existen dos perspectivas diferentes?

La respuesta es sencilla: no todos los usuarios necesitan ver la misma información.

Un administrador de plataforma tiene responsabilidades distintas a las de un desarrollador de aplicaciones. Por este motivo OpenShift adapta la interfaz para mostrar primero aquello que resulta más relevante para cada perfil.

---

# Dos formas de ver la misma plataforma

Es importante entender que no existen dos OpenShift diferentes.

La plataforma es la misma.

Lo que cambia es la forma en que se presenta la información al usuario.

Las dos perspectivas principales son:

- **Administrator**
- **Developer**

---

# Perspectiva de administración

La perspectiva de administración está orientada a la gestión de la plataforma.

Su objetivo es facilitar el trabajo de los equipos responsables del funcionamiento global de OpenShift.

Desde esta perspectiva es habitual encontrar información relacionada con:

- Nodos del clúster.
- Operadores instalados.
- Redes.
- Almacenamiento.
- Usuarios y permisos.
- Proyectos.
- Cuotas y límites de recursos.
- Estado general de la plataforma.

La pregunta que intenta responder esta vista es:

> ¿Cómo se encuentra la plataforma y cómo está configurada?

Por este motivo suele presentar una visión más cercana a la infraestructura que a las aplicaciones.

---

## ¿Quién utiliza esta perspectiva?

Normalmente:

- Administradores de OpenShift.
- Equipos de plataforma.
- Equipos de operación.
- Personal de soporte avanzado.

No significa que un desarrollador no pueda acceder a ella, pero gran parte de la información mostrada puede resultar innecesaria para las tareas habituales de desarrollo.

---

# Perspectiva de desarrollo

La perspectiva de desarrollo está orientada a las aplicaciones.

Su diseño busca que un desarrollador encuentre rápidamente los recursos relacionados con su proyecto sin necesidad de navegar por elementos de infraestructura que normalmente no necesita gestionar.

Desde esta perspectiva es habitual trabajar con:

- Aplicaciones.
- Pods.
- Deployments.
- Services.
- Routes.
- Builds.
- Imágenes de contenedor.
- Logs.

La pregunta que intenta responder esta vista es:

> ¿Cómo se encuentra mi aplicación?

Por este motivo toda la experiencia está orientada a simplificar el trabajo diario sobre las aplicaciones desplegadas.

---

## La vista Topology

Una de las vistas más características de la perspectiva de desarrollo es **Topology**.

Esta vista representa gráficamente los principales componentes de una aplicación y las relaciones existentes entre ellos.

Para un usuario que comienza a trabajar con OpenShift resulta especialmente útil porque permite obtener una visión general del proyecto sin necesidad de navegar por múltiples menús.

En lugar de revisar los recursos uno por uno, la topología permite entender rápidamente qué componentes forman parte de una aplicación y cómo se conectan entre sí.

---

# La importancia de los permisos

No todos los usuarios ven exactamente lo mismo en la consola.

OpenShift aplica un modelo de control de acceso basado en permisos.

Esto significa que dos usuarios pueden acceder a la misma plataforma y encontrar opciones diferentes.

Por ejemplo:

- Un administrador puede visualizar recursos de todo el clúster.
- Un desarrollador normalmente trabajará únicamente sobre los proyectos a los que tiene acceso.

Por tanto, es completamente normal que la apariencia de la consola varíe de un usuario a otro.

---

# Consola web y línea de comandos

La consola web y la herramienta `oc` no son alternativas excluyentes.

Ambas permiten trabajar sobre los mismos recursos.

Por ejemplo:

- Un pod puede consultarse desde la consola.
- El mismo pod puede consultarse mediante `oc`.
- Los logs pueden visualizarse desde la consola.
- Los mismos logs pueden obtenerse mediante línea de comandos.

La diferencia está principalmente en la forma de interactuar con la plataforma.

La consola facilita la visualización y el aprendizaje inicial, mientras que la línea de comandos aporta rapidez, automatización y repetibilidad.

A lo largo del curso utilizaremos ambos enfoques de manera complementaria.

---

# Ideas clave para recordar

- La consola web es una de las principales formas de interactuar con OpenShift.
- OpenShift presenta la información mediante distintas perspectivas.
- La perspectiva **Administrator** está orientada a la gestión de la plataforma.
- La perspectiva **Developer** está orientada a las aplicaciones.
- Ambas perspectivas muestran recursos de la misma plataforma.
- Los permisos del usuario determinan qué información puede visualizarse.
- La vista **Topology** facilita comprender la estructura de una aplicación.
- La consola web y la herramienta `oc` trabajan sobre los mismos recursos.

---


# 1.7 El cliente `oc`

## Objetivos de aprendizaje

Al finalizar este apartado serás capaz de:

- Comprender qué es la herramienta `oc`.
- Conectarte a un clúster OpenShift mediante `oc login`.
- Identificar dónde se almacena la configuración de acceso.
- Entender qué es un contexto y por qué resulta importante.
- Utilizar `oc project` para cambiar de proyecto de trabajo.
- Diferenciar OpenShift CLI (`oc`) de Kubernetes CLI (`kubectl`).
- Consultar información básica sobre recursos mediante `get`, `describe` y `logs`.
- Utilizar `oc explain` para descubrir recursos y atributos sin depender de documentación externa.

---

## ¿Qué es `oc`?

Hasta ahora hemos visto la consola web como una de las principales formas de interactuar con OpenShift.

La segunda herramienta fundamental es el cliente de línea de comandos **oc**.

Podemos pensar en él como el equivalente a una consola de administración para OpenShift.

Desde `oc` es posible:

- Consultar recursos.
- Desplegar aplicaciones.
- Obtener logs.
- Escalar aplicaciones.
- Gestionar configuraciones.
- Automatizar tareas mediante scripts.

De hecho, prácticamente cualquier acción realizada desde la consola web termina convirtiéndose en llamadas a la API del clúster. `oc` utiliza esa misma API.

Por este motivo, aprender algunos comandos básicos proporciona una enorme autonomía al trabajar con OpenShift.

---

## Conectarse al clúster: `oc login`

Antes de poder trabajar es necesario autenticarse.

El comando básico es:

```bash
oc login https://api.cluster.ejemplo.com:6443
```

Tras ejecutarlo, OpenShift solicitará las credenciales correspondientes.

En algunos entornos también es posible utilizar un token:

```bash
oc login --token=<TOKEN> --server=https://api.cluster.ejemplo.com:6443
```

Una vez autenticados podremos empezar a consultar recursos y ejecutar operaciones sobre aquellos proyectos para los que tengamos permisos.

### ¿Tengo que hacer login cada vez?

Normalmente no.

Tras autenticarse correctamente, el cliente guarda la información necesaria para reutilizar la sesión en futuras ejecuciones.

Por eso, en el trabajo diario, lo habitual es realizar el login una vez y reutilizar la configuración almacenada localmente.

---

## El fichero kubeconfig

Cuando se realiza un `oc login`, la configuración se almacena en un fichero denominado **kubeconfig**.

Este fichero contiene información como:

- Clústeres conocidos.
- Usuarios.
- Tokens o mecanismos de autenticación.
- Contextos.
- Proyecto activo.

En sistemas Linux y macOS suele encontrarse en:

```text
~/.kube/config
```

En Windows:

```text
%USERPROFILE%\.kube\config
```

Es importante entender que este fichero no contiene la plataforma OpenShift ni ninguna copia local de los recursos.

Simplemente almacena la información necesaria para conectar con el clúster.

Podemos imaginarlo como la agenda de conexiones del usuario.

---

## ¿Qué es un contexto?

A medida que una organización crece, es habitual trabajar con varios entornos:

- Desarrollo.
- Integración.
- Preproducción.
- Producción.

Incluso pueden existir varios clústeres OpenShift independientes.

El concepto de **contexto** permite indicar:

- Con qué clúster trabajamos.
- Con qué usuario.
- En qué proyecto nos encontramos.

Podemos consultar el contexto actual:

```bash
oc config current-context
```

Y listar los disponibles:

```bash
oc config get-contexts
```

Una forma sencilla de entenderlo es pensar que el contexto representa la combinación:

```text
Usuario + Clúster + Proyecto
```

Cuando ejecutamos un comando, OpenShift utilizará el contexto activo en ese momento.

Por este motivo, antes de realizar cambios importantes conviene comprobar siempre dónde estamos trabajando.

---

## Trabajar con proyectos: `oc project`

Uno de los primeros comandos que utilizaremos habitualmente es:

```bash
oc project
```

Permite consultar el proyecto activo.

Por ejemplo:

```bash
oc project
```

Salida aproximada:

```text
Using project "curso-openshift".
```

También permite cambiar de proyecto:

```bash
oc project desarrollo
```

### Lo que suele confundirse al principio

Muchos alumnos interpretan `oc project` como si fuese un:

```bash
cd directorio
```

Pero no es correcto.

Cuando ejecutamos:

```bash
cd /tmp
```

cambiamos de carpeta en nuestro equipo local.

Cuando ejecutamos:

```bash
oc project desarrollo
```

no estamos cambiando de carpeta.

Estamos indicando a OpenShift que los comandos posteriores actuarán sobre otro proyecto.

Es más parecido a cambiar de espacio de trabajo dentro de la plataforma que a cambiar de directorio en Linux.

---

## `oc` y `kubectl`

Una pregunta habitual es:

> Si OpenShift está basado en Kubernetes, ¿por qué existe `oc`?

La respuesta es que OpenShift añade capacidades propias sobre Kubernetes.

Por eso Red Hat proporciona el cliente `oc`.

De forma simplificada:

```text
kubectl = Kubernetes
oc      = Kubernetes + OpenShift
```

Por ejemplo:

- `kubectl` entiende recursos Kubernetes estándar.
- `oc` entiende recursos Kubernetes estándar.
- `oc` entiende además recursos específicos de OpenShift.

Entre ellos:

- Projects.
- Routes.
- ImageStreams.
- BuildConfigs.
- Recursos relacionados con operadores y funcionalidades propias de OpenShift.

En la práctica, muchos comandos básicos son equivalentes:

```bash
kubectl get pods
```

```bash
oc get pods
```

Sin embargo, cuando trabajamos en OpenShift, lo habitual es utilizar siempre `oc`.

Así tenemos acceso tanto a Kubernetes como a las capacidades adicionales de la plataforma.

---

## Consultar recursos con `oc get`

El comando más utilizado de toda la CLI probablemente sea:

```bash
oc get
```

Permite listar recursos.

Por ejemplo:

```bash
oc get pods
```

```bash
oc get deployments
```

```bash
oc get services
```

```bash
oc get routes
```

Salida típica:

```text
NAME                    READY   STATUS    RESTARTS   AGE
mi-aplicacion-1-abcde   1/1     Running   0          5m
```

La idea es sencilla:

**get muestra qué existe y en qué estado general se encuentra.**

Es el primer comando que suele ejecutarse para orientarse dentro de un proyecto.

---

## Obtener más detalle con `oc describe`

Cuando `get` no es suficiente, utilizamos:

```bash
oc describe
```

Ejemplo:

```bash
oc describe pod mi-aplicacion-1-abcde
```

Mientras que `get` ofrece una vista resumida, `describe` proporciona mucha más información:

- Etiquetas.
- Imágenes utilizadas.
- Estado de los contenedores.
- Eventos recientes.
- Configuración asociada.

Una forma práctica de recordarlo es:

```text
get      → resumen
describe → detalle
```

En los apartados dedicados al diagnóstico veremos que `describe` es una de las herramientas más utilizadas para investigar problemas.

---

## Consultar logs con `oc logs`

Si una aplicación no se comporta como esperamos, normalmente el siguiente paso consiste en revisar sus logs.

Ejemplo:

```bash
oc logs mi-aplicacion-1-abcde
```

El comando devuelve la salida generada por la aplicación.

Muchos problemas iniciales pueden identificarse únicamente leyendo los logs:

- Error de configuración.
- Puerto incorrecto.
- Dependencia no disponible.
- Fallos de conexión.
- Excepciones de la aplicación.

En OpenShift existe una regla práctica que veremos repetidamente durante el curso:

> Si algo no funciona, los logs son uno de los primeros lugares donde mirar.

---

## La herramienta más infravalorada: `oc explain`

Cuando un alumno empieza a trabajar con OpenShift suele surgir una necesidad constante:

> ¿Cómo se llama este atributo?
>
> ¿Qué significa este campo?
>
> ¿Cómo es la estructura de este recurso?

Aquí entra en juego uno de los comandos más útiles de toda la plataforma:

```bash
oc explain
```

Por ejemplo:

```bash
oc explain deployment
```

También podemos profundizar:

```bash
oc explain deployment.spec
```

```bash
oc explain deployment.spec.template
```

La idea es que OpenShift puede describir sus propios objetos desde la línea de comandos.

No es necesario memorizar todos los campos ni acudir constantemente a Internet.

### Una analogía útil

Si `oc get` responde:

> ¿Qué existe?

Y `oc describe` responde:

> ¿Cómo está configurado?

Entonces `oc explain` responde:

> ¿Qué significa cada cosa y cómo debería escribirse?

Por este motivo, muchos administradores y desarrolladores experimentados lo consideran una herramienta imprescindible.

Además, nos ayuda a ganar autonomía y a depender menos de ejemplos copiados de terceros.

---

## Consola web y CLI: dos vistas del mismo mundo

A estas alturas ya hemos visto dos formas de trabajar con OpenShift:

- Consola web.
- Cliente `oc`.

No son herramientas competidoras.

Son complementarias.

La consola facilita la exploración visual de la plataforma.

La CLI aporta:

- Rapidez.
- Repetibilidad.
- Automatización.
- Mayor capacidad de diagnóstico.

A lo largo del curso alternaremos continuamente entre ambos enfoques para entender que, en realidad, estamos trabajando sobre los mismos recursos desde perspectivas diferentes.

---

## Ideas clave para recordar

- `oc` es el cliente de línea de comandos de OpenShift.
- `oc login` permite autenticarse contra un clúster.
- La configuración de conexión se almacena en el fichero `kubeconfig`.
- Un contexto define con qué usuario, clúster y proyecto estamos trabajando.
- `oc project` cambia el proyecto activo, pero no equivale a un `cd`.
- `oc` incluye todas las capacidades habituales de Kubernetes y además las extensiones propias de OpenShift.
- `oc get` muestra un resumen de los recursos.
- `oc describe` proporciona información detallada.
- `oc logs` permite consultar la salida de una aplicación.
- `oc explain` ayuda a comprender la estructura y significado de los recursos.
- Aprender a utilizar `oc explain` es una de las mejores formas de ganar autonomía en OpenShift.



# 1.8 Práctica: de la imagen al clúster y comprobación de la reconciliación de Kubernetes

## Objetivos de aprendizaje

Al finalizar este apartado serás capaz de:

- Comprender el recorrido completo desde una aplicación hasta su ejecución en OpenShift.
- Relacionar los conceptos de imagen, contenedor, Pod y Deployment.
- Entender cómo una imagen construida localmente puede desplegarse en un clúster.
- Observar el funcionamiento práctico del estado deseado de Kubernetes.
- Comprobar cómo actúa el bucle de reconciliación cuando desaparece un Pod.
- Verificar que Kubernetes mantiene automáticamente el número de réplicas solicitado.

---

## Del Dockerfile al clúster

A lo largo de esta primera sesión hemos estudiado varios conceptos de forma separada:

- Imagen.
- Contenedor.
- Pod.
- Deployment.
- Estado deseado.
- Bucle de reconciliación.

Ahora vamos a unir todas las piezas en una demostración completa.

El objetivo no es aprender a desarrollar aplicaciones, sino visualizar cómo una aplicación sencilla recorre el camino completo desde una imagen de contenedor hasta su ejecución dentro de OpenShift.

Partiremos de una página HTML muy simple.

### Aplicación de ejemplo

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Curso OpenShift</title>
</head>
<body>

<h1>Curso OpenShift</h1>

<h2>Demostración de Kubernetes</h2>

<p>Mi primera imagen construida con Podman.</p>

</body>
</html>
```

Esta página no tiene ninguna lógica especial.

Su único objetivo es servir como contenido visible para comprobar que el proceso funciona correctamente.

---

## Construcción de la imagen

Para empaquetar la aplicación utilizaremos el siguiente Dockerfile:

```dockerfile
FROM nginx:latest

COPY demo-formacion.html /usr/share/nginx/html/index.html

EXPOSE 80
```

Recordemos qué hace cada línea:

- `FROM` indica la imagen base.
- `COPY` incorpora nuestra página HTML a la imagen.
- `EXPOSE` documenta el puerto utilizado por la aplicación.

De forma simplificada:

```text
Imagen base nginx
        +
Página HTML
        +
Dockerfile
        ↓
Imagen de contenedor
```

---

## Demostración: construcción y ejecución local con Podman

El instructor mostrará cómo construir y ejecutar la imagen localmente.

### Construcción de la imagen

```bash
podman build -t demo-formacion:v1 .
```

Comprobación de la imagen generada:

```bash
podman images
```

### Ejecución local

```bash
podman run -d --name demo-formacion -p 8080:80 demo-formacion:v1
```

```bash
podman ps
```

Acceso desde navegador:

```text
http://localhost:8080
```

```text
Dockerfile
     ↓
Imagen
demo-formacion:v1
     ↓
Contenedor
demo-formacion
```

---

## Publicación de la imagen en un registro

La imagen ha sido publicada previamente en Docker Hub con la siguiente referencia:

```text
docker.io/ieftraining/demo-formacion:v1
```

La imagen utilizada en OpenShift es exactamente la misma que hemos probado localmente.

```text
Construir una vez
        ↓
Publicar
        ↓
Desplegar en distintos entornos
```

---

## Despliegue de la imagen en OpenShift

Ejemplo con `oc`:

```bash
oc new-app docker.io/ieftraining/demo-formacion:v1
```

Comprobación de recursos:

```bash
oc get all
```

```text
Deployment
     ↓
ReplicaSet
     ↓
Pod
```

Además se crea un Service para proporcionar acceso estable a la aplicación.

---

## Comprobación del estado de la aplicación

```bash
oc get pods
```

Ejemplo:

```text
NAME                               READY   STATUS
demo-formacion-7f6b7b8c6d-abcde    1/1     Running
```

```bash
oc get deployments
```

También puede visualizarse desde la vista Topology de OpenShift.

---

# El experimento importante: comprobar la reconciliación

> Kubernetes trabaja continuamente para que el estado real coincida con el estado deseado.

### Paso 1. Verificar las réplicas actuales

```bash
oc get deployment demo-formacion
```

```text
NAME             READY   UP-TO-DATE   AVAILABLE
demo-formacion   1/1     1            1
```

Estado deseado:

```text
1 réplica
```

---

### Paso 2. Escalar la aplicación

```bash
oc scale deployment/demo-formacion --replicas=3
```

```bash
oc get pods
```

```text
demo-formacion-xxxxx
demo-formacion-yyyyy
demo-formacion-zzzzz
```

Ahora el estado deseado es de 3 Pods.

---

### Paso 3. Eliminar un Pod manualmente

```bash
oc delete pod <nombre-del-pod>
```

Ejemplo:

```bash
oc delete pod demo-formacion-xxxxx
```

El Deployment sigue definiendo tres réplicas como estado deseado.

---

### Paso 4. Observar qué ocurre

```bash
oc get pods
```

```text
Pod eliminado
        ↓
Quedan 2 Pods
        ↓
Kubernetes detecta la diferencia
        ↓
Se crea un nuevo Pod
        ↓
Vuelven a existir 3 Pods
```

El nuevo Pod tendrá un nombre diferente al eliminado.

Kubernetes no recupera el Pod antiguo; recupera el estado deseado.

---

## ¿Qué acabamos de demostrar?

```text
Estado deseado: 3 Pods
        ↓
Estado real: 2 Pods
        ↓
Reconciliación
        ↓
Estado real: 3 Pods
```

Este mecanismo constituye la base de la recuperación automática ante muchos tipos de fallos.

---

## Relación con los conceptos estudiados

```text
Página HTML
      ↓
Dockerfile
      ↓
Imagen
      ↓
Contenedor
      ↓
Pod
      ↓
Deployment
      ↓
Kubernetes mantiene el estado deseado
```

Comprender esta cadena es fundamental para entender el funcionamiento de OpenShift.

---

## Ideas clave para recordar

- Una imagen puede construirse localmente con Podman y reutilizarse posteriormente en OpenShift.
- La imagen utilizada en desarrollo y en OpenShift puede ser exactamente la misma.
- Un Deployment define cómo debe ejecutarse una aplicación.
- Kubernetes mantiene el número de réplicas solicitado por el Deployment.
- Los Pods son recursos efímeros y pueden desaparecer en cualquier momento.
- Eliminar un Pod no implica necesariamente que la aplicación deje de funcionar.
- Kubernetes detecta desviaciones entre estado real y estado deseado.
- El bucle de reconciliación es uno de los mecanismos fundamentales de Kubernetes.
- OpenShift hereda este comportamiento porque utiliza Kubernetes como motor de orquestación.



# 1.9 Cierre y qué veremos mañana

## Resumen de la sesión

A lo largo de esta primera jornada hemos construido los conceptos fundamentales necesarios para comprender OpenShift y Kubernetes.

Hemos comenzado analizando la evolución desde los despliegues tradicionales hacia los modelos basados en contenedores, entendiendo las limitaciones de las infraestructuras clásicas y los beneficios que aporta la contenerización.

Posteriormente hemos estudiado los conceptos básicos que forman la base de cualquier plataforma cloud-native:

- Imágenes.
- Imágenes base.
- Contenedores.
- Dockerfile.
- Registros de imágenes.
- Construcción y ejecución de contenedores.

También hemos conocido la arquitectura general de OpenShift y los componentes principales que forman un clúster:

- Nodos de control (Control Plane).
- Nodos de trabajo (Workers).
- Nodos de infraestructura (Infra).
- API Server.
- Operadores.
- Servicios internos de la plataforma.

Finalmente hemos visto cómo OpenShift aprovecha la reconciliación continua de Kubernetes para mantener el estado deseado de las aplicaciones y de la propia plataforma.

A estas alturas ya deberíamos ser capaces de responder preguntas como:

- ¿Qué es un contenedor?
- ¿Qué diferencia existe entre una imagen y un contenedor?
- ¿Cómo se construye una imagen?
- ¿Qué papel desempeña un Dockerfile?
- ¿Por qué Kubernetes necesita reconciliación continua?
- ¿Qué función tienen los distintos tipos de nodos dentro del clúster?

---

## Ideas clave para recordar

Antes de continuar con el resto del curso conviene consolidar algunos conceptos esenciales:

### Una imagen es una plantilla

La imagen contiene todo lo necesario para ejecutar una aplicación:

- Código.
- Librerías.
- Dependencias.
- Configuración básica.

La imagen por sí sola no ejecuta nada.

### Un contenedor es una instancia en ejecución

Cuando arrancamos una imagen obtenemos un contenedor.

Podemos tener:

- Una imagen.
- Diez contenedores distintos creados a partir de esa misma imagen.

### Kubernetes trabaja declarativamente

No describimos paso a paso cómo ejecutar una aplicación.

Indicamos:

> Quiero que existan tres instancias de esta aplicación.

Kubernetes se encarga de conseguirlo y mantenerlo.

### OpenShift es mucho más que Kubernetes

OpenShift incorpora capacidades adicionales que simplifican el ciclo completo de desarrollo y operación:

- Gestión de usuarios.
- Seguridad integrada.
- Registro de imágenes.
- Consola web.
- Pipelines CI/CD.
- Observabilidad.
- Operación automatizada mediante operadores.

---

## Qué veremos mañana

En la siguiente sesión comenzaremos a trabajar con los recursos que se utilizan diariamente para desplegar aplicaciones en OpenShift.

Nos centraremos especialmente en comprender:

### Proyectos y espacios de trabajo

Aprenderemos cómo OpenShift organiza los recursos mediante proyectos (namespaces) y cómo aislar aplicaciones y equipos dentro de un mismo clúster.

### Aplicaciones y carga de trabajo

Veremos los objetos más habituales utilizados para ejecutar aplicaciones:

- Pods.
- ReplicaSets.
- Deployments.

Entenderemos la relación existente entre ellos y cómo colaboran para mantener las aplicaciones disponibles.

### Exposición de servicios

Una aplicación no aporta valor si no puede ser consumida.

Por ello estudiaremos:

- Services.
- Routes.
- Acceso interno y externo.

### Escalado y alta disponibilidad

Analizaremos cómo Kubernetes distribuye las cargas de trabajo entre nodos y cómo mantiene las aplicaciones disponibles ante incidencias.

### Primeros despliegues en OpenShift

Comenzaremos a desplegar aplicaciones sencillas utilizando la consola web y la interfaz de línea de comandos.

---

## Objetivo de la próxima sesión

El objetivo será dar el salto desde los conceptos básicos vistos hoy hacia el despliegue real de aplicaciones.

Si en esta jornada hemos aprendido:

**Imagen → Contenedor → Clúster**

En la siguiente veremos:

**Aplicación → Deployment → Service → Route**

Es decir, pasaremos de comprender los componentes fundamentales a utilizarlos para publicar aplicaciones dentro de OpenShift de forma controlada y reproducible.

---

## Conclusión

La plataforma OpenShift puede parecer compleja cuando se observa por primera vez, pero en realidad se apoya en un conjunto reducido de conceptos fundamentales.

Comprender correctamente la relación entre imágenes, contenedores, Kubernetes y OpenShift constituye la base sobre la que construiremos todo el resto del curso.

A partir de la próxima sesión comenzaremos a trabajar directamente con los recursos que utilizan los equipos de desarrollo y operaciones en su día a día, acercándonos progresivamente a escenarios reales de despliegue de aplicaciones empresariales.
# 🌐 Guía de Microservicios con Spring Boot

Este repositorio contiene apuntes detallados y estructurados sobre la construcción de microservicios con Spring Boot, basados en el video ["Spring Boot 3: Guía de Microservicios"](https://www.youtube.com/watch?v=t0D4OPcugyI&t=7187s) de **Un programador nace** en YouTube.

Estos apuntes sigue paso a paso el contenido del video, con anotaciones y ejemplos adicionales para facilitar la
comprensión y reutilización del código en futuros proyectos asi como soluciones a diferentes problemas encontrados.

> **Nota**: Esta guía no es un reemplazo del video original y se recomienda ver el video completo para obtener
> una explicación detallada directamente de la fuente.

## 1.- 🌐 Introducción a los Microservicios con Spring Boot

En esta guía, exploraremos cómo construir una arquitectura de microservicios desde cero,
comprendiendo los fundamentos y desarrollando un ecosistema con Spring Boot. Los microservicios son una poderosa
alternativa a las aplicaciones monolíticas, y aprenderemos sus características, beneficios y cómo implementarlos
con Spring Boot.

### 1️⃣ 🏢 ¿Qué es una Aplicación Monolítica?

Para entender la arquitectura de microservicios, primero veamos qué es una **aplicación monolítica**:

- **Definición**: Una aplicación monolítica es una gran aplicación que contiene toda la funcionalidad en un solo
  proyecto. Esto significa que todo, desde la lógica de negocio hasta la lógica de datos y la interfaz de usuario, se
  encuentra en el mismo lugar.
- **Usos**: Este tipo de arquitectura es la más utilizada, especialmente para aplicaciones pequeñas o para
  desarrolladores principiantes, ya que permite trabajar con un solo proyecto y es fácil de manejar en un inicio.

#### 💼 Ejemplo Práctico

Imagina una aplicación de e-commerce. En un sistema monolítico, tendrías una sola aplicación que maneja todo: gestión de usuarios, inventario, compras, pagos, etc. Todo está interconectado en una sola base de código.

#### ⚠️ Desventajas de una Arquitectura Monolítica

Aunque la arquitectura monolítica puede ser conveniente al inicio, a medida que una aplicación crece y se vuelve más
compleja, comienzan a surgir problemas, especialmente en estos aspectos:

1. **Mantenimiento**: Cuando el negocio y la funcionalidad crecen, mantener una aplicación monolítica se vuelve
   complicado y requiere más esfuerzo.
2. **Escalabilidad**: Si necesitamos escalar solo una parte de la aplicación, como el sistema de pagos, no podemos
   hacerlo sin escalar toda la aplicación.
3. **Despliegues lentos**: Cada vez que actualizamos una parte de la aplicación, debemos desplegar toda la aplicación
   nuevamente, lo cual consume tiempo y puede afectar el rendimiento.

### 2️⃣ 🧩 ¿Qué son los Microservicios?

Aquí es donde los **microservicios** nos ofrecen una solución. Esta arquitectura distribuye la funcionalidad en varios servicios más pequeños, en lugar de tener todo en una sola aplicación. Cada uno de estos servicios (o "microservicios") se encarga de una parte específica de la aplicación y se comunica con los demás a través de redes (generalmente APIs).

#### 💡 Ventajas de los Microservicios

La arquitectura de microservicios ofrece varias ventajas, especialmente en entornos de desarrollo de software modernos:

1. **Mantenimiento Simplicado**: Con microservicios, cada equipo de desarrollo puede enfocarse en un servicio
   específico, facilitando el mantenimiento.
2. **Escalabilidad Independiente**: Podemos escalar solo el microservicio necesario sin afectar al resto de la
   aplicación.
3. **Despliegue más ágil**: Al actualizar solo los servicios necesarios, los despliegues son más rápidos y menos
   propensos a errores.
4. **Descentralización**: Cada microservicio puede estar construido en diferentes tecnologías o lenguajes según sus
   necesidades específicas, permitiendo mayor flexibilidad.

### 3️⃣ 🔧 Microservicios con Spring Boot

**Spring Boot** es uno de los frameworks más populares para crear microservicios en Java. Este framework ofrece varias herramientas y configuraciones para simplificar el desarrollo de microservicios, permitiéndonos concentrarnos en la lógica del negocio sin preocuparnos por configuraciones complejas.

---

## 2.-⚙️ Configuración del Proyecto Base con Maven en IntelliJ IDEA

En esta primera sección práctica, crearemos el proyecto Maven base para nuestra arquitectura de microservicios.
Configuraremos el archivo `pom.xml` con las propiedades, dependencias y plugins esenciales que nos permitirán trabajar de manera eficiente con Spring Boot y aprovechar librerías útiles como **Lombok**. Este proyecto será la base sobre la cual construiremos cada uno de los servicios de nuestra aplicación.

### 1️⃣ Crear el Proyecto Maven en IntelliJ IDEA

Para empezar, seguiremos estos pasos en **IntelliJ IDEA** para crear el proyecto inicial de Maven, lo llamaremos `Microsericios -Academia`:

1. **Abrimos IntelliJ IDEA** y seleccionamos **New Project** en la pantalla principal.
2. Seleccionamos **Maven** como el tipo de proyecto.
3. Completamos los siguientes campos para configurar el proyecto:
   - **GroupId**: `com.tuNombre`
   - **ArtifactId**: `Microservicios-Academia`
   - **Version**: Utilizaremos la predeterminada `1.0-SNAPSHOT`.
4. En el campo **Project name**, escribimos `Microservicios-Academia`.
5. Finalizamos la creación del proyecto.

IntelliJ IDEA generará la estructura básica del proyecto Maven y creará un archivo `pom.xml`.

Una vez hecho esto, veremos la estructura del proyecto en IntelliJ, que incluye un archivo `pom.xml` y las carpetas de código fuente.

### 2️⃣ Limpieza del proyecto y configuración del Archivo `pom.xml` del Proyecto Padre

Para crear una arquitectura de microservicios, configuraremos nuestro proyecto base, `Microservicio-Academia`, como un **proyecto padre en Maven**. Este proyecto actuará como un contenedor que centralizará configuraciones, dependencias y plugins comunes que heredarán los microservicios (módulos) que configuraremos dentro de él. Esto simplifica la gestión y la coherencia en toda la aplicación.
Como este proyecto será solo un contenedor, no necesitamos la carpeta `src` (usualmente usada para el código fuente).
Por lo tanto eliminaremos la carpeta `src` y nos quedaremos únicamente con el archivo `pom.xml`.

Vamos a configurar el archivo `pom.xml` del proyecto `Microservicio-Academia` para que actúe como un proyecto padre de los módulos:

```xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- Configuración del proyecto -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.1.4</version>
    </parent>

    <groupId>com.tuNombre</groupId>
    <artifactId>Microservicios-Academia</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>Microservicios-Academia</name>

    <!-- Configuración de propiedades -->
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

    <!-- Dependencias compartidas para los módulos -->
    <dependencies>
        <!-- Lombok para simplificar el código en todos los microservicios -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.34</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <!-- Configuración de plugins -->
    <build>
        <pluginManagement>
            <plugins>
                <!-- Plugin de Spring Boot para gestionar la construcción de los módulos -->
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                </plugin>
            </plugins>
        </pluginManagement>
    </build>
</project>
```

#### Estructura Final del Archivo `pom.xml`

- **Parent**: La sección `<parent>` especifica que este proyecto hereda de `spring-boot-starter-parent`, un arquetipo
  proporcionado por Spring Boot. Esto nos permite aprovechar configuraciones y dependencias de Spring Boot sin tener que definirlas explícitamente en nuestro proyecto.

- **GroupId, ArtifactId, y Packaging**:

  - **GroupId**: `com.tuNombre`, el identificador del grupo del proyecto, normalmente se ponemos nuestro nombre o el de nuestra organización.
  - **ArtifactId**: `Microservicios-Academia`, el identificador único del proyecto.
  - **Packaging**: `pom` define que este proyecto es un contenedor y no se ejecutará directamente. Así, podemos
    agregar subproyectos (módulos) que actuarán como nuestros microservicios.

- **Properties**: Configuramos Java 21 (el requisito minimo para Spring Boot 3 es versión 17 en adelante) y la codificación UTF-8, asegurando la compatibilidad y estandarización en nuestros módulos.

- **Dependencias**:

  - **Lombok**: Incluimos Lombok en el proyecto padre para que todos los microservicios puedan usarlo sin necesidad de agregarlo en cada uno.

- **Build y Plugin Management**:
  - **spring-boot-maven-plugin**: Este plugin es clave para construir y empaquetar nuestros microservicios en aplicaciones Spring Boot. Será necesario cuando configuremos los módulos individuales.

### 3️⃣ 💡 Usando Spring Initializr para Configurar Proyectos en Spring Boot

Si visitas [Spring Initializr](https://start.spring.io/), puedes observar que al crear un proyecto con Spring Boot, se
incluye automáticamente una etiqueta `<parent>`. Esto convierte al proyecto en un **hijo de Spring Boot**,
permitiéndonos aprovechar su configuración y dependencias predeterminadas. Hemos agregado esta sección `<parent>` en
nuestro archivo `pom.xml` para garantizar que nuestro proyecto global (`Microservicio-Academia`) pueda utilizar todas
las funcionalidades y configuraciones de Spring Boot.

### 4️⃣ Herencia en Maven

Con este archivo `pom.xml`, hemos configurado `Microservicios-Academia` como un **proyecto padre**. Cada microservicio
que creemos dentro de este proyecto heredará las dependencias, plugins y propiedades definidas en este `pom.xml`. Esto
nos permitirá mantener una arquitectura coherente y ahorrar tiempo de configuración en cada módulo.

> **Nota**: En Maven, los proyectos pueden seguir un esquema de herencia. Aquí, `Microservicios-Academia` actúa como el
> padre de los microservicios que crearemos, y es, a su vez, un hijo del `spring-boot-starter-parent` de Spring Boot.

### 5️⃣ ✅ Revisión Final

Una vez configurado el `pom.xml`, IntelliJ IDEA debería actualizar el proyecto automáticamente, descargando las
dependencias necesarias. Si todo está en orden, el proyecto aparecerá en la sección **Maven** de IntelliJ, listo para
añadir los módulos de microservicios.

## 4.- 🧩 Explicación General de la Arquitectura de Microservicios

Antes de comenzar a crear nuestros microservicios, es importante entender el **esquema de arquitectura** que
construiremos. A continuación, revisaremos los componentes clave y cómo se relacionan entre sí para formar
un ecosistema de microservicios robusto y escalable. Este esquema general servirá como base de referencia para todos los
desarrollos posteriores.

### 1️⃣ 📐 Arquitectura General de los Microservicios

La arquitectura que vamos a construir incluirá los siguientes cinco microservicios, cada uno de los cuales cumple un rol
específico en el sistema:

1. **API GATEWAY**
2. **COURSES**
3. **STUDENTS**
4. **EUREKA**
5. **CONFIG SERVER**

Cada uno de estos microservicios es una **aplicación Spring Boot** que se comunicará con otros servicios y gestionará su
propia lógica y configuración. Vamos a repasar cada componente y su función dentro del ecosistema.

### 2️⃣ 🛣️ API Gateway: El Punto de Entrada

La **API Gateway** actúa como la **puerta de entrada** a nuestra arquitectura de microservicios. Su principal responsabilidad es recibir las solicitudes de los usuarios y redirigirlas al microservicio adecuado.

- Cuando un cliente realiza una solicitud, el API Gateway determina el microservicio que
  debe procesarla y la envía allí. Por ejemplo, si el cliente necesita obtener un listado de cursos, el API Gateway
  redirige la solicitud al **Microservicio de Cursos**. De igual manera, si la solicitud es para obtener una lista de
  estudiantes, el Gateway la enviará al **Microservicio de Estudiantes**.
- Permite centralizar el acceso a los servicios, de manera que el cliente no interactúa
  directamente con los microservicios internos. Esto mejora la seguridad y el control sobre el flujo de solicitudes.

> **⚠️ Nota**: Las peticiones del cliente nunca deben dirigirse directamente a los microservicios internos; siempre deben pasar por el API Gateway.

### 3️⃣ 🏫 Microservicio de Cursos y Microservicio de Estudiantes

Estos dos microservicios representan las funcionalidades principales de nuestra aplicación:

- **Microservicio de Cursos**: Gestiona toda la información relacionada con los cursos, como el listado de cursos, la
  creación de nuevos cursos, y otros detalles específicos de cada curso.
- **Microservicio de Estudiantes**: Gestiona la información de los estudiantes, como su listado, datos personales,
  registros de matrícula, entre otros.

#### Comunicación entre Microservicios

En nuestra arquitectura, el **Microservicio de Cursos** y el **Microservicio de Estudiantes** pueden **comunicarse entre
sí** cuando necesitan información que el otro gestiona. Esta comunicación se realiza a través de **peticiones HTTP REST**.

Por ejemplo:

- Si el Microservicio de Cursos necesita información de estudiantes, puede hacer una petición al Microservicio de
  Estudiantes y obtener los datos necesarios.
- De igual forma, el Microservicio de Estudiantes puede solicitar información sobre los cursos al Microservicio de
  Cursos.

Cada microservicio gestionará su propia **base de datos** de manera independiente:

- **Cursos** utilizará una base de datos **PostgreSQL**.
- **Estudiantes** utilizará una base de datos **MySQL**.

Esto permite una separación lógica y física de los datos, lo que es muy importante en una arquitectura de microservicios.

### 4️⃣ 📜 Eureka Server: Registro y Descubrimiento de Servicios

El **Eureka Server** es un servicio de **registro y descubrimiento**. Su función es facilitar la comunicación entre
microservicios sin necesidad de gestionar manualmente direcciones IP y puertos.

- **Función de Eureka**: Cada microservicio (incluido el API Gateway) se registra en el Eureka Server con un nombre
  único. Cuando un microservicio necesita comunicarse con otro, no necesita conocer la IP o el puerto exacto, sino solo
  el nombre del servicio. Eureka se encarga de resolver esta información.
- **Ventajas de Eureka**: Simplifica la comunicación entre microservicios, evita problemas de configuración y ofrece
  alta flexibilidad para despliegues en entornos de red dinámica (como en la nube).

En conclusión, **Eureka Server** permite que los microservicios se comuniquen de manera dinámica y facilita el escalado
de la arquitectura, ya que cada servicio se identifica por su nombre en lugar de una IP específica.

### 5️⃣ ⚙️ Config Server: Gestión Centralizada de Configuración

El **Config Server** centraliza la configuración de todos los microservicios, almacenando los archivos de configuración
que cada microservicio necesita para funcionar. Esto nos ayuda a mantener todas las configuraciones en un solo lugar y a
simplificar el proceso de actualización y gestión de la configuración.

- Cada microservicio tiene un archivo `application.yml` con su configuración específica. En lugar de almacenar estos archivos en cada servicio, el Config Server guarda todas las configuraciones y las entrega a los microservicios cuando estos se inician.
- **Ventajas**:
  - Facilita la gestión de configuraciones en arquitecturas complejas con múltiples microservicios.
  - Permite actualizar configuraciones sin tener que desplegar nuevamente cada microservicio.

Por ejemplo, cuando el API Gateway necesita su configuración, realiza una solicitud al Config Server para obtenerla.
Esto es particularmente útil en entornos de producción, donde se necesita flexibilidad para realizar cambios de
configuración sin afectar la estabilidad de la aplicación.

### 6️⃣ 📊 Resumen de la Arquitectura de Microservicios que construiremos

- **API Gateway**: Puerta de entrada para todas las solicitudes externas.
- **Microservicio de Cursos**: Gestión de cursos y datos asociados (con base de datos PostgreSQL).
- **Microservicio de Estudiantes**: Gestión de estudiantes y datos asociados (con base de datos MySQL).
- **Eureka Server**: Registro centralizado para facilitar la comunicación entre microservicios.
- **Config Server**: Gestión centralizada de la configuración de todos los microservicios.

Esta estructura permitirá una **comunicación eficiente, escalabilidad independiente y una configuración gestionada de
manera centralizada**. Cada componente tiene su rol claramente definido, contribuyendo a un sistema modular y flexible.

---

## 5.- 🚪 Creación del Primer Microservicio: API Gateway

Ahora que hemos definido la arquitectura de nuestro ecosistema de microservicios, es momento de comenzar con la
implementación. En esta sección, crearemos el primer microservicio, el **API Gateway**, que será el **punto de entrada**
a nuestra arquitectura de microservicios. Este servicio redirigirá las solicitudes a los microservicios correspondientes
según sea necesario.

### 1️⃣ Crear el Microservicio API Gateway

Para iniciar, vamos a crear el proyecto del microservicio Gateway en [Spring Initializr](https://start.spring.io/),
siguiendo estos pasos:

1. **Abrir Spring Initializr** en el navegador.
2. Configurar los siguientes valores:

   - **GroupId**: `com.microservice.gateway`
   - **ArtifactId**: `microservice-gateway`
   - **Nombre del proyecto**: `microservice-gateway`
   - **Versión de Spring Boot**: `3.1.4`
   - **Java Version**: `21`

3. **Dependencias**:

   - **Spring Cloud Gateway**: Para manejar las solicitudes HTTP y redirigirlas al microservicio correspondiente.
   - **Eureka Discovery Client**: Permite registrar el API Gateway en el servidor Eureka para que otros servicios lo
     encuentren.
   - **Spring Cloud Config Client**: Para obtener la configuración centralizada del Config Server.
   - **Actuator**: Para monitoreo y métricas del microservicio.

4. **Generar el Proyecto**: Descargamos el archivo ZIP , extraemos el contenido y copiamos la
   carpeta `microservice-gateway` dentro del proyecto padre `Microservicio-Academia`.

5. **Agregar el Microservicio como Módulo** en el proyecto padre.

### 2️⃣ Configurar el Proyecto Gateway como Módulo en el Proyecto Padre

Para que el microservicio `microservice-gateway` sea parte del proyecto `Microservicio-Academia`, debemos agregarlo como
un **módulo** en el archivo `pom.xml` del proyecto padre.

Abrimos el archivo `pom.xml` de `Microservicio-Academia` y agregamos la siguiente sección de módulos:

```xml
<modules>
    <module>microservice-gateway</module>
</modules>
```

Esto le indica a Maven que `microservice-gateway` es un subproyecto (módulo) del proyecto principal.

### 3️⃣ Configurar el `pom.xml` del Microservicio Gateway

Abrimos el archivo `pom.xml` del microservicio `microservice-gateway` y realizamos las siguientes configuraciones:

#### Estructura Completa del `pom.xml` de `microservice-gateway`

```xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.tuNombre</groupId>
        <artifactId>Microservicios-Academia</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <groupId>com.microservice.gateway</groupId>
    <artifactId>microservice-gateway</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>microservice-gateway</name>
    <description>Spring Boot Microservice Gateway</description>

    <properties>
        <java.version>21</java.version>
        <spring-cloud.version>2023.0.3</spring-cloud.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-gateway</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

> **Parent**: Aquí configuramos el proyecto padre `Microservicio-Academia` para que `microservice-gateway` herede las
> configuraciones comunes.

> **spring-cloud-starter-gateway**: Implementa el API Gateway para enrutar las solicitudes HTTP a otros
> microservicios.

> **spring-cloud-starter-netflix-eureka-client**: Registra el microservicio en el Eureka Server.

> **spring-cloud-starter-config**: Permite obtener configuraciones centralizadas desde el Config Server.

> **spring-boot-starter-actuator**: Proporciona métricas y monitoreo para el microservicio.

> **dependencyManagement**: Define la versión de `spring-cloud.version` para gestionar dependencias compatibles en
> Spring Cloud.

### 4️⃣ Actualizar Dependencias para Evitar Vulnerabilidades

En el proyecto, puede ser necesario actualizar ciertas dependencias para resolver problemas de seguridad heredados de
otras librerías. Para actualizar a versiones seguras:

1. En el archivo `pom.xml` del proyecto padre `Microservicios-Academia`, agregamos las siguientes dependencias:

   ```xml
   <!-- Actualización de dependencias para evitar vulnerabilidades -->
   <dependency>
       <groupId>org.springframework</groupId>
       <artifactId>spring-context</artifactId>
       <version>6.1.14</version>
   </dependency>
   <dependency>
       <groupId>com.fasterxml.woodstox</groupId>
       <artifactId>woodstox-core</artifactId>
       <version>7.1.0</version>
   </dependency>
   <dependency>
       <groupId>org.xmlunit</groupId>
       <artifactId>xmlunit-core</artifactId>
       <version>2.10.0</version>
       <scope>test</scope>
   </dependency>
   <dependency>
       <groupId>org.apache.httpcomponents</groupId>
       <artifactId>httpclient</artifactId>
       <version>4.5.14</version>
   </dependency>
   ```

Estas actualizaciones solucionan problemas de seguridad en las versiones antiguas y garantizan que el proyecto esté
libre de vulnerabilidades.

### 5️⃣ Recargar el Proyecto en IntelliJ IDEA

Después de realizar todos los cambios, recargamos el proyecto en IntelliJ IDEA para que se apliquen las actualizaciones del archivo `pom.xml`. Esto garantizará que las dependencias se descarguen y actualicen correctamente.

### 6️⃣ ✅ Verificación de la Configuración del Microservicio Gateway

Si todo está configurado correctamente, veremos el microservicio `microservice-gateway` como un módulo
de `Microservicio-Academia` en IntelliJ IDEA. Ahora el microservicio Gateway está listo para gestionar solicitudes y
actuar como el punto de entrada a nuestra arquitectura de microservicios.

---

## 6.- 💿 Creación del Segundo Microservicio: Eureka Server

Con el **API Gateway** configurado, ahora crearemos el segundo microservicio en nuestro ecosistema: el **Eureka Server**.
Este microservicio actuará como un servidor de registro donde otros microservicios podrán registrarse para facilitar
el descubrimiento mutuo. Esto simplifica la comunicación, ya que los servicios no necesitan conocer las IPs o puertos
exactos de los demás.

### 1️⃣ Crear el Proyecto de Eureka Server en Spring Initializr

Para comenzar, usaremos [Spring Initializr](https://start.spring.io/) para crear el proyecto de Eureka Server.

1. **Abre Spring Initializr** y configuraremos los siguientes valores:

   - **GroupId**: `com.microservice.eureka`
   - **ArtifactId**: `microservice-eureka`
   - **Nombre del proyecto**: `microservice-eureka`
   - **Versión de Spring Boot**: `3.1.4`
   - **Java Version**: `21`

2. **Dependencias**:

   - **Eureka Server**: Para que este servicio actúe como un servidor de registro.
   - **Spring Cloud Config Client**: Permite que el Eureka Server obtenga su configuración del Config Server.
   - **Actuator**: Proporciona métricas y permite monitorear el estado del Eureka Server.

3. **Generar el Proyecto** y descargamos el archivo ZIP, extraemos el contenido y copiamos la carpeta `microservice-eureka` dentro del directorio `Microservicios-Academia`.

### 2️⃣ Configurar el Proyecto Eureka como Módulo en el Proyecto Padre

Para que el microservicio `microservice-eureka` se convierta en un módulo del proyecto `Microservicios-Academia`,
necesitamos hacer algunos ajustes en el archivo `pom.xml` del proyecto padre.

Abrimos el archivo `pom.xml` de `Microservicio-Academia` y agrega el nuevo módulo `microservice-eureka` en la sección de
módulos:

```xml
<modules>
    <module>microservice-gateway</module>
    <module>microservice-eureka</module>
</modules>
```

Esto le indica a Maven que `microservice-eureka` es otro subproyecto (módulo) de `Microservicio-Academia`.

### 3️⃣ Configurar el `pom.xml` del Microservicio Eureka

Abrimos el archivo `pom.xml` de `microservice-eureka` y comprobamos que tiene la siguiente configuración:

```xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.tuNombre</groupId>
        <artifactId>Microservicios-Academia</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <groupId>com.microservice.eureka</groupId>
    <artifactId>microservice-eureka</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <name>microservice-eureka</name>
    <description>Spring Boot Microservice Eureka</description>

    <properties>
        <java.version>21</java.version>
        <spring-cloud.version>2023.0.3</spring-cloud.version>
    </properties>

    <dependencies>
        <!-- Actuator para monitoreo y métricas -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <!-- Config Client para configuración centralizada -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <!-- Eureka Server para registro y descubrimiento de servicios -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

> **Parent**: Este proyecto hereda del proyecto padre `Microservicio-Academia`, de modo que comparte configuraciones
> comunes.

> **spring-cloud-starter-netflix-eureka-server**: Configura el servicio como un servidor Eureka, permitiendo el registro
> y descubrimiento de otros microservicios.

> **spring-cloud-starter-config**: Permite obtener configuraciones centralizadas desde el Config Server.

> **spring-boot-starter-actuator**: Proporciona métricas y monitoreo para el Eureka Server.

> **dependencyManagement**: Especifica la versión de Spring Cloud para gestionar dependencias compatibles en Spring
> Cloud.

---

## 7.- 🪛 Creación del Tercer Microservicio: Config Server

Con el **API Gateway** y el **Eureka Server** configurados, el siguiente paso es crear el **Config Server**. Este
microservicio centralizará la configuración de todos los demás microservicios en nuestra arquitectura, facilitando la
gestión y actualización de configuraciones sin necesidad de modificar cada servicio individualmente.

### 1️⃣ Crear el Proyecto Config Server en Spring Initializr

Para iniciar, vamos a [Spring Initializr](https://start.spring.io/) para configurar el proyecto
de `microservice-config`.

1. **Abrir Spring Initializr** y configuraremos los siguientes valores:

   - **GroupId**: `com.microservice.config`
   - **ArtifactId**: `microservice-config`
   - **Nombre del proyecto**: `microservice-config`
   - **Versión de Spring Boot**: `3.1.4`
   - **Java Version**: `21`

2. **Dependencias**:

   - **Spring Cloud Config Server**: Permite que este microservicio actúe como el servidor central de configuración
     para los otros microservicios.

3. **Generar el Proyecto** y descargamos el archivo ZIP, extraemos el contenido y copiamos la carpeta `microservice-config` dentro del directorio `Microservicios-Academia`.

### 2️⃣ Configurar el Proyecto Config Server como Módulo en el Proyecto Padre

Para que `microservice-config` se integre en el proyecto principal, debemos agregarlo como un **módulo** en el `pom.xml`
del proyecto padre `Microservicios-Academia`.

Abrimos el archivo `pom.xml` del proyecto padre y agrega `microservice-config` a la lista de módulos:

```xml
<modules>
    <module>microservice-gateway</module>
    <module>microservice-eureka</module>
    <module>microservice-config</module>
</modules>
```

Esto le indica a Maven que `microservice-config` es un módulo del proyecto padre.

### 3️⃣ Configurar el `pom.xml` del Microservicio Config Server

Abrimos el archivo `pom.xml` del microservicio `microservice-config` y lo configúramos como se muestra a continuación:

```xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.tuNombre</groupId>
        <artifactId>Microservicios-Academia</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <groupId>com.microservice.config</groupId>
    <artifactId>microservice-config</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <name>microservice-config</name>
    <description>Spring Boot Microservice Config</description>

    <properties>
        <java.version>21</java.version>
        <spring-cloud.version>2023.0.3</spring-cloud.version>
    </properties>

    <dependencies>
        <!-- Config Server para gestión centralizada de configuraciones -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config-server</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

> ⚠️ **Nota**: Al igual que con los microservicios anteriores, una vez copiado el proyecto `microservice-config`, IntelliJ debería reconocerlo como parte del proyecto. Si el proyecto aparece en color gris, realizaremos los pasos de recarga para asegurarnos de que el módulo está bien vinculado.

Con estos tres microservicios añadidos al proyecto global, tenemos configurados los componentes clave de nuestra
arquitectura de microservicios.

---

### 4️⃣ ⚙️ Configuración de la Extensión `application.yml` para Microservicios

Por convención en microservicios, **se prefiere usar `application.yml` en lugar de `application.properties`**. La razón
principal es que los archivos `.yml` utilizan una sintaxis jerárquica, que facilita la lectura y organización de
configuraciones complejas, lo cual es común en entornos de microservicios. Además, permite agrupar las configuraciones
de una manera más visualmente clara, usando indentaciones en lugar de prefijos largos.

Para cambiar la extensión, simplemente renombramos `application.properties` a `application.yml` y actualizamos el contenido según el formato YAML.

```yaml
server:
  port: 8761

spring:
  application:
    name: msvc-eureka
  config:
    import: optional:configserver:http://localhost:8888

eureka:
  instance:
    hostname: localhost
  client:
    register-with-eureka: false
    fetch-registry: false
    server-url:
      defaultZone: http://localhost:${server.port}/eureka/
```

### 5️⃣ 🛠️ Código de la Clase `MicroserviceEurekaApplication`

En el microservicio de **Eureka Server**, la clase principal necesita una anotación específica para habilitar el
servidor Eureka. Aquí está el código completo de la clase `MicroserviceEurekaApplication`:

```java
package com.microservice.eureka;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@EnableEurekaServer
@SpringBootApplication
public class MicroserviceEurekaApplication {

    public static void main(String[] args) {
        SpringApplication.run(MicroserviceEurekaApplication.class, args);
    }
}
```

> **@EnableEurekaServer**: Esta anotación indica que el microservicio funcionará como un servidor de registro de Eureka.

---

## 8.- 👩‍🎓 Creación del Cuarto Microservicio: Students

En esta sección, crearemos el microservicio **Students**, que gestionará la información de los estudiantes en nuestro
ecosistema de microservicios. Este microservicio estará conectado a una base de datos **MySQL** y se registrará en el **Eureka Server** para su descubrimiento.

### 1️⃣ Crear el Proyecto Students en Spring Initializr

Para comenzar, vamos a [Spring Initializr](https://start.spring.io/) para configurar el proyecto de `microservice-student`.

1. **Abrir Spring Initializr** y configuramos los siguientes valores:

   - **GroupId**: `com.microservice.student`
   - **ArtifactId**: `microservice-student`
   - **Nombre del proyecto**: `microservice-student`
   - **Versión de Spring Boot**: `3.1.4`
   - **Java Version**: `21`

2. **Dependencias**:

   - **Spring Web**: Para exponer servicios REST.
   - **Spring Data JPA**: Para la integración con la base de datos.
   - **MySQL Driver**: Conexión a la base de datos MySQL.
   - **Spring Cloud Config Client**: Para obtener configuraciones centralizadas del Config Server.
   - **Eureka Discovery Client**: Para que el microservicio se registre en el Eureka Server.
   - **Actuator**: Proporciona métricas y monitoreo para el microservicio.

3. **Generar el Proyecto** y descargamos el archivo ZIP, extraemos el contenido y copiamos la carpeta `microservice-student` dentro del directorio `Microservicios-Academia`.

### 2️⃣ Configurar el Proyecto Students como Módulo en el Proyecto Padre

Para que `microservice-student` se integre en el proyecto principal, debemos agregarlo como un **módulo** en
el `pom.xml` del proyecto padre `Microservicios-Academia`.

Abrimos el archivo `pom.xml` del proyecto padre y agregamos `microservice-student` a la lista de módulos:

```xml
<modules>
    <module>microservice-gateway</module>
    <module>microservice-eureka</module>
    <module>microservice-config</module>
    <module>microservice-student</module>
</modules>
```

Esto le indica a Maven que `microservice-student` es un módulo del proyecto padre.

### 3️⃣ Configurar el `pom.xml` del Microservicio Students

Abrimos el archivo `pom.xml` del microservicio `microservice-student` y lo configúramos como se muestra a continuación:

```xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.tuNombre</groupId>
        <artifactId>Microservicios-Academia</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <groupId>com.microservice.student</groupId>
    <artifactId>microservice-student</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <name>microservice-student</name>
    <description>Spring Boot Microservice Student</description>

    <properties>
        <java.version>21</java.version>
        <spring-cloud.version>2023.0.3</spring-cloud.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

### 4️⃣ Configuración del `application.yml` del Microservicio Students

Al igual que en los otros microservicios, cambiaremos el archivo de configuración a **`application.yml`** para facilitar
la organización jerárquica de la configuración. Aquí está el contenido de `application.yml` para el
microservicio `microservice-student`:

```yaml
server:
  port: 8090

spring:
  application:
    name: msvc-student

  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/studentDb
    username: root
    password: root
  jpa:
    hibernate:
      ddl-auto: create
    database: mysql
    database-platform: org.hibernate.dialect.MySQLDialect
  config:
    import: optional:configserver:http://localhost:8888

eureka:
  instance:
    hostname: localhost
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

> **server.port**: Define el puerto de ejecución del microservicio como `8090`.

> **spring.datasource**: Configura la conexión a la base de datos MySQL. La base de datos se llama `studentDb` (es
> posible que necesites crearla en tu servidor MySQL).

> **spring.jpa.hibernate.ddl-auto**: `create` para que Hibernate cree las tablas automáticamente en la base de datos.

> **eureka.client.service-url.defaultZone**: Especifica la URL de Eureka para que el microservicio se registre
> automáticamente.

### 5️⃣ Código de la Clase `MicroserviceStudentApplication`

Aquí está el código de la clase principal de `microservice-student`, que necesita la anotación `@EnableDiscoveryClient`
para que pueda registrarse en Eureka.

```java
package com.microservice.student;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

@EnableDiscoveryClient
@SpringBootApplication
public class MicroserviceStudentApplication {

    public static void main(String[] args) {
        SpringApplication.run(MicroserviceStudentApplication.class, args);
    }
}
```

> **@EnableDiscoveryClient**: Esta anotación no es obligatoria, pero es buena práctica agregarla para indicar
> explícitamente que este microservicio se registrará en el Eureka Server.

### 6️⃣ 🚀 Levantar y probar el Microservicio Students

1. **Iniciar el Eureka Server**: Nos aseguraremos de que el servidor Eureka esté en funcionamiento.
2. **Iniciar el Microservicio Students**: Iniciamos el microservicio `microservice-student`. Aunque puede mostrar un error de conexión a la base de datos si `studentDb` no existe, el microservicio debería registrarse en el servidor de Eureka.
3. **Verificar el Registro en Eureka**: Accedemos a `http://localhost:8761` en el navegador y verificamos que `msvc-student` esté listado en los servicios registrados en Eureka.

---

## 9.- 📘 Creación del Quinto Microservicio: Courses

Con el microservicio **Students** funcionando, ahora vamos a crear el microservicio **Courses**, el cual gestionará la
información de los cursos en nuestra aplicación de microservicios. Este microservicio utilizará **PostgreSQL** como su
base de datos, demostrando la flexibilidad de los microservicios para trabajar con distintas tecnologías de
almacenamiento.

### 1️⃣ Crear el Proyecto Courses en Spring Initializr

Para iniciar, vamos a [Spring Initializr](https://start.spring.io/) para configurar el proyecto
de `microservice-course`.

1. **Abrir Spring Initializr** y configuramos los siguientes valores:

   - **GroupId**: `com.microservice.course`
   - **ArtifactId**: `microservice-course`
   - **Nombre del proyecto**: `microservice-course`
   - **Versión de Spring Boot**: `3.1.4`
   - **Java Version**: `21`

2. **Dependencias**:

   - **Spring Web**: Para exponer servicios REST.
   - **Spring Data JPA**: Para la integración con la base de datos.
   - **PostgreSQL Driver**: Conexión a la base de datos PostgreSQL.
   - **Spring Cloud Config Client**: Permite obtener configuraciones centralizadas desde el Config Server.
   - **Eureka Discovery Client**: Para que el microservicio se registre en el Eureka Server.
   - **Actuator**: Para métricas y monitoreo del microservicio.

3. **Generar el Proyecto** y descargamos el archivo ZIP, extraemos el contenido y copiamos la carpeta `microservice-course` dentro del directorio `Microservicios-Academia`.

### 2️⃣ Configurar el Proyecto Courses como Módulo en el Proyecto Padre

Para que `microservice-course` se integre en el proyecto principal, debemos agregarlo como un **módulo** en el `pom.xml`
del proyecto padre `Microservicios-Academia`.

Abrimos el archivo `pom.xml` del proyecto padre y agregamos `microservice-course` a la lista de módulos:

```xml
<modules>
    <module>microservice-gateway</module>
    <module>microservice-eureka</module>
    <module>microservice-config</module>
    <module>microservice-student</module>
    <module>microservice-course</module>
</modules>
```

Esto le indica a Maven que `microservice-course` es un módulo del proyecto padre.

### 3️⃣ Configurar el `pom.xml` del Microservicio Courses

Abrimos el archivo `pom.xml` del microservicio `microservice-course` y lo configúramos como se muestra a continuación:

```xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <parent>
        <groupId>com.tuNombre</groupId>
        <artifactId>Microservicios-Academia</artifactId>
        <version>1.0-SNAPSHOT</version>
    </parent>

    <groupId>com.microservice.course</groupId>
    <artifactId>microservice-course</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <name>microservice-course</name>
    <description>Spring Boot Microservice Course</description>

    <properties>
        <java.version>21</java.version>
        <spring-cloud.version>2023.0.3</spring-cloud.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>

        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```

### 4️⃣ Configuración del `application.yml` del Microservicio Courses

Al igual que en los otros microservicios, cambiaremos el archivo de configuración a **`application.yml`** para una
organización jerárquica. Aquí está el contenido de `application.yml` para el microservicio `microservice-course`:

```yaml
server:
  port: 9090

spring:
  application:
    name: msvc-course

  datasource:
    driver-class-name: org.postgresql.Driver
    url: jdbc:postgresql://localhost:5432/courseDb
    username: root
    password: 1234
  jpa:
    hibernate:
      ddl-auto: create
    database: postgresql
    database-platform: org.hibernate.dialect.PostgreSQLDialect
  config:
    import: optional:configserver:http://localhost:8888

eureka:
  instance:
    hostname: localhost
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

> **server.port**: Define el puerto de ejecución del microservicio como `9090`.

> **spring.datasource**: Configura la conexión a la base de datos PostgreSQL. La base de datos se llama `courseDb` (
> deberás crearla en tu servidor PostgreSQL).

> **spring.jpa.hibernate.ddl-auto**: `create` para que Hibernate genere las tablas automáticamente en la base de datos.

> **eureka.client.service-url.defaultZone**: Especifica la URL de Eureka para que el microservicio se registre
> automáticamente.

### 5️⃣ Código de la Clase `MicroserviceCourseApplication`

Aquí está el código de la clase principal de `microservice-course`, que necesita la anotación `@EnableDiscoveryClient`
para que pueda registrarse en Eureka.

```java
package com.microservice.course;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;

@EnableDiscoveryClient
@SpringBootApplication
public class MicroserviceCourseApplication {

    public static void main(String[] args) {
        SpringApplication.run(MicroserviceCourseApplication.class, args);
    }
}
```

> **@EnableDiscoveryClient**: Aunque no es obligatoria, esta anotación es buena práctica para indicar explícitamente que
> este microservicio se registrará en el Eureka Server.

---

## 10.- ⚙️ Configurar el Microservicio de Estudiantes

En esta sección, configuraremos el microservicio **Students** para que administre la información de los estudiantes en
la aplicación de microservicios. Implementaremos la estructura completa del microservicio, incluyendo la entidad de base
de datos, repositorio, servicios y controladores.

### 1️⃣ Estructura del Microservicio Students

Vamos a configurar varias capas para nuestro microservicio de estudiantes:

1. **Capa de Entidades**: Define el modelo de datos y sus anotaciones de JPA.
2. **Capa de Persistencia**: La interfaz del repositorio para interactuar con la base de datos.
3. **Capa de Servicios**: Define la lógica de negocio.
4. **Capa de Controladores**: Expone los endpoints para las operaciones REST.

### 2️⃣ Entidad `Student`

La entidad `Student` representa un estudiante en el sistema. Incluye varias anotaciones importantes que permiten que
Spring Data JPA administre esta entidad en la base de datos.

```java
import lombok.*;

import javax.persistence.*;

@Data
@Entity
@Builder
@Table(name = "students")
@AllArgsConstructor
@NoArgsConstructor
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @Column(name = "last_name")
    private String lastname;

    private String email;

    @Column(name = "course_id")
    private Long courseId;
}
```

> **@Data**: Genera automáticamente getters, setters, `equals`, `hashCode`, y `toString` a través de Lombok.

> **@Entity**: Define esta clase como una entidad de JPA, vinculándola a una tabla en la base de datos.

> **@Table(name="students")**: Define el nombre de la tabla en la base de datos. En este caso, será `students`.

> **@Id**: Especifica el campo `id` como la clave primaria de la tabla.

> **@GeneratedValue(strategy = GenerationType.IDENTITY)**: Indica que el valor de `id` se generará automáticamente por
> la base de datos usando la estrategia `IDENTITY`.

> **@Column(name="...")**: Especifica el nombre exacto de la columna en la base de datos, útil cuando queremos que el
> nombre de la columna difiera del nombre del campo en la clase (como `last_name` y `course_id`).

### 3️⃣ Repositorio `StudentRepository`

El repositorio proporciona métodos para interactuar con la base de datos, incluyendo consultas personalizadas.

```java
package com.microservice.student.persistence;

import com.microservice.student.entities.Student;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

import java.util.List;

@Repository
public interface StudentRepository extends CrudRepository<Student, Long> {

    @Query("SELECT s FROM Student s WHERE s.courseId = :idCourse")
    List<Student> findAllStudent(Long idCourse);

    // Alternativa usando el nombre de método
    // List<Student> findAllByCourseId(Long idCourse);
}
```

> **@Repository**: Marca esta interfaz como un repositorio de Spring, lo que permite la inyección de dependencias y
> manejo de excepciones específicas de persistencia.

> **@Query(...)**: Define una consulta personalizada de JPA que selecciona estudiantes basándose en su `courseId`. En
> este caso, se usa `:idCourse` como un parámetro que se pasa en tiempo de ejecución.

> ✅ **Nota**: Alternativamente, podríamos usar `findAllByCourseId(Long idCourse)` sin la anotación `@Query`, ya que Spring
> Data genera la consulta automáticamente basándose en el nombre del método.

### 4️⃣ Interfaz del Servicio `IStudentService`

Definimos la interfaz `IStudentService`, que declara los métodos de la lógica de negocio que implementaremos en `StudentServiceImpl`.

```java
package com.microservice.student.service;

import com.microservice.student.entities.Student;

import java.util.List;

public interface IStudentService {

    List<Student> findAll();

    Student findById(Long id);

    void save(Student student);

    List<Student> findByIdCourse(Long idCourse);
}
```

### 5️⃣ Implementación del Servicio `StudentServiceImpl`

La clase `StudentServiceImpl` implementa los métodos declarados en la interfaz de servicio.

```java
package com.microservice.student.service;

import com.microservice.student.entities.Student;
import com.microservice.student.persistence.StudentRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class StudentServiceImpl implements IStudentService {

    private final StudentRepository studentRepository;

    public StudentServiceImpl(StudentRepository studentRepository) {
        this.studentRepository = studentRepository;
    }

    @Override
    public List<Student> findAll() {
        return (List<Student>) studentRepository.findAll();
    }

    @Override
    public Student findById(Long id) {
        return studentRepository.findById(id).orElseThrow();
    }

    @Override
    public void save(Student student) {
        studentRepository.save(student);
    }

    @Override
    public List<Student> findByIdCourse(Long idCourse) {
        return studentRepository.findAllStudent(idCourse);
    }
}
```

> **@Service**: Marca esta clase como un servicio de Spring, lo que permite su inyección en otros componentes.

> **findAll()**: Devuelve todos los estudiantes.
> **findById(Long id)**: Busca un estudiante por su ID, lanzando una excepción si no se encuentra.

> **save(Student student)**: Guarda el estudiante en la base de datos.

> **findByIdCourse(Long idCourse)**: Usa el método `findAllStudent` para obtener estudiantes por `courseId`.

### 6️⃣ Controlador `StudentController`

El controlador `StudentController` expone los endpoints REST para que el microservicio Students pueda responder a peticiones HTTP.

```java
package com.microservice.student.controller;

import com.microservice.student.entities.Student;
import com.microservice.student.service.IStudentService;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/student")
public class StudentController {

    private final IStudentService studentService;

    public StudentController(IStudentService studentService) {
        this.studentService = studentService;
    }

    @PostMapping("/create")
    @ResponseStatus(HttpStatus.CREATED)
    public void saveStudent(@RequestBody Student student) {
        studentService.save(student);
    }

    @GetMapping("/all")
    public ResponseEntity<?> findAllStudents() {
        return ResponseEntity.ok(studentService.findAll());
    }

    @GetMapping("/search/{id}")
    public ResponseEntity<?> findById(@PathVariable long id) {
        return ResponseEntity.ok(studentService.findById(id));
    }
}
```

> **@RestController**: Define la clase como un controlador de Spring que responderá a solicitudes HTTP, devolviendo datos JSON como respuesta.

> **@RequestMapping("/api/student")**: Define la ruta base del controlador. Todos los endpoints estarán bajo `/api/student`.

> **@PostMapping("/create")**: Mapea el método `saveStudent` al endpoint `/api/student/create` para crear un nuevo estudiante usando el verbo `POST`.

> **@RequestBody**: Indica que el parámetro `student` proviene del cuerpo de la solicitud JSON.

> **@ResponseStatus(HttpStatus.CREATED)**: Especifica que la respuesta será un código `201 Created` cuando el estudiante se cree correctamente.

> **@GetMapping("/all")**: Mapea el método `findAllStudents` al endpoint `/api/student/all` para obtener la lista de todos los estudiantes.

> **@GetMapping("/search/{id}")**: Mapea el método `findById` al endpoint `/api/student/search/{id}` para buscar un estudiante por su ID.

> **@PathVariable**: Captura el valor `{id}` de la URL y lo pasa como parámetro al método.

Con esto, hemos completado la configuración del microservicio **Students**, incluyendo la entidad `Student`, el repositorio, el servicio y el controlador. Este microservicio ahora está listo para responder a las solicitudes HTTP y puede conectarse con otras partes del sistema a través del `courseId` para identificar cursos asociados.

---

## ️ 11.- 📚 Servicio de Cursos

En este punto, vamos a implementar la estructura del microservicio **Courses** de manera similar al microservicio **Students**. Este servicio se encargará de administrar la información de los cursos en nuestro sistema, permitiendo almacenar, recuperar y gestionar cursos de manera independiente.

### 1️⃣ 🎢 Estructura del Microservicio Courses

Este microservicio se compone de las mismas capas clave que el servicio de estudiantes:

1. **Capa de Entidades**: Representa el modelo de datos del curso.
2. **Capa de Persistencia**: Proporciona una interfaz para la interacción con la base de datos.
3. **Capa de Servicios**: Contiene la lógica de negocio.
4. **Capa de Controladores**: Expondrá los endpoints REST.

### 2️⃣ Entidad `Course`

La entidad `Course` representa un curso en el sistema. Esta clase será gestionada por JPA, y cada instancia representa un registro en la tabla `courses` de la base de datos.

```java
package com.microservice.course.entities;

import jakarta.persistence.*;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@Entity
@Builder
@Table(name = "courses")
@AllArgsConstructor
@NoArgsConstructor
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    private String teacher;
}
```

> **@Data**: Genera métodos `getters`, `setters`, `equals`, `hashCode`, y `toString` usando Lombok.

> **@Entity**: Define que esta clase es una entidad JPA y se vincula a una tabla en la base de datos.

> **@Table(name="courses")**: Especifica el nombre de la tabla en la base de datos como `courses`.

> **@Id** y **@GeneratedValue(strategy = GenerationType.IDENTITY)**: Indican que el campo `id` es la clave primaria y que su valor se generará automáticamente mediante la estrategia `IDENTITY`.

### 3️⃣ Repositorio `ICourseRepository`

El repositorio proporciona los métodos básicos de CRUD para interactuar con la base de datos. No necesitamos métodos
personalizados en este caso.

```java
package com.microservice.course.persistence;

import com.microservice.course.entities.Course;
import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface ICourseRepository extends CrudRepository<Course, Long> {
}
```

> **@Repository**: Define la interfaz como un repositorio, lo que permite a Spring gestionar excepciones de persistencia y simplificar la inyección de dependencias.

Al extender `CrudRepository`, heredamos los métodos básicos como `save`, `findById`, `findAll`, y `delete`, permitiendo realizar operaciones CRUD sin necesidad de definir métodos explícitos.

### 4️⃣ Interfaz del Servicio `ICourseService`

La interfaz `ICourseService` define los métodos de negocio que el servicio de cursos implementará. En este caso, necesitamos métodos para obtener todos los cursos, encontrar un curso por ID y guardar un curso.

```java
package com.microservice.course.service;

import com.microservice.course.entities.Course;

import java.util.List;

public interface ICourseService {

    List<Course> findAll();

    Course findById(Long id);

    void save(Course course);
}
```

### 5️⃣ Implementación del Servicio `CourseServiceImpl`

La clase `CourseServiceImpl` implementa los métodos declarados en la interfaz `ICourseService`.

```java
package com.microservice.course.service;

import com.microservice.course.entities.Course;
import com.microservice.course.persistence.ICourseRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class CourseServiceImpl implements ICourseService {

    private final ICourseRepository courseRepository;

    public CourseServiceImpl(ICourseRepository courseRepository) {
        this.courseRepository = courseRepository;
    }

    @Override
    public List<Course> findAll() {
        return (List<Course>) courseRepository.findAll();
    }

    @Override
    public Course findById(Long id) {
        return courseRepository.findById(id).orElseThrow();
    }

    @Override
    public void save(Course course) {
        courseRepository.save(course);
    }
}
```

> **@Service**: Define esta clase como un servicio de Spring, permitiendo su inyección en otros componentes de la aplicación.

> **findAll()**: Devuelve todos los cursos.

> **findById(Long id)**: Busca un curso por su ID. Lanza una excepción si no encuentra el curso.

> **save(Course course)**: Guarda el curso en la base de datos.

### 6️⃣ Controlador `CourseController`

El controlador `CourseController` expone los endpoints REST que permiten interactuar con el microservicio de cursos.

```java
package com.microservice.course.controller;

import com.microservice.course.entities.Course;
import com.microservice.course.service.ICourseService;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/course")
public class CourseController {
    private final ICourseService courseService;

    public CourseController(ICourseService courseService) {
        this.courseService = courseService;
    }

    @PostMapping("/create")
    @ResponseStatus(HttpStatus.CREATED)
    public void saveCourse(@RequestBody Course course) {
        courseService.save(course);
    }

    @GetMapping("/all")
    public ResponseEntity<?> findAllCourses() {
        return ResponseEntity.ok(courseService.findAll());
    }

    @GetMapping("/search/{id}")
    public ResponseEntity<?> findById(@PathVariable long id) {
        return ResponseEntity.ok(courseService.findById(id));
    }
}
```

> **@RestController**: Define la clase como un controlador REST de Spring.

> **@RequestMapping("/api/course")**: Establece la ruta base para los endpoints de este controlador como `/api/course`.

> **@PostMapping("/create")**: Define el endpoint para crear un nuevo curso.

> **@RequestBody**: Permite que el parámetro `course` se mapee automáticamente desde el cuerpo de la solicitud JSON.

> **@ResponseStatus(HttpStatus.CREATED)**: Devuelve un código de estado `201 Created` al guardar el curso exitosamente.

> **@GetMapping("/all")**: Endpoint que devuelve una lista de todos los cursos.

> **@GetMapping("/search/{id}")**: Endpoint que devuelve un curso específico basado en su `id`, utilizando **@PathVariable** para capturar el valor desde la URL.

Con esta implementación, el microservicio **Courses** está listo para gestionar la información de los cursos. Este microservicio tiene una estructura similar al de estudiantes y proporciona endpoints REST para crear, obtener y buscar cursos. Con esta base, ambos microservicios están preparados para futuras configuraciones que permitan la comunicación entre ellos y otros microservicios del sistema.

---

## 12.- 📡 Comunicación entre Microservicios **Students** y **Courses**

En este punto, vamos a establecer la comunicación entre los microservicios **Students** y **Courses**. Esto permitirá que el microservicio **Courses** pueda consultar a **Students** para obtener la lista de estudiantes de un curso específico.

Para ello, usaremos **OpenFeign**, el cliente HTTP declarativo de Spring, ideal para comunicación entre microservicios en arquitecturas distribuidas.

### 1️⃣ Crear el Endpoint en el Microservicio **Students**

Primero, en el controlador del microservicio **Students**, vamos a definir un nuevo endpoint que permita obtener la lista de estudiantes según el `idCourse`. Este endpoint será consumido por **Courses**.

#### Modificación en `StudentController` de Students:

```java

@RestController
@RequestMapping("/api/student")
public class StudentController {
    private final IStudentService studentService;

    public StudentController(IStudentService studentService) {
        this.studentService = studentService;
    }

    // Nuevo endpoint para obtener estudiantes por curso
    @GetMapping("/search-by-course/{idCourse}")
    public ResponseEntity<?> findByIdCourse(@PathVariable long idCourse) {
        return ResponseEntity.ok(studentService.findByIdCourse(idCourse));
    }
}
```

> **Endpoint `/search-by-course/{idCourse}`**: Permite al microservicio **Courses** consultar a **Students** para obtener la lista de estudiantes que pertenecen a un curso específico, usando el `idCourse`.

### 2️⃣ Añadir la Dependencia de **Feign** en el Microservicio **Courses**

Para usar **Feign** en **Courses**, agregamos la dependencia `spring-cloud-starter-openfeign` en su archivo `pom.xml`.

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

Además, para evitar vulnerabilidades relacionadas, actualizamos el `pom.xml` del **proyecto padre** con la última versión de `commons-io`:

```xml
<!-- Actualización de dependencias para evitar vulnerabilidades -->
...
<dependency>
    <groupId>commons-io</groupId>
    <artifactId>commons-io</artifactId>
    <version>2.17.0</version>
</dependency>
```

### 3️⃣ Habilitar **Feign** en el Microservicio **Courses**

En la clase principal de **Courses**, añadimos la anotación `@EnableFeignClients` para habilitar el uso de Feign y `@EnableDiscoveryClient` para el registro en Eureka:

```java
package com.microservice.course;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.cloud.openfeign.EnableFeignClients;

@EnableFeignClients
@EnableDiscoveryClient
@SpringBootApplication
public class MicroserviceCourseApplication {

    public static void main(String[] args) {
        SpringApplication.run(MicroserviceCourseApplication.class, args);
    }
}
```

### 4️⃣ Crear el Cliente Feign `StudentClient` en **Courses**

En **Courses**, creamos una interfaz `StudentClient` dentro del paquete `client`, que representará la conexión con el servicio **Students**.

```java
package com.microservice.course.client;

import com.microservice.course.dto.StudentDto;
import org.springframework.cloud.openfeign.FeignClient;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;

import java.util.List;

@FeignClient(name = "msvc-student", url = "localhost:8090/api/student/")
public interface StudentClient {

    @GetMapping("/search-by-course/{idCourse}")
    List<StudentDto> findAllStudentByCourse(@PathVariable Long idCourse);
}
```

> **`@FeignClient(name="msvc-student", url="localhost:8090/api/student/")`**: Configura Feign para comunicarse con el microservicio **Students**.

> **Método `findAllStudentByCourse(Long idCourse)`**: Representa el endpoint remoto que obtendrá la lista de estudiantes en función del `idCourse`.

### 5️⃣ Crear el DTO `StudentDto` en **Courses**

Creamos un **DTO** (`StudentDto`) en **Courses** para recibir los datos de los estudiantes desde el microservicio **Students**.

```java
package com.microservice.course.dto;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@Builder
@AllArgsConstructor
@NoArgsConstructor
public class StudentDto {

    private String name;
    private String lastname;
    private String email;
    private Long courseId;
}
```

### 6️⃣ Crear una Clase de Respuesta `StudentByCourseResponse` en **Courses**

Para estructurar la respuesta que **Courses** le devolverá al cliente final, creamos `StudentByCourseResponse`, que reúne los datos del curso y la lista de estudiantes.

```java
package com.microservice.course.http.response;

import com.microservice.course.dto.StudentDto;
import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.util.List;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class StudentByCourseResponse {
    private String courseName;
    private String teacher;
    private List<StudentDto> studentDtoList;
}
```

### 7️⃣ Implementar el Método de Comunicación en `ICourseService` y `CourseServiceImpl`

En la interfaz `ICourseService`, añadimos un nuevo método `findStudentsByIdCourse` para obtener estudiantes por curso.

```java
public interface ICourseService {
    // Otros métodos
    StudentByCourseResponse findStudentsByIdCourse(Long idCourse);
}
```

Implementamos este método en `CourseServiceImpl`:

```java
package com.microservice.course.service;

import com.microservice.course.client.StudentClient;
import com.microservice.course.dto.StudentDto;
import com.microservice.course.entities.Course;
import com.microservice.course.http.response.StudentByCourseResponse;
import com.microservice.course.persistence.ICourseRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class CourseServiceImpl implements ICourseService {

    private final ICourseRepository courseRepository;
    private final StudentClient studentClient;

    public CourseServiceImpl(ICourseRepository courseRepository, StudentClient studentClient) {
        this.courseRepository = courseRepository;
        this.studentClient = studentClient;
    }

    @Override
    public StudentByCourseResponse findStudentsByIdCourse(Long idCourse) {
        // Consultar el curso
        Course course = courseRepository.findById(idCourse).orElse(new Course());

        // Obtener los estudiantes
        List<StudentDto> studentDtoList = studentClient.findAllStudentByCourse(idCourse);

        // Construir la respuesta
        return StudentByCourseResponse.builder()
                .courseName(course.getName())
                .teacher(course.getTeacher())
                .studentDtoList(studentDtoList)
                .build();
    }
}
```

### 8️⃣ Exponer el Endpoint en `CourseController` de **Courses**

Finalmente, añadimos un endpoint en **Courses** para que los clientes puedan consultar la lista de estudiantes de un curso específico.

```java
package com.microservice.course.controller;

import com.microservice.course.service.ICourseService;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/course")
public class CourseController {
    private final ICourseService courseService;

    public CourseController(ICourseService courseService) {
        this.courseService = courseService;
    }

    @GetMapping("/search-student/{idCourse}")
    public ResponseEntity<?> findStudentsByIdCourse(@PathVariable long idCourse) {
        return ResponseEntity.ok(courseService.findStudentsByIdCourse(idCourse));
    }
}
```

> **Endpoint `/search-student/{idCourse}`** en **Courses**: Permite a los clientes consultar la lista de estudiantes asociados a un curso específico, utilizando el `idCourse`.

Con esta configuración, ahora **Courses** puede consultar a **Students** para obtener la lista de estudiantes de un curso específico. Cuando el cliente accede al endpoint `/api/course/search-student/{idCourse}` en **Courses**:

1. **Courses** hace una llamada HTTP al microservicio **Students** utilizando Feign.
2. **Students** responde con la lista de estudiantes.
3. **Courses** devuelve una respuesta personalizada (`StudentByCourseResponse`) al cliente final, incluyendo el nombre del curso, el profesor y los estudiantes.

Este flujo garantiza una comunicación eficiente y desacoplada entre los microservicios, aprovechando al máximo las capacidades de Spring Cloud y OpenFeign.

---

## 13. 🛠️ Configuración de Bases de Datos y Datos de Prueba

Para probar nuestra configuración, necesitamos datos de prueba en las bases de datos de **Students** (MySQL) y **Courses** (PostgreSQL). Aquí vamos a crear las bases de datos, definir las tablas necesarias y añadir datos de prueba con el archivo `import.sql`. Además, configuraremos **Eureka** para que administre correctamente el estado de los microservicios.

### 1️⃣ Crear el archivo `import.sql` en el Microservicio **Students**

En **Students**, vamos a crear un archivo `import.sql` en `src/main/resources` para insertar automáticamente datos de prueba en la tabla `students` cada vez que arranque el microservicio.

#### 📄 Contenido de `import.sql` en el Microservicio **Students**:

```sql
INSERT INTO students (name, last_name, email, course_id) VALUES ('Juan', 'Perez', 'jua.perez@example.com', 1);
INSERT INTO students (name, last_name, email, course_id) VALUES ('María', 'González', 'mar.gon@example.com', 2);
INSERT INTO students (name, last_name, email, course_id) VALUES ('Carlos', 'López', 'car.lop@example.com', 3);
INSERT INTO students (name, last_name, email, course_id) VALUES ('Ana', 'Martínez', 'ana.mar@example.com', 1);
INSERT INTO students (name, last_name, email, course_id) VALUES ('Pedro', 'Sánchez', 'pedro.san@example.com', 3);
```

Este archivo se ejecutará al arrancar el microservicio y poblará la tabla `students` con datos de prueba.

### 2️⃣ Crear la Base de Datos **studentDb** en MySQL Workbench

Para que los datos de prueba se inserten correctamente, primero debemos crear la base de datos `studentDb` en MySQL. Ejecutamos el siguiente comando en **MySQL Workbench**:

```sql
CREATE DATABASE studentDb;
```

Luego, nos hemos de asegurar de que el microservicio **Students** se conecta correctamente a `studentDb`. Cuando levantamos el microservicio, MySQL debería crear automáticamente la tabla `students` y poblarla con los datos de prueba del archivo `import.sql`.

### 3️⃣ Crear el archivo `import.sql` en el Microservicio **Courses**

En el microservicio **Courses**, creamos un archivo similar para los datos de prueba de `courses`. Colócalo en `src/main/resources`.

#### 📄 Contenido de `import.sql` en el Microservicio **Courses**:

```sql
INSERT INTO courses (name, teacher) VALUES ('Matematicas', 'Profesor A');
INSERT INTO courses (name, teacher) VALUES ('Física', 'Profesor B');
INSERT INTO courses (name, teacher) VALUES ('Historia', 'Profesor C');
INSERT INTO courses (name, teacher) VALUES ('Literatura', 'Profesor D');
INSERT INTO courses (name, teacher) VALUES ('Biología', 'Profesor E');
```

### 4️⃣ Crear la Base de Datos **courseDb** en PostgreSQL

Para **Courses**, necesitamos crear la base de datos `courseDb` en **pgAdmin**. Seguiremos estos pasos:

1. En **pgAdmin**, seleccionamos el servidor de PostgreSQL y hacemos clic derecho en "Databases".
2. Eligimos "Create" y asignamos el nombre `courseDb`.
3. Guardamos la configuración para crear la base de datos.

Cuando arranque el microservicio **Courses**, PostgreSQL deberíamos crear automáticamente la tabla `courses` y poblarla con los datos del archivo `import.sql`.

### 5️⃣ Iniciar los Microservicios y Registrar en **Eureka**

1. Iniciamos **Eureka** (disponible en `http://localhost:8761`). Verificamos que el servidor Eureka esté corriendo.
2. Luego, iniciamos los microservicios **Students** y **Courses**.

Después de iniciar ambos servicios, deberíaamos verlos registrados en Eureka en la URL `http://localhost:8761`.

### 6️⃣ ⚠️ Mensaje de Error en **Eureka**

Si Eureka muestra el mensaje:

> _EMERGENCY! EUREKA MAY BE INCORRECTLY CLAIMING INSTANCES ARE UP WHEN THEY'RE NOT. RENEWALS ARE LESSER THAN THRESHOLD AND HENCE THE INSTANCES ARE NOT BEING EXPIRED JUST TO BE SAFE._

Este mensaje indica que los microservicios no se están comunicando con la frecuencia esperada con el servidor de Eureka. Para evitar que este mensaje aparezca, podemos ajustar las configuraciones de tiempo de espera en los `application.yml` de cada microservicio cliente, en este caso Students y Courses. Añadimos lo siguiente:

```yaml
eureka:
  instance:
    lease-renewal-interval-in-seconds: 5 # Intervalo de renovación
    lease-expiration-duration-in-seconds: 10 # Duración antes de expirar
```

Con esto, cada microservicio actualizará su registro en Eureka cada 5 segundos, y Eureka esperará 10 segundos antes de considerar un servicio como inactivo.

### 7️⃣ Consultar las Tablas en las Bases de Datos para Verificar los Datos

En **MySQL** (para **Students**) y **PostgreSQL** (para **Courses**), ejecutamos los siguientes comandos para confirmar que los datos se han insertado correctamente:

- En **MySQL**:

  ```sql
  SELECT * FROM students;
  ```

- En **PostgreSQL**:

  ```sql
  SELECT * FROM courses;
  ```

### 8️⃣ Pruebas con **Postman**

Con **Eureka**, **Students** y **Courses** en funcionamiento, vamos a probar los endpoints configurados en ambos microservicios:

1. **Obtener estudiantes de un curso específico** desde **Courses**:

   **Endpoint**: `GET http://localhost:9090/api/course/search-student/1`

   **Respuesta esperada**:

   ```json
   {
     "courseName": "Matematicas",
     "teacher": "Profesor A",
     "studentDtoList": [
       {
         "name": "Juan",
         "lastname": "Perez",
         "email": "jua.perez@example.com",
         "courseId": 1
       },
       {
         "name": "Ana",
         "lastname": "Martínez",
         "email": "ana.mar@example.com",
         "courseId": 1
       }
     ]
   }
   ```

2. **Obtener todos los cursos** en **Courses**:

   **Endpoint**: `GET http://localhost:9090/api/course/all`

   **Respuesta esperada**:

   ```json
   [
     {
       "id": 1,
       "name": "Matematicas",
       "teacher": "Profesor A"
     },
     {
       "id": 2,
       "name": "Física",
       "teacher": "Profesor B"
     },
     {
       "id": 3,
       "name": "Historia",
       "teacher": "Profesor C"
     },
     {
       "id": 4,
       "name": "Literatura",
       "teacher": "Profesor D"
     },
     {
       "id": 5,
       "name": "Biología",
       "teacher": "Profesor E"
     }
   ]
   ```

3. **Obtener estudiantes de un curso** directamente desde el microservicio **Students**:

   **Endpoint**: `GET http://localhost:8090/api/student/search-by-course/1`

   **Respuesta esperada**:

   ```json
   [
     {
       "id": 1,
       "name": "Juan",
       "lastname": "Perez",
       "email": "jua.perez@example.com",
       "courseId": 1
     },
     {
       "id": 4,
       "name": "Ana",
       "lastname": "Martínez",
       "email": "ana.mar@example.com",
       "courseId": 1
     }
   ]
   ```

---

## 14. 🌐 Configuración del microservicio Gateway

El microservicio **Gateway** actúa como punto de entrada centralizado para nuestro ecosistema de microservicios. A través de él, podemos enrutar solicitudes a los microservicios **Students** y **Courses** de manera controlada. A continuación, configuraremos el **Gateway** para que pueda redirigir las peticiones según las rutas establecidas y probaremos su funcionamiento.

### 1️⃣ Configuración del Banner y `application.yml`

Para una mejor identificación del **Gateway**, creamos un archivo `banner.txt` en el directorio `src/main/resources` con un diseño personalizado para visualizar en la consola cuando se inicia este servicio.

Después, cambiaremos la extensión del archivo de configuración a `application.yml` y añadiremos la siguiente configuración:

```yaml
server:
  port: 8080
spring:
  config:
    import: optional:configserver:http://localhost:8888
  application:
    name: msvc-gateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true # Habilita la detección de microservicios registrados en Eureka
      routes:
        - id: students # Identificador único para la ruta hacia el microservicio Students
          uri: http://localhost:8090 # URI de destino para el microservicio Students
          predicates:
            - Path=/api/student/** # Redirige todas las peticiones que empiecen con /api/student

        - id: courses # Identificador único para la ruta hacia el microservicio Courses
          uri: http://localhost:9090 # URI de destino para el microservicio Courses
          predicates:
            - Path=/api/course/** # Redirige todas las peticiones que empiecen con /api/course
```

> **server.port**: establece el puerto en el cual se ejecuta el Gateway (8080).

> **spring.cloud.gateway.discovery.locator.enabled**: permite que el Gateway descubra automáticamente los microservicios registrados en **Eureka**.

> **spring.cloud.gateway.routes**: define las rutas manuales para los microservicios **Students** y **Courses** con sus respectivos patrones de ruta y puertos.

> 📝 Nota: En el archivo `pom.xml` del **Gateway**, Nos hemos de asegurar de utilizar la dependencia correcta para el starter del gateway. Puede que, por error, se haya incluido `spring-cloud-starter-gateway-mvc`, que no funciona correctamente en este caso. La dependencia correcta es:

    ```xml
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-gateway</artifactId>
    </dependency>
    ```

### 2️⃣ 🚀 Levantando los Servicios en Orden

Para verificar el funcionamiento completo, levantaremos los servicios en el siguiente orden:

1. **Eureka** - para que registre los microservicios.
2. **Students** y **Courses** - para que estén disponibles en el Gateway.
3. **Gateway** - para redirigir las solicitudes entrantes.

### 3️⃣ 🔍 Pruebas en Postman a través del Gateway (Puerto 8080)

#### 1. Obteniendo todos los cursos

- **Solicitud:** `GET http://localhost:8080/api/course/all`
- **Respuesta esperada:**
  ```json
  [
      {
          "id": 1,
          "name": "Matematicas",
          "teacher": "Profesor A"
      },
      ...
  ]
  ```

#### 2. Obteniendo todos los estudiantes

- **Solicitud:** `GET http://localhost:8080/api/student/all`
- **Respuesta esperada:**
  ```json
  [
      {
          "id": 1,
          "name": "Juan",
          "lastname": "Perez",
          "email": "jua.perez@example.com",
          "courseId": 1
      },
      ...
  ]
  ```

### 4️⃣ 🛠 Ajuste de URL en el Cliente Feign

#### - Obteniendo estudiantes de un curso a través del cliente Feign

- **Solicitud:** `GET http://localhost:8080/api/course/search-student/1`
- **Respuesta esperada:**

  ```json
  {
      "courseName": "Matematicas",
      "teacher": "Profesor A",
      "studentDtoList": [
          {
              "name": "Juan",
              "lastname": "Perez",
              "email": "jua.perez@example.com",
              "courseId": 1
          },
          ...
      ]
  }
  ```

> ⚠️ **Nota**: Si la prueba falla con un **error 500**, revisamos que el **Cliente Feign** esté apuntando al **Gateway** y no al puerto directo del microservicio de Students.

Para que Feign Client realice las solicitudes a través del **Gateway**, actualizamos la configuración en `StudentClient.java`:

```java
@FeignClient(name="msvc-student", url = "localhost:8080/api/student/")
public interface StudentClient {

    @GetMapping("/search-by-course/{idCourse}")
    List<StudentDto> findAllStudentByCourse(@PathVariable Long idCourse);
}
```

De esta manera, el **Gateway** interceptará y redirigirá todas las solicitudes, permitiéndonos manejar la seguridad, control de rutas, y otras configuraciones desde un solo punto.

---

## 15. 🛠️ Configuración del Microservicio ConfigServer

Con **ConfigServer**, centralizaremos toda la configuración de nuestros microservicios en un solo lugar. Esto permite gestionar y actualizar la configuración de todos los servicios de manera centralizada, evitando la necesidad de modificar archivos de configuración individuales para cada microservicio.

### 1️⃣ Configuración del `ConfigServer`

En el microservicio **ConfigServer**, cambiaremos la extensión del archivo de configuración a `application.yml` y añadiremos la configuración para el servidor:

```yaml
server:
  port: 8888

spring:
  profiles:
    active: native # Usa el perfil "native" para leer archivos locales
  application:
    name: microservice-config
  cloud:
    config:
      server:
        native:
          search-locations: classpath:/configurations # Ubicación donde se almacenarán los archivos de configuración de cada microservicio
```

> **server.port**: establece el puerto para **ConfigServer** en `8888`.

> **spring.cloud.config.server.native.search-locations**: indica el directorio de búsqueda (`classpath:/configurations`) donde almacenaremos los archivos `.yml` de configuración de cada microservicio.

### 2️⃣ Creación de Archivos de Configuración en el ConfigServer

Creamos una carpeta `configurations` en `src/main/resources` dentro del proyecto **ConfigServer**. Dentro de esta carpeta, generaremos archivos `.yml` específicos para cada microservicio.

#### Archivo `msvc-student.yml`

1. Creamos `msvc-student.yml` en `configurations/`.
2. Copimos el contenido del archivo `application.yml` del microservicio **Students**, excluyendo la sección `config`.

   ```yaml
   server:
     port: 8090

   spring:
     application:
       name: msvc-student

     datasource:
       driver-class-name: com.mysql.cj.jdbc.Driver
       url: jdbc:mysql://localhost:3306/studentDb
       username: root
       password: # Añade aquí la contraseña si es necesario
     jpa:
       hibernate:
         ddl-auto: create
       database: mysql
       database-platform: org.hibernate.dialect.MySQLDialect

   eureka:
     instance:
       hostname: localhost
       lease-renewal-interval-in-seconds: 5
       lease-expiration-duration-in-seconds: 10
     client:
       service-url:
         defaultZone: http://localhost:8761/eureka
   ```

3. Simplificamos el `application.yml` del microservicio **Students** a:

   ```yaml
   spring:
     application:
       name: msvc-student
     config:
       import: optional:configserver:http://localhost:8888
   ```

#### Archivo `msvc-course.yml`

1. Creamos `msvc-course.yml` en `configurations/`.
2. Copiamos el contenido del archivo `application.yml` del microservicio **Courses**, excluyendo la sección `config`.

   ```yaml
   server:
     port: 9090

   spring:
     application:
       name: msvc-course

     datasource:
       driver-class-name: org.postgresql.Driver
       url: jdbc:postgresql://localhost:5432/courseDb
       username: postgres
       password: # Añade aquí la contraseña si es necesario
     jpa:
       hibernate:
         ddl-auto: create
       database: postgresql
       database-platform: org.hibernate.dialect.PostgreSQLDialect

   eureka:
     instance:
       hostname: localhost
       lease-renewal-interval-in-seconds: 5
       lease-expiration-duration-in-seconds: 10
     client:
       service-url:
         defaultZone: http://localhost:8761/eureka
   ```

3. Simplificamos el `application.yml` del microservicio **Courses** a:

   ```yaml
   spring:
     application:
       name: msvc-course
     config:
       import: optional:configserver:http://localhost:8888
   ```

#### Archivo `msvc-gateway.yml`

1. Creamos `msvc-gateway.yml` en `configurations/`.
2. Copiamos el contenido del archivo `application.yml` del **Gateway**, excluyendo la sección `config`. Además, desactivamos el registro en **Eureka**:

   ```yaml
   server:
     port: 8080

   spring:
     application:
       name: msvc-gateway
     cloud:
       gateway:
         discovery:
           locator:
             enabled: true
         routes:
           - id: students
             uri: http://localhost:8090
             predicates:
               - Path=/api/student/**
           - id: courses
             uri: http://localhost:9090
             predicates:
               - Path=/api/course/**

   eureka:
     client:
       register-with-eureka: false
   ```

   > Nota: Con **`register-with-eureka`**: false le estamos indicando que no se registre a Eureka

3. Simplificamos el `application.yml` del **Gateway** a:

   ```yaml
   spring:
     application:
       name: msvc-gateway
     config:
       import: optional:configserver:http://localhost:8888
   ```

#### Archivo `msvc-eureka.yml`

1. Creamos `msvc-eureka.yml` en `configurations/`.
2. Copiamos el contenido del archivo `application.yml` de **Eureka**, excluyendo la sección `config`:

   ```yaml
   server:
     port: 8761

   spring:
     application:
       name: msvc-eureka

   eureka:
     instance:
       hostname: localhost
     client:
       register-with-eureka: false
       fetch-registry: false
       server-url:
         defaultZone: http://localhost:${server.port}/eureka/
   ```

3. Simplificamos el `application.yml` del microservicio **Eureka** a:

   ```yaml
   spring:
     application:
       name: msvc-eureka
     config:
       import: optional:configserver:http://localhost:8888
   ```

De esta manera, todos los microservicios obtendrán su configuración desde **ConfigServer**, centralizando las configuraciones y facilitando su mantenimiento y actualización.

Con esto, la configuración de **ConfigServer** estará lista y los microservicios podrán acceder a ella de forma centralizada. 🥳

### 16. ✅ Prueba Final del Ecosistema de Microservicios

Con toda la configuración y los microservicios listos, es momento de hacer una prueba final para verificar que nuestra arquitectura funciona de manera fluida y coordinada.

### 1️⃣ 🛠️ Ajuste en la Aplicación de ConfigServer

Antes de levantar los servicios, nos aseguraremos de que **ConfigServer** esté habilitado correctamente.

En el archivo `MicroserviceConfigApplication.java` de **ConfigServer**, añadimos la anotación `@EnableConfigServer` para activar este servidor de configuración.

```java
package com.microservice.config;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.config.server.EnableConfigServer;

@EnableConfigServer
@SpringBootApplication
public class MicroserviceConfigApplication {

    public static void main(String[] args) {
        SpringApplication.run(MicroserviceConfigApplication.class, args);
    }

}
```

> **@EnableConfigServer**: Esta anotación activa el servidor de configuración, permitiendo que otros microservicios obtengan sus configuraciones desde este servicio.

### 2️⃣ 🚀 Levantamiento de los Microservicios en Orden

Para un funcionamiento correcto, iniciamos los servicios en el siguiente orden:

1. **ConfigServer**: Configuración centralizada en el puerto `8888`.
2. **Eureka**: Registro de microservicios en el puerto `8761`.
3. **Students**: En el puerto `8090`, usando **MySQL** como base de datos.
4. **Courses**: En el puerto `9090`, usando **PostgreSQL** como base de datos.
5. **Gateway**: En el puerto `8080` como puerta de enlace.

> ⚠️ **Nota**: Es fundamental que **Eureka** y **ConfigServer** estén funcionando antes de iniciar los demás microservicios, ya que los servicios **Students** y **Courses** dependen de la configuración centralizada y del registro en **Eureka**.

### 3️⃣ 🔍 Verificación del Registro en Eureka

Abrimos **Eureka** en el navegador accediendo a [http://localhost:8761](http://localhost:8761). Verificamos que los microservicios **Students**, **Courses** estén presentes (gateway no aparecerá pues lo hemos desactivado).

### 4️⃣ 📬 Pruebas Finales en Postman

Con los microservicios en ejecución, realizamos las siguientes pruebas en **Postman** para validar la comunicación entre ellos a través del **Gateway** (`localhost:8080`).

1. **Verificación de Cursos**:

   - **Request**: `GET http://localhost:8080/api/course/all`
   - **Resultado esperado**: Una lista de cursos con sus atributos.

   ```json
   [
       {
           "id": 1,
           "name": "Matematicas",
           "teacher": "Profesor A"
       },
       {
           "id": 2,
           "name": "Física",
           "teacher": "Profesor B"
       },
       ...
   ]
   ```

2. **Buscar Estudiantes por Curso en el Microservicio de Students**:

   - **Request**: `GET http://localhost:8080/api/student/search-by-course/1`
   - **Resultado esperado**: Una lista de estudiantes asociados al curso con `idCourse = 1`.

   ```json
   [
     {
       "id": 1,
       "name": "Juan",
       "lastname": "Perez",
       "email": "jua.perez@example.com",
       "courseId": 1
     },
     {
       "id": 4,
       "name": "Ana",
       "lastname": "Martínez",
       "email": "ana.mar@example.com",
       "courseId": 1
     }
   ]
   ```

3. **Verificación del Cliente Feign para Obtener Estudiantes desde Courses**:

   - **Request**: `GET http://localhost:8080/api/course/search-student/1`
   - **Resultado esperado**: Datos del curso `1` junto con la lista de estudiantes inscritos.

   ```json
   {
     "courseName": "Matematicas",
     "teacher": "Profesor A",
     "studentDtoList": [
       {
         "name": "Juan",
         "lastname": "Perez",
         "email": "jua.perez@example.com",
         "courseId": 1
       },
       {
         "name": "Ana",
         "lastname": "Martínez",
         "email": "ana.mar@example.com",
         "courseId": 1
       }
     ]
   }
   ```

> **Nota**: Si aparece un error `500`, revisamos que el `FeignClient` en **Courses** esté configurado para comunicarse a través de **Gateway** en `http://localhost:8080` y no directamente a **Students**.

### 5️⃣ 🎉 El ecosistema de Microservicios Funcional 🎉

El ecosistema de microservicios está ahora completamente operativo y centralizado, con configuración compartida y balanceo de carga a través de **Gateway** y **Eureka**.

# PostgreSQL

Gestor de bases de datos relacionales, orientado a objetos, donde todos los elementos se comportan como objetos, es multisistema, Extensible (compatible con extensiones), escalable y es de licencia libre.

Tabla de Contenido
===
<!--ts-->
   * [Características de Postgres](#características)
   * [Objetos en Postgres](#objetos)
   * [Desplegar](#desplegar)
   * [pgAdmin4](#pgadmin4)
      * [Login](#login)
      * [Añadir Nuevo Servidor](#Añadir-Nuevo-Servidor)
      * [Crear Rol](#Crear-Rol)
      * [Crear Tablespace](#Crear-Tablespace)
      * [Crear Base de Datos](#Crear-Base-de-Datos)
      * [Crear Esquema](#Crear-Esquema)
      * [Crear Tabla](#Crear-Tabla)
      * [Ejecutar SQL](#Query-Tool)
        * [Insertar](#Insertar)
        * [Consultar](#Consultar)
        * [Actualizar](#Actualizar)
        * [Borrar](#Borrar)

<!--te-->

Características
===
## Características principales
* Lenguaje SQL muy próximo al estándar ISO/IEC (es más sencillo portar scripts de otros sistemas de BD)
* Esquemas, tablas heredadas y event triggers
* Soporta datos definidos por el usuario
* Soporte nativo maestro-esclavo
* Escalabilidad vertical

Objetos
===
## Objetos básicos
- **Cluster** - Área de almacenamiento dentro de una instancia.
- **Base de Datos**
- **Esquemas** - Coleciones de tablas
- **Tablespace** - Área de almacenamiento en disco, desde tablas,índices. Se asignan a directorios.
- **Rol** - Entidad que representa a un usuario, grupo o ambos a la vez, pueden ser dueños de bases de datos, tienen permisos sobre ellos o los diferentes objetos. Son colecciones de permisos de objetos.
- **Tabla** - Colecciones de datos relacionales.
- **Vista**
- **Trigger** - Disparador de eventos cuando existen cambios en una tabla.
    - **Event triger** - Actúan cuando una tabla es creada, modificada o borrada.

## Diagrama
![diagrama-postgres](/statics/img/diagrama.png)

Desplegar
===
## Desplegar contenedor de Postgres y Pgadmin

## docker-compose.yml

Posicionarse en el directorio donde se descargó el archivo [docker-compose.yml](https://github.com/ivanNieto13/Manual-PostgreSQL-y-PgAdmin/blob/master/statics/yml/docker-compose.yml) y ejecutar en terminal:
```console
$ docker-compose up -d
```

Esperar a que se descargue la imagen y se generen los contenedores.

## Nota: 
Es **importante cambiar** en el contenedor `postgres` los campos `POSTGRES_USER` y `POSTGRES_PASSWORD`.
Hacer lo mismo en el contenedor `pgadmin` los campos `PGADMIN_DEFAULT_EMAIL` y `PGADMIN_DEFAULT_PASSWORD`.

pgAdmin4
===
## Login

Accedemos a `localhost:5050` desde el navegador.

Escribir las credenciales que se establecieron en el archivo `docker-compose.yml`.

![pgadmin-login](/statics/img/pgadmin/login.png)

Clic en **Login** para iniciar sesión.

Añadir Nuevo Servidor
===
En la sección **Quick Links** hacer clic en **Add New Server**.

![pgadmin-new-server](/statics/img/pgadmin/add-new-server.png)

## Pestaña General
En la pestaña **General** escribir un nombre para la conexión (puede ser cualquiera).

![pgadmin-new-server](/statics/img/pgadmin/create-server.png)

## Pestaña Connection
En la pestaña **Connection** escribir la dirección en donde se encuentra nuestro servidor. En éste caso `localhost`.

Escribir el puerto, en éste caso por defecto es el `5432`.

Escribir el nombre de usuario y contraseña que se estableció en el archivo `docker-compose.yml`.

![pgadmin-new-server](/statics/img/pgadmin/connection-server.png)

Clic en **Save** para guardar cambios.

En el árbol que se despliega en la columna **Browser**, se encontrará ahora la nueva conexión al clúster.
Debajo aparecerán las bases de datos, los roles y los tablespaces que pertenecen al clúster.

Crear Rol
===
Hacer clic derecho sobre **login/group roles** y seguir la ruta **Create** -> **Login/Group Role...**

Asignar un nombre para el nuevo rol en el campo **Name**.

![new-role](/statics/img/pgadmin/new-role.png)

## Pestaña Privilegies
En la pestaña **Privilegies** establecer los privilegios que se quieran asignar a un rol.

![privilegies-role](/statics/img/pgadmin/privilegies-role.png)

Clic en **Save** para guardar cambios.

Crear Tablespace
===
Hacer clic derecho sobre **Tablespaces** y seguir la ruta **Create** -> **Tablespace...**

Asignar un nombre para el nuevo Tablespace en el campo **Name**.

Elegir a quién le pertenece el Tablespace en el campo **Owner**.

![new-tablespace](/statics/img/pgadmin/new-tablespace.png)

## Pestaña Definition
En la pestaña **Definition** escribir la ruta absoluta de la ubicación. En el caso del contenedor `postgres`, se almacenan en `/data/postgres`.

![new-tablespace](/statics/img/pgadmin/new-tablespace_2.png)

Clic en **Save** para guardar cambios.

Crear Base de Datos
===
Hacer clic derecho sobre **Databases** y seguir la ruta **Create** -> **Database...**

Asignar un nombre para la nueva Base de Datos en el campo **Name**.

Elegir a quién le pertenece la Base de Datos en el campo **Owner**.

![new-db](/statics/img/pgadmin/new-db.png)

## Pestaña Definition
En la pestaña **Definition** se puede elegir la codificación de los caracteres, la colación, etc. Por ahora, sólo elegir el Tablespace que se creó.

![new-db_2](/statics/img/pgadmin/new-db_2.png)

Clic en **Save** para guardar cambios.

Crear Esquema
===
Deslplegando el árbol de la Base de Datos que se creó, hacer clic derecho sobre **Schemas** y seguir la ruta **Create** -> **Schema...**

Asignar un nombre para el nuevo Esquema en el campo **Name**.

Elegir a quién le pertenece el Esquema en el campo **Owner**.

![new-schema](/statics/img/pgadmin/new-schema.png)

## Pestaña Default Privilegies

En la pestaña **Default Privilegies** hacer clic en el ícono de agregar (+), elegir el rol en el campo **Garantee** y al hacer clic sobre el bloque en blanco, debajo de **Privileges**, saldrán las diferentes interacciones con los objetos, elegir una por una o todas con **ALL**.

![new-schema_2](/statics/img/pgadmin/new-schema_2.png)

Clic en **Save** para guardar cambios.

Crear Tabla
===

Hacer clic derecho sobre el Esquema y seguir la ruta **Create** -> **Table...**

Asignar un nombre para la nueva Tabla en el campo **Name**.

Elegir a quién le pertenece la Tabla en el campo **Owner**.

Elegir el Tablespace para asignar a la Tabla en el campo **Tablespace**.

![new-table](/statics/img/pgadmin/new-table.png)

## Pestaña Columns

En la pestaña **Columns** hacer clic en el ícono de agregar (+), escribir el nombre de la columna en el campo **Name**, el tipo de dato en el campo **Data type**, si se permite nulo en el toggle **Not NULL?** y si es la llave primaria en el toggle **Primary key?**.

![new-table_2](/statics/img/pgadmin/new-table_2.png)

Clic en **Save** para guardar cambios.

Añadir Llave Foránea
===

## Pre requisito
Para añadir una llave foránea se tendrá que tener al menos dos tablas en un esquema.

Hacer clic derecho sobre la Tabla en donde se creará la llave foránea y hacer clic en **Propiedades** al final del menú desplegable.

![fk_1](/statics/img/pgadmin/fk_1.png)

Seguir la ruta **Constraints** -> **Foreign Key** y hacer clic en el botón **Add new row** (+), después en **Edit row** y por último en **Columns**.

Aquí se eligirá una columna local de la tabla en el campo **Local column**, la tabla a la que se hará referencia en el campo **References** y la columna a la que se hará referencia en el campo **Referencing**.

![fk_2](/statics/img/pgadmin/fk_2.png)

Al terminar, hacer clic en el botón **Add new row**. Y para guardar cambios, hacer clic en el botón **Save**.

Query-Tool
===

Es una herramienta para ejecutar consultas usando la sintáxis SQL de Postgre.

Se compone de un sencillo editor de texto y herramientas para editar, guardar, exportar y ejecutar el código que escriba en él.

Para realizar cualquier operación, hacer clic derecho sobre una Base de Datos y seleccionar **Query Tool** en el menú desplegable.

![query-tool](/statics/img/pgadmin/query-tool.png)

## Insertar

Para realizar un `INSERT` hay que escribir en el editor:

    INSERT INTO esquema."tabla" VALUES (valor-1, valor-n);

![query-tool_2](/statics/img/pgadmin/query-tool_2.png)

Y hacer clic sobre el botón **Execute/Refresh**. O simplemente presionando `F5` en el teclado.

La consola del editor regresará un mensaje de éxito al ejecutarse correctamente el `INSERT`.

![query-tool_3](/statics/img/pgadmin/query-tool_3.png)

## Consultar

Para realizar un `SELECT` hay que escribir en el editor:

    SELECT * FROM esquema."tabla";

![query-tool_4](/statics/img/pgadmin/query-tool_4.png)

Y hacer clic sobre el botón **Execute/Refresh**. O simplemente presionando `F5` en el teclado.

Se mostrará una representación gráfica de la tabla con el resultado de los datos consultados.

![query-tool_5](/statics/img/pgadmin/query-tool_5.png)

## Nota: 
Es posible insertar datos manualmente a la tabla, una vez hecha una consulta.
Sólo hay que hacer clic en el campo vacío de la tabla, escribir el valor y para guardar cambios presionar el botón **Save Data Changes**. O simplemente presionando `F6` en el teclado.

![query-tool_7](/statics/img/pgadmin/query-tool_7.png)

## Actualizar

Para realizar un `UPDATE` hay que escribir en el editor:

    UPDATE esquema."tabla" SET "columna" = 'viejo valor' WHERE "columna" = 'nuevo valor';

![query-tool_8](/statics/img/pgadmin/query-tool_10.png)

Y hacer clic sobre el botón **Execute/Refresh**. O simplemente presionando `F5` en el teclado.

La consola del editor regresará un mensaje de éxito al ejecutarse correctamente el `UPDATE`.

![query-tool_9](/statics/img/pgadmin/query-tool_11.png)

## Borrar

Para realizar un `DELETE` hay que escribir en el editor:

    DELETE FROM esquema."tabla" WHERE "columna" = valor;

![query-tool_8](/statics/img/pgadmin/query-tool_8.png)

Y hacer clic sobre el botón **Execute/Refresh**. O simplemente presionando `F5` en el teclado.

La consola del editor regresará un mensaje de éxito al ejecutarse correctamente el `DELETE`.

![query-tool_9](/statics/img/pgadmin/query-tool_9.png)


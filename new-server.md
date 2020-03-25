# Añadir un nuevo servidor
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
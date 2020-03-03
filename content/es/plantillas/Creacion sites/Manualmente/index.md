---
title: "Creación de Sites # Manualmente"
linkTitle: "Manualmente"
description: "Creación de Sites (Adtopy) de forma manual"
weight: 51
---

Aquí podemos seguir los pasos a seguir para poder **crear y configurar un nuevo Site para Adtopy, de forma manual.**

**Nota:** Tener configurado y funcionando [XAMPP.](https://www.apachefriends.org/download.html) :computer:

### Pasos a seguir: :memo:

1. Copiar path **C:/xampp/htdocs/adtopy/sites/editor** y duplicarlo en C:/xampp/htdocs/adtopy/sites/ (tendremos un __editor copy__ `C:/xampp/htdocs/adtopy/sites/editor_copy`)
2. Cambiar el nombre de __editor_copy__ a **backend** `C:/xampp/htdocs/adtopy/sites/backend`
3. Buscar y reemplazar en archivos dentro de C:/xampp/htdocs/adtopy/sites/**backend**, `namespace sites/editor` a `namespace sites/backend`
4. Comprobar archivos que no hay ninguna llamada al antiguo site __editor__. En Linux fácil con el comando `grep -R namespaces | grep editor`.
5. Limpiar páginas y cosas que no se necesite de C:/xampp/htdocs/adtopy/sites/backend/**pages**.
6. Añadir nueva ruta `backend.adtopy.com` al fichero de xampp de apache: **httpd-vhosts.conf**. En windows está en la ruta: __xampp/apache/conf/extra/httpd-vhosts.conf__

```apacheconf
'xampp/apache/conf/extra/httpd-vhosts.conf'
<VirtualHost *:80>
    ServerName backend.adtopy.com
    DocumentRoot "${projectPath}sites/backend/html"
    php_value include_path ".;${projectPath}install/config"
    RewriteEngine on

    <Directory "${projectPath}sites/backend/html">

    RewriteCond ${projectPath}sites/backend/html/$1 -f
    RewriteRule (.*) $1?site=backend&%{QUERY_STRING} [L]

    RewriteRule .* index.php?site=backend&subpath=$0 [QSA,L]
    Options -Indexes +FollowSymLinks +MultiViews

    # Always set these headers.
    Header always set Access-Control-Allow-Origin "*"
    Header always set Access-Control-Allow-Methods "POST, GET, OPTIONS, DELETE, PUT"
    Header always set Access-Control-Max-Age "1000"
    Header always set Access-Control-Allow-Headers "x-requested-with, Content-Type, origin, authorization, accept, client-security-token"

    # Added a rewrite to respond with a 200 SUCCESS on every OPTIONS request.
    RewriteCond %{REQUEST_METHOD} OPTIONS
    RewriteRule ^(.*)$ $1 [R=200,L]
    </Directory>
</VirtualHost>
```

7. Añadir nueva ruta `backend.adtopy.com` al fichero de host de Windows **host**. En windows está en la ruta: __C:/Windows/System32/drivers/etc__

```markdown
'C:/Windows/System32/drivers/etc/host'

    127.0.0.1 statics.adtopy.com
    127.0.0.1 reflection.adtopy.com
    127.0.0.1 editor.adtopy.com
    127.0.0.1 metadata.adtopy.com
    127.0.0.1 backend.adtopy.com
```

8. En la BBDD de **mysql**, dentro de la `tabla adtopy`, añadir el nuevo ID para el nuevo site **backend** dentro de la tabla `websites`. Se puede meter a mano el valor o mediante un fichero .sql:
    > 1.- Importando .sql ubicado en: `~/adtopy/install/mysql/backend/site_backend.sql`

    > 2.- Insert into manual para nuevo site:

```sql
INSERT INTO `websites` (`id_site`,`host`,`canonical_url`,`hasSSL`,`namespace`,`websiteName`) VALUES (null,'backend','http://backend.adtopy.com',0,'backend','Backend');
```

9. Mismo paso que el anterior, pero para meter datos asociados al nuevo site `backend`. Se puede meter a mano el valor o mediante un fichero .sql en la tabla `page`:
    > 1.- Importando .sql ubicado en: `~/adtopy/install/mysql/backend/pages_backend.sql`

    > 2.- Insert into manual para nuevo site:

```sql
INSERT INTO `page` (`id_page`,`tag`,`id_site`,`name`,`date_add`,`date_modified`,`id_type`,`isPrivate`,`path`,`title`,`tags`,`description`,`role`) VALUES (null,'index',5,'Index',NULL,NULL,1,0,'index','titulo','tags','desc',NULL);
INSERT INTO `page` (`id_page`,`tag`,`id_site`,`name`,`date_add`,`date_modified`,`id_type`,`isPrivate`,`path`,`title`,`tags`,`description`,`role`) VALUES (null,'error',5,'Error',NULL,NULL,1,0,'error','Error',NULL,NULL,NULL);
INSERT INTO `page` (`id_page`,`tag`,`id_site`,`name`,`date_add`,`date_modified`,`id_type`,`isPrivate`,`path`,`title`,`tags`,`description`,`role`) VALUES (null,'Job',5,'Job',NULL,NULL,1,0,'Job','Job',NULL,NULL,NULL);
```

10. Probar a entrar en el nuevo site creado y ver que todo funciona correctamente: [backend.adtopy.com](http://backend.adtopy.com/)

Si has seguido todo los pasos, **genial, has configurado un nuevo site de forma manual** :tada:

Si por el contrario has tenido o hay algúne error en la documentación, crea una nueva petición (issue) (sidebar derecho el enlace a github del proyecto)
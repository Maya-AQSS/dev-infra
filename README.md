# dev-infra

Infraestructura global para el desarrollo con Maya AQSS

> [!WARNING]
> Esta infraestructura está pensada para entornos de desarrollo. NUNCA debe ser utilizada en entornos de producción.

## Instalación y configuración

1. Creas una carpeta llamada `maya-aqss`.

2. Clonar el repositorio dentro de la carpeta `maya-aqss`.

   ```bash
   $ git clone git@github.com:Maya-AQSS/dev_infra.git 
   ```

3. Entrar en la carpeta `dev-infra` .

   ```bash
   $ cd dev-infra 
   ``` 

4. Copiar los ficheros `.env-example-maya` y `.services-example-maya` a `.env` y `.services` respectivamente

   ```bash
   $ cp .env-example-maya.env
   $ cp .services-example-maya .services
   ```

   > [!TIP]
   > En la mayor parte de los casos los ficheros ya vendrán configurados correctamente y solo sería necesario el paso 4

5. Configurar los repositorios externos. Para ello modificar el fichero `.repos`. 

   ```text
   # ruta del repo (usuario/repositorio.git) | https o ssh
   Maya-AQSS/maya_dashboard.git | ssh
   ```

   > [!CAUTION]
   > En este fichero se incluyen aquellos repositorios que son arrancados en el ecosistema _Maya AQSS_ pero que NO son módulos de Odoo.

   > [!NOTE]
   > Se da por hecho que todos los repositorios se encuentran en _github_. En caso de querer codificar es recomendable realizar la clonación con _ssh_

   > [!IMPORTANT]
   > Todos los repositorios deben tener una rama develop. La instalación realiza un _checkout_ automático a ese rama.

6. Asignar permisos de ejecución para el usuario a los scripts

   ```bash
   $ chmod u+x up.sh create-module.sh up.sh start-maya.sh stop-maya.sh remove-infra.sh clone-repos.sh
   ```

7. Añadir el submódulo de servicios adicionales

   ```bash
   $ git submodule add -f https://github.com/Maya-AQSS/odoodock-additional-services '[ads]'
   ```

8. Entrar en la carpeta `[ads]` y copiar los ficheros .env-example y .services-example a .env y .services respectivamente

   ```bash
   cd \[ads\]/ 
   cp .env-example .env
   cp .services-example .services
   ```

9. Configurar los servicios extra (`.env`) e indicar cuales se desa arrancar (`.services`).

   > [!TIP]
   > En la mayor parte de los casos los ficheros ya vendrán configurados correctamente y solo sería necesario el paso 3

## Arranque

El sistema arranca con el comando `start-maya.sh`

```bash
$ ./start-maya.sh
```

## Parada

El sistema para con el comando `stop-maya.sh`

```bash
$ ./stop-maya.sh
```

## Reinicio

En el caso de que exista algún problema en la infraestrutura, es posible utilizar el comando `remove-infra.sh` para eliminar volúmenes, datos, redes, elementos huérfanos, etc

```bash
$ ./remove-infra.sh
```

> [!CAUTION]
> Este comando elimina todos los datos. Usalo con cabeza.

## Generación de API-KEYS

La instalación de Odoo puede generar API-KEYS para usuarios (aplicaciones) que conecten con _Odoo_ vía controlador. El usuario asociado a la aplicación estará configurado con el nombre de la aplicacion (_NOMBRE_) y como login y email _NOMBRE_app@internal_, donde NOMBRE es el nombre de la aplicación

Es posible ver las key generadas y sus fechas de caducidad desde el host en la carpeta _./.server-info/secrets_.

> [!IMPORTANT]
> La key generadas tienen una fecha de caducidad de 3 meses. Es importante utilizar la solicitud de renovación de keys para poder seguir trabajando.


## Secreto cliente Odoo19-sso

> [!CAUTION]
> Es necesario copiar el secreto generado por _keycloak_ para el cliente _odoo10-sso_ dentro de odoo o no será posible autenticarse desde Odoo

1. En Keycloak. 

`Realm CEED -> Clients -> odoo19-soo -> credentials -> client secret (copy)`

2. En Odoo. Activar el modo debug

`Ajustes -> Usuarios y compañias -> Proveedores OAuth -> keycloak`

Pegar en _Secreto del cliente_ el secreto obtenido en _keycloak_.


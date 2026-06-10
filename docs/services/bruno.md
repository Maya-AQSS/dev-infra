---
layout: page
title: bruno
subtitle: Servicios disponibles
menubar: services_menu
show_sidebar: false
hero_height: is-fullwidth
---

## bruno-test 

_Bruno_ es un cliente de API de código abierto diseñado para construir, documentar y probar interfaces de programación de aplicaciones (API). Funciona como una excelente alternativa a herramientas tradicionales como _Postman_.

### Creación de test

Las colecciones de test se crean en cada uno de los módulos. Por ejemplo, si en tenemos un módulo llamado _M1_, situado en `../addons/M1`, las colecciones de test se almacenan en una carpeta llamada `api_test`

```text
  ../addons/M1/api_test
                │
                ├ coleccion1
                │      │
                │      ├ environments
                │      │       │
                │      │       └ env.bru
                │      │       
                │      ├ 01.bru 
                │      ├ 02.bru 
                │      ├ bruno.json
                │      └ collection.bru
                │
                └ coleccion1

``` 

### Ejecución de test

La ejecución de los test se realiza desde dentro del contendor:

```bash
docker exec -it odoodock-bruno-tests-1 sh
$ cd /tests/addons/M1/api_test/coleccion1
$ bru run --env-file ./environments/env.bru
```


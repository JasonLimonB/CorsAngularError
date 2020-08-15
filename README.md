## Problema de CORS con un Servicio REST en local

Antes de comenzar cabe mencionar que esto solo para porblema de los cors en mi localhost ya que tengo mi aplicacion de ront end en Angular y mi Back end en Srping boot

[Front end](https://github.com/JasonLimonB/AngularCRUD)

[Back end](https://github.com/JasonLimonB/BackednSpringboot)

## El problema

El problema es que al conectarme para una peticion get a mi api me arroja un error de bloqueo de cors.
Esto se hace por seguridad, pero como yo solo quiero practicar tuve que hacer esta cierta confguración.

Esto es una solucion para nuestro proyecto de Angular
1.- Crear un fichero nuevo dentro de src con el nombre de "proxy.conf.json" y poner la siguiente 
Tambien podemos utilzar "/api/*", ya que a mi me funciono con doble * pero tambien funciona con api en vez de *
y los parametros de tu localhost y el puerto es dependiendo a tus necesidades.

```json
{
    "/*/*": {
        "target": "http://localhost:8080",
        "secure": false,
        "logLevel": "debug"
    }
}
```
O tambien usar:
```json
{
    "/api/*": {
        "target": "http://localhost:8080",
        "secure": false,
        "logLevel": "debug"
    }
}
```

2.- Nos dirigimos a nuestro archivo "package.json" y justo donde esta la propiedad start agregamos lo siguiente

```json
{
    "start": "ng serve --proxy-config proxy.conf.json",
}
```

3.- Ahora nos dirigimos a nuestro archivo "Angular.json" y donde esta la propiedad serve, esto puede varia en la linea de codigo pero si el proyecto es nuevo probablemente esta en la linea 68 y dentro de este hay otra propiedad de options el cual vamos agregar algo la opcion de "proxyConfig".
```json
{
    "options": {
            "browserTarget": "AngularCRUD:build",
            "proxyConfig": "src/proxy.conf.json"
          },   
}
```

Y ya solo queda detener el servidor de desarrollo y volver a iniciar para poder ver los cambios. 

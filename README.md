# Tutorial de OpenSCAD


## Introducción

OpenSCAD es un programa CAD (Computer Aided Design o Diseño asistido por ordenador) en 3D. La característica principal es que OpenSCAD *no se maneja usando el ratón* sino por medio de un lenguaje. Esto que a primera vista parece mucho más incómodo se vuelve en realidad mucho más potente cuando queremos construir estructuras repetitivas.

OpenSCAD tiene versiones para los principales sistemas operativos: Windows, Mac y Linux y no necesita instalación: puede descargarse un ZIP, descomprimirlo y simplemente ejecutar el programa

## Primeros pasos

Al ejecutar el programa veremos algo como esto:

![Ventana inicial](capturas/01-inicio.png)

Aunque nosotros crearemos un proyecto nuevo vacío pulsando el botón "Nuevo", OpenSCAD ofrece algunos ejemplos creados y que nos permiten ver algunas de las capacidades. Despues de crear un nuevo proyecto, veremos algo como esto:

![Interfaz de OpenSCAD](capturas/02-interfaz.png)

### Descripción del interfaz

* En la parte izquierda podremos escribir la descripción de nuestros modelos.
* En la parte central, arriba, podremos ver unos ejes de coordenadas:

    * Observa el eje de las X, está en rojo y apunta hacia la derecha: esto significa que en principio, los valores positivos de X crecen en ese sentido.
    * El eje de las Y apunta "hacia el interior de la pantalla", en diagonal.
    * El eje de las Z apunta hacia arriba.
* En la parte central, abajo, veremos un panel llamado "Consola", nos permitirá ver el proceso que sigue OpenSCAD al construir nuestros modelos, incluyendo los errores que cometamos.
* En la parte central, derecha, veremos los errores que cometamos y el punto exacto donde los hemos cometido.
* En la parte derecha, veremos un panel llamado "Customizer" que nos permitirá modificar algunas opciones, en este tutorial *no lo usaremos*

### Un primer modelo

Escribe en la parte izquierda el siguiente código::

    cube ([12, 3, 4])

Pulsa despues F6 y verás algo esto:

![Un primer modelo OpenSCAD](capturas/03-primer-modelo.png)

Si dejas pulsado el botón principal del ratón y "arrastras" el escenario, podrás cambiar el punto de vista. Si usas la rueda del ratón podrás cambiar la escala del modelo. Usa ambas posibilidades para explorar el modelo desde todos los puntos de vista.

## Elementos básicos del lenguaje

Todo el lenguaje se basa en estas estructuras, presta especial atención a los puntos y comas:

    //Construye un objeto
    objeto();

    //Asigna un valor a una variable
    variable=valor;

    //Un operador modifica algo, una acción realiza una tarea
    operador() accion();

    //Se pueden encadenar operadores
    operador() operador() accion();

    //Si queremos aplicar un operador
    //a varias acciones a la vez
    operador() { accion(); accion(); }

## Valores y vectores

En una variable podemos almacenar números y textos. Si necesitamos trabajar con varios valores a la vez, se usan vectores, que van entre corchetes::

    altura=10.2;
    nombre="Modelo A1";
    coordenadas=[12, 3, 4];

Es frecuente usar los vectores con coordenadas. De hecho, nuestro modelo inicial usaba las coordenadas x=12, y=3, z=4

## Objetos: cubo

Podemos crear cubos de dos maneras::

    //Esto pone un cubo poniendo una esquina
    //en la coordenada [x=0, y=0, z=0] y la 
    //esquina opuesta en [12, 3, 4]
    cube( [12, 3, 4] );

    //Esto pone el "centro del cubo" 
    //en la coordenada [x=0, y=0, z=0] y 
    //hace que el cubo mida 12 en el eje X,
    //3 en la y y 4 en la z
    cube( [12, 3, 4], center=true);

![El mismo modelo centrado](capturas/03a-primer-modelo-centrado.png)

Si combinamos este proceso con variables, podemos hacer cosas como esta::

    ancho_x=12;
    alto_z=4;
    profundo_y=3;
    cube( [ancho_x, profundo_y, alto_z], center=true);

Esto produce **exactamente el mismo resultado** pero esta forma de trabajar nos resultará útil más adelante.

## Operadores: traslación

Es posible hacer que un objeto se traslado a otro punto del espacio usando ``translate([x, y, z])``. Por ejemplo, hagamos esto::

    //Esta parte es igual que la anterior
    ancho_x=12;
    alto_z=4;
    profundo_y=3;
    cube( [ancho_x, profundo_y, alto_z], center=true);

    arista_cubo=3;
    //Observa que esto es una sola línea
    translate([0, 0, profundo_y]) 
        cube ([arista_cubo,arista_cubo,arista_cubo], center=true);

    //Y esto es también una sola línea
    translate([0, 0, profundo_y+arista_cubo]) 
        cube ([ancho_x, profundo_y, alto_z], center=true);

Deberías ver algo como esto:

![Pieza en H](capturas/04-h.png)

Observa ahora el potencial de usar las variables. Vamos a modificar el ancho de las barras horizontales y pondremos ``profundo_y`` a 6 (omitimos los comentarios por brevedad)::

    ancho_x=12;
    alto_z=4;
    profundo_y=6;
    cube( [ancho_x, profundo_y, alto_z], center=true);

    arista_cubo=3;
    translate([0, 0, profundo_y]) 
        cube ([arista_cubo,arista_cubo,arista_cubo], center=true);

    translate([0, 0, profundo_y+arista_cubo]) 
        cube ([ancho_x, profundo_y, alto_z], center=true);

# Programando un juego de adivinar

Nada mejor para continuar nuestra aventura y seguir aprendiendo que ponernos manos a la obra!
El siguiente gran clásico de los lenguajes después del `Hello, world!` es el `Guessing Game`. Se trata de programar un sencillo juego que corre en línea de comandos con el cuál introducir al estudiante nuevos conceptos cómo variables, funciones y métodos, paquetes/dependencias y sintáxis propia del lenguaje.

## Instrucciones

Esto funciona de la siguiente manera: el programa genera un número entero aleatorio o `random` entre 1 y 100. Luego le pide por pantalla al usuario que introduzca un número en ese rango, con el objetivo de intentar adivinar el número que ha sido generado. Si el número del usuario es muy bajo o muy alto, irá indicando tal situación, hasta en el momento en el que acierte, con lo cuál se imprimirá un mensaje de felicitación y se finalizará el programa.

## Preparativos

Lo primero será configurar un proyecto nuevo. Tal y como vimos anteriormente, usaremos `cargo` para tal efecto.

```
$ cargo new quessing_game
$ cd guessing_game
```

Ahora miraremos dentro del archivo `Cargo.toml` y editaremos la información que Cargo no haya obtenido de nuestro entorno correctamente.

```
[package]
name = "guessing_game"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
edition = "2018"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
rand = "0.6.0"
```

Si recordáis, Cargo genera un archivo main.rs dentro de la carpeta `src`. Abrimos el archivo *.rs y dentro comprobamos como Cargo ha generado dentro de este archivo el programa Hello, world!. Para asegurarnos que todo funciona bien, ejecutaremos en nuestra terminal (o desde nuestro editor de código favorito) el comando `cargo run`. Si obtenemos un Hello, world! es que todo funciona y está listo.


## Escribiendo el código

Borraremos el contenido e insertaremos el siguiente código:

```
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..101);

    loop {
        println!("Please input your guess.");

        let mut guess = String::new();

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```
### El análisis

Woooo! Quieto parado! Esto es demasiado... nah, que va. Está todo en orden. Vamos a echar un vistazo línea a línea y veréis como todo concuerda.

```
use std::io;
use rand::Rng;
```

Para poder obtener la información que introduzca el usuario por consola, necesitamos 'llamar' a la [librería](https://github.com/Pyzyryab/rustlang-es/tree/main/01.%20Iniciaci%C3%B3n/03.el_preludio) librería `io`, la cuál se encuentra en la librería standard.
De la misma manera importaremos `Rng`, el cuál se encargará de escoger aleatoriamente el número que debe de adivinar el usuario.

`fn main() { ` recordad, 'main' siempre es el punto de entrada a cualquier programa Rust. La llave `{` indica el comienzo del cuerpo de la función, el cuál cerraremos cuando hayamos acabado de escribir nuestro código con un  `}`.

```
    println!("Guess the number!");

    println!("Please input your guess.");
```
Llamamos a la macro `println!` para que nos imprima en pantalla la información que queremos transmitir al jugador, en este caso, imprimimos mensajes pidiéndole que introduzca un número para intentar adivinar cual ha generado el programa.

### Guardando valores en 'variables'

Bien, ahora vamos a crear un lugar dónde almacenar en memoria el número que ha introducido el usuario, de la siguiente manera:

``` let mut guess = String::new(); ```

Antes de nada, una variable (para aquellos que de verdad se estén iniciando con Rust) es el nombre que se le da a un lugar concreto en memoria que se designa para guardar un dato necesario para el desarrollo del programa. En Rust el concepto de variable difiere un poco de el del resto de lenguajes... pero a grandes rasgos siempre vamos a poder pensar en las variables como cajas en dónde guardamos datos, y en su nombre o referencia como en una etiqueta pegada en esa caja que nos indica como referirnos a ella.

La palabra reservada `let` se usa en Rust para designar variables. Toda variable ha de ir precedida en tiempo de creación por la palabra let. 
Rust trabaja dos tipos de variables, inmutables y mutables. En este caso, ya que es algo que discutiremos más adelante, usaremos `mut` para hacer a nuestra variable 'mutable' y acercarla al concepto clásico de variable en programación informática.

```
let number = 5; // variable immutable
let mut number = 5; // variable mutable
``` 

Vale, así que `let mut guess` introduce una variable, el sitio donde vamos a guardar el número que introduce el jugador. Nos encontramos con el operador `=` el cual es un operador de asignación, y esto es muy importante, ya que no iguala ni compara (para eso se usa el operador `==`) si no que asigna a lo que creamos a la izquierda de la expresión, a lo que tenemos a la derecha, lo que es el `valor` de nuestra variable, el cuál es el resultado de llamar a `String::new()` el cual crea una nueva instancia `String`, el cual no es más que un tipo de datos que representa caracteres. De eso se encarga `::new` el cual es una función asociada a dicho String. `::` indican que a continuación será llamada dicha función asociada.

En resument, `let mut guess = String::new();` ha creado una variable mutable la cual apunta a un hueco reservado (o inicializado) que contiene una nueva instancia de un String!

### Leyendo los datos de entrada

Una vez ahora hemos preparado un hueco para poder almacenar el dato que introduzca el jugador, es hora trabajar con él. Para ello llamaremos a la función `stdin()` del módulo que previamente hemos importado al principio del archivo.

```
io::stdin()
    .read_line(&mut guess)
```

Si no hubieramos importado `std:io` aún podríamos haber escrito la llamada a esa función como `std::io::stdin`. De cualquie manera, es una buena práctica el declarar los `scopes` más globales y de mayor uso a lo largo del código para hacer este lo más claro y más conciso posible.

Luego, con la notación del punto, llamamos al método `read_line` (un método es un primo hermano de una función, pero que peternece a un objeto en particular) y le pasaremos como argumento la variable que antes declaramos `guess`. Aqí estamos cargamos nuestra función `read_line` con la variable en la que guardaremos la entrada que nos de el jugador, de manera que como escribiremos algo nuevo dentro de ella, como la vamos a cambiar, necesitamos pasarla como `mut` en vez de como `&guess`.
El operador `&` simplemente hace una 'referencia' a esa variable. No os detengáis en la sintáxis, hablaremos de ella pronto. 


### Manejando errores

Por útlimo en esta parte, nos queda `.expect("Failed to read line");`. Para no entretenermos mucho, recordad que con la anterior línea leíamos la entrada dónde el jugador ponía su número y la guardamos en nuestra variable, pero también nos devuelve por defecto un valor, llamado `io:Result`. Toda instancia de **Result** tiene un método llamado `.expect()`. 
Si `read_line` devuelve un error o `Err`, debemos de manejar ese error para que no rompa nuestro programa, y dicho método nos facilita esa labor, imprimiendo además un mensaje designado por el programador dentro de sus paréntesis.

### Imprimiendo en pantalla.

``` println!("You guessed: {}", guess); ```.
Aquí sólo nos queda deternos a hablar de los `placeholders: {}` o corchetes de formateo. Ellos se encargan de simplemente reservar ese hueco para algún valor que pasaremos a continuación, en este caso después de la coma, nuestra variable `guess`, la cuál su valor será introducido luego en el sitio de los placeholder. Es una manera rápida y eficiente de mezclar valores de variables con caracteres, ya que todo lo que va dentro de los `"` de un String se trata como caracter, luego si insertamos una variable dentro a palo seco el compilador pensará que se trata de un caracter, y no de un valor de variable. 

Por ejemplo:

```
let x = 5;
let y = 10;

println!("x = {} and y = {}", x, y);
```

Ese código imprimirá `x = 5 and y = 10`.

### Usando crates externos

Ahora generaremos el número aleatorio por parte de nuestro programa, y lo haremos a través de un `crate` externo, el crate `rand`.
Antes de nada, necesitamos indicar que usaremos un crate externo, y no vale con importarlo sólo al principio de programa, tenemos que decirle a nuestro compilador que 'dependemos' de ese archivo es nuestro código, y que necesitamos de él. Para ello, abrimos el archivo `Cargo.toml` y añadimos:

```
[dependencies]
rand = "^0.5.5"
```

Esto hará que a la hora de compilar el código, cargo descargará, compilará e instalará todo lo que necesitemos para usar dicha librería externa.


### Generando el número aleatorio

Ahora que tenemos nuestro crate capaz de generar números aleatorios en nuestro código, vamos a ello.

```let secret_number = rand::thread_rng().gen_range(1, 101);```

Declaramos una variable con la palabra reservada `let` dónde almacenar dicho número, que en este caso la llamaremos `secret_number`.

Al otro lado del operador de asignación `=`, tenemos la función `rand::thread_rng()`, la cual nos brinda un generador de números. A continuación, llamámos al método 
`.gen_range()` y generará dicho número pasándole como argumentos dos números, de los cuales él generará un número aleatorio comprendido en el rango interno de los valores provistos, en este caso un número entre 1 y 100. No incluye el límite superior, por lo que para generar entre 1 y 100 necesitamos indicarle `.gen_range(1, 101)`.


### Comparando los números

```
    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }

```

`match` es la palabra clave aquí. Lo que hace match (a *grosso modo*) es comprobar coincidencias, y ejecutar código según la coincidencia establecida. 
Es muy parecida a la sentencia `switch` en otros lenguajes, y es una manera rápida de sustutuír el flujo que podrías hacer con `if/else` de manera mucho más tediosa.

He aquí un ejemplo:

```
fn main() {
  let numero = 1;

  match numero {
    1 => println!("Uno"),
    2 => println!("Dos"),
    3 => println!("Tres"),
    _ => println!("Sin coincidencias."),
  }
}
```

En este caso, match comparara el valor de la variable número con lo que le pasemos en los operandos de la izquierda, y si coincide, ejecutará el código a la derecha del operador 
`=>`. También nos permite designar un caso en el que ejecute código si **no** tiene coincidencias, como en `_ => println!("No hay coincidencias")`, en dónde `_` representa un placeholder que indica precisamente que no hay coincidencias.

Bien, en nuestro ejemplo, `match guess.cmp(&secret_number)`, dónde `guess` representa el valor del usuario, `&secret_number` es el número generado por la máquina y `.cmp` es un método que al llamarlo compara dos valores cualquiera siempre que sean comparables. `Ordering` (el cual traemos al 'scope' a través de `use`), es un tipo de que se encarga de proveer la lógica que lleva a los resultados. 

En resumen, con `match` definimos que hacer en las situaciones previstas, con `.cmp` comparamos el valor de las dos variables y nos devuelve el resultado en un `Ordering`, el cual es el que almacena el valor de esa comparación.

### Manejando la entrada del usuario

El siguiente bloque de código es el encargado de asegurarse que el usuario ha introducido un número, y no nos está trolleando el programa, así que para evitar dicha situación, a continuación escribiremos:

```
let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

```

Si recordáis guardamos la entrada del usuario como un String. Este tipo de datos se usa para representar carácteres. Rust es un lenguaje estática y fuertemente tipado, por lo que el programa fallaría al comparar el número del jugador con el de la máquina ya que por definición no podemos comparar valores de tipos distintos. La solución es trivial, como suponemos que el usuario jugará acorde al juego e introducirá un número, convertiremos el String a número, y por si acaso la entrada no es un número, aprovecharemos a corregir esa situación. 

Cogemos nuestra anterior variable y la modificamos un poco. Este concepto es muy delicado en Rust, ya que no se trata de sobreescribir el valor anterior, si no de hacerle `shadow`.Parecido, pero no igual. Dejémoslo ahora en que tenemos herramientas para cambiar la anterior variable y más adelante profundizaremos en ese concepto. 

A través de `:` definimos que queremos que el tipo de dato que queremos almacenar sea un tipo numérico entero de 32 bits. En resumen, un número por ahora. A la derecha del `=` proponemos el cambio. 

`.trim()` lo que hace es eliminar de nuestra variable guess carácteres no deseados. En este caso, cuando ejecutamos `.read_line()` el usuario introduce un carácter numérico pero ha de presionar `ENTER`, con lo que automáticamente un `\n` es añadido al String, con lo que de esta manera si el usuario introduce `10` nos quedaría sólo los caracteres que representan ese número. 
El método `.parse()` se encarga de convertir (si puede) cualquier string en un número. Para ello, en caso de que no sea capaz de convertirlo, envolvemos toda la operación en la sentencia match, el cual nos dejará elegir que hacer según lo que nos devuelvan los dos métodos. `.parse()` devuelve al igual que `.read_line()` un tipo `Result`, en este caso, con dos variantes: si lo puede convertir devuelve `Ok` junto con el número convertido, si no, devolverá un `Err()` con más información acerca del error. Como nuestra intención es capturar la fuente del error, usamos el `_` como argumento del error indicándole que todo lo que no haga match con `Ok`, será un `Err`.

### Looping y continue

Si en el anterior apartado `.parse()` no consigue convertir a número la entrada, sabemos que devolverá un `Err()`, con lo que como nuestra intención es tener una entrada válida indicamos que queremos seguir dentro del programa con la sentencia `continue`. Esto implica que aunque encuentre un error, siga en código.

La cosa es, cómo debería de seguir? El objetivo del juego es tanto que introduzca algo válido en la entrada cómo no, hemos de seguir preguntándole al usuario hasta que consiga acertar. Si introduce una entrada válida se le orientará si su intento ha estado por debajo o por encima en valor del número secreto, y si introduce algo que produzca un error se le volverá a pedir que introduzca un número. 

Para ello, encerraremos la parte del proceso desde la que le pedimos que introduzca el número hasta que le indicamos cómo de cerca o ha estado o si ha acertado; para ello, utilizaremos un bucle. Esa parte del código se repetirá una y otra vez hasta que se satisfaga una condición. En este caso, nuestra intención es jugar hasta que se acierte el número secreto, por lo que usaremos un bucle infinito definito a través de la palabra reservada `loop` y encerraremos entre llaves el código que necesitamos repetir, y usaremos la sentencia `break` en dónde deseemos terminar nuestro bucle y finalizar el programa, en este caso...

```
loop {
        println!("Please input your guess.");

        let mut guess = String::new();

        io::stdin()
            .read_line(&mut guess)
            .expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
            Ok(num) => num,
            Err(_) => continue,
        };

        println!("You guessed: {}", guess);

        match guess.cmp(&secret_number) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");  
                break; // Cómo los números son iguales, queremos finalizar nuestro programa, ya que hemos cumplido con el objetivo!
            }
        }
    }
```

### Objetivo cumplido

Y por fin, podemos ejecutar `cargo run` y jugar a nuestro `guessing game`. 

Se que es una explicación larga, se qué se ve difícil la sintáxis y las 'cosas' propuestas hasta ahora, pero es sólo es una introdución al lenguaje con el objetivo de ver un programa finalizado y jugar con él, a la vez que vemos conceptos nuevos. 

No os desaniméis, ya que esto sólo es como ver el 'trailer' de una peli, para ir ejercitando dedos y neuronas, ya que ni mucho menos alguien que está empezando debería de saber hacer casi nada de lo que hemos escrito, y poco a poco iremos escalando la curva de aprendizaje hasta convertirnos en unos magníficos desarrolladores de Rust! Todo principio es complicado, pero habéis de confiar en vosotros y superaros día a día a vosotros mismos!

Enhorabuena por haber llegado hasta aquí, sóis grandes! Nos vemos en el siguiente capítulo :)


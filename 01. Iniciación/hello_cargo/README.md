# Hello, Cargo!

Cargo es un compilador y administrador de paquetes el cuál viene incluído en la instalación base de Rust.
Es ampliamente usado en la comunidad `Rust` y por los `Rustaceans` (nombre autoacuñado por los usuarios del lenguaje) ya que hace un montón de cosas por ti, entre ellas compilar tu código y correlo, descargar librerías y craftearlas, manejar tus dependencias, generar documentación...

## Versión de Cargo

La mejor manera de saber si tenemos Cargo disponible en nuestro sistema es abriendo una terminal (en cualquier OS) y tecleando algo tan simple como `cargo --version`.
Si nos devuelve un número de versión significa que Cargo está listo para ser usado! 

Por ejemplo, si todo está correcto, debería devolvernos la salida del comando algo de este estilo:
```
cargo 1.48.0 (65cbdd2dc 2020-10-14)
```

## Creación de un nuevo proyecto

Iniciar un proyecto con Cargo es la mejor manera de mantener bien organizado tu código desde el minuto uno, y de preparar dicho proyecto para que se 'buildee' de una manera exitósa a la par que sencilla.
Simplemente, navega a cualquier directorio dónde desees almacenar tu código Rust y escribe lo siguiente:
```
$ cargo new hello_cargo
$ cd hello_cargo
```

- El primer comando crea un nuevo directorio llamado `hello_cargo`. En este directorio se construirá tu nuevo proyecto Rust, y siempre llevará por nombre lo que le pases como argumento a `cargo new [proyect name]`. 

- Entra al directorio. Verás que se ha creado un directorio llamado `src` el cual continene dentro un archivo `main.rs`. Este directorio es el indicado para poner dentro nuestros archivos de código!

- Por otra parte, también te habrás fijado que se ha creado un archivo llamado `Cargo.toml` (del tipo Tom’s Obvious, Minimal Language). Este archivo se encarga de encapsular los datos de tu proyecto, conteniendo y manejando la información del mismo desde ahí y de manejar las dependencias. Las dependencias son paquetes de código de los cuales depende tu código para funcionar correctamente. En Rust, los paquetes de código se les llama `crates`.

- Por último, Cargo automáticamente inicia un repositorio Git (salvo que corras el comando `cargo new` dentro de un directorio Git ya inicializado).

Si miras dentro del archivo `main.rs` verás que Cargo ha generado automáticamente un `Hello, world!` como el que hicimos en el primer tutorial para nosotros.
Esta es la manera que tiene Cargo de configurar un proyecto y decirte que todo esta listo para funcionar. 

Aprovechando antes de que cierres el archivo, vamos a modificarlo un poco para empezar a jugar con el lenguaje. Vamos a hacer que nos devuelva en este caso, un simple saludo a Cargo, guardando este nombre en una variable y pasándolo a dentro de nuestra macro en forma de placeholder.
```
fn main() {
    let greet_name = "Cargo";
    println!("Hello, {}!", greet_name);
}
```

Con esto tenemos nuestro proyecto estructurado. Cargo confía en que el directorio principal, en este caso el `hello cargo` lo dejes para los archivos README.md, licencias y demás cosas relacionadas con el 'standard' de repositorios y creación de proyectos de hoy en día, mientras que el directorio `src`sea el que se encargue de contenter todos los archivos relaciondos con tu código. De esta manera, nos aseguramos seguir siempre una estructura, ser más eficientes a la hora de diseñar y estructurar proyectos mientras que podemos desenvolvernos correctamente en otros repositorios cuando leamos sus archivos a la par que hacemos más fácil que otros desarrolladores encuentren lo que buscan en el nuestro.

## Compilar y ejecutar un proyecto en Cargo

Desde tu directorio `hello_cargo`, ejecutaremos el comando `$ cargo build`. 
```
C:\Users\Alex\Desktop\Rust\rustlang-es\01. Iniciación\hello_cargo>cargo build
   Compiling hello_cargo v0.1.0 (C:\Users\Alex\Desktop\Rust\rustlang-es\01. Iniciación\hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.70s
```

Esto creará un nuevo directorio llamado target. Para no extendernos mucho, para correr nuestro código simplemente nos movemos dentro del directorio y ejecutamos el archivo 
`main.exe`.
```
$ .\target\debug\hello_cargo.exe # or ./target/debug/hello_cargo on Linux.
Hello, Cargo!
```
En nuestra terminal vemos el saludo `Hello, Cargo` que nos confirma que todo el proceso se ha ejecutado correctamente.

## Todo en un paso

Cargo puede compilar y ejecutar en un solo paso lo que le pidamos con el comando `cargo run`. De esta manera, el proceso anterior desde el directorio `hello_cargo`:

```
C:\Users\Alex\Desktop\Rust\rustlang-es\01. Iniciación\hello_cargo>cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.02s
     Running `target\debug\hello_cargo.exe`
Hello, Cargo!
```

## Compila, pero no mancha!

Con el comando `cargo check` podemos pedirle a Cargo que compruebe si el código compila sin generar todos los archivos que llevan asociados la compilación (ahorrándonos el tiempo de todo ese proceso de volcado) con lo que mejoraríamos nuestro tiempo de desarrollo notáblemente, hasta el momento en el que necesitemos ejecutar nuestro programa.

## Conclusión

Hemos visto como podemos mejorar nuestra capacidad de organización y desarrollo gracias a Cargo. Solo hemos visto una parte de lo que es capaz de hacer por nosotros, así que cómo 'standard' seguiremos usando Cargo de ahora en adelante para todos nuestros proyectos. 
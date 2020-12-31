# 1. Hello, world!

No hay tradición más especial ni ceremonia más querida que escribir un clásico `hello world!` en cualquier idioma, y por supuesto, Rust no será una excepción.

Con el entorno ya configurado tal y como vimos en la introducción, crearemos un nuevo archivo llamado `main.rs`, y lo abrimos con nuestro editor de texto favorito.

## Nuestro primer programa

Ya con el editor abierto, escribiremos lo siguiente:

```
fn main() {
    println!("Hello, world");
} 

```

Guarda el archivo y si estás en `Windows` escribe lo siguiente:

```
> rustc main.rs
> .\main.exe
```

Si estás en `Linux` o en `macOS`:

```
$ rustc main.rs
$ ./main
```

Y enhorabuena :+1:! Si todo ha ido bien, deberías de haber escrito tu primer programa en Rust, lo cuál según la documentación oficial te convierte en un programador Rust!

## Análisis del código

Repasemos lo que hemos visto hasta ahora:

```
fn main() {

}
```

Este es una de las funciones más especiales de Rust. (Si no sabes lo que es una función, simplemente piénsalo como un bloque de código agrupado que nos permite ejecutar acciónes prediseñadas).

La función `main` es el punto de entrada a cualquier programa en Rust, al igual que por ejemplo, en `C++`. Siempre debe de haber una función `main` para que Rust pueda ponerse en funcionamiento, ya que será lo primero que busque en su estructura interna.

Cualquier función en Rust se declara con la palabra reservada o keyword `fn`, seguido del nombre que tome la función, y seguido por las llaves que encapsulan en cuerpo de la función en dónde pondremos nuestro código. Por cierto, es un hábito de buenas prácticas poner la llave que abre el contenido del cuerpo en la misma línea 
que los dos paréntesis `()`. 

### El contenido del cuerpo

Dentro de las llaves, pondremos nuestro código Rust:

`println!("Hello, world!");`. Todo empieza con la llamada a una `macro` de Rust. Ojo!, todas las macros en Rust se llaman con un `!` despues del nombre de la macro. Discutiremos más adelante por qué algunas funciones en Rust se usan cómo macros, pero por ahora piensa que lo que estamos haciendo es simplemente, usar una funcionalidad prediseñada para ejercer alguna acción, en este caso, println!. 

Seguido de esto, le pasamos `Hello, world!` a nuestra macro como argumento (un argumento es como una especie de embudo con el cuál podemos pasarle **información** a nuestras funciones o macros), y acabamos la expresión con `;`. Toda expresión en Rust ha de acabarse con el punto y coma para indicar el final de la expresión.

## Compilando el código.

Rust es un lenguaje compilado, lo cuál implica un paso extra antes de ejecutarlo. No es el propósito de esta guía el discutir las diferencias sobre lenguajes compilados o interpretados, pero a modo de breve resumen para los que nunca hayan visto el proceso y no sepan de que hablamos, compilar es traducir un código de programación escrito por humanos a codigo ejecutable por la máquina, así de fácil, y hay lenguajes que basan su operatividad en dicho proceso.

Tenemos dos grandes maneras de compilar código en Rust, y hoy veremos la primera.
Abrimos nuestra terminal y  escribiremos lo siguiente (siempre desde nuestro directorio de trabajo actual):

`rustc main.rs`. Con el comando rustc llamamos al compilador. Después le decimos el nombre del archivo el cual queremos compilar, en este caso nuestro `main.rs`.

Si miramos dentro de nuestro directorio (con el comando `ls(Linux, macOS) o dir(Windows)` veremos los archivos main.exe, main.pdb y main.rs).
`main.rs` es nuestro archivo de código Rust, `main.pdb` es un archivo que contiene información de debugging, y por último `main.exe` es nuestro archivo final ejecutable.

Rust es un lenguaje `ahead-of-time compiled`. Eso significa que una vez compilado, podrás distribuír tu programa a dónde quieras sin necesidad de que el usuario tenga instalado Rust en su sistema operativo. Un lenguaje compilado hace más lento el tiempo de desarrollo de un programa, pero a cambio podrás ejecutarlo en cualquier máquina, procesador, sistema embebido... Lo cuál mejora la cadena de producción de un producto final increíblemente, y sin meternos a hablar de las mejoras de potencia y rapidez. 

Siempre es un intercambio, de algo en contra por algo a favor según la perspectiva y las necesidades requeridas.


## Hasta la próxima

Espero que os haya gustado vuestra primera aventura `rustácea!`. Hemos explicado los pormenores para que cualquier futuro desarrollador pueda iniciarse con pie firme en este lenguaje.

Gracias por leer, y nos vemos en el siguiente capítulo!










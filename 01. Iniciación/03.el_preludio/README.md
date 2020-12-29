# El 'preludio'

`El preludio` en Rust es una lista de cosas que automáticamente este **importa** en cada nuevo programa. Sus desarrolladores intentan mantener esa lista tan pequeña como sea posible y enfocada a cosas que son usadas en cada programa de Rust sin importar su tamaño o cometido.

Rust trae por defecto las herramientas necesarias listas para ser utilizadas en tu código, ya que si tuviéramos que importar cada cosa que usamos, haríamos el proceso complicado en demasía, y por otra parte, si importas demasiadas cosas que nunca o poco frecuentemente son usadas tampoco es la mejor opción de cara a un desarrollo sólido.

# Las librerías y los módulos

Una **librería** no es más que una agrupación de módulos, y estos a su vez son programas diseñados para cumplir una funcionalidad específica dentro de un ambiente o programa mayor. Su objetivo es el de facilitar el desarrollo de cierta funcionalidad futura gracias a otra implementada previamente, agrupando código y recursos de manera que permiten hacer el trabajo más fácil y rápido a los desarrolladores en su posterior uso.

En resumidas cuentas son un conjunto de abstracciones listas para facilitarle la vida al desarrollador.

Rust posee dos términos distintos relacionados con el sistema de módulos: `crate` y `módulo`. Un crate es un sinónimo para `biblioteca` or `paquete` en otros lenguajes, mientras que módulo queda reservado para la misma explicación aportada anteriormente, siendo 

## La librería standard

O más conocida cómo `std`, y concepto derivado de C++, hace referencia a una librería genérica o base en el cuál se definen las herramientas básicas o primeras abstracciones disponibles para cada lenguaje.

Aunque `std` está disponible por defecto para todos los `crates`, la librería standard puede ser llamada a través de la declaración `use` a través del path `std`.






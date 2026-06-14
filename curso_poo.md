---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.19.3
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Programación Orientada a Objetos
## 1. Paradigma Imperativo: Variables Dispersas
### Problema a Resolver

Queremos almacenar información de un libro:

Título
Autor
Editorial
Año de edición
Número de páginas
Precio

En el paradigma imperativo más básico, cada dato se almacena en una variable independiente.
### Ejemplo

```python
titulo = "El Quijote"
autor = "Miguel de Cervantes"
editorial = "Espasa"
anio = 1605
paginas = 863
precio = 49.90

print("Título:", titulo)
print("Autor:", autor)
print("Editorial:", editorial)
print("Año:", anio)
print("Páginas:", paginas)
print("Precio:", precio)

## Fin del programa
```

<!-- #region -->

### Dos Libros

Ahora la situación empieza a complicarse.

```python
titulo1 = "El Quijote"
autor1 = "Miguel de Cervantes"
editorial1 = "Espasa"
anio1 = 1605
paginas1 = 863
precio1 = 49.90

titulo2 = "1984"
autor2 = "George Orwell"
editorial2 = "Debolsillo"
anio2 = 1949
paginas2 = 352
precio2 = 35.50
```
Ya tenemos:

12 variables
para solamente:

2 libros

<!-- #endregion -->

### Diez Libros

Si cada libro tiene:

    6 atributos

entonces:

    10 × 6 = 60 variables

El programa empieza a llenarse de nombres como:

    titulo7
    autor7
    precio7

    titulo8
    autor8
    precio8


### Problema 1: Desorganización

Las variables relacionadas entre sí no están unidas.

Por ejemplo se tiene un error sin mecanismo de prevención.

```python
titulo1 = "El Quijote"
precio1 = 49.90

titulo2 = "1984"
precio2 = 35.50

print(titulo1, precio2) ## Error de mezcla de variables

## Fin del programa
```

Se mezcló información de libros distintos.


### Problema 2: Escalabilidad

Si agregamos un nuevo atributo:

    ISBN

debemos crear nuevas variables:

    isbn1
    isbn2
    isbn3

y modificar todo el programa.

<!-- #region -->
### Problema 3: Repetición de Código

Para mostrar un libro:

```python
    print(titulo1)
    print(autor1)
    print(editorial1)
    print(anio1)
    print(paginas1)
    print(precio1)
```

Para el segundo:

```python
    print(titulo2)
    print(autor2)
    print(editorial2)
    print(anio2)
    print(paginas2)
    print(precio2)
```
La misma lógica se repite continuamente.
<!-- #endregion -->

### Conclusión

El paradigma imperativo funciona bien cuando:

- Hay pocos datos.
- El programa es pequeño.
- Las variables son simples.

Pero cuando aparecen muchas entidades similares (libros, alumnos, empleados, clientes, productos, etc.), surgen tres problemas:

- Demasiadas variables.
- Datos relacionados dispersos.
- Mucha repetición de código.

Estos problemas motivaron la siguiente evolución: agrupar variables relacionadas en estructuras de datos, dando paso a la programación estructurada.

_En el paradigma imperativo los datos existen como variables independientes. A medida que aumenta la cantidad de información, mantener la coherencia entre esas variables se vuelve cada vez más difícil. La siguiente etapa en la evolución de la programación consiste en agrupar variables relacionadas para representar entidades del mundo real de forma más organizada._

<!-- #region -->
## 2. Paradigma Estructurado
Agrupando Variables y Relacionándolas con Funciones
### Situación Inicial

Tenemos un libro:

```python
titulo = "El Quijote"
autor = "Miguel de Cervantes"
editorial = "Espasa"
anio = 1605
paginas = 863
precio = 49.90
```
<!-- #endregion -->

<!-- #region -->
Ya vimos que esto escala mal.

### Primer Intento: Lista

Agrupamos los datos.
```python
libro = [
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
]
```

<!-- #endregion -->

Ahora tenemos:

    1 variable

en lugar de:

    6 variables


### Problema de la Lista

¿Qué significa?

    libro[4]

- ¿Autor?
- ¿Precio?
- ¿Páginas?

No es evidente.

Hay que memorizar posiciones.

```python
libro = [
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
]

print(libro[1])

## Fin del codigo
```

### Segundo Intento: Diccionario

Asignamos nombres a los datos.



```python
libro = {
    "titulo": "El Quijote",
    "autor": "Miguel de Cervantes",
    "editorial": "Espasa",
    "anio": 1605,
    "paginas": 863,
    "precio": 49.90
}

print(libro["paginas"])

## Fin del codigo
```

Mucho más claro.

### Ventaja

Los datos ya representan una entidad completa.

    libro

representa:

    Un libro

y no seis variables aisladas.


### Aparece un Nuevo Problema

Queremos mostrar un libro.

Creamos una función.



```python
libro = {
    "titulo": "El Quijote",
    "autor": "Miguel de Cervantes",
    "editorial": "Espasa",
    "anio": 1605,
    "paginas": 863,
    "precio": 49.90
}

def mostrar_libro(libro):
    print("Título:", libro["titulo"])
    print("Autor:", libro["autor"])
    print("Precio:", libro["precio"])

mostrar_libro(libro)

## Fin del codigo
```

<!-- #region -->

### Relación Datos–Funciones

Observa algo importante.

La función:

    mostrar_libro()

trabaja exclusivamente con:

    libro

Existe una relación natural.

Podemos representarla así:

    libro
       │
       ├── mostrar_libro()
       ├── cambiar_precio()
       ├── aplicar_descuento()
       └── mostrar_resumen()

Todas esas funciones están relacionadas con el mismo conjunto de datos.

### Más Funciones

```python
def cambiar_precio(libro, nuevo_precio):
    libro["precio"] = nuevo_precio
def aplicar_descuento(libro, porcentaje):
    libro["precio"] *= (1 - porcentaje/100)
```
Uso:

```python
aplicar_descuento(libro, 10)
```

### El Problema que Queda

Observa que los datos están aquí:

    libro

y las funciones aquí:

```python
mostrar_libro()

cambiar_precio()

aplicar_descuento()
```

No existe ninguna unión física entre ambos.

Nada impide hacer:

```python
aplicar_descuento(cliente, 10)
```
o
```python
cambiar_precio(empleado, 100)
```
La relación existe solamente en la mente del programador.


<!-- #endregion -->

<!-- #region -->
### Idea Fundamental

Los programadores comenzaron a pensar:

_Si una función trabaja exclusivamente sobre un tipo de dato, ¿por qué no guardar la función junto al dato?_

En lugar de:

    Libro

por un lado,

y

```python
mostrar_libro()
cambiar_precio()
aplicar_descuento()
```
por otro,

podríamos tener:

    Libro
     ├── datos
     ├── mostrar()
     ├── cambiar_precio()
     └── aplicar_descuento()
### Nacimiento de la Programación Orientada a Objetos

La idea central de la POO no fue inicialmente la herencia ni el polimorfismo.

La idea original fue mucho más simple:

_Mantener juntos los datos y las funciones que trabajan sobre esos datos._

Esa unión recibe el nombre de:

    Objeto

y el molde para crearlo se llama:

    Clase

Para estudiantes de ingeniería, esta transición suele ser mucho más intuitiva que comenzar diciendo "una clase es una plantilla para crear objetos". Históricamente y conceptualmente, la POO aparece como la respuesta natural a una observación:

_Algunas funciones tienen una relación tan estrecha con ciertas variables que resulta conveniente tratarlas como una sola unidad._
<!-- #endregion -->

<!-- #region -->
## 3. Paradigma Orientado a Objetos
###Objetivo

Hasta ahora hemos visto que:

- Las variables aisladas generan desorganización.
- Las estructuras de datos agrupan información relacionada.
- Las funciones permiten operar sobre esos datos.

Sin embargo, los datos y las funciones siguen estando separados.

La Programación Orientada a Objetos propone una solución:

Mantener juntos los datos y las operaciones relacionadas con esos datos.

### Paso 1: El Molde del Libro

Queremos representar libros.

Primero definimos qué información debe tener un libro.
```python
class Libro:

    def __init__(self, titulo, autor, editorial,
                 anio, paginas, precio):

        self.titulo = titulo
        self.autor = autor
        self.editorial = editorial
        self.anio = anio
        self.paginas = paginas
        self.precio = precio
```
Todavía no hemos creado ningún libro.

Solamente hemos definido el molde.

### Clase y Objeto

La clase es el molde.

    Clase
      Libro

Los objetos son los libros concretos.

    Objeto
      libro1

    Objeto
      libro2

### Paso 2: Crear Objetos

Ahora construimos libros reales.

```python
libro1 = Libro(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
)

libro2 = Libro(
    "1984",
    "George Orwell",
    "Debolsillo",
    1949,
    352,
    35.50
)
```
Visualmente:

    Libro
      │
      ├── libro1
      └── libro2

La clase genera objetos.

### Paso 3: Acceder a los Atributos

Cada objeto posee sus propios datos.

    print(libro1.titulo)
    print(libro2.titulo)

Resultado:

    El Quijote
    1984

Observación:

    libro1.titulo

y

    libro2.titulo

son variables diferentes.

Cada objeto mantiene su propio estado.
<!-- #endregion -->

```python
class Libro:
    def __init__(self, titulo, autor, editorial, anio, paginas, precio):
        self.titulo = titulo
        self.autor = autor
        self.editorial = editorial
        self.anio = anio
        self.paginas = paginas
        self.precio = precio

libro1 = Libro(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
)

libro2 = Libro(
    "1984",
    "George Orwell",
    "Debolsillo",
    1949,
    352,
    35.50
)
        
print(libro1.titulo)
print(libro2.titulo)

## Fin del codigo
```

### Paso 4: Primera Función del Libro

Hasta ahora los libros sólo almacenan información.

Agregaremos un comportamiento.

```python
class Libro:

    def __init__(self, titulo, autor, editorial,
                 anio, paginas, precio):

        self.titulo = titulo
        self.autor = autor
        self.editorial = editorial
        self.anio = anio
        self.paginas = paginas
        self.precio = precio

    def mostrar(self):
        print("Título:", self.titulo)
        print("Autor:", self.autor)
        print("Precio:", self.precio)

libro1 = Libro(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
)

libro1.mostrar()

## fin del codigo
```

<!-- #region -->
¿Qué Acaba de Ocurrir?

Antes hacíamos:

```python
mostrar_libro(libro1)
```
Ahora hacemos:

```python
libro1.mostrar()
```
La función vive dentro de el propio objeto.
<!-- #endregion -->

<!-- #region -->
### Paso 5: Modificar el Precio

Los libros deben poder cambiar de precio.

Agregamos un nuevo método.

```python
def cambiar_precio(self, nuevo_precio):
    self.precio = nuevo_precio
```
Uso:

```python
libro1.cambiar_precio(60)
```

Verificación:

```python
print(libro1.precio)
```

Resultado:

    60

## Paso 6: Los Objetos Son Independientes
```python
print(libro1.precio)
print(libro2.precio)
```
Resultado:

    60
    35.5

Cambiar un objeto no afecta a los demás.

Cada objeto administra sus propios datos.


<!-- #endregion -->

```python
class Libro:

    def __init__(self, titulo, autor, editorial,
                 anio, paginas, precio):

        self.titulo = titulo
        self.autor = autor
        self.editorial = editorial
        self.anio = anio
        self.paginas = paginas
        self.precio = precio

    def mostrar(self):
        print("Título:", self.titulo)
        print("Autor:", self.autor)
        print("Precio:", self.precio)

    def cambiar_precio(self, nuevo_precio):
        self.precio = nuevo_precio

libro1 = Libro(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
)
libro1.mostrar()
print ("\n")
libro1.cambiar_precio(60)
print ("\n")
print(libro1.precio)
print ("\n")
Libro.mostrar(libro1)

## Fin del codigo
```

<!-- #region -->
### Paso 7: Interacción Entre Objeto y Clase

Cuando escribimos:

```python
libro1.mostrar()
```
ocurre internamente algo parecido a:

```python
Libro.mostrar(libro1)
```
El objeto se envía automáticamente al método mediante self.

Por eso dentro del método podemos escribir:

```python    
self.titulo
self.precio
```
y acceder a los datos del objeto que realizó la llamada.


<!-- #endregion -->

<!-- #region -->
## Paso 8: Agregar Inteligencia al Objeto

Podemos incorporar operaciones propias del dominio.

Por ejemplo:

```python
    def aplicar_descuento(self, porcentaje):
        self.precio = self.precio * (1 - porcentaje/100)
```
Uso:
```python
libro1.aplicar_descuento(10)
```
Si el precio era:

    60

ahora será:

    54 
    
### Evolución del Libro

Primero:

    Libro
     ├── titulo
     ├── autor
     ├── editorial
     ├── anio
     ├── paginas
     └── precio

Después:

    Libro
     ├── titulo
     ├── autor
     ├── editorial
     ├── anio
     ├── paginas
     ├── precio
     ├── mostrar()
     ├── cambiar_precio()
     └── aplicar_descuento()

El objeto ya no es solamente información.

También sabe qué puede hacer con esa información.

### Idea Central del Capítulo

En programación orientada a objetos:

- Los datos se llaman atributos.
- Las funciones se llaman métodos.
- Los atributos y métodos viven juntos dentro de un objeto.
- Una clase define cómo serán esos objetos.

Por eso podemos decir:

_Un objeto representa una entidad del mundo real que posee estado (atributos) y comportamiento (métodos)._

Y nuestro objeto Libro es precisamente eso: un libro que almacena información y sabe operar sobre ella.


<!-- #endregion -->

```python
class Libro:

    def __init__(self, titulo, autor, editorial,
                 anio, paginas, precio):

        self.titulo = titulo
        self.autor = autor
        self.editorial = editorial
        self.anio = anio
        self.paginas = paginas
        self.precio = precio

    def mostrar(self):
        print("Título:", self.titulo)
        print("Autor:", self.autor)
        print("Precio:", self.precio)

    def cambiar_precio(self, nuevo_precio):
        self.precio = nuevo_precio
    def aplicar_descuento(self, porcentaje):
        self.precio = self.precio * (1 - porcentaje/100)

libro1 = Libro(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
)
libro1.mostrar()
print ("\n")
libro1.cambiar_precio(60)
print ("\n")
print(libro1.precio)
print ("\n")
Libro.mostrar(libro1)
libro1.aplicar_descuento(10)
print ("\n")
print(libro1.precio)

## Fin del codigo
```

## 4. Encapsulamiento

### Problema

Los datos se puedan cambiar sin control, por ejemplo poner al atributo precio un valor negativo.

Para solucionar este problema se puede proteger las variables con "__".

Surge otro problema, una variable protegida no podría cambiar de valor, la solución entonces es crear funciones modificadoras dentro de la clase.


```python
class Libro:

    def __init__(self, titulo, autor, editorial,
                 anio, paginas, precio):

        self.__titulo = titulo
        self.__autor = autor
        self.__editorial = editorial
        self.__anio = anio
        self.__paginas = paginas
        self.__precio = precio

    def mostrar(self):
        print("Título:", self.__titulo)
        print("Autor:", self.__autor)
        print("Precio:", self.__precio)

    def cambiar_precio(self, nuevo_precio):
        if nuevo_precio >0:
            self.__precio = nuevo_precio
    def aplicar_descuento(self, porcentaje):
        self.__precio = self.__precio * (1 - porcentaje/100)
    def obtener_precio(self):
        return self.__precio

libro1 = Libro(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    863,
    49.90
)

print(libro1.obtener_precio())

libro1.precio=10
print(libro1.obtener_precio())

libro1.cambiar_precio(-100)

print(libro1.obtener_precio())

libro1.cambiar_precio(200)

print(libro1.obtener_precio())

## Fin del codigo
```

## 5. Herencia

### Motivación

Hasta ahora hemos construido una clase Libro que contiene atributos y métodos relacionados con un libro.

El encapsulamiento nos permitió proteger los atributos y controlar las modificaciones mediante métodos específicos.

Sin embargo, aparece un nuevo problema cuando el sistema comienza a crecer.

Supongamos que la biblioteca maneja distintos tipos de libros:

- Libros físicos.
- Libros digitales.

Ambos tipos de libro poseen información común:

- Título.
- Autor.
- Editorial.
- Año de publicación.
- Precio.

Y ambos necesitan realizar las mismas operaciones:

- Mostrar el precio.
- Cambiar el precio.

Una primera solución sería crear dos clases independientes.

El inconveniente es que terminaríamos copiando los mismos atributos y los mismos métodos en ambas clases.

A medida que el sistema crece, la duplicación de código genera varios problemas:

- Más trabajo de programación.
- Mayor probabilidad de errores.
- Dificultad para realizar modificaciones.
- Mayor esfuerzo de mantenimiento.

La pregunta natural es:

_Si varias clases comparten información y comportamiento, ¿por qué volver a escribir el mismo código?_

La herencia surge precisamente para resolver este problema.

La idea consiste en identificar aquello que es común y colocarlo en una clase más general.

En nuestro caso, tanto los libros físicos como los libros digitales son, en esencia, libros.

Por lo tanto, podemos construir una clase general denominada *Libro*, que contenga todo lo que comparten ambos tipos.

Posteriormente crearemos clases más especializadas:

- LibroFisico
- LibroDigital

Estas clases heredarán automáticamente los atributos y métodos definidos en *Libro*.

De esta manera:

- La clase *Libro* contendrá los atributos comunes.
- La clase *LibroFisico* añadirá el atributo paginas.
- La clase *LibroDigital* añadirá el atributo formato.
- Ambas clases reutilizarán los métodos para mostrar y modificar el precio.

Además, cada subclase podrá incorporar funcionalidades propias.

Por ejemplo, un libro digital puede descargarse, mientras que un libro físico no.

La herencia permite entonces reutilizar código existente y extenderlo con nuevas capacidades sin necesidad de duplicar información.

Visualmente:

    Libro
    │
    ├── titulo
    ├── autor
    ├── editorial
    ├── anio
    ├── precio
    ├── mostrar_precio()
    └── cambiar_precio()
            │
            ├──────────────┐
            │              │
            ▼              ▼

    LibroFisico      LibroDigital
    │                │
    ├── paginas      ├── formato
    │                └── descargar()

La relación fundamental es:

_Un LibroFisico es un Libro._

_Un LibroDigital es un Libro._

Cuando esta afirmación tiene sentido, normalmente existe una buena candidata para aplicar herencia.

Además se ha hecho un proceso de abstracción, la clase *Libro* es una idea abstracta

```python
class Libro:

    def __init__(self,
                 titulo,
                 autor,
                 editorial,
                 anio,
                 precio):

        self._titulo = titulo
        self._autor = autor
        self._editorial = editorial
        self._anio = anio
        self._precio = precio

    def mostrar_precio(self):

        print("Precio:", self._precio)

    def cambiar_precio(self, nuevo_precio):

        if nuevo_precio > 0:
            self._precio = nuevo_precio


class LibroFisico(Libro):

    def __init__(self,
                 titulo,
                 autor,
                 editorial,
                 anio,
                 precio,
                 paginas):

        super().__init__(
            titulo,
            autor,
            editorial,
            anio,
            precio
        )

        self._paginas = paginas


class LibroDigital(Libro):

    def __init__(self,
                 titulo,
                 autor,
                 editorial,
                 anio,
                 precio,
                 formato):

        super().__init__(
            titulo,
            autor,
            editorial,
            anio,
            precio
        )

        self._formato = formato

    def descargar(self):

        print(
            "Descargando",
            self._titulo,
            "en formato",
            self._formato
        )


# Crear objetos

fisico = LibroFisico(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    49.90,
    863
)

digital = LibroDigital(
    "1984",
    "George Orwell",
    "Debolsillo",
    1949,
    35.50,
    "PDF"
)

# Métodos heredados

fisico.mostrar_precio()
digital.mostrar_precio()

# Cambio de precio

digital.cambiar_precio(40)

digital.mostrar_precio()

# Método propio de LibroDigital

digital.descargar()

## Fin del codigo
```

## 6. Polimorfismo

### Motivación

En el capítulo anterior vimos cómo la herencia permite reutilizar atributos y métodos entre clases relacionadas.

Construimos una jerarquía de clases:

    Libro
    │
    ├── LibroFisico
    │
    └── LibroDigital

Ambas clases heredan los atributos y métodos comunes definidos en *Libro*.

Sin embargo, aparece una nueva necesidad.

Supongamos que queremos mostrar información de distintos tipos de libros.

Podríamos hacerlo así:

    Si es LibroFisico:
        llamar a mostrar_fisico()

    Si es LibroDigital:
        llamar a mostrar_digital()

A medida que aparecen nuevos tipos de libros, el programa comienza a llenarse de decisiones.

- Si es LibroFisico ...
- Si es LibroDigital ...
- Si es Audiolibro ...
- Si es Revista ...

El código se vuelve más complejo porque el programa necesita saber constantemente con qué tipo de objeto está trabajando.

La pregunta natural es:

_¿Podemos tratar distintos tipos de libros de la misma manera?_

La respuesta es sí.

Para ello cada clase implementa un método con el mismo nombre, pero adaptado a sus propias características.

A esta capacidad se la denomina:

### Polimorfismo

La palabra proviene del griego:

    Poly = muchos

    Morphé = formas

y puede interpretarse como:

_Un mismo mensaje puede producir comportamientos diferentes según el objeto que lo reciba._

*Idea Fundamental*

Supongamos que todos los libros poseen un método:

mostrar()

Cuando enviamos el mensaje:

    mostrar()

cada objeto responderá de acuerdo con su propia naturaleza.

    Un libro físico mostrará sus páginas.

    Un libro digital mostrará su formato.

El programa no necesita saber cuál de los dos está utilizando.

Simplemente invoca el método.

### Ventajas

El polimorfismo permite:

- Reducir decisiones condicionales.
- Escribir código más flexible.
- Incorporar nuevos tipos de objetos sin modificar código existente.
- Trabajar con objetos a través de una interfaz común.
- Estructura Conceptual
  
                    mostrar()
                        │
                        ▼
                      Libro
                        ▲
                        │
            ┌───────────┴───────────┐
            │                       │
            ▼                       ▼
        LibroFisico            LibroDigital
            mostrar()              mostrar()
            muestra páginas        muestra formato

El mismo mensaje:

    mostrar()

produce resultados distintos dependiendo del objeto.

Eso es polimorfismo.

```python
class Libro:

    def __init__(self,
                 titulo,
                 autor,
                 editorial,
                 anio,
                 precio):

        self._titulo = titulo
        self._autor = autor
        self._editorial = editorial
        self._anio = anio
        self._precio = precio

    def mostrar(self):

        print("Título:", self._titulo)
        print("Autor:", self._autor)
        print("Precio:", self._precio)


class LibroFisico(Libro):

    def __init__(self,
                 titulo,
                 autor,
                 editorial,
                 anio,
                 precio,
                 paginas):

        super().__init__(
            titulo,
            autor,
            editorial,
            anio,
            precio
        )

        self._paginas = paginas

    def mostrar(self):

        print("LIBRO FÍSICO")
        print("Título:", self._titulo)
        print("Páginas:", self._paginas)
        print("Precio:", self._precio)


class LibroDigital(Libro):

    def __init__(self,
                 titulo,
                 autor,
                 editorial,
                 anio,
                 precio,
                 formato):

        super().__init__(
            titulo,
            autor,
            editorial,
            anio,
            precio
        )

        self._formato = formato

    def mostrar(self):

        print("LIBRO DIGITAL")
        print("Título:", self._titulo)
        print("Formato:", self._formato)
        print("Precio:", self._precio)

    def descargar(self):

        print(
            "Descargando",
            self._titulo
        )


fisico = LibroFisico(
    "El Quijote",
    "Miguel de Cervantes",
    "Espasa",
    1605,
    49.90,
    863
)

digital = LibroDigital(
    "1984",
    "George Orwell",
    "Debolsillo",
    1949,
    35.50,
    "PDF"
)

fisico.mostrar()

print()

digital.mostrar()

# Fin del codigo
```

<!-- #region -->
## 7. Objetos Reales en Python: Introducción a SymPy

### Motivación

Hasta ahora hemos creado nuestros propios objetos.

Por ejemplo:

```python
libro1 = Libro(...)
```

Pero en la práctica la mayoría de las veces utilizaremos objetos creados por bibliotecas.

Una de las bibliotecas más populares para matemáticas simbólicas es **SymPy**.

La utilizaremos para descubrir objetos reales en acción.

---

# Paso 1: Instalar SymPy

```bash
pip install sympy
```

---

# Paso 2: Nuestro Primer Objeto

```python
from sympy import Symbol

x = Symbol("x")
```

Pregunta:

¿`x` es una variable de Python?

La respuesta es:

**No exactamente.**

`x` es un objeto.

Comprobémoslo:

```python
print(type(x))
```

Resultado:

```python
<class 'sympy.core.symbol.Symbol'>
```

---

# Paso 3: La Clase

Clase:

```python
Symbol
```

Objeto:

```python
x
```

Relación:

```text
Clase
  Symbol

      │

      ▼

Objeto
  x
```

Igual que:

```text
Clase
  Libro

      │

      ▼

Objeto
  libro1
```

---

# Paso 4: Construir Expresiones

```python
expresion = x**2 + 2*x + 1
```

Ahora tenemos otro objeto.

```python
print(type(expresion))
```

Resultado:

```python
<class 'sympy.core.add.Add'>
```

---

# Sorpresa

La expresión matemática también es un objeto.

```text
x

x² + 2x + 1
```

son objetos distintos.

---

# Paso 5: Invocar Métodos

Factorización:

```python
print(expresion.factor())
```

Resultado:

```python
(x + 1)**2
```

Observa:

```python
expresion.factor()
```

Es exactamente el mismo patrón que:

```python
libro.mostrar_precio()
```

o

```python
libro.cambiar_precio()
```

Estamos enviando un mensaje a un objeto.

---

# Paso 6: Derivadas

```python
print(expresion.diff(x))
```

Resultado:

```python
2*x + 2
```

El objeto sabe derivarse.

---

# Paso 7: Integrales

```python
from sympy import integrate

print(integrate(x**2, x))
```

Resultado:

```python
x**3/3
```

---

# Paso 8: Sustitución de Valores

```python
print(expresion.subs(x, 3))
```

Resultado:

```python
16
```

La expresión sabe evaluarse.

---

# Paso 9: Resolver Ecuaciones

```python
from sympy import solve

ecuacion = x**2 - 4

print(solve(ecuacion))
```

Resultado:

```python
[-2, 2]
```

---

# Paso 10: Anatomía de un Objeto Matemático

Visualmente:

```text
expresion

├── símbolos
├── operadores
├── estructura algebraica
│
├── factor()
├── diff()
├── subs()
└── simplify()
```

---

# Lo Que Hemos Aprendido

Durante el curso construimos:

```python
libro = Libro(...)
```

Ahora utilizamos:

```python
x = Symbol("x")

expresion = x**2 + 2*x + 1
```

Los conceptos son exactamente los mismos:

| Concepto POO | Ejemplo Libro    | Ejemplo SymPy                   |
| ------------ | ---------------- | ------------------------------- |
| Clase        | Libro            | Symbol                          |
| Objeto       | libro1           | x                               |
| Método       | cambiar_precio() | factor()                        |
| Método       | mostrar_precio() | diff()                          |
| Atributos    | titulo, precio   | nombre, propiedades matemáticas |

---

# Conclusión

La Programación Orientada a Objetos no es una teoría para construir ejemplos académicos.

Es la forma en que están construidas muchas de las bibliotecas profesionales que utilizaremos en:

* Matemáticas.
* Ciencia.
* Ingeniería.
* Inteligencia Artificial.
* Desarrollo de Software.

Cuando escribimos:

```python
x = Symbol("x")

expresion = x**2 + 2*x + 1

expresion.factor()
```

estamos utilizando exactamente los mismos conceptos que aprendimos con nuestros objetos `Libro`.

La diferencia no está en la Programación Orientada a Objetos.

La diferencia está en el problema que el objeto intenta resolver.

<!-- #endregion -->

```python
# ============================================
# Introducción a SymPy
# Ejemplo completo
# ============================================

from sympy import Symbol
from sympy import solve
from sympy import integrate


print("=" * 50)
print("CREACIÓN DE OBJETOS")
print("=" * 50)

# Crear objetos Symbol

x = Symbol("x")
y = Symbol("y")

print("Objeto x:", x)
print("Objeto y:", y)

print("\nTipo de x:")
print(type(x))


print("\n" + "=" * 50)
print("CONSTRUCCIÓN DE EXPRESIONES")
print("=" * 50)

expresion = x**2 + 2*x + 1

print("Expresión:")
print(expresion)

print("\nTipo de la expresión:")
print(type(expresion))


print("\n" + "=" * 50)
print("FACTORIZACIÓN")
print("=" * 50)

factorizada = expresion.factor()

print("Original:")
print(expresion)

print("Factorizada:")
print(factorizada)


print("\n" + "=" * 50)
print("EXPANSIÓN")
print("=" * 50)

otra = (x + 3)*(x - 2)

print("Expresión:")
print(otra)

print("Expandida:")
print(otra.expand())


print("\n" + "=" * 50)
print("DERIVADAS")
print("=" * 50)

derivada = expresion.diff(x)

print("Expresión:")
print(expresion)

print("Derivada:")
print(derivada)


print("\n" + "=" * 50)
print("INTEGRALES")
print("=" * 50)

integral = integrate(x**2, x)

print("Integral de x²:")
print(integral)


print("\n" + "=" * 50)
print("SUSTITUCIÓN DE VALORES")
print("=" * 50)

valor = expresion.subs(x, 3)

print("Expresión:")
print(expresion)

print("Evaluada en x = 3:")
print(valor)


print("\n" + "=" * 50)
print("ECUACIONES")
print("=" * 50)

ecuacion = x**2 - 4

print("Ecuación:")
print(ecuacion)

soluciones = solve(ecuacion)

print("Soluciones:")
print(soluciones)


print("\n" + "=" * 50)
print("EXPRESIÓN CON DOS VARIABLES")
print("=" * 50)

expr2 = x**2 + y**2

print(expr2)

print("\nSustituyendo x=3, y=4")

resultado = expr2.subs({
    x: 3,
    y: 4
})

print(resultado)


print("\n" + "=" * 50)
print("RESUMEN DE OBJETOS")
print("=" * 50)

print("x               ->", type(x))
print("y               ->", type(y))
print("expresion       ->", type(expresion))
print("factorizada     ->", type(factorizada))
print("derivada        ->", type(derivada))
print("integral        ->", type(integral))

print("\nFin del ejemplo.")

# Fin del codigo
```

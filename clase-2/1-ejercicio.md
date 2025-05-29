
## **Ejercicio: Gestión de Préstamos de Libros en una Biblioteca**

###  **Objetivo del ejercicio**

Aplicar los conceptos de:

* Creación de base de datos y tablas
* Inserción de datos
* Relación entre tablas mediante claves foráneas
* Consultas con `INNER JOIN`

---

### **Enunciado**

Una biblioteca quiere digitalizar el registro de sus préstamos. Para ello, necesita una base de datos que contenga información sobre sus **usuarios**, los **libros disponibles** y los **préstamos realizados**.

---

### Parte 1: **Creación de la base de datos**

1. Crea una base de datos llamada `BibliotecaEjemplo`.

---

### Parte 2: **Creación de tablas**

Crea las siguientes tres tablas:

#### Tabla `Usuarios`

* `IDUsuario` (entero, clave primaria) (AutoIncremental)
* `Nombre` (texto, obligatorio)

#### Tabla `Libros`

* `IDLibro` (entero, clave primaria) (AutoIncremental)
* `Titulo` (texto, obligatorio)
* `Autor` (texto, obligatorio)

#### Tabla `Prestamos`

* `IDPrestamo` (entero, clave primaria) (AutoIncremental)
* `IDLibro` (entero, clave foránea a `Libros`)
* `IDUsuario` (entero, clave foránea a `Usuarios`)
* `FechaPrestamo` (tipo fecha)

---

### Parte 3: **Inserción de datos**

Agrega la siguiente información:

#### Usuarios:

| Nombre      |
| ----------- |
| Ana Pérez   |
| Juan López  |
| María Gómez |

#### Libros:

| Titulo                  | Autor                    |
| ----------------------- | ------------------------ |
| Cien Años de Soledad    | Gabriel García Márquez   |
| El Señor de los Anillos | J.R.R. Tolkien           |
| 1984                    | George Orwell            |
| El Principito           | Antoine de Saint-Exupéry |

#### Préstamos:

| IDLibro | IDUsuario | FechaPrestamo |
| ------- | --------- | ------------- |
| 1       | 1         | 2024-03-01    |
| 3       | 2         | 2024-03-05    |
| 2       | 3         | 2024-03-10    |

---

### Parte 4: **Consultas con INNER JOIN**

1. Utiliza un `INNER JOIN` para **mostrar los libros que tiene prestados cada usuario**. El resultado debe incluir:

   * Nombre del usuario
   * Título del libro
   * Autor del libro
   * Fecha del préstamo

   *Usa alias para mejorar la presentación de las columnas.*

-- 

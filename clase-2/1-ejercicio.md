
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

* `IDUsuario` (entero, clave primaria)
* `Nombre` (texto, obligatorio)

#### Tabla `Libros`

* `IDLibro` (entero, clave primaria)
* `Titulo` (texto, obligatorio)
* `Autor` (texto, obligatorio)

#### Tabla `Prestamos`

* `IDPrestamo` (entero, clave primaria)
* `IDLibro` (entero, clave foránea a `Libros`)
* `IDUsuario` (entero, clave foránea a `Usuarios`)
* `FechaPrestamo` (tipo fecha)

---

### Parte 3: **Inserción de datos**

Agrega la siguiente información:

#### Usuarios:

| IDUsuario | Nombre      |
| --------- | ----------- |
| 100       | Ana Pérez   |
| 101       | Juan López  |
| 102       | María Gómez |

#### Libros:

| IDLibro | Titulo                  | Autor                    |
| ------- | ----------------------- | ------------------------ |
| 1       | Cien Años de Soledad    | Gabriel García Márquez   |
| 2       | El Señor de los Anillos | J.R.R. Tolkien           |
| 3       | 1984                    | George Orwell            |
| 4       | El Principito           | Antoine de Saint-Exupéry |

#### Préstamos:

| IDPrestamo | IDLibro | IDUsuario | FechaPrestamo |
| ---------- | ------- | --------- | ------------- |
| 1          | 1       | 100       | 2024-03-01    |
| 2          | 3       | 101       | 2024-03-05    |
| 3          | 2       | 102       | 2024-03-10    |

---

### Parte 4: **Consultas con INNER JOIN**

1. Utiliza un `INNER JOIN` para **mostrar los libros que tiene prestados cada usuario**. El resultado debe incluir:

   * Nombre del usuario
   * Título del libro
   * Autor del libro
   * Fecha del préstamo

   *Usa alias para mejorar la presentación de las columnas.*

---

###  **Criterios de evaluación (opcional para clases)**

| Criterio                                        | Puntaje |
| ----------------------------------------------- | ------- |
| Base de datos y tablas creadas correctamente    | 2 pts   |
| Inserción correcta de todos los datos           | 2 pts   |
| Relaciones entre tablas definidas con claves FK | 2 pts   |
| Consulta `INNER JOIN` correcta y con alias      | 4 pts   |
| **Total**                                       | 10 pts  |

---

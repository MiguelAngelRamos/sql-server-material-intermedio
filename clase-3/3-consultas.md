```sql

-- Mostrar nombre de usuario, titulo del libro y fecha de préstamo solo para prestamos existentes.

SELECT personas.Usuarios.Nombre,biblioteca.Libros.Titulo, operaciones.Prestamos.FechaPrestamo FROM operaciones.Prestamos
INNER JOIN personas.Usuarios ON operaciones.Prestamos.IDUsuario = personas.Usuarios.IDUsuario
INNER JOIN biblioteca.Libros ON operaciones.Prestamos.IDLibro = biblioteca.Libros.IDLibro;

-- Uso Alias
/*
  1) p = operaciones.Prestamos 
  2) u = personas.Usuarios
  3) l = biblioteca.Libros
*/

SELECT u.Nombre, l.Titulo, p.FechaPrestamo FROM operaciones.Prestamos p
INNER JOIN personas.Usuarios u ON p.IDUsuario = u.IDUsuario
INNER JOIN biblioteca.Libros l ON p.IDLibro = l.IDLibro;

SELECT u.Nombre, l.Titulo, p.FechaPrestamo FROM operaciones.Prestamos AS p
INNER JOIN personas.Usuarios AS u ON p.IDUsuario = u.IDUsuario
INNER JOIN biblioteca.Libros AS l ON p.IDLibro = l.IDLibro;
```
### Usuarios

```sql
-- Insertar 10 usuarios adicionales en el esquema personas
INSERT INTO personas.Usuarios (Nombre) VALUES
(N'Carlos Ruiz'), (N'Lucía Fernández'), (N'Pedro Sánchez'), (N'Laura Torres'),
(N'Andrés Ramírez'), (N'Sofía Castro'), (N'Roberto Díaz'), (N'Elena Morales'),
(N'Javier Ortega'), (N'Patricia Herrera');
```

### Libros

```sql
-- Insertar 10 libros adicionales en el esquema biblioteca
INSERT INTO biblioteca.Libros (Titulo, Autor) VALUES
(N'Rayuela', N'Julio Cortázar'),
(N'La Sombra del Viento', N'Carlos Ruiz Zafón'),
(N'Crónica de una Muerte Anunciada', N'Gabriel García Márquez'),
(N'Fahrenheit 451', N'Ray Bradbury'),
(N'Don Quijote de la Mancha', N'Miguel de Cervantes'),
(N'La Casa de los Espíritus', N'Isabel Allende'),
(N'Veinte Poemas de Amor', N'Pablo Neruda'),
(N'El Amor en los Tiempos del Cólera', N'Gabriel García Márquez'),
(N'Pedro Páramo', N'Juan Rulfo'),
(N'Los Detectives Salvajes', N'Roberto Bolaño');
```

### Prestamos

```sql
-- Insertar préstamos variados entre usuarios y libros en el esquema operaciones
INSERT INTO operaciones.Prestamos (IDLibro, IDUsuario, FechaPrestamo) VALUES
(4, 4, '2024-04-01'),
(5, 5, '2024-04-02'),
(6, 6, '2024-04-03'),
(7, 7, '2024-04-04'),
(8, 8, '2024-04-05'),
(9, 9, '2024-04-06'),
(10, 10, '2024-04-07'),
(1, 4, '2024-04-08'),
(2, 5, '2024-04-09'),
(3, 6, '2024-04-10'),
(4, 7, '2024-04-11'),
(5, 8, '2024-04-12'),
(6, 9, '2024-04-13'),
(7, 10, '2024-04-14'),
(8, 1, '2024-04-15'),
(9, 2, '2024-04-16'),
(10, 3, '2024-04-17');
```
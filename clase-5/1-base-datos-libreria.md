```sql
-- Crear base de datos
CREATE DATABASE LibreriaDataBase;
GO

USE LibreriaDataBase;
GO

-- Tabla de autores
CREATE TABLE Autor (
    Id INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(100) NOT NULL,
    Nacionalidad NVARCHAR(50)
);
-- Tabla de editoriales
CREATE TABLE Editorial (
    Id INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(100) NOT NULL,
    Pais NVARCHAR(50)
);
-- Tabla de libros
CREATE TABLE Libro (
    Id INT PRIMARY KEY IDENTITY(1,1),
    Titulo NVARCHAR(150) NOT NULL,
    IdAutor INT NOT NULL,
    IdEditorial INT NOT NULL,
    AnioPublicacion INT,
    Precio DECIMAL(10,2),
    FOREIGN KEY (IdAutor) REFERENCES Autor(Id),
    FOREIGN KEY (IdEditorial) REFERENCES Editorial(Id)
);
-- Tabla de clientes
CREATE TABLE Cliente (
    Id INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(100),
    Correo NVARCHAR(100)
);
-- Tabla de ventas
CREATE TABLE Venta (
    Id INT PRIMARY KEY IDENTITY(1,1),
    IdCliente INT NOT NULL,
    Fecha DATETIME DEFAULT GETDATE(),
    FOREIGN KEY (IdCliente) REFERENCES Cliente(Id)
);
-- Tabla de detalle de ventas
CREATE TABLE DetalleVenta (
    IdVenta INT NOT NULL,
    IdLibro INT NOT NULL,
    Cantidad INT NOT NULL,
    PRIMARY KEY (IdVenta, IdLibro),
    FOREIGN KEY (IdVenta) REFERENCES Venta(Id),
    FOREIGN KEY (IdLibro) REFERENCES Libro(Id)
);
GO
```

## Inserts

```sql
-- Autores
INSERT INTO Autor (Nombre, Nacionalidad)
VALUES 
('Gabriel García Márquez', 'Colombiana'),
('Isabel Allende', 'Chilena'),
('Mario Vargas Llosa', 'Peruana'),
('J.K. Rowling', 'Británica'),
('Stephen King', 'Estadounidense'),
('George R.R. Martin', 'Estadounidense'),
('Jorge Luis Borges', 'Argentina'),
('Haruki Murakami', 'Japonesa'),
('Julio Cortázar', 'Argentina'),
('Jane Austen', 'Británica');

-- Editoriales
INSERT INTO Editorial (Nombre, Pais)
VALUES
('Planeta', 'España'),
('Penguin Random House', 'EE.UU.'),
('Alfaguara', 'España'),
('HarperCollins', 'EE.UU.'),
('Seix Barral', 'España'),
('Debolsillo', 'España'),
('Tusquets', 'España'),
('Anagrama', 'España'),
('Knopf', 'EE.UU.'),
('Vintage', 'EE.UU.');

-- Libros
INSERT INTO Libro (Titulo, IdAutor, IdEditorial, AnioPublicacion, Precio)
VALUES
('Cien Años de Soledad', 1, 1, 1967, 15000),
('La Casa de los Espíritus', 2, 3, 1982, 12000),
('Conversación en La Catedral', 3, 2, 1969, 17000),
('Harry Potter y la Piedra Filosofal', 4, 4, 1997, 20000),
('El Resplandor', 5, 2, 1977, 18000),
('Juego de Tronos', 6, 5, 1996, 22000),
('Ficciones', 7, 6, 1944, 11000),
('Kafka en la orilla', 8, 7, 2002, 16000),
('Rayuela', 9, 8, 1963, 14000),
('Orgullo y Prejuicio', 10, 9, 1813, 13000);

-- Clientes
INSERT INTO Cliente (Nombre, Correo)
VALUES
('Carlos Pérez', 'carlos@mail.com'),
('Ana Torres', 'ana@mail.com'),
('Juan Díaz', 'juan@mail.com'),
('María López', 'maria@mail.com'),
('Pedro Sánchez', 'pedro@mail.com'),
('Lucía Herrera', 'lucia@mail.com'),
('Tomás Rivas', 'tomas@mail.com'),
('Valeria Soto', 'valeria@mail.com'),
('Jorge Silva', 'jorge@mail.com'),
('Fernanda Morales', 'fernanda@mail.com');

-- Ventas
INSERT INTO Venta (IdCliente, Fecha)
VALUES
(1, '2024-05-01'), (2, '2024-05-02'), (3, '2024-05-02'),
(4, '2024-05-03'), (5, '2024-05-03'), (6, '2024-05-04'),
(7, '2024-05-05'), (8, '2024-05-06'), (9, '2024-05-06'), (10, '2024-05-07');

-- Detalles de ventas
INSERT INTO DetalleVenta (IdVenta, IdLibro, Cantidad)
VALUES
(1, 1, 2), (2, 3, 1), (3, 4, 1), (4, 5, 1), (5, 6, 2),
(6, 7, 1), (7, 2, 1), (8, 9, 1), (9, 8, 1), (10, 10, 3);
```
```sql

-- BibliotecaEjemplo
IF DB_ID('BibliotecaEjemplo') IS NULL -- Existe?
	CREATE DATABASE BibliotecaEjemplo; -- Si no existe, creala
GO

USE BibliotecaEjemplo;
GO

CREATE TABLE Usuarios (
	IDUsuario INT IDENTITY(1,1) PRIMARY KEY,
	Nombre NVARCHAR(100) NOT NULL
);
GO
CREATE TABLE Libros (
	IDLibro INT IDENTITY(1,1) PRIMARY KEY,
	Titulo NVARCHAR(100) NOT NULL,
	Autor NVARCHAR(100) NOT NULL
);
GO

CREATE TABLE Prestamos(
	IDPrestamo INT IDENTITY(1,1) PRIMARY KEY, 
	IDLibro INT NOT NULL, 
	IDUsuario INT NOT NULL,
	FechaPrestamo DATE NOT NULL,
	CONSTRAINT FK_Prestamos_Libros FOREIGN KEY(IDLibro) REFERENCES Libros(IDLibro),
	CONSTRAINT FK_Prestamos_Usuarios FOREIGN KEY(IDUsuario) REFERENCES Usuarios(IDUsuario)
	);
GO


SELECT name, type, parent_object_id
FROM sys.objects
WHERE type IN ('F', 'PK', 'UQ', 'C', 'D');

INSERT INTO Usuarios (Nombre) VALUES (N'Ana Pérez'),
									 (N'Juan López'),
									 (N'María Gómez');
GO
SELECT * FROM Usuarios;
/*
Libros:
Titulo	                     Autor
Cien Años de Soledad	     Gabriel García Márquez
El Señor de los Anillos	     J.R.R. Tolkien
1984	                      George Orwell
El Principito	             Antoine de Saint-Exupéry
*/
INSERT INTO Libros (Titulo, Autor) 
VALUES (N'Cien Años de Soledad', N'Gabriel García Márquez'),
	   (N'El Señor de los Anillos', N'George Orwell'),
	   (N'El Principito', N'Antoine de Saint-Exupéry');
GO
SELECT * FROM Libros;
/*
Préstamos:
IDLibro	IDUsuario	FechaPrestamo
1	      1	         2024-03-01
3	      2	         2024-03-05
2	      3	         2024-03-10
*/

INSERT INTO Prestamos (IDLibro, IDUsuario, FechaPrestamo)
VALUES (1,1,'2024-03-01'),
	   (3,2,'2024-03-05'),
	   (2,3,'2024-03-10');

SELECT * FROM Usuarios;
SELECT * FROM Libros;
SELECT * FROM Prestamos;

```
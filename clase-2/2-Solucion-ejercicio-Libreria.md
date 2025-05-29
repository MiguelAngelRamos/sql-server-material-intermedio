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
```
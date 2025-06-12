```sql
--  Crear la base de datos con soporte In-Memory OLTP
USE master;
GO

-- Cambia la ruta si es necesario
IF NOT EXISTS (SELECT name FROM sys.databases WHERE name = 'EcommerceDB')
BEGIN
    CREATE DATABASE EcommerceDB
    ON PRIMARY (
        NAME = 'EcommerceDB_data',
        FILENAME = 'C:\SqlData\EcommerceDB_data.mdf'
    ),
    FILEGROUP EcommerceDB_mod CONTAINS MEMORY_OPTIMIZED_DATA (
        NAME = 'EcommerceDB_mod',
        FILENAME = 'C:\SqlData\EcommerceDB_mod'
    )
    LOG ON (
        NAME = 'EcommerceDB_log',
        FILENAME = 'C:\SqlData\EcommerceDB_log.ldf'
    );
END
GO

USE EcommerceDB;
GO

-- ================================================
-- 🧵 TABLA: Productos (en memoria)
-- ================================================
CREATE TABLE Productos (
    IdProducto INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 32),
    Nombre NVARCHAR(100) NOT NULL,
    Precio DECIMAL(10,2) NOT NULL,
    Stock INT NOT NULL,
    Categoria NVARCHAR(50)
)
WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);
GO

-- ================================================
-- 🧑‍💼 TABLA: Clientes (en memoria)
-- ================================================
CREATE TABLE Clientes (
    IdCliente INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 32),
    Nombre NVARCHAR(100) NOT NULL,
    Email NVARCHAR(100) NOT NULL UNIQUE,
    Pais NVARCHAR(50),
    FechaRegistro DATE
)
WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);
GO

-- ================================================
-- 📦 TABLA: Pedidos (en memoria)
-- ================================================
CREATE TABLE Pedidos (
    IdPedido INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 32),
    IdCliente INT NOT NULL,
    FechaPedido DATETIME2 NOT NULL,
    Total DECIMAL(10,2),
    Estado NVARCHAR(50),
    FOREIGN KEY (IdCliente) REFERENCES Clientes(IdCliente)
)
WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);
GO

-- ================================================
-- 📄 TABLA: DetallePedido (en memoria)
-- ================================================
CREATE TABLE DetallePedido (
    IdDetalle INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 64),
    IdPedido INT NOT NULL,
    IdProducto INT NOT NULL,
    Cantidad INT NOT NULL,
    PrecioUnitario DECIMAL(10,2),
    FOREIGN KEY (IdPedido) REFERENCES Pedidos(IdPedido),
    FOREIGN KEY (IdProducto) REFERENCES Productos(IdProducto)
)
WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);
GO

-- ================================================
-- 💰 TABLA: Pagos (en memoria)
-- ================================================
CREATE TABLE Pagos (
    IdPago INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 32),
    IdPedido INT NOT NULL,
    Monto DECIMAL(10,2),
    MetodoPago NVARCHAR(50),
    FechaPago DATETIME2,
    FOREIGN KEY (IdPedido) REFERENCES Pedidos(IdPedido)
)
WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);
GO
```
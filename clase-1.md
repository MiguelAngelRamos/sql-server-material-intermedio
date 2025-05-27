```sql
/* 
  1) Crear una base de datos
*/
-- NVARCHAR ' $
IF DB_ID(N'TechDataCorpDB') IS NULL -- Existe la base de datos?
   CREATE DATABASE TechDataCorpDB -- Si no creála
GO -- Fin del lote

USE TechDataCorpDB;

GO

/* 2) Crear Esquemas Lógicos) */
-- sys contiene información de los esquemas, lista todos los existentes
IF NOT EXISTS (SELECT * FROM sys.schemas WHERE name = N'catalog')
    EXEC('CREATE SCHEMA catalog AUTHORIZATION dbo'); --- Esquema de productos
GO
IF NOT EXISTS(SELECT * FROM sys.schemas WHERE name = N'sales')
    EXEC('CREATE SCHEMA sales AUTHORIZATION dbo'); -- Esquema de ventas
GO

-- (CONSTRAINT UQ_Products_ProductCode UNIQUE) Esto significa que no pueden haber dos productos con el mismo código
-- 9999999.99
-- 2024-05-27 17:22:15
CREATE TABLE catalog.Products (
  ProductId INT IDENTITY(1,1) CONSTRAINT PK_Products PRIMARY KEY,
  ProductCode VARCHAR(20) NOT NULL CONSTRAINT UQ_Products_ProductCode UNIQUE,
  ProductName NVARCHAR(150) NOT NULL,
  UnitPrice DECIMAL(10,2) NOT NULL CONSTRAINT CK_Products_UnitPrice CHECK (UnitPrice > 0),
  IsActive BIT NOT NULL CONSTRAINT DF_Products_IsActive DEFAULT(1), -- Activo por default
  CreateAt DATETIME2(0) NOT NULL CONSTRAINT DF_Products_CreatedAt DEFAULT (GETDATE())
);

GO

CREATE INDEX IX_Products_ProductCode
    ON catalog.Products(ProductCode);

GO
```

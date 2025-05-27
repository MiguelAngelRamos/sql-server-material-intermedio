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
CREATE TABLE catalog.Products (
  ProductId INT IDENTITY(1,1) CONSTRAINT PK_Products PRIMARY KEY,
  ProductCode VARCHAR(20) NOT NULL CONSTRAINT UQ_Products_ProductCode UNIQUE, 

);
```

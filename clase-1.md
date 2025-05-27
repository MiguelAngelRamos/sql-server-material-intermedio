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
IF NOT EXISTS (SELECT * FROM sys.schemas WHERE name = N'catalog')
    EXEC('CREATE SCHEMA catalog AUTHORIZATION dbo'); --- Esquema de productos
GO
IF NOT EXISTS(SELECT * FROM sys.schemas WHERE name = N'sales')
    EXEC('CREATE SCHEMA sales AUTHORIZATION dbo'); -- Esquema de ventas
GO
```

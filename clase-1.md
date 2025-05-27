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

CREATE TABLE sales.Customers (
    CustomerId  INT IDENTITY(1,1)
        CONSTRAINT PK_Customers PRIMARY KEY,            -- PK explícita
    FirstName   NVARCHAR(100) NOT NULL,                 -- Nombre
    LastName    NVARCHAR(100) NOT NULL,                 -- Apellido
    Email       NVARCHAR(150) NOT NULL
        CONSTRAINT UQ_Customers_Email UNIQUE,           -- Correo único
    PhoneNumber NVARCHAR(20) NULL,                      -- Teléfono opcional
    CreatedAt   DATETIME2(0) NOT NULL
        CONSTRAINT DF_Customers_CreatedAt DEFAULT (GETDATE())
);

GO

CREATE TABLE sales.Orders (
    OrderId     INT IDENTITY(1,1)
        CONSTRAINT PK_Orders PRIMARY KEY,               -- PK explícita
    CustomerId  INT NOT NULL
        CONSTRAINT FK_Orders_Customers                  -- FK al cliente
            REFERENCES sales.Customers(CustomerId),
    OrderDate   DATETIME2(0) NOT NULL
        CONSTRAINT DF_Orders_OrderDate DEFAULT (GETDATE()),
    Status      CHAR(1) NOT NULL DEFAULT ('N')          -- N: Nueva, P: Pagada, C: Cancelada
        CONSTRAINT CK_Orders_Status CHECK (Status IN ('N','P','C'))
);

CREATE TABLE sales.OrderItems (
    OrderId   INT NOT NULL,                             -- Parte de la PK (orden)
    ProductId INT NOT NULL,                             -- Parte de la PK (producto)
    Quantity  INT NOT NULL
        CONSTRAINT CK_OrderItems_Qty CHECK (Quantity > 0), -- Cantidad positiva
    UnitPrice DECIMAL(10,2) NOT NULL,                   -- Precio histórico
    CONSTRAINT PK_OrderItems PRIMARY KEY (OrderId, ProductId), -- PK compuesta
    CONSTRAINT FK_OrderItems_Orders                     -- FK a cabecera
        FOREIGN KEY (OrderId)  REFERENCES sales.Orders(OrderId),
    CONSTRAINT FK_OrderItems_Products                   -- FK a productos
        FOREIGN KEY (ProductId) REFERENCES catalog.Products(ProductId)
);

GO
```

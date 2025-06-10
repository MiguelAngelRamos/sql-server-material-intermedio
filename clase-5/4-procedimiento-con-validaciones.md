```sql
CREATE PROCEDURE sp_InsertarVenta
    @IdCliente INT,
    @Fecha DATETIME,
    @IdLibro1 INT = NULL,
    @Cantidad1 INT = NULL,
    @IdLibro2 INT = NULL,
    @Cantidad2 INT = NULL,
    @IdLibro3 INT = NULL,
    @Cantidad3 INT = NULL
AS
BEGIN
    SET NOCOUNT ON;
    BEGIN TRY
        DECLARE @IdVenta INT;

        -- Validar existencia del cliente
        IF NOT EXISTS (SELECT 1 FROM Cliente WHERE Id = @IdCliente)
        BEGIN
            RAISERROR('El cliente no existe.', 16, 1);
            RETURN;
        END

        -- Validar libros y stock
        IF @IdLibro1 IS NOT NULL
            IF NOT EXISTS (SELECT 1 FROM Libro WHERE Id = @IdLibro1)
            BEGIN
                RAISERROR('El libro 1 no existe.', 16, 1);
                RETURN;
            END

        IF @IdLibro2 IS NOT NULL
            IF NOT EXISTS (SELECT 1 FROM Libro WHERE Id = @IdLibro2)
            BEGIN
                RAISERROR('El libro 2 no existe.', 16, 1);
                RETURN;
            END

        IF @IdLibro3 IS NOT NULL
            IF NOT EXISTS (SELECT 1 FROM Libro WHERE Id = @IdLibro3)
            BEGIN
                RAISERROR('El libro 3 no existe.', 16, 1);
                RETURN;
            END

        -- Insertar cabecera de venta
        INSERT INTO Venta (IdCliente, Fecha)
        VALUES (@IdCliente, @Fecha);

        SET @IdVenta = SCOPE_IDENTITY();

        -- Insertar detalles (hasta 3 libros)
        IF @IdLibro1 IS NOT NULL AND @Cantidad1 IS NOT NULL
            INSERT INTO DetalleVenta (IdVenta, IdLibro, Cantidad)
            VALUES (@IdVenta, @IdLibro1, @Cantidad1);

        IF @IdLibro2 IS NOT NULL AND @Cantidad2 IS NOT NULL
            INSERT INTO DetalleVenta (IdVenta, IdLibro, Cantidad)
            VALUES (@IdVenta, @IdLibro2, @Cantidad2);

        IF @IdLibro3 IS NOT NULL AND @Cantidad3 IS NOT NULL
            INSERT INTO DetalleVenta (IdVenta, IdLibro, Cantidad)
            VALUES (@IdVenta, @IdLibro3, @Cantidad3);

        PRINT 'Venta registrada correctamente.';
    END TRY
    BEGIN CATCH
        DECLARE @Msg NVARCHAR(4000) = ERROR_MESSAGE();
        RAISERROR(@Msg, 16, 1);
    END CATCH
END;
GO

```

## Como ejecutarlo

```sql

EXEC sp_InsertarVenta
    @IdCliente = 1,
    @Fecha = '2024-06-10',
    @IdLibro1 = 2, @Cantidad1 = 1,
    @IdLibro2 = 5, @Cantidad2 = 3;
    

EXEC sp_InsertarVenta
    @IdCliente = 80,
    @Fecha = '2024-06-10',
    @IdLibro1 = 2, @Cantidad1 = 1,
    @IdLibro2 = 5, @Cantidad2 = 3;
    
 /*
 Mensaje 50000, nivel 16, estado 1, procedimiento sp_InsertarVenta, línea 69 [línea de inicio de lote 80]
El cliente no existe.
 */

-- Fecha con SysDatetime
DECLARE @FechaVenta DATETIME;

SET @FechaVenta = SYSDATETIME();

EXEC sp_InsertarVenta
    @IdCliente = 1,
    @Fecha = @FechaVenta,
    @IdLibro1 = 2, @Cantidad1 = 1,
    @IdLibro2 = 5, @Cantidad2 = 3;
```
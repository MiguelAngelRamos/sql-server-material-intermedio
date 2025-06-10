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
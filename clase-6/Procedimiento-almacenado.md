## 1. **Procedimiento nativo:** `IncrementarStockProducto`

```sql
CREATE PROCEDURE IncrementarStockProducto
    @IdProducto INT,
    @Cantidad INT
WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')
    UPDATE dbo.Productos
    SET Stock = Stock + @Cantidad
    WHERE IdProducto = @IdProducto;
END;
GO
```

## Como ejecutar los objetos

Procedimiento IncrementarStockProducto
```sql
EXEC dbo.IncrementarStockProducto @IdProducto = 1, @Cantidad = 5;
```

## 2. **Función Escalar Nativa:** `PrecioTotalProducto`

```sql
CREATE FUNCTION PrecioTotalProducto
(
    @IdProducto INT,
    @Cantidad INT
)
RETURNS DECIMAL(10,2)
WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')
    DECLARE @precio DECIMAL(10,2);

    SELECT @precio = Precio FROM dbo.Productos WHERE IdProducto = @IdProducto;

    RETURN @precio * @Cantidad;
END;
GO
```
## Como ejecutar los objetos

Función escalar PrecioTotalProducto
```sql
SELECT dbo.PrecioTotalProducto(1, 3) AS Total;
```
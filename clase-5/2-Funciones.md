```sql
-- CantidadTotalDeLibrosComprados de un cliente especifico por su ID
CREATE FUNCTION dbo.CantidadTotalLibrosComprados(@IdCliente INT)
RETURNS INT
AS
BEGIN
	DECLARE @Total INT;
	SELECT @Total = SUM(DV.Cantidad)
	FROM Venta V
	INNER JOIN DetalleVenta DV ON V.Id = DV.IdVenta
	WHERE V.IdCliente = @IdCliente;
	RETURN ISNULL(@Total, 0); -- Si el cliente no ha comprado ningun libro la funcion devuelve 0 en vez de Null
END;
GO

-- Ejemplo de Uso de esta funcion "CantidadTotalLibrosComprados"
SELECT dbo.CantidadTotalLibrosComprados(3) AS TotalLibrosComprados;

-- Necesitamos Libros con información de autor y editorial
-- Alias DetalleVenta es igual a : DV
-- Alias Venta es igual a : V
-- SELECT * FROM DetalleVenta;  DV.Cantidad -> DetalleVenta.Cantidad

/*

 Diferencias Principales entre función y procedimiento almacenado

 Funcion:
	- Función devuelve valor siempre lo hace.
	- Usa solo a modo de Consulta (SELECT, WHERE, JOIN)
	- Una función no puede llamar a un procedimiento almacenado

 Procedimiento Almacenado:
    - No necesariamente devuelve un valor
	- Un procedimiento almacenado no puede ser llamado directamente desde un "Select"
	- Puede Modificar data: Puede Ejecutar (Insert, Update, Delete, Create, Alter)
	- Try Catch
	- Si puede ejecutar otros procedimientos y tambien se le permite llamar a funciones.
*/
```
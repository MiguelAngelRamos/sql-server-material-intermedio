```sql

-- USO DE TRIGGERS

CREATE TRIGGER tr_ValidarCantidadVenta
ON DetalleVenta
INSTEAD OF INSERT
AS
BEGIN
	/* Si intentas insertar una venta con cantidad 0 o negativa, el trigger lo detecta y bloquea la inserción*/
	/* inserted es un tabla virtual que contiene todas las filas que se están insertando en la tabla objetivo
	en este caso la tabla objetivo del trigger es "DetalleVenta" 
	 nota: inserted existe solo dentro de los triggers
	*/
	IF EXISTS (SELECT 1 FROM inserted WHERE Cantidad <=0)
	BEGIN
		RAISERROR('La cantidad debe ser mayor que cero', 16, 1);
		/*
			10: Mensaje informativo
			11-16: Errores que puede corregir el usuario
			17-25: Errores graves (recursos, sistema, etc)
		*/
		ROLLBACK;
		RETURN;
	END

	-- Si todo está bien, procedo con la inserción
	INSERT INTO DetalleVenta(IdVenta, IdLibro, Cantidad) SELECT IdVenta, IdLibro, Cantidad FROM inserted;
END;
GO
```
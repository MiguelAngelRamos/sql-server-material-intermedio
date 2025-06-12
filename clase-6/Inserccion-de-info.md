```sql
-- Productos
INSERT INTO Productos VALUES
(1, N'Laptop Dell XPS', 1200.00, 15, N'Computación'),
(2, N'Smartphone Galaxy S23', 850.00, 30, N'Telefonía'),
(3, N'Notebook Lenovo ThinkPad', 1050.00, 20, N'Computación'),
(4, N'Mouse Logitech MX', 80.00, 50, N'Accesorios'),
(5, N'Monitor LG 27"', 300.00, 25, N'Pantallas'),
(6, N'Auriculares Sony WH', 250.00, 40, N'Audio'),
(7, N'Silla Gamer Razer', 320.00, 10, N'Muebles'),
(8, N'Teclado Mecánico Corsair', 150.00, 35, N'Accesorios'),
(9, N'Cámara Web Logitech', 100.00, 22, N'Video'),
(10, N'Disco SSD Samsung 1TB', 140.00, 60, N'Almacenamiento');

-- Clientes
INSERT INTO Clientes VALUES
(1, N'Ana López', N'ana@example.com', N'Chile', '2024-01-10'),
(2, N'Carlos Soto', N'carlos@example.com', N'Argentina', '2024-02-01'),
(3, N'Lucía Torres', N'lucia@example.com', N'Perú', '2024-02-15'),
(4, N'Mario Ruiz', N'mario@example.com', N'Chile', '2024-03-10'),
(5, N'Camila Rojas', N'camila@example.com', N'México', '2024-03-25'),
(6, N'José Medina', N'jose@example.com', N'Colombia', '2024-04-05'),
(7, N'Sofía Vargas', N'sofia@example.com', N'Chile', '2024-04-15'),
(8, N'Alonso Pérez', N'alonso@example.com', N'Perú', '2024-05-01'),
(9, N'Valentina Silva', N'valentina@example.com', N'Argentina', '2024-05-12'),
(10, N'Ignacio Herrera', N'ignacio@example.com', N'México', '2024-05-20');

-- Pedidos
INSERT INTO Pedidos VALUES
(1, 1, SYSDATETIME(), 1400.00, N'Procesado'),
(2, 2, SYSDATETIME(), 150.00, N'Pendiente'),
(3, 3, SYSDATETIME(), 300.00, N'Enviado'),
(4, 4, SYSDATETIME(), 1200.00, N'Procesado'),
(5, 5, SYSDATETIME(), 250.00, N'Pagado'),
(6, 6, SYSDATETIME(), 100.00, N'Enviado'),
(7, 7, SYSDATETIME(), 320.00, N'Pendiente'),
(8, 8, SYSDATETIME(), 850.00, N'Pagado'),
(9, 9, SYSDATETIME(), 140.00, N'Procesado'),
(10, 10, SYSDATETIME(), 1050.00, N'Enviado');

-- DetallePedido
INSERT INTO DetallePedido VALUES
(1, 1, 1, 1, 1200.00),
(2, 1, 4, 1, 80.00),
(3, 2, 8, 1, 150.00),
(4, 3, 5, 1, 300.00),
(5, 4, 3, 1, 1050.00),
(6, 5, 6, 1, 250.00),
(7, 6, 9, 1, 100.00),
(8, 7, 7, 1, 320.00),
(9, 8, 2, 1, 850.00),
(10, 9, 10, 1, 140.00);

-- Pagos
INSERT INTO Pagos VALUES
(1, 1, 1400.00, N'Tarjeta de Crédito', SYSDATETIME()),
(2, 2, 150.00, N'PayPal', SYSDATETIME()),
(3, 3, 300.00, N'Tarjeta Débito', SYSDATETIME()),
(4, 4, 1200.00, N'Tarjeta de Crédito', SYSDATETIME()),
(5, 5, 250.00, N'Transferencia', SYSDATETIME()),
(6, 6, 100.00, N'PayPal', SYSDATETIME()),
(7, 7, 320.00, N'Tarjeta Débito', SYSDATETIME()),
(8, 8, 850.00, N'Tarjeta de Crédito', SYSDATETIME()),
(9, 9, 140.00, N'Criptomonedas', SYSDATETIME()),
(10, 10, 1050.00, N'Transferencia', SYSDATETIME());
```
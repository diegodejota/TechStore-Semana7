# 04 · Tipos de Instrucciones SQL para TechStore
 
## DDL · Data Definition Language
Define la estructura de la base de datos.
 
```sql
CREATE TABLE productos (
  id_producto INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(100) NOT NULL,
  categoria VARCHAR(50),
  precio DECIMAL(10,2),
  stock INT DEFAULT 0
);
 
ALTER TABLE productos ADD COLUMN descripcion TEXT;
DROP TABLE productos_temporales;
```
 
## DML · Data Manipulation Language
Manipula los datos almacenados.
 
```sql
-- Insertar un nuevo pedido
INSERT INTO pedidos (id_usuario, fecha, monto_total)
VALUES (?, NOW(), ?);
 
-- Consultar el catálogo
SELECT id_producto, nombre, precio, stock
FROM productos
WHERE stock > 0;
 
-- Actualizar el stock tras una venta
UPDATE productos
SET stock = stock - ?
WHERE id_producto = ?;
 
-- Eliminar un producto descontinuado
DELETE FROM productos WHERE id_producto = ?;
```
 
## DCL · Data Control Language
Controla los permisos de acceso.
 
```sql
-- Dar permisos al administrador
GRANT SELECT, INSERT, UPDATE, DELETE
ON techstore.* TO 'admin'@'localhost';
 
-- Quitar permisos a un usuario
REVOKE DELETE ON techstore.productos FROM 'becario'@'%';
```
 
## TCL · Transaction Control Language
Asegura que las transacciones se completen correctamente.
 
```sql
BEGIN;
  UPDATE productos SET stock = stock - 1 WHERE id_producto = 42;
  INSERT INTO pedidos (id_usuario, monto_total) VALUES (15, 599.99);
  INSERT INTO pagos (id_pedido, estado_pago) VALUES (LAST_INSERT_ID(), 'OK');
COMMIT;
-- Si algo falla: ROLLBACK; (revierte todo)
```
 
## Resumen
| Tipo | Uso | Ejemplo en TechStore |
|---|---|---|
| DDL | Crear estructura | CREATE TABLE pedidos |
| DML | Mover datos | INSERT, SELECT, UPDATE, DELETE |
| DCL | Permisos | GRANT, REVOKE |
| TCL | Transacciones | BEGIN, COMMIT, ROLLBACK |

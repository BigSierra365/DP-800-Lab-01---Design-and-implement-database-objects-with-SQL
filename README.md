# DP-800 Lab 01 – Diseño e implementación de objetos de base de datos con SQL

**Autor:** Emmanuel Grande Sierra

---

## 1. Creación de la base de datos

Creamos la base de datos `EcommerceDB` que usaremos durante todo el lab.

### 1.1. Ejecutamos `CREATE DATABASE EcommerceDB` y verificamos en el explorador de objetos que se había creado.

![1 Create a new database](<images/1 Create a new database.png>)

---

## 2. Tablas principales con restricciones

Creamos las tablas base del sistema con claves primarias, foráneas y restricciones CHECK.

### 2.1. Creamos las tablas `Supplier`, `Category` y `Product` con sus constraints e índices.

![2_1 Create core tables with constraints](<images/2_1 Create core tables with constraints.png>)

### 2.2. Insertamos los datos de ejemplo: 2 proveedores, 2 categorías y 2 productos.

![2_2 Create core tables with constraints](<images/2_2 Create core tables with constraints.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![2_2_err Create core tables with constraints](<images/2_2_err Create core tables with constraints.png>)

---

## 3. Tabla temporal para historial de precios

Creamos la tabla `ProductPrice` con versionado de sistema para guardar automáticamente el historial de cambios de precio.

### 3.1. Creamos la tabla temporal, insertamos precios iniciales y actualizamos el precio del producto 1 para generar una entrada en el historial.

![3_1 Create a temporal table for price history](<images/3_1 Create a temporal table for price history.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![3_1_err Create a temporal table for price history](<images/3_1_err Create a temporal table for price history.png>)

### 3.2. Consultamos el historial de precios con `FOR SYSTEM_TIME ALL` para ver el precio anterior y el actual con sus rangos de tiempo.

![3_2 Create a temporal table for price history](<images/3_2 Create a temporal table for price history.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![3_2_err Create a temporal table for price history](<images/3_2_err Create a temporal table for price history.png>)

---

## 4. Columnas JSON para metadatos

Añadimos una columna `Metadata` de tipo JSON a `Product` para almacenar atributos variables como color, talla o material.

### 4.1. Añadimos la columna JSON, creamos una columna calculada `MetadataColor` para indexarla y actualizamos los dos productos con sus metadatos.

![4_1 Add JSON columns for metadata](<images/4_1 Add JSON columns for metadata.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![4_1_err Add JSON columns for metadata](<images/4_1_err Add JSON columns for metadata.png>)

### 4.2. Consultamos los productos filtrando por el valor JSON del campo `color`.

![4_2 Add JSON columns for metadata](<images/4_2 Add JSON columns for metadata.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![4_2_err Add JSON columns for metadata](<images/4_2_err Add JSON columns for metadata.png>)

---

## 5. Tabla de pedidos particionada

Creamos la tabla `Order` particionada por fecha para mejorar el rendimiento en consultas históricas.

### 5.1. Creamos la función de partición `PF_OrderDate`, el esquema `PS_OrderDate`, la tabla `Order` con su índice particionado e insertamos 3 pedidos de prueba.

![5_1 Create a partitioned order table](<images/5_1 Create a partitioned order table.png>)

### 5.2. Consultamos el número de pedidos por partición con `$PARTITION.PF_OrderDate`.

![5_2 Create a partitioned order table](<images/5_2 Create a partitioned order table.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![5_2_err Create a partitioned order table](<images/5_2_err Create a partitioned order table.png>)

---

## 6. Tabla de detalle de pedidos con SEQUENCE

Creamos la tabla `OrderDetail` usando una `SEQUENCE` para generar los IDs de línea de pedido de forma independiente a la tabla.

### 6.1. Creamos la secuencia `OrderLineSequence`, la tabla `OrderDetail` con columna calculada `LineTotal` e insertamos 3 líneas de detalle con `NEXT VALUE FOR`.

![6_1 Create order details with SEQUENCE](<images/6_1 Create order details with SEQUENCE.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![6_1_err Create order details with SEQUENCE](<images/6_1_err Create order details with SEQUENCE.png>)

### 6.2. Verificamos los datos insertados con `SELECT * FROM OrderDetail`.

![6_2 Create order details with SEQUENCE](<images/6_2 Create order details with SEQUENCE.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![6_2_err Create order details with SEQUENCE](<images/6_2_err Create order details with SEQUENCE.png>)

---

## 7. Verificación de objetos

Comprobamos que todos los objetos creados funcionan correctamente.

### 7.1. Intentamos insertar un producto con precio negativo para confirmar que el CHECK constraint lo bloquea correctamente.


![7_1 Verify database objects](<images/7_1 Verify database objects.png>)

### 7.2. Verificamos las consultas de JSON, particionado y tabla temporal en un único script.


![7_2 Verify database objects](<images/7_2 Verify database objects.png>)

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

![7_2_err Verify database objects](<images/7_2_err Verify database objects.png>)

---

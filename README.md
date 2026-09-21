# DP-800 Lab 01 – Diseño e implementación de objetos de base de datos con SQL

**Autor:** Emmanuel Grande Sierra

---

## 1. Creación de la base de datos

Creamos la base de datos `EcommerceDB` que usaremos durante todo el lab.

### 1.1. Ejecutamos `CREATE DATABASE EcommerceDB` y verificamos en el explorador de objetos que se había creado.

!Evidencia

---

## 2. Tablas principales con restricciones

Creamos las tablas base del sistema con claves primarias, foráneas y restricciones CHECK.

### 2.1. Creamos las tablas `Supplier`, `Category` y `Product` con sus constraints e índices.

!Evidencia

### 2.2. Insertamos los datos de ejemplo: 2 proveedores, 2 categorías y 2 productos.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

---

## 3. Tabla temporal para historial de precios

Creamos la tabla `ProductPrice` con versionado de sistema para guardar automáticamente el historial de cambios de precio.

### 3.1. Creamos la tabla temporal, insertamos precios iniciales y actualizamos el precio del producto 1 para generar una entrada en el historial.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

### 3.2. Consultamos el historial de precios con `FOR SYSTEM_TIME ALL` para ver el precio anterior y el actual con sus rangos de tiempo.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

---

## 4. Columnas JSON para metadatos

Añadimos una columna `Metadata` de tipo JSON a `Product` para almacenar atributos variables como color, talla o material.

### 4.1. Añadimos la columna JSON, creamos una columna calculada `MetadataColor` para indexarla y actualizamos los dos productos con sus metadatos.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

### 4.2. Consultamos los productos filtrando por el valor JSON del campo `color`.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

---

## 5. Tabla de pedidos particionada

Creamos la tabla `Order` particionada por fecha para mejorar el rendimiento en consultas históricas.

### 5.1. Creamos la función de partición `PF_OrderDate`, el esquema `PS_OrderDate`, la tabla `Order` con su índice particionado e insertamos 3 pedidos de prueba.

!Evidencia

### 5.2. Consultamos el número de pedidos por partición con `$PARTITION.PF_OrderDate`.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

---

## 6. Tabla de detalle de pedidos con SEQUENCE

Creamos la tabla `OrderDetail` usando una `SEQUENCE` para generar los IDs de línea de pedido de forma independiente a la tabla.

### 6.1. Creamos la secuencia `OrderLineSequence`, la tabla `OrderDetail` con columna calculada `LineTotal` e insertamos 3 líneas de detalle con `NEXT VALUE FOR`.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

### 6.2. Verificamos los datos insertados con `SELECT * FROM OrderDetail`.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

---

## 7. Verificación de objetos

Comprobamos que todos los objetos creados funcionan correctamente.

### 7.1. Intentamos insertar un producto con precio negativo para confirmar que el CHECK constraint lo bloquea correctamente.

!Evidencia

### 7.2. Verificamos las consultas de JSON, particionado y tabla temporal en un único script.

!Evidencia

**Inconvenientes:** Saltaron los siguiente errores pero se ejecutó correctamente.

!Evidencia inconveniente

---

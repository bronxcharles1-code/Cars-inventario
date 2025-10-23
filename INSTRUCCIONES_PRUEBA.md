# Instrucciones para probar la nueva funcionalidad

## Cambios implementados ✅

Se ha mejorado el sistema de ventas para permitir **seleccionar el precio** (normal o con descuento) al momento de agregar productos al carrito.

## Cómo funciona ahora:

### 1. **Selección de Producto**
Cuando seleccionas un producto del dropdown, aparecerá automáticamente una sección con las opciones de precio.

### 2. **Opciones de Precio**
- **Precio Normal**: Se muestra siempre
- **Precio con Descuento**: Solo aparece si el producto tiene un `precio_descuento` configurado en la base de datos

### 3. **Interfaz Visual**
- ⚪ Radio buttons para elegir entre precio normal o descuento
- 🏷️ Badge "OFERTA" para el precio con descuento
- 💰 Muestra el porcentaje de ahorro
- ✨ Resaltado visual de la opción seleccionada

### 4. **En el Carrito**
- Muestra claramente qué precio se aplicó
- Si tiene descuento: muestra el precio original tachado, el nuevo precio, el porcentaje y el ahorro total
- Cada producto puede tener un precio diferente (algunos con descuento, otros sin descuento)

## Cómo probarlo:

### Paso 1: Configurar la base de datos
```sql
-- Asegúrate de que algunos productos tengan precio_descuento
UPDATE productos SET precio_descuento = 850.00 WHERE id = 1;
UPDATE productos SET precio_descuento = NULL WHERE id = 2; -- Sin descuento
```

### Paso 2: Ejecutar el servidor
```bash
# Desde la carpeta del proyecto
php -S localhost:8000
```

### Paso 3: Probar el flujo
1. Ir a http://localhost:8000/login.php
2. Iniciar sesión
3. Ir a "Registrar Ventas"
4. Seleccionar un producto CON descuento → Verás 2 opciones de precio
5. Seleccionar un producto SIN descuento → Solo verás 1 opción
6. Agregar varios productos con diferentes precios
7. Generar la factura PDF

## Ventajas de esta implementación:

✅ **Flexibilidad total**: Puedes vender el mismo producto a diferentes precios en la misma venta
✅ **Control de descuentos**: Tú decides cuándo aplicar o no el descuento
✅ **Transparencia**: El cliente ve claramente cuánto ahorra
✅ **Experiencia mejorada**: Interfaz intuitiva con feedback visual

## Archivos modificados:

- `sales.php` - Lógica completa de selección de precios y visualización del carrito

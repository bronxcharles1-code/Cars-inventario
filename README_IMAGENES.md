# Funcionalidad de Imágenes en Productos - Omega Cars

## Descripción

Se ha agregado la capacidad de cargar y visualizar imágenes para cada producto en el sistema de inventario Omega Cars.

## Características Principales

### 1. Carga de Imágenes
- **Formatos soportados**: JPG, JPEG, PNG, GIF, WEBP
- **Campo opcional**: No es obligatorio cargar una imagen
- **Tamaño de visualización**: Automático y responsive

### 2. Funcionalidades

#### Al Agregar un Producto Nuevo
- Puedes seleccionar una imagen desde tu computadora
- La imagen se sube automáticamente al crear el producto
- Se guarda en la carpeta `uploads/productos/`

#### Al Editar un Producto
- Visualizas la imagen actual (si existe)
- Puedes reemplazar la imagen subiendo una nueva
- Si no seleccionas una nueva, la imagen actual se mantiene
- Al subir una nueva imagen, la anterior se elimina automáticamente

#### En el Catálogo de Productos
- Cada tarjeta de producto muestra su imagen
- Las imágenes tienen un efecto zoom al pasar el cursor (hover)
- Diseño responsive que se adapta a diferentes pantallas

## Instalación

### Para Base de Datos Nueva
Si estás instalando el sistema por primera vez:
```sql
source db/database.sql
```

El script ya incluye el campo `imagen` en la tabla de productos.

### Para Base de Datos Existente
Si ya tienes el sistema funcionando, ejecuta el script de actualización:
```sql
source db/update_add_images.sql
```

Este script agregará la columna `imagen` a la tabla `productos`.

### Crear la Carpeta de Uploads
El sistema crea automáticamente la carpeta, pero puedes crearla manualmente:
```bash
mkdir -p uploads/productos
chmod 777 uploads/productos
```

## Estructura de Base de Datos

### Campo agregado a la tabla `productos`:
```sql
imagen VARCHAR(255) DEFAULT NULL
```

- **Tipo**: VARCHAR(255)
- **Predeterminado**: NULL
- **Descripción**: Almacena la ruta relativa de la imagen del producto

## Uso del Sistema

### Agregar Producto con Imagen

1. Ve a **"Gestión de Productos"**
2. Completa los datos del producto (marca, descripción, precio, etc.)
3. En el campo **"Imagen del Producto"**, haz clic en **"Seleccionar archivo"**
4. Elige una imagen de tu computadora (JPG, PNG, GIF o WEBP)
5. Haz clic en **"Guardar Producto"**

### Editar Imagen de un Producto

1. En el catálogo, haz clic en **"Editar"** en la tarjeta del producto
2. Verás la imagen actual en la parte superior del formulario
3. Para cambiarla, selecciona una nueva imagen
4. Haz clic en **"Actualizar Producto"**
5. La imagen anterior se eliminará automáticamente

### Visualizar Productos con Imágenes

En el catálogo de productos:
- Los productos con imagen muestran una foto destacada
- Los productos sin imagen no muestran ningún contenedor de imagen
- Al pasar el cursor sobre la imagen, esta hace un zoom suave

## Archivos Modificados

### Nuevos Archivos
- `db/update_add_images.sql` - Script SQL para agregar soporte de imágenes
- `uploads/productos/` - Carpeta para almacenar imágenes (se crea automáticamente)
- `README_IMAGENES.md` - Esta documentación

### Archivos Modificados
- `products.php` - Lógica para carga y gestión de imágenes
- `assets/css/products.css` - Estilos para visualización de imágenes
- `db/database.sql` - Schema actualizado con campo de imagen

## Detalles Técnicos

### Nomenclatura de Archivos
Las imágenes se guardan con el siguiente formato:
```
producto_{id}_{timestamp}.{extension}
```

Ejemplo: `producto_5_1698234567.jpg`

### Validaciones
- Solo se aceptan formatos: JPG, JPEG, PNG, GIF, WEBP
- La imagen se valida del lado del servidor
- Si el formato no es válido, la imagen no se carga

### Seguridad
- Validación de extensiones permitidas
- Uso de `move_uploaded_file()` para subida segura
- Eliminación automática de imágenes antiguas al actualizar
- Paths relativos para evitar vulnerabilidades

### Gestión de Espacio
- Al actualizar un producto con nueva imagen, la anterior se elimina
- Solo se mantiene una imagen por producto
- Las imágenes se almacenan fuera del control de versiones (en `uploads/`)

## Recomendaciones

### Tamaño de Imágenes
- **Resolución recomendada**: 800x800 píxeles
- **Peso máximo sugerido**: 2 MB
- **Formato preferido**: JPG o WEBP (mejor compresión)

### Buenas Prácticas
1. Usa imágenes con fondo transparente (PNG) para mejor presentación
2. Asegúrate de que las imágenes sean claras y de buena calidad
3. Mantén un tamaño de archivo razonable para carga rápida
4. Usa nombres descriptivos al seleccionar las imágenes

## Resolución de Problemas

### La imagen no se carga
- Verifica que la carpeta `uploads/productos` exista
- Verifica permisos de escritura: `chmod 777 uploads/productos`
- Revisa que el formato sea uno de los permitidos
- Verifica el tamaño máximo de carga en `php.ini`

### La imagen no se muestra
- Revisa que la ruta en la base de datos sea correcta
- Verifica que el archivo exista en `uploads/productos/`
- Comprueba permisos de lectura en la carpeta

### Error al subir imagen
- Aumenta `upload_max_filesize` en `php.ini`
- Aumenta `post_max_size` en `php.ini`
- Verifica que el formulario tenga `enctype="multipart/form-data"`

## Próximas Mejoras Sugeridas

- Compresión automática de imágenes
- Múltiples imágenes por producto (galería)
- Recorte y edición de imágenes en línea
- Vista previa antes de subir
- Soporte para imágenes desde URL
- Marca de agua automática

---

**Desarrollado para: Omega Cars Boutique** 🚗

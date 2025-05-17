# 1. Carga de Datos
ventas = [
    {"fecha": "2024-02-15", "producto": "Laptop", "cantidad": 2, "precio": 750000.00},
    {"fecha": "2024-02-15", "producto": "Mouse", "cantidad": 5, "precio": 12500.50},
    {"fecha": "2024-01-02", "producto": "Teclado", "cantidad": 3, "precio": 18500.00},
    {"fecha": "2024-01-03", "producto": "Monitor", "cantidad": 1, "precio": 130000.00},
    {"fecha": "2024-01-03", "producto": "Laptop", "cantidad": 1, "precio": 750000.00}
]

# 2. Cálculo de Ingresos Totales
ingresos_totales = 0
for venta in ventas:
    ingresos_totales += venta["cantidad"] * venta["precio"]
print("Ingresos Totales:", ingresos_totales)

# 3. Análisis del Producto Más Vendido
ventas_por_producto = {}
for venta in ventas:
    producto = venta["producto"]
    cantidad = venta["cantidad"]
    ventas_por_producto[producto] = ventas_por_producto.get(producto, 0) + cantidad

producto_mas_vendido = max(ventas_por_producto, key=ventas_por_producto.get)
print("Producto más vendido:", producto_mas_vendido, "- Cantidad:", ventas_por_producto[producto_mas_vendido])

# 4. Promedio de Precio por Producto
precios_por_producto = {}
for venta in ventas:
    producto = venta["producto"]
    cantidad = venta["cantidad"]
    ingreso = venta["cantidad"] * venta["precio"]
    if producto not in precios_por_producto:
        precios_por_producto[producto] = (0, 0)
    suma_ingresos, total_cantidad = precios_por_producto[producto]
    precios_por_producto[producto] = (suma_ingresos + ingreso, total_cantidad + cantidad)

print("Precio Promedio por Producto:")
for producto, (suma, cantidad) in precios_por_producto.items():
    promedio = suma / cantidad if cantidad != 0 else 0
    print(f"{producto}: {promedio:.2f}")

# 5. Ventas por Día
ingresos_por_dia = {}
for venta in ventas:
    fecha = venta["fecha"]
    ingreso = venta["cantidad"] * venta["precio"]
    ingresos_por_dia[fecha] = ingresos_por_dia.get(fecha, 0) + ingreso

print("Ingresos por Día:")
for fecha, ingreso in ingresos_por_dia.items():
    print(f"{fecha}: {ingreso:.2f}")

# 6. Representación de Datos
resumen_ventas = {}
for producto in ventas_por_producto:
    cantidad_total = ventas_por_producto[producto]
    ingresos_totales_producto = precios_por_producto[producto][0]
    precio_promedio = ingresos_totales_producto / cantidad_total if cantidad_total != 0 else 0
    resumen_ventas[producto] = {
        "cantidad_total": cantidad_total,
        "ingresos_totales": ingresos_totales_producto,
        "precio_promedio": round(precio_promedio, 2)
    }

print("Resumen de Ventas por Producto:")
for producto, resumen in resumen_ventas.items():
    print(f"{producto} -> Cantidad: {resumen['cantidad_total']}, Ingresos: {resumen['ingresos_totales']:.2f}, Precio Promedio: {resumen['precio_promedio']:.2f}")

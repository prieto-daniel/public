Explicación del Modelo de Datos: Escenario de Retail

Este modelo de datos ha sido diseñado específicamente para evaluar competencias en Power BI, centrándose en el modelado relacional, la creación de medidas DAX y el análisis de tendencias temporales y geográficas.

1. Arquitectura: Esquema en Estrella (Star Schema)

El modelo sigue un diseño de Esquema en Estrella, que es el estándar de oro para el rendimiento y la facilidad de uso en Power BI. Se compone de una tabla de hechos central rodeada por tablas de dimensiones.

Tablas de Dimensiones (Tablas "Dim")

Contienen los atributos descriptivos del negocio. Son las que se utilizan para filtrar, segmentar y agrupar los datos en los informes.

productos.csv: Provee el contexto sobre qué se está vendiendo (Categorías, Subcategorías).

clientes.csv: Provee el contexto sobre quién compra y dónde (Geografía, Segmento).

Tabla de Hechos (Tabla "Fact")

Contiene los eventos cuantitativos (transacciones).

ventas.csv: Registra cada venta individual, incluyendo las métricas numéricas necesarias para los cálculos.

2. Descripción de las Tablas

Ventas (Hechos)

Es la tabla principal del modelo. Cada fila representa una transacción única.

ID_Producto / ID_Cliente: Claves foráneas para relacionar con las dimensiones.

Cantidad / Precio_Unitario: Permiten calcular los ingresos brutos.

Costo_Unitario: Permite calcular el costo de lo vendido (COGS) y el margen.

Descuento_Aplicado: Introduce complejidad para calcular ingresos netos (valor decimal entre 0 y 1).

Productos (Dimensión)

ID_Producto: Clave primaria.

Categoría / Subcategoría: Permite crear jerarquías de productos (ej. Electrónica > Computadoras).

Clientes (Dimensión)

ID_Cliente: Clave primaria.

País / Ciudad: Permite crear jerarquías geográficas y visualizaciones de mapas.

Segmento: Facilita el análisis de comportamiento por tipo de cliente (VIP, Corporativo, etc.).

Fecha_Alta: Útil para calcular la antigüedad del cliente o análisis de cohortes.

3. Relaciones y Cardinalidad

Para que el modelo funcione correctamente en Power BI, se deben establecer las siguientes relaciones:

Productos 1:N Ventas: Relación de uno a muchos a través del campo ID_Producto. La dirección del filtro debe ser de Productos hacia Ventas (única).

Clientes 1:N Ventas: Relación de uno a muchos a través del campo ID_Cliente. La dirección del filtro debe ser de Clientes hacia Ventas (única).

Calendario (Sugerido): Aunque no se incluye como CSV, el postulante debería crear una tabla de fechas en Power BI (usando DAX CALENDARAUTO() o CALENDAR()) vinculada a Ventas[Fecha] para habilitar funciones de Inteligencia de Tiempo.

4. Potencial Analítico (Métricas Sugeridas)

Con este modelo, se puede evaluar la capacidad del postulante para escribir expresiones DAX:

Venta Bruta:

$$Venta\ Bruta = \sum(Cantidad \times Precio\_Unitario)$$

Venta Neta:

$$Venta\ Neta = \sum(Venta\_Bruta \times (1 - Descuento\_Aplicado))$$

Margen de Utilidad:

$$Margen = Venta\ Neta - \sum(Cantidad \times Costo\_Unitario)$$

% de Margen

Crecimiento Año tras Año (YoY): Comparación de ventas entre los periodos 2023, 2024 y 2025.

# SQL Select Fundamentals — TechStore

## ¿Por qué es mala práctica utilizar SELECT * en producción?

La instrucción:

SELECT *
FROM sales;

devuelve todas las columnas existentes en una tabla.

Puede ser útil cuando estamos explorando por primera vez una base de datos, porque permite conocer rápidamente qué información contiene una tabla.

Sin embargo, utilizar SELECT * de forma habitual en producción se considera una mala práctica por varias razones.

1. Rendimiento

Si una tabla posee muchas columnas, SELECT * devuelve información que probablemente no necesitamos.

Esto aumenta la cantidad de datos que debe leer la base de datos y también la cantidad de información que debe transferirse.

Por ejemplo, si Finanzas solamente necesita:

customer_id
product_id
total_amount

es preferible escribir:

SELECT
    customer_id,
    product_id,
    total_amount
FROM sales;

en lugar de:

SELECT *
FROM sales;

De esta manera solamente obtenemos los datos necesarios.

2. Mantenibilidad

Las tablas pueden cambiar con el tiempo.

Por ejemplo, podrían agregarse nuevas columnas a sales. Si una consulta utiliza SELECT *, esas nuevas columnas aparecerían automáticamente en el resultado, aunque no fueran necesarias.

En cambio, especificar las columnas permite saber exactamente qué información esperamos obtener y hace que la consulta sea más fácil de entender y mantener.

3. Seguridad

Una tabla puede contener información sensible que algunos usuarios no necesitan consultar.

Utilizar SELECT * podría mostrar accidentalmente columnas con información confidencial.

Seleccionar únicamente las columnas necesarias ayuda a disminuir este riesgo.

¿Por qué son importantes los alias para un stakeholder no técnico?

Los nombres de las columnas de una base de datos suelen estar diseñados pensando en criterios técnicos y no necesariamente en los usuarios del negocio.

Por ejemplo, una columna podría llamarse:

total_amount

Un usuario del área de Finanzas podría interpretar más fácilmente ese dato si utilizamos un alias como:

total_amount AS monto_total

La consulta sería:

SELECT
    total_amount AS monto_total
FROM sales;

El dato almacenado en la base no cambia. Solamente cambia el nombre con el
que se presenta la columna en el resultado de la consulta.

Otro ejemplo es:

SELECT
    order_date AS fecha_pedido,
    product_name AS nombre_producto,
    quantity AS cantidad_unidades
FROM sales;

Esto permite transformar nombres técnicos en inglés en nombres claros para
los usuarios del negocio.

Los alias facilitan la comunicación entre el análisis de datos y las distintas
áreas de una organización, ya que permiten entregar información con nombres
comprensibles sin modificar la estructura original de la base de datos.


### 3. Tu repositorio debería quedar así

```text
sql-select-fundamentals/
│
├── consultas_basicas.sql
└── README.md

Y el repositorio de GitHub debe llamarse exactamente:

sql-select-fundamentals

y configurarse como público.

4. Qué deberías obtener en cada consulta

La Consulta 1 muestra las 9 columnas:

order_id
order_date
customer_id
product_id
product_name
category
quantity
unit_price
total_amount

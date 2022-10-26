# WorkShop 3

## Preparando el ambiente

Entramos a Mysql
`sudo mysql`

Creamos la DB
`create database northwind`

Creamos un usuario
`create user user_laravel identified by "12345"`

Le damos permisos
` grant all privileges on northwind.\* to user_laravel`

Habilitamos las conexiones remotas de mysql
`nano /etc/mysql/mariadb.conf.d/50-server.cnf`

Y comentamos la linea

```
# bind-address = 127.0.0.1
```

Reiniciamos mariadb
`sudo systemctl restart mysql`

Cargamos nuestro backup
`mysql northwind > northwind.sql`
`mysql northwind > northwind-data.sql`

Nos conectamos desde la maquina local con un gestor como DBEAVER o TABLEPLUS

# Challenges

## Challenge 1

Recupere el código (id) y la descripción (type_name) de los tipos de movimiento de inventario (inventory_transaction_types).

```
SELECT id as "Codigo", type_name as "Description" FROM inventory_transaction_types
```

## Challenge 2

Recupere la cantidad de ordenes (orders)
registradas por cada vendedor (employees).

```
SELECT
CONCAT(e.first_name, " ", e.last_name) as `Vendedor`,
COUNT(1) as `Cantidad`
from orders o
join employees e
on e.id = o.employee_id
GROUP BY `Vendedor`
ORDER BY e.id
```

## Challenge 3

Recupere la lista de los 10 productos más ordenados (order_details),
y la cantidad total de unidades ordenadas para cada uno de los
productos.
Deberá incluir como mínimo los campos de código (product_code),
nombre del producto (product_name) y la cantidad de unidades.

```
select p.product_code as `Codigo`,
        p.product_name as `Producto`,
        round(sum(od.quantity),2) as `Cantidad`
        from products p
        join order_details od
            on od.product_id = p.id
        group by p.id
        order by `Cantidad` DESC
        limit 10;
```

## Challenge 4

Recupere el monto total (invoices, orders, order_details, products) y la
cantidad de facturas (invoices) por vendedor (employee). Debe
considerar solamente las ordenes con estado diferente de 0 y
solamente los detalles en estado 2 y 3, debe utilizar el precio
unitario de las lineas de detalle de orden, no considere el descuento,
no considere los impuestos, porque la comisión a los vendedores se
paga sobre el precio base.

```
select count(1) as `Cantidad`,
		concat(e.first_name, ' ', e.last_name) as `Vendedor`,
        round(sum(od.unit_price * od.quantity),2) as `Monto`
        from employees e
        join orders o
        	on o.employee_id = e.id
        join order_details od
        	on od.order_id = o.id
        where o.status_id <> 0
        	and od.status_id in (2,3)
        group by e.id
        order by `Cantidad` DESC, e.first_name ASC;
```

## Challenge 4

Recupere el monto total (invoices, orders, order_details, products) y la
cantidad de facturas (invoices) por vendedor (employee). Debe
considerar solamente las ordenes con estado diferente de 0 y
solamente los detalles en estado 2 y 3, debe utilizar el precio
unitario de las lineas de detalle de orden, no considere el descuento,
no considere los impuestos, porque la comisión a los vendedores se
paga sobre el precio base.

---

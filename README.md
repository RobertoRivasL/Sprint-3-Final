# Sprint-3-Final

Este Sprint trata de una base datos con clientes, proveedores y productos. Indudablmente faltaba algo para conectar a estas tablas, por tanto se hizo una tabla intermedia entre productos y proveedores, se agrego una tabla de pedidos de clientes.

Se contestaron las siguientes preguntas :

-- Cuál es la categoría de productos que  más se repite.

select categoria_de_productos, count(*) total
 from productos   
 group by categoria_de_productos
 order by count(*) desc limit 1;
 
 -- La categoria que mas se repite es : computacion
 
 -- Cuáles son los productos con mayor  stock

select nombre, stock from productos
where stock = (select max(stock) from productos);

-- el producto con mayor stock es : Blusa Mujer Lesage, 60 unidades


-- Qué color de producto es más común en nuestra tienda.

select color, count(*) total from productos
group by color
order by count(*) desc limit 1;

-- el color es negro.


-- Cual o cuales son los proveedores con menor stock de productos. (error)

select * from proveedores as prov;
select * from productos as pro;
select pro.nombre, pro.stock, pro.SKU, prov.nombre_corporativo from productos as pro
inner join proveedores as prov on pro.categoria_de_productos = prov.categoria_de_productos
where pro.stock = (select min(pro.stock) from productos) limit 1;

-- otra forma sria :

select nombre, stock, categoria_de_productos from productos  
where stock = (select min(stock) from productos);  -- Encontramos el stock minimo en la tyabla productos
select * from proveedores where categoria_de_productos = "computacion"; -- mostramos los datos del proveedor del cual tenemos pocos productos

-- El proveedor con menos productos en stock seria : 18.232.782-4

select * from proveedores where id_proveedor = "18232782-4";

-- Su nombre corporativo seria : Tecnoglobal S.A.


-- Cambien la categoría de productos más popular por ‘Electrónica y computación’.

select nombre, stock, categoria_de_productos from productos where stock = (select max(stock) from productos);

-- El producto con mas stock es : Blusa Mujer Lesage con  60 unidades de la categoria : ropa mujer

-- Procedemos a cambiar de categoria el producto

select * from productos where nombre = 'Blusa Mujer Lesage';
update productos set categoria_de_productos = "Electrónica y computación" where nombre = 'Blusa Mujer Lesage';

-- Se realizo el cambio de categoria para el producto con exito


-- Grupo Sala 7 : Vannya Riffo, Ignacio Ulloa, Mauro Boccardo, Roberto Rivas


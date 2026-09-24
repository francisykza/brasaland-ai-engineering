# Elección de empresa

## Empresa elegida: Brasaland

He elegido **Brasaland**, la cadena de 14 restaurantes a la brasa con locales en Colombia y Florida.

## Por qué Brasaland

Lo que más me llamó la atención es que Brasaland es rentable y tiene clientes fieles, pero funciona con herramientas pensadas para un solo restaurante. Los pedidos de materia prima se hacen por WhatsApp sin datos de inventario detrás, y Mariana Restrepo toma decisiones con un PDF que llega los martes. Hay muchísimo margen para mejorar con automatización sin tener que inventarse el problema.

Me gusta también que el dominio se entiende a la primera. Todo el mundo sabe cómo funciona un restaurante, y eso me permite centrarme en la parte técnica y explicar el valor de lo que construya a alguien no técnico, como Mariana.

Por último, la parte multipaís (COP y USD, español e inglés, dos sistemas de punto de venta distintos) me parece un reto realista. Obliga a diseñar bien los datos desde el principio, en lugar de hacer algo que solo funcione en un local.

## Departamentos que me parecen más interesantes

**1. Operaciones de Restaurante (Felipe Guerrero)**
Los 14 locales funcionan casi aislados. Felipe no sabe en tiempo real cuánto vende cada local, y los pedidos de ingredientes por WhatsApp o teléfono provocan exceso de stock en unos locales y roturas en otros. El procedimiento interno dice que ningún local debe bajar de 3 días de inventario de proteínas, y que un pedido de emergencia lleva un recargo del 8%. Si nadie ve el stock, esos pedidos de emergencia son dinero que se pierde cada semana.

**2. Compras y Proveedores (Lucía Fernández)**
Lucía negocia con unos 20 proveedores en dos países por email y Excel, y se entera de las subidas de precio cuando llega la factura. No hay ningún dato consolidado de compras a nivel de cadena, así que no puede negociar volumen conjunto. Además, tiene que aprobar a mano cada pedido de emergencia que supere los 500 USD.

**3. Formación y Estándares de Calidad (Jake Morrison)**, como mención extra
Las recetas están en un Google Drive que nadie sabe navegar, y comunicar un cambio de receta a los 14 locales en dos idiomas tarda días. Es un caso muy claro para búsqueda semántica (RAG).

## Reto de automatización que más ganas tengo de construir

El **sistema inteligente de pedidos de ingredientes basado en ventas históricas y stock actual**, que aparece en las necesidades de Operaciones de Restaurante. Conecta directamente con Compras, porque genera los datos consolidados que Lucía no tiene hoy.

## Mi idea de Agente de IA / My AI Agent Idea

**Agente de Pedidos Semanales de Ingredientes**

**Qué haría:**
Cada lunes a primera hora, antes de las 10:00 de cada local (la hora límite del procedimiento de pedidos), el agente prepara un **borrador de pedido semanal para cada uno de los 14 locales**:
- Estima cuánto va a vender cada local esa semana a partir de sus ventas de semanas anteriores.
- Lo compara con el stock actual y calcula cuánto pedir de cada categoría (proteínas, vegetales, bebidas y empaques, salsas importadas), respetando la frecuencia y el plazo de entrega de cada una.
- Comprueba que ningún local quedará por debajo de **3 días de inventario de proteínas** antes de la siguiente entrega. Si va a pasar, lo avisa con tiempo para evitar el pedido de emergencia con recargo del 8%.
- No hace el pedido por su cuenta: envía el borrador al gerente del local para que lo revise y lo confirme.

**Qué información necesitaría:**
- Ventas históricas por local y por plato, de los sistemas de punto de venta de Colombia y de Florida.
- Stock actual de cada local.
- Registro de desperdicio de cada local (vencimiento, error de cocina, merma no explicada), para no confundir merma con consumo.
- Catálogo de los ~20 proveedores con precios, categorías y plazos de entrega.
- Calendario de pedidos: proteínas semanal, vegetales lunes y jueves, bebidas y empaques quincenal, salsas importadas mensual.

**Qué produciría o desencadenaría:**
- Un borrador de pedido por local, enviado al gerente por email o WhatsApp para que lo apruebe o lo ajuste.
- Si un pedido de emergencia supera los **500 USD** (o su equivalente en COP), una solicitud de aprobación automática a **Lucía Fernández** con el motivo.
- Un resumen semanal consolidado para Lucía con el gasto total por proveedor y por país, y los productos cuyo precio ha subido respecto a semanas anteriores, para que pueda negociar a nivel de cadena.
- Una alerta a **Felipe Guerrero** si un local pide mucho más o mucho menos de lo esperado según sus ventas. Podría indicar un error, merma o un problema en ese local.

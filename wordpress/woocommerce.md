## Añadir marcas o proveedores a los productos

#### Plugin Perfect Woocommerce Brands

Con el plugin vamos a poder realizar las siguientes acciones:

    i.- Crear marcas
    ii.- Asignar marca a cada producto
    iii.- Utilizar widgets especiales para listar marcas y filtrar productos por marca
    iv.- Añadir carrusel de marcas + filtro
    vi.- creación automática de página de marca en la que se mostrarán los productos que pertenecen a dicha marca
    
    
https://www.tiendaonlinemurcia.es/como-poner-marcas-de-productos-o-fabricantes-en-woocommerce/

[Video](https://www.youtube.com/watch?time_continue=1&v=qE3bzs7bCCw&feature=emb_logo)

#### Control de stock

Como activar el control de stock y varios plugin que nos pueden servir

https://www.webempresa.com/blog/control-stock-woocommerce.html




## Utilizar API REST PARA CRUD DE PRODUCTOS DESDE EL FRONT-END

- API Documentation: https://woocommerce.github.io/woocommerce-rest-api-docs/?javascript#create-a-product

https://decodecms.com/como-usar-la-rest-api-de-woocommerce/


### Ejemplo de cómo crear un producto
Crear productos es muy similar a crear publicaciones con la API REST de WordPress. Solo difieren los parámetros.

Para obtener KEY:SECRET seguir los pasos.

![alt text](https://rudrastyh.com/wp-content/uploads/2017/10/woocommerce-rest-api-keys.gif)

        $api_response = wp_remote_post( 'https://your-website/wp-json/wc/v2/products', array(
            'headers' => array(
                'Authorization' => 'Basic ' . base64_encode( 'KEY:SECRET' )
            ),
            'body' => array(
                'name' => 'My test2', // product title
                'status' => 'draft', // product status, default: publish
                'categories' => array(
                    array( 
                        'id' => 5 // each category in a separate array
                    ),
                    array(
                        'id' => 10
                    )
                ),
                'regular_price' => '9.99' // product price
                // more params http://woocommerce.github.io/woocommerce-rest-api-docs/?shell#product-properties
            )
        ) );
        
        $body = json_decode( $api_response['body'] );
        //print_r( $body );
        
        if( wp_remote_retrieve_response_message( $api_response ) === 'Created' ) {
            echo 'The product ' . $body->name . ' has been created';
        }

Fuente: https://rudrastyh.com/woocommerce/rest-api-create-update-remove-products.html

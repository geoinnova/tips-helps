### Actualiza todos los pedidos con estado de procesamiento a completado
Esto es necesario porque los tickets son productos virtuales y no se pueden descargar

    public function update_order_status_to_completed($order_id)
    {
        global $woocommerce;

        // Payment gateway ids
        $paymentMethods = array('paytpv', 'paypal');

        if ( !$order_id ) return;
        $order = new WC_Order( $order_id );

        if ( !in_array( $order->payment_method, $paymentMethods ) ) return;
        $order->update_status('completed');
    }
  
### Función para quitar el telefono del formulario de checkout.
Sólo está en billing hook woocommerce_checkout_fields

    public function remove_phone_billing_checkout_field($fields)
    {
      unset($fields['billing']['billing_phone']);
      unset($fields['order']['order_comments']); // notas - info adicional
      return $fields;
    }

## Eliminar campos  del formulario de checkout a la hora de comprar (woocommerce)
woocommerce_default_address_fields > modificar tanto billing como shipping
 
    public function remove_checkout_fields($fields)
    {
        unset($fields['company']);
        unset($fields['address_1']);
        unset($fields['address_2']);
        unset($fields['billing']['billing_phone']);
        unset($fields['city']);
        unset($fields['postcode']);
        unset($fields['country']);
        return $fields;
    }

## current_user_can( string $capability, mixed $args )

Devuelve si el usuario actual tiene la capacidad especificada.

    if (current_user_can('edit_others_posts')) {
        /**
         * add the delete link to the end of the post content
         */
        add_filter('the_content', 'erb_generate_delete_link');

        /**
         * register our request handler with the init hook
         */
        add_action('init', 'erb_delete_post');
    }
Capacidades y roles: https://wordpress.org/support/article/roles-and-capabilities/


## add_query_arg( $args )

Puede reconstruir la URL y agregar variables de consulta a la consulta de URL utilizando esta función. Hay dos formas de utilizar esta función; ya sea una única clave y valor, o una matriz asociativa.

    add_query_arg( 'key', 'value', 'http://example.com' );

    $url = add_query_arg(
                [
                    'action' => 'erb_frontend_delete',
                    'post'   => get_the_ID(),
                ],
                home_url()
            );

Url devuelta: http://wordpress.vm/?action=erb_frontend_delete&post=12

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

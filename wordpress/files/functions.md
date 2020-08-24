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

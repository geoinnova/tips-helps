### JSON CATEGORÍAS DE EVENTOS PLUGIN EVENTON


Creación de endpoint personalizado para la REST API de Wordpress, recibe un parámetro en la url (musica || teatro)


        // Registramos una ruta nueva para la rest api
        add_action( 'rest_api_init', function () {
		register_rest_route( 'erb/v2', '/events-categories/(?P<tipo>(musica|teatro))',
		array(
			'methods' => 'GET', 
			'callback' => 'erb_events_categories'
		)
	    );
        });


Función que devuelve json con los id y categorías de los eventos (eventon)
    
        function erb_events_categories(){
          global $wpdb;
          $query = "SELECT t.name, t.term_id 
                    FROM wp_terms AS t 
                      INNER JOIN wp_term_taxonomy AS tt 
                      ON t.term_id = tt.term_id AND tt.taxonomy='event_type_2'";
          $categories = $wpdb->get_results($query);

          $events_categories = array();

          foreach ($categories as $category) {
            array_push($events_categories, array(
              'id_category' => $category->term_id,
              'name_category' => $category->name)
            );
          }

          echo json_encode($events_categories);
        }
  
  La misma funcion pero devolviendo todos los datos
  
          function erb_events_categories(){
          global $wpdb;
          $query = "SELECT * 
                    FROM wp_terms AS t 
                      INNER JOIN wp_term_taxonomy AS tt 
                      ON t.term_id = tt.term_id AND tt.taxonomy='event_type_2'";
             $categories = $wpdb->get_results($query);

             echo json_encode($categories);
          }
  
  llamada: https://abasedemusica.es/agenda/wp-json/erb/v2/events-categories
  

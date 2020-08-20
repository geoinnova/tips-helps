### JSON CATEGORÍAS DE EVENTOS PLUGIN EVENTON


Creación de endpoint personalizado para la REST API de Wordpress
devuelve json con los id y categorías de los eventos (eventon)

    
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
  

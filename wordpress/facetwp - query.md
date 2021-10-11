## order random


  $args = [
        "post_type" => [
          "jma_entidades"
        ],
        "post_status" => [
          "publish"
        ],
        'orderby' => 'rand',
        "posts_per_page" => 10,
      "meta_query" => [
          [
            "key" => "url_entidad",
            "compare" => "EXISTS",
            "type" => "CHAR"
          ]
        ],
        'tax_query' => array(
                    'relation' => 'AND',
                     array(
                         'taxonomy' => 'cat_categoria_entidad',
                          'field'    => 'slug',
                          'terms'    => 'clientes',
                      ),)
      ];
      return $args;

### single_jma_cursos

    // AÑADIR MARCADO SCHEMA
    add_action('wp_head', 'addschema_producto'); //Add Schema to header
    function addschema_producto() //Function for Schema.org
    {

      $title = get_the_title( $post_id);
      $thumbID = get_post_thumbnail_id( $post->ID );
      $imgDestacada = wp_get_attachment_image_src( $thumbID, 'full' );
      $excerpt = get_the_excerpt();
      $url = get_permalink();
      $precio = get_field('precio');


    echo '<script type="application/ld+json">
    {
      "@context": "https://schema.org/", 
      "@type": "Product", 
      "name": "'. $title .'",
      "image": "' . $imgDestacada[0] . '",
      "description": "'. $excerpt .'",
      "brand": "Geoinnova",
      "offers": {
        "@type": "Offer",
        "url": "' . $url . '",
        "priceCurrency": "EUR",
        "price": "' . $precio . '",
        "availability": "https://schema.org/LimitedAvailability"
      },
      "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.9",
        "ratingCount": "165"
      } 
    }
    </script>';
    
 Hay que tomar los siguientes datos de forma dinánimica desde ekomi
 
        "ratingValue": "4.9",
        "ratingCount": "165"
 
https://www.ekomi.es/testimonios-geoinnova.html


## getSnapshot (public)
Para obtener los datos necesarios utilizar esta url de la API https://ekomi01.atlassian.net/wiki/spaces/KB/pages/2113339432

De los datos devueltos:

    {
        "info": {
            "fb_count": "419",
            "fb_avg": "4.3",
            "fb_avg_detail": "4.27",
            "active": true,
            "account_name": "test test",
            "ekomi_certificate": "https:\/\/www.ekomi.de\/cert\/4090571468444361",
            "ekomi_certificate_id": "4090571468444361",
            "ekomi_certificate_seo": "https:\/\/www.ekomi.co.uk\/review-ekomi-testelino2.html"
        },

**"fb_count": "419",
"fb_avg": "4.3",**

### single_jma_cursos

#### obtener json desde php https://www.it-swarm-es.com/es/php/llamar-rest-api-en-php/941947080/

    <?php
    $response = file_get_contents('http://api.ekomi.de/v3/getSnapshot?auth=665|FMJuyuC8uEbo3WxRa5aG&version=cust-1.0.0&type=json&charset=utf-8');
    $response = json_decode($response);
    $ratingCount = $response->info->fb_count;
    $ratingValue = $response->info->fb_avg;
    echo "ratingCount: ".$ratingCount;
    echo "<br>";
    echo "ratingValue: " .$ratingValue;

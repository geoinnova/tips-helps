
## Etiquetas og
https://ayudawp.com/open-graph-jetpack/

### Eliminar caché de FB
https://developers.facebook.com/tools/debug/


### Eliminar caché de linkein
https://www.linkedin.com/post-inspector/inspect/https:%2F%2Fgeoinnova.org%2Fplanero-web%2F

### Eliminar caché de twitter
https://cards-dev.twitter.com/validator
*posible problema con el isp https://wordpress.org/support/topic/unable-to-render-card-preview-twitter/


### Eliminar caché de telegrama
Use @webpagebot
https://telegram.me/webpagebot

## Fundamental para que funcione correctamete todo en wordpress

No utilizar plugin All in One SEO > utilidad Social Meta

Incluir las meta desde el theme-child de nuestro theme
copiar en el *head* el código:

    <meta name="title" content="María Sáez" />
    <meta name="description" content="Web oficial de María Sáez, con toda la info de la cantante y compositora española" />
    <meta name="twitter:url" content="https://mariasaez.com/" />
    <meta name="twitter:description" content="Web oficial de María Sáez, con toda la info de la cantante y compositora española" />
    <meta name="og:title" content="María Sáez" />
    <meta name="og:description" content="Web oficial de María Sáez, con toda la info de la cantante y compositora española" />
    <meta name="og:url" content="https://mariasaez.com/" />
    
    <!-- Esta actúa tambien para wasap, Whatsapp no admite imágenes con un tamaño superior a 300 KB.-->
    <meta name="og:image" content="https://mariasaez.com/wp-content/uploads/2020/07/ms-cabecera-wasap.jpg" />
    <meta name="twitter:card" content="summary_large_image" />
    <!--<meta name="twitter:site" content="@mariasaez" />-->
    <meta name="twitter:image" content="https://mariasaez.com/wp-content/uploads/2020/07/ms-cabecera.jpg" />
    <meta name="robots" content="index, follow" />
    <meta name="locality" content="Spain" />
    <meta name="organization" content="María Sáez" />

En mi caso lo he incluido dentro del archivo header.php y se sube en el raiz del theme-child

**Importante: Whatsapp no admite imágenes con un tamaño superior a 300 KB

## Error en twitter: ERROR: Fetching the page failed because it's denied by robots.txt.
El problema estaba en que como este wordpress estaba montado sobre un subdirectorio (/vo) y en el raiz había otro robot.txt, el del raiz tenía bloqueado.

**Incluir esto en robot.txt del raiz

    # Allow twitter bot
    User-agent: Twitterbot
    Allow: /vo/

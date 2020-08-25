### Comprobar nombre navegador y redireccionar

    <script src="https://cdnjs.cloudflare.com/ajax/libs/bowser/1.9.4/bowser.min.js"></script>
    <script>
        var navegador = bowser.name;
        console.log(navegador, bowser.version);

        if((navegador.indexOf("Chrome"))>-1){
        window.location="https://rabasco-developer.es/";
         jQuery(document).ready(function( $ ) {
          $('#instagram').css({"background-color": "red"});

        });
     </script>

Dentro de wordpress - Se comprueba si la web se está ejecutando dentro de un iframe o no

    <script>
      var iFrameDetection = (window === window.parent) ? false : true;
      if (iFrameDetection){
        jQuery(document).ready(function( $ ) {
           console.log("no está definida");
           window.location="https://rabasco-developer.es/";
        }); 
    </script>

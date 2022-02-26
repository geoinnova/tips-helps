## Checkear si una url hay una imagen
```js
function checkImage(urlImg) {
    // console.log("urlImg", urlImg);
    const request = new XMLHttpRequest();
    request.open("GET", urlImg, true);
    request.send();
    request.onload = function (e) {
        // if (request.status == 200 ) //if(statusText == OK)
        if (e.target.response != '') {
            console.log("existe imagen");
        } else {
            console.log("No existe la imagen");
        }
    }
}
```
## Chequear si existe una imagen desde una llamada a un proxy externo
```js
const existImg = (urlImg) =>
  new Promise((resolve, reject) => {
    fetch('http://urlproxy/proxy.php?function=imageExist&url='
    + encodeURIComponent(urlImg))
        .then(response => response.json())
        .then(data => {
          let resultado = data;
          // Resolvemos la Promise con el array 
          // elements ya procesado
          resolve(resultado);
        })
        // Capturamos el error en caso de haber uno
        .catch(reject);
  });
 ```
 Devuelve una promesa.
 
  

## arrays asociativos
```js
const configColor = {
    FO: { color: '#44ea8e', descripcion: 'Formación', url: 'https://geoinnova.org/cursos/' },
    IG: { color: '#1473aa', descripcion: 'SIG-Desarrollo', url: '#' },
    PA: { color: '#4eb7b7', descripcion: 'Proyectos Ambientales', url: 'https://geoinnova.org/consultoria-medio-ambiente/' },
    TU: { color: '#ff6600', descripcion: 'Turismo', url: 'https://geoinnova.org/servicios-consultoria-turismo-sostenible/' }
};
```

llamada
```js
color: configColor[element.codtipo].color,
```

## Serializar un objeto en una lista de parámetro de consulta de URL
// con js vanilla > let url = new **URLSearchParams(defaultParameters).toString()**;

// https://stackoverflow.com/questions/6566456/how-to-serialize-an-object-into-a-list-of-url-query-parameters

         const defaultParameters = {
                service: 'WFS',
                version: '1.0.0',
                request: 'GetFeature',
                typeName: `vse:${wfsLayer}`,
                maxFeatures: 200,
                outputFormat: 'text/javascript',
                format_options: 'callback:getJson',
                SRSNAME: 'EPSG:3857',
                FEATUREID: `${wfsLayer}.${searchField}`,
            };

           

             const url = URLSearchParams(defaultParameters).toString());





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

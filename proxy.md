## Javascript

    // Capa catastro

    const catastro = new OlLayerImage({
        name: 'Catastro',
        extent: extent,
        source: new ImageWMS({
          url: "https://inspire.navarra.es/services/CP/wms",
          crossOrigin: "anonymous",
          attributions:
            'Base © <a href="https://www.geo.admin.ch/internet/geoportal/' +
            'en/home.html">PNOA</a>',
          params: { LAYERS: "CP:CadastralParcel" },
          //serverType: "mapserver",
        }),
      });
  
  
       if (url) {
           //parseo la url para enviarla al proxy
            const referencia = **encodeURIComponent(url)**;

            //paso la url por get al proxy
            fetch('https://planero-web.geoinnova.org/proxy/proxy.php?referencia='+**referencia**,
            )
            .then(res => res.json())
            .then(data =>{


              contentPopup.innerHTML = '';
              popup.setPosition(evt.coordinate);
              // si el nivel de zoom es superior a 14.80 se activa la referencia catastral
              if (getZoomView(map) > 14.80) {

              //console.log("datos de vuelta: ",**data**)
              contentPopup.innerHTML=**data**;
              } else {
                contentPopup.innerHTML += '<div class="erb-table-wms--alert"> ¡¡ No existen datos para este nivel de zoom !!</div>';
              }
            })
         }
        
        
    ## proxy.php
    
      // la url viene de javascrip codificada con encodeURIComponent(url) hay que decodificarla en php con urldecode

      $referencia = **urldecode**($_GET['referencia']); 

      $fichero = file_get_contents("$referencia");


      header("Access-Control-Allow-Origin:*");
      header('Content-type: application/json');
      echo **json_encode**($fichero);

      exit;

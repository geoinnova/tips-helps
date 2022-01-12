## Problema de importaciones con ejemplos OpenLayers
1. incluir type="module" en la llamada del script en index.html

      <script type="module" src="main.js"></script>


### Impresión con ctrl+ arrastre ratón

  //*****************************************++ para impresion
  const dragBox = new DragBox({
      condition: platformModifierKeyOnly,
    });

  map.addInteraction(dragBox);

  //selección
  dragBox.on('boxend', function () {

     let extent = dragBox.getGeometry().getExtent();

     console.log(extent)

    // map.getView().setCenter(coordinates);

  //   //Añade un botón para ampliar zona seleccionada
  //   const zoomToExtentControl = new ZoomToExtent({
  //     extent: extent
  //   });
  //   map.addControl(zoomToExtentControl);

    let extentView = map.getView().calculateExtent(map.getSize());
    //let extentView = map.getView().getProjection().getExtent(); //extend initial de la vista
    console.log(extentView);
    map.getView().fit(extent);


    //Impresión
    spinner.classList.remove("hidden");
    window.setTimeout(imprimirArea, 5000);
    window.onafterprint = function(){
      console.log("Printing completed...");
      map.getView().fit(extentView);
   }


  function imprimirArea(){
      spinner.classList.add("hidden");
      javascript: window.print();

  }

    //window.setTimeout( map.getView().fit(extentView), 12000);

  });

    // clear selection when drawing a new box and when clicking on the map
  dragBox.on('boxstart', function () {
        //zoomAntesImpresion = map.getView().getZoom();
        //console.log("entra")

  });



  

### VectorLayer, obtener datos (source) de GeoJson externo o con constante
  //obtención de los puntos desde una constante geoJson
  const vectorSource = new VectorSource({
      features: new GeoJSON().readFeatures(geoJsonData, { featureProjection: get('EPSG:3857') }),
  });

  const vectorLayer = new VectorLayer({
      name: 'Info xample',
      source: vectorSource,
      style: selectIcon,
  });

/*
  //obtención de los puntos desde un geoJson externo
  const vectorLayer = new VectorLayer({
      name: 'vector Layer nuevo',
      source: new VectorSource({
          format: new GeoJSON(),
          //url: './data/4_1_1.js'
          //url: 'http://visores.geoinnova.org/planero-react/4_1_1.js'
          //url: 'https://gist.githubusercontent.com/neogis-de/154f4bd155f77e0f3689/raw/5a1642fac4afff463c3ff08beaad55892fe9acd4/geojson.js'
      }),
      style: selectIcon,
  });
*/


//configuración del icono y color según característica
  const selectIcon = (feature) =>{
    let bgColors = {
        35100018:'#6aff00', // sifonico
        35100019:'red',     // arqueta
        35100023:'green',
        35100004:'#d1ba5e',    
     } ;

    const codigo = feature.get('Codigo'); 
    const myStyle = new Style({
      image: new CircleStyle({
        radius: 5,
        fillColor: '#da2122',
        color: '#000000',
        dashArray: '',
        opacity: '1.0',
        fillOpacity: '1.0',
        stroke: new Stroke({ color: 'white', width: 1 }),
        fill: new Fill({color: bgColors[codigo]})
      }),
    });
    return myStyle;
  }

### Varias funciones:
 const feature = map.forEachFeatureAtPixel(evt.pixel,
        function(feature) {
            return feature;
        });

//obtener coordenadas de una caracteristica de un geoJson al pulsar sobre el mapa
feature.getGeometry().getCoordinates()[0];

Sobre feature:
* feature.get('TIPO') //obtiene la propiedad con clave "tipo"
* feature.getProperties() //obtiene todas las propiedades
*
recorrer todas la propiedades:

     var objeto = feature.getProperties(),propiedades;
              for (propiedades in objeto) {
                console.log (propiedades + ''+ objeto[propiedades]+'</b></i><br />');
                }
 
Sobre el mapa:
* Centrar sobre coordenadas: map.getView().setCenter(coordinates);
* 
Popup: popup.setPosition(coordinates); 

### Estilos según geometrías
    // estilos para geometrías
      const image = new CircleStyle({
        radius: 5,
        fillColor: '#da2122',
        color: '#000000',
        dashArray: '',
        opacity: '1.0',
        fillOpacity: '1.0',
        stroke: new Stroke({ color: 'white', width: 1 }),
        fill: new Fill({color: 'red'})
      });


      const styles = {
        'Point': new Style({
            image: image,
        }),
        'LineString': new Style({
            stroke: new Stroke({
                color: 'green',
                width: 8,
            }),
        }),
        'MultiLineString': new Style({
            stroke: new Stroke({
                color: 'green',
                width: 5,
            }),
        }),
        'MultiPoint': new Style({
            image: image,
        }),
        'MultiPolygon': new Style({
            stroke: new Stroke({
                color: 'yellow',
                width: 5,
            }),
            fill: new Fill({
                color: 'rgba(255, 255, 0, 0.1)',
            }),
        }),
        'Polygon': new Style({
            stroke: new Stroke({
                color: 'blue',
                lineDash: [4],
                width: 5,
            }),
            fill: new Fill({
                color: 'rgba(0, 0, 255, 0.1)',
            }),
        }),
        'GeometryCollection': new Style({
            stroke: new Stroke({
                color: 'magenta',
                width: 5,
            }),
            fill: new Fill({
                color: 'magenta',
            }),
            image: new CircleStyle({
                radius: 10,
                fill: null,
                stroke: new Stroke({
                    color: 'magenta',
                }),
            }),
        }),
        'Circle': new Style({
            stroke: new Stroke({
                color: 'red',
                width: 5,
            }),
            fill: new Fill({
                color: 'rgba(255,0,0,0.2)',
            }),
        }),
      };
      
     //llamada
      const styleFunction = function(feature) {
            // console.log(feature.get('Codigo'))
            return styles[feature.get('Codigo')];
            // return styles[feature.getGeometry().getType()];
          };

### Comprobar si existe previamente una capa VectorLayer
https://gis.stackexchange.com/questions/240372/how-do-i-get-all-the-layer-vectors-added-to-a-map-in-openlayers-3

    // Comprobamos si hay alguna capa anterior VectorLayer
    map.getLayers().forEach(function(layer) {
        if (layer instanceof VectorLayer) {
            map.removeLayer(layer);
        }
    });

### Borrar datos de una capa vector
How can I clear a vector layer features in OpenLayers 4?
https://gis.stackexchange.com/questions/251770/how-can-i-clear-a-vector-layer-features-in-openlayers-4

    layerVector.getSource().clear();
    
### ¿Desactivar la herramienta de medición en OpenLayers 5? 
https://gis.stackexchange.com/questions/24879/measuring-on-openlayers-map
** https://gis.stackexchange.com/questions/321943/deactivating-measurement-tool-in-openlayers-5


###  serializar un objeto en una lista de parametros de consulta de URL ---- $.param(objeto) ---- con jquery y ---- new URLSearchParams(defaultParameters).toString(); ---- con jsvanilla
    // con js vanilla > let url = new URLSearchParams(defaultParameters).toString();
    // service=WFS&version=1.0.0&request=GetFeature&typeName=vse%3Ahigh_voltage_lines&maxFeatures=200&outputFormat=text%2Fjavascript&format_options=callback%3AgetJson&SRSNAME=EPSG%3A3857&FEATUREID:high_voltage_lines.130
    // https://stackoverflow.com/questions/6566456/how-to-serialize-an-object-into-a-list-of-url-query-parameters

### WFS obtener URL y hacer zoom 
https://progworks.tistory.com/22
https://gis.stackexchange.com/questions/30595/how-to-zoom-to-object-on-wms-layer-with-openlayers
const zoom2WFS = (wfsLayer, searchField, resultLayer, map) => {

    const rootUrl = CONF.wfssoller;
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

    // serializa un objeto en una lista de parametros de consulta de URL ---- $.param(objeto) ----
    // con js vanilla > let url = new URLSearchParams(defaultParameters).toString();
    // service=WFS&version=1.0.0&request=GetFeature&typeName=vse%3Ahigh_voltage_lines&maxFeatures=200&outputFormat=text%2Fjavascript&format_options=callback%3AgetJson&SRSNAME=EPSG%3A3857&FEATUREID:high_voltage_lines.130
    // https://stackoverflow.com/questions/6566456/how-to-serialize-an-object-into-a-list-of-url-query-parameters

    $.ajax({
        jsonp: false,
        url: rootUrl + "?" + (new URLSearchParams(defaultParameters).toString()),
        jsonp: false,
        dataType: 'jsonp',
        crossDomain: true,
        headers: {
            accept: 'application/json',
            'Access-Control-Allow-Origin': '*',
        },
        jsonpCallback: 'getJson',

        success(data) {
            if (data.totalFeatures > 0) {

                const styleFunction = function(feature) {
                    return styles[feature.getGeometry().getType()];
                };

                //crear vectorSource con las geometrías
                const vectorSource = new VectorSource({
                    features: new GeoJSON().readFeatures(data),
                });

                // Podemos añadir una nueva geometría con vectorSource.addFeature
                //vectorSource.addFeature(new Feature(new Circle([5e6, 7e6], 1e6)));

                //Crear vectorLayer con source vectorSource
                const vectorLayer = new VectorLayer({
                    source: vectorSource,
                    style: styleFunction,
                });

                //Añadimos la capa al mapa
                map.addLayer(vectorLayer);

                // Centramos la vista a los limites del vectorSource
                map.getView().fit(vectorSource.getExtent(), { "maxZoom": 18 });
            } else {
                cardNoGeom();
            }
        },
    });
};


### Transformar proyecciones
      import { transformExtent } from 'ol/proj';
      
      let currentExtent = map.getView().calculateExtent(map.getSize());
      let projectionCode = map.getView().getProjection().code_;
      //Transformadas para BBox
      let transformExtentERB = transformExtent(currentExtent, projectionCode, 'EPSG:4326');
      
     //coordenadas en EPSG 4326(latLon)
      let transformCoordinate4326 = toLonLat(coordinate, 'EPSG:3857');
      console.log(transformCoordinate4326);

### GetFeatureInfo
 La solicitud GetFeatureInfo incorpora muchos de los parámetros necesarios en la GetMap solicitud junto con parámetros específicos para las capas de consulta. 
 
http://webhelp.esri.com/arcims/9.3/General/mergedProjects/wms_connect/wms_connector/get_featureinfo.htm


### Obtener capa activa de un grupo de capas
      function getCapaActiva() {
          // let capas = map.getLayers().array_[1]
          let capas = map.getLayerGroup();
          console.log(capas);
          // console.log(overlays_maps.getLayers().array_[2].values_.name);
          // console.log('capas overlay')
          // console.log(overlays_maps.getLayers().array_[2].values_.visible);
          // console.log(overlays_maps.getLayers().array_[2].values_.name);
          // console.log(overlays_maps.getLayers().array_[2].values_);


          let capasOverlays = overlays_maps.getLayers().array_;
          //console.log('capa 2')
          //console.log(overlays_maps.getLayers().array_[2].values_.source);
          for (let i = 0; i < capasOverlays.length; i++) {
              let visible = capasOverlays[i].values_.visible;
              let source = capasOverlays[i].values_.source; //objeto

              // console.log(capasOverlays[i].values_.source + "- " + visible);
              if (visible) {
                  return source;
                  break;
              }
          }

      }

### OpenLayers: How to detect the map view is completely loaded?
https://stackoverflow.com/questions/34311461/openlayers-how-to-detect-the-map-view-is-completely-loaded

      map.once('postrender', function(event) {
          doyourmagic();
      });

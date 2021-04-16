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

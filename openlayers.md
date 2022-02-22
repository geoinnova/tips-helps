Capa Vectorial con GeoJSON [https://github.com/erabasco/tips-helps/blob/master/openlayers.md#capas-de-catastro]

## Capa Vectorial con GeoJSON

Función para estilo del punto

```js
function pointStyleFunction(feature, resolution) {
 
  //console.log("Resolucion",resolution)
  return new Style({
    // image: new CircleStyle({
    //   radius: 10,
    //   fill: new Fill({color: 'rgba(255, 0, 0, 0.1)'}),
    //   stroke: new Stroke({color: 'red', width: 1}),
    // }),
    text: createTextStyle(feature),
  });
}
```
Delaración del VectorLayer

```js
const vectorSupplies = new VectorLayer({
  source: new VectorSource({
    projection: 'EPSG:4326',
    url: 'https://.../wfs/data/supplies.geojson',
    format: new GeoJSON(),
  }),
  style: pointStyleFunction,
});
```





## Capas de Catastro

```js

import TileLayer from 'ol/layer/Tile';
import TileWMS from 'ol/source/TileWMS';

const catastroInspire = new TileLayer({
  title: 'catastroInspire',
  source: new TileWMS({
  url: 'http://ovc.catastro.meh.es/cartografia/INSPIRE/spadgcwms.aspx',
  params: {
    LAYERS: "CP.CadastralParcel",
  }
  }),
  visible:false
  });

  const catastro = new TileLayer({
    title: 'catastro',
    source: new TileWMS({
    url: 'http://ovc.catastro.meh.es/Cartografia/WMS/ServidorWMS.aspx?',
    
    params: {
      LAYERS: "Catastro",
      TILED: "true",
      VERSION: "1.1.1",
    },
    }),
    visible:true
    });
    
    
  const map = new Map({
  layers: [
    new LayerGroup({
      title: 'Base maps',
      layers: [
        catastroInspire,
        catastro,
      ],
      attributions: '< a href = "....."_blank ">.....</a>',
    }),
  ],
  target: 'map',
  view,
  controls: defaultControls({ attribution: false }).extend([attribution]),
});
    
```

## Ver resolución y zoom
```js
 console.log(view.getResolution())
 console.log(map.getView().getZoom())
```

## Mostrar capa de PNOA con servicio xyz de teselas raster

https://blog-idee.blogspot.com/2022/01/servicios-xyz-de-teselas-raster.html
https://openlayers.org/en/latest/examples/xyz.html

#### CON IMAGE WMS

```js
const pnoa = new OlLayerImage({
   name: 'Base PNOA',
   // extent: extent,
   source: new ImageWMS({
     url: "http://www.ign.es/wms-inspire/pnoa-ma?",
     crossOrigin: "anonymous",
     attributions:
       'Base © <a href="http://www.geo.admin.ch/internet/geoportal/' +
       'en/home.html">PNOA</a>',
     params: { LAYERS: "OI.OrthoimageCoverage" },
     serverType: "mapserver",
   }),
 });
 ```
          

#### CON XYZ

         import TileLayer from 'ol/layer/Tile';

  
          const pnoa =  new TileLayer({
            name: 'Base PNOA',
            crossOrigin: "anonymous",
            attributions:
                  'Base © <a href="https://tms-pnoa-ma.idee.es/1.0.0/pnoa-ma/{z}/{x}/{-y}.jpeg/' +
                   '">PNOA</a>',
            source: new XYZ({
                      url:  'https://tms-pnoa-ma.idee.es/1.0.0/pnoa-ma/{z}/{x}/{-y}.jpeg',
                    }),
          });



## Importante para localizar una capa por nombre, id u otro campo:

Definirlo a la hora de declarar la capa.

```js
    const vectorPoints = new VectorLayer({
      name: 'simbologia',
      source: new VectorSource({
        projection: 'EPSG:4326',
       
        format: new GeoJSON(),
        url: function(extent) {
          return  'url?'
          +'service=WFS&version=1.0.0&request=GetFeature&'
          +'typeName=vse%3Asupplies&id&'
          +'outputFormat=application/json'
          +'&SRSNAME=EPSG%3A4326';
        }
      }),
      style: pointStyleFunction,
    });
  ```

Para acceder a esa característica


     map.getLayers().forEach(function(layer) {
            if ((layer instanceof VectorLayer) && (layer.get('name')!='simbologia')) {
                map.removeLayer(layer);
            }
     });



## Funcion para comprobar si una capa concreta está visible, busca dentro de un grupo concreto y la activa si está desactivada
https://sisteme-ig.com/questions/5096/obtener-una-capa-en-openlayers-3

https://blog.onesaitplatform.com/2021/02/05/visores-de-mapas-parte-3-openlayers/

 
        erbSetLayerVisible(wfsLayersTranslations['supplies'],'Overlays');
  
  
              /**
             * Comprueba si una capa está activa
             * Si está dentro de un grupo hay que indicar el grupo
             * Por defecto no tiene grupo
             * 
             * @param {*} titleLayer nombre de la capa a buscar
             * @param {*} titleLayerGroup grupo de capas donde puede estar Overlays, Base
             */
            function erbSetLayerVisible(titleLayer,titleLayerGroup=''){
                 //obtenemos array con todas las capas
                 let arrayLayers = map.getLayers().getArray();

                 //console.dir(map.getLayers().getArray());
                 //recorremos las capas
                 arrayLayers.forEach(function (layer, i) {

                    //si vamos a comprobar un grupo de capas por ejemplo overlays será otro array
                    if (titleLayerGroup){
                        if (layer.values_.title==titleLayerGroup){

                            let arrayLayersOverlay = layer.values_.layers.array_;
                            arrayLayersOverlay.forEach(function (layerOverlay, i) {

                                 if (layerOverlay.values_.title==titleLayer){
                                     if (!layerOverlay.getVisible()){
                                        layerOverlay.setVisible(true);
                                       //TODO intentar salir del bucle foreach, no existe break
                                     }
                                 }
                            });
                         }
                    }
                    else{
                       if (!layer.getVisible()) layer.setVisible(true);
                    }

                 });
            }


## Función para obtener un grupo de capas

```js
function getGroup(nameGroup, map) {
    let layers = map.getLayers();
    let length = layers.getLength(), l;
    for (let i = 0; i < length; i++) {
        l = layers.item(i);
        let lt = l.get('name');

        // check for layers within groups
        if (lt === nameGroup) { // Title of Group
                if (l.getLayers) {
                var innerLayers = l.getLayers().getArray();
                return innerLayers;
            }
        }
    }
}
let baseMap; //grupo BaseMaps para añadir la capa catastro

```

Llamada

```js
baseMap = getGroup('BaseMaps', map)
baseMap.push(catastro);  //Agrega un elemento al final de una matriz.
baseMap.pop(catastro);   //Elimina un elemento del final de una matriz.
```

## Controlar cuando se hace un zoom
https://stackoverflow.com/questions/26734512/open-layers-3-zoom-map-event-handler

            map.on('moveend', function(){
              let zoom = map.getView().getZoom()

              // zoom >= 16.30875113752317
              if (zoom >= 17){ 
                map.addLayer(vectorPoints);
                isVectorLayerAdded = true;
              }else{
                if (isVectorLayerAdded){
                  map.removeLayer(vectorPoints);
                  isVectorLayerAdded = false;
                  console.log("desactivo")
                }
              }
            });

            map.getView().on('change:resolution', (event) => {
              console.log(event);
              let zoom = map.getView().getZoom()

                // zoom >= 16.30875113752317
                if (zoom >= 17){ 
                  map.addLayer(vectorPoints);
                  isVectorLayerAdded = true;
                }else{
                  if (isVectorLayerAdded){
                    map.removeLayer(vectorPoints);
                    isVectorLayerAdded = false;
                    console.log("desactivo")
                  }
                }
            });


## Controlar cuando se pulsa en desactivar/activar capa desde layerSwitcher (VISIBLE NO VISIBLE)
https://gis.stackexchange.com/questions/223641/how-to-get-the-change-event-of-a-layer-in-ol3-using-ol-control-layerswitcher

            layerOverlay.supplies.on('change:visible', function(){
                alert("Cambia");
            });


## Formatos salida geoserver
https://docs.geoserver.org/latest/en/user/services/wfs/outputformats.html
Capa supplies, acometidas: https://url?service=WFS&version=1.0.0&request=GetFeature&typeName=vse%3Asupplies&maxFeatures=200&outputFormat=application/json&SRSNAME=EPSG%3A3857


## Cómo añadir un servicio WFS en OpenLayers y darle simbología
https://mappinggis.com/2016/06/anadir-wfs-en-openlayers-simbologia/


            let openSansAdded = false;

            const getText = function (feature) {
              // const maxResolution = 600;
              let text = feature.get('id');

              // console.log("resolution",resolution);
              // console.log("maxResolution", maxResolution)

              // if (resolution > maxResolution) {
              //   text = '';
              // } else if (type == 'hide') {
              //   text = '';
              // } else if (type == 'shorten') {
              //   text = text.trunc(12);
              // } else if (
              //   type == 'wrap' &&
              //   (!dom.placement || dom.placement.value != 'line')
              // ) {
              //   text = stringDivider(text, 16, '\n');
              // }

              return text;
            };

            const createTextStyle = function (feature) {
             let CONF =  require('../conf/conf_simbologia');

              return new Text({
                textAlign: CONF.align == '' ? undefined : CONF.align,
                textBaseline: CONF.baseline,
                font: CONF.weight + ' ' + CONF.size + '/' + CONF.height + ' ' + 'Arial',
                text: getText(feature),
                fill: new Fill({color: CONF.fillColor}),
                stroke: new Stroke({color: CONF.outlineColor, width: CONF.outlineWidth}),
                offsetX: CONF.offsetX,
                offsetY: CONF.offsetY,
                placement: CONF.placement,
                maxAngle: CONF.maxAngle,
                overflow: CONF.overflow,
                rotation: CONF.rotation,
              });
            };

            // Points
            function pointStyleFunction(feature, resolution) {
              //console.log("Resolucion",resolution)
              return new Style({
                // image: new CircleStyle({
                //   radius: 10,
                //   fill: new Fill({color: 'rgba(255, 0, 0, 0.1)'}),
                //   stroke: new Stroke({color: 'red', width: 1}),
                // }),
                text: createTextStyle(feature),
              });
            }

            // const vectorPoints = new VectorLayer({
            //   source: new VectorSource({
            //     projection: 'EPSG:4326',
            //     url: 'https://url/data/supplies.geojson',
            //     format: new GeoJSON(),
            //   }),
            //   style: pointStyleFunction,
            // });

            const vectorPoints = new VectorLayer({
              source: new VectorSource({
                projection: 'EPSG:4326',
                //url: 'https://url/wfs?service=WFS&version=1.0.0&request=GetFeature&typeName=vse%3Asupplies&id&outputFormat=application/json&SRSNAME=EPSG%3A4326',
                format: new GeoJSON(),
                url: function(extent) {
                  return  'https://url?'
                  +'service=WFS&version=1.0.0&request=GetFeature&'
                  +'typeName=vse%3Asupplies&id&'
                  +'outputFormat=application/json'
                  +'&SRSNAME=EPSG%3A4326';
                }
              }),
              style: pointStyleFunction,
            });


Despues de MAP

            // controlo el nivel de zoom para mostrar/ocultar
            let isVectorLayerAdded = false;

            // map.on('moveend', function(){
            //   let zoom = map.getView().getZoom()

            //   // zoom >= 16.30875113752317
            //   if (zoom >= 17){ 
            //     map.addLayer(vectorPoints);
            //     isVectorLayerAdded = true;
            //   }else{
            //     if (isVectorLayerAdded){
            //       map.removeLayer(vectorPoints);
            //       isVectorLayerAdded = false;
            //       console.log("desactivo")
            //     }
            //   }
            // });

            // map.getView().on('change:resolution', (event) => {
            //   console.log(event);
            //   let zoom = map.getView().getZoom()

            //     // zoom >= 16.30875113752317
            //     if (zoom >= 17){ 
            //       map.addLayer(vectorPoints);
            //       isVectorLayerAdded = true;
            //     }else{
            //       if (isVectorLayerAdded){
            //         map.removeLayer(vectorPoints);
            //         isVectorLayerAdded = false;
            //         console.log("desactivo")
            //       }
            //     }
            // });


            let currentZoomLevel =  CONF.zoomInicial;                   //zoom inicial 

            let isLayerAcometidaVisible = layerOverlay.supplies.values_.visible;;
            // si la visibilidad de capa de Acometidas cambia comprobamos capa simbología
            layerOverlay.supplies.on('change:visible', function(){
              isLayerAcometidaVisible = layerOverlay.supplies.values_.visible; // true-false
              if (!isLayerAcometidaVisible){
                map.removeLayer(vectorPoints);
                isVectorLayerAdded = false;
              }else{
                map.addLayer(vectorPoints);
                isVectorLayerAdded = true;
              }

            });

            function checknewzoom(evt)
            {
               let newZoomLevel = map.getView().getZoom();

               // si cambia de nivel de zoom y la capa acometidas está activa
               if (newZoomLevel != currentZoomLevel & isLayerAcometidaVisible)
               {
                      currentZoomLevel = newZoomLevel;
                      if (currentZoomLevel >= CONF.nivelZoomActivaCapa){ 
                        if (!isVectorLayerAdded){
                          map.addLayer(vectorPoints);
                          isVectorLayerAdded = true;
                        }

                      }else{
                        if (isVectorLayerAdded){
                          map.removeLayer(vectorPoints);
                          isVectorLayerAdded = false;
                          console.log("desactivo")
                        }
                      }
                      console.log(currentZoomLevel);
               }
            }

            map.on('moveend', checknewzoom);


En conf_simbología.js

            const align = 'center';
            const baseline = 'middle';
            const size = '1.5em';
            const height = 'normal';
            const offsetX = parseInt(60, 10);
            const offsetY = parseInt(-20, 10);
            const weight = 'bold'
            const placement = undefined;
            const maxAngle = undefined;
            const overflow = undefined;
            const rotation = parseFloat(0); //parseFloat(feature.get('rotation'));


            const fillColor = '#000000';
            const outlineColor = '#ffffff';
            const outlineWidth = parseInt(3, 10);

            let zoomInicial =  13;             //zoom inicial 
            let nivelZoomActivaCapa = 20.449; //zoom en el que se activa la capa de simbología


            module.exports = {
                align,
                baseline,
                size,
                height,
                offsetX,
                offsetY,
                weight,
                placement,
                maxAngle,
                overflow,
                rotation,
                fillColor,
                outlineColor,
                outlineWidth,
                zoomInicial,
                nivelZoomActivaCapa,
            };





## Problema de importaciones con ejemplos OpenLayers
1. incluir type="module" en la llamada del script en index.html

      <script type="module" src="main.js"></script>
      
2. Si da error: unexpected character at line 1 column 1 of the JSON data

      SUBIR A UN SERVIDOR, ENTORNO PRODUCCION Y FUNCIONARÁ


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

    const rootUrl = CONF.wfs;
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

### proxy publico 
https://corsanywhere.herokuapp.com/ 

# urls
https://www.google.com/search?client=firefox-b-d&q=ajax+jsonp+transformar+xml+a+json
https://www.youtube.com/watch?v=ErPOtzP85UM

https://uniwebsidad.com/libros/fundamentos-jquery/capitulo-7/trabajar-con-jsonp

### Cómo convertir HTML seleccionado a Json
https://www.it-swarm-es.com/es/javascript/como-convertir-html-seleccionado-json/822816122/
https://www.it-swarm-es.com/es/javascript/como-convertir-html-json-usando-php/1046190629/


### 

### Usar JSONP al devolver XML 
https://stackoverflow.com/questions/3435454/using-jsonp-when-returning-xml

### Error de respuesta de jquery jsonp: no se llamó a la devolución de llamada
https://www.it-swarm-es.com/es/javascript/error-de-respuesta-de-jquery-jsonp-no-se-llamo-la-devolucion-de-llamada/1043771067/

### Ejemplos de comprensión y uso de jQuery ajax jsonp
https://programmerclick.com/article/27331699578/
https://programmerclick.com/article/81541785800/
https://programmerclick.com/article/27281065902/


## algo de código visto
 
         // serializa un objeto en una lista de parametros de consulta de URL ---- $.param(objeto) ----
            // con js vanilla > let url = new URLSearchParams(defaultParameters).toString();
            // service=WFS&version=1.0.0&request=GetFeature&typeName=vse%3Ahigh_voltage_lines&maxFeatures=200&outputFormat=text%2Fjavascript&format_options=callback%3AgetJson&SRSNAME=EPSG%3A3857&FEATUREID:high_voltage_lines.130
            // https://stackoverflow.com/questions/6566456/how-to-serialize-an-object-into-a-list-of-url-query-parameters

            // console.log(rootUrl + "?" + (new URLSearchParams(defaultParameters).toString()))
         //llamada url
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

                        // if (vectorLayer.getSource()) {
                        //     vectorLayer.getSource().clear;
                        // }
                        //Crear vectorLayer con source vectorSource
                        const vectorLayer = new VectorLayer({
                            source: vectorSource,
                            style: styleFunction,
                        });

                        //Añadimos la capa al mapa
                        map.addLayer(vectorLayer);

                        // Si maxZoom es mayor que 0 se centrará la vista a los limites del vectorSource con maxZoom
                        // map.getView().fit(vectorSource.getExtent(), { maxZoom });

                        if(maxZoom>0){
                            map.getView().fit(
                                vectorSource.getExtent(), {
                                    maxZoom,
                                    // size: map.getSize() - 500,
                                    padding: [20, 400, 20, 100],
                                }
                            );
                        }


                        //sacamos las coordenadas de las geometrías con otra llamada
                        // let idGeometria = data.features[0].properties.id;
                        // console.log(idGeometria);
                        // coordinatesGeometrieWFS(wfsLayer, idGeometria);

                    } else {
                        cardNoGeom();
                    }
                },
            });





        function mostrarFeaturesCatastro(e,layerCatastro,map)
        {
              const viewProjection = map.getView().getProjection();
              const viewResolution = map.getView().getResolution();
              let url = layerCatastro.getSource().getFeatureInfoUrl(
                e.coordinate, viewResolution, viewProjection,
                {
                    'INFO_FORMAT': 'text/plain',
                    'callback':'callbackFun',

                });


                map.addOverlay(popup);
                popup.setPosition(e.coordinate);
                contentPopup.innerHTML = '<iframe style="width:100%;height:110px;border:0px;" id="iframe" seamless src="' + url + '"><base target="_blank" /></iframe>';

                console.log(url);
                /*
                if (url) {
                  fetch(url)
                    .then(function (response) { return response.json(); })
                    .then(function (responseText) {
                      contentPopup.innerHTML = '';
                      popup.setPosition(evt.coordinate);
                      // si el nivel de zoom es superior a 14.80 se activa la referencia catastral
                      if (getZoomView(map) > 14.80) {

                        let area = Math.round(responseText.features[0].properties.areaValue);
                        let catastro = responseText.features[0].properties.nationalCadastralReference;
                        let parcela = responseText.features[0].properties.label;
                        let info = 'https://catastro.navarra.es/ref_catastral/unidades.aspx?C=258&PO=1&PA=' + parcela

                        contentPopup.innerHTML = '<div class="erb-catastro--title"> Información del Catastro</div>';
                        contentPopup.innerHTML += '<table class="erb-info-layer">' +
                          '<tr><td>Ref. catastral</td><td>' + catastro + '</td></tr>' +
                          '<tr><td>Área</td><td>' + area + ' [m2]</td></tr>' +
                          '<tr><td>Parcela</td><td>' + parcela + '</td></tr>' +
                          '<tr><td>Otros datos</td><td><a target="_blank" href=' + info + '> +Info </a></td></tr>';

                        contentPopup.innerHTML += '</table>';
                        // setTimeout(cerrarPopup,3000);
                      } else {
                        contentPopup.innerHTML += '<div class="erb-table-wms--alert"> ¡¡ No existen datos para este nivel de zoom !!</div>';
                      }
                    });
                }
                */

              // if (popupText) {
              //     overlayPopup.setPosition(coord);
              //     content.innerHTML = popupText;
              //     container.style.display = 'block';        
              // } else {
              //     container.style.display = 'none';
              //     closer.blur();
              // }


              $.ajax({
                //jsonp: false,
                url: url,

                // dataType: 'jsonp',
                // crossDomain: true,
                // headers: {
                //     accept: 'application/json',
                //     // accept: 'application/json, text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8',
                //     'Access-Control-Allow-Origin': '*',
                // },


                dataType: "jsonp",  // Especifica que el tipo de datos devuelto por el servidor es jsonp


                /*
                jsonp: 'callback',
                jsonpCallback: 'callbackFun',


                */

                jsonp: false,
                dataType: 'jsonp',
                crossDomain: true,
                headers: {
                    accept: 'application/json',
                    'Access-Control-Allow-Origin': '*',
                },
                jsonpCallback: 'getJson',

                outputFormat: 'text/javascript',
                format_options: 'callback:getJson',



                //jsonpCallback: 'getJson',

                /*
                success(callbackFun(data)) {
                    console.log("A ver")
                    console.log(data.age);
                    // if (data.totalFeatures > 0) {
                    //     const styleFunction = function(feature) {
                    //         return styles[feature.getGeometry().getType()];
                    //     };

                    //     //crear vectorSource con las geometrías
                    //     const vectorSource = new VectorSource({
                    //         features: new GeoJSON().readFeatures(data),
                    //     });

                    //     // Podemos añadir una nueva geometría con vectorSource.addFeature
                    //     //vectorSource.addFeature(new Feature(new Circle([5e6, 7e6], 1e6)));

                    //     // if (vectorLayer.getSource()) {
                    //     //     vectorLayer.getSource().clear;
                    //     // }
                    //     //Crear vectorLayer con source vectorSource
                    //     const vectorLayer = new VectorLayer({
                    //         source: vectorSource,
                    //         style: styleFunction,
                    //     });

                    //     //Añadimos la capa al mapa
                    //     map.addLayer(vectorLayer);

                    //     // Si maxZoom es mayor que 0 se centrará la vista a los limites del vectorSource con maxZoom
                    //     // map.getView().fit(vectorSource.getExtent(), { maxZoom });

                    //     if(maxZoom>0){
                    //         map.getView().fit(
                    //             vectorSource.getExtent(), {
                    //                 maxZoom,
                    //                 // size: map.getSize() - 500,
                    //                 padding: [20, 400, 20, 100],
                    //             }
                    //         );
                    //     }


                    //     //sacamos las coordenadas de las geometrías con otra llamada
                    //     // let idGeometria = data.features[0].properties.id;
                    //     // console.log(idGeometria);
                    //     // coordinatesGeometrieWFS(wfsLayer, idGeometria);

                    // } else {
                    //     cardNoGeom();
                    // }
                },

                */
                success: function (data) {
                    // Cambie la función llamada con éxito por el nombre de la función de devolución de llamada.
                    callbackFun(data)
                },
                error(data){
                    console.log('error'+callbackFun(data))
                    callbackFun(data)
                    //alert('error'+callbackFun(data))
                },

            });
            function callbackFun(data)
            {

                console.log('dentro callback'+data)
                console.dir(data)
               //console.log(data.readyState);
                var cadena = '{"nombre":'+data.toString()+'}'
                return cadena;
            }  


        function mostrarFeaturesCatastro(e,layerCatastro,map)
        {
              const viewProjection = map.getView().getProjection();
              const viewResolution = map.getView().getResolution();
              let url = layerCatastro.getSource().getFeatureInfoUrl(
                e.coordinate, viewResolution, viewProjection,
                {
                    'INFO_FORMAT': 'text/plain',
                    'callback':'callbackFun',

                });


                map.addOverlay(popup);
                popup.setPosition(e.coordinate);
                contentPopup.innerHTML = '<iframe style="width:100%;height:110px;border:0px;" id="iframe" seamless src="' + url + '"><base target="_blank" /></iframe>';

                console.log(url);
                /*
                if (url) {
                  fetch(url)
                    .then(function (response) { return response.json(); })
                    .then(function (responseText) {
                      contentPopup.innerHTML = '';
                      popup.setPosition(evt.coordinate);
                      // si el nivel de zoom es superior a 14.80 se activa la referencia catastral
                      if (getZoomView(map) > 14.80) {

                        let area = Math.round(responseText.features[0].properties.areaValue);
                        let catastro = responseText.features[0].properties.nationalCadastralReference;
                        let parcela = responseText.features[0].properties.label;
                        let info = 'https://catastro.navarra.es/ref_catastral/unidades.aspx?C=258&PO=1&PA=' + parcela

                        contentPopup.innerHTML = '<div class="erb-catastro--title"> Información del Catastro</div>';
                        contentPopup.innerHTML += '<table class="erb-info-layer">' +
                          '<tr><td>Ref. catastral</td><td>' + catastro + '</td></tr>' +
                          '<tr><td>Área</td><td>' + area + ' [m2]</td></tr>' +
                          '<tr><td>Parcela</td><td>' + parcela + '</td></tr>' +
                          '<tr><td>Otros datos</td><td><a target="_blank" href=' + info + '> +Info </a></td></tr>';

                        contentPopup.innerHTML += '</table>';
                        // setTimeout(cerrarPopup,3000);
                      } else {
                        contentPopup.innerHTML += '<div class="erb-table-wms--alert"> ¡¡ No existen datos para este nivel de zoom !!</div>';
                      }
                    });
                }
                */

              // if (popupText) {
              //     overlayPopup.setPosition(coord);
              //     content.innerHTML = popupText;
              //     container.style.display = 'block';        
              // } else {
              //     container.style.display = 'none';
              //     closer.blur();
              // }


              $.ajax({
                //jsonp: false,
                url: url,

                // dataType: 'jsonp',
                // crossDomain: true,
                // headers: {
                //     accept: 'application/json',
                //     // accept: 'application/json, text/html, application/xhtml+xml, application/xml;q=0.9, */*;q=0.8',
                //     'Access-Control-Allow-Origin': '*',
                // },


                dataType: "jsonp",  // Especifica que el tipo de datos devuelto por el servidor es jsonp


                /*
                jsonp: 'callback',
                jsonpCallback: 'callbackFun',


                */

                jsonp: false,
                dataType: 'jsonp',
                crossDomain: true,
                headers: {
                    accept: 'application/json',
                    'Access-Control-Allow-Origin': '*',
                },
                jsonpCallback: 'getJson',

                outputFormat: 'text/javascript',
                format_options: 'callback:getJson',



                //jsonpCallback: 'getJson',

                /*
                success(callbackFun(data)) {
                    console.log("A ver")
                    console.log(data.age);
                    // if (data.totalFeatures > 0) {
                    //     const styleFunction = function(feature) {
                    //         return styles[feature.getGeometry().getType()];
                    //     };

                    //     //crear vectorSource con las geometrías
                    //     const vectorSource = new VectorSource({
                    //         features: new GeoJSON().readFeatures(data),
                    //     });

                    //     // Podemos añadir una nueva geometría con vectorSource.addFeature
                    //     //vectorSource.addFeature(new Feature(new Circle([5e6, 7e6], 1e6)));

                    //     // if (vectorLayer.getSource()) {
                    //     //     vectorLayer.getSource().clear;
                    //     // }
                    //     //Crear vectorLayer con source vectorSource
                    //     const vectorLayer = new VectorLayer({
                    //         source: vectorSource,
                    //         style: styleFunction,
                    //     });

                    //     //Añadimos la capa al mapa
                    //     map.addLayer(vectorLayer);

                    //     // Si maxZoom es mayor que 0 se centrará la vista a los limites del vectorSource con maxZoom
                    //     // map.getView().fit(vectorSource.getExtent(), { maxZoom });

                    //     if(maxZoom>0){
                    //         map.getView().fit(
                    //             vectorSource.getExtent(), {
                    //                 maxZoom,
                    //                 // size: map.getSize() - 500,
                    //                 padding: [20, 400, 20, 100],
                    //             }
                    //         );
                    //     }


                    //     //sacamos las coordenadas de las geometrías con otra llamada
                    //     // let idGeometria = data.features[0].properties.id;
                    //     // console.log(idGeometria);
                    //     // coordinatesGeometrieWFS(wfsLayer, idGeometria);

                    // } else {
                    //     cardNoGeom();
                    // }
                },

                */
                success: function (data) {
                    // Cambie la función llamada con éxito por el nombre de la función de devolución de llamada.
                    callbackFun(data)
                },
                error(data){
                    console.log('error'+callbackFun(data))
                    callbackFun(data)
                    //alert('error'+callbackFun(data))
                },

            });
            function callbackFun(data)
            {

                console.log('dentro callback'+data)
                console.dir(data)
               //console.log(data.readyState);
                var cadena = '{"nombre":'+data.toString()+'}'
                return cadena;
            }  




        }




        }

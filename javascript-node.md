## Utilizar variables configuradas en un fichero externo

const CONF = require('../conf/conf_map');

        **conf_map.js**
        // WMS zoom levels
        const wmsMaxNativeZoom = 29;
        const wmsMaxZoom = 30;

        module.exports = {
            wmsMaxNativeZoom,
            wmsMaxZoom,
        };

        **llamada: CONF.wmsMaxNativeZoom;**


## Exportar funciones y variables
https://www.sitepoint.com/understanding-module-exports-exports-node-js/

main.js

    exports.desactivarConsultas = desactivarConsultas;
    exports.desactivarMeasure = desactivarMeasure;
    module.exports = {
        map,
        // desactivaConsultas,  < desde aquí no funciona
        // desactivarMeasure(map),
    };
    
    
tools.js

    import { desactivarConsultas, desactivarMeasure } from './main'
    
    Uso: 
    desactivarConsultas();

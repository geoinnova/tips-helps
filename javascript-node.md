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

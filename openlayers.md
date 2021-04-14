## Transformar proyecciones
      let currentExtent = map.getView().calculateExtent(map.getSize());
      let projectionCode = map.getView().getProjection().code_;
      //Transformadas para BBox
      let transformExtentERB = transformExtent(currentExtent, projectionCode, 'EPSG:4326');
      
     //coordenadas en EPSG 4326(latLon)
      let transformCoordinate4326 = toLonLat(coordinate, 'EPSG:3857');
      console.log(transformCoordinate4326);

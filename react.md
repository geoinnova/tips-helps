
# Desplegar proyecto en subcarpetas:
# Configurar APP en subditectorio

   - .htaccess
   - package.json
   - App.js
   - data.js
   - Main.jsx

## .htaccess
crear un archivo .htaccess ubicado en la subcarpeta donde se despliegue la  y añadir:

       Options -MultiViews
          RewriteEngine On
          RewriteCond %{REQUEST_FILENAME} !-f
          RewriteRule ^ index.html [QSA,L]

## package.json

        "homepage": "https://planero-web.geoinnova.org/subdirectorio",

## App.js

Añadir en path la variable baseRoute configurada en data.js (no funca exportandola, añado la url a mano)

       <BrowserRouter basename="/">
           <Route path="/subdirectorio" exact render={Main} />
              .....
          </Route>
          ))}
      </BrowserRouter>

## data.js
// Indicar carpeta raiz '/' o subdirectorio '/subdirectorio/'

      const baseRoute = "/benirredra";


## Main.jsx
Cuidado con esta ruta en ese link

      <Link to="/subidrectorio/PLANO_2_MEDIO_FISICO">


# Mostrar/Ocultar popup

## Map.css
 Eliminar display none para mostrar el popup

      .ol-popup{
        display: none;
       }


## Generar archivos para producciön
    npm run-script build

* muy importante: comprobar en package.json la url donde se desplegará el proyecto
      
      "homepage": "http://planero-web2.geoinnova.org/"
      
      

### Solución error: Se bloqueó la carga de un módulo de “---” debido a un tipo MIME no permitido (“text/html”)

El error es consecuencia de que está buscando el archivo index.xxxx.js en el raiz del dominio y se ha subido en un directorio, por ejemplo: /visor/dist.

La solución es sencilla, hay que indicar a vite que al empaquetar considere que el directorio base será /visor/ por lo que tendrás que crear un archivo llamado **vite.config.js** en el raiz de tu proyecto en incluir lo siguiente dentro:

```js
exportdefault {
    base:'/visor/'
  }  
```

Una vez generes los archivos estáticos con npm run build ya puedes subirlos al servidor en la carpeta /visor/ 
(omitir la carpeta /dist ya que sino tendrás que indicar que el directorio base sería visor/dist/).

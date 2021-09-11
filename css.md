## href con target blank
<a href="#" target="_blank" rel="noreferrer noopener nofollow">Enlace</a>
`<a href="#" target="_blank" rel="noreferrer noopener nofollow">Enlace</a>`

### modo autofit de Android que causa problemas con el ancho css en la página web

Es como si no detectara que estás en versión movil.

    .mod-icon-grid {
        display: grid ;
        grid-gap: 15px;
        grid-template-columns: repeat(auto-fit, minmax(100px, 1fr) );   
    }

https://html.dokry.com/6736

https://www.youtube.com/watch?v=hPd93mijFCM


### Paginador

  Paginador Prensa

    ul.page-numbers>li>a.page-numbers, ul.page-numbers>li>a.next.page-numbers, ul.page-numbers>li>a.prev.page-numbers{
      color: #fff;
      background: #000;
      height: 40px;
      width: 40px;
      border-radius: 25px;
      line-height: 39px;
      font-size: 18px;
    }

     ul.page-numbers > li>span.page-numbers.current{
      height: 40px;
      width: 40px;
      border-radius: 25px;
      line-height: 39px;
      font-size: 18px;
      }


  Paginador GIRAS Y OTROS
  
    ul.pagination>li>a.page-numbers.page-numbers{
      color: #fff !important;
      background: #000;
      height: 40px;
      width: 40px;
      border-radius: 25px;
      line-height: 39px;
      font-size: 18px;   
      margin: 0 10px;
      }

    ul.pagination>li>span.page-numbers.current{
      color: #fff !important;
      background: #e74c3c;
      height: 40px;
      width: 40px;
      border-radius: 25px;
      line-height: 39px;
      font-size: 18px;   
       margin: 0 5px;
      }

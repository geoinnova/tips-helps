## EN VERSIÓN ORIGINAL

Dentro del producto en el apartado de bottom, incluimos el script

<script src="https://nube.abasedemusica.es/vo/wp-content/themes/kleo-child/assets/js/erb_registration_form.js">
</script>
 

### erb_registration_form.js

        function selectFormFieldsToBeShown() {
            if (document.getElementById('concursar_0').checked){
                erb_show_some_form_data();
            } else {
                erb_hide_some_form_data();
            }
        }

        function checkFileInput(id, msg) {
            var f = document.getElementById(id);
            if (f.files && f.files.length == 0) {
                alert(msg)
            }
        }


        function erb_hide_some_form_data(){
            jQuery('.single_add_to_cart_button').fadeTo( "fast", 1 )
            
            //ocultamos los campos
            jQuery('#group_name').parents("tr").hide();
            jQuery('#song_writers').parents("tr").hide();
            jQuery('#song_title').parents("tr").hide();
            jQuery('#song_lyrics').parents("tr").hide();
            jQuery('#group_menbers').parents("tr").hide();
            jQuery('#group_history').parents("tr").hide();
            jQuery('#yt_url').parents("tr").hide();	
            jQuery('.product_meta').hide();
            jQuery('#check_02').parents("tr").hide();	
            
            //Eliminamos subida de archivos
            jQuery('#wcuf_file_uploads_container').hide();
            
            jQuery('#group_name').val(' ');
            jQuery('#song_writers').val(' ');
            jQuery('#song_writers').val(' ');
            jQuery('#song_lyrics').val(' ');
            jQuery('#group_menbers').val(' ');
            jQuery('#song_title').val(' ');
            jQuery('#yt_url').val(' ');
            jQuery('#group_history').val(' ');
            jQuery('#check_02').prop("checked",true);
        }

        function erb_show_some_form_data(){
            jQuery('.single_add_to_cart_button').fadeTo( "fast", 1 )
            
            //ocultamos los campos
            jQuery('#group_name').parents("tr").show();
            jQuery('#song_writers').parents("tr").show();
            jQuery('#song_title').parents("tr").show();
            jQuery('#song_lyrics').parents("tr").show();
            jQuery('#group_menbers').parents("tr").show();
            jQuery('#group_history').parents("tr").show();
            jQuery('#yt_url').parents("tr").show();	
            jQuery('.product_meta').show();
            jQuery('#check_02').parents("tr").show();
            
            //Eliminamos subida de archivos
            jQuery('#wcuf_file_uploads_container').show();
            
            jQuery('#group_name').val('');
            jQuery('#song_writers').val('');
            jQuery('#song_writers').val('');
            jQuery('#song_lyrics').val('');
            jQuery('#group_menbers').val('');
            jQuery('#song_title').val('');
            jQuery('#yt_url').val('');
            jQuery('#group_history').val('');
            jQuery('#check_02').prop("checked",false);
            
        }

        jQuery(document).ready(function(){
            document.querySelector('form.cart').addEventListener('submit', function() {
                if (document.getElementById('concursar_0').checked) {
                    checkFileInput('wcuf_upload_field_0-1933', 'Por favor, sube una imagen de portada');
                    checkFileInput('wcuf_upload_field_1-1933', 'Por favor, sube la canción en formato mp3');
                    checkFileInput('wcuf_upload_field_2-1933', 'Por favor, adjunta un documento o certificado de autoría');
                }
            });
            selectFormFieldsToBeShown();
            document.getElementById('concursar_0').addEventListener('change', function() {
                selectFormFieldsToBeShown();
            });
            document.getElementById('concursar_1').addEventListener('change', function() {
                selectFormFieldsToBeShown();
            });
        });
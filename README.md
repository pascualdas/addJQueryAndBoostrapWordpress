# addJQueryAndBoostrapWordpress
How to add HTML, JQuery and Css styles to your wordpress Theme - Example in: www.lizetbenavidesdermatologa.com.co

USAR JQUERY y Bootstrap EN WORDPRESS: https://decodecms.com/incluir-bootstrap-en-wordpress/

1. Ubicar functions.php dentro de la carpeta del tema.

2. Incluir funciones al final del fichero:

// Incluir Bootstrap CSS
function bootstrap_css() {
	wp_enqueue_style( 'bootstrap_css', 
	'https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css', 
	array(), 
	'4.1.1'
	); 
}
add_action( 'wp_enqueue_scripts', 'bootstrap_css');


// Incluir Bootstrap JS y dependencia popper
function bootstrap_js() {

	wp_enqueue_script( 'popper_js', 
		'https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js', 
		array(), 
		'1.16.0', 
	true); 
	wp_enqueue_script( 'bootstrap_js', 
		'https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js', 
		array('jquery','popper_js'), 
		'4.4.1', 
	true); 
	
}
add_action( 'wp_enqueue_scripts', 'bootstrap_js');

3. usar ejemplo: Se agrega en wordpress-> apariencia - widgets => uno nuevo de tipo HTML PERSONALIZADO ASI:

<script>
	
jQuery(document).ready(function() {
	jQuery('#modalTitle').html('Medidas contra el COVID-19 <strong style="color: #000000 !important;"><a href="https://www.instagram.com/explore/tags/yomequedoencasa/?hl=es-la" target="_new" style="color: #000000 !important;">#yoMeQuedoEnCasa</a> <a href="https://www.instagram.com/explore/tags/lizetbenavidesdermatologa/?hl=es-la" target="_new" style="color: #000000 !important;">#lizetbenavidesdermatologa</a></strong>');
	jQuery('#modalBody').html('<a href="https://api.whatsapp.com/send?phone=573112558004&text=Hola,%20te%20hablo%20desde%20tu%20web"><p align="center"><img src="covid19MiniLizet.png" class="figure-img img-fluid rounded"></p></a><p align="center" style="color: #000000 !important;">Click sobre la imagen si deseas contactarnos mediante WhatsApp.</p>');
	jQuery('#frmModal').modal({backdrop: 'static', keyboard: true});
	jQuery('#frmModal').modal('show');
	jQuery('#frmModal').fadeIn('slow');
});
	
jQuery('.modal').on('shown.bs.modal', function() {
  //Make sure the modal and backdrop are siblings (changes the DOM)
  jQuery(this).before(jQuery('.modal-backdrop'));
  //Make sure the z-index is higher than the backdrop
  jQuery(this).css("z-index", parseInt(jQuery('.modal-backdrop').css('z-index')) + 1);
});	
	
</script>
	

4. Para evitar problemas con la capa backdrop, se aconseja dejar el codigo del modal al final del html, terminando el body asi: https://wordpress.org/support/topic/how-to-inset-code-the-closing-tag/
Ubicar functions.php dentro de la carpeta del tema y se agrega el HTML con JS asi:

add_action('wp_footer', 'my_custom_footer_js');
function my_custom_footer_js() {
  echo '<div id="frmModal" class="modal fade bd-example-modal-xl" tabindex="-1" role="dialog" aria-labelledby="myExtraLargeModalLabel" aria-hidden="true">
  <div class="modal-dialog modal-xl modal-dialog-centered" role="document">
    <div class="modal-content">

		<div class="modal-header text-center">
			<p align="center">
				<h5 id="modalTitle" class="modal-title text-center">Modal title</h5>
			</p>
			<button type="button" class="close" data-dismiss="modal" aria-label="Close">
				<span aria-hidden="true">&times;</span>
			</button>
		</div>
		<div id="modalBody" class="modal-body">
			
		</div>

    </div>
  </div>
</div>';
}

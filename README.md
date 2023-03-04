# site-chatschool
Projeto para treinar o desenvolvimento de um website utilizando HTML e CSS, utilizando os principais conceitos de requisições HTTP
https://otthonleao.github.io/site-chatschool/

### Ícones
Nesse projeto utilizamos o [Material Icons](https://m3.material.io/styles/icons/overview) que é mantido pelo Google. E para conectar com o projeto, utilizamos a seguinte linha no index.html
```html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```
Há outros sites para explorar os diversos icones, como:
[Font Awesome Icon](https://fontawesome.com), 
[Glyphicons](https://glyphicons.com/), 
[Ionicons](https://ionic.io/ionicons)

### Enviando e-mail sem back-end
Para formatos simples ou até mesmo testes é possível usar o [Google Apps Mail](https://github.com/dwyl/learn-to-send-email-via-google-script-html-no-server/blob/master/README.md) ou a API do [FormSubmit](https://formsubmit.co/).

#### Configurando o comportamento de envio
Caso não configure uma resposta de envio, após enviar o e-mail pode carregar uma página com o json que para o usuário não é legal.

1. Nesse caso usamos o jQuery CDN para fazer o script e assim poder. É preciso copiar o endereço do link do `minifief`
```html
<script src="https://code.jquery.com/jquery-3.6.3.min.js"></script>
```
2. Mudar o valor do botão para "AGUARDE" e travar após ouvir o clique (event)
```javascript
$('form').submit(function (event) {
	event.preventDefault();
	$('form input[type="submit"]').val('Aguarde').attr('disable', true);
	$.ajax({
		type: $('form').attr('method'),
		url: $('form').attr('action'),
		data: $('form').serialize()
	)}
}
```
3. Pegar o nome do usário para colocar no campo assunto
```javascript
let name = document.querySelector("#nome");
$('form').submit(function (event) {
	$('form input[name="_subject"]').val('Contato - Chatboot: ' + name.value);
}
```
4. Notificar o sucesso do envio por meio de um alerta
```javascript
$('form').submit(function (event) {
	$.ajax({
		success: function () {
			alert('E-mail enviado com sucesso!\nEm breve entraremos em contato');
	})
}
```
5. Limpar os campos do formulário e ativar o botão novamente renomeado para "enviar"
```javascript
$('form').submit(function (event) {
	$.ajax({
		success: function () {
			$('form').trigger('reset');
			$('form input[type="submit"]').val('enviar').attr('disable', false);
	})
}
```
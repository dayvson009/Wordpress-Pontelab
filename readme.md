# Wordpress Pontelab

### MELHOR USABILIDADE

Para cada projeto é essêncial fazer algumas alterações no wordpress.

Muitas vezes nossos clientes não possuem um conhecimento muito grande em administração de conteúdo para a web e a visão do painel de controle pode ser meio intimidadora.

Criar elementos que facilitem o uso, adaptando a interface para a cultura / nível de conhecimento de cada empresa é fazer com que o usuário se sinta em casa.

### MENOS DOR DE CABEÇA

Se o seu administrador for mais simples de usar você vai receber menos e-mails / ligações / chamadas no Skype com reclamações, certo? O ganho de produtividade (e horas de sono) não tem preço. 

## VAMOS COMEÇAR PELO ACESSO

Se você está habituado a utilizar o WordPress provavelmente já digita "/wp-admin". Mas talvez para o cliente seria mais fácil de lembrar do endereço se a url tivesse um nome mais amigável como "/admin" ou até mesmo apenas "/login", certo?

Para isto vamos precisar editar o arquivo .htaccess. Este arquivo fica geralmente na pasta raíz do seu diretorio do WordPress.

```
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteRule ^admin$ wp-admin
</IfModule>

```

## A TELA DE LOGIN

Para deixar o sistema com a identidade visual da sua empresa o primeiro passo é substituir logo do wordpress pelo seu próprio logo. Crie um arquivo de imagem com o tamanho máximo de **323px** de largura por **67px** de altura.

O logo do WordPress está como background de uma classe de CSS. Adicione a seguinte classe na sua folha de estilos e substitua o endereço pelo nome e caminho correto da imagem.

```
body.login div#login h1 a {
    background-image: url(/wp-content/themes/nome-do-tema/img/site-logo.png);
}
```

Opcionalmente é possível realizar esta modificação através do **functions.php**. Lembre-se de alterar o valor de padding-bottom para o que funcionar melhor no seu caso e modificar o nome e caminho da imagem.

```
<?php
// Custom WordPress Login Logo
function my_login_logo() {
?>
  body.login div#login h1 a {
    background-image: url(/img/site-login-logo.png);
    padding-bottom: 30px;
  }
 
<?php 
}
add_action( 'login_enqueue_scripts', 'my_login_logo' );
?>
```

### CRIANDO SEUS PRÓPRIOS ESTILOS

Não é possível editar o arquivo HTML core do WordPress, mas podemos modifica-lo completamente através de CSS. Existem duas opções: utilizar sua folha de estilos padrão ou criar uma especificamente para o seu tema. Dá para realizar diversas modificações nesta tela como mudança de *background*, *tipografia*, trocar as *dimensões do logo*, etc. Para isto cole este código no **functions.php** e altere para o caminho e nome da sua folha de estilos. No caso o arquivo se chama style-login.css

```
//Login Stylesheet

function my_login_stylesheet() { 

  echo '<link rel="stylesheet" id="custom_wp_admin_css"  href="" type="text/css" media="all" />';

}
add_action( 'login_enqueue_scripts', 'my_login_stylesheet' );

```

Segue uma lista de classes úteis para a personalização desta tela de acesso.
```
body.login {}
body.login div#login {}
body.login div#login h1 {}
body.login div#login h1 a {}
body.login div#login form#loginform {}
body.login div#login form#loginform p {}
body.login div#login form#loginform p label {}
body.login div#login form#loginform input {}
body.login div#login form#loginform input#user_login {}
body.login div#login form#loginform input#user_pass {}
body.login div#login form#loginform p.forgetmenot {}
body.login div#login form#loginform p.forgetmenot input#rememberme {}
body.login div#login form#loginform p.submit {}
body.login div#login form#loginform p.submit input#wp-submit {}
body.login div#login p#nav {}
body.login div#login p#nav a {}
body.login div#login p#backtoblog {}
body.login div#login p#backtoblog a {}
```

## DENTRO DO ADMINISTRADOR

### COMO MODIFICAR O TEXTO DO FOOTER

Por padrão o footer do WordPress exibe a mensagem "**Obrigado por criar com o WordPress**".

Para trocar este texto novamente vamos utilizar o nosso grande amigo functions.php. Adicione o seguinte código e mude o texto entre as aspas depois do echo.

```
// Customizar o Footer do WordPress
function remove_footer_admin () {
  echo '© <a href="http://pontelab.com/">PONTELAB</a> - Desenvolvimento criativo.';
}
add_filter('admin_footer_text', 'remove_footer_admin');
```

## CUSTOMIZANDO O ADMINISTRADOR

Para alterar o estilo visual de seu administrador para ficar a cara da sua empresa. A folha de estilos padrão (/wp-admin/css) é bem completa e organizadinha. Pode ser que você só precise fazer alguns ajustes.
 
Ou você pode criar um arquivo css e colocalo na pasta (/wp-admin), e utilizar a seguinte função no arquivo **function.php**.

```
function custom_panel_admin() {

  echo '<link rel="stylesheet" id="custom_panel_admin"  href="custom_panel_admin.css" type="text/css" media="all" />';

}

add_action('admin_head', 'custom_panel_admin');

```

Aqui estão algumas das classes mais utilizadas:

**#wphead**
O cabeçalho do painél contendo o título principal, nome do blog e link para o site.

**#adminmenu ul**
A barra de navegação lateral com os links: Posts, Mídia, Ferramentas…

**#adminmenu2 ul**
A subnavegação da barra lateral. Por exemplo “dentro” de Posts teríamos Todos os Posts, Adicionar Novo, Tags e Categorias.

**.wrap**
A div que funciona como um container principal do painel de administração.

**#footer**
O rodapé do site com logotipo do wordpress, versão e links.

**.wrap h2**
Títulos das seções principais como por exemplo Painel.


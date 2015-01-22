# Arquitetura

Criar a arquitetura de um projeto de CSS é uma das coisas mais difíceis que terás que fazer durante a vida desse projeto.
Manter essa arquitetura constante e significativa é ainda mais difícil.

Felizmente, um dos benefícios principais de usar um pré-processador de CSS é ter a habilidade de dividir a nossa base de código em vários ficheiros sem ter impacto na performance (como a diretiva de CSS `@import` fazia). Graças à sobrecarga da diretiva `@import` no Sass, é perfeitamente seguro (e até recomendado) usar os ficheiros necessários na fase de desenvolvimento, todos estes compilados numa única stylesheet quando o projeto for para produção.

Em cima disso, não posso salientar o suficiente a necessidade de pastas, mesmo em pequenos projetos. Em casa, não deixas todas as folhas de papel na mesma caixa. Tens uma para os papéis da casa, uma para documentos do banco, uma para contas e assim em diante. Não há razão para fazeres de maneira diferente quando estás a estruturar um projeto de CSS. Separa o teu código em pastas com nomes compreensíveis para depois ser fácil encontrar qualquer código quando mais tarde tiveres que voltar ao projeto.

Há muitas arquiteturas populares para projectos de CSS: [OOCSS](http://oocss.org/), [Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/), como [Bootstrap](http://getbootstrap.com/), como [Foundation](http://foundation.zurb.com/)... Todas têm os seus méritos, prós e contras.

Eu uso uma abordagem que acaba por ser muito parecida com [SMACSS](https://smacss.com/) de [Jonathan Snook](http://snook.ca/), e que se foca em manter as coisas simples e óbvias.

<div class="note">
  <p>Eu aprendi que a arquitetura é muito especifica para o projeto. Sente te à vontade para ignorares ou adaptares a solução proposta para lidares com um sistema que se adapta melhor às tuas necessidade</p>
</div>

### Leitura Adicional

* [Arquitetura para um projeto de SASS](http://www.sitepoint.com/architecture-sass-project/)
* [Uma Olhada a diferentes arquiteturas de SASS](http://www.sitepoint.com/look-different-sass-architectures/)
* [FR] [Sass, une architecture composée](http://slides.com/hugogiraudel/sass-une-architecture-composee)
* [SMACSS](https://smacss.com/)
* [Uma introdução a OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)
* [Atomic Web Design](http://bradfrost.com/blog/post/atomic-web-design/)






## Componentes

Há uma grande diferença entre fazer algo *funcionar* e fazer algo *bom*. Mais uma vez, CSS é uma linguagem muito desorganizada <sup>[Citação Necessária]</sup>. Quanto menos CSS tiverem melhor. Nós não queremos lidar com megabytes de CSS. Para manter as nossas stylesheets pequenas e efecientes&mdash;e isto não será nenhuma surpresa para ti&mdash; é normalmente uma boa ideia pensar numa interface como uma coleção de componentes.

Componentes podem ser qualquer coisa desde que:

* façam uma e apenas uma coisa;
* sejam reutilizáveis e usados por todo o projeto;
* sejam independentes.

Por exemplo um formulário de pesquisa deve ser tratado como um componente. Deverá ser reutilizável, em diferentes posições, páginas e em situações diversas. Não deve depender da sua posição na DOM (rodapé, barra lateral, conteúdo principal...).

A maior parte de qualquer interface pode ser pensada como pequenos componentes e eu recomendo que fique com este paradigma. Isto vai não só diminuir a quantidade de CSS necessário para um projeto completo, mas também acaba por ser muito mais fácil de manter do que uma desorganização onde tudo está tudo junto.




## O padrão 7-1

Vamos então voltar à arquitetura, ok? Eu normalmente uso o que chamo *O padrão 7-1*: 7 pastas, 1 ficheiro. Basicamente, tudo o que tens são ficheiros parciais colocados em 7 pastas diferentes, e um único ficheiro na raiz do projeto (normalmente chamado `main.scss`) que importa todos os ficheiros parciais para serem compilados numa stylesheet de CSS.

* `base/`
* `components/`
* `layout/`
* `pages/`
* `themes/`
* `utils/`
* `vendors/`

E claro:

* `main.scss`

<figure role="group">
  <img src="/assets/images/sass-wallpaper.jpg" alt="Um ficheiro para governá-los todos, um ficheiro para encontrá-los, um ficheiro para trazê-los todos, E a maneira do SASS para fundi-los." />
  <figcaption>Wallpaper de <a href="https://twitter.com/julien_he">Julien He</a></figcaption>
</figure>

Idealmente, teríamos algo como:

<div class="highlight"><pre><code>
sass/
|
|- base/
|   |- _reset.scss       # Reset
|   |- _typography.scss  # Regras de Tipografia
|   ...                  # Etc...
|
|- components/
|   |- _buttons.scss     # Botões
|   |- _carousel.scss    # Carossel
|   |- _cover.scss       # Cover
|   |- _dropdown.scss    # Dropdown
|   ...                  # Etc..
|
|- layout/
|   |- _navigation.scss  # Navegação
|   |- _grid.scss        # Grelha
|   |- _header.scss      # Cabeçalho
|   |- _footer.scss      # Rodapé
|   |- _sidebar.scss     # Barra Lateral
|   |- _forms.scss       # Formulários
|   ...                  # Etc...
|
|- pages/
|   |- _home.scss        # Estilos especificos á Home
|   |- _contact.scss     # Estilos especificos á página de Contacto
|   ...                  # Etc...
|
|- themes/
|   |- _theme.scss       # Tema Padrão
|   |- _admin.scss       # Tema de Adminisração
|   ...                  # Etc...
|
|- utils/
|   |- _variables.scss   # Variáveis
|   |- _functions.scss   # Funções
|   |- _mixins.scss      # Mixins
|   |- _helpers.scss     # Auxiliares de classes e placeholders
|
|- vendors/
|   |- _bootstrap.scss   # Bootstrap
|   |- _jquery-ui.scss   # jQuery UI
|   ...                  # Etc...
|
|
`- main.scss             # Prinicipal ficheiro de SASS
</code></pre></div>

<div class="note">
  <p>Os ficheiros seguem as mesma convenções de nome descritas em acima: são delimitados com um hífen.</p>
</div>


### Pasta Base

A pasta `base/` contém o que nós podemos chamar de código padrão para o projeto. Aqui podemos encontrar um ficheiro de reset, algumas regras tipográficas e provavelmente uma stylesheet (que estou a chamar `_base.scss`), que define alguns estilos padrão para elementos de HTML mais usados.

* `_base.scss`
* `_reset.scss`
* `_typography.scss`



### Pasta Layout

A pasta `layout/` contêm tudo que é necessário para criar o layout do site ou aplicação. Esta pasta contêm as stylesheets para as partes principais do site (cabeçalho, rodapé, navegação, barra lateral...), a grelha ou mesmo o CSS de todos os formulários.

* `_grid.scss`
* `_header.scss`
* `_footer.scss`
* `_sidebar.scss`
* `_forms.scss`
* `_navigation.scss`

<div class="note">
  <p>A pasta <code>layout/</code> também pode ser chamada <code>parciais/</code>, sendo isto uma questão de preferência.</p>
</div>



### Pasta Components

Para componentes mais pequenos, há a pasta `components/`. Enquanto a pasta `layout/`é *macro* (definindo a estrutura global), a pasta `components/` é mais focada em módulos. Contêm todo o tipo de módulos específicos como um slider, um carregador e tudo que seja desse tipo.
Há normalmente imensos ficheiros na pasta `components/` tendo em conta que todo o site/aplicação deverá ser constituído por pequenos módulos.

* `_media.scss`
* `_carousel.scss`
* `_thumbnails.scss`

<div class="note">
  <p>A pasta <code>components/</code> também se poderá chamar <code>modulos/</code>, sendo isto uma questão de preferência.</p>
</div>



### Pasta Pages

Se tiveres estilos específicos a páginas, o melhor será colocá-las na pasta `pages/`, num ficheiro com o nome da página. Por exemplo, não deixa de ser comum ter estilos muito específicos para a página inicial que criam a necessidade de ter um `_home.scss` na pasta `pages/`.

* `_home.scss`
* `_contact.scss`

<div class="note">
  <p>Dependendo do processo de desenvolvimento estes ficheiros podem ser chamados individualmente para evitar que eles se juntem com outros quando todas as stylesheets se juntam. Na realidade depende do que preferires.</p>
</div>


### Pasta Temas

Em grandes sites ou aplicações, é comum existirem vários temas. Há certamente diversas maneira de lidar com temas mas eu pessoalmente gosto de colocar tudo numa pasta com o nome `themes/`.

* `_theme.scss`
* `_admin.scss`

<div class="note">
  <p>Isto é algo muito especifico a cada projeto e em muitos deles podem nem existir a necessidade.</p>
</div>



### Pasta utils

A pasta de `/utils` guarda todas as ferramentas e auxiliares de SASS usados por todo o projeto. Todas as funções globais, mixins e placeholders devem ser colocados nesta pasta.

A regra desta pasta é que não deve produzir uma única linha de CSS se for compilada sozinha. Tudo o que está aqui deverá ser nada mais que auxiliares.

* `_variables.scss`
* `_mixins.scss`
* `_functions.scss`
* `_placeholders.scss` (normalmente chamado `_helpers.scss`)

<div class="note">
  <p>A pasta <code>utils/</code> também pode ser chamada de <code>helpers/</code>, <code>sass-helpers/</code> ou <code>sass-utils/</code>, sendo uma questão de preferência.</p>
</div>



### Vendors folder

And last but not least, most projects will have a `vendors/` folder containing all the CSS files from external libraries and frameworks – Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered, and so on. Putting those aside in the same folder is a good way to say “Hey, this is not from me, not my code, not my responsibility”.

* `_normalize.scss`
* `_bootstrap.scss`
* `_jquery-ui.scss`
* `_select2.scss`

If you have to override a section of any vendor, I recommend you have an 8th folder called `vendors-extensions/` in which you may have files named exactly after the vendors they overwrite.

For instance, `vendors-extensions/_boostrap.scss` is a file containing all CSS rules intended to re-declare some of Bootstrap's default CSS. This is to avoid editing the vendor files themselves, which is generally not a good idea.



### Main file

The main file (usually labelled `main.scss`) should be the only Sass file from the whole code base not to begin with an underscore. This file should not contain anything but `@import` and comments.

Files should be imported according to the folder they live in, one after the other in the following order:

1. `vendors/`
1. `utils/`
1. `base/`
1. `layout/`
1. `components/`
1. `pages/`
1. `themes/`

In order to preserve readability, the main file should respect these guidelines:

* one file per `@import`;
* one `@import` per line;
* no new line between two imports from the same folder;
* a new line after the last import from a folder;
* file extensions and leading underscores omitted.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
@import 'vendors/bootstrap';
@import 'vendors/jquery-ui';

@import 'utils/variables';
@import 'utils/functions';
@import 'utils/mixins';
@import 'utils/placeholders';

@import 'base/reset';
@import 'base/typography';

@import 'layout/navigation';
@import 'layout/grid';
@import 'layout/header';
@import 'layout/footer';
@import 'layout/sidebar';
@import 'layout/forms';

@import 'components/buttons';
@import 'components/carousel';
@import 'components/cover';
@import 'components/dropdown';

@import 'pages/home';
@import 'pages/contact';

@import 'themes/theme';
@import 'themes/admin';
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
@import vendors/bootstrap
@import vendors/jquery-ui

@import utils/variables
@import utils/functions
@import utils/mixins
@import utils/placeholders

@import base/reset
@import base/typography

@import layout/navigation
@import layout/grid
@import layout/header
@import layout/footer
@import layout/sidebar
@import layout/forms

@import components/buttons
@import components/carousel
@import components/cover
@import components/dropdown

@import pages/home
@import pages/contact

@import themes/theme
@import themes/admin
{% endhighlight %}
  </div>
</div>

There is another way of importing partials that I deem valid as well. On the bright side, it makes the file more readable. On the other hand, it makes updating it slightly more painful. Anyway, I'll let you decide which is best, it does not matter much. For this way of doing, the main file should respect these guidelines:

* one `@import` per folder;
* a linebreak after `@import`;
* each file on its own line;
* a new line after the last import from a folder;
* file extensions and leading underscores omitted.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
@import
  'vendors/bootstrap',
  'vendors/jquery-ui';

@import
  'utils/variables',
  'utils/functions',
  'utils/mixins',
  'utils/placeholders';

@import
  'base/reset',
  'base/typography';

@import
  'layout/navigation',
  'layout/grid',
  'layout/header',
  'layout/footer',
  'layout/sidebar',
  'layout/forms';

@import
  'components/buttons',
  'components/carousel',
  'components/cover',
  'components/dropdown';

@import
  'pages/home',
  'pages/contact';

@import
  'themes/theme',
  'themes/admin';
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
@import
  vendors/bootstrap,
  vendors/jquery-ui

@import
  utils/variables,
  utils/functions,
  utils/mixins,
  utils/placeholders

@import
  base/reset,
  base/typography

@import
  layout/navigation,
  layout/grid,
  layout/header,
  layout/footer,
  layout/sidebar,
  layout/forms

@import
  components/buttons,
  components/carousel,
  components/cover,
  components/dropdown

@import
  pages/home,
  pages/contact

@import
  themes/theme,
  themes/admin
{% endhighlight %}
  </div>
</div>

<div class="note">
  <p>In order to not have to import each file manually, there is an extension to Ruby Sass called <a href="https://github.com/chriseppstein/sass-globbing">sass-globbing</a>, making it possible to use glob patterns in Sass <code>@import</code> such as <code>@import "components/*"</code>.</p>
  <p>That being said, I would not recommend it because it imports files following the alphabetical order which is usually not what you want, especially when dealing with a source-order dependent language.</p>
</div>






## Shame file

There is an interesting concept that has been made popular by [Harry Roberts](http://csswizardry.com), [Dave Rupert](http://daverupert.com) and [Chris Coyier](http://css-tricks.com) that consists of putting all the CSS declarations, hacks and things we are not proud of in a *shame file*. This file, dramatically titled `_shame.scss`, would be imported after any other file, at the very end of the stylesheet.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/**
 * Nav specificity fix.
 *
 * Someone used an ID in the header code (`#header a {}`) which trumps the
 * nav selectors (`.site-nav a {}`). Use !important to override it until I
 * have time to refactor the header stuff.
 */
.site-nav a {
    color: #BADA55 !important;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/**
 * Nav specificity fix.
 *
 * Someone used an ID in the header code (`#header a {}`) which trumps the
 * nav selectors (`.site-nav a {}`). Use !important to override it until I
 * have time to refactor the header stuff.
 */
.site-nav a
    color: #BADA55 !important
{% endhighlight %}
  </div>
</div>



### Further reading

* [shame.css](http://csswizardry.com/2013/04/shame-css/)
* [shame.css - full .net interview](http://csswizardry.com/2013/04/shame-css-full-net-interview/)
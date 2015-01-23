# Arquitetura

Criar a arquitetura de um projeto de CSS é uma das coisas mais difíceis que terás que fazer durante a vida de um projeto.
Manter essa arquitetura constante e significativa é ainda mais difícil.

Felizmente, um dos benefícios principais de usar um pré-processador de CSS é ter a habilidade de dividir a nossa base de código em vários ficheiros sem ter impacto na performance (como a diretiva de CSS `@import` fazia). Graças à sobrecarga da diretiva `@import` no Sass, é perfeitamente seguro (e até recomendado) usar os ficheiros necessários na fase de desenvolvimento, todos estes compilados numa única stylesheet quando o projeto for para produção.

Em cima disso, não posso salientar o suficiente a necessidade de pastas, mesmo em pequenos projetos. Em casa, não deixas todas as folhas de papel na mesma caixa. Tens uma para os papéis da casa, uma para documentos do banco, uma para contas e assim em diante. Não há razão para fazeres de maneira diferente quando estás a estruturar um projeto de CSS. Separa o teu código em pastas com nomes compreensíveis para depois ser fácil encontrar qualquer código quando mais tarde tiveres que voltar ao projeto.

Há muitas arquiteturas populares para projectos de CSS: [OOCSS](http://oocss.org/), [Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/), arquitetura usada no [Bootstrap](http://getbootstrap.com/), arquitetura usada no [Foundation](http://foundation.zurb.com/)... Todas têm os seus méritos, prós e contras.

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

A maior parte de qualquer interface pode ser pensada como pequenos componentes e eu recomendo que fique com este paradigma. Isto vai não só diminuir a quantidade de CSS necessário para um projeto completo, mas também acaba por ser muito mais fácil so que manter uma desorganização onde está tudo junto.




## O padrão 7-1

Vamos então voltar à arquitetura, ok? Eu normalmente uso o que chamo *O padrão 7-1*: 7 pastas, 1 ficheiro. Basicamente, tudo o que tens são ficheiros parciais colocados em 7 pastas diferentes, e um único ficheiro na raiz do projeto (normalmente chamado `main.scss`) que importa todos os ficheiros parciais para serem compilados numa única stylesheet de CSS.

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
  <img src="/assets/images/sass-wallpaper.jpg" alt="Um ficheiro para governá-los todos, um ficheiro para encontrá-los, um ficheiro para trazê-los todos, e a maneira do SASS para fundi-los." />
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
|   |- _home.scss        # Estilos especificos á página Inicial
|   |- _contact.scss     # Estilos especificos á página de Contacto
|   ...                  # Etc...
|
|- themes/
|   |- _theme.scss       # Tema Padrão
|   |- _admin.scss       # Tema de Administração
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
  <p>Os ficheiros seguem as mesma convenções de nome descritas acima: são delimitados com um hífen.</p>
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
  <p>A pasta <code>layout/</code> também pode ser chamada <code>partials/</code>, sendo isto uma questão de preferência.</p>
</div>



### Pasta Components

Para componentes mais pequenos, há a pasta `components/`. Enquanto a pasta `layout/`é *macro* (definindo a estrutura global), a pasta `components/` é mais focada em módulos. Contêm todo o tipo de módulos específicos como um slider, um carregador e tudo que seja desse tipo.
Há normalmente imensos ficheiros na pasta `components/` tendo em conta que todo o site/aplicação deverá ser constituído por pequenos módulos.

* `_media.scss`
* `_carousel.scss`
* `_thumbnails.scss`

<div class="note">
  <p>A pasta <code>components/</code> também se poderá chamar <code>modules/</code>, sendo isto uma questão de preferência.</p>
</div>



### Pasta Pages

Se tiveres estilos específicos a páginas, o melhor será colocá-las na pasta `pages/`, num ficheiro com o nome da página. Por exemplo, não deixa de ser comum ter estilos muito específicos para a página inicial que criam a necessidade de ter um `_home.scss` na pasta `pages/`.

* `_home.scss`
* `_contact.scss`

<div class="note">
  <p>Dependendo do processo de desenvolvimento estes ficheiros podem ser chamados individualmente para evitar que eles se juntem com outros quando todas as stylesheets se juntam. Na realidade depende è uma questão de preferência.</p>
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



### Pasta Vendors

E por fim, a maioria dos projetos irão ter uma pasta `vendors/` que vai conter todo o CSS usado por livrarias e frameworks externas - Normalize, Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered, e por ai. Por todos estes componentes na mesma pasta é uma boa maneira de dizer "Hey, este código não é meu, não o escrevi, não é a minha responsabilidade".

* `_normalize.scss`
* `_bootstrap.scss`
* `_jquery-ui.scss`
* `_select2.scss`

Se tiveres que substituir uma secção de alguma destas extensões, eu recomendo criar um oitava pasta chamada `vendors-extensions/` na qual estarão ficheiros com os mesmos nomes dos quais estás a substituir.

Por exemplo, `vendors-extensions/_boostrap.scss` é um ficheiro que contém todas as regras de CSS que tiveste que declarar de novo por cima do CSS padrão do Bootstrap. Isto é para evitar editar os ficheiros originais das extensões, o que normalmente não é uma boa ideia.



### Ficheiro Principal

O ficheiro principal (normalmente chamado `main.scss`) deverá ser o único ficheiro de SASS que não começa com um underscore. Este ficheiro não deve conter nada mais que `@import` e comentários.

Os ficheiros devem ser importados de acordo com a pasta onde estão, uma depois da outra na seguinte ordem:

1. `vendors/`
1. `utils/`
1. `base/`
1. `layout/`
1. `components/`
1. `pages/`
1. `themes/`

De maneira a preservar a legibilidade, o ficheiro principal deverá seguir as seguintes diretrizes:

* um ficheiro por `@import`;
* um `@import`por linha;
* não colocar linha de espaço entre importações da mesma pasta;
* uma linha de espaço depois da ultima importação de uma pasta;
* extensões e underscores antes do nome devem ser omitidos.

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

Existe outra maneira de importar parciais que também considero válida. O lado positivo dela é que torna o ficheiro mais legível. Por outro lado, faz qualquer mudança a esse ficheiro mais difícil. De qualquer maneira eu vou deixar isto ao vosso critério pois a diferença não é muita. Ao importar desta maneira o ficheiro principal deve seguir as seguintes diretrizes:

* um `@import`por pasta;
* linha de espaço entre cada `@import`;
* cada ficheiro fica na sua linha;
* uma linha de espaço depois da ultima importação numa pasta;
* extensões e underscores antes do nome devem ser omitidos.

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
  <p>De maneira a não ter que importar cada ficheiro manualmente, existe uma extensão para o Sass chamada <a href="https://github.com/chriseppstein/sass-globbing">sass-globbing</a>, que torna possivel usar padrões globais no <code>@import</code> como <code>@import "components/*"</code>.</p>
  <p>Tendo isto dito, eu não recomendo o uso desta extensão porque ela importa os ficheiros por ordem alfabética e normalmente não é isto que queremos, principalmente quando lidamos com uma linguagem que se baseia na ordem.</p>
</div>





## Ficheiro Vergonhoso

Existe um conceito interessante que foi tornado popular por [Harry Roberts](http://csswizardry.com), [Dave Rupert](http://daverupert.com) e [Chris Coyier](http://css-tricks.com) que consiste em colocar todas as declarações, hacks e coisas das quais não estamos propriamente orgulhosos num *ficheiro vergonhoso*. Este ficheiro dramaticamente chamado `_shame.css`, seria importado depois de todos os outros mesmo no fim da stylesheet.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
/**
 * Arranjar a navegação.
 *
 * Alguém usou um ID no código do cabeçalho (`#header a {}`) que passa por cima
 * dos seletores da navegação (`.site-nav a {}`). Usar !important para sobrepor 
 * estes até ter tempo de refazer o código do cabeçalho.
 */
.site-nav a {
    color: #BADA55 !important;
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
/**
 * Arranjar a navegação.
 *
 * Alguém usou um ID no código do cabeçalho (`#header a {}`) que passa por cima
 * dos seletores da navegação (`.site-nav a {}`). Usar !important para sobrepor 
 * estes até ter tempo de refazer o código do cabeçalho.
 */
.site-nav a
    color: #BADA55 !important
{% endhighlight %}
  </div>
</div>



### Leitura Adicional

* [shame.css](http://csswizardry.com/2013/04/shame-css/)
* [shame.css - Entrevista completa .net](http://csswizardry.com/2013/04/shame-css-full-net-interview/)
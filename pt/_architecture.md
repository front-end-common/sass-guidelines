# Arquitectura

Criar a arquitectura de um projecto de CSS é uma das coisas mais dificeis que terC!s que fazer durante a vida desse projecto.
Manter essa arquitectura constante e significativa é ainda mais dificil.

Felizmente, um dos beneficios principais de usar um preprocessor de CSS C) ter a habilidade de dividir a nossa base de código em vários ficheiros sem ter impacto na performance (como a directiva de CSS `@import` fazia). Graças á sobrecarga da directiva `@import` no Sass, é perfeitamente seguro(e até recomendado) usar os ficheiros necessC!rios na fase de desenvolvimento, todos estes compilados num unica stylesheet quando o projecto for para produçõ.

Em cima disso, não posso salientar o suficiente a necessidade de pastas, mesmo em pequenos projectos. Em casa, não deixas todas as folhas de papel na mesma caixa. Tens uma para papeis da casa, uma para documentos do banco, uma contas e assim em diante. Não há razão para fazeres de maneira difrente quando estás a estruturar um projecto de CSS. Separa o teu código em pastas com nomes compreensiveis para depois ser fácil encontrar qualquer código quando mais tarde tiveres que voltar ao projecto.

Há muitas arquitecturas populares para projectos de CSS: [OOCSS](http://oocss.org/), [Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/), como [Bootstrap](http://getbootstrap.com/), como [Foundation](http://foundation.zurb.com/)... Todas teêm os seus méritos, prós e contras.

Eu uso uma abordagem que acaba por ser muito paraecida com [SMACSS](https://smacss.com/) de [Jonathan Snook](http://snook.ca/), e que se foca em manter as coisas simples e óbvias.

<div class="note">
  <p>Eu aprendi que a arquitectura é muito especifica para o projeto. Sente te á vontade para ignorares ou adpatares a solução proposta para lidares com um sistema que se adapta melhor ás tuas necessidades.</p>
</div>

### Leitura Adicional

* [Arquitetura para um projecto de SASS](http://www.sitepoint.com/architecture-sass-project/)
* [Uma Olhada a diferentes arquiteturas de SASS](http://www.sitepoint.com/look-different-sass-architectures/)
* [FR] [Sass, une architecture composée](http://slides.com/hugogiraudel/sass-une-architecture-composee)
* [SMACSS](https://smacss.com/)
* [Uma introdução a  OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)
* [Atomic Web Design](http://bradfrost.com/blog/post/atomic-web-design/)






## Componentes

Há uma grande diferença entre fazer algo *funcionar* e fazer algo *bom*. Mais uma vez, CSS é uma linguagem muito desorganizada <sup>[Citação Necessária]</sup>. Quanto menos CSS tivermos melhor. Nós não queremos lidar com megabytes de CSS. Para manter as nossas stylesheets pequenas e efecientes&mdash;e isto não será nenhuma supresa para ti&mdash; é normalmente uma boa ideia pensar numa interface como uma colecção de componentes.

Componentes podem ser qualquer coisa desde que:

* façam uma e apenas uma coisa;
* sejam reutilizáveis e usados por todo o projecto;
* sejam independentes.

Por exemplo um formulário de pesquisa devem ser tratado como um componente. Deverá ser reutilizável, em diferentes posições, páginas e em situações diversas. Não deve depender da sua posição na DOM (rodapé, barra lateral, conteudo principal..).

A maior parte de qualquer interface pode ser pensada como pequenos componentes e eu recomendo que fique com este paradigma. Isto vai não só diminuir a quantidade de CSS necessário para um projecto completo, mas também acaba por ser muito mais fácil de manter do que uma desorganização onde tudo está tudo junto. 




## O padrão 7-1

Vamos então voltar á arquitetra, ok ? Eu normalmente uso o que chamo *O padrão 7-1*: 7 pastas, 1 ficheiro. Basicamnente, tudo o que tens são ficheiros parciais colocados em 7 pastas diferentes, e um único ficheiro na raiz do projeto (normalmente chamado `main.scss`) que importa todos os ficheiros parciais para serem compilados numa stylesheet de CSS.

* `base/`
* `componentes/`
* `layout/`
* `páginas/`
* `temas/`
* `utilidades/`
* `vendors/`

E claro:

* `main.scss`

<figure role="group">
  <img src="/assets/images/sass-wallpaper.jpg" alt="Um ficheiro para governá-los todos, um ficheiro para encontrá-los, um ficheiro para trazê-los todos, E a maneira do SASS para fundi-los." />
  <figcaption>Wallpaper de <a href="https://twitter.com/julien_he">Julien He</a></figcaption>
</figure>

Idealmente, teriamos algo como:

<div class="highlight"><pre><code>
sass/
|
|- base/
|   |- _reset.scss       # Reset
|   |- _typography.scss  # Regras de Tipografia
|   ...                  # Etc...
|
|- componentes/
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
|- paginas/
|   |- _home.scss        # Estilos especificos á Home
|   |- _contact.scss     # Estilos especificos á página de Contacto
|   ...                  # Etc...
|
|- themes/
|   |- _theme.scss       # Tema Padrão
|   |- _admin.scss       # Tema de Adminisração
|   ...                  # Etc...
|
|- utilidades/
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
  <p>Os ficheiros seguem as mesma convenções de nome descritas em acima: são delimitados com um hifen.</p>
</div>


### A pasta base

A pasta `base/`contém o que nós podemos chamar de código padrão para o projeto. Aqui podemos encontrar um ficheiro de reset, algumas regras tipográficas e provavelmente uma stylesheet (que estou a chamar `_base.scss`), que define alguns estilos padrão para elementos de HTML mais usados.

* `_base.scss`
* `_reset.scss`
* `_typography.scss`



### Pasta Layout

A pasta `layout/` contêm tudo que é nesesário para criar o layout do site ou aplicação. Esta pasta contêm as stylesheets para as partes principais do site (cabeçalho, rodapé, navegação, barra lateral...), a grelha ou mesmo o CSS de todos os formulários.  

* `_grid.scss`
* `_header.scss`
* `_footer.scss`
* `_sidebar.scss`
* `_forms.scss`
* `_navigation.scss`

<div class="note">
  <p>A pasta <code>layout/</code> também pode ser chamada <code>parciais/</code>, sendo isto uma questão de preferência.</p>
</div>



### Pasta de Componentes

Para componentes mais pequenos, há a pasta `componentes/`. Enquanto a pasta `layout/`é *macro* (definindo a estrutura global), a pasta `componentes/` é mais focada em módulos. Contêm todo o tipo de módulos especificos como um slider, um carregador e tudo que seja desse tipo.
Há normalmente imensos ficheiros na pasta `componentes/` tendo em conta que todo o site/aplicação deverá ser constituido por pequenos módulos.

* `_media.scss`
* `_carousel.scss`
* `_thumbnails.scss`

<div class="note">
  <p>A pasta <code>componentes/</code> também se poderá chamar <code>modulos/</code>, sendo isto uma questão de preferência.</p>
</div>



### A pasta páginas

If you have page-specific styles, it is better to put them in a `pages/` folder, in a file named after the page. For instance, it's not uncommon to have very specific styles for the home page hence the need for a `_home.scss` file in `pages/`.

* `_home.scss`
* `_contact.scss`

<div class="note">
  <p>Depending on your deployment process, these files could be called on their own to avoid merging them with the others in the resulting stylesheet. It is really up to you.</p>
</div>



### Pasta Temas

On large sites and applications, it is not unusual to have different themes. There are certainly different ways of dealing with themes but I personally like having them all in a `themes/` folder.

* `_theme.scss`
* `_admin.scss`

<div class="note">
  <p>This is very project-specific and is likely to be non-existent on many projects.</p>
</div>



### Utils folder

The `utils/` folder gathers all Sass tools and helpers used across the project. Every global variable, function, mixin and placeholder should be put in here.

The rule of thumb for this folder is that it should not output a single line of CSS when compiled on its own. These are nothing but Sass helpers.

* `_variables.scss`
* `_mixins.scss`
* `_functions.scss`
* `_placeholders.scss` (frequently named `_helpers.scss`)

<div class="note">
  <p>The <code>utils/</code> folder might also be called <code>helpers/</code>, <code>sass-helpers/</code> or <code>sass-utils/</code>, depending on what you prefer.</p>
</div>



### Vendors folder

And last but not least, most projects will have a `vendors/` folder containing all the CSS files from external libraries and frameworks b
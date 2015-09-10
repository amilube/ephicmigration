<div class="container">
    <div class="row">
    <h1> ephicmigration v1.0 </h1>
    <p>Migración de Django1.2 a 1.6</p>
    <h1 id="versión-1.2.7">Versión 1.2.7</h1>
    <p><em>Septiembre, 10 de 2011</em></p>
    <h1 id="versión-1.3">Versión 1.3</h1>
    <p><em>Marzo, 23 de 2011</em></p>
    <h2 id="nuevas-características-y-cambios">Nuevas Características y Cambios</h2>
    <h3 id="vistas-basadas-en-clases">Vistas basadas en clases</h3>
    <p>Para reemplazar las viejas referencias a las funciones genéricas de las vistas hay que usar <strong>as_view()</strong> para crear una &quot;instanciación&quot; de las nuevas vistas genéricas basadas en clases.</p>
    <ul>
    <li><p><strong>django.views.generic.simple.redirect_to</strong></p>
    <p>Lo que antes era</p>
    <pre class="sourceCode Python"><code class="sourceCode python"><span class="ch">from</span> django.views.generic.simple <span class="ch">import</span> redirect_to
    ...
    (<span class="st">&#39;^about/$&#39;</span>, direct_to_template, {<span class="st">&#39;template&#39;</span>: <span class="st">&#39;about.html&#39;</span>})</code></pre>
    <p>ahora se escribe:</p>
    <pre class="sourceCode Python"><code class="sourceCode python"><span class="ch">from</span> django.views.generic.base <span class="ch">import</span> TemplateView
    ...
    (<span class="st">&#39;^about/$&#39;</span>, TemplateView.as_view(template_name=<span class="st">&#39;about.html&#39;</span>))</code></pre></li>
    <li><p><strong>django.views.generic.list_detail.object_list</strong> pasa a ser <strong>django.views.generic.list.ListView</strong> En vez de:</p>
    <pre class="sourceCode Python"><code class="sourceCode python">object_list(request, template_name=template_name, **kwargs)</code></pre>
    <p>Una forma rápida de solucionarlo es:</p>
    <pre class="sourceCode Python"><code class="sourceCode python">render_to_response(request, template_name=template_name, **kwargs)                </code></pre>
    <p>Digo una forma rápida porque en realidad, esta solución se aplica cuando se adapta un proyecto con vistas basadas en funciones, para una implementación menos <em>herética</em> es necesario definir una clase que herede de ListView y a partir de allí realizar la implementación de la vista. <a href="https://docs.djangoproject.com/en/1.4/topics/generic-views-migration/#replace-generic-views-with-generic-classes">[Más información]</a></p></li>
    <li><p>static files: agrega <strong>django.contrib.staticfiles</strong> para manejar los archivos estáticos necesarios para renderizar un página.</p>
    <p>Se separan los archivos esáticos subidos por el usuario de los que son necesarios para renderizar la página (JS, CSS, imágenes, etc) y pasan a ubicarse en subdirectorios de <em>static/</em> d cada app o en dirctorios listados en STATICFILES_DIRS y que se guradarán en STATIC_URL.</p></li>
    <li>Agrega soporte para <em>unittest2</em></li>
    <li>En los <em>template tags</em>:
    <ul>
    <li><em>include</em> acepta la opcion <strong>with</strong> para especificar el contexo de las variables incluidas en la plantilla.</li>
    <li>También el <em>include</em> acepta la opción <strong>only</strong>, lo que permite excluir el contexto actual del contexto incluido.</li>
    <li>El tag <strong>with</strong> permite definir multiples contextos para las variables en un simple bloque de <em>with</em>.</li>
    <li>El tag <strong>load</strong> acepta un argumento <strong>from</strong>, permitiendo cargar un simple tag o filter desde una librería.</li>
    </ul></li>
    <li>Agrega la clase <strong>TemplateResponse</strong></li>
    <li><p><strong>Caching changes</strong></p>
    <p>Django 1.3 sees the introduction of several improvements to the Django’s caching infrastructure.</p>
    <p>Firstly, Django now supports multiple named caches. In the same way that Django 1.2 introduced support for multiple database connections, Django 1.3 allows you to use the new CACHES setting to define multiple named cache connections.</p>
    <p>Secondly, versioning, site-wide prefixing and transformation have been added to the cache API.</p>
    <p>Thirdly, cache key creation has been updated to take the request query string into account on GET requests.</p>
    <p>Finally, support for pylibmc has been added to the memcached cache backend.</p>
    <p>For more details, see the documentation on caching in Django.</p></li>
    <li><p><strong>Permisos para usuarios inactivos</strong></p>
    <p>Se puede asignar <strong>True</strong> a <strong>supports_inactive_user</strong> y una instancia de <em>User</em> inactiva verifica el backend de los permisos.</p></li>
    <li><strong>MEDIA_URL y STATIC_URL debe terminar con una barra</strong></li>
    </ul>
    <h2 id="características-deprecadas">Características Deprecadas</h2>
    <ul>
    <li>soporte para mod_python</li>
    <li>Vistas genéricas basadas en funciones
    <ul>
    <li><strong>django.views.generic.create_update</strong></li>
    <li><strong>django.views.generic.date_based</strong></li>
    <li><strong>django.views.generic.list_detail</strong></li>
    <li><strong>django.views.generic.simple</strong></li>
    </ul></li>
    <li><p>Cambios a <em>url</em> y <em>ssi</em></p>
    <p>Escribir</p>
    <pre class="sourceCode html"><code class="sourceCode html">{% load url from future %}
    {% url &#39;sample&#39; %}</code></pre>
    <p>en vez de</p>
    <pre class="sourceCode html"><code class="sourceCode html">{% extends templ %}</code></pre>
    <p>(siendo que <em>templ</em> contiene el valor <em>base.html</em>)</p></li>
    <li><strong>Cambios en los métodos de login del admin</strong> Esta release refactoriza el mecanismo de login del admin para usar una subclase de AhenticationForm en lugar de una forma(o &quot;en lugar de un formulario&quot;) manual de validación. <strong>django.contrib.admin.sites.AdminSite.display_login_form</strong> se removió en favor del atributo <strong>login_form</strong>.</li>
    </ul>
    <h1 id="versión-1.4">Versión 1.4</h1>
    <p><em>Marzo, 23 de 2012</em></p>
    <h2 id="nuevas-características">Nuevas Características</h2>
    <ul>
    <li><strong>Personalización de las plantillas de projects y app</strong> A los comandos <strong>startapp</strong> y <strong>startproject</strong> se le agrega la opción <strong>--template</strong> para especificar la ruta o URL de la plantilla personalizada de app o project. También se puede pasar el directorio de destino como un segundo argumento a <strong>startapp</strong> y a <strong>startproject</strong></li>
    <li>Se agrega un a lista de filtros a la interface del Admin</li>
    <li>Se agrega la posibilidad de ordenar múltiples columnas clickeando en las cabeceras de las mismas. El nuevo método <strong>get_ordering()</strong> para especificar dinamicamente el orden(es decir, dependiendo de las peticiones)</li>
    <li>Nuevos métodos para <strong>ModelAdmin</strong>
    <ul>
    <li><strong>save_related()</strong></li>
    <li><strong>get_list_display()</strong></li>
    <li><strong>get_list_display_link()</strong></li>
    </ul></li>
    <li>Elementos <em>inline</em> de Admin respetan los permisos de usuario</li>
    <li>El template tag <strong>if</strong> soporta <strong>{% elif %}</strong></li>
    <li>Se agrega el método <strong>distinc()</strong> a <strong>QuerySet</strong> (soportado sólo en PostgreSQL)</li>
    <li>Es posible pasar valores iniciales a los <em>model formsets</em> y a los <em>inline model formsets</em> como valores retornados de las funciones factory (modelformset_factory y ilineformeset_factory respectivamente) como si fuesen formsets comunes. Sin embargo, los valores iniciales, solo aplican a forms adicionales,es decir, aquellos valores que no existen en la instancia del modelo.</li>
    <li><strong>SECRET_KEY</strong> es requerida en <em>settings</em></li>
    <li><p><strong>ADMIN_MEDIA_PREFIX</strong> es deprecada y reemplazada por <strong>STATIC_URL</strong> Si se definió <strong>ADMIN_MEDIA_PREFIX</strong> con un dominio específico (por ejemplo, <a href="http://media.ejemplo.com/admin/">http://media.ejemplo.com/admin/</a>), asegúrese de redefinir su <strong>STATIC_URL</strong> con la URL correcta - por ejemplo <a href="http://media.ejemplo.com/admin/">http://media.ejemplo.com/admin/</a></p>
    <strong>Nota:</strong> Si se usa implícitamente la ruta de los archivos estáticos del admin del código fuente de Django, se debe cambiar dicha ruta. Los archivos fueron trasladados desde <strong>django/contrib/admin/media/</strong> a <strong>django/contrib/admin/static/admin/</strong>.</li>
    <li>Serialización de <strong>datatime</strong> y <strong>time</strong>: se usa la letra <strong>T</strong> para separar la parte de la fecha de la parte del tiempo en lugar de un espacio en blanco.</li>
    <li>Se cambia <em>django.core.template_loaders</em> a <em>django.template.loaders</em></li>
    <li><strong>django.db.models.fields.URLField.verify_exists</strong> : Cualquier uso de verify_exists debe eliminarse por problemas de seguridad y rendimiento intratables.</li>
    <li><p>El parámetro <strong>mixin</strong> del método <strong>open</strong> (de django.core.files.storage.Storage.open) ha sido eliminado. Si se ha usado este parámetro se debe sobreescribir el método <em>open</em> de la siguiente manera.</p>
    <pre class="sourceCode python"><code class="sourceCode python"><span class="ch">from</span> django.core.files <span class="ch">import</span> File
    <span class="ch">from</span> django.core.files.storage <span class="ch">import</span> FileSystemStorage

    <span class="kw">class</span> Spam(File):
        <span class="co">&quot;&quot;&quot;</span>
    <span class="co">    Spam, spam, spam, spam and spam.</span>
    <span class="co">    &quot;&quot;&quot;</span>
        <span class="kw">def</span> ham(<span class="ot">self</span>):
            <span class="kw">return</span> <span class="st">&#39;eggs&#39;</span>

    <span class="kw">class</span> SpamStorage(FileSystemStorage):
        <span class="co">&quot;&quot;&quot;</span>
    <span class="co">    A custom file storage backend.</span>
    <span class="co">    &quot;&quot;&quot;</span>
        <span class="kw">def</span> <span class="dt">open</span>(<span class="ot">self</span>, name, mode=<span class="st">&#39;rb&#39;</span>):
            <span class="kw">return</span> Spam(<span class="dt">open</span>(<span class="ot">self</span>.path(name), mode))</code></pre></li>
    <li>El servidor de desarrollo es multihilos en forma predefinida. Para deshabilitarlo se debe usar la opción <strong>--nothreading</strong> al correr el servidor</li>
    <li>Las formas heredadas de llamar <strong>cache_page()</strong> han sido deprecadas. Ver documentación del decorador <em>cache_page</em></li>
    <li>Ahora las excepciones de <em>Request</em> son simepre &quot;logeadas&quot;</li>
    <li>Las funciones <em>include()</em>, <em>patterns()</em>, y <em>url()</em> más <em>handler500</em>, <em>handler404</em> que se localizaban en el módulo <strong>django.conf.urls.defaults</strong> ahora pasan a estar en <strong>django.conf.urls</strong></li>
    <li><strong>django.core.mangement.setup.environ</strong> y <strong>django.core.management.execute_manager</strong> están deprecadas.</li>
    <li><p>Los atributos <em>is_safe</em> y <em>needs_autoescape</em> de los template filters, son reemplazados por argumentos de <strong>@register.filter</strong></p>
    <p>Pasa de ser:</p>
    <blockquote>
    <pre class="sourceCode python"><code class="sourceCode python"><span class="ot">@register.filter</span>
    <span class="kw">def</span> noop(value):
        <span class="kw">return</span> value
    noop.is_safe = <span class="ot">True</span></code></pre>
    </blockquote>
    <p>a escribirse de la siguiente manera:</p>
    <blockquote>
    <pre class="sourceCode python"><code class="sourceCode python"><span class="ot">@register.filter</span>(is_safe=<span class="ot">True</span>)
    <span class="kw">def</span> noop(value):
        <span class="kw">return</span> value</code></pre>
    </blockquote></li>
    <li>No se aceptan comodines en <strong>INSTALLED_APPS</strong></li>
    <li><strong>HttpRequest.raw_post_data</strong> renombrado a como <strong>HttpRequest.body</strong></li>
    <li><strong>django.contrib.sitemaps</strong> solución de bug con potenciales implicancias en el rendimiento. Usar <a href="https://docs.djangoproject.com/en/1.6/topics/cache/">caching framework</a> en su subclase de <strong>Sitemap</strong></li>
    </ul>
    <h4 id="django.core.management.execute_manager">django.core.management.execute_manager</h4>
    <p>Esta función se usaba por manage.py para ejecutar el comando de &quot;management&quot;. Es idéntica a <strong>django.core.management.execute_from_command_line</strong>, exceptuando que esta <strong>execute_manager</strong> llama a <strong>setup_environ</strong>, la cual ahora está deprecada. Por lo tanto, hay que usar <strong>execute_from_command_line</strong> en lugar de <strong>execute_manager</strong></p>
    <h1 id="versión-1.5">Versión 1.5</h1>
    <p><em>Febrero 26, de 2013</em></p>
    <h2 id="nuevas-características-1">Nuevas Características</h2>
    <ul>
    <li><strong>User</strong> <em>model</em> configurable.</li>
    <li><strong>Soporte para guardar un subconjunto de compos del modelo.</strong> Al método <em>Model.save()</em> se le puede pasar el nuevo argumento <strong>update_fields</strong>. Ver la documentación de <a href="https://docs.djangoproject.com/en/1.6/ref/models/instances/#django.db.models.Model.save">Model.save()</a> por más detalles.</li>
    <li><p><strong>&quot;Cacheo&quot; de instancias relacionadas del modelo.</strong> Cuando hay relaciones cruzadas, el ORM podrá evitar volver a hacer las consultas a objetos previamente cargados. Por ejemplo.</p>
    <pre class="sourceCode python"><code class="sourceCode python">&gt;&gt;&gt; first_poll = Poll.objects.<span class="dt">all</span>()[<span class="dv">0</span>]
    &gt;&gt;&gt; first_choice = first_poll.choice_set.<span class="dt">all</span>()[<span class="dv">0</span>]
    &gt;&gt;&gt; first_choice.poll is first_poll
    <span class="ot">True</span></code></pre>
    <p>En Django 1.5, la tercer línea no lanza una nueva y larga consulta SQL para traer <strong>first_choise.poll</strong>; esta fué asignada (&quot;setada&quot;) en la segunda línea.</p>
    Para relaciones <em>uno a uno</em>, se puede cachear en ambas direcciones. Para las relaciones <em>muchos a uno</em>, solo el lado simple (&quot;el lado uno de la relación muchos a uno&quot;) se cachea. Esto es particularmente útil en combinación con <strong>prefetch_related</strong></li>
    <li><strong>Soporte Explícito para respuestas streaming</strong> En versiones anteriores se creaban respuestas streaming pasando un iterador a <strong>HttpResponse</strong> pero esto era inseguro. Ahora, se puede generar explícitamente una respuesta streaming con la nueva clase <strong>StreamingHttpResponse</strong></li>
    <li>Template tag <strong>{% verbatim%}</strong> Se puede usar un bloque <strong>verbatim</strong> para evitar las colisiones entre la sintaxis de Javascript con la sintaxis de Django. Ver <a href="https://docs.djangoproject.com/en/1.6/ref/templates/builtins/#std:templatetag-verbatim">detalles</a></li>
    <li><a href="https://docs.djangoproject.com/en/1.6/releases/1.5/#retrieval-of-contenttype-instances-associated-with-proxy-models">Obtención de instancias de <strong>ContentType</strong> asociadas con <em>modelos proxy</em></a></li>
    <li>Nueva variable <strong>view</strong> en el contexto de las vistas basadas en clases. Esta variable apunta a la instancia de <strong>View</strong></li>
    <li>El motor de plantillas ahora interpreta <strong>True</strong>, <strong>False</strong> y <strong>None</strong> como los correspondientes objetos en Python.</li>
    <li>Las vistas genéricas soportan petiociones OPTIONS</li>
    <li>En el admin se which they are members o puede filtrar por grupos a los usuarios</li>
    <li>Django ahora provee páginas por defecto para los errores 500 y 404.</li>
    <li><strong>ALOWED_HOSTS</strong> es requerido en rpducción. Ver <a href="https://docs.djangoproject.com/en/1.6/ref/settings/#std:setting-ALLOWED_HOSTS">documentación</a></li>
    <li><strong>Manejadores en modelos abstractos.</strong> Si impletentó una funcionalidad sobre un manejador que se invoque usando la clase abstracta, deberá migrar a una lógica a un <strong>staticmethod</strong> o <strong>classmethod</strong> de Python en la case abstracta.</li>
    <li>Si está usando <strong>{{ year }}</strong> en sus plantillas debe reemplazarlo con <strong>{{ year|date:&quot;Y&quot; }}</strong></li>
    <li><strong>TemplateView</strong> ya no pasa un diccionario <strong>params</strong> en el contexto, en su lugar pasa las variables desde la URLconf directamente en el contexto.</li>
    <li><strong>reuest.POST</strong> ya no incluye <em>data posted</em> via peticiones HTTP sin especificar un formato en la cabecera. Para acceder a estos datos se debe utilizar ahora el atributo <strong>request.body</strong></li>
    <li><a href="https://docs.djangoproject.com/en/1.6/releases/1.5/#system-version-of-simplejson-no-longer-used">La versión del sistema <strong>simplejson</strong> ya no se utiliza</a></li>
    <li>Validación de <strong>previous_page_number</strong> y <strong>next_page_numbre</strong>. Ahora levantan una excepción <strong>InvalidPage</strong> cuando el número de página es muy alto o muy bajo.</li>
    <li>El diccionario <strong>cleaned_data</strong> se mantiene para los forms inválidos. Siempre está presente luego de una validación de form.</li>
    <li><strong>django.forms.ModelMultipleChoiceField</strong> ahora retorna un <strong>QuerySet</strong> vacío en vez de una lista vacía.</li>
    <li><strong>into_to_base36()</strong> apropiadamente levanta un <strong>TypeError</strong> en lugar del <strong>ValueError</strong> para inputs no enteros.</li>
    <li><strong>slugify</strong> y <strong>remove_tags</strong> ahora están disponibles como <strong>django.utils.text.slugify()</strong> y <strong>django.utils.html.remove_tags()</strong> respectivamente.</li>
    <li>En las <strong>expresiones F()</strong>, se reemplazan los operadores <strong>&amp;</strong> y <strong>|</strong> por <strong>.bitand()</strong> y <strong>.bitor()</strong> rspectivamente</li>
    <li>Ahora, las <strong>expresiones F()</strong> siempre utilizan las mismas relaciones que otras búsquedas dentro de la llamada al mismo filtro</li>
    <li>El filtro <strong>csrf_token</strong> ya no se encierra en un div.</li>
    <li>La libreria de template tags <strong>adminmedia</strong> ha sido eliminada.</li>
    <li>Si usa <strong>django.contrib.redirects</strong>, asegure que <strong>INSTALLED_APPS</strong> contiene <strong>django.contri.sites</strong></li>
    <li>El acceso invertido a relaciones uno a uno a través de <strong>select_related()</strong> ahora levanta una excepción <strong>DoesNotExist</strong> en lugar de retornar <strong>None</strong></li>
    <li><strong>django.contrib.localflavor</strong> será removido en la versión 1.6. Vea la <a href="https://docs.djangoproject.com/en/1.6/topics/localflavor/#localflavor-how-to-migrate">documentación de migración</a></li>
    <li><strong>django.contrib.markup</strong> ha sido deprecado: es preferible usar el markup directamente de Python o de librerías de terceros.</li>
    <li><strong>AUTH_PROFILE_MODULE</strong>, con la introducción de modelos personalizados de User, este ya no necesitará un mecanismo de construcción para almacenar datos del perfil.</li>
    <li><strong>django.utils.encoding.StrAndUnicode</strong> ha sido deprecado. En su lugar, defina un método <strong>__str__</strong> y aplique el decorador <strong>python_2_unicode_compatible()</strong></li>
    <li>La función <strong>django.utils.itercompat.product</strong> ha sido deprecada . Use <strong>itertools.produc()</strong></li>
    <li>El comando <strong>cleanup</strong> ha sido deprecado y reemplazado por <strong>clearsessions</strong></li>
    <li>El argumento <strong>depth</strong> en <strong>select_related()</strong> ha sido deprecado. En su lugar deberá usar los nombres de los campos</li>
    </ul>
    <h1 id="versión-1.6">Versión 1.6</h1>
    <p><em>Noviembre 6, 2013</em></p>
    <h2 id="nuevas-características-2">Nuevas Características</h2>
    <ul>
    <li>Agrega el campo BinaryField al modelo</li>
    <li>Se agrega el comando <strong>check</strong> para comprobar si la configuración es compatible con la versión actual de Django (settings). <a href="https://docs.djangoproject.com/en/1.6/ref/django-admin/#django-admin-check">Ver detalles</a></li>
    <li>Se optimiza el algoritmo de <strong>Model.save()</strong>. Ahora prueba directamente un <strong>UPDATE</strong> a la base de datos si la instancia tiene un valor clave primaria. Antes, se hacía usaba <strong>SELECT</strong> para determinar si se necesitaba <strong>UPDATE</strong> o <strong>INSERT</strong>. El nuevo algoritmo necesita sólo de una consulta para actualizar una columna existente mientras que el anterior lo hacía con dos consultas. En casos muy raros esto no funciona (por ejemplo el trigger <strong>ON UPDATE</strong> de PostgreSQL) y para que esto funcione puede usar la bandera <strong>django.db.models.Options.select_on_save</strong> para forzar a guardar con el antigüo algoritmo.</li>
    <li><p>El ORM, además de permitir <strong>year</strong>, <strong>month</strong> y <strong>day</strong> en las consultas, ahora soporta <strong>hour</strong>, <strong>minute</strong> y <strong>second</strong>. Por ejemplo:</p>
    <pre class="sourceCode Python"><code class="sourceCode python">Event.objects.<span class="dt">filter</span>(timestamp__hour=<span class="dv">23</span>)</code></pre></li>
    <li>Django ahora se pliega (&quot;abriga&quot;) a todas las excepciones de PEP-249</li>
    <li>Por defecto, los widgets <strong>EmailField</strong>, <strong>URLFiel</strong>, <strong>IntegerField</strong> y <strong>DecimalField</strong>, usan los nuevos atributos <em>type</em> disponibles en HTML5 (<em>type=email</em>, <em>type=url</em>, <em>type=number</em> )</li>
    <li>El <strong>success_url</strong> of <strong>DeletionMixin</strong> se interpola ahora con el <strong>__dict__</strong> de este objeto.</li>
    <li><strong>HttpResponseRedirect</strong> y <strong>HttpResponsePermanentRedirect</strong> ahora proveen un atributo <strong>url</strong>.</li>
    <li>La versión de JQuery del admin se actualizó a la versión 1.9.1</li>
    <li><strong>Pillow</strong> pasa a ser la librería para la manipulación de imágenes preferida ya que <em>PIL</em> será deprecada. Para actualizar esto <strong>primero</strong> debe desinstalar PIL y <strong>luego</strong> instalar Pillow.</li>
    <li>Los argumentos <strong>choice</strong> de los campos del modelo, ahora aceptan un iterable de iterables en lugar de requerir un iterable de listas o tuplas.</li>
    <li>Las frases estándar HTTP (Por ej, &quot;404: Not Found&quot;: 404 es el código de estado HTTP, y &quot;Not Found&quot; es la frase estándar) puede ser personalizada en las respuestas HTTP mediante <strong>reason_phrase</strong></li>
    <li><strong>View</strong> y <strong>RedirectView</strong> ahora soportan el método HTTP <strong>PATCH</strong></li>
    <li><strong>GenericForeingKey</strong> ahora toma el argumento opcional <strong>for_concrete_model</strong>, el cual puede definirse como <strong>False</strong> para permitir al campo hacer referencia a un modelo proxy. Por defecto está definido como <strong>True</strong> para continuar con el antiguo comportamiento.</li>
    <li>La excepción <strong>DoesNotExist</strong> ahora incluye un mensaje que indica el nombre del atributo usado para la búsqueda.</li>
    <li>El método <strong>get_or_create()</strong> ya no requiere al menos un argumento como clave</li>
    <li>La lista que agrega campos relacionados a un <strong>QuerySet</strong> mediante <strong>select_related</strong> puede &quot;despejarse&quot; usando <strong>select_related(None)</strong></li>
    <li>Formsets ahora tiene un método <strong>total_error_count()</strong></li>
    </ul>
    <h2 id="cambios-con-incompatibilidad-hacia-atrás">Cambios con incompatibilidad hacia atrás</h2>
    <h3 id="nuevo-manejo-de-las-transacciones-del-modelo">Nuevo manejo de las transacciones del modelo</h3>
    <h4 id="cambios-en-el-funcionamiento">Cambios en el funcionamiento</h4>
    <p>El autocommit a nivel de base de datos está habilitado por defecto en Django 1.6. Esto no cambia el espíritu general del manejo de transacciones en Django pero hay incompatibilidades hacia atrás conocidas, las cuales se describen en la <a href="https://docs.djangoproject.com/en/1.6/topics/db/transactions/#transactions-upgrading-from-1-5">manejo de transacciones</a>. Se debe revisar el código hecho en versiones anteriores para determinar si está afectado o no.</p>
    <h4 id="savepoints-y-assertnumqueries">Savepoints<a href="#fn1" class="footnoteRef" id="fnref1"><sup>1</sup></a> y <strong>assertNumQueries</strong></h4>
    <p>Los cambios en el manejo de transacciones pueden resultar en declaraciones adicionales para <em>create</em>, <em>release</em>, o <em>rollback</em> los <em>savepoints</em>. Esto es más probable que suceda con SQLite, ya que no soportaba los <em>savepoints</em> hasta esta versión. Si las pruebas usando <strong>assertNumQueries()</strong> fallan debido a que el numero de consultas es mayor a las esperadas. verifique que las consultas extra están relacionadas con los <em>savepoints</em>, y ajuste en consecuencia el número esperado de consultas.</p>
    <h4 id="bolleanfield-ya-no-es-false-por-defecto"><strong>BolleanField</strong> ya no es <strong>False</strong> por defecto</h4>
    <p>Este campo ya no tiene un valor explícito por defecto, el valor implícito por defecto es <strong>None</strong>. En versiones anteriores en las que se usaba <strong>False</strong> por defecto, puede levantar una excepción cuando guarde nuevas intancias del modelo en la base de datos, porque <strong>None</strong> no es un valor aceptable para un <strong>BooleanField</strong>. Por ello, se debe especificar <strong>default=False</strong> en la definición del campo o garantizar que el campo se define como <strong>True</strong> o <strong>False</strong> antes de guardar el objeto.</p>
    <h4 id="quoting-en-reverse">Quoting en <strong>reverse()</strong></h4>
    <p>Al pasar URL's por reverse, las versiones anteriores de Django, no aplicaban <strong>urlquote</strong> a los argumentos antes de pasarlos a URL patterns. Este bug se corrige en Django 1.6. Si anteriormente se trabajo en función de corregir este bug aplicando comillas a las URL antes de pasar los argumentos a <strong>reverse()</strong>, esto puede resultar en <em>double-quoting</em>. Si este es el caso, simplemente hay que quitar las comillas del código. También se tendrán que reemplazar los caracteres especiales en <strong>assertRedirects()</strong> con sus versiones de encoding.</p>
    <h4 id="queryset-iteration"><a href="https://docs.djangoproject.com/en/1.6/releases/1.6/#queryset-iteration">QuerySet iteration</a></h4>
    <h4 id="boundfield.label_tag-ahora-incluye-el-label_suffix-de-los-formularios"><a href="https://docs.djangoproject.com/en/1.6/releases/1.6/#boundfield-label-tag-now-includes-the-form-s-label-suffix"><strong>BoundField.label_tag</strong> ahora incluye el <strong>label_suffix</strong> de los formularios</a></h4>
    <h4 id="cambios-en-el-orm"><a href="https://docs.djangoproject.com/en/1.6/releases/1.6/#object-relational-mapper-changes">Cambios en el ORM</a></h4>
    <p>Estos cambios pueden resultar en algunos problemas de incompatibilidad arrojando resultados difenerentes a los de Djando 1.5</p>
    <h3 id="misceláneas">Misceláneas</h3>
    <ul>
    <li><p>Las <a href="https://docs.djangoproject.com/en/1.6/topics/auth/default/#built-in-auth-views">Vistas de Autenticación</a> es ahora obtenida por nombre, no en su ubicación <strong>django.contrib.auth.views</strong>. Si anteriormente se estaban usando sin un <strong>name</strong>, deberá actualizarse el <strong>urlpatterns</strong> para usar <strong>url()</strong> con el parámetro <strong>name</strong>. Por ejemplo, lo que era:</p>
    <pre class="sourceCode Python"><code class="sourceCode python">(<span class="st">r&#39;^reset/done/$&#39;</span>, <span class="st">&#39;django.contrib.auth.views.password_reset_complete&#39;</span>)</code></pre>
    <p>pasa a ser</p>
    <pre class="sourceCode Python"><code class="sourceCode python">url(<span class="st">r&#39;^reset/done/$&#39;</span>, <span class="st">&#39;django.contrib.auth.views.password_reset_complete&#39;</span>, name=<span class="st">&#39;password_reset_complete&#39;</span>)</code></pre></li>
    </ul>
    <h2 id="características-deprecadas-en-1.6"><a href="https://docs.djangoproject.com/en/1.6/releases/1.6/#features-deprecated-in-1-6">Características Deprecadas en 1.6</a></h2>
    <div class="footnotes">
    <hr />
    <ol>
    <li id="fn1"><p>Más información sobre <a href="http://es.wikipedia.org/wiki/Savepoint">savepoints</a><a href="#fnref1">↩</a></p></li>
    </ol>
    </div>
    
    </div>
    
</div>

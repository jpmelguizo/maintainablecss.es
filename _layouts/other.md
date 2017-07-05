<!DOCTYPE HTML>
<html dir="ltr" lang="es">
	<head>
	    <title>{{ page.title }} - {{ site.name }}</title>
	    {% include head.html %}
	</head>
	<body>
		{% include header.html %}
		<main>
	        <div class="content">
				<h1>{{page.title }}</h1>
	           	{{ content }}
	        </div>
	    </main>
        {% include footer.html %}
	</body>
</html>

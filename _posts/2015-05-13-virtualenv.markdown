---
layout: post
title: "Virtualenv"
date: 2015-05-13 21:33:45
tags: dev python
---

Un petit mémo sur comment utiliser Virtualenv. Virtualenv permet de créer un environnement virtuel où on installe des libs python qui soient isolées du reste du système. On peut aussi utiliser une version de python spécifique.

Installer Virtualenv :
{% highlight console %}
pip install --user virtualenv
virtualenv /chemin/vers/projet/env_nom_du_projet
{% endhighlight %}

Pour rentrer dans l'environnement virtuel :
{% highlight console %}
source /chemin/vers/projet/env_nom_du_projet/bin/activate
{% endhighlight %}

Pour sortir de l'environnement virtuel :
{% highlight console %}
deactivate
{% endhighlight %}

Utiliser une version de python spécifique :
{% highlight console %}
virtualenv mon_env -p /usr/bin/python2.6
{% endhighlight %}

Isolation par rapport à l'OS :

* environnement vierge, n'hérite pas des libs du système
{% highlight console %}
virtualenv mon_env --no-site-packages
{% endhighlight %}
* libs du système disponibles dans l'environnement virtuel :
{% highlight console %}
virtualenv mon_env --system-site-packages
{% endhighlight %}

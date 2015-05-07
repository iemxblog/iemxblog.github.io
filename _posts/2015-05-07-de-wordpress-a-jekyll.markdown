---
layout: post
title: "De Wordpress à Jekyll"
date: 2015-05-07 15:05:00
categories: divers
---

J'avais commencé ce blog sur Wordpress, j'avais écris 2 articles (et commencé plein de brouillons). Et puis finalement l'amour de la ligne de commande m'a rattrapé et j'ai décidé d'utiliser [Jekyll](http://jekyllrb.com) et de mettre mon blog sur [Github Pages](https://pages.github.com). 

C'est quoi Jekyll ? C'est un générateur de site statique. On écrit ses posts dans des fichiers texte au format [Markdown](http://fr.wikipedia.org/wiki/Markdown), et Jekyll génère toutes les pages.

Pourquoi utiliser Jekyll ?
Parce que je préfère la ligne de commande qu'un clicodrome, je peux versionner le tout avec git, je peux utiliser Vim pour rédiger les articles, etc.

Enfin, on peut mettre en valeur facilement des bouts de code. Exemple :

{% highlight python %}
print "Hello, world!"
{% endhighlight %}

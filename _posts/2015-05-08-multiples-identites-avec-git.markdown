---
layout: post
title: "Utiliser plusieurs identités avec Git"
date: 2015-05-08 12:36:00
---

Voici le problème que j'ai rencontré. J'ai 2 adresse mail, une perso et l'autre pour le blog, en l'occurence [iemxblog@gmail.com](mailto:iemxblog@gmail.com). 

Quand j'ai configuré git (il y a plusieurs années...), j'ai donc fait ceci :

{% highlight console %}
$ git config --global user.name "Prénom NOM"
$ git config --global user.email adresseperso@provider.com
{% endhighlight %}

Or j'ai créé un compte github en lien avec ce blog, et je voudrais pouvoir utiliser parfois mon "identité" perso pour certains dépôts git, et parfois mon identité "iemxblog" pour d'autres dépôts.

Il se trouve que c'est très simple, il suffit d'enregistrer son nom et email en local dans le dépôt, tout simplement en utilisant les mêmes commandes mais sans le *--global* :

{% highlight console %}
$ git config user.name "iemxblog"
$ git config user.email iemxblog@gmail.com
{% endhighlight %}

Et cette config locale est sauvegardée dans *.git/config*. Voici celui du dépôt git de mon blog :
{% highlight ini %}
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
[remote "origin"]
	url = https://github.com/iemxblog/iemxblog.github.io
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
[user]
	name = iemxblog
	email = iemxblog@gmail.com
{% endhighlight %}

Donc pour résumer, si git trouve une identité locale dans le dépôt, les commits seront créés sous cette identité. Sinon, s'il ne trouve rien, il utilisera l'identité "globale", sauvegardée dans *~/.gitconfig*.

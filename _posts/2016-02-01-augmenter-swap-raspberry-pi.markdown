---
layout: post
title: "Augmenter la taille de la swap sur un Raspberry Pi"
date: 2016-02-01 16:00:00
thumbnail: /assets/2016-02-01-augmenter-swap-raspberry-pi/thumbnail.jpg
tags: raspberrypi linux
---

Je suis en train d'essayer de compiler sur mon Raspberry Pi un projet en Haskell sur lequel je travaille, afin de voir s'il fonctionne sur une architecture ARM. Malheureusement la compilation des dépendances a échoué, et je soupçonne le fait que je n'avais pas assez de mémoire d'être la cause de cet échec. Je vais donc augmenter la taille de la swap avant de retester la compilation. J'en profite donc pour faire une petite synthèse de la méthode à utiliser.

J'ai décidé, pour des raisons de simplicité, d'utiliser comme swap un fichier sur un disque dur externe que je vais brancher au respberry pi. Je n'ai pas envie de créer une partition spécialement pour ça.

Je branche donc mon disque dur, je monte son unique partition.

{% highlight console %}
$ sudo mkdir /mnt/sda1
$ sudo mount /dev/sda1 /mnt/sda1
{% endhighlight %}

Je crée un fichier de 2Go de la façon suivante :

{% highlight console %}
$ dd if=/dev/zero of=/mnt/sda1/swap.file bs=1M count=2048
$ sudo mkswap /mnt/sda1/swap.file
{% endhighlight %}

J'édite le fichier de config de dphys-swapfile :
{% highlight console %}
$ sudo vim /etc/phys-swapfile
{% endhighlight %}

Contenu initial du fichier :
{% highlight cfg %}
CONF_SWAPSIZE=100
{% endhighlight %}

Je l'ai remplacé par ceci, pour obtenir 2Go de swap.
{% highlight cfg %}
CONF_SWAPFILE=/mnt/sda1/swap.file
CONF_SWAPSIZE=2048
{% endhighlight %}

Et ensuite j'exécute cette commande, pour swapper sur le nouveau fichier :
{% highlight console %}
$ sudo dphys-swapfile swapon
{% endhighlight %}

On vérifie que l'on obtient bien ce qu'il faut :
{% highlight console %}
$ cat /proc/meminfo | grep SwapTotal
SwapTotal:  2199544 kb
{% endhighlight %}


Finalement, la mémoire n'était pas la cause de mon problème. C'est template-haskell qui est en cause, car la version actuelle de ghc pour processeur ARM fournie par Debian testing ne le supporte pas complètement. Vu que ce n'est pas urgent, je vais attendre tranquillement que la nouvelle version arrive.

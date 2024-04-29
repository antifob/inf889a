# INF889A - Analyse de programmes pour la sécurité logicielle

Les _slides_ des présentations faites dans le cadre du cours
INF889A, Analyse de programmes pour la sécurité logicielle, à
l'université du Québec à Montréal (UQAM), à la session d'hiver
2024 (https://web.archive.org/web/20240429002708/https://inf889a.uqam.ca/)


## Présentation 1 - Un article

La présentation d'un article au choix. Le sujet:

```
Simple and Efficient Construction of Static Single Assignment Form
Braun, Buchwald, Hack, Leissa, Mallon, and Zwinkau
2013

https://link.springer.com/chapter/10.1007/978-3-642-37051-9_6
```

- Présente différentes formes de RIs et leur forme.
- Compare minimalement des RIs afin de souligner les différences et leurs impacts potentiels.
- Présente l'algorithme de l'article de manière progressive.


## Présentation 2 - Un outil

La présentation d'un outil au choix. Le sujet:

`GadgetInspector`, par Ian Haken, disponible à https://github.com/jackofmosttrades/gadgetinspector
La présentation contient:

- Une brève mise en contexte relative aux vulnérabilités de désérialisation Java.
- Une brève description des différentes passes d'analyse effectuées
  pour parvenir à détecter les chaines de gadgets.
- La présentation de divers limitations dans l'implémentation de l'outil.
  Ces limitations empêchent de détecter certaines chaines et démontrent
  la contradiction entre certains composants du programme.


## Présentation 3 - Un projet

La présentation d'un projet au choix.

Le projet visait à modifier l'outil `GadgetInspector` pour améliorer la
détection de chaines. Les modifications suivantes ont été effectuées:

- L'ajout d'une source de teinte, `java/io/ObjectInputStream.readUTF()Ljava/lang/String;`.
  Il s'agit d'une simple omission par l'auteur. On démontre l'ajout
  avec le puit `Runtime.exec(String)`.
- L'ajout d'une source de teinte, `java/io/ObjectInputStream.read()I`.
  Il s'agit d'un teinte sur un type primitif, qui n'est pas supporté
  par l'outil puisqu'il supporte uniquement le teintage d'objets.
  On démontre le support avec le puit `System.exit(int)`.
- L'ajout d'une source de désérialisation, `java/io/ObjectStream.readExternal()V`.
  Cette méthode moins commune de source de désérialisation fait partie de
  l'interface `java/io/Externalizable`, une spécialisation de `java/io/Serializable`.
- L'ajout d'un puit d'exploitation, `java/net/InetAddress.getHostByName(Ljava/lang/String;)Ljava/net/InetAddress;`.
  Il s'agit de la composante principale du _payload_ `URLDNS`.

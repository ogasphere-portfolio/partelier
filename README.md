# Parcours de la saison 8 :star2:

C'est la dernière saison du socle PHP, et donc, le dernier challenge :sob:

Je sais... c'est pas facile... :cry:  

Bon, il va bien falloir avancer malgré tout... :rocket:

Comme d'habitude, le parcours va porter sur une ou plusieurs des notions vues au cours de cette saison dédiée à la découverte de Wordpress.

## Sujet

En saison 4, nous avons mis en place _oBlog_.  
C'est un blog pour les étudiants O'clock, pour qu'ils puissent y écrire leurs ressentis.

**Problème** !  
Nous n'avions mis en place que la partie visible du site. Il n'y avait rien pour l'administrer et pouvoir ajouter facilement des catégories, des pages, etc.

**Solution** ?  
Wordpress, bien entendu :nerd_face:

## Etapes

- L'intégration HTML/CSS de _oBlog_ est fournie dans le répertoire `inte-html-css`
- Les pages `article.html` et `category.html` sont des exemples, des gabarits pour 1 article ou 1 catégorie
- Dans ce dépôt, on va installer Wordpress et mettre en place le thème pour cette intégration

### #1 - On s'installe :pizza:

#### Installer Wordpress en ligne de commande :
<details>
    <summary>Pas à pas</summary>

Vous pouvez suivre la fiche récap : https://kourou.oclock.io/ressources/fiche-recap/wordpress-installation-classique/

N'oubliez pas :
- de créer une base de données dédiée avant l'installation
- la manip à faire en ligne de commande pour faire fonctionner correctement les droits.

**Quelques précisions sur la section _Récupérer Wordpress_ :**
- Il faut d'abord récupérer les fichiers de wordpress et les placer sur notre serveur web. On se rend sur [la section "get Wordpress"](https://wordpress.org/download/) du site wordpress.org. On fait un clic droit sur le lien _Download .tar.gz_ puis "Copier l'adresse du lien"
- Dans un terminal, on se rend dans le répertoire qui va contenir notre projet. :warning: On ne crée pas un dossier qui représente la racine de notre projet, celui-ci sera créé pendant la décompression. On se rend plutôt dans son répertoire parent.
- Télécharger l'archive dans le répertoire courant : `wget [url copiée depuis le site de WP]` => généralement `wget https://wordpress.org/latest.tar.gz`
- On peut faire un `ls` pour vérifier que le fichier **latest.tar.gz** a bien été téléchargé dans le répertoire courant.
- On peut décompresser l'archive ! Utiliser la commande `tar -zxvf latest.tar.gz` dans le répertoire courant. On y retrouve dorénavant un dossier **wordpress**. Ce dossier est la racine de notre projet :muscle:
- On renomme le dossier en `S08-oBlog-wp` par exemple : `mv wordpress S08-oBlog-wp`
- On accède au site dans le navigateur pour lancer l'installation, et :tada:
</details>

#### Créer le thème
- Découper et placer le code HTML dans le(s) template(s) du thème. On pourra utiliser le même template pour les pages et les articles :+1:

:bulb: rappel :
- le thème est le répertoire à l'intérieur de `wp_content/themes` dans lequel vous placerez vos fichiers
- les templates sont les fichiers de votre thème

Vous pouvez vous aider des fiches récap pour mettre en place votre thème : 
- https://kourou.oclock.io/ressources/fiche-recap/theme-structure/
- https://kourou.oclock.io/ressources/fiche-recap/themes-templates/

### #2 - On remplit :beer:

- Ajouter le contenu du site dans l'admin Wordpress. Ça tombe bien, dans Wordpress on retrouve des articles et des catégories !
- Les auteurs sont en fait des utilisateurs du backoffice :bulb: Lorsque vous créez un article, n'oubliez pas de sélectionner le bon auteur (il faut donc les avoir créés au préalable ;))
- Vous trouverez tous les contenus à créer dans l'intégration fournie :muscle:

### #3 - On dynamise :fireworks:

- Afficher dynamiquement la page d'accueil en utilisant les contenus ajoutés dans l'étape précédente
- Modifier les liens "en dur" pour qu'ils pointent vers la bonne URL dynamiquement
- Faire en sorte que les menus suivants soient gérés dynamiquement via Wordpress :
    - navigation en haut
    - catégories dans la sidebar
    - liens en bas de page

<details>
    <summary>Aide pour la gestion des contenus</summary>
    
On utilise une boucle spécifique à Wordpress pour manipuler et afficher les contenus : `the_loop()` :muscle:

Plus de détails : https://kourou.oclock.io/ressources/fiche-recap/the-loop/  
N'hésitez pas à faire un tour sur la documentation également : https://codex.wordpress.org/The_Loop
</details>

<details>
    <summary>Aide pour la gestion des menus</summary>
    
Pour générer dans les templates les menus définis côté backoffice, on peut utiliser `wp_nav_menu()`. Il faut fournir quelques données dans le tableau qu'on passe en paramètre. Vous devrez vous appuyer sur la doc et les fiches récap pour l'utilisation des menus dans le thème :  

- d'abord ici : https://kourou.oclock.io/ressources/fiche-recap/setup-dun-theme/#menus-de-navigation
- çà : https://developer.wordpress.org/reference/functions/wp_nav_menu/
- et là : https://codex.wordpress.org/Navigation_Menus
</details>

### #4 - On vérifie :see_no_evil:

- naviguer sur le site et s'assurer que chaque lien est correctement configuré

## Un petit bonus !

Si vous vous ennuyez (:thinking:), voici une petite évolution intéressante à faire :
vous vous souvenez probablement de DRY, cette fabuleuse bonne pratique qui nous empêche de répéter le code qui pourrait être factorisé ? Don't Repeat Yourself !

Wordpress permet de mettre en oeuvre cette bonne pratique grâce aux _template parts_, qui, comme le nom semble l'indiquer, nous offrent la possibilité de créer des morceaux de templates que l'on pourra réutiliser çà et là dans nos templates principaux.

<details>
    <summary>Guide</summary>

On pourrait prévoir un template part pour la liste des auteurs :
- repérer le code HTML à extraire
- créer un répertoire _**template-parts**_ 
- dans ce dernier, on ajoute fichier _**sidebar-authors.php**_ 
- placer le code HTML à factoriser à l'intérieur de ce fichier
- dans le template d'une page dans laquelle on veut afficher cette liste d'auteurs (par exemple dans _**archive.php**_), on inclut le _template part_ avec `get_template_part('template-parts/sidebar', 'authors')`
Notez que les noms de fichiers et de répertoires sont des exemples et sont nommés librement.
</details>  

Vous pourrez trouver plus d'infos dans la fiche récap correspondante : https://kourou.oclock.io/ressources/fiche-recap/themes-templates/#fragments-de-templates  
Et aussi, _RTFM_ :smirk: : 
- https://developer.wordpress.org/reference/functions/get_header/
- https://developer.wordpress.org/reference/functions/get_footer/
- https://developer.wordpress.org/reference/functions/get_sidebar/
- https://developer.wordpress.org/reference/functions/get_template_part

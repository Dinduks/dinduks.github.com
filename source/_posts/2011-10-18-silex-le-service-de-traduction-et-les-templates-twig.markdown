---
comments: true
date: 2011-10-18 22:12:43
layout: post
slug: silex-le-service-de-traduction-et-les-templates-twig
title: 'Silex: Le service de traduction et les templates Twig'
categories:
- Development
- Symfony 2
- Tutorials
tags:
- php
- silex
- twig
---

[*Silex*](http://silex.sensiolabs.org/) est un micro-framework basé sur les composants de Symfony 2 grâce auquel je suis entrain de développer une sorte de [vCard ou page d'accueil](https://github.com/Dinduks/ChaoticCard) (faute de meilleur terme).

Parmi ses nombreuses fonctionnalités: La traduction. Bien qu'elle soit très facile à implémenter, la méthode n'est décrite nulle part sur la doc.  
Heureusement, sinon je n'aurais rien à poster sur ce blog.

Trêve de plaisanteries, voici sans attendre comment implémenter la traduction avec Silex.

### Déclarer les traductions
Dans un répertoire _src/locales/_ créez autant de fichiers _yml_ que de langues désirées.

#### Exemple de fichiers:
*en.yml*:

      hello:      Hello
      about_me:   About me
      contact_me: Contact me

*fr.yml*:

    hello:      Bonjour
    about_me:   A propos de moi
    contact_me: Contactez-moi

### Déclarer le service *TranslationServiceProvider* dans votre _app.php_

    $app->register(new Silex\Provider\TranslationServiceProvider(), array(
        'locale'                    => LiveGeekUtil::getClientLanguage(),
        'locale_fallback'           => 'en',
        'translation.class_path'    => __DIR__.'/vendor/Symfony/Component',
    ));

`locale` indique la langue utilisée.  
`locale_fallback` indique la langue utilisée si notre application ne supporte pas la langue donnée dans locale.

Notez que j'ai utilisé une méthode statique pour récupérer la langue du navigateur du visiteur. La voici:

    public static function getClientLanguage() {
        $langs = explode(',', $_SERVER['HTTP_ACCEPT_LANGUAGE']);
        return substr($langs[0], 0, 2);
    }

### Indiquer à l'application où se trouvent vos fichiers de langue:

    $app['translator.messages'] = array(
        'fr' => __DIR__.'/../src/locales/fr.yml',
        'en' => __DIR__.'/../src/locales/en.yml'
    );

### Charger le composant qui lit les fichiers *yml*
PHP ne comprennant pas les fichiers *YAML*, on utilise le composant *YAML* de Symfony;

    $app['autoloader']->registerNamespace('Symfony', __DIR__.'/../vendor/Symfony/src');
    $app['translator.loader'] = new Symfony\Component\Translation\Loader\YamlFileLoader();

### Déclarer `SymfonyBridgesServiceProvider`
Ce service fait la liaison entre la traduction et les templates *Twig*.

    $app->register(new Silex\Provider\SymfonyBridgesServiceProvider(), array(
        'symfony_bridges.class_path' => __DIR__.'/vendor/Symfony/Component',
    ));

Et voilà.

A partir de maintenant, affichez le texte dans vos templates grâce aux balises *Twig* `{% trans %}`, ceux-ci seront automatiquement traduits dans la langue du navigateur de votre utilisateur, du moment qu'elle soit supportée.

    {% trans %}contact_me{% endtrans %}

### Liens utiles:

  * La documentation de Silex: [http://silex.sensiolabs.org/documentation](http://silex.sensiolabs.org/documentation).

Bon courage et amusez-vous bien avec Silex! :)

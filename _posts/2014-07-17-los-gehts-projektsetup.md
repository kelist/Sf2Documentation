---
layout: pages
title: Los geht's - Projektsetup
---

# Los geht's - Projektsetup

##Installation via Composer:

{% highlight console %}
$ php composer.phar create-project symfony/framework-standard-edition PfadZumProjekt/ "2.5.*"
{% endhighlight %}

##Bundle erstellen

Aufbau: Namespacename/BundlenameBundle

{% highlight console %}
$ php app/console generate:bundle --namespace=Namespacename/BundlenameBundle
{% endhighlight %}

## Route erstellen

Dieser Eintrag zeigt der App wo die Routendatei des Bundles liegt.
Hier werden dann die Routeninformationen für das Bundle hinterlegt (Namespacename/Bundlename/Resources/config/routing.php).
Die Route verweist auf den entsprechenden Controller nach dem Schema: NamespacenameBundlenameBundle:%Controllername%:%routenname%
In geschweiften Klammern werden evtl. vorhandene Variablen der Route übergeben (hier: {name}).

{% highlight php %}
$collection->add('namespacename_bundlename_homepage', new Route('/hello/{name}', array(
    '_controller' => 'NamespacenameBundlenameBundle:Default:index',
)));
{% endhighlight %}

##Controller erstellen

Der Controller wird unter Namespace/Bundlename/Controller/%Controllername%Controller.php angelegt.
Er mappt die Route entsprechend dem in den Routeninformationen angegebenen Schema: %routenname%Action
Standardmäßig wird der entsprechende View zurückgegeben, hier mit der aus der Route übergebenen Variable "name".

{% highlight php %}
public function indexAction($name)
{
    return $this->render('BikerentCoreBundle:Default:index.html.twig', array('name' => $name));
}
{% endhighlight %}

##View anpassen

Der View liegt unter Namespacename/Bundlename/Resources/config/views/%Controllername%/%routenname%.html.twig.
Aus dem Controller übergebene Variablen werden über doppelt-geschweifte Klammern im View ausgegenem (hier: "name").

{% highlight smarty %}
Hello {{ name }}
{% endhighlight %}

##Testing

###Unit Testing

Die Test Cases für dir Unittests liegen im Regelfall in Namespacename/Bundlename/Tests/%Meinverzeichnis%/%Klassenname%Test.php.

###Functional Testing

Die Test Cases für dir Funktionstests liegen im Regelfall in Namespacename/Bundlename/Tests/Controler/%Controllername%ControllerTest.php.

###Tests durchführen

Für einen Gesamttest genügt folgenden Aufruf:

{% highlight console %}
phpunit -c app/
{% endhighlight %}

Um z.B. oben genannten Controller allein zu testen wird der Pfad an den Aufruf angehängt:

{% highlight console %}
phpunit -c app/ src/Namespacename/Bundlename/Tests/Controller/%Controllername%ControllerTest.php.
{% endhighlight %}
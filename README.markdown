# Test de communication mobile/webview

Ce projet permet de voir s'il est possible, peu importe la plateforme, de communiquer facilement entre le code source mobile et le code javascript d'une WebView. Il permet aussi de voir l'utilisation du localStorage (*stockage de données au sein de la webview*).

L'exemple courant va permettre aux mobiles d'envoyer une valeur dans la variable `test` et de voir s'ils peuvent aussi la récupérer.

## Script à lancer au démarrage

Selon les plateformes, il est possible d'exécuter des scripts au démarrage. Pour ce fichier d'exemple, le script à exécuter est vraiment simple :

```
localStorage.setItem('test', 'valeurdetest');
localStorage.setItem('platform' 'valeur'); // La valeur est à remplacer par android, ios ou windows
```

## Réglages de base :

- Activer l'exécution du javascript sur la webview
- Activer l'utilisation du localStorage (sur endroit `webview.setDomStorageEnabled(true)`
- Lancer la page index.html présente ici

## URL à capturer

Selon les plateformes, la méthode de capture n'est pas la même. L'url à capturer est de la forme suivante :

```
acs://weviewcallback?test=valeurdetest
```

### Android

Pour Android, nous utilisons un objet passé à la webview à l'aide de la méthode `addJavascriptInterface`. L'objet devra s'appeler `androidProxyObject` et devra avoir la méthode `captureUrl(String url)`.

```
 class JsObject {
    @JavascriptInterface
    public void captureUrl(String url) {
        // affichage de la valeur test dans un toast
    }
 }

webView.addJavascriptInterface(new JsObject(), "androidProxyObject");
```

### IOS

Vous devez intercepter l'url notée plus haut.

### Windows Phone

Pour windows Phone, nous passons par la méthode `ScriptNotify` et nous passeront en paramètre l'url notée plus haut. Vous devrez afficher le résultat obtenu.

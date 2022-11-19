# DAKboard

![](castDeck.jpg)

Application chromecast de diaporama générique basée sur `iframe`. Traits:

- Ajustement du facteur d'échelle
- Ajustement du rapport d'aspect
- Ajustement de surbalayage
- Ajustement de la rotation
- Transitions entre plusieurs URL

## Utilisation

- Allez sur [l'url de contrôle](https://nlcamarillo.github.io/castDeck)
- Ajuster les paramètres
- Appuyez sur "diffuser"

## Utilisation du récepteur seul

L'application de gestion n'est qu'un exemple. Vous pouvez également utiliser l'application récepteur dans votre propre produit. En général, le fonctionnement est le suivant :

- créer une page Web, n'importe où. Celui-ci contient le contenu que vous souhaitez afficher.
- créer une application d'envoi, qui charge castDeck sur votre chromecast, dont la page Web de contenu.
- contrôlez castDeck depuis votre propre application. L'API est décrite ci-dessous.

##API

Pour créer votre propre application autour de castDeck :

- inclure l'API Google Cast : `www.gstatic.com/cv/js/sender/v1/cast_sender.js`
- inclure le `senderApplication.js`

CastDeck est disponible en tant que singleton global "castDeck"

## options

définissez `castDeck.options.log = true;` après avoir inclus `senderApplication.js` pour activer la journalisation pour le débogage

## méthodes

### castDeck.cast(url ? || url[]?)

commencer à diffuser avec l'URL donnée. L'URL peut être une chaîne unique ou un tableau

### castDeck.stop()

arrêter de diffuser

### castDeck.setZoom(valeur), castDeck.zoomIn(), castDeck.zoomOut(), castDeck.zoomReset()

ajuster le zoom

### castDeck.rotateCCW(), castDeck.rotateCW()

tourner dans le sens antihoraire (CCW) ou dans le sens horaire (CW)

### castDeck.adjustTop(px), castDeck.adjustRight(px), castDeck.adjustBottom(px), castDeck.adjustLeft(px)

régler les paramètres de surbalayage. Certains moniteurs (téléviseurs en particulier) coupent certains des côtés de la fenêtre. Vous pouvez ajuster les paramètres de surbalayage pour atténuer cela.

### castDeck.updateAspect(value | 'native')

passez la chaîne `native` ou une valeur numérique pour ajuster le format d'image. Certains moniteurs déforment le rapport d'aspect HD (qui est de 16:9) pour s'adapter au rapport de l'appareil. Transmettez le format d'image réel de l'appareil pour corriger cette distorsion.

### castDeck.updateTransition(valeur)

définir le type de transition, actuellement seul "fondu" est pris en charge

### castDeck.updateDuration(valeur)

définir la durée d'affichage entre les transitions, par défaut à 10 secondes.

## Remarques

- L'identifiant de l'API castDeck est `4EC978AD`
- Une fois démarré, le message json suivant peut être envoyé à l'espace de noms `urn:x-cast:org.firstlegoleague.castDeck`

          {
              "url":"<url à charger>",
              "rotation": <rotation en degrés>,
              "zoom": <niveau de zoom>,
              "aspect": <"natif"|ratio>,
              "overscan": [<haut>,<droite>,<bas>,<gauche>],
              "transition": "fondu",
              "durée": <secondes>
          }

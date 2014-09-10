MFP Accessible Video Player
=======

The MFP Video Player is a project leading by the Multimedia France Production Ltd (a subsidiary of the French group France Télévisions) that conceived the player, in collaboration with Access42 Ltd that leaded the developments. 

The accessibility has been checked by the French Association BrailleNet that delivered the AccessiWeb Label testifying the MFP Video Player code is compliant with the Web Content Accessibility Guidelines (WCAG 2) at level double A (AA), and thus usable by any user regerdless one's abilities.

The MFP Video Player project is a fork of [videojs](http://www.videojs.com/) to make it accessible and add some options useful for captionning and audiodescription. The code of videojs was originally modified without Git, and a lot of new specific options have been added. That's why it was impossible to contribute to the great work of Steve Heffernan (@heff) on videojs, but it's not an unfriendly fork, just a different work.

The initial project (videojs) was under an Apache2 license, and the new project embed the JS Mootools library under the MIT license. Both licenses are compatible with the GPL 3 license, which is the license of the MFP video Player. See the [FSF page about licenses compatibilities with the GPL](https://www.gnu.org/licenses/license-list.html#GPLCompatibleLicenses) for more info.


How to use the MFP Accessible Video Player ([French version bellow](#french-version))
----

### How to embed the player


The HTML code of the player just use the `<div>` element with an `id` "player" ; below a sample:

	<div id="player">
		<video id="video" controls="controls" height="480" width="640">
			<source src="client/medias/tontons_flingueurs_vo.mp4" type="video/mp4" />
			<source src="client/medias/tontons_flingueurs_vo.webm" type="video/webm" />
			<source src="client/medias/tontons_flingueurs_vo.ogv" type="video/ogg" />
			<track kind="captions" label="Français" src="client/captions/fr.srt" srclang="fr" data-transcription="server/transcriptions/fr.txt" />
		</video>
		<audio src="client/medias/tontons_flingueurs_ad.mp3" preload="auto" hidden="hidden"></audio>
	</div>


Copy-paste this code where you want the player to be display on the page. 

Then, in the head element (between the tags `<head>` and `</head>`) of the document, you have to call external resources:

	<!-- VideoJS -->
	<link rel="stylesheet" href="client/scripts/video-js/video-js.css" type="text/css" />
	<!-- Personnalisation -->
	<link rel="stylesheet" href="client/styles/styles.css" type="text/css" />
	<!-- Internationalisation, images de l'interface et couleurs (paramètres des sous-titres) -->
	<script src="client/scripts/settings.js" type="text/javascript"></script>
	<!-- Framework Mootools -->
	<script src="client/scripts/mootools-core-1.4.5-full-nocompat-yc.js" type="text/javascript"></script>
	<script src="client/scripts/mootools-more-1.4.0.1.js" type="text/javascript"></script>
	<!-- VideoJS (remaniée : audiodescription et panneau des paramètres des sous-titres + mise en accessibilité) -->
	<script src="client/scripts/video-js/video.dev.js" type="text/javascript"></script>
	<!-- Fonctions liées aux paramètres des sous-titres -->
	<script src="client/scripts/subtitles.js" type="text/javascript"></script>
	<!-- Utilisation de VideoJS -->
	<script type="text/javascript">
		window.addEventListener('DOMContentLoaded', function(event) {
			videojs(video.getAttribute('id'), { preload: 'auto' }, function () {
				this.addClass('video-js');
				this.addClass('vjs-default-skin');
			});
		}, false);
	</script>

Note: you may have to change the path of the resources (`src` in `script` elements and `href` of the `link` elements) according of their actual location.


### Enable Closed Caption

In the video element (betweeen the tags `<video>` and `</video>`), in each closed captioning file you must add the following line of code:

	<track kind="captions" label="" src="" srclang="" data-transcription="" />

And complete the code following the rules described bellow:
- `label` allows you to give a title to the closed captioning file: this title will appear in the dropdowmn list of the closed caption panel;
- `src` allow you to indicate where the closed captioning file is located;
- `srclang` allows you to indicate the lang of the closed caption or subtitles;
- `data-transcription` allows you to indicate where the transcript file is located (to be downloaded), if there is one.

Example for a closed captioning file in French intitled "Français", with a transcript file to be download:
	
	<track kind="captions" label="Français" src="client/captions/fr.srt"
		 srclang="fr" data-transcription="server/transcriptions/fr.txt" />

Notes:
- if there isn't any closed captions, you musn't add any line `<track ... />` : the button ST will not then be present;
- if there isn't any transcript file (to be downloaded), `data-transcription` musn't be used: the link "Download the transcript" will not appear.


### Enable Audio Description

Just after the `video` element (tag `</video>`), add the following line of code:

	<audio src="" preload="auto" hidden="hidden"></audio>

And complete the code following the rule bellow:
- `src` allows you to indicate where the Audio Description file is located.

Note :
- if there isn't any Audio Description, do not add this line of code: the AD button will not appear.



<a name="french-version"></a>Comment utiliser le lecteur vidéo accessible MFP
----

### Intégration du lecteur


Le code HTML du lecteur est limité à l'élément `<div>` avec un `id` "player"; ci-dessous un code "type" :

	<div id="player">
		<video id="video" controls="controls" height="480" width="640">
			<source src="client/medias/tontons_flingueurs_vo.mp4" type="video/mp4" />
			<source src="client/medias/tontons_flingueurs_vo.webm" type="video/webm" />
			<source src="client/medias/tontons_flingueurs_vo.ogv" type="video/ogg" />
			<track kind="captions" label="Français" src="client/captions/fr.srt" srclang="fr" data-transcription="server/transcriptions/fr.txt" />
		</video>
		<audio src="client/medias/tontons_flingueurs_ad.mp3" preload="auto" hidden="hidden"></audio>
	</div>

Placez ce code à l'endroit souhaité dans la page où le lecteur doit être intégré.

Enfin, dans l'élément `head` (entre les balises `<head>` et `</head>`) de la page, un appel à des ressources externes est requis :

	<!-- VideoJS -->
	<link rel="stylesheet" href="client/scripts/video-js/video-js.css" type="text/css" />
	<!-- Personnalisation -->
	<link rel="stylesheet" href="client/styles/styles.css" type="text/css" />
	<!-- Internationalisation, images de l'interface et couleurs (paramètres des sous-titres) -->
	<script src="client/scripts/settings.js" type="text/javascript"></script>
	<!-- Framework Mootools -->
	<script src="client/scripts/mootools-core-1.4.5-full-nocompat-yc.js" type="text/javascript"></script>
	<script src="client/scripts/mootools-more-1.4.0.1.js" type="text/javascript"></script>
	<!-- VideoJS (remaniée : audiodescription et panneau des paramètres des sous-titres + mise en accessibilité) -->
	<script src="client/scripts/video-js/video.dev.js" type="text/javascript"></script>
	<!-- Fonctions liées aux paramètres des sous-titres -->
	<script src="client/scripts/subtitles.js" type="text/javascript"></script>
	<!-- Utilisation de VideoJS -->
	<script type="text/javascript">
		window.addEventListener('DOMContentLoaded', function(event) {
			videojs(video.getAttribute('id'), { preload: 'auto' }, function () {
				this.addClass('video-js');
				this.addClass('vjs-default-skin');
			});
		}, false);
	</script>

Note : selon l'emplacement de ces ressources externes, les chemins (`src` des éléments `script` et `href` des éléments `link`) peuvent être changés. 


### Mise en place des sous-titres

Dans l'élément `video` (entre les balises `<video>` et `</video>`), ajoutez pour chaque fichier de sous-titres la ligne de code suivante :

	<track kind="captions" label="" src="" srclang="" data-transcription="" />

Et complétez le code en suivant les règles suivantes :
- `label` permet de donner un intitulé au fichier de sous-titres : cet intitulé sera repris dans la liste déroulante du panneau des sous-titres ;
- `src` permet d'indiquer où se trouve le fichier de sous-titres ;
- `srclang` permet d'indiquer la langue des sous-titres ;
- `data-transcription` permet d'indiquer où se trouve un éventuel fichier de transcript (à télécharger).

Exemple pour un fichier de sous-titres en français intitulé "Français" accompagné d'un transcript :
	
	<track kind="captions" label="Français" src="client/captions/fr.srt"
		 srclang="fr" data-transcription="server/transcriptions/fr.txt" />

Notes :
- en l'absence de sous-titres, aucune ligne `<track ... />` ne doit être ajoutée : le bouton ST sera alors absent.
- en l'absence de transcript (à télécharger), `data-transcription` ne doit pas être renseigné : le lien "Télécharger le transcript" ne sera alors pas proposé.


### Mise en place de l'audiodescription

Directement après l'élément `video` (balise `</video>`), ajoutez la ligne de code suivante :

	<audio src="" preload="auto" hidden="hidden"></audio>

Et complétez le code en suivant la règle suivante :
- `src` permet d'indiquer où se trouve le fichier de l'audiodescription.

Note :
- en l'absence d'audiodescription, n'ajoutez pas cette ligne de code : le bouton AD sera alors absent.

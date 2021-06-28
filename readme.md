# L'ECF JS de Bertrand Bouland

Bienvenue sur mon ECF JavaScript ! Ici, vous (enfin, surtout toi Antho) allez découvrir le fruit de ma sueur, de mon sang, de mes larmes.
A vrai dire, j'ai pas grand chose à raconter ici, vu tous les commentaires que j'ai mis partout dans les fichiers... Juste deux trois choses ...

## Quelques mots sur la structure

Vous remarquerez que j'ai tenté de strucuter mon projet en utilisant la glorieuse architecture MVC. J'étais pas parti comme ça au début (cf le controller.js) mais j'ai décidé de m'y mettre à partir de l'affichage des détails car j'étais plus confiant, suivant des petits tutos et lisant de la doc par ci par là. Malheureusement, j'ai avancé et au moment où je me suis dit _Tiens, et si je retouchais tout ce qui gère mes résultats et que j'ai fait au début ?_ c'était presque trop tard et j'ai un peu peur maintenant de tout casser si j'essaye de refaire toute cette partie sur le même schéma.

## POURQUOI LE `INNERHTML` ET `INSERTADJACENTHTML` BERTRAND ? POURQUOI ?

Parce que pour moi, comme je n'utilisais jamais l'input de l'utilisateur pour l'intégrer dans le DOM, je me suis dit que ce ne serait pas problématique : Musicbrainz fait sans doute du parsing et refuse à la soumission les pistes / artistes / releases etc ... qui contiennent des balises HTML, ou traite ces dernières pour échapper les caractères. En plus de ça, étant donné que j'ai voulu tester Tailwind, c'est quand même beaucoup plus simple d'utiliser du markup HTML que de s'embêter à ajouter des classList à ralonge et de créer le dom petit à petit (d'ailleurs, on est en plein React présentement, et je me rends compte qu'en fait, ce que j'ai fait, c'est une sorte de "proto-react" mélangeant du HTML et du JS via le state à l'aide des templates litterals ...).
Et puis un jour, notre très cher formateur (oui, toi Anthony !) nous a fait comprendre que c'était pas bien de supposer que Musicbrainz ferait bien son boulot, alors que j'avais déjà fait les 99/100ème de mon ECF (en gros, il me restait juste à commenter une partie de mon code ...). Un super hacker pourrait tout casser sur Musicbrainz et faire passer des trucs et des machins en HTML et donc que j'étais cuit telle une merguez un dimanche de méchoui avec mes `innerHTML` à la noix de pécan.

## SOLUTION : une fonction d'échappement

A défaut de tout reprendre à zéro pour mettre du `textContent` partout, j'me suis dit : _Ok Bertrand, est-ce que y'a pas un truc qui limiterait les dégâts et de forcerait pas à tout refaire ?_
J'ai donc récupérer une fonction `ESCAPE_HTML`, et je l'applique à l'intégralité de mes chaînes directement quand je les insère dans mon state. Si ce ne sont pas des strings (souvent des nombres), je ne peux pas utiliser `ESCAPE_HTML` (vu qu'il utilise la méthode replace) et dans ce cas, je vérifie le `typeof` des données que je récupère.
Je pense que c'est tout sauf performant, mais malheureusement, c'est ce que j'ai trouvé de mieux pour pouvoir garder la structure de mon projet sans le refaire de zéro. En espérant que ça convienne comme solution de damage control.

## Le mot de la fin

Un truc sur, c'est que c'était un projet cool. On se rend compte quand on fait quelque chose comme ça qu'on a jamais vraiment fini, on veut toujours rajouter des trucs par ci par là. Mais il faut savoir s'arrêter, et donc j'en resterai à cet état (le 28 juin 2021, à 19h02), sauf si je trouve un bug de mort qui casse tout.
Pour tester l'appli directement en ligne, c'est par là : https://ecfjs.bouland.o2switch.cefim.site. Normalement, cloner le repo puis faire un `npm install` fonctionne sans soucis.

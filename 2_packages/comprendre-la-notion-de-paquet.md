---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# 🏛 Comprendre la notion de paquet

> _Paquet / librairie / dépendance / module ?_&#x20;
>
>
>
> Si ces mots ne sont pas exactement équivalents, en python ou en R, ils signifient presque toujours avoir recours à une ou plusieurs fonctionnalités additionnelles du langage par l'import dans le code. Cela permet parfois de ne pas recoder soi-même ce qui existe déjà. Certaines librairies sont directement amenées avec python (sys ou os) ou R (stats), d'autres doivent être installées manuellement (pandas, tensorflow pour Python, deeplyr pour R).

Le CASD propose des environnements de travail sans internet pour des raisons de sécurité. Par conséquent, impossible de consulter une documentation Python ou R. Votre ordinateur personnel ou votre téléphone peut tout à fait vous aider dans ce cas. Il vous suffit de retranscrire la commande ou ligne de code obtenue en réponse à votre question. Cependant, pour les paquets, ce n’est pas possible d’effectuer une telle manœuvre. Les serveurs auxquels vous avez l’habitude de vous connecter pour récupérer les paquets (PYPI ou le CRAN par exemple) ne sont pas joignables sans internet. À gauche, dans le fonctionnement dans votre système personnel, votre ordinateur utilise sa connexion internet pour atteindre les serveurs PYPI ou CRAN et récupérer les paquets voulus.

<figure><img src="../chapters/images/serveurs.png" alt="" width="375"><figcaption><p>Fonctionnement des paquets au CASD pour R et Python</p></figcaption></figure>

Afin de vous permettre d’installer vous-même les packages, sans envoi de mail, le CASD vous met à disposition des serveurs internes pour Python et R (à droite sur le schéma). Ces serveurs ne contiennent pas l’ensemble des paquets disponibles sur les serveurs publics pour assurer la sécurité des environnements de travail. Ils sont synchronisés par nos équipes de façon manuelle. Ils contiennent les paquets les plus communs avec lesquels les utilisateurs travaillent. La liste est disponible ici.

Si vous souhaitez installer un paquet non présent dans nos dépôts, vous êtes invités à envoyer un email à [service@casd.eu](mailto:service@casd.eu) contenant les informations sur le package ainsi que le lien avec lequel le trouver. Nos équipes importeront alors le paquet et vous donneront les instructions nécessaires pour procéder à l’installation.

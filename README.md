# Project-Alpha
Algorithme de trading automatique basé sur du *reinforcement learning* (RL)

## Introduction
### Qu'est ce que Project Alpha ?
#### Objectif
L'objectif de ce projet est de créer un algorithme capable de gagner de l'argent en tradant des cryptomonnaies. L'algorithme sera contruit grâce à du *reinforcement learning* (RL).
Ce projet sera long et ardu, et ne se fera pas en un jour. Certains domaines sont encore à l'état de recherche et prendront plusieurs années avant d'être exploitables, c'est pourquoi je ne m'attend pas à ce que ce projet se construise rapidement.
Il faut aussi comprendre que je mène ce projet en parallèle de mes études et que je n'ai donc pas énormément de temps à y dédier.

#### Tentatives infructueuses
Ce n'est pas ma première tentative de créer un algorithme de trading automatique. Certaines de mes tentatives passées se trouvent sur ce github, d'autres non. Ces mois de travail infructueux m'ont apporté l'expérience nécessaire, je pense, pour mener ce dernier projet à bien.

## Mise en place
Je vais ici expliciter mes différents choix et les différents challenge que je dois surmonter pour mener à bien le projet. Cette partie se remplira au fur et à mesure de mon avancement.

### Pas une prédiction de prix
Au premier abord on aurait tendance à vouloir simplement faire une prédiction de prix. Si on sait que le marché va monter lors des prochaines minutes on achète, et si on sait qu'il va descendre on vend. Il y a plusieurs problèmes avec cette approche :
* Il n'y a pas qu'un seul prix. Il y a tout d'abord le _ask_, c'est plus petit prix auquel quelqu'un accepte de vendre. Ensuite il y a le _bid_, c'est le plus haut prix auquel quelqu'un accepte d'acheter. Une approche naïve serait de prédire le _mid price_, c'est la moyenne entre _ask_ et _bid_. Ce prix n'est que théorique et peut parfois être assez éloigné du prix réel.
* Un achat ou une vente peut s'étaler sur plusieurs prix différents. Imaginons qu'on veut acheter 1 bitcoin et que le _ask_ est à 7000$. Cette personne accepte de vendre 0.1 bitcoin à 7000$. La personne suivante dans la liste accepte de vendre 0.9 bitcoin à 7020$. Quand on achète notre bitcoin il nous coûte au final plus cher que le prix affiché à la base, 7018$.
* Une _price prediction_ ne prend pas en compte les _fees_, latences, ect. La bourse c'est plus compliqué qu'un simple graphe qui fluctue.
<a/>
On retient ici que le seul moyen de faire de l'argent avec un modèle de *price prediction* est ou bien de faire des prédictions sur de grandes timeframes et donc de grandes différences de prix, ou bien d'avoir une très bonne stratégie de placement d'ordres et de gestion des fees (ce qui est extrêmement complexe).
<br> <br>
Mais le gros inconvénient d'un modèle de *price prediction*

### Domaine d'application
Le programme tradera uniquement des cryptomonnaies pour plusieurs raisons :
* la data est gratuite et facile à obtenir, en une ligne de code je peux obtenir la data minute par minute d'une crypto depuis sa création
* tout peut être facilement automatisé grâce à des api publiques très complètes
* c'est du 24h/24 7j/7
* les marchés sont très volatiles
* c'est plus exitant

### Fonction objectif
Il semblerait logique au premier abord de demander à l'algorithme de maximiser son profit. Mais ce n'est pas suffisant. Pour tester leurs algorithmes les tradeurs utilisent différents indicateurs que voici :
* Net PnL (Net Profit and Loss) : Simplement combien l'algo gagne ou perd sur une certaine période de temps, moins les trading fees. Il faut maximiser cet indice.
* Alpha et Beta : Alpha définit à quel point la stratégie que vous utilisez est meilleure en terme de profit qu'une stratégie alternative sans risque. Beta exprime à quel point votre stratégie est volatile par rapport au marché. Un Alpha élevé et un Beta faible sont idéaux.
* Sharpe Ratio : Ce ratio mesure combien vous gagnez en plus par unité de risque que vous prenez. Le plus élevé il est, le mieux c'est.
* Maximum Drawdown : C'est la différence maximum entre un minimum local et un maximum local. Un MD de 50% signifie que vous avez à un moment perdu 50% de votre capital. Il faut minimiser cet indice le plus possible.
* Value at Risk (VaR) : Cette mesure quantifie avec une certaine probabilité combien vous pouvez perdre au maximum sur une certaine période de temps, sur un marché en condition normale. Il faut également minimiser cet indicateur.
<a/>
La fonction objectif est donc un mélange judicieux de ces différents facteurs. Par exemple, on peut demander à l'algorithme de maximiser son profit tout en gardant le Maximum Drawdown sous les 20%. C'est à nous de décider quelles caractéristiques on veut donner à notre stratégie.







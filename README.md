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

## Choix de conception
Je vais ici expliciter dans leurs grandes lignes certains de mes choix de conception, sans rentrer dans les aspects techniques de l'algorithme.

### Pas une prédiction de prix
Au premier abord on aurait tendance à vouloir simplement faire une prédiction de prix. Si on sait que le marché va monter lors des prochaines minutes on achète, et si on sait qu'il va descendre on vend. Il y a plusieurs problèmes avec cette approche :
* Il n'y a pas qu'un seul prix. Il y a tout d'abord le _ask_, c'est plus petit prix auquel quelqu'un accepte de vendre. Ensuite il y a le _bid_, c'est le plus haut prix auquel quelqu'un accepte d'acheter. Une approche naïve serait de prédire le _mid price_, c'est la moyenne entre _ask_ et _bid_. Ce prix n'est que théorique et peut parfois être assez éloigné du prix réel.
* Un achat ou une vente peut s'étaler sur plusieurs prix différents. Imaginons qu'on veut acheter 1 bitcoin et que le _ask_ est à 7000$. Cette personne accepte de vendre 0.1 bitcoin à 7000$. La personne suivante dans la liste accepte de vendre 0.9 bitcoin à 7020$. Quand on achète notre bitcoin il nous coûte au final plus cher que le prix affiché à la base, 7018$.
* Une _price prediction_ ne prend pas en compte les _fees_, latences, ect. La bourse c'est plus compliqué qu'un simple graphe qui fluctue.  

On retient ici que le seul moyen de faire de l'argent avec un modèle de _price prediction_ est ou bien de faire des prédictions sur de grandes timeframes et donc de grandes différences de prix, ou bien d'avoir une très bonne stratégie de placement d'ordres et de gestion des fees (ce qui est extrêmement complexe).  
  
Mais le gros inconvénient d'un modèle de _price prediction_, c'est surtout qu'il n'a pas de stratégie. Imaginons que le modèle se trompe lors d'une prédiction, que doit il faire ? Tout vendre ? Vendre seulement une partie ? Et si le prix descend un peu plus remonte, le modèle doit il adopter la même stratégie que si le prix tombe ? Une prédiction du prix, aussi robuste soit-elle, ne peut être parfaite. C'est pourquoi on a besoin d'un modèle qui sait faire preuve de stratégie et qui sait faire des choix en fonction de la situation. On a besoin de _reinforcement learning_.

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

La fonction objectif est donc un mélange judicieux de ces différents facteurs. Par exemple, on peut demander à l'algorithme de maximiser son profit tout en gardant le Maximum Drawdown sous les 20%. C'est à nous de décider quelles caractéristiques on veut donner à notre stratégie.
	
### Echelle temporelle
Pour pouvoir trader à une échelle de jours, il faut pouvoir avoir une vision global de l'environnement autour de la monnaie. Beaucoup de facteurs rentrent en compte, tels que les news ou l'engouement général. Ce genre d'analyse est très difficile à automatiser avec des techniques de _machine learning_. De l'autre côté on trouve le trading à haute fréquence, les trades se font à des échelles de millisecondes et même parfois de nanosecondes. Les stratégies sont très simples et réagissent à certains patterns. Un _neural net_, bien que beaucoup plus rapide que l'humain, est très lent par rapport à ces stratégies "no brain". Il ne peut les battre.  
  
L'échelle temporelle idéale pour notre algorithme se trouve quelque part entre ces deux extrêmes. On veut une échelle temporelle où on peut analyser la data plus rapidement qu'un humain et où l'intelligence de notre algo permet de battre les programmes simples mais rapides. Je pense que l'algorithme trouve sa place quelque part entre des échelles de quelques millisecondes et de quelques minutes. Un humain peut certainement être compétant à une échelle de minutes mais il ne peut pas prendre en compte autant de data que notre algorithme et être aussi rapide. 

## Aspects techniques
Je vais ici expliciter les challenges auquels je fais face dans la réalisation de ce projet. Certains aspects peuvent être difficiles à comprendre pour une personne n'ayant jamais touché au _machine learning_ et particulièrement au _reinforcement learning_.







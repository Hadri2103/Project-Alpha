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
[//]: # (Hello)
La fonction objectif est donc un mélange judicieux de ces différents facteurs. Par exemple, on peut demander à l'algorithme de maximiser le profit tout en gardant le Maximum Drawdown sous les 20%. C'est à nous de décider quelles caractéristiques on veut donner à notre stratégie.

### 





# Remplacement d'un switch d'étage saturé

[← Retour au portfolio](tp-camille.html)

*PME de métallurgie, 45 postes, site principal — mars 2026 — option SISR*

## Contexte

Le site principal compte 45 postes, dont 12 dans l'atelier, reliés à un switch d'étage installé en 2016. Les postes de l'atelier servent aux plans de fabrication et à la saisie des temps.

## Problématique

Depuis trois semaines, les 12 postes de l'atelier subissaient des coupures réseau de quelques secondes, plusieurs fois par jour. La sauvegarde du serveur de fichiers, lancée à 12 h, durait 42 minutes au lieu des 6 minutes habituelles et terminait parfois en erreur.

## Démarche

J'ai d'abord relevé les débits depuis un poste de l'atelier : 8 Mo/s en copie vers le serveur, contre 74 Mo/s depuis un poste du bureau. Trois hypothèses : le câblage, la carte réseau des postes, le switch.

J'ai écarté le câblage : les liens ont été certifiés en 2023 et un test au testeur de câble sur trois prises n'a rien montré. J'ai écarté la carte réseau : le problème touchait les 12 postes, pas un seul.

Restait le switch, un modèle 16 ports à 100 Mb/s dont les compteurs affichaient des erreurs de collision. Je l'ai remplacé par un switch administrable gigabit prêté par le fournisseur, pour valider l'hypothèse avant tout achat.

## Outils mobilisés

- Switch administrable 16 ports gigabit (modèle de prêt, puis modèle acheté)
- Testeur de câble RJ45
- Wireshark 4.2 pour observer les retransmissions
- GLPI 10.0 pour le suivi du ticket et la mise à jour de l'inventaire

## Précautions prises

J'ai sauvegardé la configuration de l'ancien switch, étiqueté les 16 câbles avant de les débrancher, et programmé l'intervention entre 12 h 30 et 13 h 15, hors production. J'ai prévenu le chef d'atelier la veille.

## Résultats

Le débit de copie est passé de 8 Mo/s à 74 Mo/s. La sauvegarde est redescendue à 6 minutes. Aucune coupure signalée dans les trois semaines qui ont suivi. L'inventaire GLPI a été mis à jour le jour même.

## Bilan personnel

J'ai perdu deux jours à suspecter le câblage alors que les compteurs d'erreurs du switch donnaient la réponse dès le premier relevé. La prochaine fois, je commencerai par interroger les équipements réseau en SNMP avant de tester les liens un par un.

---

**Compétences mobilisées** : gérer le patrimoine informatique ; répondre aux incidents et aux demandes d'assistance.

## SITUATION B

## Contexte
Intervention réalisée le 28 septembre 2026 au sein du bureau d'études.
Matériel concerné : Station de travail Dell Precision 3630.

## Problème initial
Le poste de travail subissait des redémarrages inopinés (3 à 4 fois par jour) depuis une quinzaine de jours, entraînant la perte récurrente du travail en cours pour l'utilisateur.

## Diagnostic et options écartées
L'analyse de l'observateur d'événements a mis en évidence des erreurs critiques Kernel-Power 41. Deux hypothèses initiales ont été traitées et écartées :

Instabilité logicielle : Option écartée car l'application complète des mises à jour Windows n'a pas modifié le comportement du poste.

Défaillance de la mémoire vive (RAM) : Option écartée sur critère technique (un diagnostic MemTest86 exécuté sur une nuit complète a retourné 0 erreur).

## Mesures de sécurité
Avant l'ouverture du boîtier, le poste a été mis hors tension, le câble secteur débranché, et le bouton d'alimentation a été maintenu enfoncé pendant 10 secondes afin de décharger les condensateurs de la carte mère.

## Intervention technique
L'inspection visuelle a révélé une alimentation d'origine (350 W) saturée de poussière dont le ventilateur émettait un bruit anormal. Une mesure à la prise wattmétrique a indiqué une consommation de 310 W en pic de charge, laissant une marge de tolérance insuffisante. Le bloc a été remplacé par une alimentation neuve de 550 W, opération complétée par un dépoussiérage intégral du châssis.

## Résultats
Stabilité totale du système retrouvée : le monitoring confirme 0 redémarrage intempestif sur une période d'observation de 30 jours consécutifs.

## Bilan personnel
Validation d'un premier diagnostic matériel mené et résolu en autonomie. L'axe d'amélioration pour les prochaines interventions consistera à inclure la vérification des contraintes énergétiques (mesure wattmétrique) plus tôt dans l'arbre de diagnostic, immédiatement après l'identification d'une erreur d'alimentation dans les journaux système.




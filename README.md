# Géométrie Computationnelle Universelle (GCU)

[![Licence CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Statut](https://img.shields.io/badge/Statut-recherche%20en%20cours-orange.svg)]()

**GCU** est un cadre mathématique en développement depuis environ trois ans, à titre indépendant, sous QuantumLens Research Initiative. Il part d'un pavage octovalent de l'espace — un stencil à 14 points (6 faces + 8 sommets d'un cube) — et l'étend en une géométrie de calcul plus riche que le binaire, sans l'exclure : le binaire en est une coupe dégénérée, pas l'inverse.

> Ce document décrit l'état réel du projet, sans enjolivement. GCU n'est pas publié ni relu par des pairs à ce stade.

## Structure

GCU s'organise autour de trois couches sur un même objet géométrique (cube/octaèdre) :

- **Combinatoire** — (ℤ/2ℤ)³, le squelette : 8 champs, 12 transitions, 4 dualités.
- **Génératrice** — Cl(3), l'algèbre de Clifford associative des 3 générateurs.
- **États** — 𝕆, les octonions (non-associatifs), seule algèbre réelle de dimension 8 à division normée (Hurwitz) — la non-associativité y est une nécessité structurelle, pas un défaut.

Huit champs d'analyse (géométrie, arithmétique, topologie, computation, statistique, physique, quantique, éthique) sont dérivés de cette structure à des degrés de maturité inégaux — certains établis (D, démontré), d'autres encore ouverts (O) ou contraints par construction (C).

## Ce qui est établi

- Un noyau d'invariants figé, vérifié par 142 assertions indépendantes.
- Un mécanisme d'estimation locale sans gradient global (GGR), testé sur plusieurs régimes synthétiques, y compris non-stationnaires.
- Une règle de décision par signe de l'associateur octonionique, avec effet mesuré (non-associativité causale même pour un agent isolé).
- Une famille de langages (O/O+/O++) pour l'implémentation, distincte de l'algèbre 𝕆.

Le détail de ce qui est démontré, contraint ou encore ouvert est documenté dans le corpus complet (non public à ce stade).

## Direction actuelle

Exploration d'une application à des substrats biologiques réels (organoïdes neuronaux sur électrodes) — encore au stade du test, pas d'un système opérationnel. Rien n'est validé sur données réelles à ce jour.

## Licence

CC BY-NC-SA 4.0 © 2026 QuantumLens Research Initiative
Recherche non commerciale. Citations requises.

## Contact

Jean-Christophe Ané — QuantumLens Research Initiative
quantumlens.research@gmail.com

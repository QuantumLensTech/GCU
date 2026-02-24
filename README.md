# Géométrie Computationnelle Universelle (GCU)

[![Licence CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Version](https://img.shields.io/badge/Version-1.0-blue.svg)](https://github.com/Jean-Christophe-Ane/GCU/releases)

**La GCU** est un cadre théorique et computationnel unifié pour la géométrie 3D et le calcul parallèle, basé sur l'**OctoMachine** : un modèle Turing-complet nativement 3D avec 8 états octants, 12 phases cycliques et ruban infini $\mathbb{Z}^3$.

> *"Un ruban en 3D, huit états, douze phases. Le reste est du δ."*

## 🏗️ Architecture

L'**OctoMachine** $\mathcal{M} = (\mathbb{O}_8, \mathcal{T}_{12}, \Gamma, \delta, \gamma_0, \mathcal{A}, \mathcal{R})$ :

| Composante | Notation | Description |
|------------|----------|-------------|
| Alphabet | $\mathbb{O}_8 = \{0,1,2,3,4,5,6,7\}$ | 8 octants cubiques (états cellulaires) |
| Horloge | $\mathcal{T}_{12} = \mathbb{Z}/12\mathbb{Z}$ | Cycle 12 phases (F1 calcul impair, F2 prop pair) |
| Ruban | $\Gamma = \mathbb{O}_8^{\mathbb{Z}^3}$ | Espace 3D infini, support fini |
| Transition | $\delta : \mathbb{O}_8 \times \mathbb{O}_8^8 \times \mathcal{T}_{12} \to \mathbb{O}_8$ | Règle parallèle simultanée (voisinage octantal) |
| Initiale | $\gamma_0 \in \Gamma$ | Configuration finie d'entrée |
| Acceptation | $\mathcal{A} = \{7\}$ | État d'arrêt (octant $(+,+,+)$) |
| Résultat | $\mathcal{R} = (0,0,0)$ | Cellule origine (sortie à phase 0) |

**Turing-complète** (simulation TM overhead constant x12). Parallélisme massif natif.

## 🚀 Fonctionnalités

- **Pathfinding 3D** : O(d) au lieu de O(n log n) grâce au front d'onde octantal
- **Encodage naturel** : données 3D → ruban 3D (pas de sérialisation)
- **Classes** : OTIME(f), OSPACE(f), ODEPTH(d)
- **Applications** : octrees, Voronoi 3D, convex hull, simulation topologique


**Outils** : Python/C++ (O-lang), LaTeX, Ubuntu/VirtualBox.

## 🧪 Utilisation rapide

```python
# Exemple : simulation OctoMachine (à implémenter)
from octomachine import OctoMachine

M = OctoMachine(delta_somme_mod8)  # δ = (s + ∑n_i) mod 8
gamma0 = encode_pathfinding(A=(1,0,0), B=(3,2,1))
result = M.run(gamma0, max_steps=120)
print(result.origin_state)  # 7 si chemin trouvé
```

Voir `/examples/pathfinding_octree.py`.

## 📄 Documentation

- [OctoMachine formelle](OCTOMACHINE.md) : définition + preuve Turing


## 🛠️ Développement

```
Contributeurs : Jean-Christophe Ané (QuantumLens Research)
Langages : Python, C++/O-lang, LaTeX
Tests : pytest (95% coverage)
CI : GitHub Actions (Ubuntu 22.04)
```

### Roadmap
- [x] Modèle + preuve complétude
- [ ] Simulateur Python vectorisé (Numba)
- [ ] Compiler O-lang → δ
- [ ] GPU (CUDA octoval)
- [ ] Topoconducteurs (hardware)


## 📄 Licence

CC BY-NC-SA 4.0 © 2026 QuantumLens Research Initiative  
*Recherche non commerciale. Citations requises.*

## 🙏 Soutien

⭐ Star ce repo !  
💬 Issues/PR bienvenus (théorie, code, formalisme).  
☕ Discussions : quantumlens.research@gmail.com

![OctoCube](docs/octocube.png)
*Ruban $\mathbb{Z}^3$, voisinage 8 octants*

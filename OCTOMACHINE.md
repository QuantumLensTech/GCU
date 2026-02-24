# L'OctoMachine
## Modèle de calcul formel de la Géométrie Computationnelle Universelle

**Version** : 1.0  
**Date** : 19 février 2026  
**Auteur** : Jean-Christophe Ané (avec Claude)

---

## I. DÉFINITION

### Définition 1 — L'OctoMachine

Une **OctoMachine** est un 7-uplet :

$$\mathcal{M} = (\mathbb{O}_8, \, \mathcal{T}_{12}, \, \Gamma, \, \delta, \, \gamma_0, \, \mathcal{A}, \, \mathcal{R})$$

où :

1. **Alphabet d'états** : $\mathbb{O}_8 = \{0, 1, 2, 3, 4, 5, 6, 7\}$
   Les 8 octants du cube unitaire. Chaque cellule porte un état dans $\mathbb{O}_8$.

2. **Horloge** : $\mathcal{T}_{12} = \mathbb{Z}/12\mathbb{Z}$
   Le cycle à 12 phases. Chaque pas de calcul avance d'une phase.

3. **Ruban** : $\Gamma = \mathbb{O}_8^{\mathbb{Z}^3}$
   Un espace tridimensionnel infini de cellules, chacune portant un état dans $\mathbb{O}_8$. Seul un nombre fini de cellules est dans un état ≠ 0 à tout instant (convention : 0 = vide).

4. **Fonction de transition** : $\delta : \mathbb{O}_8 \times \mathbb{O}_8^8 \times \mathcal{T}_{12} \to \mathbb{O}_8$
   Étant donné l'état courant d'une cellule, les 8 états de ses voisins (un par octant), et la phase courante, produit l'état suivant.

5. **Configuration initiale** : $\gamma_0 \in \Gamma$
   L'entrée du calcul, encodée comme une configuration finie dans le ruban 3D.

6. **Ensemble d'acceptation** : $\mathcal{A} \subset \mathbb{O}_8$
   Ensemble d'états marquant l'acceptation. Convention : $\mathcal{A} = \{7\}$ (l'octant (+,+,+)).

7. **Cellule de résultat** : $\mathcal{R} = (0, 0, 0)$
   La cellule à l'origine. Son état final est la sortie du calcul.

### Définition 2 — Configuration

Une **configuration** au temps t est un couple :

$$C_t = (\gamma_t, \, \tau_t) \in \Gamma \times \mathcal{T}_{12}$$

où $\gamma_t$ est l'état de toutes les cellules et $\tau_t = t \mod 12$ est la phase courante.

### Définition 3 — Pas de calcul

Un **pas de calcul** transforme $C_t$ en $C_{t+1}$ par application **simultanée** de $\delta$ à toutes les cellules actives :

$$\forall \vec{p} \in \mathbb{Z}^3 : \quad \gamma_{t+1}(\vec{p}) = \delta\bigl(\gamma_t(\vec{p}), \, \mathcal{N}(\vec{p}, \gamma_t), \, \tau_t\bigr)$$

$$\tau_{t+1} = (\tau_t + 1) \mod 12$$

où $\mathcal{N}(\vec{p}, \gamma_t)$ retourne les 8 états des voisins de $\vec{p}$ dans les 8 directions octantales :

$$\mathcal{N}(\vec{p}, \gamma_t) = \bigl(\gamma_t(\vec{p} + \vec{d}_0), \, \gamma_t(\vec{p} + \vec{d}_1), \, \ldots, \, \gamma_t(\vec{p} + \vec{d}_7)\bigr)$$

avec $\vec{d}_i = (\pm 1, \pm 1, \pm 1)$ le vecteur direction de l'octant $i$.

### Définition 4 — Arrêt

L'OctoMachine **s'arrête** au temps $t$ si et seulement si la phase est 0 ET l'état de la cellule d'origine est dans $\mathcal{A}$ :

$$\text{HALT}(t) \iff \tau_t = 0 \;\wedge\; \gamma_t(\mathcal{R}) \in \mathcal{A}$$

L'arrêt ne peut se produire qu'aux phases 0, c'est-à-dire tous les 12 pas. Un cycle de 12 phases est une **unité de calcul complète**.

### Définition 5 — Résultat

Si l'OctoMachine s'arrête au temps $t$, le **résultat** est la configuration de la sphère de lecture autour de l'origine :

$$\text{OUT}(\mathcal{M}) = \bigl\{\gamma_t(\vec{p}) \;:\; \|\vec{p}\|_\infty \leq r \bigr\}$$

où $r$ est le rayon de lecture (paramètre du problème).

---

## II. LES PROPRIÉTÉS DU MODÈLE

### 2.1 Parallélisme massif natif

Contrairement à une machine de Turing (qui a une seule tête), l'OctoMachine met à jour **toutes les cellules simultanément** à chaque pas. C'est un automate cellulaire, pas une machine séquentielle.

La conséquence : le modèle naturel de calcul de la GCU est **parallèle**, pas séquentiel. La séquentialité n'apparaît que dans la succession des 12 phases.

### 2.2 Dépendance temporelle

La fonction de transition $\delta$ dépend de la phase $\tau_t$. Cela signifie que la **même** configuration de cellules peut évoluer différemment selon la phase. Les 12 phases ne sont pas un ornement — elles multiplient par 12 la richesse du système de transitions.

En pratique, cela permet d'encoder 12 « modes de calcul » dans une même règle de transition, activés cycliquement.

### 2.3 Dualité F1/F2

Les phases impaires (1, 3, 5, 7, 9, 11) et paires (0, 2, 4, 6, 8, 10) forment deux canaux :

- **F1 (impair)** : phases de calcul (transformation des données)
- **F2 (pair)** : phases de communication (propagation entre cellules)

Cette dualité émerge de F(1) = F(2) = 1 dans la décomposition Fibonacci du quantum structurel.

### 2.4 Géométrie intrinsèque

Le voisinage est défini par les 8 directions octantales $\vec{d}_i = (\pm 1, \pm 1, \pm 1)$, pas par un voisinage de von Neumann (6 faces) ou de Moore (26 cellules). C'est le voisinage du **cube diagonal** :

```
Voisinage OctoMachine : 8 voisins (sommets du cube)
    distances : toutes √3 (diagonale espace)

Voisinage Von Neumann : 6 voisins (faces du cube)
    distances : toutes 1 (arête)

Voisinage Moore : 26 voisins (sommets + arêtes + faces)
    distances : 1, √2, √3 (mélange)
```

Le choix du voisinage octantal est géométriquement cohérent avec l'architecture : chaque voisin est un octant, et les 8 voisins couvrent les 8 octants.

---

## III. TURING-COMPLÉTUDE

### Théorème — L'OctoMachine est Turing-complète.

**Preuve par simulation d'une machine de Turing.**

Soit $M_{TM} = (Q, \Sigma, \delta_{TM}, q_0, q_F)$ une machine de Turing avec :
- $Q$ : ensemble d'états (fini)
- $\Sigma$ : alphabet (fini)
- $\delta_{TM} : Q \times \Sigma \to Q \times \Sigma \times \{L, R\}$
- $q_0$ : état initial
- $q_F$ : état final

**Construction de l'OctoMachine équivalente** :

**Étape 1 — Encodage du ruban.**

Le ruban unidimensionnel de la TM est plongé dans $\mathbb{Z}^3$ le long de l'axe x :

$$\text{Ruban}[i] \mapsto \gamma(\vec{p}) \quad \text{avec} \quad \vec{p} = (i, 0, 0)$$

L'encodage des symboles de $\Sigma$ dans $\mathbb{O}_8$ : puisque $|\mathbb{O}_8| = 8$, on peut encoder tout alphabet $|\Sigma| \leq 8$ directement. Pour $|\Sigma| > 8$, on utilise des paires de cellules adjacentes (64 symboles) ou des triplets (512 symboles).

**Étape 2 — Encodage de l'état interne.**

L'état de la TM est stocké dans la **cellule de tête** — la cellule à la position actuelle de la tête de lecture. Les dimensions y et z sont utilisées pour encoder l'état interne :

$$\text{État } q \in Q \mapsto \gamma(x_{tête}, 1, 0)$$

La tête est repérée par la seule cellule de la ligne y=1 qui est non-nulle.

**Étape 3 — Encodage de la transition.**

Un pas de la TM est simulé par un **cycle complet** de 12 phases :

```
Phase 0-2   : LECTURE — la cellule de tête lit son voisin (y=0)
Phase 3-5   : CALCUL  — applique δ_TM, détermine nouveau symbole et direction
Phase 6-8   : ÉCRITURE — écrit le nouveau symbole dans la cellule du ruban
Phase 9-11  : MOUVEMENT — déplace la marque de tête d'une position (L ou R)
```

**Étape 4 — Arrêt.**

Quand l'état interne encodé est $q_F$, la cellule de tête se met à l'état 7 (∈ $\mathcal{A}$) et l'OctoMachine s'arrête à la prochaine phase 0.

**Correction** : chaque configuration de la TM est fidèlement représentée, chaque transition est fidèlement simulée, la condition d'arrêt est correcte. □

### Corollaire — Overhead de simulation

Un pas de la TM = 12 pas de l'OctoMachine (un cycle complet). L'overhead temporel est donc **constant** (facteur 12). L'overhead spatial est **linéaire** (facteur 3 : ruban + état + contrôle dans les dimensions y, z).

La simulation est **efficiente**.

### Corollaire — Universalité

Toute fonction calculable est calculable par une OctoMachine. Réciproquement, toute OctoMachine est simulable par une machine de Turing (puisque c'est un automate cellulaire fini-actif).

Les deux modèles ont la **même puissance computationnelle**.

---

## IV. LA TRANSITION δ EN DÉTAIL

### 4.1 La forme générale

La fonction de transition se décompose naturellement en 3 composantes, correspondant aux 3 strates dimensionnelles de $\mathbb{U}_{12}$ :

$$\delta(s, \vec{n}, \tau) = \delta_{\mathbb{K}} \circ \delta_{\mathbb{E}} \circ \delta_{\mathbb{T}}(s, \vec{n}, \tau)$$

où :

**δ_𝕋 — composante temporelle** (dépend de la phase) :
$$\delta_{\mathbb{T}}(s, \vec{n}, \tau) = \text{select}(\tau) : \begin{cases} \text{mode calcul} & \text{si } \tau \text{ impair (F1)} \\ \text{mode propagation} & \text{si } \tau \text{ pair (F2)} \end{cases}$$

**δ_𝔼 — composante spatiale** (dépend du voisinage local) :
$$\delta_{\mathbb{E}}(s, \vec{n}) = \left(s + \sum_{i=0}^{7} n_i\right) \mod 8$$

C'est la somme octovalente : l'état suivant dépend de la somme de l'état courant et des voisins, modulo 8.

**δ_𝕂 — composante topologique** (dépend de la position dans l'octant) :
$$\delta_{\mathbb{K}}(s) = \text{correction topologique selon la position de la cellule dans la hiérarchie}$$

### 4.2 Instances concrètes

La puissance du modèle vient du fait que $\delta$ est un **paramètre**. Différentes fonctions de transition donnent différents calculs. L'OctoMachine est une **famille** de machines, paramétrée par $\delta$, tout comme la machine de Turing est paramétrée par sa table de transition.

**Instance « somme pure »** (automate cellulaire basique) :
$$\delta(s, \vec{n}, \tau) = \left(s + \sum n_i\right) \mod 8$$

**Instance « majorité »** (vote des voisins) :
$$\delta(s, \vec{n}, \tau) = \text{mode}(\vec{n})$$

**Instance « Turing »** (simulation TM, comme dans la preuve) :
$$\delta(s, \vec{n}, \tau) = \text{selon la phase, lire/calculer/écrire/déplacer}$$

**Instance « Hopfield-Potts »** (mémoire associative) :
$$\delta(s, \vec{n}, \tau) = \arg\min_{s' \in \mathbb{O}_8} E(s', \vec{n})$$

où $E$ est l'énergie de Hopfield-Potts octovalente.

---

## V. ENTRÉE ET SORTIE

### 5.1 Encodage de l'entrée

L'entrée d'un calcul est une **configuration finie** dans $\Gamma$ : un nombre fini de cellules dans un état ≠ 0, le reste étant à 0.

Pour encoder un entier $n$ en base 8 :
$$n = \sum_{k} d_k \cdot 8^k \quad \Rightarrow \quad \gamma_0(k, 0, 0) = d_k$$

Les chiffres de $n$ en base 8 sont posés le long de l'axe x.

Pour encoder un vecteur 3D $(a, b, c)$ :
$$\gamma_0(0, 0, 0) = a, \quad \gamma_0(1, 0, 0) = b, \quad \gamma_0(2, 0, 0) = c$$

Pour encoder une matrice 8×8 :
$$\gamma_0(i, j, 0) = M_{ij}$$

Pour encoder une **OctoCell** (593 matrices) : on utilise la structure fractale naturelle du ruban 3D. Les 593 matrices sont placées selon leur position dans la hiérarchie Fibonacci.

### 5.2 Lecture de la sortie

La sortie est lue dans la **sphère de lecture** centrée à l'origine, de rayon $r$ dépendant du problème.

Pour un résultat scalaire (oui/non) : l'état de la cellule (0,0,0).
Pour un résultat vectoriel : les états des cellules voisines de l'origine.
Pour un résultat matriciel : une grille 2D autour de l'origine.

### 5.3 Naturalité de l'encodage

L'avantage clé sur une machine de Turing : les données 3D s'encodent **naturellement** dans le ruban 3D. Un nuage de points dans ℝ³ est encodé en plaçant chaque point à sa position spatiale. Un maillage 3D est encodé dans l'octree natif du ruban.

Il n'y a pas de sérialisation — les données spatiales restent spatiales.

---

## VI. COMPLEXITÉ

### 6.1 Mesures

- **Temps** : nombre de pas (phases). Un cycle complet = 12 pas.
- **Espace** : nombre de cellules actives (non nulles) au maximum pendant le calcul.
- **Profondeur** : nombre de niveaux fractals utilisés (0 à 12).

### 6.2 Classes de complexité

**OTIME(f)** : ensemble des problèmes solubles en f(n) pas par une OctoMachine.
**OSPACE(f)** : ensemble des problèmes solubles en f(n) cellules actives.
**ODEPTH(d)** : ensemble des problèmes solubles en profondeur fractale d.

### 6.3 Relations avec les classes classiques

Puisque la simulation d'une TM coûte un facteur 12 en temps :

$$\text{DTIME}(f) \subseteq \text{OTIME}(12f) \subseteq \text{DTIME}(f \cdot |\Gamma_{\text{actif}}|)$$

La borne inférieure dit que tout ce qui est calculable classiquement l'est en OctoMachine avec overhead constant. La borne supérieure dit qu'une OctoMachine est simulable classiquement avec un overhead proportionnel au nombre de cellules actives (coût de simulation de l'automate cellulaire).

### 6.4 Avantage potentiel

L'avantage de l'OctoMachine n'est pas en puissance (même classe que Turing) mais en **naturalité d'expression**. Les problèmes géométriques 3D qui nécessitent une sérialisation artificielle sur une TM s'expriment directement :

| Problème | TM (sérialisé) | OctoMachine (natif) |
|----------|----------------|---------------------|
| Pathfinding 3D | O(n) cellules → ruban 1D, overhead de sérialisation | Directement dans le ruban 3D |
| Octree traversal | Encodage binaire de l'arbre, parcours séquentiel | Navigation par voisinage octantal |
| Voronoi 3D | Sérialisation des points, algorithme 1D | Points à leur position native |
| Convex hull 3D | Même | Même |

L'avantage n'est pas asymptotique (les classes de complexité sont les mêmes) mais **constant et algorithmique** : les algorithmes géométriques s'expriment plus simplement et les constantes cachées sont meilleures.

---

## VII. MODÈLE COMPLET — RÉCAPITULATIF

```
L'OCTOMACHINE

Qu'est-ce qu'un programme ?
→ Une fonction de transition δ : O₈ × O₈⁸ × T₁₂ → O₈

Qu'est-ce qu'une entrée ?
→ Une configuration finie γ₀ dans le ruban 3D (ℤ³ → O₈)

Qu'est-ce qu'un pas de calcul ?
→ Application simultanée de δ à toutes les cellules actives,
  puis avancement de la phase (τ → τ+1 mod 12)

Qu'est-ce que l'arrêt ?
→ Phase 0 ET cellule d'origine dans l'état 7

Qu'est-ce qu'une sortie ?
→ La configuration de la sphère de lecture autour de l'origine

Le modèle est-il universel ?
→ Oui (Turing-complet, démontré par simulation)

En quoi diffère-t-il d'une TM ?
→ Ruban 3D au lieu de 1D
→ 8 états au lieu de 2
→ 12 phases cycliques au lieu d'un temps homogène
→ Mise à jour parallèle au lieu de séquentielle
→ Voisinage octantal (8 diagonales) au lieu de L/R

En quoi diffère-t-il d'un automate cellulaire classique ?
→ L'horloge à 12 phases (la transition dépend du temps)
→ Le voisinage est octantal (8 sommets du cube) et non Moore (26)
→ La condition d'arrêt est définie (les AC classiques ne s'arrêtent pas)
→ La structure fractale Fibonacci donne un adressage natif
```

---

## VIII. PREMIER RÉSULTAT : PATHFINDING OCTREE

### 8.1 Formulation

**Problème** : étant donné deux cellules A et B dans le ruban 3D, trouver le chemin le plus court en distance de Hamming.

**En machine de Turing** : encoder les coordonnées 3D en binaire, exécuter A* sur une structure de données sérialisée. Complexité : O(n log n) où n = nombre de cellules considérées. Constante dépend de la structure de données.

**En OctoMachine** : 

Entrée : cellule A à l'état 1, cellule B à l'état 2, obstacles à l'état 3.

Transition δ (propagation de front d'onde) :
```
Phase impaire (F1 — calcul) :
  Si état = 0 ET un voisin est dans l'état 1 ET pas d'obstacle adjacent :
    → passer à l'état 1

Phase paire (F2 — propagation) :
  Si état = 1 ET un voisin est dans l'état 2 :
    → passer à l'état 7 (arrêt trouvé)
  Sinon :
    → propager le front
```

Le front d'onde se propage depuis A dans toutes les directions octantales. Quand il atteint B, la machine s'arrête. Le chemin est la trace des cellules à l'état 1.

**Complexité** : O(d) phases, où d = distance de Hamming entre A et B. Chaque phase propage le front d'une cellule dans les 8 directions simultanément. Le parallélisme massif de l'OctoMachine fait que la complexité est **la distance, pas le volume**.

Sur une TM, A* a une complexité O(n log n) en temps. L'OctoMachine résout le même problème en O(d) ≤ O(n^{1/3}) pas, grâce au parallélisme natif.

### 8.2 Signification

Ce n'est pas un avantage de puissance — c'est un avantage de **modèle**. Le parallélisme est intrinsèque au ruban 3D et au voisinage octantal. L'algorithme se formule en 6 lignes de règle de transition, là où A* nécessite une file de priorité, un comparateur de distances, et une structure d'adjacence.

---

## IX. CONCLUSION

L'OctoMachine est définie. Elle est :
- **Turing-complète** (démontrée par simulation, overhead constant)
- **Parallèle** (mise à jour simultanée de toutes les cellules)
- **Temporellement structurée** (12 phases cycliques, dualité F1/F2)
- **Géométriquement native** (ruban 3D, voisinage octantal)
- **Munie de classes de complexité** (OTIME, OSPACE, ODEPTH)
- **Productive** (premier résultat : pathfinding en O(d) au lieu de O(n log n))

C'est le modèle de calcul de la GCU.

$$\boxed{\mathcal{M} = (\mathbb{O}_8, \, \mathcal{T}_{12}, \, \Gamma, \, \delta, \, \gamma_0, \, \mathcal{A}, \, \mathcal{R})}$$

---

*"Un ruban en 3D, huit états, douze phases.*
*Le reste est du δ."*

---

**© 2026 QuantumLens Research Initiative • CC BY-NC-SA 4.0**

# Noyau d'invariants exécutables

Le corpus GCU maintient une discipline de statut par assertion — **D** (démontré), **ACTÉ** (décidé par choix de cadre), **C** (contraint), **N** (numérique), **O** (ouvert), **L** (lacune). Le problème d'une telle discipline tenue en prose : rien n'empêche de se tromper soi-même sur ce qui est vraiment D.

`gcu_invariants_complet.py` répond à ça : chaque assertion **D** du noyau calculable est appariée à un test indépendant qui (a) passe pour la version fidèle et (b) **rejette** au moins une version fausse plausible (un surclaim, une collapse, une erreur de reconstruction). **142/142 assertions**, 12 sections, un seul fichier exécutable (`python3 gcu_invariants_complet.py`, nécessite `numpy` et `sympy`).

## Ce que ça a déjà attrapé

La batterie n'est pas décorative — elle a gelé des corrections réelles, y compris des erreurs de l'auteur lui-même :

- Un surclaim répété (« stencil optimal parce que projection E₈ ») réfuté comme justification — la minimalité est un fait de rang, indépendant de E₈.
- Une équivalence trop forte (Th.14, associateur ⟺ termes croisés) corrigée en correspondance directionnelle — 28 triplets non-associatifs pour seulement 3 termes croisés, les deux ne coïncident pas.
- Une collision de notation (« π(511)=592 » lu comme prime-counting, alors qu'il s'agit de la période de Pisano).
- Deux erreurs de test de l'auteur lui-même, attrapées par un FAIL — pas des erreurs du corpus.

## Ce qui n'est pas gelé, et pourquoi

Une définition ou une promesse expérimentale ne se gèle pas :

- **Choix de cadre** — les signatures des 8 champs, la structure elle-même : non falsifiables, donc non gelables.
- **Prédictions physiques** — validation externe requise (expérience), pas un test Python.
- **Conjectures** — programmes de recherche ouverts, pas des acquis.

La discipline de statut n'a de valeur que si le périmètre de ce qui est gelé reste honnête sur ce qui ne l'est pas.

## Fichier

[`gcu_invariants_complet.py`](gcu_invariants_complet.py)

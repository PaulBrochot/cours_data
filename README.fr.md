# cours_data 🏠📊

[🇬🇧 English](README.md) | 🇫🇷 Français

Mon apprentissage de **NumPy, pandas, matplotlib et scikit-learn**, qui se termine par un petit projet de data science : **prédire le prix d'appartements**.

> Suite de [mini_sklearn](https://github.com/PaulBrochot/mini_sklearn), où j'avais codé une mini-bibliothèque de machine learning en Python pur. Ici, j'utilise les vrais outils.

---

## Projet final : prédire le prix d'un appartement

📓 Notebook : [`projet.ipynb`](projet.ipynb)

### La question

Peut-on prédire le prix d'un appartement à partir de sa surface ? Et le quartier joue-t-il un rôle ?

### Les étapes

1. **Charger et nettoyer** les données : supprimer les doublons, retirer les lignes sans prix, compléter les étages manquants par la médiane, ajouter une colonne prix au m² (17 lignes → 15 appartements propres)
2. **Explorer** : prix médian, quartiers les plus et les moins chers au m², filtres
3. **Visualiser** : prix selon la surface, coloré par quartier
4. **Modéliser avec la surface seule** : `LinearRegression` de scikit-learn, comparée à un modèle de référence qui prédit toujours le prix moyen
5. **Ajouter le quartier** : encodage one-hot avec `pd.get_dummies`
6. **Conclure**

### Prix selon la surface, par quartier

![Prix selon la surface](nuage.png)

À surface égale, les appartements du Centre sont systématiquement plus chers, et ceux du Nord moins chers.

### Résultats

Erreur moyenne absolue sur le jeu de test (5 appartements, `random_state=42`) :

| Modèle | Erreur moyenne (k€) |
|---|---|
| Moyenne (référence) | 79.5 |
| Surface seule | 48.5 |
| Surface + quartier | **19.5** |

### Conclusion

Ajouter la surface fait passer l'erreur de 79.5 à 48.5 k€, et ajouter le quartier la fait encore baisser à 19.5 k€. Le quartier apporte presque autant d'information que la surface et **divise l'erreur par plus de 2**.

⚠️ **Limite :** ces chiffres reposent sur seulement 15 appartements, dont 5 en test. Avec un autre découpage, les erreurs pourraient être assez différentes. Pour une conclusion fiable, il faudrait beaucoup plus de données, ou une validation croisée.

---

## Le cours, chapitre par chapitre

| Notebook | Sujet |
|---|---|
| `chapitre1.ipynb` | Tableaux NumPy : shape, dtype, vectorisation |
| `chapitre2.ipynb` | Sélection, masques booléens, agrégations, nombres aléatoires |
| `chapitre3.ipynb` | Recoder une partie de mini_sklearn avec NumPy (erreur, séparation train/test, régression linéaire) |
| `chapitre4.ipynb` | pandas : Series, DataFrame, `read_csv` |
| `chapitre5.ipynb` | `loc` / `iloc`, filtres, `isin` |
| `chapitre6.ipynb` | Nettoyage : valeurs manquantes, doublons, types |
| `chapitre7.ipynb` | `groupby`, `agg`, tri |
| `chapitre8.ipynb` | Visualisation avec matplotlib |

---

## Installation

```bash
git clone https://github.com/PaulBrochot/cours_data.git
cd cours_data
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Ensuite, ouvre les notebooks dans VS Code ou Jupyter.

---

## Ce que j'ai appris

- Penser en **vecteurs** plutôt qu'en boucles (NumPy)
- Charger, nettoyer, filtrer et agréger des tableaux (pandas)
- Faire des graphiques lisibles (matplotlib)
- Entraîner et évaluer un modèle avec scikit-learn : `train_test_split`, `fit`, `predict`, `mean_absolute_error`
- Transformer des catégories texte en nombres (encodage one-hot)
- Toujours comparer un modèle à une **référence**, et ne jamais laisser le jeu de test fuiter dans l'entraînement
- Rester prudent sur les conclusions tirées de petits jeux de données

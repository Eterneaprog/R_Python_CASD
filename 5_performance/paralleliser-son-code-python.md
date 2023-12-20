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

# 🐍 Paralléliser son code Python

### Paralléliser un calcul avec Python

Le calcul utilisant plusieurs cœurs est possible en Python et en R. Un certain nombre de traitements natifs ou accessibles via des paquets sont d'ailleurs naturellement parallélisés dans ces langages. Voici un exemple de calcul multicœur utilisant des processus en Python. Il ne s'agit pas de la seule façon de faire. Le principe de fonctionnement est souvent identique :

<figure><img src="../chapters/images/parallel.png" alt=""><figcaption><p>Le multi processing permet de gagner du temps d'exécution</p></figcaption></figure>

Il s'agit de distribuer la charge de travail sur plusieurs cœurs/machines afin d'assurer une vitesse de calcul optimale plutôt que de faire faire les opérations par un seul cœur. En effet, on fait donc plusieurs calculs en même temps plutôt que les uns après les autres.

Généralement, un processus central est responsable d'invoquer les autres et de récupérer leurs résultats. De cette manière, on divise la charge des différents cœurs du nombre de cœurs utilisés pour les calculs.

**Attention :** L'ensemble des calculs ne se prêtent pas au calcul distribué, en particulier si les calculs à effectuer sur les différentes opérations sont fortement liés. Ce paradigme est particulièrement efficace et simple à mettre en place sur les traitements séquentiels indépendants.

```python
import multiprocessing

# Fonction qui sera exécutée dans chaque processus indépendant
def worker_function(worker_id, data):
    print(f"Worker {worker_id} traite {data}")
    # Vous pouvez insérer ici vos traitements

if __name__ == "__main__":
    # Données à traiter (peut être une liste, un dictionnaire, etc.)
    data_to_process = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

    # Créer un pool de processus avec multiprocessing.Pool
    num_processes = 4  # Utilise 4 coeurs pour effectuer le traitement
    pool = multiprocessing.Pool(processes=num_processes)

    # Mapper la fonction de travail sur les données en parallèle
    # Chaque processus exécute la worker_function avec une partie des données
    results = []
    for i, data_chunk in enumerate(data_to_process):
        result = pool.apply_async(worker_function, (i, data_chunk))
        results.append(result)

    # Attendre la fin de tous les processus
    pool.close()
    pool.join()

    # Récupérer les résultats si nécessaire
    final_output = [result.get() for result in results]

    # Traitement final avec les résultats si nécessaire
    # ...

    print("Tous les processus sont terminés.")

```

Dans ce code, on exécute un traitement sur les données de façon parallèle avec 4 processus. On commence par définir le traitement que chaque processus va effectuer. Puis, la partie du code qui suite l'instruction `if __name__ == "__main__"` correspond au processus central sur le schéma précédent. Il commence par invoquer les autres processus. Puis, il leur assigne une tâche à effectuer et enregistre les résultats. Une fois ces traitements effectués, les processus sont terminés et on obtient le résultat final que l'on peut retraiter dans le processus central (ou non si ce n'est pas nécessaire).

**Attention :** Les ressources mémoires associées à chaque processus sont partagées dans cet exemple ! Cela veut dire que l'utilisation massive de processus peut provoquer une saturation de la mémoire RAM. Chaque processus peut être amené à utiliser des ressources mémoires dans son traitement, et donc augmenter fortement la consommation par rapport à un traitement monoprocesseur.

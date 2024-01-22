# 🐍 VSCode

### Les possibilités

VScode est l'environnement de développement le plus populaire au monde. Il permet pratiquement de coder avec tout langage de programmation. Cependant, l'utiliser nécessite une configuration plus importante du fait qu'il est très généraliste. Faisons un tour d'horizons de certaines fonctions utiles :

1. **Langue :** VScode est utilisable en langue française en utilisant la touche F1, et en saisissant `Configure Display Language`
2. **Syntaxe :** La coloration syntaxique avancée et l'indentation automatique sont activées par défaut.
3. **Enregistrement et formatage automatique** : Vous pouvez demander à VSCode d'enregistrer le code pour vous en ouvrant les paramètres dans fichiers > préférences > paramètres. Recherchez le paramètre Auto-save. De plus, VSCode peut formatter le fichier à chaque enregistrement de celui-ci à l'aide du paramètre Format On Save.
4. **Git intégré** : VSCode est livré avec une intégration Git native, cette interface peut être plus simple d'utilisation que le terminal. Pour l'utiliser, le bouton se situe dans la colonne de gauche et se nomme Contrôle de code source.
5. **IntelliSense**: Il s'agit du système d'auto-complétion pour Python.
6. **Débuggeur intégré**: À l'aide des points d'arrêt dans le code, vous pouvez suivre l'exécution à l'aide du mode debug. Vous pourrez visualiser l'évolution des variables. Le mode débug de VSCode se situe juste en dessous de l'intégration git dans la colonne de gauche.
7. **Terminal intégré :** VSCode propose un terminal intégré qui vous permet d'exécuter des commandes Python et d'autres tâches sans quitter l'éditeur. Pour cela, utilisez le menu terminal.
8. **Linter intégré :** Les linters tels que Pylint peuvent être intégrés pour identifier et corriger les erreurs de style de code et les problèmes potentiels.

<figure><img src="../chapters/images/VScode.png" alt=""><figcaption><p>VScode est un éditeur de code généraliste</p></figcaption></figure>

### Les extensions

Vous pouvez installer de nombreuses extensions VSCode dans la bulle. Pour cela, voici la procédure :

* Dans VSCode, appuyez sur Ctrl+Shift+X pour ouvrir le menu extensions
* Dans les ... de ce menu, cliquez sur 'installer depuis VSIX'.
* Choissisez un fichier VSIX correspond à l'extension que vous souhaitez installer dans le dossier S:\VsCode

Deux extensions sont obligatoires : ms-python.python et ms-tollsai.jupyter.

Une fois les extensions installées, pour utiliser votre environnement conda, appuyer sur "Ctrl+Shift+P" puis sélectionner "Python : select interpreter" et choisissez votre environnement.

Il est possible d'ouvrir des notebooks jupyter depuis VSCode ou d’exécuter les programmes dans une fenêtre interactive.&#x20;

Si vous préférez lancer vos programmes dans un Terminal :

* Utiliser « Ctrl+Shift+P » puis chercher « Terminal : Select Default Profile »&#x20;
* Choisir « Command Prompt »&#x20;
* &#x20;Tuer les terminaux éventuellement ouverts avec l’icône corbeille






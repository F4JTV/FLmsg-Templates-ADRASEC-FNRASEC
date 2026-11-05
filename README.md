# Formulaires FLmsg ADRASEC et FNRASEC

Formulaires personnalisés pour **FLmsg**, l'éditeur de messages de la suite NBEMS associée à **fldigi**. Ils permettent de rédiger, transmettre et relire par radio les messages des ADRASEC et de la FNRASEC, avec la même mise en page chez l'émetteur et chez le destinataire.

Deux jeux indépendants sont fournis. Ils peuvent être installés ensemble ou séparément.

| Archive | Formulaires | Menu FLmsg |
|---|---|---|
| `ADRASEC_FLmsg_v1.1.0.zip` | `ADRASEC_Message.html` | Message ADRASEC (ambiance, situation, message encapsulé, procédure codifiée) |
| | `ADRASEC_AR.html` | AR ADRASEC (accusé de réception) |
| `FNRASEC_FLmsg_25.10.1.zip` | `FNRASEC_MessageExercice.html` | FNRASEC Message Exercice |
| | `FNRASEC_MessageCommandement.html` | FNRASEC Message de commandement |
| | `FNRASEC_BilanSituation.html` | FNRASEC Bilan de situation |
| | `FNRASEC_ArretePrefectoral.html` | FNRASEC Arrete prefectoral |
| | `FNRASEC_EtatReseaux.html` | FNRASEC Etat des reseaux |
| | `FNRASEC_AR.html` | FNRASEC Accuse de reception |

Les formulaires ADRASEC sont communs à tous les départements. Les formulaires FNRASEC sont le portage pour FLmsg des modèles Winlink FNRASEC 25.10.1.

---

## Prérequis

- **fldigi** et **FLmsg** (version 4.0 ou plus récente).
- Un **navigateur web** par défaut (Firefox, Chrome, Edge…) : FLmsg y ouvre les formulaires.

FLmsg et fldigi se téléchargent sur la page du projet : <https://sourceforge.net/projects/fldigi/files/> (dossiers `flmsg` et `fldigi`).

---

## Principe : le dossier `CUSTOM`

Pour installer les formulaires, il suffit de copier les fichiers `.html` dans le dossier **`CUSTOM`** de FLmsg. FLmsg crée ce dossier à son premier lancement :

| Système | Dossier `CUSTOM` |
|---|---|
| Windows | `C:\Users\<utilisateur>\NBEMS.files\CUSTOM\` |
| Linux | `~/.nbems/CUSTOM/` (dossier caché) |

FLmsg surveille ce dossier en permanence : un formulaire copié apparaît dans les menus au bout d'une seconde, sans redémarrage.

Seuls les fichiers `.html` sont des formulaires. Les fichiers `README` et `LICENSE` des archives n'ont pas besoin d'être copiés.

---

## Installation sous Windows

1. **Installer fldigi et FLmsg** avec leurs installateurs Windows (`fldigi-x.x.x_setup.exe`, `flmsg-x.x.x_setup.exe`).
2. **Lancer FLmsg une première fois.** Il crée le dossier `NBEMS.files` et demande quelle interface utiliser :
   - *Simple* : création et lecture de messages, adaptée aux personnels non radioamateurs ;
   - *Expert* : toutes les fonctions, dont l'envoi par fldigi. C'est le choix de l'opérateur radio.
3. **Ouvrir le dossier `CUSTOM`** : dans l'Explorateur de fichiers, coller dans la barre d'adresse
   ```
   %USERPROFILE%\NBEMS.files\CUSTOM
   ```
   puis appuyer sur Entrée. En interface simple, un élément de menu de FLmsg ouvre directement ce dossier des modèles.
4. **Extraire l'archive** : clic droit sur le `.zip` → *Extraire tout…*
5. **Copier les fichiers `.html`** du dossier extrait dans `CUSTOM`.

Pour installer les deux jeux, répéter les étapes 4 et 5 pour chaque archive : tous les fichiers vont dans le même dossier `CUSTOM`.

---

## Installation sous Linux

Exemple pour Debian, Ubuntu et dérivés :

1. **Installer fldigi et FLmsg** :
   ```bash
   sudo apt install fldigi flmsg
   ```
2. **Lancer FLmsg une première fois** pour qu'il crée `~/.nbems/`, et choisir l'interface (voir l'étape 2 de Windows).
3. **Copier les formulaires** depuis le dossier où se trouvent les archives :
   ```bash
   mkdir -p ~/.nbems/CUSTOM

   # Jeu ADRASEC
   unzip -o ADRASEC_FLmsg_v1.1.0.zip -d /tmp/adrasec_flmsg
   cp /tmp/adrasec_flmsg/ADRASEC_FLmsg/*.html ~/.nbems/CUSTOM/

   # Jeu FNRASEC
   unzip -o FNRASEC_FLmsg_25.10.1.zip -d /tmp/fnrasec_flmsg
   cp /tmp/fnrasec_flmsg/FNRASEC_FLmsg_25.10.1/*.html ~/.nbems/CUSTOM/
   ```
4. **Vérifier** :
   ```bash
   ls ~/.nbems/CUSTOM/
   ```

Pour passer par le gestionnaire de fichiers plutôt que par le terminal, afficher les dossiers cachés avec **Ctrl+H** : `.nbems` apparaît alors dans le dossier personnel.

---

## Dossier `NBEMS.files` déplacé

Si FLmsg est lancé avec l'option `--flmsg-dir "chemin"`, par exemple pour faire tourner plusieurs couples fldigi / FLmsg, le dossier `CUSTOM` se trouve sous ce chemin et non à l'emplacement par défaut. Il faut alors copier les formulaires dans le `CUSTOM` de **chaque** instance utilisée.

---

## Vérifier l'installation

- **Interface expert** : menu **Form → Custom**. Les entrées « Message ADRASEC », « AR ADRASEC » et « FNRASEC … » doivent apparaître.
- **Interface simple** : bouton **Create**. Les mêmes noms figurent dans la liste.

En sélectionnant un formulaire puis **Edit Form**, FLmsg ouvre le formulaire dans le navigateur.

---

## Recevoir automatiquement les messages avec fldigi

Pour qu'un message reçu s'ouvre dans FLmsg, configurer fldigi dans **Configure → Config Dialog → Misc → NBEMS interface** :

- activer l'ouverture des messages reçus avec FLmsg ;
- indiquer l'emplacement de l'exécutable FLmsg s'il n'est pas trouvé automatiquement ;
- optionnellement, activer l'ouverture du message dans le navigateur.

---

## Règles d'interopérabilité

Elles valent pour les deux jeux et conditionnent les échanges entre stations et entre départements.

1. **L'émetteur et le destinataire doivent avoir les mêmes formulaires.** Par radio, FLmsg ne transmet que les valeurs des champs, pas le formulaire. Sans le fichier, le destinataire voit les données brutes ou le message « Custom form … not found! ».
2. **Ne jamais renommer les fichiers.** Chaque message contient le nom de son formulaire (par exemple `CUSTOM_FORM,ADRASEC_Message.html`), et la station réceptrice cherche un fichier portant exactement ce nom.
3. **Distribuer les formulaires à l'avance.** FLmsg sait transmettre un formulaire par radio (menu **Form → Custom → Transfer FORM**), mais les fichiers pèsent de 26 à 88 Ko, ce qui est long en HF. Mieux vaut les installer avant l'activation : clé USB, courriel, site de l'association.

**Seule personnalisation sans risque :** le titre affiché. Dans `ADRASEC_Message.html`, la ligne `<h1>Message ADRASEC` peut devenir `<h1>Message ADRASEC 83`. Il ne faut modifier ni le nom du fichier ni la ligne `META NAME="MENU_ITEM"`.

---

## Utilisation en bref

1. Ouvrir le formulaire (**Edit Form**), le remplir, puis cliquer sur **Transmettre à FLmsg** en bas de page.
2. Dans FLmsg, enregistrer le message (fichier `.k2s`).
3. Choisir le mode numérique, puis cliquer sur **AutoSend** : fldigi transmet le message.

**Accusé de réception.** FLmsg n'a pas de fonction « Répondre ». Ouvrir le message reçu (**View Form**), cliquer sur **Préparer l'accusé de réception**, puis ouvrir le formulaire d'accusé correspondant (« AR ADRASEC » ou « FNRASEC Accuse de reception »). Le numéro, le destinataire et la référence y sont repris automatiquement.

**Accents.** Tous les textes sont convertis en ASCII à l'envoi : les modes de fldigi (MT63, Olivia…) ne transmettent pas toujours les caractères accentués.

**Navigateur.** Le numéro de message et les indicatifs sont mémorisés par le navigateur qui affiche les formulaires. Ils sont donc perdus si le navigateur par défaut change ou s'il fonctionne en navigation privée : il suffit alors de les ressaisir une fois.

---

## Mise à jour depuis la version ADRASEC 06

Les anciens formulaires s'appelaient `ADRASEC06_Message.html` et `ADRASEC06_AR.html`.

- Copier les nouveaux fichiers `ADRASEC_*.html` comme indiqué plus haut.
- **Conserver les anciens fichiers** tant qu'il faut relire des messages enregistrés avec l'ancienne version : ces messages font référence aux anciens noms. Ensuite, les supprimer du dossier `CUSTOM`.
- Ressaisir une fois l'indicatif et le dernier numéro de message.

---

## Désinstallation

Supprimer les fichiers `ADRASEC_*.html` et/ou `FNRASEC_*.html` du dossier `CUSTOM`. Les messages enregistrés (`.k2s`) ne sont pas touchés, mais ne pourront plus être affichés en formulaire.

---

## Dépannage

| Symptôme | Cause probable | Solution |
|---|---|---|
| Le formulaire n'apparaît pas dans les menus | Fichier copié ailleurs que dans `CUSTOM`, ou laissé dans un sous-dossier | Copier le `.html` directement dans `CUSTOM` |
| « Custom form … not found! » à la réception | Formulaire absent chez le destinataire, ou fichier renommé | Installer le même fichier, sous le même nom, chez les deux stations |
| Le navigateur ne s'ouvre pas | Pas de navigateur par défaut, ou port du serveur interne de FLmsg occupé | Définir un navigateur par défaut ; vérifier le serveur de formulaires dans la configuration de FLmsg |
| Page restée vide après **Transmettre à FLmsg** | FLmsg fermé pendant la saisie | Garder FLmsg ouvert pendant toute la rédaction |
| Numéro de message ou indicatif non proposés | Navigateur différent, navigation privée ou données de navigation effacées | Ressaisir une fois ; utiliser toujours le même navigateur |

---

## Licence et crédits

- **Formulaires FNRASEC** : portage des modèles Winlink FNRASEC de F4IXH Jean-Louis Zola et F1COB Jean-Michel Brocal, <https://github.com/jlzola/fnrasec-winlink-template>. Licence MIT, voir `LICENSE.txt` dans l'archive FNRASEC.
- **Formulaires ADRASEC** : gabarit visuel inspiré des modèles FNRASEC.

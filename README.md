# Suivi Nat — par TechByDsk

**Votre dossier ANEF, votre progression et vos dates importantes, dans une extension Chrome à usage local.**

Suivi Nat permet de consulter le statut de votre demande de naturalisation et de conserver son évolution sur votre appareil. Son interface TechByDsk associe un thème sombre, des accents cyan et une lecture simple de votre parcours.

Il s’agit d’un outil personnel et non officiel, indépendant de l’administration française. Les informations et documents de votre espace ANEF restent la référence : les étapes affichées par l’extension sont une interprétation des données disponibles, pas une décision administrative.

## Fonctionnalités

- **Vue du dossier** : statut actuel, étape, durée à cette étape et dernière vérification.
- **Progression visuelle** : étapes passées en vert, étape en cours en orange, étapes à venir grisées. Une procédure clôturée utilise un affichage de fin de parcours.
- **Historique local** des statuts observés par l’extension.
- **Dates d’étapes** : consultation des dates disponibles et rectification manuelle des champs modifiables.
- **Plusieurs dossiers** : consultation des dossiers détectés et choix d’un dossier principal.
- **Mode discrétion** : bouton en forme d’œil pour masquer visuellement certaines informations sensibles.
- **Notifications Chrome** lors des changements détectés, selon vos réglages.
- **Copier le suivi** : copie d’un résumé dans le presse-papiers, à votre initiative.
- **Export et import JSON** pour conserver une sauvegarde personnelle.

## Installation dans Chrome

Aucune compilation, clé API ou installation de dépendances n’est nécessaire.

1. Téléchargez le projet avec **Code → Download ZIP**, puis décompressez-le, ou clonez le dépôt :

   ```bash
   git clone https://github.com/sdiawa/anef-extension-local.git
   ```

2. Ouvrez `chrome://extensions` dans Chrome.
3. Activez le **Mode développeur**.
4. Cliquez sur **Charger l’extension non empaquetée**.
5. Sélectionnez le dossier contenant `manifest.json` — pas le fichier ZIP.
6. Dans le menu des extensions de Chrome, épinglez **Suivi Nat** pour accéder facilement au popup.

Conservez ce dossier à son emplacement : Chrome utilise directement les fichiers qui s’y trouvent.

## Première utilisation

1. Ouvrez le [portail officiel ANEF](https://administration-etrangers-en-france.interieur.gouv.fr/).
2. **Connectez-vous manuellement** avec votre compte ANEF.
3. Accédez à votre espace personnel, puis à **Mon compte**.
4. Attendez le chargement de la page et des informations du dossier.
5. Cliquez sur l’icône **Suivi Nat** dans la barre d’outils Chrome.

Lorsqu’un dossier a été récupéré, le popup affiche son statut et sa progression. Si aucune donnée n’est disponible, utilisez **Vérifier mon statut** pour ouvrir ANEF, puis assurez-vous d’être connecté au bon compte.

## Utilisation au quotidien

### Actualiser le dossier

Cliquez sur **Actualiser** dans le popup. L’extension ouvre temporairement une fenêtre minimisée ou un onglet inactif pour consulter ANEF avec votre session existante, puis tente de le fermer à la fin de la vérification.

L’opération peut prendre jusqu’à environ **45 secondes**. Si la session a expiré, reconnectez-vous manuellement sur ANEF, revenez à **Mon compte**, puis relancez l’actualisation.

L’extension ne contourne ni la connexion, ni les restrictions, ni les indisponibilités du portail.

### Lire la progression

| Couleur | Signification |
| --- | --- |
| Vert | Étapes précédentes du parcours affiché |
| Orange | Étape actuellement en cours |
| Gris | Étapes suivantes |

La jauge comporte 12 segments. Un statut comme **9.3/12** désigne une sous-étape de l’étape 9 : il ne signifie pas qu’une date de décision est connue.

Le compteur « À cette étape » indique une durée calculée à partir des dates connues. Il ne prédit pas le délai restant.

### Ouvrir les paramètres

Cliquez sur la **roue dentée** du popup pour accéder aux onglets :

- **Historique** : statuts enregistrés, journal des vérifications et dates d’étapes.
- **Paramètres** : notifications, réglages de vérification et gestion des identifiants encore présents dans cette version.
- **Export** : téléchargement d’une sauvegarde JSON, import d’un fichier et suppression des données.
- **Debug** : consultation et effacement des journaux techniques.

Pour une date modifiable, utilisez le champ ou le bouton de rectification disponible, puis **Enregistrer**. Certains champs issus d’ANEF ou certaines étapes futures restent verrouillés.

### Gérer plusieurs dossiers

Les dossiers sont détectés lorsque vous consultez les comptes correspondants sur ANEF. Le popup permet de passer d’un dossier enregistré à un autre lorsqu’il y en a plusieurs.

Choisissez le dossier principal avant d’utiliser les actions qui lui sont réservées. Les dossiers secondaires sont consultables en lecture seule pour certaines opérations.

**Attention au compte connecté :** l’actualisation utilise la session ANEF du navigateur. Pour consulter un autre compte, déconnectez-vous d’ANEF puis connectez-vous au compte souhaité.

### Sauvegarder et restaurer

Dans **Paramètres → Export**, cliquez sur **Exporter (JSON)**. Conservez ce fichier dans un emplacement privé : il peut contenir des numéros de dossier, des dates et d’autres informations personnelles.

Pour restaurer une sauvegarde, utilisez **Importer** et choisissez un fichier provenant de votre propre export. L’export standard exclut la clé de chiffrement et les identifiants enregistrés ; il ne permet donc pas de les transférer sur un autre appareil.

La synchronisation Chrome étant désactivée, **aucune sauvegarde automatique entre appareils n’est assurée par l’extension**.

## Confidentialité et fonctionnement local

Cette version a été adaptée pour supprimer les statistiques communautaires et désactiver la sauvegarde Chrome Sync. Les anciennes clés de synchronisation sont supprimées au chargement du module de stockage ; une erreur de purge est signalée dans la console si cette opération échoue.

- Les données du dossier et l’historique sont conservés dans `chrome.storage.local`.
- Les consultations du dossier contactent les services officiels ANEF : **« local » ne signifie pas « hors ligne »**.
- La connexion automatique est désactivée : le service worker ne transmet plus les identifiants pour se connecter.
- Aucun script, police ou thème distant n’est nécessaire à l’interface.
- Les exports et la copie du suivi sont déclenchés par l’utilisateur.

### Limites à connaître

- Des formulaires d’enregistrement d’identifiants hérités restent visibles. **Ils ne réactivent pas l’auto-login et ne sont pas nécessaires à l’utilisation manuelle.**
- La vérification automatique conserve actuellement une condition liée à la présence d’identifiants enregistrés. Elle ne doit pas être considérée comme un suivi autonome garanti ; privilégiez la consultation et l’actualisation manuelles.
- Le bouton **Récupérer** des dates ne restaure rien depuis un serveur : cette fonction est neutralisée dans la version locale.
- Le mode discrétion masque l’affichage ; il ne chiffre pas l’historique. Les journaux techniques peuvent également contenir des informations du dossier.
- Le bouton **Tout supprimer** conserve les identifiants selon le comportement actuel. Il ne constitue pas un effacement intégral de tous les secrets enregistrés.
- Cette version ne constitue pas une garantie absolue contre une compromission du navigateur, de l’appareil ou du site ANEF.

Ne partagez pas vos sauvegardes ou journaux techniques sans avoir retiré les informations personnelles.

## Mettre à jour l’extension

Si vous avez cloné le dépôt :

```bash
cd anef-extension-local
git pull --ff-only
```

Si vous utilisez une archive ZIP, remplacez les fichiers dans le dossier déjà chargé par Chrome.

Ensuite :

1. Ouvrez `chrome://extensions`.
2. Cliquez sur **Recharger** pour Suivi Nat.
3. Rechargez les onglets ANEF déjà ouverts.
4. Fermez puis rouvrez le popup et la page des paramètres.

Il n’est pas nécessaire de désinstaller l’extension pour la mettre à jour. Une désinstallation peut supprimer les données locales : exportez-les avant toute réinstallation.

## Dépannage

| Problème | Action conseillée |
| --- | --- |
| Aucune donnée dans le popup | Connectez-vous à ANEF et ouvrez **Mon compte**, puis relancez la consultation. |
| Session expirée | Reconnectez-vous manuellement sur le portail officiel. |
| Mot de passe expiré | Renouvelez-le directement sur ANEF. |
| Mauvais dossier affiché | Vérifiez le compte ANEF connecté et le dossier sélectionné dans l’extension. |
| Actualisation trop longue ou en échec | Vérifiez que le portail fonctionne et réessayez plus tard. |
| Ancien design encore visible | Rechargez l’extension, puis rouvrez le popup et les paramètres. |
| Erreur de service worker | Rechargez l’extension depuis le bon dossier et consultez la liste des erreurs dans `chrome://extensions`. |

Les changements de l’API ou de l’interface ANEF peuvent nécessiter une adaptation du code.

---

**TechByDsk · Suivi Nat** — un tableau de bord personnel pour suivre votre parcours ANEF.

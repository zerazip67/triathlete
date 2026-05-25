# triathlete

Le projet nécessite une base de données SQL Server nommée `AP_TRIATHLON`. Un script d'initialisation complet est fourni à la racine.

### Procédure d'installation : BDD
1. Ouvrez **SQL Server Management Studio (SSMS)** et connectez-vous à votre instance locale.
2. Sur un compte ayant tout les droits sur votre instance :
USE [master]
GO
CREATE LOGIN [express_user] 
WITH PASSWORD = 'express_user', 
DEFAULT_DATABASE = [master], 
CHECK_EXPIRATION = OFF, 
CHECK_POLICY = OFF
GO
4. Ouvrez le fichier `script.sql` dans SSMS (Fichier ➔ Ouvrir ➔ Fichier...).

### Procédure d'installation : Appli
Télécharger le fichier triathlon-app.zip
Decompresser le fichier.
Ouvrir visual studio code -> File -> Open Folder
Prendre le deuxieme triathlon-app (A gauche vous ne devez pas voir le script.sql)

Des modifications peuvent être nécessaire si le port suivant est déja utilisée : 3001.
dans backend/server.js ligne 5, 3001 par un port non utilisé

Dans VSCode -> Terminal -> New terminal
cd backend
npm install

cd .. 
npm install
Fermer le terminal.
Pour lancer le projet : 
Ouvrer un terminal et éxecuter : ng serve
Ouvrer un autre terminal et éxecuter : 
cd backend
node server.js
Laisser bien les deux terminaux et VSCode ouvert.

Aller sur localhost:4200 et utiliser le site.

## 🛑 Dépannage : Erreur de connexion à SQL Server (Port Dynamique)

Si l'API Express lors de l'execution de node server.js affiche une erreur de connexion alors que le script SQL a bien été exécuté, cela est généralement dû à la configuration des ports dynamiques de **SQL Express**.

### Comment fixer le port sur 1433 :
1. Ouvrez l'application **Gestionnaire de configuration SQL Server** (*SQL Server Configuration Manager*).
2. Déroulez *Configuration réseau SQL Server* ➔ Cliquez sur **Protocoles pour SQLEXPRESS** (ou votre nom d'instance).
3. Faites un clic droit sur **TCP/IP** et passez-le sur **Activé** (*Enabled*).
4. Faites un double-clic sur **TCP/IP** et allez dans l'onglet **Adresses IP**.
5. Faites défiler tout en bas jusqu'à la section **IPAll** :
   * **Supprimez le `0`** dans la ligne `Ports TCP dynamiques` (laissez la case complètement **vide**).
   * Écrivez `1433` dans la ligne `Port TCP`.
6. Cliquez sur *Appliquer* puis *OK*.
7. **Important :** Allez dans *Services SQL Server*, faites un clic droit sur votre service SQL Server et cliquez sur **Redémarrer**.

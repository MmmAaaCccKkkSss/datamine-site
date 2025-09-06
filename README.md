# DATAMINE ($DATA) — Site & Airdrop officiels

> Reprends le contrôle de tes données. Un écosystème Web3 où l’utilisateur choisit ce qu’il partage et peut le monétiser. $DATA est le jeton utilitaire du protocole, déployé sur **Polygon (POL)**.

---

## 🔗 Liens officiels

- **Site** : https://mmmaaaccckkksss.github.io/datamine-site/
- **Page de claim** : https://mmmaaaccckkksss.github.io/datamine-site/claim.html?ver=final
- **Swap (QuickSwap dApp)** : https://dapp.quickswap.exchange/#/swap?inputCurrency=0x3c499c542cEF5E3811e1192ce70d8cC03d5c3359&outputCurrency=0x79E1424617B0BeC83Ac00B59D39ED922e55E09f6
- **Pool (analytics)** : https://www.geckoterminal.com/polygon_pos/pools/0x6c2f35a80d219d48f30115537b549dcdcd321ad3
- **Contrat $DATA (Polygonscan)** : https://polygonscan.com/token/0x79E1424617B0BeC83Ac00B59D39ED922e55E09f6

---

## 🧾 Détails & adresses

- **Réseau** : Polygon (Mainnet) — Chain ID `137`
- **Jeton** : `Datamine Token (DATA)`
- **Adresse $DATA** : `0x79E1424617B0BeC83Ac00B59D39ED922e55E09f6`
- **Décimales** : `18`
- **USDC (native)** : `0x3c499c542cEF5E3811e1192ce70d8cC03d5c3359`
- **Pool DATA/USDC** : `0x6c2f35a80d219d48f30115537b549dcdcd321ad3`
- **MerkleDistributor (airdrop)** : `0x36073810B663210E28cb7960D0Df68517BCfA33d`
- **Merkle root (publié)** : voir `merkle-root.txt` à la racine du repo

**Vérifications rapides :**
- Sur Polygonscan, l’adresse du **token** doit finir par `...E09f6`.
- Le swap QuickSwap doit afficher **USDC (0x3c49…3359)** → **DATA (0x79E1…09f6)**.

---

## 🛒 Acheter $DATA (débutant)

1. Ouvre le lien **Swap** :  
   https://dapp.quickswap.exchange/#/swap?inputCurrency=0x3c499c542cEF5E3811e1192ce70d8cC03d5c3359&outputCurrency=0x79E1424617B0BeC83Ac00B59D39ED922e55E09f6
2. **Connecte** ton wallet (MetaMask) sur **Polygon**.  
3. Sélectionne le montant d’**USDC** à échanger → **Swap** → confirme la transaction.
4. (Option) Ajoute le jeton **DATA** dans MetaMask (import de l’adresse ci-dessus).

---

## 🎁 Réclamer l’airdrop (claim)

1. Va sur la **page de claim** :  
   https://mmmaaaccckkksss.github.io/datamine-site/claim.html?ver=final
2. Clique **Connecter mon wallet** (réseau **Polygon**).  
3. Vérifie que les champs sont **pré-remplis** :
   - **MerkleDistributor** : `0x36073810B663210E28cb7960D0Df68517BCfA33d`
   - **claims.json** : `https://mmmaaaccckkksss.github.io/datamine-site/claims.json`
4. Clique **Charger mon allocation** :
   - Si ton adresse est éligible, tu verras **“Éligible: X DATA”**.
5. Clique **Claim mes DATA** → confirme dans MetaMask.  
6. À la confirmation, ton statut devient **“Claim réussi ✅”** puis **“Déjà réclamé ✅”** après rechargement.

---

## 🧰 Dépannage (FAQ rapide)

- **Rien ne se passe en cliquant “Connecter”**  
  - Active **MetaMask** dans ton navigateur (autoriser en navigation privée si nécessaire).  
  - Rafraîchis fort (**Ctrl+F5**) ou ouvre le lien avec `?ver=final` / en fenêtre privée.  
  - Ferme d’autres extensions wallet (Rabby, Coinbase Wallet, etc.) qui peuvent interférer.

- **Message “invalid proof” au claim**  
  - Le `merkle-root` du contrat **ne correspond pas** au `claims.json` publié, ou ton adresse n’est pas dans la liste.  
  - Solution : régénérer **ensemble** `claims.json` + `merkle-root.txt`, republier `claims.json`, **redéployer** le MerkleDistributor avec le **nouveau root**.

- **Message “transfer failed”**  
  - Le contrat MerkleDistributor **n’a pas assez de DATA**.  
  - Solution : envoyer davantage de **DATA** à l’adresse du **MerkleDistributor**.

- **Réseau incorrect**  
  - Bascule sur **Polygon (Chain 137)** depuis MetaMask.

---

## 🧑‍🔧 Régénérer l’airdrop (`claims.json` + `merkle-root.txt`) — 100% GitHub

> **Aucune installation locale** (tout dans GitHub Codespaces).

1. Ajoute/édite **`airdrop.csv`** à la racine (format) :
   ```csv
   address,amount
   0xAdresse1,1000000000000000000
   0xAdresse2,2500000000000000000

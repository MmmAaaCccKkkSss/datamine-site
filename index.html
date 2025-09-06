// --- Constantes & helpers ---
const POLYGON_CHAIN_ID = '0x89'; // 137
const POLYGON_PARAMS = {
  chainId: POLYGON_CHAIN_ID,
  chainName: 'Polygon Mainnet',
  nativeCurrency: { name:'POL', symbol:'POL', decimals:18 },
  rpcUrls: ['https://polygon-rpc.com/'],
  blockExplorerUrls: ['https://polygonscan.com/']
};
const MERKLE_ABI = [
  "function claimed(address) view returns (bool)",
  "function claim(uint256 amount, bytes32[] calldata proof) external"
];
const isHexAddress = (a) => /^0x[0-9a-fA-F]{40}$/.test((a||"").trim());
const log = (...a) => {
  console.log(...a);
  const d = document.getElementById('diag');
  if (d) d.textContent += '\n' + a.map(x=> (typeof x==='string'?x:JSON.stringify(x))).join(' ');
};

// --- État global ---
let provider, signer, account, claimsMap = null;
let connectBtn, loadBtn, claimBtn, addrEl, networkBox, allocEl, eligBox, statusEl;

function bindUI() {
  connectBtn = document.getElementById('connectBtn');
  loadBtn    = document.getElementById('loadBtn');
  claimBtn   = document.getElementById('claimBtn');
  addrEl     = document.getElementById('addr');
  networkBox = document.getElementById('networkBox');
  allocEl    = document.getElementById('alloc');
  eligBox    = document.getElementById('eligBox');
  statusEl   = document.getElementById('status');

  connectBtn?.addEventListener('click', () => { log('CLICK_CONNECT'); connect().catch(e=>log('CONNECT_ERR', e.message||e)); });
  loadBtn?.addEventListener('click',    () => { log('CLICK_LOAD');    loadAllocation().catch(e=>log('LOAD_ERR', e.message||e)); });
  claimBtn?.addEventListener('click',   () => { log('CLICK_CLAIM');   doClaim().catch(e=>log('CLAIM_ERR', e.message||e)); });

  const hasMM = typeof window.ethereum !== 'undefined';
  const hasEthers = typeof window.ethers !== 'undefined';
  const diag = document.getElementById('diag');
  if (diag) diag.textContent = `Diagnostic: ${hasMM?'MetaMask détecté ✅':'MetaMask non détecté ❌'} | ${hasEthers?'ethers.js chargé ✅':'ethers.js non chargé ❌'}`;
}

// --- Connexion ---
async function connect() {
  if (!window.ethereum) { alert('MetaMask non détecté. Active l’extension dans Edge.'); return; }
  await ethereum.request({ method: 'eth_requestAccounts' });

  if (!window.ethers) { alert('Problème de chargement d’ethers.js. Recharge la page (Ctrl+F5).'); return; }

  provider = new ethers.providers.Web3Provider(window.ethereum, 'any');
  const network = await provider.getNetwork();
  log('NETWORK', network);

  if (network.chainId !== 137) {
    networkBox.innerHTML = 'Réseau: <b>'+network.name+'</b>. <span class="warn">Passe sur Polygon.</span> ';
    const switchBtn = document.createElement('button');
    switchBtn.textContent = 'Basculer sur Polygon';
    switchBtn.className = 'ghost';
    switchBtn.onclick = switchToPolygon;
    networkBox.appendChild(switchBtn);
  } else {
    networkBox.innerHTML = '<span class="ok">Réseau Polygon détecté ✅</span>';
  }

  signer  = provider.getSigner();
  account = await signer.getAddress();
  addrEl.textContent = account;
  log('ACCOUNT', account);
}

async function switchToPolygon() {
  try {
    await ethereum.request({ method: 'wallet_switchEthereumChain', params: [{ chainId: POLYGON_CHAIN_ID }] });
    networkBox.innerHTML = '<span class="ok">Réseau Polygon détecté ✅</span>';
    log('SWITCHED_POLYGON');
  } catch (e) {
    if (e.code === 4902) {
      await ethereum.request({ method: 'wallet_addEthereumChain', params: [POLYGON_PARAMS] });
      networkBox.innerHTML = '<span class="ok">Réseau Polygon ajouté ✅</span>';
      log('ADDED_POLYGON');
    } else {
      alert('Switch annulé : '+e.message);
      log('SWITCH_ERR', e.message||e);
    }
  }
}

// --- Allocation ---
async function loadAllocation() {
  statusEl.textContent = ''; eligBox.textContent = ''; allocEl.textContent = 'Chargement…';
  const distributorAddr = (document.getElementById('distributor').value||'').trim();
  const claimsUrl = (document.getElementById('claimsUrl').value||'').trim();

  if (!claimsUrl) { allocEl.textContent=''; alert('Renseigne l’URL de claims.json'); return; }

  const res = await fetch(claimsUrl, { cache:'no-store' });
  if (!res.ok) throw new Error('Impossible de charger claims.json');
  claimsMap = await res.json();
  log('CLAIMS_LOADED', Object.keys(claimsMap).length);

  if (!account) { allocEl.textContent=''; alert('Connecte ton wallet d’abord.'); return; }
  const entry = claimsMap[account.toLowerCase()];
  if (!entry) { allocEl.textContent=''; eligBox.innerHTML='<span class="err">Adresse non éligible.</span>'; return; }

  const { amount } = entry;
  const amountHuman = ethers.utils.formatUnits(amount, 18);
  allocEl.innerHTML = `Éligible: <b>${amountHuman} DATA</b>`;

  if (!isHexAddress(distributorAddr)) {
    eligBox.innerHTML = '<span class="warn">Colle l’adresse 0x… du MerkleDistributor pour vérifier le statut et pouvoir claim.</span>';
    return;
  }

  const c = new ethers.Contract(distributorAddr, MERKLE_ABI, provider);
  const already = await c.claimed(account);
  eligBox.innerHTML = already ? '<span class="warn">Déjà réclamé ✅</span>' : '<span class="ok">Non réclamé — prêt à claim</span>';
  log('CLAIM_STATUS', already ? 'already' : 'not_claimed');
}

// --- Claim ---
async function doClaim() {
  statusEl.textContent = 'Préparation…';
  const distributorAddr = (document.getElementById('distributor').value||'').trim();
  const claimsUrl = (document.getElementById('claimsUrl').value||'').trim();
  if (!account || !signer) { alert('Connecte ton wallet.'); statusEl.textContent=''; return; }
  if (!isHexAddress(distributorAddr)) { alert('Adresse du MerkleDistributor invalide (format 0x…)'); statusEl.textContent=''; return; }
  if (!claimsMap) { await loadAllocation(); if (!claimsMap) return; }
  const entry = claimsMap[account.toLowerCase()];
  if (!entry) { statusEl.innerHTML = '<span class="err">Adresse non éligible.</span>'; return; }

  const { amount, proof } = entry;
  const contract = new ethers.Contract(distributorAddr, MERKLE_ABI, signer);
  const tx = await contract.claim(amount, proof);
  statusEl.textContent = 'Tx envoyée: '+tx.hash+' (en attente…)';
  const rec = await tx.wait();
  statusEl.innerHTML = rec.status===1 ? '<span class="ok">Claim réussi ✅</span>' : '<span class="err">Échec de la transaction.</span>';
  if (rec.status===1) await loadAllocation();
  log('CLAIM_TX', rec.status);
}

// --- Démarrage ---
window.addEventListener('DOMContentLoaded', bindUI);

<!DOCTYPE html>
<html lang="sq">
<head>
  <meta charset="UTF-8" />
  <title>POS Market – Final Fixed + Complete</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <style>
    :root{
      --bg:#eef4ff;
      --card:#ffffff;
      --primary:#2563eb;
      --primary-2:#1d4ed8;
      --nav:#111827;
      --text:#1f2937;
      --muted:#6b7280;
      --line:#e5e7eb;
      --success:#16a34a;
      --danger:#dc2626;
      --warning:#b45309;
      --soft:#eff6ff;
      --soft-2:#f8fafc;
      --shadow:0 10px 26px rgba(15,23,42,.08);
      --radius:16px;
    }

    *{box-sizing:border-box}
    html,body{
      margin:0;
      padding:0;
      font-family:Segoe UI,Roboto,Arial,sans-serif;
      background:var(--bg);
      color:var(--text);
    }
    body{min-height:100vh}

    header{
      background:linear-gradient(135deg, var(--nav), #1f2937);
      color:white;
      padding:14px 18px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:12px;
      flex-wrap:wrap;
      box-shadow:0 8px 18px rgba(17,24,39,.12);
      position:sticky;
      top:0;
      z-index:30;
    }
    header h2{margin:0;font-size:1.15rem}
    nav{display:flex;flex-wrap:wrap;gap:8px;align-items:center}
    nav button{
      border:none;border-radius:10px;background:rgba(255,255,255,.08);color:#fff;padding:8px 12px;font-weight:600;cursor:pointer
    }
    nav button:hover{background:rgba(255,255,255,.16)}
    .alert-bell{
      background:linear-gradient(135deg,#fbbf24,#f59e0b);
      color:#111827;font-weight:800;border-radius:999px;padding:7px 12px;display:inline-flex;align-items:center;gap:8px;cursor:pointer;
      box-shadow:0 6px 16px rgba(245,158,11,.25)
    }
    .badge{background:#ef4444;color:white;border-radius:999px;padding:2px 7px;font-size:.75rem;min-width:20px;text-align:center}

    section{display:none;padding:18px}
    section.active{display:block}

    .card{
      background:var(--card);border-radius:var(--radius);box-shadow:var(--shadow);padding:18px;margin-bottom:14px;
      border:1px solid rgba(148,163,184,.15);
    }
    .card h3{margin-top:0;margin-bottom:12px}
    .row{display:flex;gap:10px;flex-wrap:wrap}
    .col{flex:1;min-width:120px}
    input,select,button,textarea{
      font:inherit;padding:10px 12px;border-radius:10px;border:1px solid #cbd5e1;outline:none;
    }
    input:focus,select:focus,textarea:focus{
      border-color:var(--primary);box-shadow:0 0 0 3px rgba(37,99,235,.12);
    }
    button{
      background:linear-gradient(135deg, var(--primary), var(--primary-2));
      color:#fff;border:none;font-weight:700;cursor:pointer;
      transition:.18s ease;box-shadow:0 8px 18px rgba(37,99,235,.2);
    }
    button:hover{transform:translateY(-1px)}
    button.secondary{background:linear-gradient(135deg,#64748b,#475569)}
    button.danger{background:linear-gradient(135deg,#dc2626,#b91c1c)}
    button.success{background:linear-gradient(135deg,#16a34a,#15803d)}

    table{width:100%;border-collapse:collapse;margin-top:12px;background:#fff;border-radius:10px;overflow:hidden}
    th,td{padding:10px 8px;border-bottom:1px solid var(--line);text-align:center;word-break:break-word;vertical-align:middle}
    th{background:var(--soft-2);font-weight:700;color:#334155}
    tr:last-child td{border-bottom:none}

    .small{font-size:.9rem;color:var(--muted)}
    .muted{color:var(--muted)}
    .admin{display:none}
    .qtyBtn{padding:5px 8px;border-radius:8px}

    .modal{
      position:fixed;inset:0;background:rgba(15,23,42,.58);display:none;z-index:99;padding:20px;overflow:auto;
    }
    .modal-content{
      background:white;border-radius:18px;max-width:760px;width:min(95%,760px);margin:60px auto;padding:18px;
      box-shadow:0 20px 45px rgba(0,0,0,.18);max-height:78vh;overflow:auto;
    }
    .small-modal{max-width:620px}
    .txn-list{margin:6px 0;padding-left:18px}
    .txn-summary{font-weight:700;margin-top:8px}
    .warn{color:var(--warning);font-weight:700}
    .success{color:var(--success);font-weight:700}
    .danger-text{color:var(--danger);font-weight:700}
    .expired{background:#fee2e2}
    .expiring{background:#fff7ed}
    .lowstock{background:#fff7f0}
    .category-select{width:100%}
    .stats-grid{
      display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px;margin-bottom:14px;
    }
    .stat-box{
      background:linear-gradient(135deg,#f8fbff,#eef6ff);padding:14px;border-radius:12px;border:1px solid rgba(37,99,235,.12);
      box-shadow:inset 0 1px 0 rgba(255,255,255,.4);
    }
    .stat-label{color:var(--muted);font-size:.8rem;text-transform:uppercase;letter-spacing:.05em}
    .stat-value{font-size:1.5rem;font-weight:800;margin-top:6px}
    .loyalty-box{
      background:linear-gradient(135deg,#eff6ff,#dbeafe);border:1px solid #bfdbfe;border-radius:12px;padding:12px;margin-top:12px;
    }
    .loyalty-positive{color:#15803d;font-weight:700}
    .loyalty-balance{
      background:rgba(255,255,255,.4);border:1px solid rgba(59,130,246,.15);border-radius:8px;padding:8px;margin-top:8px;
    }
    .report-box{
      background:linear-gradient(135deg,#f8fafc,#f1f5f9);
      border:1px solid #dbe3ef;border-radius:12px;padding:12px;margin-top:12px;
    }
    @media (max-width:700px){
      .row{flex-direction:column}
      nav{width:100%}
      nav button{flex:1 1 100%}
      .modal-content{margin:16px auto}
    }
  </style>

  <script src="https://unpkg.com/@ericblade/quagga2/dist/quagga.js"></script>
</head>
<body>

<header>
  <div style="display:flex;align-items:center;gap:12px;flex-wrap:wrap">
    <h2>🛒 POS Market Final</h2>
    <div id="alertBell" class="alert-bell" title="Alerts" onclick="openAlertsModal()">
      ALARME <span id="alertCount" class="badge">0</span>
    </div>
  </div>

  <nav id="menu" style="display:none">
    <button onclick="openSec('prod')" class="admin">Stok</button>
    <button onclick="openSec('sale')">Shitje</button>
    <button onclick="openSec('bil')" class="admin">Bilanc</button>
    <button onclick="openSec('hist')">Historik</button>
    <button onclick="openSec('clients')">Klientët</button>
    <button onclick="openSec('settings')" class="admin">Cilësimet</button>
    <button onclick="logout()">Dil</button>
  </nav>
</header>

<section id="loginSec" class="active">
  <div class="card" style="max-width:440px;margin:40px auto 0">
    <h3>Login</h3>
    <input id="u" placeholder="User" style="width:100%;margin-bottom:8px">
    <input id="p" type="password" placeholder="Password" style="width:100%;margin-bottom:8px">
    <button onclick="doLogin()">Hyr</button>
    <p id="msg" style="color:red;margin:10px 0 0"></p>
  </div>
</section>

<section id="prod">
  <div class="card admin">
    <h3>Shto Produkt</h3>
    <div class="row">
      <input id="pn" placeholder="Emri" class="col">
      <input id="pb" placeholder="Barkodi" class="col">
    </div>
    <div class="row" style="margin-top:8px">
      <input id="pp" type="number" placeholder="Çmimi (ALL)" class="col">
      <input id="ps" type="number" placeholder="Sasia" class="col">
    </div>
    <div class="row" style="margin-top:8px">
      <select id="pcat" class="col category-select">
        <option value="ushqim">Ushqim</option>
        <option value="pije">Pije</option>
        <option value="higjienike">Higjenike</option>
      </select>
      <input id="pexp" type="date" class="col">
      <input id="pmin" type="number" class="col" placeholder="Min Stock">
    </div>
    <div style="margin-top:10px">
      <button onclick="addProduct()">➕ Shto</button>
      <button onclick="openCam('stock','environment')">📷 Mbrapa</button>
      <button onclick="openCam('stock','user')">🤳 Para</button>
    </div>
  </div>

  <div class="card">
    <h3>Inventari</h3>
    <table id="prodTable"></table>
  </div>
</section>

<section id="sale">
  <div class="stats-grid" id="statsGrid"></div>

  <div class="card">
    <div class="row">
      <input id="saleScan" placeholder="Emër / Barkod / Scan USB" class="col">
      <input id="client" placeholder="Emri i klientit (opsional)" class="col">
      <input id="clientPhone" placeholder="Telefoni i klientit (opsional)" class="col">
    </div>

    <div class="row" style="margin-top:10px;align-items:center">
      <div style="flex:1;min-width:160px">
        <label class="small">Valuta e shitjes</label>
        <select id="saleCurrency" onchange="recalc()" style="width:100%">
          <option value="ALL">Lek (ALL)</option>
          <option value="EUR">Euro (EUR)</option>
        </select>
      </div>

      <div style="flex:1;min-width:160px">
        <label class="small">Shtesë (%)</label>
        <input id="surcharge" type="number" placeholder="0" value="0" onchange="recalc()">
        <div class="muted small">Shtesë e aplikueshme si % e totalit</div>
      </div>

      <div style="flex:1;min-width:160px">
        <label class="small">Mënyra pagesës</label>
        <select id="paymentMethod" onchange="recalc()" style="width:100%">
          <option value="cash_all">Cash (LEK)</option>
          <option value="card">Kartë</option>
          <option value="cash_eur">Cash (EUR)</option>
        </select>
      </div>
    </div>

    <div style="margin-top:10px">
      <button onclick="manualAdd()">➕ Shto</button>
      <button onclick="openCam('sale','environment')">📷 Mbrapa</button>
      <button onclick="openCam('sale','user')">🤳 Para</button>
    </div>
  </div>

  <div class="card">
    <table id="saleTable"></table>
    <h3>Total (ALL): <span id="tot">0</span> ALL</h3>
    <div id="totInEur" class="small" style="margin-bottom:6px"></div>

    <div class="loyalty-box">
      <b>Programi Loyal</b>
      <div id="loyaltyInfo" class="small">Vendos emrin ose telefonin e klientit për të parë pikët.</div>

      <div class="loyalty-balance">
        <label style="display:block">
          <input id="useLoyaltyPoints" type="checkbox" onchange="recalc()">
          Përdor pikët e klientit
        </label>
      </div>

      <div id="loyaltyDiscount" class="small" style="margin-top:8px"></div>
    </div>

    <div style="display:flex;gap:10px;align-items:center;flex-wrap:wrap;margin-top:12px">
      <input id="paid" type="number" placeholder="Shuma nga klienti" style="flex:1;min-width:180px">
      <div style="min-width:170px">
        <button onclick="pay()">Paguaj</button>
        <button class="secondary" onclick="cancel()">Anulo</button>
      </div>
    </div>

    <h3>Kusur / Mungesë: <span id="change">0</span></h3>
    <div class="small">Kusuri gjithmonë përllogaritet dhe shfaqet në Lek (ALL).</div>
  </div>
</section>

<section id="bil" class="admin">
  <div class="card">
    <h3>Bilanci Ditor</h3>
    <p>Sistemi (ALL): <b><span id="daily">0</span> ALL</b></p>
    <p>Sistemi (EUR): <b><span id="dailyEUR">0</span> EUR</b></p>
    <p>Arka reale (ALL): <input id="cashRealALL" type="number" placeholder="Shuma reale ALL" style="width:160px"></p>
    <p>Arka reale (EUR): <input id="cashRealEUR" type="number" placeholder="Shuma reale EUR" style="width:160px"></p>
    <p class="small">(Përllogaritja e ndryshes tregon dif. në secilën valutë.)</p>

    <div style="margin-top:10px">
      <label class="small">Kursi i këmbimit (1 EUR = ? ALL)</label>
      <input id="exchangeRateInput" type="number" step="0.01" placeholder="100" style="width:160px">
      <button onclick="saveExchangeRate()">Ruaj Kurs</button>
      <div class="small" style="margin-top:8px">
        <input id="forceDailyRate" type="checkbox"> Të kërkohet përditësimi i kursit çdo ditë
      </div>
    </div>

    <div style="margin-top:12px">
      <button onclick="closeDay()">Mbyll Ditën</button>
    </div>
  </div>
</section>

<section id="hist">
  <div class="card">
    <h3>Historiku i Shitjeve</h3>
    <div style="margin-bottom:10px">
      <button onclick="exportCSV()">⬇️ Eksporto CSV</button>
      <button class="secondary" onclick="clearOld()">🧹 Fshi të gjitha (lokal)</button>
    </div>
    <table id="histTable"></table>
  </div>
</section>

<section id="clients">
  <div class="card">
    <h3>Klientët Loyal</h3>
    <div class="row" style="margin-bottom:10px">
      <input id="clientSearch" class="col" placeholder="Kërko sipas emri ose telefoni">
      <button onclick="renderLoyaltyTable()">Kërko</button>
      <button class="secondary" onclick="resetClientFilter()">Pastro</button>
    </div>

    <div class="report-box">
      <div style="display:flex;gap:10px;flex-wrap:wrap">
        <button onclick="exportLoyaltyData()">⬇️ Eksporto Klientët</button>
        <button class="secondary" onclick="backupData()">💾 Backup JSON</button>
        <button class="secondary" onclick="restoreData()">📥 Restore JSON</button>
      </div>
    </div>

    <table id="loyaltyTable"></table>
  </div>
</section>

<section id="settings" class="admin">
  <div class="card">
    <h3>Cilësimet</h3>
    <p class="small">Ndrysho parametrat e riporositjes dhe kontrollit të skadencave.</p>

    <div class="row">
      <div class="col">
        <label class="small">LeadDays</label>
        <input id="cfg_leadDays" type="number" value="3">
      </div>
      <div class="col">
        <label class="small">ReviewDays</label>
        <input id="cfg_reviewDays" type="number" value="7">
      </div>
      <div class="col">
        <label class="small">Safety factor</label>
        <input id="cfg_safety" type="number" step="0.1" value="1.5">
      </div>
    </div>

    <div style="margin-top:10px">
      <button onclick="saveSettings()">Ruaj Cilësimet</button>
    </div>
  </div>
</section>

<div class="modal" id="alertsModal">
  <div class="modal-content">
    <h3>Alarmet e Inventarit</h3>
    <div id="alertsBody"></div>
    <div style="margin-top:12px;text-align:right">
      <button class="secondary" onclick="closeAlertsModal()">Mbyll</button>
    </div>
  </div>
</div>

<div class="modal" id="cam">
  <div class="modal-content">
    <h3>Scan Barcode</h3>
    <div id="scanner"></div>
    <div style="margin-top:12px;text-align:right">
      <button id="camCloseBtn" class="secondary">Mbyll</button>
    </div>
  </div>
</div>

<div class="modal" id="viewModal">
  <div class="modal-content">
    <h3>Detajet e Shitjes</h3>
    <div id="viewBody"></div>
    <div style="margin-top:12px">
      <input id="settleAmount" type="number" placeholder="Shuma për të shlyer (ALL)">
      <button onclick="settleDebt()">Shlyej Borxh</button>
      <button class="secondary" onclick="closeView()">Mbyll</button>
    </div>
  </div>
</div>

<div class="modal" id="txnModal">
  <div class="modal-content small-modal">
    <h4 id="txnTitle">Transaksioni</h4>
    <div id="txnMsg" class="small"></div>
    <div style="margin-top:12px;text-align:right">
      <button class="secondary" onclick="closeTxn()">Mbyll</button>
    </div>
  </div>
</div>

<script>
/* ========= SECURE HASH + USERS ========= */
function hashTextSync(value){
  const encoder = new TextEncoder();
  const data = encoder.encode(String(value));
  let hash = 0;
  for (let i = 0; i < data.length; i++) {
    hash = ((hash << 5) - hash + data[i]) >>> 0;
  }
  let hex = hash.toString(16);
  while (hex.length < 8) hex = '0' + hex;
  return hex;
}

async function sha256(value){
  const str = String(value);
  if (window.crypto && crypto.subtle && window.isSecureContext) {
    try{
      const utf8 = new TextEncoder().encode(str);
      const hashBuffer = await crypto.subtle.digest('SHA-256', utf8);
      const hashArray = Array.from(new Uint8Array(hashBuffer));
      return hashArray.map(b => b.toString(16).padStart(2,'0')).join('');
    }catch(e){}
  }
  return hashTextSync(str);
}

async function getStoredUsers(){
  const raw = localStorage.getItem('posUsers');
  if(!raw){
    const defaults = [
      { u:'admin', p: await sha256('admin'), r:'admin' },
      { u:'kasier', p: await sha256('kasier'), r:'kasier' }
    ];
    localStorage.setItem('posUsers', JSON.stringify(defaults));
    return defaults;
  }
  try{
    const parsed = JSON.parse(raw);
    return Array.isArray(parsed) ? parsed : [];
  }catch{
    return [];
  }
}

async function verifyLogin(username, password){
  const users = await getStoredUsers();
  const hashed = await sha256(password);
  return users.find(u => u.u === username && u.p === hashed) || null;
}

async function ensureDefaultUsers(){
  const raw = localStorage.getItem('posUsers');
  if(!raw){
    const defaults = [
      { u:'admin', p: await sha256('admin'), r:'admin' },
      { u:'kasier', p: await sha256('kasier'), r:'kasier' }
    ];
    localStorage.setItem('posUsers', JSON.stringify(defaults));
  }
}

/* ========= HELPERS ========= */
function safeParse(str, fallback){
  try { return JSON.parse(str); } catch (e) { return fallback; }
}
function safeNumber(value, fallback = 0){
  const n = Number(value);
  return Number.isFinite(n) ? n : fallback;
}
function round2(value){
  return Math.round((Number(value) || 0) * 100) / 100;
}
function escapeHtml(str){
  return String(str ?? '').replace(/[&<>"']/g, s => ({
    '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'
  }[s]));
}
function formatMoney(num){
  return round2(num).toFixed(2);
}
function getLocalDateStr(iso){
  const d = new Date(iso);
  return d.getFullYear() + '-' + String(d.getMonth()+1).padStart(2,'0') + '-' + String(d.getDate()).padStart(2,'0');
}
function daysBetween(a,b){
  return Math.ceil((b.getTime()-a.getTime())/(24*60*60*1000));
}
function normalizeLoyaltyValue(value){
  return String(value || '').trim().toLowerCase().replace(/\s+/g, ' ');
}
function stableString(value){
  return String(value ?? '').trim();
}

/* ========= STATE ========= */
let role = 'guest';
let products = safeParse(localStorage.getItem('p'), []);
let sales = [];
let salesHistory = safeParse(localStorage.getItem('salesHistory'), []);
let daily = safeNumber(localStorage.getItem('daily'), 0);
let eurInRegister = safeNumber(localStorage.getItem('eurInRegister'), 0);

let reorderConfig = safeParse(localStorage.getItem('reorderCfg'), {
  leadDays:3,
  reviewPeriodDays:7,
  safetyStockFactor:1.5,
  minOrderQty:1
});

let exchangeRate = safeNumber(localStorage.getItem('exchangeRate'), 100.00);
let forceDailyRate = localStorage.getItem('forceDailyRate') === '1';

let loyaltyCustomers = safeParse(localStorage.getItem('loyaltyCustomers'), {});
const POINTS_PER_ALL = 100;
const ALL_PER_POINT = 1;

let scanTarget = null;
let camMode = 'environment';
let quaggaHandler = null;
let quaggaRunning = false;
let quaggaDebounce = false;

/* ========= ELEMENTS ========= */
const alertCountEl = document.getElementById('alertCount');
const alertsModal = document.getElementById('alertsModal');
const alertsBody = document.getElementById('alertsBody');
const camEl = document.getElementById('cam');
const scannerEl = document.getElementById('scanner');
const camCloseBtn = document.getElementById('camCloseBtn');
const saleScanEl = document.getElementById('saleScan');
const paidEl = document.getElementById('paid');
const totEl = document.getElementById('tot');
const totInEurEl = document.getElementById('totInEur');
const changeEl = document.getElementById('change');
const prodTableEl = document.getElementById('prodTable');
const saleTableEl = document.getElementById('saleTable');
const histTableEl = document.getElementById('histTable');
const loyalTableEl = document.getElementById('loyaltyTable');
const dailyEl = document.getElementById('daily');
const dailyEurEl = document.getElementById('dailyEUR');
const cashRealALLEl = document.getElementById('cashRealALL');
const cashRealEUREl = document.getElementById('cashRealEUR');
const exchangeRateInput = document.getElementById('exchangeRateInput');
const forceDailyRateEl = document.getElementById('forceDailyRate');
const viewModalEl = document.getElementById('viewModal');
const settleAmountEl = document.getElementById('settleAmount');
const txnModalEl = document.getElementById('txnModal');
const txnMsgEl = document.getElementById('txnMsg');
const txnTitleEl = document.getElementById('txnTitle');

const uEl = document.getElementById('u');
const pEl = document.getElementById('p');
const msgEl = document.getElementById('msg');
const clientEl = document.getElementById('client');
const clientPhoneEl = document.getElementById('clientPhone');
const loyaltyInfoEl = document.getElementById('loyaltyInfo');
const useLoyaltyPointsEl = document.getElementById('useLoyaltyPoints');
const loyaltyDiscountEl = document.getElementById('loyaltyDiscount');
const statsGridEl = document.getElementById('statsGrid');
const clientSearchEl = document.getElementById('clientSearch');

function sanitizeProduct(obj){
  if(!obj || typeof obj !== 'object') return null;
  return {
    n: stableString(obj.n || 'Pa emër'),
    b: stableString(obj.b || ''),
    p: Math.max(0, safeNumber(obj.p, 0)),
    s: Math.max(0, safeNumber(obj.s, 0)),
    category: obj.category || 'ushqim',
    expiry: obj.expiry || '',
    minStock: Math.max(0, safeNumber(obj.minStock, 0))
  };
}

function normalizeProducts(){
  products = products.map(sanitizeProduct).filter(Boolean);
  localStorage.setItem('p', JSON.stringify(products));
}

/* ========= AUTH ========= */
async function doLogin(){
  const username = (uEl.value || '').trim();
  const password = (pEl.value || '').trim();
  if(!username || !password){ msgEl.textContent = 'Shkruaj user dhe password'; return; }

  await ensureDefaultUsers();
  const user = await verifyLogin(username, password);
  if(!user){ msgEl.textContent = 'Gabim login'; return; }

  role = user.r;
  document.getElementById('loginSec').style.display = 'none';
  document.getElementById('menu').style.display = 'block';
  document.querySelectorAll('.admin').forEach(el => {
    el.style.display = role === 'admin' ? 'inline-block' : 'none';
  });

  openSec('sale');
  normalizeProducts();
  renderProducts();
  renderHistory();
  renderStats();
  renderLoyaltyTable();
  checkAlerts();
}

function logout(){ location.reload(); }
function openSec(id){
  document.querySelectorAll('section').forEach(s => s.classList.remove('active'));
  const target = document.getElementById(id);
  if(target) target.classList.add('active');
}

/* ========= DASHBOARD ========= */
function renderStats(){
  const todayDate = getLocalDateStr(new Date().toISOString());
  const todaySales = salesHistory.filter(r => getLocalDateStr(r.timestamp) === todayDate);
  const totalToday = todaySales.reduce((sum, r) => sum + Number(r.totalAll || 0), 0);
  const totalProducts = products.length;
  const lowStock = products.filter(p => Number(p.s || 0) <= Number(p.minStock || 0)).length;
  const expired = products.filter(p => {
    if(!p.expiry) return false;
    const expDate = new Date(p.expiry + 'T23:59:59');
    return expDate < new Date();
  }).length;

  statsGridEl.innerHTML = [
    { label:'Shitjet e sotme', value:`${formatMoney(totalToday)} ALL` },
    { label:'Produkte', value:String(totalProducts) },
    { label:'Low stock', value:String(lowStock) },
    { label:'Skaduar', value:String(expired) }
  ].map(s => `
    <div class="stat-box">
      <div class="stat-label">${s.label}</div>
      <div class="stat-value">${s.value}</div>
    </div>
  `).join('');
}

/* ========= PRODUCTS ========= */
function storeProducts(){
  normalizeProducts();
  renderProducts();
  renderStats();
  checkAlerts();
}

function addProduct(){
  const obj = {
    n: stableString(document.getElementById('pn').value || 'Pa emër'),
    b: stableString(document.getElementById('pb').value || ''),
    p: safeNumber(document.getElementById('pp').value, 0),
    s: safeNumber(document.getElementById('ps').value, 0),
    category: document.getElementById('pcat').value || 'ushqim',
    expiry: document.getElementById('pexp').value || '',
    minStock: safeNumber(document.getElementById('pmin').value, 0)
  };

  if(!obj.b){ alert('Barkodi është i kërkuar.'); return; }
  if(obj.p < 0 || obj.s < 0 || obj.minStock < 0){ alert('Çmimi, sasia dhe min stock duhet të jenë pozitive ose zero.'); return; }

  const duplicate = products.some(item => String(item.b).trim() === String(obj.b).trim());
  if(duplicate){ alert('Barkodi ekziston tashmë.'); return; }

  products.push(obj);
  storeProducts();

  document.getElementById('pn').value = '';
  document.getElementById('pb').value = '';
  document.getElementById('pp').value = '';
  document.getElementById('ps').value = '';
  document.getElementById('pexp').value = '';
  document.getElementById('pmin').value = '';
  document.getElementById('pcat').value = 'ushqim';
}

function renderProducts(){
  prodTableEl.innerHTML = `
    <tr>
      <th>Emër</th><th>Barkod</th><th>Çmim (ALL)</th><th>Stok</th><th>MinStock</th>
      <th>Kategori</th><th>Skadenca</th><th>Alarm</th><th>❌</th>
    </tr>
  `;

  const today = new Date();
  products.forEach((p,i)=>{
    let alarmHtml = '';
    let rowClass = '';

    if(p.expiry){
      const expDate = new Date(p.expiry + 'T23:59:59');
      if(expDate < today){
        alarmHtml += `<span class="danger-text" title="Skaduar">Skaduar</span>`;
        rowClass = 'expired';
      } else {
        const days = daysBetween(today, expDate);
        if(days <= 7){
          alarmHtml += `<span class="warn" title="Skadon brenda ${days} ditëve">Skadon (${days}d)</span>`;
          if(!rowClass) rowClass = 'expiring';
        }
      }
    }

    if(Number(p.s || 0) <= Number(p.minStock || 0)){
      alarmHtml += (alarmHtml ? ' • ' : '') + `<span class="danger-text" title="Stock i ulët">Stock i ulët</span>`;
      rowClass = rowClass || 'lowstock';
    }

    prodTableEl.innerHTML += `
      <tr class="${rowClass || ''}">
        <td><input value="${escapeHtml(p.n || '')}" onchange="products[${i}].n=this.value;storeProducts()"></td>
        <td><input value="${escapeHtml(p.b || '')}" onchange="products[${i}].b=this.value.trim();storeProducts()"></td>
        <td><input type="number" value="${Number(p.p || 0)}" onchange="products[${i}].p=Math.max(0,safeNumber(this.value,0));storeProducts()"></td>
        <td><input type="number" value="${Number(p.s || 0)}" onchange="products[${i}].s=Math.max(0,safeNumber(this.value,0));storeProducts()"></td>
        <td><input type="number" value="${Number(p.minStock || 0)}" onchange="products[${i}].minStock=Math.max(0,safeNumber(this.value,0));storeProducts()"></td>
        <td>
          <select onchange="products[${i}].category=this.value;storeProducts()" class="category-select">
            <option value="ushqim" ${p.category === 'ushqim' ? 'selected' : ''}>Ushqim</option>
            <option value="pije" ${p.category === 'pije' ? 'selected' : ''}>Pije</option>
            <option value="higjienike" ${p.category === 'higjienike' ? 'selected' : ''}>Higjenike</option>
          </select>
        </td>
        <td><input type="date" value="${p.expiry || ''}" onchange="products[${i}].expiry=this.value;storeProducts()"></td>
        <td>${alarmHtml || '<span class=\"muted\">—</span>'}</td>
        <td><button class="danger" onclick="products.splice(${i},1);storeProducts();">🗑️</button></td>
      </tr>
    `;
  });
}

/* ========= ALERTS ========= */
function checkAlerts(){
  const alerts = [];
  const today = new Date();

  products.forEach(p=>{
    if(Number(p.s || 0) <= Number(p.minStock || 0)){
      alerts.push({ type:'lowstock', product:p, msg:`Stoku i produktit "${p.n}" (barkod: ${p.b}) është në/poshtë minStock (${p.s} ≤ ${p.minStock}).` });
    }
    if(p.expiry){
      const expDate = new Date(p.expiry + 'T23:59:59');
      const days = daysBetween(today, expDate);
      if(expDate < today){
        alerts.push({ type:'expired', product:p, msg:`Produkti "${p.n}" (barkod: ${p.b}) ka skaduar më ${p.expiry}.` });
      } else if(days <= 7){
        alerts.push({ type:'expiring', product:p, msg:`Produkti "${p.n}" (barkod: ${p.b}) skadon në ${days} ditë (${p.expiry}).` });
      }
    }
  });

  alertCountEl.textContent = alerts.length;
  window.lastInventoryAlerts = alerts;
  return alerts;
}

function openAlertsModal(){
  const alerts = checkAlerts();
  alertsBody.innerHTML = '';
  if(!alerts.length){
    alertsBody.innerHTML = '<div>Nuk ka alarme.</div>';
    alertsModal.style.display = 'block';
    return;
  }

  let html = '<ul>';
  alerts.forEach(a=>{
    const barcode = String((a.product && a.product.b) || '');
    html += `<li><b>${escapeHtml(a.type.toUpperCase())}</b>: ${escapeHtml(a.msg)} <button style="margin-left:8px" onclick="openProdAndHighlight('${escapeHtml(barcode)}')">Shiko</button></li>`;
  });
  html += '</ul>';
  alertsBody.innerHTML = html;
  alertsModal.style.display = 'block';
}
function closeAlertsModal(){ alertsModal.style.display = 'none'; }
function openProdAndHighlight(barcode){
  closeAlertsModal();
  openSec('prod');
  setTimeout(()=>{
    renderProducts();
    const rows = prodTableEl.querySelectorAll('tr');
    for(const r of rows){
      if(r.innerText.includes(barcode)){
        r.style.transition = 'background 0.3s';
        r.style.background = '#fffbeb';
        setTimeout(()=>r.style.background='',2500);
        r.scrollIntoView({ behavior:'smooth', block:'center' });
        break;
      }
    }
  }, 200);
}

/* ========= LOYALTY ========= */
function getLoyaltyKey(){
  const name = normalizeLoyaltyValue(clientEl.value);
  const phone = normalizeLoyaltyValue(clientPhoneEl.value);
  if(!name && !phone) return '';
  return `${name}|${phone}`;
}

function getLoyaltyCustomer(){
  const key = getLoyaltyKey();
  if(!key) return null;
  if(!loyaltyCustomers[key]){
    loyaltyCustomers[key] = {
      key,
      name: stableString(clientEl.value),
      phone: stableString(clientPhoneEl.value),
      points: 0,
      totalSpentALL: 0,
      transactions: 0,
      createdAt: new Date().toISOString(),
      updatedAt: new Date().toISOString()
    };
  }
  return loyaltyCustomers[key];
}

function saveLoyaltyCustomers(){
  localStorage.setItem('loyaltyCustomers', JSON.stringify(loyaltyCustomers));
}

function calculateEarnedPoints(amountPaidALL){
  return Math.floor(Math.max(0, amountPaidALL) / POINTS_PER_ALL);
}

function calculateLoyaltyDiscount(totalBeforeDiscount){
  if(!useLoyaltyPointsEl.checked) return { discountALL:0, pointsUsed:0 };
  const customer = getLoyaltyCustomer();
  if(!customer || customer.points <= 0) return { discountALL:0, pointsUsed:0 };
  const maximumDiscount = customer.points * ALL_PER_POINT;
  const discountALL = Math.min(maximumDiscount, totalBeforeDiscount);
  const pointsUsed = Math.ceil(discountALL / ALL_PER_POINT);
  return { discountALL: round2(discountALL), pointsUsed };
}

function refreshLoyaltyUI(){
  const key = getLoyaltyKey();
  if(!key){
    loyaltyInfoEl.innerHTML = 'Vendos emrin ose telefonin e klientit për të parë pikët.';
    loyaltyDiscountEl.textContent = '';
    useLoyaltyPointsEl.checked = false;
    useLoyaltyPointsEl.disabled = true;
    recalc();
    return;
  }

  const customer = getLoyaltyCustomer();
  loyaltyInfoEl.innerHTML = `Klienti ka: <span class="loyalty-positive">${customer.points} pikë</span><br>Vlera e pikëve: <b>${formatMoney(customer.points * ALL_PER_POINT)} ALL</b>`;

  if(customer.points <= 0){
    useLoyaltyPointsEl.checked = false;
    useLoyaltyPointsEl.disabled = true;
    loyaltyDiscountEl.textContent = 'Klienti nuk ka pikë për përdorim.';
  } else {
    useLoyaltyPointsEl.disabled = false;
    loyaltyDiscountEl.textContent = `Mund të përdorë deri në ${formatMoney(customer.points * ALL_PER_POINT)} ALL zbritje.`;
  }

  recalc();
}

function updateLoyaltyAfterPayment(record){
  const key = getLoyaltyKey();
  if(!key) return;
  const customer = getLoyaltyCustomer();
  if(!customer) return;

  const pointsUsed = record.loyaltyPointsUsed || 0;
  const earnedPoints = calculateEarnedPoints(record.amountPaid);

  customer.points = Math.max(0, customer.points - pointsUsed + earnedPoints);
  customer.totalSpentALL += record.amountPaid;
  customer.transactions += 1;
  customer.updatedAt = new Date().toISOString();

  saveLoyaltyCustomers();

  record.loyaltyPointsEarned = earnedPoints;
  record.loyaltyBalanceAfter = customer.points;
}

/* ========= CUSTOMER TABLE ========= */
function getAllLoyaltyCustomers(){
  return Object.values(loyaltyCustomers || {}).sort((a,b) => (Number(b.points)||0) - (Number(a.points)||0));
}

function renderLoyaltyTable(){
  const search = normalizeLoyaltyValue(clientSearchEl.value);
  const rows = getAllLoyaltyCustomers().filter(c => {
    if(!search) return true;
    const hay = normalizeLoyaltyValue(`${c.name || ''} ${c.phone || ''}`);
    return hay.includes(search);
  });

  loyalTableEl.innerHTML = `
    <tr>
      <th>Emri</th>
      <th>Telefoni</th>
      <th>Pikë</th>
      <th>Vlera ALL</th>
      <th>Shpenzuar</th>
      <th>Transaksione</th>
      <th>Veprime</th>
    </tr>
  `;

  rows.forEach(c => {
    const tr = document.createElement('tr');
    const cells = [
      ['td', c.name || '--'],
      ['td', c.phone || '--'],
      ['td', String(Number(c.points || 0))],
      ['td', `${formatMoney(Number(c.points || 0) * ALL_PER_POINT)} ALL`],
      ['td', `${formatMoney(Number(c.totalSpentALL || 0))} ALL`],
      ['td', String(Number(c.transactions || 0))]
    ];

    cells.forEach(([tag, value]) => {
      const td = document.createElement(tag);
      td.textContent = value;
      tr.appendChild(td);
    });

    const act = document.createElement('td');
    const btn = document.createElement('button');
    btn.textContent = 'Zgjidh';
    btn.addEventListener('click', () => applyCustomerToSale(c.name || '', c.phone || ''));
    act.appendChild(btn);
    tr.appendChild(act);

    loyalTableEl.appendChild(tr);
  });

  if(!rows.length){
    loyalTableEl.innerHTML += `<tr><td colspan="7" class="muted">Nuk u gjet asnjë klient.</td></tr>`;
  }
}

function applyCustomerToSale(name, phone){
  clientEl.value = name || '';
  clientPhoneEl.value = phone || '';
  refreshLoyaltyUI();
  openSec('sale');
}

function resetClientFilter(){
  clientSearchEl.value = '';
  renderLoyaltyTable();
}

function exportLoyaltyData(){
  const rows = getAllLoyaltyCustomers();
  if(!rows.length){
    alert('Nuk ka klientë për eksport.');
    return;
  }

  const csv = [
    ['name','phone','points','totalSpentALL','transactions'],
    ...rows.map(c => [c.name || '', c.phone || '', Number(c.points || 0), Number(c.totalSpentALL || 0), Number(c.transactions || 0)])
  ].map(r => r.map(v => `"${String(v).replace(/"/g, '""')}"`).join(',')).join('\n');

  const blob = new Blob([csv], { type:'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'loyalty_customers.csv';
  a.click();
  URL.revokeObjectURL(url);
}

function backupData(){
  const backup = {
    products,
    salesHistory,
    daily,
    eurInRegister,
    exchangeRate,
    forceDailyRate,
    loyaltyCustomers,
    reorderConfig
  };

  const blob = new Blob([JSON.stringify(backup, null, 2)], { type:'application/json' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'pos_market_backup.json';
  a.click();
  URL.revokeObjectURL(url);
}

function restoreData(){
  const input = document.createElement('input');
  input.type = 'file';
  input.accept = 'application/json';
  input.onchange = function(e){
    const file = e.target.files[0];
    if(!file) return;
    const reader = new FileReader();
    reader.onload = function(ev){
      try{
        const data = JSON.parse(ev.target.result);
        if(data.products) products = data.products.map(sanitizeProduct).filter(Boolean);
        if(data.salesHistory) salesHistory = data.salesHistory;
        if(data.daily !== undefined) daily = safeNumber(data.daily, 0);
        if(data.eurInRegister !== undefined) eurInRegister = safeNumber(data.eurInRegister, 0);
        if(data.exchangeRate !== undefined) exchangeRate = safeNumber(data.exchangeRate, 100);
        if(data.forceDailyRate !== undefined) forceDailyRate = !!data.forceDailyRate;
        if(data.loyaltyCustomers) loyaltyCustomers = data.loyaltyCustomers;
        if(data.reorderConfig) reorderConfig = { ...reorderConfig, ...data.reorderConfig };

        localStorage.setItem('p', JSON.stringify(products));
        localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
        localStorage.setItem('daily', String(daily));
        localStorage.setItem('eurInRegister', String(eurInRegister));
        localStorage.setItem('exchangeRate', String(exchangeRate));
        localStorage.setItem('forceDailyRate', forceDailyRate ? '1' : '0');
        localStorage.setItem('loyaltyCustomers', JSON.stringify(loyaltyCustomers));
        localStorage.setItem('reorderCfg', JSON.stringify(reorderConfig));

        renderProducts();
        renderHistory();
        renderStats();
        renderLoyaltyTable();
        updateDaily();
        refreshLoyaltyUI();
        alert('Backup u restaurua me sukses.');
      } catch(err){
        alert('Backup i pavlefshëm ose i dëmtuar.');
      }
    };
    reader.readAsText(file);
  };
  input.click();
}

/* ========= SALES ========= */
function getCurrentSaleTotals(){
  let subtotalALL = 0;
  sales.forEach(x => subtotalALL += Number(x.q || 0) * Number(x.p || 0));

  const surchargePct = Math.max(0, safeNumber(document.getElementById('surcharge').value, 0));
  const surchargeAmount = round2(subtotalALL * (surchargePct / 100));
  const totalBeforeDiscount = round2(subtotalALL + surchargeAmount);

  const loyalty = calculateLoyaltyDiscount(totalBeforeDiscount);
  const totalAll = round2(Math.max(0, totalBeforeDiscount - loyalty.discountALL));

  return {
    subtotalALL: round2(subtotalALL),
    surchargePct,
    surchargeAmount,
    totalBeforeDiscount,
    loyalty,
    totalAll
  };
}

function addToSale(p){
  if(!p) return;
  if(Number(p.s || 0) < 1) return alert('Stoku = 0');

  const item = sales.find(x => x.b === p.b);
  if(item){
    if(item.q + 1 > Number(p.s || 0)) return alert('Sasia tejkalon stoqen');
    item.q++;
  } else {
    sales.push({ b:p.b, n:p.n, p: safeNumber(p.p,0), q:1 });
  }
  drawSale();
}

function manualAdd(){
  const v = (saleScanEl.value || '').trim().toLowerCase();
  if(!v) return;

  const product = products.find(x => {
    const barcode = String(x.b || '').toLowerCase();
    const name = String(x.n || '').toLowerCase();
    return barcode === v || name.includes(v);
  });

  if(!product) return alert('Nuk u gjet produkti');

  addToSale(product);
  saleScanEl.value = '';
  saleScanEl.focus();
}
saleScanEl.addEventListener('keydown', e => { if(e.key === 'Enter') manualAdd(); });

function drawSale(){
  saleTableEl.innerHTML = '<tr><th>Produkt</th><th>Sasi</th><th>Çmim (ALL)</th><th>Total (ALL)</th><th></th></tr>';
  sales.forEach((x,i)=>{
    saleTableEl.innerHTML += `
      <tr>
        <td>${escapeHtml(x.n)}</td>
        <td>
          <button class="qtyBtn" onclick="changeQty(${i},-1)">➖</button>
          ${x.q}
          <button class="qtyBtn" onclick="changeQty(${i},1)">➕</button>
        </td>
        <td>${formatMoney(x.p)}</td>
        <td>${formatMoney(x.q * x.p)}</td>
        <td><button class="danger" onclick="sales.splice(${i},1);drawSale();">🗑️</button></td>
      </tr>
    `;
  });
  recalc();
}

function changeQty(i, delta){
  const item = sales[i];
  if(!item) return;

  const product = products.find(p => p.b === item.b);
  item.q += delta;

  if(item.q < 1){
    sales.splice(i,1);
  } else if(product && item.q > Number(product.s || 0)){
    item.q = Number(product.s || 0);
    alert('Sasia tejkalon stoqen');
  }

  drawSale();
}

function recalc(){
  const totals = getCurrentSaleTotals();
  const totalAll = totals.totalAll;

  totEl.textContent = totalAll.toFixed(2);

  if(totals.loyalty.discountALL > 0){
    loyaltyDiscountEl.innerHTML = `<span class="loyalty-positive">Zbritje nga pikët: -${formatMoney(totals.loyalty.discountALL)} ALL</span>`;
  } else {
    loyaltyDiscountEl.textContent = useLoyaltyPointsEl.checked ? 'Nuk ka pikë të mjaftueshme për këtë total.' : '';
  }

  const saleCurrency = document.getElementById('saleCurrency').value;
  if(saleCurrency === 'EUR'){
    const totalEur = round2(totalAll / exchangeRate);
    totInEurEl.innerHTML = `Total (EUR): <b>${totalEur.toFixed(2)}</b> EUR (kursi: 1 EUR = ${exchangeRate} ALL)`;
  } else {
    totInEurEl.innerHTML = '';
  }

  const paymentMethod = document.getElementById('paymentMethod').value;
  const paidRaw = safeNumber(paidEl.value, 0);
  let paidAllEquivalent = 0;

  if(paymentMethod === 'cash_eur'){
    paidAllEquivalent = round2(paidRaw * exchangeRate);
  } else {
    paidAllEquivalent = paidRaw;
  }

  const diff = round2(paidAllEquivalent - totalAll);
  if(diff < 0){
    changeEl.textContent = `Mungojnë ${Math.abs(diff).toFixed(2)} ALL`;
    changeEl.style.color = 'red';
  } else {
    changeEl.textContent = `Kusur ${diff.toFixed(2)} ALL`;
    changeEl.style.color = 'green';
  }
}

paidEl.addEventListener('input', recalc);
clientEl.addEventListener('input', refreshLoyaltyUI);
clientPhoneEl.addEventListener('input', refreshLoyaltyUI);
clientSearchEl.addEventListener('input', renderLoyaltyTable);

/* ========= CAMERA ========= */
camCloseBtn.addEventListener('click', stopCam);
camEl.addEventListener('click', e => { if(e.target === camEl) stopCam(); });
document.addEventListener('keydown', e => {
  if(e.key === 'Escape'){
    if(camEl.style.display === 'block') stopCam();
    if(viewModalEl.style.display === 'block') closeView();
    if(txnModalEl.style.display === 'block') closeTxn();
  }
});

function openCam(target, mode){
  scanTarget = target;
  camMode = mode;
  camEl.style.display = 'block';
  stopCam();

  if(!window.Quagga){
    alert('Quagga nuk u gjet');
    camEl.style.display = 'none';
    return;
  }

  Quagga.init({
    inputStream:{ type:'LiveStream', target: scannerEl, constraints:{ facingMode:{ ideal:mode }, width:{ ideal:640 }, height:{ ideal:480 } } },
    locator:{ patchSize:'medium', halfSample:true },
    decoder:{ readers:['ean_reader','ean_8_reader','code_128_reader','upc_reader'] },
    locate:true
  }, err=>{
    if(err){
      alert('Kamera nuk u hap: ' + (err.message || err));
      camEl.style.display = 'none';
      return;
    }

    try{ Quagga.start(); quaggaRunning = true; }catch(e){
      alert('Gabim duke nisur kamerën: ' + (e.message || e));
      camEl.style.display = 'none';
      return;
    }

    quaggaHandler = function(d){
      if(quaggaDebounce) return;
      quaggaDebounce = true; setTimeout(()=>quaggaDebounce = false, 600);

      const code = d && d.codeResult && (d.codeResult.code || d.codeResult.codeResult);
      if(!code) return;

      if(scanTarget === 'stock'){
        document.getElementById('pb').value = code;
      } else if(scanTarget === 'sale'){
        const p = products.find(x => String(x.b).trim() === String(code).trim());
        if(p) addToSale(p);
        else alert('Barkodi nuk u gjet: ' + code);
      }

      setTimeout(stopCam, 300);
    };

    try{ Quagga.onDetected(quaggaHandler); }catch(e){ try{ Quagga.on('detected', quaggaHandler); }catch(e){} }
  });
}

function stopCam(){
  camEl.style.display = 'none';
  try{
    if(quaggaHandler && window.Quagga){
      try{ Quagga.offDetected(quaggaHandler); }catch(e){ try{ Quagga.off('detected', quaggaHandler); }catch(e){} }
    }
  }catch(e){}
  try{ if(window.Quagga && quaggaRunning) Quagga.stop(); }catch(e){}
  quaggaHandler = null;
  quaggaRunning = false;
}

/* ========= PRINT RECEIPT ========= */
function buildReceiptText(record){
  const rows = record.items.map(it => `${it.n} x${it.q} = ${formatMoney(it.q * it.p)} ALL`).join('\n');
  const loyaltyLine = record.loyaltyDiscountALL > 0 ? `Zbritje pikë: -${formatMoney(record.loyaltyDiscountALL)} ALL\n` : '';
  return `
POS MARKET
-------------------------
Data: ${new Date(record.timestamp).toLocaleString('sq-AL')}
Klient: ${record.client || '--'}
Telefoni: ${record.clientPhone || '--'}
-------------------------
${rows}
-------------------------
Subtotal: ${formatMoney(record.subtotalAll)} ALL
Shtesë: ${formatMoney(record.surchargePct)}%
${loyaltyLine}Total: ${formatMoney(record.totalAll)} ALL
Paguar: ${formatMoney(record.amountPaid)} ALL
Kusur: ${formatMoney(record.changeALL)} ALL
Status: ${record.status}
-------------------------
`;
}

function printReceipt(record){
  const printWindow = window.open('', '_blank', 'width=400,height=700');
  if(!printWindow) return;

  printWindow.document.write(`
    <html>
      <head>
        <title>Receipt</title>
        <style>
          body{font-family:monospace;padding:20px;font-size:12px;line-height:1.5;color:#111}
          .box{white-space:pre-wrap}
        </style>
      </head>
      <body>
        <div class="box">${escapeHtml(buildReceiptText(record))}</div>
        <script>window.print(); setTimeout(()=>window.close(), 500);</script>
      </body>
    </html>
  `);
}

/* ========= PAYMENTS + HISTORY ========= */
function pay(){
  if(sales.length === 0){
    alert('Shporta është bosh');
    return;
  }

  const totalAll = round2(Number(totEl.textContent) || 0);
  const cashInput = safeNumber(paidEl.value, 0);

  if(cashInput <= 0){
    alert('Shuma e paguar duhet të jetë më e madhe se 0');
    return;
  }

  const paymentMethod = document.getElementById('paymentMethod').value;
  let cashGivenRaw = cashInput;
  let cashGivenALL = 0;
  let paymentCurrency = 'ALL';

  if(paymentMethod === 'cash_eur'){
    paymentCurrency = 'EUR';
    cashGivenALL = round2(cashGivenRaw * exchangeRate);
  } else {
    paymentCurrency = 'ALL';
    cashGivenALL = round2(cashGivenRaw);
  }

  const subtotalALL = sales.reduce((sum, item) => sum + Number(item.q || 0) * Number(item.p || 0), 0);
  const surchargePct = Math.max(0, safeNumber(document.getElementById('surcharge').value, 0));
  const surchargeAmount = round2(subtotalALL * (surchargePct / 100));
  const totalBeforeDiscount = round2(subtotalALL + surchargeAmount);

  const loyalty = calculateLoyaltyDiscount(totalBeforeDiscount);
  const loyaltyPointsUsed = loyalty.pointsUsed || 0;

  const netCollectedALL = Math.min(cashGivenALL, totalAll);
  const changeALL = Math.max(0, cashGivenALL - totalAll);
  const due = Math.max(0, totalAll - cashGivenALL);
  const status = cashGivenALL >= totalAll ? 'paid' : 'owed';

  for(const item of sales){
    const prod = products.find(p => p.b === item.b);
    if(prod) prod.s = Math.max(0, Number(prod.s || 0) - Number(item.q || 0));
  }
  storeProducts();

  const timestamp = new Date().toISOString();
  const record = {
    id: timestamp + '_' + Math.random().toString(36).slice(2,7),
    timestamp,
    client: (clientEl.value || '').trim() || null,
    clientPhone: (clientPhoneEl.value || '').trim() || null,
    items: JSON.parse(JSON.stringify(sales)),
    subtotalAll: round2(subtotalALL),
    surchargePct: round2(surchargePct),
    loyaltyDiscountALL: round2(loyalty.discountALL || 0),
    loyaltyPointsUsed,
    totalBeforeLoyaltyDiscount: round2(totalBeforeDiscount),
    totalAll,
    paymentMethod,
    paymentCurrency,
    cashGivenRaw: round2(cashGivenRaw),
    cashGivenALL: round2(cashGivenALL),
    changeALL: round2(changeALL),
    amountPaid: round2(netCollectedALL),
    due: round2(due),
    status,
    loyaltyPointsEarned: 0,
    loyaltyBalanceAfter: 0
  };

  updateLoyaltyAfterPayment(record);

  salesHistory.unshift(record);
  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
  renderStats();

  daily += record.amountPaid;
  localStorage.setItem('daily', String(daily));

  if(paymentCurrency === 'EUR'){
    const netEur = round2(Math.min(cashGivenALL, totalAll) / exchangeRate);
    eurInRegister += netEur;
    localStorage.setItem('eurInRegister', String(round2(eurInRegister)));
  }

  cancel();
  updateDaily();
  renderHistory();

  printReceipt(record);

  let html = '';
  html += status === 'paid' ? `<div class="success">Transaksioni u mbyll me sukses</div>` : `<div class="warn">Shitja u regjistrua si BORXH</div>`;
  html += `<div><b>Produkte:</b><ul class="txn-list">${record.items.map(it => `<li>${escapeHtml(it.n)} x${it.q} = ${it.q*it.p} ALL</li>`).join('')}</ul></div>`;
  html += `<div class="txn-summary">Total (ALL): ${record.totalAll} ALL</div>`;
  if(record.loyaltyDiscountALL > 0){
    html += `<div class="success">Zbritje nga pikët: -${record.loyaltyDiscountALL} ALL</div>`;
  }
  html += `<div>Klienti dha: ${record.cashGivenRaw} ${record.paymentCurrency}</div>`;
  html += `<div>Kusur (ALL): ${record.changeALL}</div>`;
  html += `<div class="small">Shuma e shtuar në arkë (neto, ALL): ${record.amountPaid} ALL</div>`;
  if(record.paymentCurrency === 'EUR'){
    html += `<div class="small">Euro të mbledhura (neto): ${round2(record.amountPaid / exchangeRate)} EUR</div>`;
  }

  txnTitleEl.textContent = status === 'paid' ? 'Shitje e plotë' : 'Shitje me borxh';
  showTxn(html);
}

function cancel(){
  sales = [];
  saleTableEl.innerHTML = '';
  totEl.textContent = '0';
  totInEurEl.innerHTML = '';
  paidEl.value = '';
  changeEl.textContent = '0';
  changeEl.style.color = '';
  clientEl.value = '';
  clientPhoneEl.value = '';
  useLoyaltyPointsEl.checked = false;
  useLoyaltyPointsEl.disabled = false;
  loyaltyInfoEl.textContent = 'Vendos emrin ose telefonin e klientit për të parë pikët.';
  loyaltyDiscountEl.textContent = '';
  document.getElementById('surcharge').value = 0;
  recalc();
}

/* ========= HISTORY ========= */
function renderHistory(){
  histTableEl.innerHTML = `
    <tr>
      <th>Data</th><th>Klient</th><th>Telefon</th><th>Total(ALL)</th><th>Paguar(ALL)</th>
      <th>Paguar/Valutë</th><th>Pikë</th><th>Mbetje</th><th>Status</th><th>Veprime</th>
    </tr>
  `;

  salesHistory.forEach(rec=>{
    histTableEl.innerHTML += `
      <tr>
        <td>${String(rec.timestamp || '').replace('T',' ').slice(0,19)}</td>
        <td>${escapeHtml(rec.client || '--')}</td>
        <td>${escapeHtml(rec.clientPhone || '--')}</td>
        <td>${formatMoney(rec.totalAll)}</td>
        <td>${formatMoney(rec.amountPaid)}</td>
        <td>${rec.cashGivenRaw} ${rec.paymentCurrency} (${rec.paymentMethod})</td>
        <td>${rec.loyaltyPointsEarned || 0}</td>
        <td>${formatMoney(rec.due)}</td>
        <td>${escapeHtml(rec.status)}</td>
        <td>
          <button onclick='viewSale(${JSON.stringify(rec.id)})'>Shiko</button>
          <button class="danger" onclick='deleteSale(${JSON.stringify(rec.id)})'>🗑️</button>
        </td>
      </tr>
    `;
  });
}

function viewSale(id){
  const r = salesHistory.find(x => x.id === id);
  if(!r) return alert('Nuk u gjet shitja');

  const body = document.getElementById('viewBody');
  let html = `<p><b>Data:</b> ${String(r.timestamp || '').replace('T',' ').slice(0,19)}</p>`;
  html += `<p><b>Klient:</b> ${escapeHtml(r.client || '--')}</p>`;
  html += `<p><b>Telefon:</b> ${escapeHtml(r.clientPhone || '--')}</p>`;
  html += `<p><b>Subtotal:</b> ${formatMoney(r.subtotalAll)} ALL</p>`;
  html += `<p><b>Surcharge (%):</b> ${r.surchargePct}</p>`;
  html += `<p><b>Zbritje nga pikët:</b> ${formatMoney(r.loyaltyDiscountALL || 0)} ALL</p>`;
  html += `<p><b>Pikë të përdorura:</b> ${r.loyaltyPointsUsed || 0}</p>`;
  html += `<p><b>Pikë të fituara:</b> ${r.loyaltyPointsEarned || 0}</p>`;
  html += `<p><b>Bilanci i pikëve:</b> ${r.loyaltyBalanceAfter || 0}</p>`;
  html += `<p><b>Total (ALL):</b> ${formatMoney(r.totalAll)} ALL</p>`;
  html += `<p><b>Paguar (neto, ALL):</b> ${formatMoney(r.amountPaid)} ALL</p>`;
  html += `<p><b>Klienti dha:</b> ${r.cashGivenRaw} ${r.paymentCurrency}</p>`;
  html += `<p><b>Kusur:</b> ${formatMoney(r.changeALL)} ALL</p>`;
  html += `<p><b>Mbetje:</b> ${formatMoney(r.due)} ALL</p>`;
  html += `<p><b>Status:</b> ${escapeHtml(r.status)}</p>`;
  html += `<hr><p><b>Produkte:</b></p><ul>`;
  r.items.forEach(it => html += `<li>${escapeHtml(it.n)} x${it.q} = ${it.q * it.p} ALL</li>`);
  html += '</ul>';

  body.innerHTML = html;
  viewModalEl.dataset.currentId = id;
  settleAmountEl.value = r.due || '';
  viewModalEl.style.display = 'block';
}
function closeView(){ viewModalEl.style.display = 'none'; delete viewModalEl.dataset.currentId; }

function deleteSale(id){
  if(!confirm('Fshi këtë regjistrim?')) return;
  salesHistory = salesHistory.filter(x => x.id !== id);
  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
  renderHistory();
  renderStats();
}

/* ========= DEBT ========= */
function settleDebt(){
  const id = viewModalEl.dataset.currentId;
  if(!id) return alert('Nuk ka shitje të zgjedhur');

  const r = salesHistory.find(x => x.id === id);
  if(!r) return alert('Nuk u gjet shitja');

  let amt = safeNumber(settleAmountEl.value, 0);
  if(amt <= 0) return alert('Shuma duhet > 0');
  if(r.due <= 0) return alert('Nuk ka borxh për këtë shitje');

  const payNow = Math.min(amt, r.due);
  r.amountPaid += payNow;
  r.due -= payNow;

  if(r.due <= 0){
    r.status = 'paid';
    r.due = 0;
  } else {
    r.status = 'owed';
  }

  daily += payNow;
  localStorage.setItem('daily', String(daily));

  localStorage.setItem('salesHistory', JSON.stringify(salesHistory));
  updateDaily();
  renderHistory();
  viewSale(id);
  showTxn(`<div class="success">Transaksioni u mbyll me sukses</div><div>U faturua shuma: ${payNow} ALL</div>`);
}

/* ========= EXPORT / CLEAR ========= */
function exportCSV(){
  if(!salesHistory.length) return alert('Nuk ka të dhëna për eksport');

  const rows = [];
  const header = ['id','timestamp','client','clientPhone','subtotalAll','surchargePct','loyaltyDiscountALL','loyaltyPointsUsed','totalAll','amountPaid','cashGivenRaw','paymentCurrency','paymentMethod','changeALL','due','status','items'];
  rows.push(header.join(','));

  salesHistory.slice().reverse().forEach(r=>{
    const itemsText = r.items.map(i => `${i.n} x${i.q}=${i.q*i.p}`).join(' | ');
    const row = [
      `"${r.id}"`,
      `"${r.timestamp}"`,
      `"${(r.client || '')}"`,
      `"${(r.clientPhone || '')}"`,
      r.subtotalAll,
      r.surchargePct,
      r.loyaltyDiscountALL || 0,
      r.loyaltyPointsUsed || 0,
      r.totalAll,
      r.amountPaid,
      r.cashGivenRaw,
      `"${r.paymentCurrency}"`,
      `"${r.paymentMethod}"`,
      r.changeALL,
      r.due,
      `"${r.status}"`,
      `"${itemsText}"`
    ];
    rows.push(row.join(','));
  });

  const csv = rows.join('\n');
  const blob = new Blob([csv], { type:'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'sales_history.csv';
  a.click();
  URL.revokeObjectURL(url);
}

function clearOld(){
  if(!confirm('Je i sigurt? Kjo do fshij historikun lokal.')) return;
  salesHistory = [];
  localStorage.removeItem('salesHistory');
  renderHistory();
  renderStats();
}

/* ========= DAILY & BALANCE ========= */
function updateDaily(){
  dailyEl.textContent = Number(daily || 0).toFixed(2);
  dailyEurEl.textContent = Number(eurInRegister || 0).toFixed(2);
}

function saveExchangeRate(){
  const v = Math.max(0.0001, safeNumber(exchangeRateInput.value, 0));
  if(v <= 0) return alert('Kurs i pavlefshëm');
  exchangeRate = v;
  localStorage.setItem('exchangeRate', String(exchangeRate));
  forceDailyRate = !!forceDailyRateEl.checked;
  localStorage.setItem('forceDailyRate', forceDailyRate ? '1' : '0');
  showTxn(`<div class="success">Kursi u ruajt: 1 EUR = ${exchangeRate} ALL</div>`);
  txnTitleEl.textContent = 'Kursi i këmbimit';
  recalc();
}

function closeDay(){
  const sysAll = daily;
  const sysEur = eurInRegister;
  const realAll = safeNumber(cashRealALLEl.value, 0);
  const realEur = safeNumber(cashRealEUREl.value, 0);

  const diffAll = realAll - sysAll;
  const diffEur = realEur - sysEur;

  const closures = safeParse(localStorage.getItem('dayClosures'), []);
  const closure = {
    timestamp: new Date().toISOString(),
    systemAll: sysAll,
    systemEur: sysEur,
    cashAll: realAll,
    cashEur: realEur,
    diffAll,
    diffEur
  };

  closures.push(closure);
  localStorage.setItem('dayClosures', JSON.stringify(closures));

  daily = 0;
  localStorage.setItem('daily', '0');

  cashRealALLEl.value = '';
  cashRealEUREl.value = '';
  updateDaily();

  const html = `
    <div class="success">Mbyllje dite u krye</div>
    <div><b>Shuma në sistem (ALL):</b> ${closure.systemAll} ALL</div>
    <div><b>Shuma në sistem (EUR):</b> ${closure.systemEur} EUR</div>
    <div><b>Arka reale (ALL):</b> ${closure.cashAll} ALL</div>
    <div><b>Arka reale (EUR):</b> ${closure.cashEur} EUR</div>
    <div><b>Diferenca (ALL):</b> ${closure.diffAll} ALL</div>
    <div><b>Diferenca (EUR):</b> ${closure.diffEur} EUR</div>
    <div class="small">Kursi i përdorur: 1 EUR = ${exchangeRate} ALL</div>
  `;

  txnTitleEl.textContent = 'Mbyllje dite + Raport';
  showTxn(html);
}

/* ========= REORDER REPORT ========= */
function aggregateSales(records){
  const agg = {};
  records.forEach(r=>{
    (r.items || []).forEach(it=>{
      const key = it.b || it.n;
      if(!agg[key]) agg[key] = { b: it.b, n: it.n, qty:0, revenue:0, daily:{} };
      agg[key].qty += it.q;
      agg[key].revenue += (it.q * it.p);
      const day = getLocalDateStr(r.timestamp);
      agg[key].daily[day] = (agg[key].daily[day] || 0) + it.q;
    });
  });
  return agg;
}

function computeMovingAverageForProduct(dailyCountsObj, windowDays){
  const arr = [];
  for(let i=0;i<windowDays;i++){
    const dt = new Date(Date.now() - i*24*60*60*1000);
    const key = getLocalDateStr(dt.toISOString());
    arr.push(dailyCountsObj[key] || 0);
  }
  const sum = arr.reduce((a,b)=>a+b,0);
  const avg = sum / windowDays;
  const variance = arr.reduce((acc,v)=>acc + Math.pow(v - avg, 2), 0) / windowDays;
  const sd = Math.sqrt(variance);
  return { avg, sd };
}

function getSalesSinceDays(days){
  const cutoff = Date.now() - (days * 24 * 60 * 60 * 1000);
  return salesHistory.filter(r => new Date(r.timestamp).getTime() >= cutoff);
}

function buildReorderReportRaw(manual = false){
  const now = new Date();
  const isWeekly = [1,4].includes(now.getDay());
  if(!manual && !isWeekly) return null;

  const last7 = getSalesSinceDays(7);
  const agg7 = aggregateSales(last7);
  const last14 = getSalesSinceDays(14);
  const agg14 = aggregateSales(last14);

  const suggestions = [];
  const slowItems = [];

  products.forEach(p=>{
    const key = p.b || p.n;
    const entry7 = agg7[key] || { qty:0, daily:{} };
    const stats = computeMovingAverageForProduct(entry7.daily, reorderConfig.reviewPeriodDays || 7);
    const avgDaily = stats.avg;
    const sdDaily = stats.sd;
    const targetStock = Math.ceil(avgDaily * (reorderConfig.leadDays || 3) * (reorderConfig.safetyStockFactor || 1.5));

    if(avgDaily > 0.001){
      if(p.s < targetStock){
        const desiredCoverage = Math.ceil(avgDaily * ((reorderConfig.leadDays || 3) + (reorderConfig.reviewPeriodDays || 7)));
        const safety = Math.ceil(sdDaily * Math.sqrt(reorderConfig.leadDays || 1));
        let suggestedQty = Math.max(reorderConfig.minOrderQty || 1, desiredCoverage + safety - p.s);
        suggestedQty = Math.max(1, suggestedQty);
        suggestions.push({ b:p.b, n:p.n, stock:p.s, avgDaily:avgDaily.toFixed(2), sdDaily:sdDaily.toFixed(2), targetStock, suggestedQty });
      }
    } else {
      const entry14 = agg14[key] || { qty:0 };
      if(!entry14 || entry14.qty === 0) slowItems.push({ b:p.b, n:p.n, stock:p.s });
    }
  });

  suggestions.sort((a,b)=> (a.avgDaily>0 ? a.stock / a.avgDaily : Infinity) - (b.avgDaily>0 ? b.stock / b.avgDaily : Infinity));
  return { isWeekly:true, suggestions, slowItems };
}

/* ========= SETTINGS ========= */
function loadSettingsUI(){
  document.getElementById('cfg_leadDays').value = reorderConfig.leadDays || 3;
  document.getElementById('cfg_reviewDays').value = reorderConfig.reviewPeriodDays || 7;
  document.getElementById('cfg_safety').value = reorderConfig.safetyStockFactor || 1.5;
  exchangeRateInput.value = exchangeRate || 100;
  forceDailyRateEl.checked = forceDailyRate;
  useLoyaltyPointsEl.disabled = true;
}

function saveSettings(){
  reorderConfig.leadDays = Math.max(1, safeNumber(document.getElementById('cfg_leadDays').value, 3));
  reorderConfig.reviewPeriodDays = Math.max(1, safeNumber(document.getElementById('cfg_reviewDays').value, 7));
  reorderConfig.safetyStockFactor = Math.max(0.1, safeNumber(document.getElementById('cfg_safety').value, 1.5));
  localStorage.setItem('reorderCfg', JSON.stringify(reorderConfig));
  showTxn('<div class="success">Cilësimet u ruajtën</div>');
  txnTitleEl.textContent = 'Cilësimet';
}

/* ========= MODALS ========= */
function showTxn(html){ txnMsgEl.innerHTML = html; txnModalEl.style.display = 'block'; }
function closeTxn(){ txnModalEl.style.display = 'none'; txnMsgEl.innerHTML = ''; }

/* ========= STORAGE SYNC ========= */
window.addEventListener('storage', e=>{
  if(e.key === 'p'){ products = safeParse(e.newValue, []); renderProducts(); renderStats(); checkAlerts(); }
  if(e.key === 'salesHistory'){ salesHistory = safeParse(e.newValue, []); renderHistory(); renderStats(); }
  if(e.key === 'daily'){ daily = safeNumber(e.newValue, 0); updateDaily(); }
  if(e.key === 'exchangeRate'){ exchangeRate = safeNumber(e.newValue, exchangeRate); exchangeRateInput.value = exchangeRate; }
  if(e.key === 'eurInRegister'){ eurInRegister = safeNumber(e.newValue, 0); updateDaily(); }
  if(e.key === 'loyaltyCustomers'){ loyaltyCustomers = safeParse(e.newValue, {}); renderLoyaltyTable(); refreshLoyaltyUI(); }
});

document.addEventListener('DOMContentLoaded', async () => {
  await ensureDefaultUsers();
  normalizeProducts();
  renderProducts();
  renderHistory();
  renderLoyaltyTable();
  updateDaily();
  loadSettingsUI();
  renderStats();
  checkAlerts();
  refreshLoyaltyUI();
});

window.checkAlerts = checkAlerts;
window.buildReorderReportRaw = buildReorderReportRaw;
window.setExchangeRate = v => {
  exchangeRate = safeNumber(v, exchangeRate);
  localStorage.setItem('exchangeRate', String(exchangeRate));
  exchangeRateInput.value = exchangeRate;
  recalc();
};

</script>

</body>
</html>

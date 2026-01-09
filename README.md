<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Inventory</title>

  <style>
    :root {
      --bg: #f4f1ff;
      --card: #ffffff;
      --text: #111;
      --muted: #666;
      --purple: #6c4cff;
      --purple-2: #5a3ff2;
      --green-bg: #d9fbe0;
      --green-text: #116c2e;
      --red: #e11d48;
      --border: #e8e6ff;
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      padding: 18px;
      font-family: Arial, sans-serif;
      background: var(--bg);
      color: var(--text);
    }

    h1 {
      margin: 6px 0 6px;
      font-size: 46px;
      letter-spacing: -1px;
    }

    .subtitle {
      margin: 0 0 14px;
      color: #2b2b2b;
      font-size: 18px;
    }

    .card {
      background: var(--card);
      border-radius: 22px;
      padding: 16px;
      margin-bottom: 16px;
      box-shadow: 0 6px 18px rgba(0,0,0,0.04);
      border: 1px solid rgba(0,0,0,0.03);
    }

    .row { display: flex; gap: 10px; flex-wrap: wrap; align-items: center; }
    .row > * { flex: 1 1 auto; }

    input, select {
      width: 100%;
      padding: 12px 14px;
      border-radius: 14px;
      border: 1px solid #d7d7d7;
      outline: none;
      font-size: 16px;
      background: #fff;
    }

    .btn {
      border: none;
      border-radius: 999px;
      padding: 12px 16px;
      font-weight: 700;
      font-size: 16px;
      cursor: pointer;
      white-space: nowrap;
    }

    .btn-purple { background: var(--purple); color: #fff; }
    .btn-purple:hover { background: var(--purple-2); }

    .btn-soft {
      background: #efeaff;
      color: #2b2b2b;
    }

    .status {
      margin-top: 10px;
      border-radius: 14px;
      padding: 10px 12px;
      background: var(--green-bg);
      color: var(--green-text);
      font-weight: 700;
    }

    .hint {
      margin-top: 10px;
      color: var(--muted);
      font-size: 13px;
      line-height: 1.35;
    }

    .pill {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      min-width: 34px;
      padding: 8px 12px;
      border-radius: 999px;
      background: #efeaff;
      font-weight: 700;
    }

    .section-title {
      font-size: 44px;
      margin: 0;
      letter-spacing: -1px;
    }

    .section-sub {
      margin: 6px 0 0;
      color: var(--muted);
      font-size: 14px;
      line-height: 1.35;
    }

    /* Category header (tap to toggle) */
    .cat-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      padding: 14px 16px;
      border-radius: 18px;
      background: #f1eeff;
      border: 1px solid var(--border);
      cursor: pointer;
      user-select: none;
    }

    .cat-name {
      font-size: 34px;
      font-weight: 900;
      letter-spacing: -0.5px;
    }

    .cat-right {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .chev {
      width: 30px;
      height: 30px;
      border-radius: 999px;
      background: #e9e4ff;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      font-weight: 900;
    }

    .items-wrap { margin-top: 12px; }

    /* Each item card */
    .item-card {
      border-radius: 18px;
      background: #fff;
      border: 1px solid #eee;
      padding: 14px;
      margin-bottom: 12px;
    }

    .item-top {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
    }

    .item-name {
      font-weight: 900;
      font-size: 22px;
      line-height: 1.15;
      margin: 0;
    }

    .item-meta {
      margin-top: 4px;
      color: #333;
      font-size: 18px;
      line-height: 1.25;
    }

    .item-meta .muted { color: var(--muted); }

    .qty-line {
      margin-top: 6px;
      font-size: 18px;
      font-weight: 700;
    }

    .qty-controls {
      margin-top: 10px;
      display: flex;
      gap: 12px;
      align-items: center;
    }

    .qty-btn {
      width: 58px;
      height: 58px;
      border-radius: 999px;
      border: none;
      cursor: pointer;
      background: var(--purple);
      color: #fff;
      font-size: 28px;
      font-weight: 900;
      display: inline-flex;
      align-items: center;
      justify-content: center;
    }

    .qty-btn:active { transform: scale(0.98); }

    .low-stock {
      border: 2px solid var(--red);
      box-shadow: 0 0 0 3px rgba(225,29,72,0.12);
    }

    .admin-banner {
      background: var(--green-bg);
      color: var(--green-text);
      border-radius: 16px;
      padding: 12px 14px;
      font-weight: 900;
      margin-bottom: 10px;
    }

    .admin-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      margin-bottom: 10px;
    }

    .admin-title {
      margin: 0;
      font-size: 28px;
      font-weight: 900;
    }

    .btn-exit {
      background: #ffe5e5;
      color: #a30000;
    }

    .small-note {
      color: var(--muted);
      font-size: 13px;
      margin-top: 8px;
      line-height: 1.35;
    }

    .error {
      background: #ffe7ef;
      border: 1px solid #ffb3c7;
      color: #8a0033;
      padding: 10px 12px;
      border-radius: 14px;
      font-weight: 700;
      margin-top: 10px;
      display: none;
    }
  </style>
</head>

<body>
  <h1>Inventory</h1>
  <p class="subtitle">Real-time inventory synced via Firestore</p>

  <div class="card">
    <div class="row">
      <div style="flex: 2 1 260px;">
        <input id="search" placeholder="Search item name / category / location" />
      </div>

      <div style="flex: 1 1 160px;">
        <select id="stepSelect" title="Step affects the + / - buttons">
          <option value="1">Step 1</option>
          <option value="0.5">Step 0.5</option>
          <option value="0.25">Step 0.25</option>
        </select>
      </div>

      <div style="flex: 1 1 190px;">
        <select id="lowThreshold" title="Low stock threshold">
          <option value="2">Low stock = 2 or less</option>
          <option value="3" selected>Low stock = 3 or less</option>
          <option value="5">Low stock = 5 or less</option>
        </select>
      </div>
    </div>

    <div class="row" style="margin-top: 10px;">
      <button class="btn btn-purple" id="adminBtn">Enter Admin Mode</button>
      <button class="btn btn-soft" id="refreshBtn">Refresh</button>
      <span class="pill" id="itemsCount">Items: 0</span>
    </div>

    <div class="status" id="statusText">✔ Connected. Live updates are ON.</div>
    <div class="error" id="errBox"></div>
  </div>

  <div id="adminCard" class="card" style="display:none;">
    <div class="admin-banner">Admin Mode ON</div>

    <div class="admin-header">
      <h3 class="admin-title">Add new item</h3>
      <button class="btn btn-exit" id="exitAdminBtn">Exit Admin</button>
    </div>

    <input id="itemName" placeholder="Item name (e.g. Mozzarella grated cheese)" />
    <div style="height: 10px;"></div>

    <select id="itemCategory">
      <option value="Spice Direct Order">Spice Direct Order</option>
      <option value="Caterchoice Order">Caterchoice Order</option>
    </select>

    <div style="height: 10px;"></div>
    <input id="itemLocation" placeholder="Location (e.g. Cold Room)" />

    <div style="height: 10px;"></div>
    <input id="itemQty" type="number" step="0.01" placeholder="Qty (e.g. 12 or 1.5)" />

    <div style="height: 12px;"></div>
    <button class="btn btn-purple" id="addItemBtn">Add item</button>

    <div class="small-note">
      Tip: This is a simple password gate for admin. For real security, use Firebase Auth later.
    </div>
  </div>

  <div class="card">
    <div class="row" style="justify-content: space-between;">
      <div>
        <h2 class="section-title">Stock List</h2>
        <p class="section-sub">
          Low stock items automatically float to the top (based on the threshold you choose). Tap a category title to collapse/expand.
        </p>
      </div>
      <div class="pill" id="catCount">0 categories</div>
    </div>
  </div>

  <div id="categoriesRoot"></div>

  <!-- Firebase (compat build for simple HTML) -->
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
  <script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>

  <script>
    // ✅ Your Firebase config
    const firebaseConfig = {
      apiKey: "AIzaSyC1a-QH7GDbyf47QfsvDia3sHReBN9ALho",
      authDomain: "internal-stock-d055b.firebaseapp.com",
      projectId: "internal-stock-d055b",
      storageBucket: "internal-stock-d055b.firebasestorage.app",
      messagingSenderId: "755909434320",
      appId: "1:755909434320:web:6b24b882d6c86831ca77d5"
    };

    // ✅ Admin password (same as the earlier HTML)
    // If you changed it before, change it here to match.
    const ADMIN_PASSWORD = "admin123";

    // Collection name
    const COLLECTION = "items";

    // --- App state ---
    let isAdmin = false;
    let allItems = [];
    const collapsed = {}; // categoryName -> boolean

    // --- DOM ---
    const searchEl = document.getElementById("search");
    const stepSelectEl = document.getElementById("stepSelect");
    const lowThresholdEl = document.getElementById("lowThreshold");
    const adminBtn = document.getElementById("adminBtn");
    const refreshBtn = document.getElementById("refreshBtn");
    const itemsCountEl = document.getElementById("itemsCount");
    const catCountEl = document.getElementById("catCount");
    const statusTextEl = document.getElementById("statusText");
    const errBoxEl = document.getElementById("errBox");

    const adminCardEl = document.getElementById("adminCard");
    const exitAdminBtn = document.getElementById("exitAdminBtn");
    const addItemBtn = document.getElementById("addItemBtn");

    const itemNameEl = document.getElementById("itemName");
    const itemCategoryEl = document.getElementById("itemCategory");
    const itemLocationEl = document.getElementById("itemLocation");
    const itemQtyEl = document.getElementById("itemQty");

    const categoriesRootEl = document.getElementById("categoriesRoot");

    // --- Firebase init ---
    firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore();

    // --- Helpers ---
    function showError(msg) {
      if (!msg) {
        errBoxEl.style.display = "none";
        errBoxEl.textContent = "";
        return;
      }
      errBoxEl.style.display = "block";
      errBoxEl.textContent = msg;
    }

    function norm(v) {
      return (v ?? "").toString().trim();
    }

    function safeNumber(v) {
      const n = Number(v);
      return Number.isFinite(n) ? n : 0;
    }

    function itemMatchesSearch(item, q) {
      if (!q) return true;
      const hay = (
        norm(item.name) + " " +
        norm(item.category) + " " +
        norm(item.location)
      ).toLowerCase();
      return hay.includes(q.toLowerCase());
    }

    function getStep() {
      return Number(stepSelectEl.value || 1);
    }

    function getLowThreshold() {
      return Number(lowThresholdEl.value || 3);
    }

    function groupByCategory(items) {
      const map = {};
      for (const it of items) {
        const cat = norm(it.category) || "Uncategorized";
        if (!map[cat]) map[cat] = [];
        map[cat].push(it);
      }
      return map;
    }

    // Low stock items float to top (globally) AND inside each category
    function sortItemsForDisplay(items) {
      const t = getLowThreshold();
      return items.slice().sort((a, b) => {
        const aq = safeNumber(a.quantity);
        const bq = safeNumber(b.quantity);

        const aLow = aq <= t ? 1 : 0;
        const bLow = bq <= t ? 1 : 0;

        // low stock first
        if (aLow !== bLow) return bLow - aLow;

        // then lowest quantity first
        if (aq !== bq) return aq - bq;

        // then name
        return norm(a.name).localeCompare(norm(b.name));
      });
    }

    // --- Firestore actions ---
    async function addItem() {
      const name = norm(itemNameEl.value);
      const category = norm(itemCategoryEl.value);
      const location = norm(itemLocationEl.value);
      const qty = Number(itemQtyEl.value);

      if (!name) return alert("Please enter item name");
      if (!location) return alert("Please enter location");
      if (!Number.isFinite(qty)) return alert("Please enter a valid quantity");

      showError("");

      try {
        await db.collection(COLLECTION).add({
          name,
          category,
          location,
          quantity: qty
        });

        // clear fields
        itemNameEl.value = "";
        itemLocationEl.value = "";
        itemQtyEl.value = "";
      } catch (e) {
        showError("Add failed: " + (e.message || e));
      }
    }

    async function setQty(docId, newQty) {
      // prevent negative
      const qty = Math.max(0, Number(newQty));
      showError("");

      try {
        await db.collection(COLLECTION).doc(docId).update({ quantity: qty });
      } catch (e) {
        showError("Update failed: " + (e.message || e));
      }
    }

    // --- UI actions ---
    function enterAdmin() {
      const p = prompt("Enter admin password:");
      if (p === ADMIN_PASSWORD) {
        isAdmin = true;
        adminCardEl.style.display = "block";
        showError("");
      } else {
        alert("Wrong password.");
      }
    }

    function exitAdmin() {
      isAdmin = false;
      adminCardEl.style.display = "none";
    }

    function toggleCategory(catName) {
      collapsed[catName] = !collapsed[catName];
      render();
    }

    function render() {
      const q = norm(searchEl.value);
      const threshold = getLowThreshold();

      // filter + sort
      const filtered = allItems.filter(it => itemMatchesSearch(it, q));

      itemsCountEl.textContent = "Items: " + filtered.length;

      // group
      const grouped = groupByCategory(filtered);
      const cats = Object.keys(grouped);

      catCountEl.textContent = `${cats.length} categor${cats.length === 1 ? "y" : "ies"}`;

      // Order categories: show ones that have low stock items first
      cats.sort((a, b) => {
        const aHasLow = grouped[a].some(x => safeNumber(x.quantity) <= threshold) ? 1 : 0;
        const bHasLow = grouped[b].some(x => safeNumber(x.quantity) <= threshold) ? 1 : 0;
        if (aHasLow !== bHasLow) return bHasLow - aHasLow;
        return a.localeCompare(b);
      });

      categoriesRootEl.innerHTML = "";

      for (const cat of cats) {
        const catItems = sortItemsForDisplay(grouped[cat]);
        const isCollapsed = !!collapsed[cat];

        const catCard = document.createElement("div");
        catCard.className = "card";

        const header = document.createElement("div");
        header.className = "cat-header";
        header.addEventListener("click", () => toggleCategory(cat));

        header.innerHTML = `
          <div class="cat-name">${cat}</div>
          <div class="cat-right">
            <span class="pill">${catItems.length}</span>
            <span class="chev">${isCollapsed ? "▸" : "▾"}</span>
          </div>
        `;

        catCard.appendChild(header);

        const wrap = document.createElement("div");
        wrap.className = "items-wrap";
        wrap.style.display = isCollapsed ? "none" : "block";

        for (const it of catItems) {
          const qty = safeNumber(it.quantity);
          const isLow = qty <= threshold;

          const itemDiv = document.createElement("div");
          itemDiv.className = "item-card" + (isLow ? " low-stock" : "");
          itemDiv.innerHTML = `
            <div class="item-top">
              <div style="flex:1;">
                <p class="item-name">${norm(it.name) || "Unnamed item"}</p>
                <div class="item-meta">
                  <span class="muted">${norm(it.location) || "No location"}</span>
                </div>
                <div class="qty-line">Quantity: ${Number.isFinite(qty) ? qty : 0}</div>
              </div>
            </div>

            <div class="qty-controls">
              <button class="qty-btn" aria-label="decrease">−</button>
              <button class="qty-btn" aria-label="increase">+</button>
            </div>
          `;

          const btns = itemDiv.querySelectorAll("button.qty-btn");
          btns[0].addEventListener("click", () => setQty(it.id, qty - getStep()));
          btns[1].addEventListener("click", () => setQty(it.id, qty + getStep()));

          wrap.appendChild(itemDiv);
        }

        catCard.appendChild(wrap);
        categoriesRootEl.appendChild(catCard);
      }

      if (cats.length === 0) {
        const empty = document.createElement("div");
        empty.className = "card";
        empty.innerHTML = `<div style="color:#555;font-weight:700;">No items found.</div>`;
        categoriesRootEl.appendChild(empty);
      }
    }

    // --- Events ---
    adminBtn.addEventListener("click", enterAdmin);
    exitAdminBtn.addEventListener("click", exitAdmin);
    addItemBtn.addEventListener("click", addItem);

    refreshBtn.addEventListener("click", () => render());
    searchEl.addEventListener("input", () => render());
    stepSelectEl.addEventListener("change", () => render());
    lowThresholdEl.addEventListener("change", () => render());

    // --- Live sync ---
    statusTextEl.textContent = "⏳ Connecting...";
    showError("");

    db.collection(COLLECTION).onSnapshot(
      (snap) => {
        const items = [];
        snap.forEach(doc => items.push({ id: doc.id, ...doc.data() }));
        allItems = items;
        statusTextEl.textContent = "✔ Connected. Live updates are ON.";
        showError("");
        render();
      },
      (err) => {
        statusTextEl.textContent = "❌ Not connected";
        showError("Firestore error: " + (err.message || err));
      }
    );
  </script>
</body>
</html>

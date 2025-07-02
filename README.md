# BiteLinke
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8">
  <title>BiteLink – Die erste Rezepte-Website online!</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    :root {
      --primary: #0076ff;
      --primary-dark: #0057b8;
      --bg: #f7faff;
      --card: #fff;
      --shadow: 0 2px 18px #0001;
      --radius: 20px;
      --border: #e3e6ea;
      --danger: #d7263d;
      --success: #4bb543;
    }
    html, body {
      background: var(--bg);
      color: #232323;
      font-family: system-ui, Arial, sans-serif;
      margin: 0;
      padding: 0;
      min-height: 100vh;
      height: 100%;
    }
    #app-container {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      height: 100dvh;
      max-width: 540px;
      margin: 0 auto;
      background: var(--bg);
    }
    .main-content {
      flex: 1;
      overflow-y: auto;
      padding-bottom: 84px;
    }
    .header {
      background: var(--card);
      padding: 18px 17px 10px 17px;
      display: flex;
      align-items: center;
      position: sticky;
      top: 0; left: 0; right: 0;
      z-index: 99;
      box-shadow: 0 2px 14px #0002;
    }
    .header .logo {
      font-size: 1.35em;
      font-weight: 700;
      flex: 1;
      letter-spacing: -1.5px;
      user-select: none;
      color: var(--primary-dark);
    }
    .header .logout-btn {
      background: none;
      border: none;
      color: var(--primary);
      font-size: 1em;
      font-weight: 600;
      cursor: pointer;
      padding: 8px 13px;
      border-radius: 9px;
      transition: background .15s;
    }
    .header .logout-btn:hover {
      background: #e7f4ff;
    }
    .admin-badge {
      margin-left: 9px;
      padding: 2.5px 9px;
      font-size: .82em;
      background: #e7f4ff;
      color: var(--primary-dark);
      border-radius: 9px;
      font-weight: 700;
      letter-spacing: .5px;
    }
    /* TABBAR */
    .tab-bar {
      position: fixed;
      left: 0; right: 0; bottom: 0;
      background: var(--card);
      border-top: 1.5px solid var(--border);
      box-shadow: 0 -2px 14px #0001;
      display: flex;
      justify-content: space-around;
      align-items: center;
      height: 65px;
      z-index: 100;
      max-width: 540px;
      margin: 0 auto;
      width: 100vw;
    }
    .tab-bar button {
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 0;
      border: none;
      background: none;
      color: #888;
      font-size: 1em;
      font-weight: 500;
      cursor: pointer;
      border-radius: 0;
      transition: color .15s;
      height: 100%;
    }
    .tab-bar button.active,
    .tab-bar button:active {
      color: var(--primary-dark);
    }
    .tab-bar .tab-icon {
      font-size: 1.37em;
      display: block;
      margin-bottom: 2px;
    }
    /* SECTION & CARD */
    .section {
      background: var(--card);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      margin: 23px 12px 23px 12px;
      padding: 18px 19px 11px 18px;
      display: flex;
      flex-direction: column;
    }
    .section-title {
      font-size: 1.17em;
      font-weight: 700;
      margin-bottom: 8px;
      color: var(--primary-dark);
    }
    /* KARTENLISTE */
    .recipes-list {
      display: grid;
      grid-template-columns: 1fr;
      gap: 15px;
    }
    @media(min-width: 450px) {
      .recipes-list { grid-template-columns: 1fr 1fr; }
    }
    .recipe-card {
      background: #f4f9ff;
      border-radius: 14px;
      box-shadow: 0 1px 5px #0001;
      padding: 12px 13px 11px 13px;
      cursor: pointer;
      border: 1.5px solid transparent;
      transition: border-color .17s;
      display: flex;
      flex-direction: column;
      position: relative;
      min-height: 112px;
    }
    .recipe-card:hover { border-color: #0076ff; }
    .recipe-img-thumb {
      width: 100%;
      max-height: 80px;
      object-fit: cover;
      border-radius: 8px;
      margin-bottom: 7px;
      display: block;
    }
    .recipe-title {
      font-weight: 700;
      font-size: 1.11em;
      margin-bottom: 2px;
      color: #212529;
    }
    .recipe-meta {
      font-size: .98em;
      color: #888;
    }
    .rc-actions {
      margin-top: 6px;
      display: flex;
      align-items: center;
      gap: 9px;
    }
    .like-btn, .sub-btn {
      background: none;
      border: none;
      color: #0076ff;
      font-size: 1.16em;
      cursor: pointer;
      margin-right: 4px;
      transition: color .15s;
      vertical-align: middle;
      padding: 0 3px;
    }
    .like-btn.liked { color: #d7263d; }
    .sub-btn.subscribed { color: #4bb543; }
    /* OVERLAY/DETAIL */
    .overlay-bg {
      position: fixed;
      left: 0; top: 0; right: 0; bottom: 0;
      background: rgba(0,0,0,0.13);
      z-index: 9999;
      display: flex;
      align-items: center;
      justify-content: center;
      animation: fadeIn .18s;
    }
    .overlay-card {
      background: var(--card);
      border-radius: var(--radius);
      box-shadow: 0 4px 32px #0002;
      min-width: 320px;
      max-width: 97vw;
      max-height: 97vh;
      overflow: auto;
      padding: 20px 13px 11px 16px;
      position: relative;
      display: flex;
      flex-direction: column;
      gap: 7px;
    }
    .close-btn {
      background: none;
      border: none;
      color: #999;
      font-size: 1.32em;
      font-weight: 700;
      position: absolute;
      top: 10px; right: 15px;
      cursor: pointer;
    }
    .overlay-card h3 { margin: 0 0 7px 0; }
    .overlay-content { font-size: 1.03em; color: #212529; }
    .divider { border: none; border-top: 1.5px solid #eee; margin: 13px 0 9px 0; }
    /* Suche */
    .search-bar {
      display: flex;
      align-items: center;
      margin-bottom: 18px;
      gap: 7px;
      background: #f4f9ff;
      border-radius: 13px;
      padding: 8px 13px;
    }
    .search-bar input {
      flex: 1;
      border: none;
      background: transparent;
      font-size: 1.12em;
      outline: none;
      padding: 7px 0;
    }
    .search-bar .clear-btn {
      background: none;
      border: none;
      color: #aaa;
      font-size: 1.18em;
      cursor: pointer;
    }
    .search-results {
      background: #fff;
      border-radius: 12px;
      box-shadow: 0 2px 12px #0001;
      margin-bottom: 18px;
      padding: 7px 0;
      max-height: 44vh;
      overflow-y: auto;
    }
    .search-result {
      padding: 11px 16px;
      cursor: pointer;
      border-bottom: 1px solid #f3f4f6;
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 1.09em;
    }
    .search-result:last-child { border-bottom: none; }
    .search-result-type {
      font-size: .93em;
      color: var(--primary);
      font-weight: 700;
    }
    /* Tipp */
    .tip-card {
      background: #e7f4ff;
      border-radius: 13px;
      padding: 13px 12px 12px 12px;
      color: #0057b8;
      font-size: 1.08em;
      margin-bottom: 2px;
      box-shadow: 0 1px 6px #0001;
    }
    .tip-card .tip-meta {
      font-size: .93em;
      color: #0057b8;
      margin-top: 5px;
    }
    /* Profil & Admin */
    .profile-header {
      display: flex; align-items: center; gap:19px;
    }
    .profile-img {
      width: 80px; height: 80px; border-radius: 50%; border:2px solid #e3e6ea;
      object-fit: cover;
    }
    .profile-username {
      font-size:1.38em;font-weight:800;letter-spacing:-.5px;color:var(--primary-dark);
    }
    .profile-stat {
      color: var(--primary);margin-top:4px;
    }
    .profile-actions {
      margin-top: 7px; display: flex; gap:11px; align-items:center;
    }
    .admin-panel {
      background: var(--card);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 18px 10px 14px 10px;
      margin: 17px 7px 22px 7px;
    }
    /* MODAL */
    .fullscreen-modal-bg {
      position: fixed;
      left:0; top:0; right:0; bottom:0;
      background: #f7faff;
      z-index: 10000;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100dvh;
      width: 100vw;
      transition: opacity .18s;
    }
    .fullscreen-modal {
      width: 100vw; height: 100dvh;
      max-width: 540px;
      margin: 0 auto;
      background: var(--card);
      border-radius: 0;
      box-shadow: var(--shadow);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: stretch;
      padding: 0;
      position: relative;
      animation: fadeIn .17s;
    }
    .fullscreen-modal .modal-content {
      padding: 36px 22px 24px 22px;
      flex: 1; 
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
    .fullscreen-modal .close-btn {
      background: none;
      border: none;
      color: #aaa;
      font-size: 1.54em;
      font-weight: 800;
      position: absolute;
      top: 18px; right: 19px;
      cursor: pointer;
      z-index: 11;
    }
    .fullscreen-modal h2 {
      font-size: 2.1em;
      margin-bottom: 7px;
      text-align: center;
      font-weight: 800;
      color: var(--primary-dark);
      letter-spacing: -1px;
    }
    .fullscreen-modal .subtitle {
      text-align: center;
      color: #888;
      margin-bottom: 26px;
      font-size: 1em;
    }
    .btn {
      background: var(--primary);
      color: #fff;
      border: none;
      padding: 13px 0;
      border-radius: 12px;
      font-size: 1.19em;
      font-weight: 700;
      cursor: pointer;
      margin-top: 11px;
      transition: background .2s;
      box-shadow: 0 0.5px 2px #0002;
      letter-spacing: -.5px;
    }
    .btn:disabled {
      background: #a9cfff;
      cursor: not-allowed;
    }
    .btn.secondary {
      background: #f7faff;
      color: var(--primary);
      border: 1.2px solid var(--primary);
      margin: 0;
    }
    .error {
      color: var(--danger);
      font-size: 1em;
      margin: 0 0 7px 0;
      text-align: center;
      font-weight: 500;
    }
    @media (max-width: 600px) {
      #app-container { max-width: 100vw; }
      .section, .admin-panel { margin: 13px 2vw 13px 2vw; padding: 12px 2vw 10px 2vw; }
      .fullscreen-modal { max-width: 100vw; }
      .tab-bar { max-width: 100vw; }
    }
  </style>
</head>
<body>
  <div id="app-container"></div>
  <script>
    // --- DB & State
    const DB_KEY = "bitelink_app_launch_v11";
    const DB_VERSION = 13;
    function getDB() {
      let db = JSON.parse(localStorage.getItem(DB_KEY) || "null");
      if (!db || db.version !== DB_VERSION) {
        db = getDefaultDB();
        saveDB(db);
      }
      return db;
    }
    function saveDB(db) {
      localStorage.setItem(DB_KEY, JSON.stringify(db));
    }
    function getDefaultDB() {
      return {
        version: DB_VERSION,
        users: [
          { username: "FLAP", password: "1234", admin: true, blocked: false, agreed: true, created: Date.now()-4000000, lastActive: Date.now(), likes: [], subscriptions: [], subscribers: [], photo:"" },
          { username: "kochfee", password: "salat", admin: false, blocked: false, agreed: true, created: Date.now()-86400000, lastActive: Date.now()-30000, likes: [], subscriptions: [], subscribers: [], photo:"" }
        ],
        recipes: [
          {
            id: 1,
            title: "Spaghetti Carbonara",
            author: "FLAP",
            created: Date.now()-1800000,
            ingredients: ["200g Spaghetti", "2 Eier", "50g Parmesan", "80g Speck", "Salz", "Pfeffer"],
            steps: ["Spaghetti kochen.", "Speck anbraten.", "Eier und Parmesan verrühren.", "Spaghetti abgießen, mit Speck und Ei-Parmesan-Mix mischen."],
            remixes: [],
            likes: ["kochfee"],
            image: ""
          },
          {
            id: 2,
            title: "Avocado Toast Deluxe",
            author: "FLAP",
            created: Date.now()-3600000,
            ingredients: ["2 Scheiben Brot", "1 Avocado", "Chili-Flocken", "Zitrone", "Salz", "Pfeffer"],
            steps: ["Brot toasten.", "Avocado zerdrücken, würzen.", "Auf das Brot geben, mit Chili toppen."],
            remixes: [],
            likes: [],
            image: ""
          },
          {
            id: 3,
            title: "Schneller Bananen-Smoothie",
            author: "FLAP",
            created: Date.now()-7200000,
            ingredients: ["2 Bananen", "200ml Milch", "1 TL Honig"],
            steps: ["Alles in Mixer geben.", "Fein pürieren.", "Sofort genießen."],
            remixes: [],
            likes: [],
            image: ""
          }
        ],
        tips: [
          { id: 1, text: "Verwende frische Kräuter für mehr Geschmack.", author: "kochfee" },
          { id: 2, text: "Vor dem Kochen immer alles vorbereiten!", author: "tastymax" },
          { id: 3, text: "Mit Liebe würzen.", author: "FLAP" },
          { id: 4, text: "Resteverwertung reduziert Lebensmittelverschwendung.", author: "saver" },
          { id: 5, text: "Nudeln nach dem Kochen mit etwas Öl mischen, damit sie nicht kleben.", author: "pastaqueen" }
        ],
        categories: ["Vegan", "Schnell", "Low Carb", "Backen"],
        challenge: {
          title: "Das beste Blitzgericht mit 3 Zutaten!",
          daysLeft: 3,
          entries: []
        }
      };
    }
    let state = {
      loggedIn: false,
      user: null,
      tab: "home", // home, search, machen, profile, admin
      search: "",
      showLogin: false,
      showRegister: false,
      showCreate: false,
      tipOrRecipe: null, // "tip" oder "recipe"
      overlay: null // {type, data}
    };

    // --- Render Main
    function render() {
      const db = getDB();
      const root = document.getElementById("app-container");
      if(state.showLogin) { root.innerHTML = loginModalHTML(); loginModalEvents(db); return; }
      if(state.showRegister) { root.innerHTML = registerModalHTML(); registerModalEvents(db); return; }
      if(state.showCreate) { root.innerHTML = createModalHTML(); createModalEvents(db); return; }
      root.innerHTML = `
        <div class="header">
          <span class="logo">BiteLink</span>
          ${state.loggedIn && state.user.admin ? `<span class="admin-badge">ADMIN</span>` : ""}
          ${state.loggedIn ? `<button class="logout-btn" id="logout-btn">Logout</button>` : ""}
        </div>
        <div class="main-content">
          ${bannerHTML()}
          ${state.tab==="home"?homeHTML(db):""}
          ${state.tab==="search"?searchHTML(db):""}
          ${state.tab==="machen"?machenHTML(db):""}
          ${state.tab==="profile"?profileHTML(db, state.user ? state.user.username : null):""}
          ${state.tab==="admin" && state.loggedIn && state.user && state.user.admin ? adminHTML(db) : ""}
        </div>
        ${tabBarHTML()}
        ${state.overlay?overlayHTML(db):""}
      `;
      // Events
      if(state.loggedIn) {
        $("#logout-btn").onclick = () => { state.loggedIn=false; state.user=null; render(); };
      }
      $all(".tab-bar button").forEach(btn =>
        btn.onclick = () => { state.tab = btn.dataset.tab; state.overlay=null; render(); }
      );
      $("#open-login-btn") && ($("#open-login-btn").onclick = ()=>{state.showLogin=true; render();});
      $("#open-register-btn") && ($("#open-register-btn").onclick = ()=>{state.showRegister=true; render();});
      $all(".create-btn").forEach(btn =>
        btn.onclick = ()=>{state.tipOrRecipe=btn.dataset.type; state.showCreate=true; render();}
      );
      // Rezept-Details
      $all(".recipe-card").forEach(card =>
        card.onclick = e => {
          if(e.target.classList.contains("like-btn") || e.target.classList.contains("sub-btn")) return;
          state.overlay = {type: "rezept", id: card.dataset.id}; render();
        }
      );
      // Like & Abo in Listen
      $all(".like-btn").forEach(btn => {
        btn.onclick = e => {
          e.stopPropagation();
          if(!state.loggedIn) { state.showLogin = true; render(); return; }
          toggleLike(btn.dataset.id);
        }
      });
      $all(".sub-btn").forEach(btn => {
        btn.onclick = e => {
          e.stopPropagation();
          if(!state.loggedIn) { state.showLogin = true; render(); return; }
          toggleAbo(btn.dataset.user);
        }
      });
      // Suche
      const inSearch = $("#search-input");
      if(inSearch) {
        inSearch.oninput = e => { state.search = e.target.value; render(); };
        inSearch.focus();
        $("#search-clear") && ($("#search-clear").onclick = () => { state.search=""; render(); });
      }
      $all(".search-result").forEach(el => {
        el.onclick = () => {
          const typ = el.dataset.type, id = el.dataset.id;
          if(!typ || !id) return;
          if(!state.loggedIn) { state.showLogin = true; render(); return; }
          if(typ==="rezept") state.overlay = {type:"rezept", id};
          if(typ==="user") state.overlay = {type:"profil", username:id};
          if(typ==="tipp") state.overlay = {type:"tipp", id};
          render();
        };
      });
      // Overlay close
      if(state.overlay) {
        $(".overlay-bg .close-btn").onclick = ()=>{state.overlay=null; render();}
      }
    }

    // --- Overlay
    function overlayHTML(db) {
      const o = state.overlay;
      if(!o) return "";
      let html = "";
      if(o.type==="rezept") {
        const r = db.recipes.find(rr=>rr.id==o.id);
        if(!r) return "";
        const user = db.users.find(u=>u.username===r.author);
        html = `
          <h3>${r.title}</h3>
          <div class="overlay-content">
            <b>Autor:</b> <span class="profile-link">${r.author}</span> <br>
            <b>Erstellt:</b> ${formatDate(r.created)}<br>
            ${r.image?`<img src="${r.image}" alt="Bild" style="width:100%;max-height:170px;object-fit:cover;border-radius:10px;margin:7px 0;">`:""}
            <hr class="divider"/>
            <b>Zutaten:</b>
            <ul>${r.ingredients.map(i=>`<li>${i}</li>`).join('')}</ul>
            <b>Zubereitung:</b>
            <ol>${r.steps.map(s=>`<li>${s}</li>`).join('')}</ol>
            <div class="rc-actions" style="margin-top:11px;">
              <button class="like-btn${r.likes&&state.user&&r.likes.includes(state.user.username)?" liked":""}" data-id="${r.id}" title="Like">&#10084;</button>
              <span style="font-size:.98em;">${r.likes?r.likes.length:0} Likes</span>
              ${user && state.user && state.user.username!==user.username ? `
                <button class="sub-btn${state.user.subscriptions&&state.user.subscriptions.includes(user.username)?" subscribed":""}" data-user="${user.username}">
                  ${state.user.subscriptions&&state.user.subscriptions.includes(user.username)?"Abonniert":"Abonnieren"}
                </button>
              `: ""}
            </div>
          </div>
        `;
      }
      if(o.type==="profil") {
        const user = db.users.find(u=>u.username===o.username);
        if(!user) return "";
        const recipes = db.recipes.filter(r=>r.author===user.username);
        html = `
          <div class="profile-header">
            <img class="profile-img" src="${user.photo||'https://api.dicebear.com/8.x/initials/svg?seed='+encodeURIComponent(user.username)}" alt="Profilbild"/>
            <div>
              <span class="profile-username">${user.username}</span>
              <div class="profile-stat">${recipes.length} Rezepte</div>
              <div class="profile-stat">${user.subscribers.length} Abonnenten • ${user.subscriptions.length} Abos</div>
              ${state.user && state.user.username!==user.username?`
                <div class="profile-actions">
                  <button class="sub-btn${state.user.subscriptions.includes(user.username)?" subscribed":""}" data-user="${user.username}">
                    ${state.user.subscriptions.includes(user.username)?"Abonniert":"Abonnieren"}
                  </button>
                </div>
              `:""}
            </div>
          </div>
          <div style="margin-top:17px;">
            <b>Rezepte von ${user.username}:</b>
            <div class="recipes-list">
              ${recipes.map(r=>recipeCardHTML(r)).join("")||"<div>Noch keine Rezepte.</div>"}
            </div>
          </div>
        `;
      }
      if(o.type==="tipp") {
        const t = getDB().tips.find(tt=>tt.id==o.id);
        html = `<div class="tip-card" style="font-size:1.21em;margin-bottom:0;">${t.text}<div class="tip-meta">– ${t.author}</div></div>`;
      }
      return `<div class="overlay-bg"><div class="overlay-card">${html}<button class="close-btn" aria-label="Schließen" title="Schließen">&times;</button></div></div>`;
    }

    // --- Like/Abo
    function toggleLike(rid) {
      const db = getDB();
      const r = db.recipes.find(rr => rr.id==rid);
      if(!r) return;
      r.likes = r.likes||[];
      const idx = r.likes.indexOf(state.user.username);
      if(idx>-1) r.likes.splice(idx,1); else r.likes.push(state.user.username);
      saveDB(db);
      render();
    }
    function toggleAbo(username) {
      if(!state.user || state.user.username===username) return;
      const db = getDB();
      const u = db.users.find(u=>u.username===username);
      const me = db.users.find(u=>u.username===state.user.username);
      if(!u||!me) return;
      const idx = me.subscriptions.indexOf(username);
      const idx2 = u.subscribers.indexOf(me.username);
      if(idx>-1) me.subscriptions.splice(idx,1); else me.subscriptions.push(username);
      if(idx2>-1) u.subscribers.splice(idx2,1); else u.subscribers.push(me.username);
      saveDB(db);
      render();
    }

    // --- Banner
    function bannerHTML() {
      return `<div style="margin:19px 0 14px 0;text-align:center;padding:7px 0;">
        <b>BiteLink</b> – Die erste Rezepte-Website, die online geht!<br>
        <span style="color:var(--primary);font-size:.99em;">Willkommen bei der neuen Ära der Essensverbindung.</span>
      </div>`;
    }

    // --- Home
    function homeHTML(db) {
      let feed = db.recipes;
      let aboFeed = [];
      if(state.loggedIn && state.user.subscriptions.length>0) {
        aboFeed = db.recipes.filter(r=>state.user.subscriptions.includes(r.author));
      }
      return `
        ${aboFeed.length?`
          <div class="section">
            <div class="section-title">Von deinen Abos</div>
            <div class="recipes-list">
              ${aboFeed.map(r=>recipeCardHTML(r)).join("")}
            </div>
          </div>
        `:""}
        <div class="section">
          <div class="section-title">Alle Rezepte</div>
          <div class="recipes-list">
            ${feed.map(r=>recipeCardHTML(r)).join('')||"<div>Keine Rezepte gefunden.</div>"}
          </div>
        </div>
        <div class="section">
          <div class="section-title">Tipps des Tages</div>
          <div class="tip-list">
            ${randomTipsHTML(db.tips, 3)}
          </div>
        </div>
      `;
    }

    // --- Rezept-Karte
    function recipeCardHTML(r) {
      const db = getDB();
      const user = db.users.find(u=>u.username===r.author);
      return `
        <div class="recipe-card" data-id="${r.id}">
          ${r.image?`<img src="${r.image}" class="recipe-img-thumb" alt="Bild">`:""}
          <span class="recipe-title">${r.title||"Rezept"}</span>
          <div class="recipe-meta">von ${r.author||"?"} • ${formatDate(r.created)}</div>
          <div class="rc-actions">
            <button class="like-btn${state.user&&r.likes&&r.likes.includes(state.user.username)?" liked":""}" data-id="${r.id}" title="Like">&#10084;</button>
            <span style="font-size:.98em;">${r.likes?r.likes.length:0}</span>
            ${user && state.user && state.user.username!==user.username ? `
              <button class="sub-btn${state.user.subscriptions&&state.user.subscriptions.includes(user.username)?" subscribed":""}" data-user="${user.username}">
                ${state.user.subscriptions&&state.user.subscriptions.includes(user.username)?"Abonniert":"Abo"}
              </button>
            `:""}
          </div>
        </div>
      `;
    }

    // --- Tipps: 3 zufällig
    function randomTipsHTML(arr, n) {
      if(arr.length<=n) return arr.map(t=>tipCardHTML(t)).join('');
      let copy = arr.slice();
      let tips = [];
      while(tips.length<n && copy.length) {
        let idx = Math.floor(Math.random()*copy.length);
        tips.push(copy.splice(idx,1)[0]);
      }
      return tips.map(t=>tipCardHTML(t)).join('');
    }
    function tipCardHTML(t) {
      return `<div class="tip-card">${t.text}<div class="tip-meta">– ${t.author}</div></div>`;
    }

    // --- Suche
    function searchHTML(db) {
      const s = state.search.trim().toLowerCase();
      const recipeResults = db.recipes.filter(r => r.title.toLowerCase().includes(s) || r.ingredients?.join(" ").toLowerCase().includes(s));
      const userResults = db.users.filter(u => u.username.toLowerCase().includes(s));
      const tipResults = db.tips.filter(t => t.text.toLowerCase().includes(s));
      return `
        <div class="section">
          <div class="section-title">Suche</div>
          <div class="search-bar">
            <input type="text" id="search-input" placeholder="Suche nach Rezept, Nutzer oder Tipp..." value="${state.search||""}" autocomplete="off" />
            ${state.search?'<button class="clear-btn" id="search-clear" title="Reset">×</button>':''}
          </div>
          <div class="search-results">
            ${state.search && !recipeResults.length && !userResults.length && !tipResults.length ?
              "Keine Ergebnisse." : ""}
            ${recipeResults.map(r=>`
              <div class="search-result" data-type="rezept" data-id="${r.id}">
                <span class="search-result-type">Rezept</span> ${r.title}
              </div>
            `).join('')}
            ${userResults.map(u=>`
              <div class="search-result" data-type="user" data-id="${u.username}">
                <span class="search-result-type">User</span> ${u.username}
              </div>
            `).join('')}
            ${tipResults.map(t=>`
              <div class="search-result" data-type="tipp" data-id="${t.id}">
                <span class="search-result-type">Tipp</span> ${t.text}
              </div>
            `).join('')}
          </div>
        </div>
      `;
    }

    // --- Machen (Erstellen/Teilen)
    function machenHTML(db) {
      if(!state.loggedIn) {
        return `<div class="section"><b>Bitte melde dich an, um Rezepte oder Tipps zu erstellen!</b><br>
        <button class="btn" id="open-login-btn" style="margin-top:14px;">Login</button>
        <button class="btn secondary" id="open-register-btn" style="margin-top:7px;">Registrieren</button></div>`;
      }
      return `
        <div class="section">
          <div class="section-title">Was möchtest du machen?</div>
          <button class="btn create-btn" data-type="recipe">Rezept erstellen</button>
          <button class="btn create-btn" data-type="tip">Tipp teilen</button>
        </div>
      `;
    }

    // --- Profil
    function profileHTML(db, username) {
      if(!username) {
        return `<div class="section"><b>Bitte melde dich an, um dein Profil zu sehen!</b><br>
        <button class="btn" id="open-login-btn" style="margin-top:14px;">Login</button>
        <button class="btn secondary" id="open-register-btn" style="margin-top:7px;">Registrieren</button></div>`;
      }
      const user = db.users.find(u=>u.username===username);
      if(!user) return "<div>Nutzer nicht gefunden.</div>";
      const recipes = db.recipes.filter(r=>r.author===username);
      return `
        <div class="section" style="min-height:70vh;">
          <div class="profile-header">
            <img class="profile-img" src="${user.photo||'https://api.dicebear.com/8.x/initials/svg?seed='+encodeURIComponent(user.username)}" alt="Profilbild"/>
            <div>
              <span class="profile-username">${user.username}</span>
              <div class="profile-stat">${recipes.length} Rezepte</div>
              <div class="profile-stat">${user.subscribers.length} Abonnenten • ${user.subscriptions.length} Abos</div>
            </div>
          </div>
          <div style="margin-top:17px;">
            <b>Eigene Rezepte:</b>
            <div class="recipes-list">
              ${recipes.map(r=>recipeCardHTML(r)).join("")||"<div>Noch keine Rezepte.</div>"}
            </div>
          </div>
        </div>
      `;
    }

    // --- Adminbereich
    function adminHTML(db) {
      return `
        <div class="admin-panel">
          <div class="section-title">Admin-Bereich</div>
          <div>
            <b>Alle Nutzer</b>:
            <ul>
              ${db.users.map(u=>
                `<li>${u.username}${u.admin?" (Admin)":" "}${u.blocked?" [gesperrt]":""}</li>`
              ).join("")}
            </ul>
          </div>
          <div>
            <b>Rezepte insgesamt:</b> ${db.recipes.length}
          </div>
          <div>
            <b>Tipps insgesamt:</b> ${db.tips.length}
          </div>
        </div>
      `;
    }

    // --- Login/Registrierung/Create-Modal (Fullpage)
    function loginModalHTML() {
      return `
        <div class="fullscreen-modal-bg">
          <div class="fullscreen-modal">
            <button class="close-btn" id="close-login">&times;</button>
            <div class="modal-content">
              <h2>BiteLink</h2>
              <div class="subtitle">Die beste Essensverbindung. Willkommen!</div>
              <form id="login-form" autocomplete="off">
                <div class="input-group">
                  <label for="username">Benutzername</label>
                  <input type="text" id="username" maxlength="22" required autocomplete="username" autofocus/>
                </div>
                <div class="input-group">
                  <label for="password">Passwort</label>
                  <input type="password" id="password" maxlength="32" required autocomplete="current-password" />
                </div>
                <div class="error" id="login-error"></div>
                <button class="btn" type="submit">Login</button>
                <div style="margin-top:18px;text-align:center;">
                  Noch kein Account? <a href="#" id="to-register">Jetzt registrieren!</a>
                </div>
              </form>
            </div>
          </div>
        </div>
      `;
    }
    function registerModalHTML() {
      return `
        <div class="fullscreen-modal-bg">
          <div class="fullscreen-modal">
            <button class="close-btn" id="close-register">&times;</button>
            <div class="modal-content">
              <h2>BiteLink</h2>
              <div class="subtitle">Registriere dich für die Essensverbindung!</div>
              <form id="register-form" autocomplete="off">
                <div class="input-group">
                  <label for="reg-username">Benutzername</label>
                  <input type="text" id="reg-username" maxlength="22" required />
                </div>
                <div class="input-group">
                  <label for="reg-password">Passwort</label>
                  <input type="password" id="reg-password" maxlength="32" required />
                </div>
                <div class="error" id="reg-error"></div>
                <button class="btn" type="submit">Registrieren</button>
                <div style="margin-top:18px;text-align:center;">
                  Bereits ein Account? <a href="#" id="to-login">Jetzt einloggen!</a>
                </div>
              </form>
            </div>
          </div>
        </div>
      `;
    }
    function createModalHTML() {
      return `
        <div class="fullscreen-modal-bg">
          <div class="fullscreen-modal">
            <button class="close-btn" id="close-create">&times;</button>
            <div class="modal-content">
              <h2>${state.tipOrRecipe==="tip"?"Tipp teilen":"Rezept erstellen"}</h2>
              <form id="create-form" autocomplete="off">
                ${state.tipOrRecipe==="tip"?`
                  <div class="input-group">
                    <label for="tip-text">Tipp*</label>
                    <textarea id="tip-text" maxlength="120" required style="min-height:54px;"></textarea>
                  </div>
                `:`
                  <div class="input-group">
                    <label for="title">Titel*</label>
                    <input type="text" id="title" maxlength="30" required />
                  </div>
                  <div class="input-group">
                    <label for="ingredients">Zutaten* <small>(Komma-getrennt)</small></label>
                    <input type="text" id="ingredients" maxlength="80" required />
                  </div>
                  <div class="input-group">
                    <label for="steps">Schritte* <small>(Komma-getrennt)</small></label>
                    <input type="text" id="steps" maxlength="120" required />
                  </div>
                  <div class="input-group">
                    <label for="image">Bild (optional)</label>
                    <input type="file" id="image" accept="image/*" />
                  </div>
                `}
                <div class="error" id="create-error"></div>
                <button class="btn" type="submit">${state.tipOrRecipe==="tip"?"Tipp veröffentlichen":"Rezept speichern"}</button>
              </form>
            </div>
          </div>
        </div>
      `;
    }

    // --- EVENTS für Vollbild-Modals
    function loginModalEvents(db) {
      $("#close-login").onclick = ()=>{state.showLogin=false; render();};
      $("#to-register").onclick = e => {e.preventDefault(); state.showLogin=false; state.showRegister=true; render();};
      $("#login-form").onsubmit = e => {
        e.preventDefault();
        const uname = $("#username").value.trim();
        const pwd = $("#password").value;
        const user = db.users.find(u=>u.username === uname);
        const errorEl = $("#login-error");
        errorEl.textContent = "";
        if (!user) { errorEl.textContent = "Benutzername nicht gefunden."; return; }
        if (user.blocked) { errorEl.textContent = "Account gesperrt."; return; }
        if (user.password !== pwd) { errorEl.textContent = "Falsches Passwort."; return; }
        user.lastActive = Date.now();
        saveDB(db);
        state.loggedIn = true;
        state.user = user;
        state.showLogin = false;
        render();
      };
    }
    function registerModalEvents(db) {
      $("#close-register").onclick = ()=>{state.showRegister=false; render();};
      $("#to-login").onclick = e => {e.preventDefault(); state.showRegister=false; state.showLogin=true; render();};
      $("#register-form").onsubmit = e => {
        e.preventDefault();
        const uname = $("#reg-username").value.trim();
        const pwd = $("#reg-password").value;
        const errorEl = $("#reg-error");
        errorEl.textContent = "";
        if (uname.length < 3) { errorEl.textContent = "Benutzername zu kurz."; return; }
        if (pwd.length < 3) { errorEl.textContent = "Passwort zu kurz."; return; }
        if (db.users.some(u => u.username.toLowerCase() === uname.toLowerCase())) {
          errorEl.textContent = "Benutzername vergeben."; return;
        }
        db.users.push({
          username: uname,
          password: pwd,
          admin: false,
          blocked: false,
          agreed: true,
          created: Date.now(),
          lastActive: Date.now(),
          likes: [],
          subscriptions: [],
          subscribers: [],
          photo: ""
        });
        saveDB(db);
        state.showRegister = false;
        state.showLogin = true;
        render();
      };
    }
    function createModalEvents(db) {
      $("#close-create").onclick = ()=>{state.showCreate=false; render();};
      $("#create-form").onsubmit = e => {
        e.preventDefault();
        const errorEl = $("#create-error");
        errorEl.textContent = "";
        if(state.tipOrRecipe==="tip") {
          const text = $("#tip-text").value.trim();
          if(text.length<5){ errorEl.textContent="Tipp zu kurz!"; return; }
          db.tips.unshift({
            id: Math.max(0,...db.tips.map(t=>t.id))+1,
            text, author: state.user?state.user.username:"Gast"
          });
          saveDB(db);
          state.showCreate = false;
          render();
        } else {
          const title = $("#title").value.trim();
          let ingredients = $("#ingredients").value.split(",").map(s=>s.trim()).filter(Boolean);
          let steps = $("#steps").value.split(",").map(s=>s.trim()).filter(Boolean);
          const imgInput = $("#image");
          if (!title || !ingredients.length || !steps.length) { errorEl.textContent="Alle Pflichtfelder ausfüllen!"; return; }
          const newId = Date.now();
          if(imgInput.files[0]){
            const reader = new FileReader();
            reader.onload = e => {
              db.recipes.unshift({
                id: newId,
                title, author: state.user?state.user.username:"Gast",
                created: Date.now(),
                ingredients, steps, remixes:[], likes:[], image: e.target.result
              });
              saveDB(db);
              state.showCreate = false;
              render();
            };
            reader.readAsDataURL(imgInput.files[0]);
          } else {
            db.recipes.unshift({
              id: newId,
              title, author: state.user?state.user.username:"Gast",
              created: Date.now(),
              ingredients, steps, remixes:[], likes:[], image:""
            });
            saveDB(db);
            state.showCreate = false;
            render();
          }
        }
      };
    }

    // --- Tab-Bar
    function tabBarHTML() {
      return `<div class="tab-bar">
        <button class="${state.tab==="home"?"active":""}" data-tab="home">
          <span class="tab-icon">🏠</span><span>Home</span>
        </button>
        <button class="${state.tab==="search"?"active":""}" data-tab="search">
          <span class="tab-icon">🔎</span><span>Suche</span>
        </button>
        <button class="${state.tab==="machen"?"active":""}" data-tab="machen">
          <span class="tab-icon">✨</span><span>Machen</span>
        </button>
        <button class="${state.tab==="profile"?"active":""}" data-tab="profile">
          <span class="tab-icon">👤</span><span>Profil</span>
        </button>
        ${state.loggedIn && state.user && state.user.admin ? `
        <button class="${state.tab==="admin"?"active":""}" data-tab="admin">
          <span class="tab-icon">🛠️</span><span>Admin</span>
        </button>` : ""}
      </div>`;
    }

    // --- Hilfsfunktionen
    function $(sel, root=document) { return root.querySelector(sel); }
    function $all(sel, root=document) { return Array.from(root.querySelectorAll(sel)); }
    function formatDate(ts) {
      const d = new Date(ts);
      const pad = n => n.toString().padStart(2,"0");
      return `${pad(d.getDate())}.${pad(d.getMonth()+1)}.${d.getFullYear()}`;
    }

    render();
  </script>
</body>
</html>

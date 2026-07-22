<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EHEI Oujda — Espace Étudiant</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=IBM+Plex+Sans:wght@400;500;6
<style>
  :root{
    --navy-deep:#0B2138;
    --navy-mid:#14304A;
    --paper:#F3EFE4;
    --paper-dim:#E7E1D2;
    --brass:#C99A3E;
    --brass-bright:#E0B65A;
    --line:#3F5B76;
    --ink:#101B26;
    --ok:#5C8A6B;
    --warn:#C1673B;
    --font-display:'Space Grotesk',sans-serif;
    --font-body:'IBM Plex Sans',sans-serif;
    --font-mono:'IBM Plex Mono',monospace;
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  html,body{height:100%;}
  body{
    font-family:var(--font-body);
    background:var(--navy-deep);
    color:var(--paper);
    min-height:100vh;
    background-image:
      linear-gradient(rgba(201,154,62,0.06) 1px, transparent 1px),
      linear-gradient(90deg, rgba(201,154,62,0.06) 1px, transparent 1px);
    background-size:32px 32px;
  }
  .crosshair{position:fixed;width:18px;height:18px;pointer-events:none;opacity:.45;z-index:5;}
  .crosshair::before,.crosshair::after{content:'';position:absolute;background:var(--brass);}
  .crosshair::before{width:100%;height:1px;top:50%;left:0;}
  .crosshair::after{width:1px;height:100%;left:50%;top:0;}
  .ch-tl{top:14px;left:14px;} .ch-tr{top:14px;right:14px;} .ch-bl{bottom:14px;left:14px;} .ch-br{bottom:14px;right:14px;}


  a{color:inherit;}
  button{font-family:var(--font-body);cursor:pointer;}
  .visually-hidden{position:absolute;width:1px;height:1px;overflow:hidden;clip:rect(0,0,0,0);}


  /* ---------- LOGIN SCREEN ---------- */
  #login-screen{
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:24px;
  }
  .login-card{
    width:100%;
    max-width:420px;
    background:var(--navy-mid);
    border:1px solid var(--line);
    padding:40px 36px 34px;
    position:relative;
  }
  .login-card::before{
    content:'';
    position:absolute;
    inset:8px;
    border:1px solid rgba(201,154,62,0.35);
    pointer-events:none;
  }
  .login-eyebrow{
    font-family:var(--font-mono);
    font-size:11px;
    letter-spacing:.14em;
    color:var(--brass-bright);
    text-transform:uppercase;
    margin-bottom:14px;
  }
  .login-title{
    font-family:var(--font-display);
    font-size:28px;
    font-weight:700;
    line-height:1.15;
    margin-bottom:6px;
  }
  .login-sub{
    font-size:14px;
    color:#B9C6D3;
    margin-bottom:30px;
  }
  .field{margin-bottom:20px;}
  .field label{
    display:block;
    font-family:var(--font-mono);
    font-size:11px;
    letter-spacing:.08em;
    text-transform:uppercase;
    color:#9FB4C7;
    margin-bottom:8px;
  }
  .field input{
    width:100%;
    background:var(--navy-deep);
    border:1px solid var(--line);
    color:var(--paper);
    font-family:var(--font-mono);
    font-size:15px;
    padding:12px 14px;
    outline:none;
    transition:border-color .15s;
  }
  .field input:focus{border-color:var(--brass-bright);}
  .field input::placeholder{color:#5A7286;}
  #login-error{
    display:none;
    font-family:var(--font-mono);
    font-size:12.5px;
    color:var(--warn);
    margin-bottom:16px;
    border-left:2px solid var(--warn);
    padding-left:10px;
  }
  .btn-primary{
    width:100%;
    background:var(--brass);
    color:var(--navy-deep);
    border:none;
    font-family:var(--font-display);
    font-weight:700;
    font-size:15px;
    letter-spacing:.03em;
    padding:14px;
    text-transform:uppercase;
    transition:background .15s;
  }
  .btn-primary:hover{background:var(--brass-bright);}
  .btn-primary:focus-visible, a:focus-visible, button:focus-visible, input:focus-visible{
    outline:2px solid var(--brass-bright); outline-offset:2px;
  }
  .login-foot{
    margin-top:22px;
    font-size:12px;
    color:#7C90A2;
    display:flex;
    justify-content:space-between;
    font-family:var(--font-mono);
  }
  .school-mark{
    display:flex;
    align-items:center;
    gap:10px;
    margin-bottom:34px;
  }
  .school-mark .badge{
    width:38px;height:38px;
    border:1.5px solid var(--brass);
    display:flex;align-items:center;justify-content:center;
    font-family:var(--font-display);font-weight:700;font-size:14px;
    color:var(--brass-bright);
    transform:rotate(45deg);
    flex-shrink:0;
  }
  .school-mark .badge span{transform:rotate(-45deg);}
  .school-mark .name{font-family:var(--font-mono);font-size:12px;letter-spacing:.1em;color:#B9C6D3;text-transform:uppercas


  /* ---------- WELCOME TOAST ---------- */
  #welcome-flash{
    position:fixed;
    inset:0;
    background:var(--navy-deep);
    display:none;
    align-items:center;
    justify-content:center;
    z-index:100;
    flex-direction:column;
    text-align:center;
    padding:24px;
  }
  #welcome-flash .stamp{
    font-family:var(--font-mono);
    font-size:12px;
    letter-spacing:.2em;
    color:var(--brass-bright);
    text-transform:uppercase;
    margin-bottom:18px;
    opacity:0;
    animation:fadeUp .5s ease forwards .1s;
  }
  #welcome-flash h1{
    font-family:var(--font-display);
    font-size:clamp(30px,6vw,52px);
    font-weight:700;
    opacity:0;
    animation:fadeUp .6s ease forwards .3s;
  }
  #welcome-flash .sub{
    margin-top:14px;
    color:#B9C6D3;
    font-size:15px;
    opacity:0;
    animation:fadeUp .6s ease forwards .55s;
  }
  @keyframes fadeUp{from{opacity:0;transform:translateY(10px);}to{opacity:1;transform:translateY(0);}}


  /* ---------- APP SHELL ---------- */
  #app{display:none;min-height:100vh;}
  .topbar{
    display:flex;
    align-items:center;
    justify-content:space-between;
    padding:16px 28px;
    border-bottom:1px solid var(--line);
    background:var(--navy-mid);
    position:sticky;top:0;z-index:20;
  }
  .topbar .school-mark{margin:0;}
  .topbar .school-mark .badge{width:32px;height:32px;font-size:12px;}
  .topbar-right{display:flex;align-items:center;gap:18px;}
  .user-chip{
    font-family:var(--font-mono);
    font-size:12.5px;
    color:#DCE4EA;
    display:flex;align-items:center;gap:8px;
  }
  .user-chip .dot{width:7px;height:7px;background:var(--ok);border-radius:50%;}
  .btn-ghost{
    background:transparent;
    border:1px solid var(--line);
    color:var(--paper);
    font-family:var(--font-mono);
    font-size:12px;
    padding:8px 14px;
    letter-spacing:.05em;
    text-transform:uppercase;
    transition:border-color .15s,color .15s;
  }
  .btn-ghost:hover{border-color:var(--brass);color:var(--brass-bright);}


  .layout{display:flex;max-width:1240px;margin:0 auto;}
  nav.sidenav{
    width:220px;
    flex-shrink:0;
    padding:28px 12px;
    border-right:1px solid var(--line);
    position:sticky;
    top:65px;
    align-self:flex-start;
    height:calc(100vh - 65px);
  }
  nav.sidenav .navlabel{
    font-family:var(--font-mono);
    font-size:10.5px;
    letter-spacing:.14em;
    text-transform:uppercase;
    color:#65798C;
    padding:0 12px;
    margin-bottom:10px;
  }
  nav.sidenav button{
    display:flex;
    align-items:center;
    gap:10px;
    width:100%;
    text-align:left;
    background:transparent;
    border:none;
    color:#B9C6D3;
    font-family:var(--font-body);
    font-size:14px;
    padding:11px 12px;
    margin-bottom:2px;
    border-left:2px solid transparent;
    transition:all .15s;
  }
  nav.sidenav button .idx{font-family:var(--font-mono);font-size:11px;color:#5A7286;}
  nav.sidenav button:hover{color:var(--paper);background:rgba(201,154,62,0.06);}
  nav.sidenav button.active{
    color:var(--brass-bright);
    border-left-color:var(--brass);
    background:rgba(201,154,62,0.08);
  }
  nav.sidenav button.active .idx{color:var(--brass-bright);}


  main{flex:1;padding:36px 40px 80px;min-width:0;}
  .view{display:none;}
  .view.active{display:block;animation:fadeUp .35s ease;}


  .view-head{margin-bottom:30px;}
  .view-eyebrow{
    font-family:var(--font-mono);
    font-size:11px;
    letter-spacing:.14em;
    color:var(--brass-bright);
    text-transform:uppercase;
    margin-bottom:10px;
  }
  .view-title{
    font-family:var(--font-display);
    font-size:clamp(24px,3.4vw,34px);
    font-weight:700;
  }
  .view-desc{color:#B9C6D3;font-size:14.5px;margin-top:8px;max-width:60ch;}


  /* Accueil hero */
  .hero-panel{
    border:1px solid var(--line);
    padding:30px;
    background:var(--navy-mid);
    margin-bottom:24px;
    position:relative;
  }
  .hero-panel .readout{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(140px,1fr));
    gap:20px;
    margin-top:24px;
    border-top:1px solid var(--line);
    padding-top:22px;
  }
  .readout .item .k{font-family:var(--font-mono);font-size:10.5px;letter-spacing:.1em;color:#7C90A2;text-transform:upperca
  .readout .item .v{font-family:var(--font-display);font-size:22px;font-weight:600;color:var(--paper);}
  .readout .item .v.brass{color:var(--brass-bright);}


  .card-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(230px,1fr));gap:16px;}
  .card{
    border:1px solid var(--line);
    background:var(--navy-mid);
    padding:22px 20px 22px 20px;
    transition:transform .2s, border-color .15s, background .15s, box-shadow .15s;
    cursor:pointer;
    position:relative;
    overflow:hidden;
  }
  .card:hover{
    border-color:var(--brass);
    transform:translateY(-3px);
    background:rgba(201,154,62,0.08);
    box-shadow:0 16px 30px rgba(0,0,0,0.08);
  }
  .card .card-icon{
    display:inline-flex;
    align-items:center;
    justify-content:center;
    width:36px;
    height:36px;
    border-radius:10px;
    background:rgba(201,154,62,0.14);
    color:var(--brass-bright);
    font-size:17px;
    margin-bottom:14px;
  }
  .card .tag{font-family:var(--font-mono);font-size:10px;color:var(--brass-bright);letter-spacing:.08em;text-transform:uppe
  .card h3{font-family:var(--font-display);font-size:16px;margin-bottom:6px;}
  .card p{font-size:13px;color:#AEBECC;line-height:1.6;}


  .hero-icons{display:flex;flex-wrap:wrap;gap:12px;margin-bottom:18px;}
  .hero-chip{
    display:flex;align-items:center;gap:10px;
    background:rgba(255,255,255,0.06);
    border:1px solid rgba(201,154,62,0.16);
    color:#D8E2EA;
    padding:12px 14px;
    border-radius:12px;
    font-size:13px;
  }
  .hero-chip .symbol{
    width:34px;height:34px;
    display:flex;align-items:center;justify-content:center;
    border-radius:10px;
    background:rgba(201,154,62,0.16);
    color:var(--brass-bright);
    font-size:16px;
  }


  /* Filieres / accordion */
  .year-block{border:1px solid var(--line);margin-bottom:12px;background:var(--navy-mid);}
  .year-head{
    width:100%;display:flex;align-items:center;justify-content:space-between;
    background:transparent;border:none;color:var(--paper);
    padding:18px 20px;font-family:var(--font-display);font-size:16px;font-weight:600;
    cursor:pointer;
    transition:background .15s, color .15s;
  }
  .year-head:hover{background:rgba(201,154,62,0.06);color:var(--paper);}
  .year-head .coord{font-family:var(--font-mono);font-size:11px;color:var(--brass-bright);margin-right:auto;margin-left:14p
  .year-head .chevron{font-family:var(--font-mono);color:var(--brass-bright);transition:transform .2s;}
  .year-block.open .chevron{transform:rotate(45deg);}
  .year-body{display:none;padding:0 20px 20px;}
  .year-block.open .year-body{display:block;}
  .sem{margin-bottom:16px;}
  .sem-title{font-family:var(--font-mono);font-size:11px;letter-spacing:.1em;color:#7C90A2;text-transform:uppercase;margin
  .mod-list{display:flex;flex-direction:column;gap:6px;}
  .mod-row{display:flex;justify-content:space-between;font-size:13.5px;padding:10px 0;border-bottom:1px dashed rgba(159,18
  .mod-row:hover{background:rgba(201,154,62,0.06);}
  .mod-row .coef{font-family:var(--font-mono);color:#7C90A2;font-size:12px;}


  /* Table results */
  .term-select{display:flex;gap:8px;margin-bottom:22px;flex-wrap:wrap;}
  .term-select button{
    background:transparent;border:1px solid var(--line);color:#B9C6D3;
    font-family:var(--font-mono);font-size:12px;padding:8px 14px;letter-spacing:.04em;
  }
  .term-select button.active{border-color:var(--brass);color:var(--brass-bright);background:rgba(201,154,62,0.08);}
  table.grades{width:100%;border-collapse:collapse;font-size:13.5px;}
  table.grades th{
    text-align:left;font-family:var(--font-mono);font-size:10.5px;letter-spacing:.08em;
    text-transform:uppercase;color:#7C90A2;padding:10px 14px;border-bottom:1px solid var(--line);
  }
  table.grades td{padding:12px 14px;border-bottom:1px solid rgba(63,91,118,0.4);}
  table.grades tr:hover td{background:rgba(201,154,62,0.05);}
  .grade-val{font-family:var(--font-mono);font-weight:600;}
  .grade-val.good{color:var(--ok);}
  .grade-val.mid{color:var(--brass-bright);}
  .grade-val.low{color:var(--warn);}
  .gpa-panel{
    display:flex;gap:24px;margin-top:20px;padding:18px 20px;
    border:1px solid var(--brass);background:rgba(201,154,62,0.06);
    flex-wrap:wrap;
  }
  .gpa-panel .item .k{font-family:var(--font-mono);font-size:10px;color:#B9C6D3;text-transform:uppercase;letter-spacing:.0
  .gpa-panel .item .v{font-family:var(--font-display);font-size:24px;font-weight:700;color:var(--brass-bright);margin-top:4


  /* Contact */
  .contact-grid{display:grid;grid-template-columns:1.1fr 1fr;gap:24px;}
  @media (max-width:800px){.contact-grid{grid-template-columns:1fr;}}
  .contact-info .row{display:flex;gap:14px;padding:16px 0;border-bottom:1px solid rgba(63,91,118,0.4);}
  .contact-info .row .k{font-family:var(--font-mono);font-size:10.5px;color:#7C90A2;text-transform:uppercase;letter-spacin
  .contact-info .row .v{font-size:14px;color:var(--paper);line-height:1.5;}
  .contact-form{border:1px solid var(--line);background:var(--navy-mid);padding:26px;}
  .contact-form .field textarea{
    width:100%;background:var(--navy-deep);border:1px solid var(--line);color:var(--paper);
    font-family:var(--font-body);font-size:14px;padding:12px 14px;min-height:100px;resize:vertical;outline:none;
  }
  .contact-form .field textarea:focus{border-color:var(--brass-bright);}
  #contact-sent{display:none;font-family:var(--font-mono);font-size:12.5px;color:var(--ok);margin-top:14px;border-left:2px 


  /* mobile nav */
  .mobile-tabs{display:none;}
  @media (max-width:880px){
    nav.sidenav{display:none;}
    .mobile-tabs{
      display:flex;overflow-x:auto;gap:6px;padding:12px 16px;
      border-bottom:1px solid var(--line);background:var(--navy-mid);position:sticky;top:65px;z-index:19;
    }
    .mobile-tabs button{
      flex-shrink:0;background:transparent;border:1px solid var(--line);color:#B9C6D3;
      font-family:var(--font-mono);font-size:11.5px;padding:8px 12px;white-space:nowrap;
    }
    .mobile-tabs button.active{border-color:var(--brass);color:var(--brass-bright);}
    main{padding:26px 18px 60px;}
    .topbar{padding:14px 16px;}
    .contact-grid{gap:18px;}
  }
  .crosshair{display:none;}
  @media (min-width:640px){.crosshair{display:block;}}
</style>
</head>
<body>


<div class="crosshair ch-tl"></div>
<div class="crosshair ch-tr"></div>
<div class="crosshair ch-bl"></div>
<div class="crosshair ch-br"></div>


<!-- ================= LOGIN SCREEN ================= -->
<section id="login-screen">
  <div class="login-card">
    <div class="school-mark">
      <div class="badge"><span>EH</span></div>
      <div class="name">EHEI — Oujda</div>
    </div>
    <div class="login-eyebrow">Espace étudiant</div>
    <h1 class="login-title">Connexion à votre portail</h1>
    <p class="login-sub">École des Hautes Études d'Ingénierie — accédez à vos modules, résultats et informations administra


    <form id="login-form" novalidate>
      <div class="field">
        <label for="login-name">Nom complet</label>
        <input type="text" id="login-name" placeholder="ex. Yassine El Amrani" autocomplete="name" required>
      </div>
      <div class="field">
        <label for="login-pass">Mot de passe</label>
        <input type="password" id="login-pass" placeholder="••••••••" autocomplete="current-password" required>
      </div>
      <p id="login-error">Veuillez renseigner votre nom et votre mot de passe.</p>
      <button type="submit" class="btn-primary">Se connecter</button>
    </form>


    <div class="login-foot">
      <span>Décret n° 2.21.934 — MESRS</span>
      <span>Oujda, Maroc</span>
    </div>
  </div>
</section>


<!-- ================= WELCOME FLASH ================= -->
<div id="welcome-flash">
  <div class="stamp">Authentification réussie</div>
  <h1>Bienvenue, <span id="welcome-name">—</span></h1>
  <p class="sub">Redirection vers votre espace étudiant…</p>
</div>


<!-- ================= APP ================= -->
<div id="app">
  <div class="topbar">
    <div class="school-mark">
      <div class="badge"><span>EH</span></div>
      <div class="name">EHEI — Espace étudiant</div>
    </div>
    <div class="topbar-right">
      <div class="user-chip"><span class="dot"></span><span id="chip-name">—</span></div>
      <button class="btn-ghost" id="logout-btn">Déconnexion</button>
    </div>
  </div>


  <div class="mobile-tabs" id="mobile-tabs"></div>


  <div class="layout">
    <nav class="sidenav" id="sidenav">
      <div class="navlabel">Navigation</div>
    </nav>


    <main>
      <!-- ACCUEIL -->
      <section class="view active" id="view-accueil">
        <div class="view-head">
          <div class="view-eyebrow">01 — Accueil</div>
          <h1 class="view-title">Bienvenue sur votre portail, <span id="hero-name">Étudiant</span></h1>
          <p class="view-desc">Retrouvez ici un aperçu de votre parcours à l'EHEI : filière, année en cours et statut admin
        </div>


        <div class="hero-panel">
          <div class="hero-icons">
            <div class="hero-chip"><span class="symbol">🏫</span><span><strong>EHEI</strong> — Campus ingénierie</span></di
            <div class="hero-chip"><span class="symbol">⚙️</span><span><strong>Ingénierie</strong> & innovation</span></div
            <div class="hero-chip"><span class="symbol">📐</span><span><strong>Modules</strong> techniques</span></div>
          </div>
          <div class="view-eyebrow" style="margin-bottom:4px;">Fiche étudiant</div>
          <div class="readout">
            <div class="item"><div class="k">Filière</div><div class="v">Génie Informatique</div></div>
            <div class="item"><div class="k">Année</div><div class="v brass">3ᵉ année ingénieur</div></div>
            <div class="item"><div class="k">Semestre en cours</div><div class="v">S6</div></div>
            <div class="item"><div class="k">Statut</div><div class="v" style="color:#5C8A6B;">Inscrit — à jour</div></div
          </div>
        </div>


        <div class="card-grid">
          <div class="card" data-view="filieres" aria-label="Voir le programme par année">
            <div class="card-icon">📚</div>
            <div class="tag">Filières & modules</div>
            <h3>Programme par année</h3>
            <p>Consultez les modules enseignés chaque semestre, de la 1ʳᵉ à la 5ᵉ année.</p>
          </div>
          <div class="card" data-view="resultats" aria-label="Voir mes résultats">
            <div class="card-icon">📊</div>
            <div class="tag">Résultats</div>
            <h3>Mes notes & moyennes</h3>
            <p>Suivez vos notes par module et votre moyenne générale à chaque semestre.</p>
          </div>
          <div class="card" data-view="optionnels" aria-label="Voir les modules optionnels">
            <div class="card-icon">🧠</div>
            <div class="tag">Modules optionnels</div>
            <h3>Filières modernes</h3>
            <p>IA, cybersécurité, cloud, data — choisissez vos options selon votre profil.</p>
          </div>
          <div class="card" data-view="contact" aria-label="Contacter l'école">
            <div class="card-icon">🏫</div>
            <div class="tag">Administration</div>
            <h3>Contacter l'école</h3>
            <p>Une question administrative ? L'équipe de l'EHEI vous répond.</p>
          </div>
        </div>
      </section>


      <!-- FILIERES / TERMS PER YEAR -->
      <section class="view" id="view-filieres">
        <div class="view-head">
          <div class="view-eyebrow">02 — Programme</div>
          <h1 class="view-title">Modules par année et par semestre</h1>
          <p class="view-desc">Le cursus ingénieur EHEI se déroule sur 5 années, chacune divisée en deux semestres.</p>
        </div>
        <div id="years-container"></div>
      </section>


      <!-- RESULTATS -->
      <section class="view" id="view-resultats">
        <div class="view-head">
          <div class="view-eyebrow">03 — Résultats</div>
          <h1 class="view-title">Mes notes et moyennes</h1>
          <p class="view-desc">Sélectionnez un semestre pour consulter le détail de vos notes.</p>
        </div>
        <div class="term-select" id="term-select"></div>
        <table class="grades">
          <thead>
            <tr><th>Module</th><th>Coefficient</th><th>Note / 20</th><th>Mention</th></tr>
          </thead>
          <tbody id="grades-body"></tbody>
        </table>
        <div class="gpa-panel">
          <div class="item"><div class="k">Moyenne du semestre</div><div class="v" id="term-avg">—</div></div>
          <div class="item"><div class="k">Moyenne générale (année)</div><div class="v" id="year-avg">—</div></div>
          <div class="item"><div class="k">Résultat</div><div class="v" id="term-status" style="font-size:16px;">—</div></d
        </div>
      </section>


      <!-- MODULES OPTIONNELS -->
      <section class="view" id="view-optionnels">
        <div class="view-head">
          <div class="view-eyebrow">04 — Filières modernes</div>
          <h1 class="view-title">Modules optionnels</h1>
          <p class="view-desc">En 4ᵉ et 5ᵉ année, choisissez une spécialisation parmi ces modules modernes proposés par l'E
        </div>
        <div class="card-grid" id="optionnels-grid"></div>
      </section>


      <!-- CONTACT -->
      <section class="view" id="view-contact">
        <div class="view-head">
          <div class="view-eyebrow">05 — Contact</div>
          <h1 class="view-title">Contacter l'administration</h1>
          <p class="view-desc">Une question sur votre dossier, un stage ou une démarche administrative ? Écrivez-nous.</p>
        </div>
        <div class="contact-grid">
          <div class="contact-info">
            <div class="row"><div class="k">Adresse</div><div class="v">Rue de la Liberté — Hay Al Hikma, Oujda, Maroc</div
            <div class="row"><div class="k">Téléphone</div><div class="v">+212 536 533 076<br>+212 661 644 095</div></div>
            <div class="row"><div class="k">Email</div><div class="v">ehei.oujda@gmail.com</div></div>
            <div class="row"><div class="k">Site officiel</div><div class="v"><a href="https://ehei.ac.ma/" target="_blank"
            <div class="row"><div class="k">Horaires</div><div class="v">Lundi – Vendredi, 9h00 – 17h00</div></div>
          </div>
          <form class="contact-form" id="contact-form">
            <div class="field">
              <label for="c-subject">Objet</label>
              <input type="text" id="c-subject" placeholder="ex. Attestation de scolarité" required>
            </div>
            <div class="field">
              <label for="c-message">Message</label>
              <textarea id="c-message" placeholder="Décrivez votre demande…" required></textarea>
            </div>
            <button type="submit" class="btn-primary">Envoyer le message</button>
            <p id="contact-sent">Message transmis à l'administration. Réponse sous 48h ouvrées.</p>
          </form>
        </div>
      </section>
    </main>
  </div>
</div>


<script>
// ---------------- DATA ----------------
const NAV = [
  {id:'accueil', label:'Accueil'},
  {id:'filieres', label:'Programme par année'},
  {id:'resultats', label:'Mes résultats'},
  {id:'optionnels', label:'Modules optionnels'},
  {id:'contact', label:'Contact'}
];


const YEARS = [
  {year:1, title:'1ʳᵉ année — Tronc commun', S1:[['Analyse mathématique',5],['Algèbre linéaire',4],['Algorithmique & C',5],
    S2:[['Probabilités & statistiques',4],['Électronique de base',4],['Programmation orientée objet',5],['Économie & gestio
  {year:2, title:'2ᵉ année — Tronc commun', S1:[['Structures de données',5],['Systèmes d\'exploitation',4],['Bases de donné
    S2:[['Génie logiciel',5],['Architecture des ordinateurs',4],['Mathématiques discrètes',3],['Administration systèmes',4]
  {year:3, title:'3ᵉ année — Spécialisation', S1:[['Développement web avancé',5],['Intelligence artificielle — fondamentaux
    S2:[['Cloud computing',5],['Ingénierie logicielle avancée',4],['Bases de données avancées',4],['Symfony & frameworks PH
  {year:4, title:'4ᵉ année — Ingénieur', S1:[['Data science',5],['Architecture microservices',4],['DevOps & CI/CD',4],['Man
    S2:[['Projet d\'ingénierie',6],['Salesforce & CRM',4],['SAP — systèmes d\'information',4],['Droit du numérique',2],['Mo
  {year:5, title:'5ᵉ année — Projet de fin d\'études', S1:[['Recherche opérationnelle',4],['Innovation & entrepreneuriat',3
    S2:[['Projet de fin d\'études (PFE)',10],['Soutenance & stage entreprise',8]]}
];


const OPTIONS = [
  {tag:'IA', title:'Intelligence Artificielle & Machine Learning', desc:'Apprentissage automatique, deep learning et traite
  {tag:'Cyber', title:'Cybersécurité & Cyberdéfense', desc:'Sécurisation des systèmes, tests d\'intrusion et gouvernance de
  {tag:'Cloud', title:'Cloud & DevOps', desc:'Infrastructures cloud, conteneurisation et automatisation du déploiement.'},
  {tag:'Data', title:'Data Engineering & Big Data', desc:'Conception de pipelines de données et architectures big data pour
  {tag:'Réseaux', title:'Réseaux & Télécoms', desc:'Conception, administration et sécurisation des infrastructures réseaux 
  {tag:'Mgmt', title:'Management de Projets IT', desc:'Pilotage de projets numériques avec les méthodologies agiles et hybr
];


const TERMS = ['S1','S2','S3','S4','S5','S6'];
// mock grades per term: [module, coef, note]
const GRADES = {
  S1:[['Analyse mathématique',5,14.5],['Algèbre linéaire',4,13],['Algorithmique & C',5,16],['Physique appliquée',3,11.5],['
  S2:[['Probabilités & statistiques',4,12],['Électronique de base',4,10.5],['Programmation orientée objet',5,17],['Économie
  S3:[['Structures de données',5,15],['Systèmes d\'exploitation',4,12.5],['Bases de données',5,14],['Réseaux informatiques'
  S4:[['Génie logiciel',5,16.5],['Architecture des ordinateurs',4,11],['Mathématiques discrètes',3,10],['Administration sys
  S5:[['Développement web avancé',5,15],['IA — fondamentaux',5,14],['Sécurité informatique',4,12.5],['Gestion de projet agi
  S6:[['Cloud computing',5,13.5],['Ingénierie logicielle avancée',4,14],['Bases de données avancées',4,12],['Symfony & fram
};


let currentTerm = 'S6';
let studentName = '';


// ---------------- LOGIN ----------------
const loginForm = document.getElementById('login-form');
const loginError = document.getElementById('login-error');


loginForm.addEventListener('submit', function(e){
  e.preventDefault();
  const name = document.getElementById('login-name').value.trim();
  const pass = document.getElementById('login-pass').value;
  if(!name || !pass){
    loginError.style.display = 'block';
    return;
  }
  loginError.style.display = 'none';
  studentName = name;
  showWelcome(name);
});


function showWelcome(name){
  document.getElementById('login-screen').style.display = 'none';
  const flash = document.getElementById('welcome-flash');
  document.getElementById('welcome-name').textContent = name;
  flash.style.display = 'flex';
  setTimeout(function(){
    flash.style.display = 'none';
    document.getElementById('chip-name').textContent = name;
    document.getElementById('hero-name').textContent = name.split(' ')[0];
    document.getElementById('app').style.display = 'block';
  }, 2000);
}


// ---------------- NAV ----------------
const sidenav = document.getElementById('sidenav');
const mobileTabs = document.getElementById('mobile-tabs');


NAV.forEach(function(item, i){
  const btn = document.createElement('button');
  btn.innerHTML = '<span class="idx">' + String(i+1).padStart(2,'0') + '</span>' + item.label;
  btn.dataset.view = item.id;
  btn.addEventListener('click', function(){ switchView(item.id); });
  sidenav.appendChild(btn);


  const mbtn = document.createElement('button');
  mbtn.textContent = item.label;
  mbtn.dataset.view = item.id;
  mbtn.addEventListener('click', function(){ switchView(item.id); });
  mobileTabs.appendChild(mbtn);
});


function switchView(id){
  document.querySelectorAll('.view').forEach(function(v){ v.classList.remove('active'); });
  document.getElementById('view-' + id).classList.add('active');
  document.querySelectorAll('nav.sidenav button, .mobile-tabs button').forEach(function(b){
    b.classList.toggle('active', b.dataset.view === id);
  });
  window.scrollTo({top:0, behavior:'smooth'});
}
switchView('accueil');


document.querySelectorAll('.card[data-view]').forEach(function(card){
  card.addEventListener('click', function(){
    switchView(this.dataset.view);
  });
});


document.getElementById('logout-btn').addEventListener('click', function(){
  document.getElementById('app').style.display = 'none';
  document.getElementById('login-screen').style.display = 'flex';
  loginForm.reset();
  switchView('accueil');
});


// ---------------- FILIERES / YEARS ----------------
const yearsContainer = document.getElementById('years-container');
YEARS.forEach(function(y, idx){
  const block = document.createElement('div');
  block.className = 'year-block' + (idx===2 ? ' open' : '');
  block.innerHTML =
    '<button class="year-head">' + y.title +
      '<span class="coord">AN.' + y.year + '</span>' +
      '<span class="chevron">+</span>' +
    '</button>' +
    '<div class="year-body">' +
      '<div class="sem"><div class="sem-title">Semestre ' + (y.year*2-1) + '</div><div class="mod-list">' +
        y.S1.map(function(m){ return '<div class="mod-row"><span>' + m[0] + '</span><span class="coef">coef. ' + m[1] + '</
      '</div></div>' +
      '<div class="sem"><div class="sem-title">Semestre ' + (y.year*2) + '</div><div class="mod-list">' +
        y.S2.map(function(m){ return '<div class="mod-row"><span>' + m[0] + '</span><span class="coef">coef. ' + m[1] + '</
      '</div></div>' +
    '</div>';
  block.querySelector('.year-head').addEventListener('click', function(){
    block.classList.toggle('open');
  });
  yearsContainer.appendChild(block);
});


// ---------------- OPTIONS ----------------
const optionsGrid = document.getElementById('optionnels-grid');
OPTIONS.forEach(function(o){
  const card = document.createElement('div');
  card.className = 'card';
  card.innerHTML = '<div class="tag">' + o.tag + '</div><h3>' + o.title + '</h3><p>' + o.desc + '</p>';
  optionsGrid.appendChild(card);
});


// ---------------- RESULTATS ----------------
const termSelect = document.getElementById('term-select');
TERMS.forEach(function(t){
  const btn = document.createElement('button');
  btn.textContent = t;
  btn.dataset.term = t;
  if(t === currentTerm) btn.classList.add('active');
  btn.addEventListener('click', function(){
    currentTerm = t;
    document.querySelectorAll('.term-select button').forEach(function(b){ b.classList.toggle('active', b.dataset.term === t
    renderGrades();
  });
  termSelect.appendChild(btn);
});


function mention(note){
  if(note >= 16) return 'Très bien';
  if(note >= 14) return 'Bien';
  if(note >= 12) return 'Assez bien';
  if(note >= 10) return 'Passable';
  return 'Insuffisant';
}
function gradeClass(note){
  if(note >= 14) return 'good';
  if(note >= 10) return 'mid';
  return 'low';
}


function renderGrades(){
  const rows = GRADES[currentTerm];
  const body = document.getElementById('grades-body');
  body.innerHTML = rows.map(function(r){
    return '<tr><td>' + r[0] + '</td><td class="coef">coef. ' + r[1] + '</td>' +
      '<td class="grade-val ' + gradeClass(r[2]) + '">' + r[2].toFixed(1) + '</td>' +
      '<td>' + mention(r[2]) + '</td></tr>';
  }).join('');


  let sumW = 0, sum = 0;
  rows.forEach(function(r){ sum += r[1]*r[2]; sumW += r[1]; });
  const avg = sum / sumW;
  document.getElementById('term-avg').textContent = avg.toFixed(2) + ' / 20';
  document.getElementById('year-avg').textContent = avg.toFixed(2) + ' / 20';
  const statusEl = document.getElementById('term-status');
  if(avg >= 10){
    statusEl.textContent = 'Validé';
    statusEl.style.color = '#5C8A6B';
  } else {
    statusEl.textContent = 'Non validé';
    statusEl.style.color = '#C1673B';
  }
}
renderGrades();


// ---------------- CONTACT ----------------
document.getElementById('contact-form').addEventListener('submit', function(e){
  e.preventDefault();
  document.getElementById('contact-sent').style.display = 'block';
  this.reset();
});
</script>
</body>
</html>


---
layout: null
---
<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Terravend B.V.</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />

  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --sand:    #f5f0e8;
      --cream:   #faf7f2;
      --stone:   #c8b89a;
      --earth:   #7a6650;
      --dark:    #1e1a16;
      --ink:     #2d2720;
      --muted:   #9b8f83;
      --accent:  #4a7c6f;
    }

    html { scroll-behavior: smooth; }

    body {
      font-family: 'DM Sans', sans-serif;
      background: var(--cream);
      color: var(--ink);
      overflow-x: hidden;
    }

    /* ── CURSOR ── */
    body { cursor: none; }
    #cursor {
      position: fixed;
      width: 10px; height: 10px;
      background: var(--accent);
      border-radius: 50%;
      pointer-events: none;
      z-index: 9999;
      transform: translate(-50%, -50%);
      transition: transform 0.1s, width 0.3s, height 0.3s, background 0.3s;
    }
    #cursor-ring {
      position: fixed;
      width: 36px; height: 36px;
      border: 1px solid var(--stone);
      border-radius: 50%;
      pointer-events: none;
      z-index: 9998;
      transform: translate(-50%, -50%);
      transition: transform 0.18s ease, width 0.3s, height 0.3s;
    }
    body:hover #cursor { opacity: 1; }

    /* ── NOISE TEXTURE OVERLAY ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 1000;
      opacity: 0.4;
    }

    /* ── NAV ── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      padding: 1.6rem 3rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 100;
      mix-blend-mode: normal;
      background: rgba(250,247,242,0.92);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border-bottom: 1px solid rgba(200,184,154,0.18);
      opacity: 0;
      transform: translateY(-10px);
      animation: navReveal 0.7s ease 0.1s forwards;
    }
    @keyframes navReveal {
      to { opacity: 1; transform: translateY(0); }
    }

    .nav-logo {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      font-weight: 600;
      letter-spacing: 0.04em;
      color: var(--dark);
      text-decoration: none;
    }
    .nav-logo span { color: var(--accent); }

    nav ul {
      list-style: none;
      display: flex;
      gap: 2.5rem;
    }
    nav ul li a {
      font-size: 0.8rem;
      font-weight: 400;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
      text-decoration: none;
      transition: color 0.2s;
    }
    nav ul li a:hover { color: var(--ink); }

    /* ── HERO ── */
    .hero {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      position: relative;
      overflow: hidden;
    }

    .hero-left {
      display: flex;
      flex-direction: column;
      justify-content: flex-end;
      padding: 12rem 5rem 7rem 5rem;
      position: relative;
      z-index: 2;
    }

    .hero-eyebrow {
      font-size: 0.72rem;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--accent);
      font-weight: 500;
      margin-bottom: 1.8rem;
      opacity: 0;
      animation: fadeUp 0.8s ease 0.3s forwards;
    }

    .hero-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(3.5rem, 7vw, 7rem);
      font-weight: 300;
      line-height: 1.0;
      letter-spacing: -0.01em;
      color: var(--dark);
      opacity: 0;
      animation: fadeUp 0.9s ease 0.5s forwards;
    }

    .hero-title em {
      font-style: italic;
      color: var(--accent);
    }

    .hero-sub {
      margin-top: 2.5rem;
      font-size: 0.95rem;
      line-height: 1.75;
      color: var(--muted);
      max-width: 380px;
      font-weight: 300;
      opacity: 0;
      animation: fadeUp 0.9s ease 0.7s forwards;
    }

    .hero-cta {
      margin-top: 3.5rem;
      display: flex;
      gap: 1.2rem;
      align-items: center;
      opacity: 0;
      animation: fadeUp 0.9s ease 0.9s forwards;
    }

    .btn-primary {
      display: inline-block;
      padding: 0.85rem 2.2rem;
      background: var(--dark);
      color: var(--cream);
      font-size: 0.78rem;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      text-decoration: none;
      font-weight: 400;
      transition: background 0.25s, color 0.25s;
    }
    .btn-primary:hover { background: var(--accent); }

    .btn-ghost {
      display: inline-block;
      font-size: 0.78rem;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--muted);
      text-decoration: none;
      font-weight: 400;
      transition: color 0.2s;
    }
    .btn-ghost:hover { color: var(--ink); }

    .hero-right {
      position: relative;
      background: var(--sand);
      overflow: hidden;
    }

    .hero-right::before {
      content: '';
      position: absolute;
      inset: 0;
      background:
        radial-gradient(ellipse 60% 70% at 60% 40%, rgba(74,124,111,0.12) 0%, transparent 70%),
        linear-gradient(160deg, #e8e0d2 0%, #d4c8b5 100%);
    }

    .hero-right-inner {
      position: absolute;
      inset: 0;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    /* Geometric logo mark */
    .logo-mark {
      width: 220px;
      height: 220px;
      position: relative;
      opacity: 0;
      animation: fadeIn 1.2s ease 0.8s forwards;
    }

    .logo-mark svg {
      width: 100%;
      height: 100%;
    }

    .hero-right .watermark {
      position: absolute;
      bottom: 3rem;
      right: 3rem;
      font-family: 'Cormorant Garamond', serif;
      font-size: 0.7rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--stone);
      writing-mode: vertical-rl;
      text-orientation: mixed;
    }

    .scroll-line {
      position: absolute;
      bottom: 2.5rem;
      left: 5rem;
      display: flex;
      align-items: center;
      gap: 1rem;
      font-size: 0.7rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--stone);
      opacity: 0;
      animation: fadeIn 1s ease 1.4s forwards;
    }
    .scroll-line::before {
      content: '';
      display: block;
      width: 40px;
      height: 1px;
      background: var(--stone);
      animation: lineGrow 1s ease 1.6s both;
    }
    @keyframes lineGrow {
      from { width: 0; } to { width: 40px; }
    }

    /* ── ABOUT ── */
    .about {
      padding: 10rem 5rem;
      display: grid;
      grid-template-columns: 1fr 2fr;
      gap: 8rem;
      align-items: start;
      border-top: 1px solid rgba(200,184,154,0.3);
    }

    .section-label {
      font-size: 0.7rem;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: var(--stone);
      font-weight: 400;
      margin-bottom: 0;
      padding-top: 0.4rem;
    }

    .about-text h2 {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2.2rem, 4vw, 3.5rem);
      font-weight: 300;
      line-height: 1.2;
      color: var(--dark);
      margin-bottom: 2rem;
    }
    .about-text h2 em { font-style: italic; color: var(--accent); }

    .about-text p {
      font-size: 0.95rem;
      line-height: 1.85;
      color: var(--muted);
      font-weight: 300;
      max-width: 600px;
      margin-bottom: 1.4rem;
    }

    .stats {
      display: flex;
      gap: 4rem;
      margin-top: 3.5rem;
      padding-top: 3rem;
      border-top: 1px solid rgba(200,184,154,0.3);
    }

    .stat-item {
      display: flex;
      flex-direction: column;
      gap: 0.4rem;
    }

    .stat-num {
      font-family: 'Cormorant Garamond', serif;
      font-size: 2.6rem;
      font-weight: 300;
      color: var(--dark);
      line-height: 1;
    }

    .stat-label {
      font-size: 0.72rem;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--stone);
    }

    /* ── SERVICES ── */
    .services {
      padding: 10rem 5rem;
      background: var(--dark);
    }

    .services-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 6rem;
    }

    .services-header h2 {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2.5rem, 5vw, 4.5rem);
      font-weight: 300;
      color: var(--cream);
      line-height: 1.1;
      max-width: 500px;
    }
    .services-header h2 em { font-style: italic; color: var(--stone); }

    .services-header .section-label { color: rgba(255,255,255,0.25); }

    .services-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 1px;
      background: rgba(255,255,255,0.06);
    }

    .service-card {
      padding: 3.5rem 3rem;
      background: var(--dark);
      border: none;
      transition: background 0.3s;
      position: relative;
      overflow: hidden;
    }

    .service-card::after {
      content: '';
      position: absolute;
      bottom: 0; left: 0;
      width: 0; height: 1px;
      background: var(--accent);
      transition: width 0.4s ease;
    }

    .service-card:hover { background: #262018; }
    .service-card:hover::after { width: 100%; }

    .service-num {
      font-family: 'Cormorant Garamond', serif;
      font-size: 0.9rem;
      color: var(--accent);
      margin-bottom: 2rem;
      display: block;
    }

    .service-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.6rem;
      font-weight: 400;
      color: var(--cream);
      line-height: 1.2;
      margin-bottom: 1.2rem;
    }

    .service-desc {
      font-size: 0.85rem;
      line-height: 1.8;
      color: rgba(255,255,255,0.38);
      font-weight: 300;
    }

    /* ── STRUCTURE ── */
    .structure {
      padding: 10rem 5rem;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8rem;
      align-items: center;
    }

    .structure-visual {
      position: relative;
      height: 400px;
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      justify-content: center;
      gap: 0;
    }

    .struct-box {
      border: 1px solid;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 2rem 2.5rem;
      position: relative;
    }

    .struct-box.main {
      width: 65%;
      border-color: var(--accent);
      background: var(--accent);
      z-index: 2;
    }
    .struct-box.main .struct-label { color: rgba(255,255,255,0.7); font-size: 0.7rem; letter-spacing: 0.18em; text-transform: uppercase; margin-bottom: 0.5rem; }
    .struct-box.main .struct-name { font-family: 'Cormorant Garamond', serif; font-size: 1.8rem; font-weight: 300; color: white; }

    .struct-connector {
      width: 1px;
      height: 48px;
      background: var(--stone);
      margin-left: calc(65% / 2);
      position: relative;
      z-index: 3;
      flex-shrink: 0;
    }
    .struct-connector::before,
    .struct-connector::after {
      content: '';
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      width: 6px; height: 6px;
      border-radius: 50%;
      background: var(--stone);
    }
    .struct-connector::before { top: -3px; }
    .struct-connector::after { bottom: -3px; }

    .struct-box.sub {
      width: 85%;
      border-color: var(--stone);
      background: var(--cream);
      z-index: 1;
    }
    .struct-box.sub .struct-label { color: var(--muted); font-size: 0.7rem; letter-spacing: 0.18em; text-transform: uppercase; margin-bottom: 0.5rem; }
    .struct-box.sub .struct-name { font-family: 'Cormorant Garamond', serif; font-size: 1.8rem; font-weight: 300; color: var(--dark); }
    .struct-box.sub .struct-note { margin-top: 0.8rem; font-size: 0.78rem; color: var(--muted); font-weight: 300; line-height: 1.6; }
    .structure-text h2 {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2rem, 3.5vw, 3rem);
      font-weight: 300;
      line-height: 1.2;
      color: var(--dark);
      margin-bottom: 2rem;
    }
    .structure-text h2 em { font-style: italic; color: var(--accent); }

    .structure-text p {
      font-size: 0.9rem;
      line-height: 1.85;
      color: var(--muted);
      font-weight: 300;
      margin-bottom: 1.2rem;
      max-width: 480px;
    }

    /* ── CONTACT ── */
    .contact {
      padding: 10rem 5rem;
      background: var(--sand);
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 8rem;
      align-items: start;
      border-top: 1px solid rgba(200,184,154,0.3);
    }

    .contact-left h2 {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2.5rem, 4vw, 4rem);
      font-weight: 300;
      line-height: 1.1;
      color: var(--dark);
      margin-bottom: 2rem;
    }
    .contact-left h2 em { font-style: italic; color: var(--accent); }

    .contact-left p {
      font-size: 0.9rem;
      line-height: 1.85;
      color: var(--muted);
      font-weight: 300;
      max-width: 380px;
    }

    .contact-details {
      margin-top: 3.5rem;
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .contact-item {
      display: flex;
      flex-direction: column;
      gap: 0.25rem;
    }
    .contact-item .ci-label {
      font-size: 0.7rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--stone);
    }
    .contact-item .ci-val {
      font-size: 0.9rem;
      color: var(--ink);
      font-weight: 400;
    }
    .contact-item a.ci-val {
      text-decoration: none;
      color: var(--ink);
      transition: color 0.2s;
    }
    .contact-item a.ci-val:hover { color: var(--accent); }

    .contact-form {
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .form-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1rem;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
    }
    .form-group label {
      font-size: 0.7rem;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      color: var(--muted);
    }
    .form-group input,
    .form-group textarea {
      background: transparent;
      border: none;
      border-bottom: 1px solid var(--stone);
      padding: 0.75rem 0;
      font-family: 'DM Sans', sans-serif;
      font-size: 0.9rem;
      color: var(--ink);
      font-weight: 300;
      outline: none;
      transition: border-color 0.2s;
      width: 100%;
    }
    .form-group input:focus,
    .form-group textarea:focus { border-color: var(--accent); }
    .form-group textarea { resize: none; min-height: 100px; }

    .form-submit {
      margin-top: 1rem;
    }
    .form-submit button {
      padding: 0.9rem 2.5rem;
      background: var(--dark);
      color: var(--cream);
      font-family: 'DM Sans', sans-serif;
      font-size: 0.78rem;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      border: none;
      cursor: pointer;
      transition: background 0.25s;
    }
    .form-submit button:hover { background: var(--accent); }

    /* ── FOOTER ── */
    footer {
      padding: 3rem 5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: var(--dark);
    }

    .footer-logo {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.1rem;
      font-weight: 600;
      color: rgba(255,255,255,0.6);
      letter-spacing: 0.04em;
    }
    .footer-logo span { color: var(--accent); }

    .footer-copy {
      font-size: 0.72rem;
      color: rgba(255,255,255,0.22);
      letter-spacing: 0.08em;
    }

    .footer-kvk {
      font-size: 0.72rem;
      color: rgba(255,255,255,0.22);
      letter-spacing: 0.08em;
    }

    /* ── ANIMATIONS ── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn {
      from { opacity: 0; } to { opacity: 1; }
    }

    /* Scroll reveal */
    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 0.8s ease, transform 0.8s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 1024px) {
      nav { padding: 1.4rem 2rem; }
      .hero { grid-template-columns: 1fr; }
      .hero-left { padding: 9rem 2.5rem 5rem; }
      .hero-right { height: 40vh; }
      .about, .contact { grid-template-columns: 1fr; gap: 3rem; padding: 7rem 2.5rem; }
      .services { padding: 7rem 2.5rem; }
      .services-header { flex-direction: column; align-items: flex-start; gap: 2rem; }
      .services-grid { grid-template-columns: 1fr; }
      .structure { grid-template-columns: 1fr; gap: 4rem; padding: 7rem 2.5rem; }
      .structure-visual { height: auto; }
      .struct-box.main { width: 75%; }
      .struct-box.sub { width: 95%; }
      .struct-connector { margin-left: calc(75% / 2); }
      footer { padding: 2.5rem; flex-direction: column; gap: 1rem; text-align: center; }
      .stats { gap: 2.5rem; }
      nav ul { gap: 1.5rem; }
    }
  </style>
</head>
<body>

  <div id="cursor"></div>
  <div id="cursor-ring"></div>

  <!-- NAV -->
  <nav>
    <a href="#" class="nav-logo">Terra<span>vend</span></a>
    <ul>
      <li><a href="#over">Over ons</a></li>
      <li><a href="#diensten">Diensten</a></li>
      <li><a href="#structuur">Structuur</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <!-- HERO -->
  <section class="hero">
    <div class="hero-left">
      <p class="hero-eyebrow">Terravend B.V. — Holding</p>
      <h1 class="hero-title">
        Stabiel.<br>
        <em>Wendbaar.</em><br>
        Professioneel.
      </h1>
      <p class="hero-sub">
        Terravend B.V. is de solide basis waaronder ondernemingsactiviteiten worden ontplooid. 
        Flexibel inzetbaar, juridisch helder, altijd op orde.
      </p>
      <div class="hero-cta">
        <a href="#over" class="btn-primary">Meer informatie</a>
        <a href="#contact" class="btn-ghost">Contact opnemen →</a>
      </div>
      <div class="scroll-line">Scroll</div>
    </div>
    <div class="hero-right">
      <div class="hero-right-inner">
        <div class="logo-mark">
          <svg viewBox="0 0 220 220" fill="none" xmlns="http://www.w3.org/2000/svg">
            <!-- Outer ring -->
            <circle cx="110" cy="110" r="100" stroke="#c8b89a" stroke-width="0.5" opacity="0.4"/>
            <!-- Middle ring -->
            <circle cx="110" cy="110" r="70" stroke="#c8b89a" stroke-width="0.5" opacity="0.6"/>
            <!-- Inner ring -->
            <circle cx="110" cy="110" r="40" stroke="#4a7c6f" stroke-width="1" opacity="0.8"/>

            <!-- Cross lines -->
            <line x1="10" y1="110" x2="210" y2="110" stroke="#c8b89a" stroke-width="0.5" opacity="0.3"/>
            <line x1="110" y1="10" x2="110" y2="210" stroke="#c8b89a" stroke-width="0.5" opacity="0.3"/>

            <!-- Diamond -->
            <polygon points="110,60 160,110 110,160 60,110" stroke="#4a7c6f" stroke-width="1" fill="rgba(74,124,111,0.06)"/>

            <!-- Center dot -->
            <circle cx="110" cy="110" r="5" fill="#4a7c6f"/>

            <!-- Tick marks -->
            <line x1="110" y1="8" x2="110" y2="18" stroke="#c8b89a" stroke-width="1"/>
            <line x1="110" y1="202" x2="110" y2="212" stroke="#c8b89a" stroke-width="1"/>
            <line x1="8" y1="110" x2="18" y2="110" stroke="#c8b89a" stroke-width="1"/>
            <line x1="202" y1="110" x2="212" y2="110" stroke="#c8b89a" stroke-width="1"/>

            <!-- T lettermark -->
            <text x="110" y="118" font-family="Georgia, serif" font-size="28" fill="#4a7c6f" text-anchor="middle" font-style="italic" opacity="0.9">T</text>
          </svg>
        </div>
      </div>
      <div class="watermark">Terravend B.V. — Est. 2024</div>
    </div>
  </section>

  <!-- ABOUT -->
  <section class="about" id="over">
    <div class="section-label reveal">Over ons</div>
    <div class="about-text reveal">
      <h2>Ondernemen vanuit<br>een <em>sterke basis</em></h2>
      <p>
        Terravend B.V. fungeert als houdstermaatschappij van waaruit uiteenlopende activiteiten 
        kunnen worden uitgevoerd. Of het nu gaat om dienstverlening, handel of consultancy — 
        de structuur staat, de operatie is flexibel.
      </p>
      <p>
        Via verschillende handelsnamen worden dagelijkse activiteiten ontplooid, volledig 
        ondergebracht en geborgd binnen Terravend B.V. Dat biedt overzicht, helderheid 
        en de ruimte om te groeien.
      </p>
      <div class="stats">
        <div class="stat-item">
          <span class="stat-num">1</span>
          <span class="stat-label">Juridische entiteit</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">∞</span>
          <span class="stat-label">Mogelijkheden</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">NL</span>
          <span class="stat-label">Gevestigd</span>
        </div>
      </div>
    </div>
  </section>

  <!-- SERVICES -->
  <section class="services" id="diensten">
    <div class="services-header">
      <div class="section-label" style="color:rgba(255,255,255,0.25)">Wat wij bieden</div>
      <h2>Diensten &<br><em>activiteiten</em></h2>
    </div>
    <div class="services-grid">
      <div class="service-card reveal">
        <span class="service-num">01</span>
        <h3 class="service-title">Holding &amp; Beheer</h3>
        <p class="service-desc">Centraal beheer van bedrijfsactiviteiten, deelnemingen en vermogen. Terravend B.V. vormt de juridische en financiële kern.</p>
      </div>
      <div class="service-card reveal">
        <span class="service-num">02</span>
        <h3 class="service-title">Handelsnamen</h3>
        <p class="service-desc">Activiteiten worden uitgevoerd onder één of meerdere handelsnamen, elk met een eigen identiteit en marktfocus.</p>
      </div>
      <div class="service-card reveal">
        <span class="service-num">03</span>
        <h3 class="service-title">Zakelijke dienstverlening</h3>
        <p class="service-desc">Van advies tot uitvoering. Wij opereren snel, helder en professioneel — zonder onnodige bureaucratie.</p>
      </div>
    </div>
  </section>

  <!-- STRUCTURE -->
  <section class="structure" id="structuur">
    <div class="structure-visual reveal">
      <div class="struct-box main">
        <span class="struct-label">Houdstermaatschappij</span>
        <span class="struct-name">Terravend B.V.</span>
      </div>
      <div class="struct-connector"></div>
      <div class="struct-box sub">
        <span class="struct-label">Operationele activiteiten</span>
        <span class="struct-name">Handelsnamen</span>
        <p class="struct-note">Dagelijkse activiteiten worden uitgevoerd via één of meer handelsnamen, volledig gedragen door Terravend B.V.</p>
      </div>
    </div>
    <div class="structure-text reveal">
      <div class="section-label" style="margin-bottom:1.5rem">Bedrijfsstructuur</div>
      <h2>Eén B.V.,<br>meerdere <em>gezichten</em></h2>
      <p>
        De holding-structuur biedt maximale flexibiliteit. Terravend B.V. is de 
        moeder: juridisch verantwoordelijk, administratief centraal, financieel overzichtelijk.
      </p>
      <p>
        De handelsnamen zijn de gezichten naar de markt. Elk met een eigen aanpak, 
        samen gedragen door één solide fundament.
      </p>
      <p>
        Deze opzet maakt het eenvoudig om te schalen, te diversifiëren of nieuwe 
        activiteiten op te starten — zonder telkens een nieuwe rechtspersoon te hoeven oprichten.
      </p>
    </div>
  </section>

  <!-- CONTACT -->
  <section class="contact" id="contact">
    <div class="contact-left reveal">
      <div class="section-label" style="margin-bottom:1.5rem">Contact</div>
      <h2>Laten we<br>kennismaken.</h2>
      <p>Heeft u een vraag, een zakelijk voorstel of wilt u meer informatie? Wij zijn bereikbaar en reageren snel.</p>
      <div class="contact-details">
        <div class="contact-item">
          <span class="ci-label">Bedrijf</span>
          <span class="ci-val">Terravend B.V.</span>
        </div>
        <div class="contact-item">
          <span class="ci-label">Vestigingsland</span>
          <span class="ci-val">Nederland</span>
        </div>
        <div class="contact-item">
          <span class="ci-label">E-mail</span>
          <a href="mailto:info@terravend.nl" class="ci-val">info@terravend.nl</a>
        </div>
        <div class="contact-item">
          <span class="ci-label">Website</span>
          <a href="https://terravend.nl" class="ci-val">terravend.nl</a>
        </div>
      </div>
    </div>
    <div class="contact-form reveal">
      <div class="form-row">
        <div class="form-group">
          <label for="naam">Naam</label>
          <input type="text" id="naam" placeholder="Uw naam" />
        </div>
        <div class="form-group">
          <label for="bedrijf">Bedrijf</label>
          <input type="text" id="bedrijf" placeholder="Bedrijfsnaam" />
        </div>
      </div>
      <div class="form-group">
        <label for="email">E-mailadres</label>
        <input type="email" id="email" placeholder="uw@email.nl" />
      </div>
      <div class="form-group">
        <label for="bericht">Bericht</label>
        <textarea id="bericht" placeholder="Hoe kunnen wij u helpen?"></textarea>
      </div>
      <div class="form-submit">
        <button type="button" onclick="handleSubmit()">Verstuur bericht</button>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <div class="footer-logo">Terra<span>vend</span></div>
    <div class="footer-copy">© 2025 Terravend B.V. — Alle rechten voorbehouden</div>
    <div class="footer-kvk">KvK-nummer: —</div>
  </footer>

  <script>
    // Custom cursor
    const cursor = document.getElementById('cursor');
    const ring   = document.getElementById('cursor-ring');
    let mx = 0, my = 0, rx = 0, ry = 0;

    document.addEventListener('mousemove', e => {
      mx = e.clientX; my = e.clientY;
      cursor.style.left = mx + 'px';
      cursor.style.top  = my + 'px';
    });

    (function animateRing() {
      rx += (mx - rx) * 0.12;
      ry += (my - ry) * 0.12;
      ring.style.left = rx + 'px';
      ring.style.top  = ry + 'px';
      requestAnimationFrame(animateRing);
    })();

    document.querySelectorAll('a, button, input, textarea').forEach(el => {
      el.addEventListener('mouseenter', () => {
        cursor.style.width = '6px';
        cursor.style.height = '6px';
        ring.style.width = '52px';
        ring.style.height = '52px';
      });
      el.addEventListener('mouseleave', () => {
        cursor.style.width = '10px';
        cursor.style.height = '10px';
        ring.style.width = '36px';
        ring.style.height = '36px';
      });
    });

    // Scroll reveal
    const reveals = document.querySelectorAll('.reveal');
    const io = new IntersectionObserver((entries) => {
      entries.forEach((e, i) => {
        if (e.isIntersecting) {
          setTimeout(() => e.target.classList.add('visible'), 80);
          io.unobserve(e.target);
        }
      });
    }, { threshold: 0.12 });
    reveals.forEach(el => io.observe(el));

    // Form submit
    function handleSubmit() {
      const naam = document.getElementById('naam').value;
      const email = document.getElementById('email').value;
      if (!naam || !email) {
        alert('Vul minimaal uw naam en e-mailadres in.');
        return;
      }
      alert('Bedankt voor uw bericht! Wij nemen zo spoedig mogelijk contact met u op.');
    }
  </script>
</body>
</html>

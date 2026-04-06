<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ilia Esmaeilinasab — Fullstack Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #080B10;
    --bg2: #0D1117;
    --bg3: #0A0D14;
    --border: #1A2030;
    --border-hover: rgba(0,210,255,0.3);
    --text: #E8EDF5;
    --text-dim: #5A6478;
    --text-muted: #2D3748;
    --accent: #00D2FF;
    --accent-glow: rgba(0,210,255,0.15);
    --font-display: 'Syne', sans-serif;
    --font-mono: 'DM Mono', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-mono);
    min-height: 100vh;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed; width: 8px; height: 8px;
    background: var(--accent); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%, -50%);
    transition: width 0.2s, height 0.2s, opacity 0.2s;
  }
  .cursor-ring {
    position: fixed; width: 32px; height: 32px;
    border: 1px solid rgba(0,210,255,0.4); border-radius: 50%;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.12s ease, width 0.2s, height 0.2s;
  }

  /* Background grid */
  .bg-grid {
    position: fixed; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(0,210,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,210,255,0.03) 1px, transparent 1px);
    background-size: 52px 52px;
    pointer-events: none;
  }
  .bg-glow-top {
    position: fixed; top: -300px; left: 50%; transform: translateX(-50%);
    width: 900px; height: 600px;
    background: radial-gradient(ellipse, rgba(0,210,255,0.05) 0%, transparent 70%);
    pointer-events: none; z-index: 0;
  }
  .scanline {
    position: fixed; top: 0; left: 0; right: 0;
    height: 1px; background: rgba(0,210,255,0.08);
    animation: scan 8s linear infinite;
    pointer-events: none; z-index: 5;
  }
  @keyframes scan {
    0% { top: -1px; } 100% { top: 100vh; }
  }

  /* Corner brackets */
  .bracket { position: fixed; width: 32px; height: 32px; z-index: 2; pointer-events: none; }
  .bracket-tr { top: 24px; right: 24px; border-top: 1px solid rgba(0,210,255,0.18); border-right: 1px solid rgba(0,210,255,0.18); }
  .bracket-bl { bottom: 24px; left: 24px; border-bottom: 1px solid rgba(0,210,255,0.18); border-left: 1px solid rgba(0,210,255,0.18); }
  .bracket-tl { top: 24px; left: 24px; border-top: 1px solid rgba(0,210,255,0.18); border-left: 1px solid rgba(0,210,255,0.18); }
  .bracket-br { bottom: 24px; right: 24px; border-bottom: 1px solid rgba(0,210,255,0.18); border-right: 1px solid rgba(0,210,255,0.18); }

  /* Layout */
  .page { position: relative; z-index: 1; }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 20px 48px;
    display: flex; justify-content: space-between; align-items: center;
    border-bottom: 1px solid transparent;
    transition: border-color 0.3s, background 0.3s;
  }
  nav.scrolled {
    background: rgba(8,11,16,0.92);
    border-bottom-color: var(--border);
    backdrop-filter: blur(12px);
  }
  .nav-logo {
    font-family: var(--font-display); font-weight: 800;
    font-size: 15px; letter-spacing: 0.18em;
    color: var(--accent); text-transform: uppercase;
  }
  .nav-links { display: flex; gap: 32px; }
  .nav-links a {
    font-size: 11px; letter-spacing: 0.12em; color: var(--text-dim);
    text-decoration: none; text-transform: uppercase;
    transition: color 0.2s;
    position: relative;
  }
  .nav-links a::after {
    content: ''; position: absolute; bottom: -3px; left: 0; right: 0;
    height: 1px; background: var(--accent);
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.3s ease;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-links a:hover::after { transform: scaleX(1); }

  /* SECTIONS */
  section { min-height: 100vh; display: flex; align-items: center; }

  .container {
    max-width: 860px; margin: 0 auto;
    padding: 120px 48px 80px;
    width: 100%;
  }

  /* ── HERO ── */
  #hero { padding-top: 0; }
  #hero .container { padding-top: 140px; }

  .tag {
    display: inline-flex; align-items: center; gap: 8px;
    font-size: 11px; letter-spacing: 0.14em; text-transform: uppercase;
    color: var(--accent); border: 1px solid rgba(0,210,255,0.2);
    padding: 5px 14px; border-radius: 2px; margin-bottom: 32px;
    opacity: 0; animation: fadeUp 0.6s ease 0.2s forwards;
  }
  .tag-dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--accent); box-shadow: 0 0 8px var(--accent);
    animation: blink 2s ease infinite;
  }
  @keyframes blink { 0%,100%{opacity:1;} 50%{opacity:0.2;} }

  .hero-name {
    font-family: var(--font-display); font-weight: 800;
    font-size: clamp(48px, 7vw, 76px);
    line-height: 1.0; letter-spacing: -0.025em;
    color: #F0F4FF;
    opacity: 0; animation: fadeUp 0.7s ease 0.3s forwards;
  }
  .hero-name .accent { color: var(--accent); text-shadow: 0 0 50px rgba(0,210,255,0.25); }

  .hero-sub {
    margin-top: 20px; font-size: 13px; letter-spacing: 0.08em;
    color: var(--text-dim); font-weight: 300;
    opacity: 0; animation: fadeUp 0.7s ease 0.45s forwards;
  }
  .hero-sub strong { color: #8A95A8; font-weight: 400; }

  .hero-desc {
    margin-top: 28px; font-size: 13px; line-height: 2;
    color: var(--text-muted); max-width: 480px;
    opacity: 0; animation: fadeUp 0.7s ease 0.55s forwards;
  }

  .cta-row {
    display: flex; gap: 12px; margin-top: 48px; flex-wrap: wrap;
    opacity: 0; animation: fadeUp 0.7s ease 0.65s forwards;
  }
  .btn-primary {
    padding: 12px 28px; font-size: 12px; letter-spacing: 0.1em;
    text-transform: uppercase; font-family: var(--font-mono);
    background: var(--accent); color: var(--bg);
    border: none; border-radius: 2px; cursor: none; font-weight: 500;
    transition: opacity 0.2s, transform 0.2s;
    text-decoration: none; display: inline-block;
  }
  .btn-primary:hover { opacity: 0.85; transform: translateY(-2px); }
  .btn-ghost {
    padding: 12px 28px; font-size: 12px; letter-spacing: 0.1em;
    text-transform: uppercase; font-family: var(--font-mono);
    background: transparent; color: var(--text-dim);
    border: 1px solid var(--border); border-radius: 2px; cursor: none;
    transition: border-color 0.2s, color 0.2s, transform 0.2s;
    text-decoration: none; display: inline-block;
  }
  .btn-ghost:hover { border-color: var(--border-hover); color: #8A95A8; transform: translateY(-2px); }

  .meta-row {
    display: flex; align-items: center; gap: 24px; flex-wrap: wrap;
    margin-top: 48px; font-size: 11px; letter-spacing: 0.1em;
    color: var(--text-muted); text-transform: uppercase;
    opacity: 0; animation: fadeUp 0.6s ease 0.75s forwards;
  }
  .meta-item { display: flex; align-items: center; gap: 7px; }
  .meta-sep { color: var(--border); }

  /* Scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 40px; left: 50%; transform: translateX(-50%);
    font-size: 10px; letter-spacing: 0.15em; color: var(--text-muted);
    text-transform: uppercase; display: flex; flex-direction: column;
    align-items: center; gap: 10px;
    opacity: 0; animation: fadeUp 0.6s ease 1.1s forwards;
  }
  .scroll-line {
    width: 1px; height: 40px;
    background: linear-gradient(180deg, var(--accent), transparent);
    animation: scrollPulse 2s ease infinite;
  }
  @keyframes scrollPulse { 0%,100%{opacity:0.3;} 50%{opacity:1;} }

  /* ── ABOUT ── */
  .section-header {
    display: flex; align-items: center; gap: 16px; margin-bottom: 48px;
  }
  .section-num {
    font-size: 11px; letter-spacing: 0.12em; color: var(--accent);
    font-weight: 500;
  }
  .section-title {
    font-family: var(--font-display); font-size: 32px; font-weight: 800;
    color: var(--text); letter-spacing: -0.02em;
  }
  .section-line {
    flex: 1; height: 1px;
    background: linear-gradient(90deg, var(--border), transparent);
  }

  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 48px;
    align-items: start;
  }
  .about-text {
    font-size: 13px; line-height: 2; color: var(--text-dim);
  }
  .about-text p + p { margin-top: 16px; }
  .about-text strong { color: #8A95A8; font-weight: 400; }

  .about-info { display: flex; flex-direction: column; gap: 0; }
  .info-row {
    display: flex; justify-content: space-between; align-items: center;
    padding: 14px 0; border-bottom: 1px solid var(--border);
    font-size: 12px;
  }
  .info-row:first-child { border-top: 1px solid var(--border); }
  .info-key { color: var(--text-muted); letter-spacing: 0.1em; text-transform: uppercase; font-size: 10px; }
  .info-val { color: #8A95A8; text-align: right; }
  .info-val .accent { color: var(--accent); }

  /* ── STACK ── */
  #stack { background: none; }
  .stack-desc {
    font-size: 13px; line-height: 1.9; color: var(--text-muted);
    margin-bottom: 40px; max-width: 520px;
  }
  .stack-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 10px;
  }
  .chip {
    display: flex; align-items: center; gap: 10px;
    padding: 14px 16px; border-radius: 3px;
    font-size: 13px; letter-spacing: 0.04em;
    background: var(--bg2); border: 1px solid var(--border);
    color: #8A95A8; font-family: var(--font-mono);
    transition: border-color 0.2s, color 0.2s, transform 0.2s, background 0.2s;
    cursor: default;
  }
  .chip:hover {
    border-color: rgba(0,210,255,0.35);
    color: var(--text); background: #0F1520;
    transform: translateY(-3px);
  }
  .chip-dot { width: 7px; height: 7px; border-radius: 50%; flex-shrink: 0; }
  .chip-tag { margin-left: auto; font-size: 10px; color: var(--text-muted); letter-spacing: 0.08em; }

  .dot-py  { background: #3776AB; box-shadow: 0 0 6px #3776AB55; }
  .dot-java{ background: #007396; box-shadow: 0 0 6px #00739655; }
  .dot-js  { background: #F7DF1E; box-shadow: 0 0 6px #F7DF1E55; }
  .dot-html{ background: #E34F26; box-shadow: 0 0 6px #E34F2655; }
  .dot-css { background: #1572B6; box-shadow: 0 0 6px #1572B655; }
  .dot-sql { background: #4479A1; box-shadow: 0 0 6px #4479A155; }
  .dot-mongo{background: #47A248; box-shadow: 0 0 6px #47A24855; }
  .dot-latex{background: #008080; box-shadow: 0 0 6px #00808055; }

  /* ── PROJECTS ── */
  .projects-grid { display: flex; flex-direction: column; gap: 2px; }
  .project-card {
    background: var(--bg2); border: 1px solid var(--border);
    border-radius: 3px; padding: 28px 32px;
    display: grid; grid-template-columns: 1fr auto;
    gap: 16px; align-items: start;
    transition: border-color 0.2s, background 0.2s, transform 0.2s;
    cursor: none;
  }
  .project-card:hover {
    border-color: rgba(0,210,255,0.25);
    background: #0F1520;
    transform: translateX(4px);
  }
  .project-num { font-size: 11px; color: var(--text-muted); letter-spacing: 0.1em; margin-bottom: 10px; }
  .project-name {
    font-family: var(--font-display); font-size: 18px; font-weight: 700;
    color: var(--text); letter-spacing: -0.01em; margin-bottom: 8px;
  }
  .project-desc { font-size: 12px; line-height: 1.8; color: var(--text-dim); }
  .project-tags { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 16px; }
  .project-tag {
    font-size: 10px; padding: 3px 10px; border-radius: 2px;
    background: var(--bg); border: 1px solid var(--border);
    color: var(--text-muted); letter-spacing: 0.08em;
  }
  .project-link {
    font-size: 11px; color: var(--accent); text-decoration: none;
    letter-spacing: 0.1em; text-transform: uppercase;
    display: flex; align-items: center; gap: 6px;
    transition: gap 0.2s;
    white-space: nowrap;
  }
  .project-link:hover { gap: 10px; }
  .coming-soon {
    text-align: center; padding: 60px 32px;
    border: 1px dashed var(--border); border-radius: 3px;
  }
  .cs-label { font-size: 11px; letter-spacing: 0.18em; color: var(--text-muted); text-transform: uppercase; }
  .cs-big { font-family: var(--font-display); font-size: 28px; font-weight: 800; color: var(--border); margin-top: 12px; }

  /* ── CONTACT ── */
  .contact-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 48px;
    align-items: start;
  }
  .contact-text { font-size: 13px; line-height: 2; color: var(--text-dim); }
  .contact-links { display: flex; flex-direction: column; gap: 0; }
  .contact-link {
    display: flex; align-items: center; justify-content: space-between;
    padding: 18px 0; border-bottom: 1px solid var(--border);
    text-decoration: none;
    transition: padding-left 0.2s;
  }
  .contact-link:first-child { border-top: 1px solid var(--border); }
  .contact-link:hover { padding-left: 8px; }
  .contact-link:hover .cl-name { color: var(--accent); }
  .cl-platform { font-size: 10px; letter-spacing: 0.12em; color: var(--text-muted); text-transform: uppercase; }
  .cl-name { font-size: 13px; color: #8A95A8; margin-top: 3px; transition: color 0.2s; }
  .cl-arrow { font-size: 16px; color: var(--text-muted); transition: color 0.2s; }
  .contact-link:hover .cl-arrow { color: var(--accent); }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--border);
    padding: 32px 48px;
    display: flex; justify-content: space-between; align-items: center;
    position: relative; z-index: 1;
  }
  .footer-copy { font-size: 11px; color: var(--text-muted); letter-spacing: 0.08em; }
  .footer-handle { font-size: 11px; color: var(--text-muted); letter-spacing: 0.1em; }
  .footer-handle span { color: var(--accent); }

  /* Divider */
  .section-divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), transparent);
    margin: 0 48px;
    position: relative; z-index: 1;
  }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0; transform: translateY(24px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }
  .reveal-delay-1 { transition-delay: 0.1s; }
  .reveal-delay-2 { transition-delay: 0.2s; }
  .reveal-delay-3 { transition-delay: 0.3s; }

  /* Responsive */
  @media (max-width: 700px) {
    nav { padding: 20px 24px; }
    .nav-links { gap: 20px; }
    .container { padding: 120px 24px 80px; }
    .about-grid, .contact-grid { grid-template-columns: 1fr; gap: 32px; }
    .hero-name { font-size: 42px; }
    footer { padding: 24px; flex-direction: column; gap: 8px; text-align: center; }
    .section-divider { margin: 0 24px; }
  }
</style>
</head>
<body>

<!-- Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- BG effects -->
<div class="bg-grid"></div>
<div class="bg-glow-top"></div>
<div class="scanline"></div>
<div class="bracket bracket-tr"></div>
<div class="bracket bracket-bl"></div>
<div class="bracket bracket-tl"></div>
<div class="bracket bracket-br"></div>

<!-- NAV -->
<nav id="navbar">
  <div class="nav-logo">IE_</div>
  <div class="nav-links">
    <a href="#about">About</a>
    <a href="#stack">Stack</a>
    <a href="#projects">Projekte</a>
    <a href="#contact">Kontakt</a>
  </div>
</nav>

<div class="page">

  <!-- ══ HERO ══ -->
  <section id="hero" style="position:relative;">
    <div class="container">
      <div class="tag"><span class="tag-dot"></span>Available for hire</div>

      <h1 class="hero-name">
        Ilia<br>
        <span class="accent">Esmaeilinasab</span>
      </h1>

      <p class="hero-sub">
        <strong>Fullstack Developer</strong> &nbsp;·&nbsp; Python &nbsp;·&nbsp; JavaScript &nbsp;·&nbsp; Java
      </p>

      <p class="hero-desc">
        // Ich baue Webanwendungen von der Datenbank<br>
        // bis zum Interface — clean, schnell, wartbar.
      </p>

      <div class="cta-row">
        <a class="btn-primary" href="#projects">Projekte ansehen</a>
        <a class="btn-ghost" href="#contact">Kontakt aufnehmen</a>
      </div>

      <div class="meta-row">
        <span class="meta-item">📍 Frankfurt am Main, DE</span>
        <span class="meta-sep">—</span>
        <span class="meta-item">🟢 Open to opportunities</span>
        <span class="meta-sep">—</span>
        <span class="meta-item">github.com/Iliaies</span>
      </div>
    </div>

    <div class="scroll-hint">
      <span>Scroll</span>
      <div class="scroll-line"></div>
    </div>
  </section>

  <div class="section-divider"></div>

  <!-- ══ ABOUT ══ -->
  <section id="about">
    <div class="container">
      <div class="section-header reveal">
        <span class="section-num">01 /</span>
        <h2 class="section-title">Über mich</h2>
        <div class="section-line"></div>
      </div>

      <div class="about-grid">
        <div class="about-text reveal reveal-delay-1">
          <p>
            Ich bin <strong>Ilia Esmaeilinasab</strong>, Fullstack-Entwickler mit Sitz in Frankfurt am Main.
            Meine Leidenschaft liegt darin, digitale Produkte zu bauen, die sowohl technisch sauber als auch
            benutzerfreundlich sind.
          </p>
          <p>
            Mit Kenntnissen in <strong>Python, JavaScript, Java</strong> und modernen
            Web-Technologien entwickle ich sowohl Backend-Systeme als auch Frontend-Interfaces.
          </p>
          <p>
            Derzeit arbeite ich an spannenden Projekten und bin offen für neue Möglichkeiten und
            Kooperationen.
          </p>
        </div>

        <div class="about-info reveal reveal-delay-2">
          <div class="info-row">
            <span class="info-key">Name</span>
            <span class="info-val">Ilia Esmaeilinasab</span>
          </div>
          <div class="info-row">
            <span class="info-key">Handle</span>
            <span class="info-val"><span class="accent">@Iliaies</span></span>
          </div>
          <div class="info-row">
            <span class="info-key">Standort</span>
            <span class="info-val">Frankfurt am Main, DE</span>
          </div>
          <div class="info-row">
            <span class="info-key">Fokus</span>
            <span class="info-val">Fullstack Development</span>
          </div>
          <div class="info-row">
            <span class="info-key">Status</span>
            <span class="info-val"><span class="accent">Open to work</span></span>
          </div>
          <div class="info-row">
            <span class="info-key">Sprachen</span>
            <span class="info-val">Deutsch · Englisch · Farsi</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <div class="section-divider"></div>

  <!-- ══ STACK ══ -->
  <section id="stack">
    <div class="container">
      <div class="section-header reveal">
        <span class="section-num">02 /</span>
        <h2 class="section-title">Tech Stack</h2>
        <div class="section-line"></div>
      </div>

      <p class="stack-desc reveal">
        // Sprachen und Technologien mit denen ich arbeite
      </p>

      <div class="stack-grid">
        <div class="chip reveal reveal-delay-1"><span class="chip-dot dot-py"></span>Python<span class="chip-tag">Backend</span></div>
        <div class="chip reveal reveal-delay-1"><span class="chip-dot dot-java"></span>Java<span class="chip-tag">OOP</span></div>
        <div class="chip reveal reveal-delay-2"><span class="chip-dot dot-js"></span>JavaScript<span class="chip-tag">Frontend</span></div>
        <div class="chip reveal reveal-delay-2"><span class="chip-dot dot-html"></span>HTML5<span class="chip-tag">Markup</span></div>
        <div class="chip reveal reveal-delay-3"><span class="chip-dot dot-css"></span>CSS3<span class="chip-tag">Styling</span></div>
        <div class="chip reveal reveal-delay-3"><span class="chip-dot dot-sql"></span>SQL<span class="chip-tag">Database</span></div>
        <div class="chip reveal reveal-delay-1"><span class="chip-dot dot-mongo"></span>MongoDB<span class="chip-tag">NoSQL</span></div>
        <div class="chip reveal reveal-delay-2"><span class="chip-dot dot-latex"></span>LaTeX<span class="chip-tag">Typesetting</span></div>
      </div>
    </div>
  </section>

  <div class="section-divider"></div>

  <!-- ══ PROJECTS ══ -->
  <section id="projects">
    <div class="container">
      <div class="section-header reveal">
        <span class="section-num">03 /</span>
        <h2 class="section-title">Projekte</h2>
        <div class="section-line"></div>
      </div>

      <div class="projects-grid">
        <!-- Placeholder - einfach durch echte Projekte ersetzen -->
        <div class="coming-soon reveal">
          <div class="cs-label">// Kommt bald</div>
          <div class="cs-big">PROJECTS LOADING_</div>
        </div>

        <!-- Beispiel-Karte (auskommentiert) — zum Aktivieren <!-- entfernen:
        <div class="project-card reveal">
          <div>
            <div class="project-num">01 /</div>
            <div class="project-name">Projektname</div>
            <div class="project-desc">Kurze Beschreibung was das Projekt macht und welches Problem es löst.</div>
            <div class="project-tags">
              <span class="project-tag">Python</span>
              <span class="project-tag">JavaScript</span>
              <span class="project-tag">MongoDB</span>
            </div>
          </div>
          <a href="#" class="project-link">GitHub →</a>
        </div>
        -->
      </div>
    </div>
  </section>

  <div class="section-divider"></div>

  <!-- ══ CONTACT ══ -->
  <section id="contact">
    <div class="container">
      <div class="section-header reveal">
        <span class="section-num">04 /</span>
        <h2 class="section-title">Kontakt</h2>
        <div class="section-line"></div>
      </div>

      <div class="contact-grid">
        <div class="contact-text reveal">
          <p>Ich bin offen für neue Projekte, Freelance-Anfragen oder einfach ein gutes Gespräch über Technologie.</p>
          <br>
          <p style="color: var(--text-muted);">// Schreib mir — ich antworte in der Regel innerhalb von 24h.</p>
        </div>

        <div class="contact-links reveal reveal-delay-1">
          <a href="https://github.com/Iliaies" target="_blank" class="contact-link">
            <div>
              <div class="cl-platform">GitHub</div>
              <div class="cl-name">github.com/Iliaies</div>
            </div>
            <span class="cl-arrow">→</span>
          </a>
          <a href="https://linkedin.com/in/iliaies" target="_blank" class="contact-link">
            <div>
              <div class="cl-platform">LinkedIn</div>
              <div class="cl-name">linkedin.com/in/iliaies</div>
            </div>
            <span class="cl-arrow">→</span>
          </a>
          <a href="mailto:deine@email.de" class="contact-link">
            <div>
              <div class="cl-platform">Email</div>
              <div class="cl-name">deine@email.de</div>
            </div>
            <span class="cl-arrow">→</span>
          </a>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer>
    <span class="footer-copy">© 2025 Ilia Esmaeilinasab</span>
    <span class="footer-handle"><span>@</span>Iliaies</span>
  </footer>

</div>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });
  function animRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animRing);
  }
  animRing();
  document.querySelectorAll('a, button, .chip, .project-card').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '12px'; cursor.style.height = '12px';
      ring.style.width = '48px'; ring.style.height = '48px';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '8px'; cursor.style.height = '8px';
      ring.style.width = '32px'; ring.style.height = '32px';
    });
  });

  // Navbar on scroll
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 40);
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.12 });
  reveals.forEach(el => observer.observe(el));
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Emmanuella Turkson — Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,700;1,9..144,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050810;
    --surface: #0b1120;
    --surface2: #111827;
    --accent: #4fffb0;
    --accent2: #38bdf8;
    --accent3: #f472b6;
    --text: #e8eaf2;
    --muted: #6b7280;
    --border: rgba(255,255,255,0.07);
    --glow: rgba(79,255,176,0.15);
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Mono', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    border-radius: 50%;
    background: var(--accent);
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    mix-blend-mode: screen;
    transition: transform 0.1s ease;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border-radius: 50%;
    border: 1px solid rgba(79,255,176,0.5);
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: transform 0.15s ease, width 0.2s, height 0.2s;
  }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 9990; opacity: 0.4;
  }

  /* Ambient glow blobs */
  .blob {
    position: fixed; border-radius: 50%;
    filter: blur(120px); pointer-events: none; z-index: 0;
  }
  .blob-1 { width: 600px; height: 600px; background: rgba(79,255,176,0.04); top: -200px; right: -100px; }
  .blob-2 { width: 500px; height: 500px; background: rgba(56,189,248,0.04); bottom: 100px; left: -100px; }
  .blob-3 { width: 400px; height: 400px; background: rgba(244,114,182,0.03); top: 40%; left: 40%; }

  /* Nav */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 20px 60px;
    display: flex; justify-content: space-between; align-items: center;
    background: rgba(5,8,16,0.8);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }

  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-weight: 800; font-size: 1.1rem;
    color: var(--accent);
    letter-spacing: 0.05em;
    text-decoration: none;
  }

  .nav-links {
    display: flex; gap: 36px; list-style: none;
  }

  .nav-links a {
    color: var(--muted); text-decoration: none;
    font-size: 0.72rem; letter-spacing: 0.15em;
    text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--accent); }

  /* ─── Hero ─── */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center; padding: 120px 60px 80px;
    position: relative; overflow: hidden;
  }

  .hero-eyebrow {
    font-size: 0.72rem; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--accent);
    margin-bottom: 28px;
    display: flex; align-items: center; gap: 12px;
    opacity: 0; animation: fadeUp 0.8s 0.2s forwards;
  }
  .hero-eyebrow::before {
    content: ''; display: block;
    width: 40px; height: 1px; background: var(--accent);
  }

  .hero-name {
    font-family: 'Fraunces', serif;
    font-size: clamp(4rem, 12vw, 10rem);
    font-weight: 700; line-height: 0.9;
    letter-spacing: -0.02em;
    background: linear-gradient(135deg, #fff 30%, var(--accent) 70%, var(--accent2) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    opacity: 0; animation: fadeUp 0.8s 0.4s forwards;
  }

  .hero-role {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1rem, 3vw, 1.6rem);
    font-weight: 400; color: var(--muted);
    margin-top: 24px; letter-spacing: 0.02em;
    opacity: 0; animation: fadeUp 0.8s 0.6s forwards;
  }

  .hero-role span { color: var(--accent2); }

  .hero-desc {
    max-width: 540px;
    font-size: 0.9rem; line-height: 1.8;
    color: var(--muted); margin-top: 28px;
    opacity: 0; animation: fadeUp 0.8s 0.8s forwards;
  }

  .hero-cta {
    display: flex; gap: 16px; margin-top: 48px;
    opacity: 0; animation: fadeUp 0.8s 1s forwards;
    flex-wrap: wrap;
  }

  .btn {
    padding: 14px 32px;
    border-radius: 3px;
    font-family: 'DM Mono', monospace;
    font-size: 0.75rem; letter-spacing: 0.12em;
    text-transform: uppercase; cursor: none;
    text-decoration: none; display: inline-block;
    transition: all 0.2s;
  }
  .btn-primary {
    background: var(--accent); color: #050810;
    font-weight: 500;
  }
  .btn-primary:hover {
    background: #fff; transform: translateY(-2px);
    box-shadow: 0 0 40px rgba(79,255,176,0.3);
  }
  .btn-ghost {
    border: 1px solid var(--border); color: var(--muted);
  }
  .btn-ghost:hover { border-color: var(--accent2); color: var(--accent2); }

  /* Scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 40px; left: 60px;
    display: flex; align-items: center; gap: 12px;
    font-size: 0.7rem; letter-spacing: 0.2em;
    text-transform: uppercase; color: var(--muted);
    opacity: 0; animation: fadeUp 0.8s 1.4s forwards;
  }
  .scroll-line {
    width: 40px; height: 1px; background: var(--muted);
    transform-origin: left;
    animation: scaleX 2s 2s ease-in-out infinite alternate;
  }

  /* Grid background */
  .hero-grid {
    position: absolute; inset: 0; z-index: -1;
    background-image:
      linear-gradient(rgba(79,255,176,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(79,255,176,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    mask-image: radial-gradient(ellipse 80% 80% at 100% 20%, black, transparent);
  }

  /* Section base */
  section { padding: 100px 60px; position: relative; z-index: 1; }

  .section-tag {
    font-size: 0.68rem; letter-spacing: 0.3em;
    text-transform: uppercase; color: var(--accent);
    display: flex; align-items: center; gap: 12px;
    margin-bottom: 56px;
  }
  .section-tag::after {
    content: ''; flex: 1; max-width: 80px;
    height: 1px; background: var(--border);
  }

  /* About */
  .about-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 80px; align-items: start;
  }

  .about-heading {
    font-family: 'Fraunces', serif;
    font-size: clamp(2.5rem, 5vw, 4rem);
    font-weight: 700; line-height: 1.1;
    letter-spacing: -0.02em;
  }
  .about-heading em {
    font-style: italic; color: var(--accent);
  }

  .about-text {
    font-size: 0.88rem; line-height: 1.9;
    color: var(--muted); margin-top: 24px;
  }

  .about-stats {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 2px; margin-top: 48px;
  }
  .stat-box {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 24px;
    transition: border-color 0.2s, transform 0.2s;
  }
  .stat-box:hover { border-color: var(--accent); transform: translateY(-2px); }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 2.2rem; font-weight: 800;
    color: var(--accent); line-height: 1;
  }
  .stat-label {
    font-size: 0.7rem; letter-spacing: 0.1em;
    text-transform: uppercase; color: var(--muted);
    margin-top: 6px;
  }

  .about-list {
    list-style: none;
    display: flex; flex-direction: column; gap: 16px;
  }
  .about-list li {
    display: flex; align-items: flex-start; gap: 14px;
    font-size: 0.85rem; line-height: 1.6; color: var(--muted);
    padding: 16px;
    border: 1px solid var(--border);
    transition: border-color 0.2s;
  }
  .about-list li:hover { border-color: var(--accent2); }
  .about-list li .icon {
    width: 32px; height: 32px; flex-shrink: 0;
    border-radius: 6px; background: var(--surface2);
    display: flex; align-items: center; justify-content: center;
    font-size: 1rem;
  }

  /* Skills */
  #skills { background: var(--surface); }

  .skills-layout {
    display: grid; grid-template-columns: 320px 1fr;
    gap: 80px; align-items: start;
  }

  .skills-intro h2 {
    font-family: 'Fraunces', serif;
    font-size: 3rem; font-weight: 700;
    line-height: 1.1; letter-spacing: -0.02em;
  }
  .skills-intro p {
    font-size: 0.85rem; color: var(--muted);
    line-height: 1.8; margin-top: 20px;
  }

  .tech-grid {
    display: grid; grid-template-columns: repeat(4, 1fr);
    gap: 2px;
  }

  .tech-card {
    background: var(--bg);
    border: 1px solid var(--border);
    padding: 20px 16px;
    display: flex; flex-direction: column;
    align-items: center; gap: 10px;
    transition: all 0.25s; cursor: none;
    position: relative; overflow: hidden;
  }
  .tech-card::before {
    content: ''; position: absolute;
    inset: 0; opacity: 0;
    background: radial-gradient(circle at center, var(--glow), transparent 70%);
    transition: opacity 0.3s;
  }
  .tech-card:hover { border-color: var(--accent); transform: translateY(-3px); }
  .tech-card:hover::before { opacity: 1; }

  .tech-icon { font-size: 1.6rem; }
  .tech-name {
    font-size: 0.7rem; letter-spacing: 0.08em;
    text-transform: uppercase; color: var(--muted);
    text-align: center;
  }

  .category-label {
    font-size: 0.65rem; letter-spacing: 0.25em;
    text-transform: uppercase; color: var(--accent);
    grid-column: 1/-1; padding: 12px 0 6px;
    border-bottom: 1px solid var(--border);
  }

  /* Work */
  .work-grid {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 2px; margin-top: 0;
  }

  .work-card {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 36px;
    transition: all 0.25s;
    position: relative; overflow: hidden;
    cursor: none;
  }
  .work-card::after {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 2px; background: var(--accent);
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.3s ease;
  }
  .work-card:hover { border-color: rgba(79,255,176,0.3); transform: translateY(-4px); }
  .work-card:hover::after { transform: scaleX(1); }

  .work-num {
    font-family: 'Syne', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.2em;
    color: var(--accent); margin-bottom: 20px;
  }
  .work-title {
    font-family: 'Fraunces', serif;
    font-size: 1.4rem; font-weight: 700;
    line-height: 1.2; margin-bottom: 14px;
  }
  .work-desc {
    font-size: 0.82rem; line-height: 1.75;
    color: var(--muted);
  }
  .work-tags {
    display: flex; flex-wrap: wrap; gap: 6px;
    margin-top: 24px;
  }
  .tag {
    font-size: 0.65rem; letter-spacing: 0.1em;
    text-transform: uppercase; padding: 4px 10px;
    border: 1px solid var(--border); color: var(--muted);
    border-radius: 2px;
  }
  .tag.accent { border-color: var(--accent); color: var(--accent); }
  .tag.blue { border-color: var(--accent2); color: var(--accent2); }
  .tag.pink { border-color: var(--accent3); color: var(--accent3); }

  /* Experience timeline */
  #experience { background: var(--surface); }

  .timeline {
    display: flex; flex-direction: column;
    gap: 0; max-width: 860px; margin: 0 auto;
    position: relative;
  }
  .timeline::before {
    content: ''; position: absolute;
    left: 20px; top: 0; bottom: 0; width: 1px;
    background: var(--border);
  }

  .timeline-item {
    display: grid; grid-template-columns: 60px 1fr;
    gap: 28px; padding: 32px 0;
    border-bottom: 1px solid var(--border);
    position: relative;
  }
  .timeline-item:last-child { border-bottom: none; }

  .timeline-dot {
    width: 40px; height: 40px;
    border-radius: 50%; border: 2px solid var(--border);
    background: var(--bg);
    display: flex; align-items: center; justify-content: center;
    font-size: 1rem; flex-shrink: 0;
    position: relative; z-index: 1;
    transition: border-color 0.2s;
  }
  .timeline-item:hover .timeline-dot { border-color: var(--accent); }

  .timeline-date {
    font-size: 0.68rem; letter-spacing: 0.15em;
    text-transform: uppercase; color: var(--accent);
    margin-bottom: 8px;
  }
  .timeline-role {
    font-family: 'Syne', sans-serif;
    font-size: 1.1rem; font-weight: 700;
  }
  .timeline-org {
    font-size: 0.8rem; color: var(--accent2);
    margin-top: 2px; margin-bottom: 12px;
  }
  .timeline-desc {
    font-size: 0.82rem; line-height: 1.8;
    color: var(--muted);
  }

  /* Honors */
  .honors-grid {
    display: grid; grid-template-columns: repeat(2, 1fr);
    gap: 2px;
  }
  .honor-card {
    background: var(--surface);
    border: 1px solid var(--border);
    padding: 28px 32px;
    display: flex; align-items: center; gap: 20px;
    transition: all 0.2s;
  }
  .honor-card:hover { border-color: var(--accent3); transform: translateX(4px); }
  .honor-icon { font-size: 1.5rem; flex-shrink: 0; }
  .honor-text { font-size: 0.82rem; line-height: 1.5; color: var(--muted); }
  .honor-text strong { display: block; color: var(--text); font-family: 'Syne', sans-serif; font-size: 0.9rem; margin-bottom: 2px; }

  /* Connect */
  .connect-inner {
    max-width: 700px; margin: 0 auto; text-align: center;
  }
  .connect-inner h2 {
    font-family: 'Fraunces', serif;
    font-size: clamp(2.5rem, 6vw, 5rem);
    font-weight: 700; line-height: 1;
    letter-spacing: -0.02em;
    margin-bottom: 20px;
  }
  .connect-inner h2 span { color: var(--accent); }
  .connect-inner p {
    font-size: 0.88rem; color: var(--muted);
    line-height: 1.8; max-width: 440px; margin: 0 auto 40px;
  }

  .social-row {
    display: flex; justify-content: center;
    gap: 12px; flex-wrap: wrap; margin-top: 48px;
  }
  .social-btn {
    display: flex; align-items: center; gap: 10px;
    padding: 12px 22px;
    border: 1px solid var(--border);
    color: var(--muted); text-decoration: none;
    font-size: 0.72rem; letter-spacing: 0.12em;
    text-transform: uppercase;
    transition: all 0.2s; border-radius: 2px;
  }
  .social-btn:hover { border-color: var(--accent); color: var(--accent); }
  .social-btn svg { width: 14px; height: 14px; fill: currentColor; }

  /* Footer */
  footer {
    padding: 36px 60px;
    border-top: 1px solid var(--border);
    display: flex; justify-content: space-between;
    align-items: center;
    font-size: 0.72rem; letter-spacing: 0.08em;
    color: var(--muted);
  }
  .footer-sig { color: var(--accent); }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes scaleX {
    from { transform: scaleX(0.3); }
    to { transform: scaleX(1); }
  }

  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* Terminal blink */
  .blink {
    animation: blink 1.2s step-end infinite;
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  /* Responsive */
  @media (max-width: 900px) {
    nav { padding: 18px 24px; }
    .nav-links { display: none; }
    section { padding: 70px 24px; }
    .hero { padding: 100px 24px 60px; }
    .about-grid, .skills-layout { grid-template-columns: 1fr; gap: 40px; }
    .tech-grid { grid-template-columns: repeat(3, 1fr); }
    .work-grid { grid-template-columns: 1fr; }
    .honors-grid { grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 12px; text-align: center; }
    .scroll-hint { display: none; }
  }
</style>
</head>
<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- Ambient blobs -->
<div class="blob blob-1"></div>
<div class="blob blob-2"></div>
<div class="blob blob-3"></div>

<!-- Nav -->
<nav>
  <a href="#" class="nav-logo">ET_</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Stack</a></li>
    <li><a href="#work">Work</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#connect">Connect</a></li>
  </ul>
</nav>

<!-- Hero -->
<section class="hero" id="home">
  <div class="hero-grid"></div>
  <div class="hero-eyebrow">Available for opportunities</div>
  <h1 class="hero-name">Emmanuella<br>Turkson</h1>
  <p class="hero-role">Computer Science <span>×</span> AI Research <span>×</span> UI/UX</p>
  <p class="hero-desc">
    I build thoughtful technology — from AI security systems to intuitive digital experiences.
    Currently studying CS at Philander Smith University and exploring the intersection of
    intelligence and design.
  </p>
  <div class="hero-cta">
    <a href="#work" class="btn btn-primary">View My Work</a>
    <a href="#connect" class="btn btn-ghost">Get In Touch</a>
  </div>

  <div class="scroll-hint">
    <div class="scroll-line"></div>
    Scroll to explore
  </div>
</section>

<!-- About -->
<section id="about">
  <div class="section-tag">// 01 — About</div>
  <div class="about-grid">
    <div>
      <h2 class="about-heading reveal">Building technology<br>that <em>actually</em><br>serves people.</h2>
      <p class="about-text reveal">
        I'm a Computer Science student with a deep interest in AI, systems engineering,
        and developer tools — with a strong belief that the best technology is both
        powerful and humane. I care equally about how systems work and how they feel to use.
      </p>
      <div class="about-stats reveal">
        <div class="stat-box">
          <div class="stat-num">3+</div>
          <div class="stat-label">Years Coding</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">2</div>
          <div class="stat-label">Research Internships</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">8+</div>
          <div class="stat-label">Languages & Tools</div>
        </div>
        <div class="stat-box">
          <div class="stat-num">1</div>
          <div class="stat-label">World to Save</div>
        </div>
      </div>
    </div>
    <ul class="about-list reveal">
      <li>
        <span class="icon">🎓</span>
        <span><strong style="color:var(--text)">Philander Smith University</strong><br>Computer Science — pursuing excellence in CS fundamentals, AI, and systems programming</span>
      </li>
      <li>
        <span class="icon">💻</span>
        <span><strong style="color:var(--text)">Dell Technologies</strong><br>Software Engineering Intern — built real systems in a high-performance engineering environment</span>
      </li>
      <li>
        <span class="icon">🔬</span>
        <span><strong style="color:var(--text)">Lawrence Berkeley National Laboratory</strong><br>AI Research Intern — evaluated LLMs, analyzed security vulnerabilities and CLI output interpretation</span>
      </li>
      <li>
        <span class="icon">🌍</span>
        <span><strong style="color:var(--text)">Save Our World — Founder</strong><br>Community initiative serving underrepresented communities through mentorship and outreach</span>
      </li>
      <li>
        <span class="icon">🎨</span>
        <span><strong style="color:var(--text)">UI/UX & Product Design</strong><br>Passionate about redesigning digital products for usability, accessibility, and clarity</span>
      </li>
    </ul>
  </div>
</section>

<!-- Skills -->
<section id="skills">
  <div class="section-tag">// 02 — Tech Stack</div>
  <div class="skills-layout">
    <div class="skills-intro reveal">
      <h2>Languages,<br>tools &<br>frameworks.</h2>
      <p>My current working stack — from backend systems to AI research pipelines and frontend interfaces.</p>
    </div>
    <div class="tech-grid reveal">
      <div class="category-label">Languages</div>
      <div class="tech-card"><div class="tech-icon">🐍</div><div class="tech-name">Python</div></div>
      <div class="tech-card"><div class="tech-icon">⚙️</div><div class="tech-name">C++</div></div>
      <div class="tech-card"><div class="tech-icon">☕</div><div class="tech-name">Java</div></div>
      <div class="tech-card"><div class="tech-icon">🗄️</div><div class="tech-name">SQL</div></div>
      <div class="tech-card"><div class="tech-icon">🌐</div><div class="tech-name">JavaScript</div></div>
      <div class="tech-card"><div class="tech-icon">🔷</div><div class="tech-name">TypeScript</div></div>
      <div class="tech-card"><div class="tech-icon">🏷️</div><div class="tech-name">HTML</div></div>
      <div class="tech-card"><div class="tech-icon">🎨</div><div class="tech-name">CSS</div></div>

      <div class="category-label">Frameworks & Tools</div>
      <div class="tech-card"><div class="tech-icon">⚛️</div><div class="tech-name">React</div></div>
      <div class="tech-card"><div class="tech-icon">🐳</div><div class="tech-name">Docker</div></div>
      <div class="tech-card"><div class="tech-icon">🔀</div><div class="tech-name">Git</div></div>
      <div class="tech-card"><div class="tech-icon">🐧</div><div class="tech-name">Linux</div></div>
      <div class="tech-card"><div class="tech-icon">🧠</div><div class="tech-name">TensorFlow</div></div>
    </div>
  </div>
</section>

<!-- Work -->
<section id="work">
  <div class="section-tag">// 03 — Featured Work</div>
  <div class="work-grid">
    <div class="work-card reveal">
      <div class="work-num">01 / AI Security</div>
      <h3 class="work-title">Command Injection Detection</h3>
      <p class="work-desc">
        Evaluated large language models to analyze CLI outputs and detect command injection
        vulnerabilities. Combined AI model evaluation with practical security analysis
        to surface real-world threat vectors.
      </p>
      <div class="work-tags">
        <span class="tag accent">AI Evaluation</span>
        <span class="tag">Security Analysis</span>
        <span class="tag">CLI Systems</span>
        <span class="tag blue">LLMs</span>
      </div>
    </div>
    <div class="work-card reveal">
      <div class="work-num">02 / Product Design</div>
      <h3 class="work-title">UX Redesign Experiments</h3>
      <p class="work-desc">
        Ongoing series of redesigning everyday digital products to improve usability,
        accessibility, and information clarity. Each project starts with user research
        and ends with high-fidelity prototypes grounded in real behavior.
      </p>
      <div class="work-tags">
        <span class="tag pink">User Research</span>
        <span class="tag">Interface Design</span>
        <span class="tag">Prototyping</span>
        <span class="tag blue">Accessibility</span>
      </div>
    </div>
    <div class="work-card reveal">
      <div class="work-num">03 / Community</div>
      <h3 class="work-title">Save Our World Initiative</h3>
      <p class="work-desc">
        A grassroots initiative focused on building relationships and creating pathways
        in underrepresented communities. Projects include mentorship programs, tech
        outreach, and community service across multiple cities.
      </p>
      <div class="work-tags">
        <span class="tag accent">Mentorship</span>
        <span class="tag">Community Outreach</span>
        <span class="tag pink">Founder</span>
      </div>
    </div>
  </div>
</section>

<!-- Experience -->
<section id="experience">
  <div class="section-tag">// 04 — Experience</div>
  <div class="timeline">
    <div class="timeline-item reveal">
      <div class="timeline-dot">🔬</div>
      <div>
        <div class="timeline-date">2024</div>
        <div class="timeline-role">AI Research Intern</div>
        <div class="timeline-org">Lawrence Berkeley National Laboratory</div>
        <p class="timeline-desc">Conducted AI model evaluation and security analysis, focusing on CLI output interpretation and command injection detection using large language models.</p>
      </div>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-dot">💻</div>
      <div>
        <div class="timeline-date">2023</div>
        <div class="timeline-role">Software Engineering Intern</div>
        <div class="timeline-org">Dell Technologies</div>
        <p class="timeline-desc">Built and shipped software within a large engineering organization. Gained deep experience with enterprise-grade systems, codebases, and professional engineering workflows.</p>
      </div>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-dot">🌍</div>
      <div>
        <div class="timeline-date">Ongoing</div>
        <div class="timeline-role">Founder & Director</div>
        <div class="timeline-org">Save Our World</div>
        <p class="timeline-desc">Founded and leads an initiative dedicated to serving underrepresented communities through mentorship, technology outreach, and community service projects.</p>
      </div>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-dot">🎓</div>
      <div>
        <div class="timeline-date">Current</div>
        <div class="timeline-role">Computer Science Student</div>
        <div class="timeline-org">Philander Smith University</div>
        <p class="timeline-desc">Pursuing a CS degree with focus areas in AI systems, scalable backend development, and UI/UX strategy. Active in engineering communities and research programs.</p>
      </div>
    </div>
  </div>

  <!-- Honors -->
  <div style="margin-top: 80px;">
    <div class="section-tag" style="margin-bottom: 32px;">// Honors & Recognition</div>
    <div class="honors-grid">
      <div class="honor-card reveal">
        <div class="honor-icon">🏆</div>
        <div class="honor-text">
          <strong>Splunk HBCU Academic Scholar</strong>
          Recognized for academic excellence and potential in the tech industry
        </div>
      </div>
      <div class="honor-card reveal">
        <div class="honor-icon">🎨</div>
        <div class="honor-text">
          <strong>ColorStack Scholar</strong>
          Member of ColorStack, advancing Black and Latinx students in computing
        </div>
      </div>
      <div class="honor-card reveal">
        <div class="honor-icon">🔬</div>
        <div class="honor-text">
          <strong>Lawrence Berkeley Lab Research</strong>
          Selected for competitive AI research internship at a national laboratory
        </div>
      </div>
      <div class="honor-card reveal">
        <div class="honor-icon">💡</div>
        <div class="honor-text">
          <strong>Dell Technologies Intern</strong>
          Secured engineering internship at a Fortune 500 technology company
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Connect -->
<section id="connect" style="background: var(--surface);">
  <div class="connect-inner">
    <div class="section-tag" style="justify-content: center;">// 05 — Connect</div>
    <h2 class="reveal">Let's build<br><span>something</span><br>together.</h2>
    <p class="reveal">Open to internships, research collaborations, and conversations about AI, design, and technology that matters.</p>
    <a href="mailto:turkson.emmanuella@philander.edu" class="btn btn-primary reveal" style="font-size:0.82rem; padding: 16px 40px;">
      turkson.emmanuella@philander.edu
    </a>

    <div class="social-row reveal">
      <a href="https://www.linkedin.com/in/emmanuella-turkson/" class="social-btn" target="_blank">
        <svg viewBox="0 0 24 24"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
      <a href="https://github.com/Emmanuella-t" class="social-btn" target="_blank">
        <svg viewBox="0 0 24 24"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
        GitHub
      </a>
      <a href="https://www.instagram.com/_imanoela/" class="social-btn" target="_blank">
        <svg viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg>
        Instagram
      </a>
    </div>
  </div>
</section>

<!-- Footer -->
<footer>
  <span>© 2025 Emmanuella Turkson</span>
  <span class="footer-sig">Built with clarity & purpose <span class="blink">_</span></span>
  <span style="color: var(--muted);">CS × AI × UX</span>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.transform = `translate(${mx - 6}px, ${my - 6}px)`;
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.transform = `translate(${rx - 18}px, ${ry - 18}px)`;
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .tech-card, .work-card, .honor-card, .stat-box').forEach(el => {
    el.addEventListener('mouseenter', () => {
      ring.style.width = '56px'; ring.style.height = '56px';
      ring.style.borderColor = 'rgba(79,255,176,0.8)';
    });
    el.addEventListener('mouseleave', () => {
      ring.style.width = '36px'; ring.style.height = '36px';
      ring.style.borderColor = 'rgba(79,255,176,0.5)';
    });
  });

  // Scroll reveal
  const observer = new IntersectionObserver(entries => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), i * 80);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Animated blob following mouse slowly
  const blob1 = document.querySelector('.blob-1');
  let bx = 0, by = 0;
  document.addEventListener('mousemove', e => {
    bx = e.clientX - 300; by = e.clientY - 300;
  });
  function animateBlob() {
    blob1.style.left = bx + 'px';
    blob1.style.top = by + 'px';
    requestAnimationFrame(animateBlob);
  }
  // subtle, very slow
  let tbx = 0, tby = 0, cbx = 0, cby = 0;
  document.addEventListener('mousemove', e => { tbx = e.clientX; tby = e.clientY; });
  function slowBlob() {
    cbx += (tbx - cbx) * 0.01;
    cby += (tby - cby) * 0.01;
    blob1.style.left = (cbx - 300) + 'px';
    blob1.style.top = (cby - 300) + 'px';
    requestAnimationFrame(slowBlob);
  }
  slowBlob();
</script>

</body>
</html>

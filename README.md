<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Shivam Bhatt — Full-Stack & Shopify Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;700;800;900&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --border: #1e1e2e;
    --accent: #7c3aed;
    --accent2: #06b6d4;
    --accent3: #f59e0b;
    --text: #e2e8f0;
    --muted: #64748b;
    --card: #13131f;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.15s ease;
    mix-blend-mode: exclusion;
  }
  .cursor-ring {
    width: 40px; height: 40px;
    border: 1px solid rgba(124,58,237,0.5);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none;
    z-index: 9998;
    transition: all 0.3s ease;
    mix-blend-mode: exclusion;
  }

  /* Noise texture overlay */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 9000;
    opacity: 0.3;
  }

  /* Grid background */
  body::after {
    content: '';
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(124,58,237,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(124,58,237,0.03) 1px, transparent 1px);
    background-size: 50px 50px;
    pointer-events: none;
    z-index: 0;
  }

  /* ─── NAV ─── */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 1.2rem 3rem;
    background: rgba(10,10,15,0.8);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
  }
  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-weight: 900;
    font-size: 1.2rem;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    letter-spacing: 0.05em;
  }
  .nav-links { display: flex; gap: 2rem; list-style: none; }
  .nav-links a {
    color: var(--muted);
    text-decoration: none;
    font-size: 0.75rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--text); }
  .nav-badge {
    display: flex; align-items: center; gap: 0.5rem;
    padding: 0.4rem 1rem;
    border: 1px solid var(--accent);
    border-radius: 100px;
    font-size: 0.7rem;
    color: var(--accent);
    animation: pulse-border 2s infinite;
  }
  .nav-badge .dot {
    width: 6px; height: 6px;
    background: #22c55e;
    border-radius: 50%;
    animation: blink 1s infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.3} }
  @keyframes pulse-border {
    0%,100%{ box-shadow: 0 0 0 0 rgba(124,58,237,0.3); }
    50%{ box-shadow: 0 0 0 4px rgba(124,58,237,0); }
  }

  /* ─── HERO ─── */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column;
    justify-content: center; align-items: flex-start;
    padding: 8rem 3rem 4rem;
    position: relative;
    overflow: hidden;
  }

  /* Animated orbs */
  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(80px);
    pointer-events: none;
    animation: float-orb 8s ease-in-out infinite;
  }
  .orb-1 {
    width: 500px; height: 500px;
    background: rgba(124,58,237,0.12);
    top: -150px; right: -100px;
    animation-delay: 0s;
  }
  .orb-2 {
    width: 400px; height: 400px;
    background: rgba(6,182,212,0.08);
    bottom: -100px; left: 200px;
    animation-delay: -3s;
  }
  .orb-3 {
    width: 300px; height: 300px;
    background: rgba(245,158,11,0.06);
    top: 30%; right: 20%;
    animation-delay: -5s;
  }
  @keyframes float-orb {
    0%,100%{ transform: translate(0,0) scale(1); }
    33%{ transform: translate(-20px, 30px) scale(1.05); }
    66%{ transform: translate(15px, -20px) scale(0.95); }
  }

  .hero-eyebrow {
    display: flex; align-items: center; gap: 1rem;
    margin-bottom: 1.5rem;
    animation: slide-up 0.8s ease both;
  }
  .hero-eyebrow span {
    font-size: 0.7rem;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--accent2);
  }
  .hero-eyebrow::before {
    content: '';
    display: block;
    width: 40px; height: 1px;
    background: var(--accent2);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-weight: 900;
    font-size: clamp(3.5rem, 8vw, 8rem);
    line-height: 0.9;
    letter-spacing: -0.03em;
    margin-bottom: 0.5rem;
    animation: slide-up 0.8s ease 0.1s both;
  }
  .hero-name .line1 { display: block; color: var(--text); }
  .hero-name .line2 {
    display: block;
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 60%, var(--accent3) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-title {
    font-size: 0.85rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 2.5rem;
    animation: slide-up 0.8s ease 0.2s both;
  }
  .hero-title span { color: var(--accent3); }

  .hero-desc {
    max-width: 500px;
    line-height: 1.8;
    color: var(--muted);
    font-size: 0.85rem;
    margin-bottom: 3rem;
    animation: slide-up 0.8s ease 0.3s both;
  }

  .hero-cta {
    display: flex; gap: 1rem; flex-wrap: wrap;
    animation: slide-up 0.8s ease 0.4s both;
  }
  .btn-primary {
    display: inline-flex; align-items: center; gap: 0.5rem;
    padding: 0.9rem 2rem;
    background: linear-gradient(135deg, var(--accent), #5b21b6);
    color: white;
    text-decoration: none;
    font-size: 0.75rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    border: none;
    position: relative;
    overflow: hidden;
    transition: transform 0.2s, box-shadow 0.2s;
    clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
  }
  .btn-primary::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(255,255,255,0.2), transparent);
    opacity: 0;
    transition: opacity 0.2s;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 10px 30px rgba(124,58,237,0.4); }
  .btn-primary:hover::before { opacity: 1; }
  .btn-outline {
    display: inline-flex; align-items: center; gap: 0.5rem;
    padding: 0.9rem 2rem;
    background: transparent;
    color: var(--text);
    text-decoration: none;
    font-size: 0.75rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    border: 1px solid var(--border);
    transition: border-color 0.2s, color 0.2s;
  }
  .btn-outline:hover { border-color: var(--accent); color: var(--accent); }

  /* Scroll indicator */
  .scroll-hint {
    position: absolute; bottom: 2rem; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 0.5rem;
    animation: slide-up 1s ease 1s both;
  }
  .scroll-hint span { font-size: 0.6rem; letter-spacing: 0.2em; color: var(--muted); }
  .scroll-line {
    width: 1px; height: 60px;
    background: linear-gradient(to bottom, var(--accent), transparent);
    animation: scroll-anim 2s ease-in-out infinite;
  }
  @keyframes scroll-anim {
    0%{ transform: scaleY(0); transform-origin: top; }
    50%{ transform: scaleY(1); transform-origin: top; }
    51%{ transform: scaleY(1); transform-origin: bottom; }
    100%{ transform: scaleY(0); transform-origin: bottom; }
  }

  /* Stats bar */
  .stats-bar {
    background: var(--card);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 1.5rem 3rem;
    display: flex; gap: 3rem;
    overflow-x: auto;
    position: relative; z-index: 1;
  }
  .stat {
    display: flex; flex-direction: column;
    white-space: nowrap;
  }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 1.8rem;
    font-weight: 900;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .stat-label { font-size: 0.65rem; color: var(--muted); letter-spacing: 0.15em; text-transform: uppercase; margin-top: 0.2rem; }

  /* ─── SECTIONS ─── */
  section {
    padding: 5rem 3rem;
    position: relative; z-index: 1;
  }
  .section-header {
    display: flex; align-items: center; gap: 1.5rem;
    margin-bottom: 3rem;
  }
  .section-num {
    font-family: 'Syne', sans-serif;
    font-size: 0.7rem;
    color: var(--accent);
    letter-spacing: 0.2em;
  }
  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: 2rem;
    font-weight: 800;
    color: var(--text);
  }
  .section-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, var(--border), transparent);
  }

  /* ─── SKILLS GRID ─── */
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
  }
  .skill-card {
    background: var(--card);
    padding: 2rem;
    position: relative;
    overflow: hidden;
    transition: background 0.3s;
    cursor: default;
  }
  .skill-card::before {
    content: '';
    position: absolute; top: 0; left: 0;
    width: 100%; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s ease;
  }
  .skill-card:hover { background: #161622; }
  .skill-card:hover::before { transform: scaleX(1); }
  .skill-icon { font-size: 2rem; margin-bottom: 1rem; }
  .skill-name {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 1rem;
    margin-bottom: 0.5rem;
  }
  .skill-desc { font-size: 0.75rem; color: var(--muted); line-height: 1.7; }
  .skill-tags { display: flex; flex-wrap: wrap; gap: 0.4rem; margin-top: 1rem; }
  .tag {
    padding: 0.2rem 0.6rem;
    background: rgba(124,58,237,0.1);
    border: 1px solid rgba(124,58,237,0.2);
    font-size: 0.65rem;
    color: var(--accent);
    letter-spacing: 0.05em;
  }
  .tag.cyan {
    background: rgba(6,182,212,0.1);
    border-color: rgba(6,182,212,0.2);
    color: var(--accent2);
  }
  .tag.amber {
    background: rgba(245,158,11,0.1);
    border-color: rgba(245,158,11,0.2);
    color: var(--accent3);
  }

  /* ─── EXPERIENCE TIMELINE ─── */
  .timeline {
    display: flex; flex-direction: column; gap: 0;
    position: relative;
    padding-left: 2rem;
  }
  .timeline::before {
    content: '';
    position: absolute; left: 0; top: 0; bottom: 0;
    width: 1px;
    background: linear-gradient(to bottom, var(--accent), var(--accent2), var(--accent3), transparent);
  }
  .timeline-item {
    padding: 0 0 3rem 2rem;
    position: relative;
  }
  .timeline-item::before {
    content: '';
    position: absolute; left: -5px; top: 6px;
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    box-shadow: 0 0 0 4px rgba(124,58,237,0.2);
  }
  .timeline-item.current::before { background: #22c55e; box-shadow: 0 0 0 4px rgba(34,197,94,0.2); }
  .timeline-date { font-size: 0.65rem; color: var(--accent2); letter-spacing: 0.15em; margin-bottom: 0.5rem; }
  .timeline-role {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 1.2rem;
    margin-bottom: 0.2rem;
  }
  .timeline-company { font-size: 0.75rem; color: var(--muted); margin-bottom: 1rem; }
  .timeline-points { list-style: none; }
  .timeline-points li {
    font-size: 0.8rem;
    color: var(--muted);
    line-height: 1.7;
    padding: 0.3rem 0;
    padding-left: 1rem;
    position: relative;
  }
  .timeline-points li::before {
    content: '→';
    position: absolute; left: 0;
    color: var(--accent);
  }
  .current-badge {
    display: inline-block;
    padding: 0.15rem 0.6rem;
    background: rgba(34,197,94,0.1);
    border: 1px solid rgba(34,197,94,0.3);
    color: #22c55e;
    font-size: 0.6rem;
    letter-spacing: 0.1em;
    margin-left: 0.8rem;
    vertical-align: middle;
  }

  /* ─── PROJECTS ─── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
  }
  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    padding: 2rem;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
  }
  .project-card:hover {
    transform: translateY(-4px);
    border-color: var(--accent);
    box-shadow: 0 20px 50px rgba(124,58,237,0.1);
  }
  .project-card::after {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transition: transform 0.4s;
  }
  .project-card:hover::after { transform: scaleX(1); }
  .project-num {
    font-family: 'Syne', sans-serif;
    font-size: 3rem;
    font-weight: 900;
    color: rgba(124,58,237,0.1);
    line-height: 1;
    margin-bottom: 0.5rem;
  }
  .project-name {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 1rem;
    margin-bottom: 0.5rem;
  }
  .project-desc { font-size: 0.75rem; color: var(--muted); line-height: 1.7; margin-bottom: 1rem; }
  .project-tech { display: flex; flex-wrap: wrap; gap: 0.4rem; }

  /* ─── TECH MARQUEE ─── */
  .marquee-section {
    background: var(--card);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 1.5rem 0;
    overflow: hidden;
  }
  .marquee-track {
    display: flex;
    animation: marquee 20s linear infinite;
    width: max-content;
  }
  .marquee-section:hover .marquee-track { animation-play-state: paused; }
  @keyframes marquee {
    from{ transform: translateX(0); }
    to{ transform: translateX(-50%); }
  }
  .marquee-item {
    display: flex; align-items: center; gap: 0.6rem;
    padding: 0 2.5rem;
    font-size: 0.7rem;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
    white-space: nowrap;
    border-right: 1px solid var(--border);
  }
  .marquee-item span { color: var(--accent); }

  /* ─── CONTACT ─── */
  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    align-items: start;
  }
  .contact-big {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2.5rem, 5vw, 4rem);
    font-weight: 900;
    line-height: 1.1;
    margin-bottom: 1.5rem;
  }
  .contact-big span {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .contact-desc { font-size: 0.8rem; color: var(--muted); line-height: 1.8; margin-bottom: 2rem; }
  .contact-links { display: flex; flex-direction: column; gap: 1rem; }
  .contact-link {
    display: flex; align-items: center; gap: 1rem;
    padding: 1rem 1.5rem;
    background: var(--card);
    border: 1px solid var(--border);
    text-decoration: none;
    color: var(--text);
    transition: border-color 0.2s, transform 0.2s;
    font-size: 0.8rem;
  }
  .contact-link:hover { border-color: var(--accent); transform: translateX(4px); }
  .contact-link-icon { font-size: 1.2rem; }
  .contact-link-label { font-size: 0.6rem; color: var(--muted); letter-spacing: 0.1em; display: block; }

  /* ─── GITHUB README TERMINAL ─── */
  .terminal {
    background: #0d0d14;
    border: 1px solid var(--border);
    border-radius: 0;
    overflow: hidden;
    font-family: 'Space Mono', monospace;
  }
  .terminal-bar {
    background: #1a1a2e;
    padding: 0.8rem 1rem;
    display: flex; align-items: center; gap: 0.5rem;
    border-bottom: 1px solid var(--border);
  }
  .terminal-dot {
    width: 12px; height: 12px;
    border-radius: 50%;
  }
  .terminal-dot.red { background: #ff5f57; }
  .terminal-dot.yellow { background: #febc2e; }
  .terminal-dot.green { background: #28c840; }
  .terminal-title { margin-left: auto; font-size: 0.65rem; color: var(--muted); letter-spacing: 0.1em; }
  .terminal-body { padding: 1.5rem; }
  .terminal-line { font-size: 0.75rem; line-height: 2; }
  .t-prompt { color: var(--accent); }
  .t-cmd { color: var(--accent2); }
  .t-str { color: #f59e0b; }
  .t-comment { color: var(--muted); }
  .t-key { color: var(--accent); }
  .t-val { color: #4ade80; }
  .t-blink {
    display: inline-block;
    width: 8px; height: 1.1em;
    background: var(--accent);
    vertical-align: text-bottom;
    animation: blink 1s step-end infinite;
  }
  .typing {
    overflow: hidden;
    white-space: nowrap;
    border-right: none;
  }

  /* ─── FOOTER ─── */
  footer {
    padding: 2rem 3rem;
    border-top: 1px solid var(--border);
    display: flex; justify-content: space-between; align-items: center;
    position: relative; z-index: 1;
  }
  .footer-name {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 0.9rem;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
  .footer-note { font-size: 0.65rem; color: var(--muted); letter-spacing: 0.1em; }

  /* ─── ANIMATIONS ─── */
  @keyframes slide-up {
    from { opacity: 0; transform: translateY(30px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* Glitch effect on hover for name */
  .hero-name:hover .line1 {
    animation: glitch 0.5s ease;
  }
  @keyframes glitch {
    0%,100%{ transform: none; text-shadow: none; }
    20%{ transform: translate(-2px, 0); text-shadow: 2px 0 var(--accent2); }
    40%{ transform: translate(2px, 0); text-shadow: -2px 0 var(--accent); }
    60%{ transform: translate(0, 1px); }
  }

  /* Gradient border card */
  .grad-border {
    position: relative;
    padding: 1px;
    background: linear-gradient(135deg, var(--accent), var(--accent2), var(--accent3));
  }
  .grad-border-inner {
    background: var(--card);
    padding: 2rem;
    height: 100%;
  }

  @media (max-width: 768px) {
    nav { padding: 1rem 1.5rem; }
    .nav-links { display: none; }
    .hero { padding: 6rem 1.5rem 3rem; }
    section { padding: 3rem 1.5rem; }
    .contact-grid { grid-template-columns: 1fr; }
    .stats-bar { padding: 1rem 1.5rem; }
    footer { flex-direction: column; gap: 0.5rem; text-align: center; }
  }
</style>
</head>
<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">SB.DEV</div>
  <ul class="nav-links">
    <li><a href="#skills">Skills</a></li>
    <li><a href="#experience">Experience</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <div class="nav-badge">
    <div class="dot"></div>
    Available for work
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="orb orb-3"></div>

  <div class="hero-eyebrow">
    <span>Full-Stack Developer · Ahmedabad, IN</span>
  </div>

  <h1 class="hero-name">
    <span class="line1">Shivam</span>
    <span class="line2">Bhatt</span>
  </h1>

  <p class="hero-title">
    Shopify · WordPress · <span>React · Full-Stack</span>
  </p>

  <p class="hero-desc">
    Crafting pixel-perfect e-commerce experiences and dynamic web applications. 
    Specializing in Shopify customizations, WordPress development, and modern React frontends.
  </p>

  <div class="hero-cta">
    <a href="#contact" class="btn-primary">↗ Let's Work Together</a>
    <a href="https://github.com/shivambhatt15" target="_blank" class="btn-outline">⌘ GitHub Profile</a>
  </div>

  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- STATS BAR -->
<div class="stats-bar">
  <div class="stat">
    <span class="stat-num">4+</span>
    <span class="stat-label">Years Experience</span>
  </div>
  <div class="stat">
    <span class="stat-num">3</span>
    <span class="stat-label">Companies</span>
  </div>
  <div class="stat">
    <span class="stat-num">20+</span>
    <span class="stat-label">GitHub Repos</span>
  </div>
  <div class="stat">
    <span class="stat-num">∞</span>
    <span class="stat-label">Lines of Code</span>
  </div>
  <div class="stat">
    <span class="stat-num">MCA</span>
    <span class="stat-label">Computer Applications</span>
  </div>
</div>

<!-- TECH MARQUEE -->
<div class="marquee-section">
  <div class="marquee-track" id="marquee">
    <div class="marquee-item"><span>⬡</span> Shopify</div>
    <div class="marquee-item"><span>⬡</span> WordPress</div>
    <div class="marquee-item"><span>⬡</span> React JS</div>
    <div class="marquee-item"><span>⬡</span> JavaScript</div>
    <div class="marquee-item"><span>⬡</span> HTML5 / CSS3</div>
    <div class="marquee-item"><span>⬡</span> Bootstrap 5</div>
    <div class="marquee-item"><span>⬡</span> PHP</div>
    <div class="marquee-item"><span>⬡</span> MySQL</div>
    <div class="marquee-item"><span>⬡</span> Firebase</div>
    <div class="marquee-item"><span>⬡</span> Redux</div>
    <div class="marquee-item"><span>⬡</span> Magento 2</div>
    <div class="marquee-item"><span>⬡</span> Figma</div>
    <div class="marquee-item"><span>⬡</span> Git / GitHub</div>
    <div class="marquee-item"><span>⬡</span> REST API</div>
    <!-- Duplicate for seamless loop -->
    <div class="marquee-item"><span>⬡</span> Shopify</div>
    <div class="marquee-item"><span>⬡</span> WordPress</div>
    <div class="marquee-item"><span>⬡</span> React JS</div>
    <div class="marquee-item"><span>⬡</span> JavaScript</div>
    <div class="marquee-item"><span>⬡</span> HTML5 / CSS3</div>
    <div class="marquee-item"><span>⬡</span> Bootstrap 5</div>
    <div class="marquee-item"><span>⬡</span> PHP</div>
    <div class="marquee-item"><span>⬡</span> MySQL</div>
    <div class="marquee-item"><span>⬡</span> Firebase</div>
    <div class="marquee-item"><span>⬡</span> Redux</div>
    <div class="marquee-item"><span>⬡</span> Magento 2</div>
    <div class="marquee-item"><span>⬡</span> Figma</div>
    <div class="marquee-item"><span>⬡</span> Git / GitHub</div>
    <div class="marquee-item"><span>⬡</span> REST API</div>
  </div>
</div>

<!-- SKILLS -->
<section id="skills">
  <div class="section-header reveal">
    <span class="section-num">01</span>
    <h2 class="section-title">Core Skills</h2>
    <div class="section-line"></div>
  </div>
  <div class="skills-grid">
    <div class="skill-card reveal">
      <div class="skill-icon">🛍️</div>
      <div class="skill-name">Shopify Development</div>
      <div class="skill-desc">Building and customizing Shopify stores from scratch. Custom themes, Liquid templating, app integrations, and conversion optimization.</div>
      <div class="skill-tags">
        <span class="tag">Liquid</span>
        <span class="tag">Theme Dev</span>
        <span class="tag amber">Custom Apps</span>
        <span class="tag amber">E-Commerce</span>
      </div>
    </div>
    <div class="skill-card reveal" style="transition-delay:0.1s">
      <div class="skill-icon">🌐</div>
      <div class="skill-name">WordPress Development</div>
      <div class="skill-desc">Custom themes, plugin development, performance optimization, and complete WordPress solutions for clients.</div>
      <div class="skill-tags">
        <span class="tag cyan">Themes</span>
        <span class="tag cyan">Plugins</span>
        <span class="tag">PHP</span>
        <span class="tag">WooCommerce</span>
      </div>
    </div>
    <div class="skill-card reveal" style="transition-delay:0.2s">
      <div class="skill-icon">⚛️</div>
      <div class="skill-name">React & Frontend</div>
      <div class="skill-desc">Modern, responsive interfaces with React, Redux state management, and clean HTML5/CSS3/JS foundations.</div>
      <div class="skill-tags">
        <span class="tag">React JS</span>
        <span class="tag">Redux</span>
        <span class="tag cyan">JS ES6+</span>
        <span class="tag cyan">Bootstrap 5</span>
      </div>
    </div>
    <div class="skill-card reveal" style="transition-delay:0.3s">
      <div class="skill-icon">🗄️</div>
      <div class="skill-name">Backend & Databases</div>
      <div class="skill-desc">Full-stack capabilities with PHP, Java, SQL databases, Firebase, Magento 2 module development.</div>
      <div class="skill-tags">
        <span class="tag amber">PHP</span>
        <span class="tag amber">MySQL</span>
        <span class="tag">Firebase</span>
        <span class="tag">Magento 2</span>
      </div>
    </div>
  </div>
</section>

<!-- EXPERIENCE -->
<section id="experience" style="background: var(--card); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);">
  <div class="section-header reveal">
    <span class="section-num">02</span>
    <h2 class="section-title">Experience</h2>
    <div class="section-line"></div>
  </div>
  <div class="timeline">
    <div class="timeline-item current reveal">
      <div class="timeline-date">JUNE 2023 — PRESENT</div>
      <div class="timeline-role">Full-Stack Developer <span class="current-badge">● CURRENT</span></div>
      <div class="timeline-company">Zero Gravity Communications</div>
      <ul class="timeline-points">
        <li>Versatile full-stack development bridging design and functionality for dynamic web apps</li>
        <li>WordPress development: custom themes, plugins, performance optimization</li>
        <li>Shopify development: e-commerce stores, customizations, third-party app integrations</li>
      </ul>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-date">2023</div>
      <div class="timeline-role">Front-End Developer</div>
      <div class="timeline-company">Felix IT Systems</div>
      <ul class="timeline-points">
        <li>Created database tables and modules</li>
        <li>Re-branding module development</li>
        <li>Web design and UI implementation</li>
        <li>Built E-Commerce Furniture Website, React Covid-19 Tracker, React Image Finder</li>
      </ul>
    </div>
    <div class="timeline-item reveal">
      <div class="timeline-date">JAN — DEC 2022</div>
      <div class="timeline-role">Backend Developer</div>
      <div class="timeline-company">Magneto IT Solution Company</div>
      <ul class="timeline-points">
        <li>10 months of Magento 2 backend development</li>
        <li>Module development and re-branding modules</li>
        <li>Database administration and website design</li>
        <li>Figma layout to HTML conversion</li>
      </ul>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-header reveal">
    <span class="section-num">03</span>
    <h2 class="section-title">Projects</h2>
    <div class="section-line"></div>
  </div>
  <div class="projects-grid">
    <div class="project-card reveal">
      <div class="project-num">01</div>
      <div class="project-name">E-Commerce Furniture Website</div>
      <div class="project-desc">Full-featured furniture e-commerce store with product catalog, cart functionality, and modern UI/UX design.</div>
      <div class="project-tech">
        <span class="tag">React</span><span class="tag cyan">CSS3</span><span class="tag">JS</span>
      </div>
    </div>
    <div class="project-card reveal" style="transition-delay:0.1s">
      <div class="project-num">02</div>
      <div class="project-name">React Covid-19 Tracker</div>
      <div class="project-desc">Real-time pandemic data dashboard fetching live stats from a public API with country filtering and data visualization.</div>
      <div class="project-tech">
        <span class="tag">React</span><span class="tag amber">API</span><span class="tag cyan">Charts</span>
      </div>
    </div>
    <div class="project-card reveal" style="transition-delay:0.2s">
      <div class="project-num">03</div>
      <div class="project-name">React Image Finder</div>
      <div class="project-desc">Image search application using the Pixabay API with dynamic filtering, lazy loading, and responsive gallery layout.</div>
      <div class="project-tech">
        <span class="tag">React</span><span class="tag amber">Pixabay API</span><span class="tag">Redux</span>
      </div>
    </div>
    <div class="project-card reveal" style="transition-delay:0.3s">
      <div class="project-num">04</div>
      <div class="project-name">Online Library Management</div>
      <div class="project-desc">Complete library system with PHP backend, documentation, database design, and full CRUD operations.</div>
      <div class="project-tech">
        <span class="tag cyan">PHP</span><span class="tag">MySQL</span><span class="tag amber">HTML5</span>
      </div>
    </div>
  </div>
</section>

<!-- GITHUB README TERMINAL -->
<section style="background: var(--card); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); padding: 4rem 3rem;">
  <div class="section-header reveal">
    <span class="section-num">04</span>
    <h2 class="section-title">README.md</h2>
    <div class="section-line"></div>
  </div>
  <div class="terminal reveal">
    <div class="terminal-bar">
      <div class="terminal-dot red"></div>
      <div class="terminal-dot yellow"></div>
      <div class="terminal-dot green"></div>
      <div class="terminal-title">shivambhatt15 / README.md</div>
    </div>
    <div class="terminal-body">
      <div class="terminal-line"><span class="t-comment"># 👋 Hello World, I'm</span></div>
      <div class="terminal-line" style="margin-bottom:0.5rem"></div>
      <div class="terminal-line"><span class="t-key">const</span> <span class="t-cmd">developer</span> = {</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">name</span>: <span class="t-str">"Shivam Bhatt"</span>,</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">location</span>: <span class="t-str">"Ahmedabad, Gujarat 🇮🇳"</span>,</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">currentRole</span>: <span class="t-str">"Full-Stack Developer @ Zero Gravity"</span>,</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">specialties</span>: [</div>
      <div class="terminal-line">&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-str">"Shopify"</span>, <span class="t-str">"WordPress"</span>, <span class="t-str">"React"</span>, <span class="t-str">"PHP"</span></div>
      <div class="terminal-line">&nbsp;&nbsp;],</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">education</span>: <span class="t-str">"MCA — LJ University (Pursuing)"</span>,</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">funFact</span>: <span class="t-str">"I am Funny 😄"</span>,</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">openToWork</span>: <span class="t-val">true</span>,</div>
      <div class="terminal-line">&nbsp;&nbsp;<span class="t-key">email</span>: <span class="t-str">"shivam.bhatt1512@gmail.com"</span></div>
      <div class="terminal-line">};</div>
      <div class="terminal-line" style="margin-top:1rem">
        <span class="t-prompt">$</span> <span class="t-cmd">git</span> status <span class="t-comment">// always learning, always building</span>
      </div>
      <div class="terminal-line">
        <span class="t-val">On branch: main · Status: committed to clean code ✓</span>
      </div>
      <div class="terminal-line" style="margin-top:0.5rem">
        <span class="t-prompt">$</span> <span class="t-blink"></span>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-grid">
    <div class="reveal">
      <p class="contact-big">Let's Build<br><span>Something</span><br>Great.</p>
      <p class="contact-desc">
        Available for freelance projects, full-time opportunities, and collaborations. 
        Specializing in Shopify, WordPress, and React development.
      </p>
      <a href="mailto:shivam.bhatt1512@gmail.com" class="btn-primary" style="display:inline-flex">
        ✉ Send Email
      </a>
    </div>
    <div class="reveal" style="transition-delay:0.2s">
      <div class="contact-links">
        <a href="mailto:shivam.bhatt1512@gmail.com" class="contact-link">
          <span class="contact-link-icon">✉</span>
          <div>
            <span class="contact-link-label">Email</span>
            shivam.bhatt1512@gmail.com
          </div>
        </a>
        <a href="https://github.com/shivambhatt15" target="_blank" class="contact-link">
          <span class="contact-link-icon">⌘</span>
          <div>
            <span class="contact-link-label">GitHub</span>
            github.com/shivambhatt15
          </div>
        </a>
        <a href="https://www.linkedin.com/in/shivam-bhatt-1a36b621b/" target="_blank" class="contact-link">
          <span class="contact-link-icon">in</span>
          <div>
            <span class="contact-link-label">LinkedIn</span>
            linkedin.com/in/shivambhatt1512
          </div>
        </a>
        <a href="https://twitter.com/shivam897739369" target="_blank" class="contact-link">
          <span class="contact-link-icon">𝕏</span>
          <div>
            <span class="contact-link-label">Twitter / X</span>
            @shivam897739369
          </div>
        </a>
        <a href="https://www.instagram.com/_shivam_1512" target="_blank" class="contact-link">
          <span class="contact-link-icon">◎</span>
          <div>
            <span class="contact-link-label">Instagram</span>
            @_shivam_1512
          </div>
        </a>
        <div class="contact-link" style="cursor:default">
          <span class="contact-link-icon">📍</span>
          <div>
            <span class="contact-link-label">Location</span>
            Venus Park Heights, Ahmedabad, Gujarat
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-name">SHIVAM BHATT</div>
  <div class="footer-note">Designed & Built with ♥ · Ahmedabad 2024</div>
  <div class="footer-note">Full-Stack · Shopify · WordPress · React</div>
</footer>

<script>
// Custom cursor
const cursor = document.getElementById('cursor');
const cursorRing = document.getElementById('cursorRing');
let mouseX = 0, mouseY = 0;
let ringX = 0, ringY = 0;

document.addEventListener('mousemove', e => {
  mouseX = e.clientX; mouseY = e.clientY;
  cursor.style.left = mouseX - 6 + 'px';
  cursor.style.top = mouseY - 6 + 'px';
});

function animateRing() {
  ringX += (mouseX - ringX - 20) * 0.12;
  ringY += (mouseY - ringY - 20) * 0.12;
  cursorRing.style.left = ringX + 'px';
  cursorRing.style.top = ringY + 'px';
  requestAnimationFrame(animateRing);
}
animateRing();

document.querySelectorAll('a, button, .skill-card, .project-card').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.transform = 'scale(2)';
    cursorRing.style.transform = 'scale(1.5)';
    cursorRing.style.borderColor = 'var(--accent2)';
  });
  el.addEventListener('mouseleave', () => {
    cursor.style.transform = 'scale(1)';
    cursorRing.style.transform = 'scale(1)';
    cursorRing.style.borderColor = 'rgba(124,58,237,0.5)';
  });
});

// Scroll reveal
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach((entry, i) => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.1 });

reveals.forEach(el => observer.observe(el));

// Smooth nav link
document.querySelectorAll('a[href^="#"]').forEach(a => {
  a.addEventListener('click', e => {
    e.preventDefault();
    const target = document.querySelector(a.getAttribute('href'));
    if (target) target.scrollIntoView({ behavior: 'smooth', block: 'start' });
  });
});

// Counter animation on stat nums
function animateCounter(el, target, suffix = '') {
  const isNum = !isNaN(parseInt(target));
  if (!isNum) return;
  let current = 0;
  const end = parseInt(target);
  const step = end / 40;
  const timer = setInterval(() => {
    current += step;
    if (current >= end) { current = end; clearInterval(timer); }
    el.textContent = Math.floor(current) + suffix;
  }, 30);
}

const statNums = document.querySelectorAll('.stat-num');
const statObserver = new IntersectionObserver(entries => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const el = entry.target;
      const text = el.textContent;
      if (text === '4+') animateCounter(el, 4, '+');
      else if (text === '3') animateCounter(el, 3);
      else if (text === '20+') animateCounter(el, 20, '+');
      statObserver.unobserve(el);
    }
  });
}, { threshold: 0.5 });
statNums.forEach(el => statObserver.observe(el));
</script>
</body>
</html>

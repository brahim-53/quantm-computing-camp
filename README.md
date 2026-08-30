<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>رحلة في عالم الحوسبة الكمية — من بايثون إلى التشابك الكمي</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800;900&family=IBM+Plex+Sans+Arabic:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">

<style>
:root{
  --void:#050712; --bg:#070a18; --panel:#0b1024; --panel-2:#0e1530;
  --glass:rgba(14,20,46,.55); --glass-brd:rgba(148,180,255,.14);
  --border:rgba(148,180,255,.12); --border-soft:rgba(148,180,255,.06);
  --cyan:#2dd4ff; --cyan-dim:#1596c2; --cyan-glow:rgba(45,212,255,.35);
  --purple:#9b6bff; --purple-dim:#6d46c9; --purple-glow:rgba(155,107,255,.35);
  --green:#34e0a1; --green-dim:#1fa87a; --green-glow:rgba(52,224,161,.32);
  --gold:#f2b851; --amber:#ffb454;
  --text:#e9eefb; --text-dim:#9aa8c7; --text-faint:#5f6d8c; --danger:#ff6b81;
  --font-display:'Tajawal','Segoe UI',sans-serif;
  --font-body:'IBM Plex Sans Arabic','Tajawal',sans-serif;
  --font-mono:'JetBrains Mono','Consolas',monospace;
  --radius-sm:10px; --radius-md:16px; --radius-lg:24px;
  --ease:cubic-bezier(.22,.9,.32,1);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth;scroll-padding-top:90px}
body{background:var(--bg);color:var(--text);font-family:var(--font-body);line-height:1.85;overflow-x:hidden;direction:rtl}
a{color:inherit;text-decoration:none}
button{font:inherit;color:inherit;background:none;border:none;cursor:pointer}
ul,ol{list-style:none}
code,pre{font-family:var(--font-mono)}
@media (prefers-reduced-motion: reduce){*,*::before,*::after{animation-duration:.001ms !important;animation-iteration-count:1 !important;transition-duration:.001ms !important;scroll-behavior:auto !important}}
::selection{background:var(--cyan-glow);color:#fff}
::-webkit-scrollbar{width:10px}
::-webkit-scrollbar-track{background:var(--void)}
::-webkit-scrollbar-thumb{background:linear-gradient(var(--cyan-dim),var(--purple-dim));border-radius:10px}

.quantum-grid-bg{position:fixed;inset:0;z-index:-2;background-color:var(--void);
  background-image:radial-gradient(circle at 15% 20%,rgba(45,212,255,.10),transparent 40%),
  radial-gradient(circle at 85% 75%,rgba(155,107,255,.10),transparent 40%),
  linear-gradient(rgba(148,180,255,.05) 1px,transparent 1px),
  linear-gradient(90deg,rgba(148,180,255,.05) 1px,transparent 1px);
  background-size:auto,auto,42px 42px,42px 42px}
.noise-overlay{position:fixed;inset:0;z-index:-1;pointer-events:none;opacity:.35;mix-blend-mode:overlay;
  background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.35'/%3E%3C/svg%3E")}

.container{max-width:1180px;margin-inline:auto;padding-inline:24px}
.section{padding:90px 0;position:relative}
.stage-anchor{display:block;position:relative;top:-90px;height:0;visibility:hidden;pointer-events:none}
.section-head{max-width:760px;margin-bottom:46px}
.eyebrow{display:inline-flex;align-items:center;gap:8px;font-family:var(--font-mono);font-size:12.5px;letter-spacing:.12em;
  color:var(--cyan);background:rgba(45,212,255,.08);border:1px solid rgba(45,212,255,.25);border-radius:999px;
  padding:6px 14px;margin-bottom:18px;text-transform:uppercase}
.eyebrow.purple{color:var(--purple);background:rgba(155,107,255,.08);border-color:rgba(155,107,255,.28)}
.eyebrow.green{color:var(--green);background:rgba(52,224,161,.08);border-color:rgba(52,224,161,.28)}
.eyebrow.amber{color:var(--amber);background:rgba(255,180,84,.08);border-color:rgba(255,180,84,.28)}
.section-head h2{font-family:var(--font-display);font-weight:800;font-size:clamp(26px,4vw,40px);margin-bottom:14px;letter-spacing:-.01em}
.section-head p{color:var(--text-dim);font-size:16.5px;max-width:640px}
.glow-text{background:linear-gradient(90deg,var(--cyan),var(--purple));-webkit-background-clip:text;background-clip:text;color:transparent}
/* Reveal-on-scroll is a progressive enhancement only: content is visible
   (opacity:1) by default. JS may briefly animate elements in, but nothing
   in the page ever depends on JavaScript running for content to appear. */
.reveal{opacity:1;transform:none;transition:opacity .7s var(--ease),transform .7s var(--ease)}
.reveal.is-visible{opacity:1;transform:none}
.glass{background:var(--glass);border:1px solid var(--glass-brd);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);border-radius:var(--radius-md)}

.btn{display:inline-flex;align-items:center;justify-content:center;gap:10px;padding:13px 26px;border-radius:999px;font-weight:700;font-size:15px;
  transition:transform .25s var(--ease),box-shadow .25s var(--ease),background .25s var(--ease),border-color .25s var(--ease);white-space:nowrap}
.btn:focus-visible{outline:2px solid var(--cyan);outline-offset:3px}
.btn-primary{background:linear-gradient(90deg,var(--cyan),var(--purple));color:#051019;box-shadow:0 8px 30px -8px var(--cyan-glow)}
.btn-primary:hover{transform:translateY(-2px);box-shadow:0 14px 36px -8px var(--purple-glow)}
.btn-ghost{border:1px solid var(--border);color:var(--text);background:rgba(255,255,255,.02)}
.btn-ghost:hover{border-color:var(--cyan);color:var(--cyan);background:rgba(45,212,255,.06)}
.btn-sm{padding:9px 18px;font-size:13.5px}

.navbar{position:fixed;top:0;inset-inline:0;z-index:500;padding:14px 0;background:rgba(6,9,20,.65);
  backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);border-bottom:1px solid var(--border-soft)}
.nav-inner{display:flex;align-items:center;justify-content:space-between;gap:20px}
.brand{display:flex;align-items:center;gap:10px;font-family:var(--font-display);font-weight:800;font-size:16.5px}
.brand-mark{width:32px;height:32px;border-radius:10px;position:relative;flex-shrink:0;
  background:radial-gradient(circle at 30% 30%,var(--cyan),var(--purple) 75%);box-shadow:0 0 18px var(--cyan-glow)}
.brand-mark::after{content:"";position:absolute;inset:7px;border:1.5px solid rgba(255,255,255,.65);border-radius:50%}
.nav-links{display:flex;align-items:center;gap:4px;flex-wrap:wrap}
.nav-links a{padding:8px 13px;border-radius:999px;font-size:14px;font-weight:600;color:var(--text-dim);transition:color .2s,background .2s}
.nav-links a:hover{color:var(--text);background:rgba(255,255,255,.04)}
.nav-links a.active{color:var(--cyan);background:rgba(45,212,255,.09)}
.nav-toggle{display:none;width:42px;height:42px;border-radius:10px;border:1px solid var(--border);align-items:center;justify-content:center;flex-direction:column;gap:5px}
.nav-toggle span{width:20px;height:2px;background:var(--text);border-radius:2px;transition:transform .25s,opacity .25s}
.nav-toggle.open span:nth-child(1){transform:translateY(7px) rotate(45deg)}
.nav-toggle.open span:nth-child(2){opacity:0}
.nav-toggle.open span:nth-child(3){transform:translateY(-7px) rotate(-45deg)}
.mobile-menu{display:none;position:fixed;top:66px;inset-inline:12px;z-index:499;border-radius:var(--radius-md);padding:10px;
  flex-direction:column;gap:4px;opacity:0;transform:translateY(-12px);pointer-events:none;transition:opacity .25s var(--ease),transform .25s var(--ease)}
.mobile-menu.open{opacity:1;transform:none;pointer-events:auto}
.mobile-menu a{padding:13px 16px;border-radius:10px;font-weight:600;color:var(--text-dim)}
.mobile-menu a.active,.mobile-menu a:hover{color:var(--cyan);background:rgba(45,212,255,.08)}
.scroll-progress{position:fixed;top:0;inset-inline:0;height:3px;z-index:600;background:transparent}
.scroll-progress-bar{height:100%;width:0%;background:linear-gradient(90deg,var(--cyan),var(--purple),var(--green));transition:width .1s linear}

.hero{min-height:92vh;display:flex;align-items:center;padding-top:110px;padding-bottom:50px;position:relative;overflow:hidden}
.hero-grid{display:grid;grid-template-columns:1.05fr .95fr;gap:50px;align-items:center}
.hero-copy h1{font-family:var(--font-display);font-weight:900;font-size:clamp(32px,5vw,56px);line-height:1.2;letter-spacing:-.01em;margin-bottom:20px}
.hero-copy p.lead{font-size:17.5px;color:var(--text-dim);max-width:540px;margin-bottom:30px}
.hero-actions{display:flex;flex-wrap:wrap;gap:14px;margin-bottom:36px}
.hero-stats{display:flex;gap:28px;flex-wrap:wrap}
.hero-stat b{display:block;font-family:var(--font-display);font-size:25px;font-weight:800;
  background:linear-gradient(90deg,var(--cyan),var(--green));-webkit-background-clip:text;background-clip:text;color:transparent}
.hero-stat span{font-size:12.5px;color:var(--text-faint)}
.hero-visual{position:relative}
.circuit-card{padding:24px;position:relative}
.circuit-card .tag{font-family:var(--font-mono);font-size:12px;color:var(--text-faint);margin-bottom:14px;display:flex;justify-content:space-between;direction:ltr}
.circuit-svg-wrap{direction:ltr}
@keyframes travel{0%{offset-distance:0%;opacity:0}8%{opacity:1}92%{opacity:1}100%{offset-distance:100%;opacity:0}}
.qubit-dot{offset-path:path("M20,70 L340,70");animation:travel 3.6s linear infinite}
@keyframes pulseGate{0%,100%{filter:drop-shadow(0 0 2px var(--cyan))}50%{filter:drop-shadow(0 0 10px var(--cyan))}}
.gate-pulse{animation:pulseGate 2.4s ease-in-out infinite}

.flow-strip{display:flex;align-items:center;gap:8px;flex-wrap:wrap;direction:ltr;padding:0}
.flow-node{font-family:var(--font-mono);font-size:12.5px;padding:8px 13px;border-radius:8px;background:var(--panel-2);border:1px solid var(--border);white-space:nowrap}
.flow-node.hi{color:var(--cyan);border-color:rgba(45,212,255,.4);background:rgba(45,212,255,.08);font-weight:700}
.flow-arrow{color:var(--text-faint);font-size:14px}

.timeline{display:grid;grid-template-columns:repeat(4,1fr);gap:18px;position:relative}
.timeline::before{content:"";position:absolute;top:32px;inset-inline:6%;height:2px;
  background:linear-gradient(90deg,var(--cyan),var(--purple),var(--green),var(--amber));opacity:.35;z-index:0}
.path-card{position:relative;z-index:1;padding:20px;display:flex;flex-direction:column;gap:11px;
  transition:transform .3s var(--ease),border-color .3s var(--ease),box-shadow .3s var(--ease)}
.path-card:hover{transform:translateY(-6px);border-color:rgba(45,212,255,.35);box-shadow:0 18px 40px -18px rgba(45,212,255,.35)}
.path-num{width:42px;height:42px;border-radius:50%;display:flex;align-items:center;justify-content:center;
  font-family:var(--font-display);font-weight:800;font-size:16px;background:var(--panel-2);border:1px solid var(--border)}
.path-card[data-color="cyan"] .path-num{background:linear-gradient(135deg,var(--cyan),var(--purple));color:#04101f;border:none}
.path-card[data-color="purple"] .path-num{background:linear-gradient(135deg,var(--purple),var(--cyan));color:#0c0620;border:none}
.path-card[data-color="green"] .path-num{background:linear-gradient(135deg,var(--green),var(--cyan));color:#04150f;border:none}
.path-card[data-color="amber"] .path-num{background:linear-gradient(135deg,var(--amber),var(--gold));color:#241505;border:none}
.path-card h3{font-family:var(--font-display);font-size:18px;font-weight:800}
.path-card p{color:var(--text-dim);font-size:13.5px;flex:1}
.path-status{display:inline-flex;align-self:flex-start;align-items:center;gap:6px;font-size:12px;font-weight:700;padding:5px 12px;
  border-radius:999px;border:1px solid var(--border);color:var(--text-faint)}
.path-status.done{color:var(--green);border-color:rgba(52,224,161,.35);background:rgba(52,224,161,.08)}
.path-status.active{color:var(--cyan);border-color:rgba(45,212,255,.35);background:rgba(45,212,255,.08)}
.path-progress-track{height:6px;border-radius:999px;background:rgba(255,255,255,.06);overflow:hidden}
.path-progress-fill{height:100%;border-radius:999px;background:linear-gradient(90deg,var(--cyan),var(--green));transition:width .6s var(--ease)}
.path-pct{font-size:12px;color:var(--text-faint);font-family:var(--font-mono);direction:ltr;display:inline-block}

.stage-intro{padding:20px 22px;margin-bottom:30px;display:flex;gap:16px;align-items:flex-start}
.stage-intro .badge{flex-shrink:0;width:42px;height:42px;border-radius:12px;display:flex;align-items:center;justify-content:center;
  background:rgba(45,212,255,.1);border:1px solid rgba(45,212,255,.3);color:var(--cyan);font-weight:800}
.stage-intro p{color:var(--text-dim);font-size:14.5px}
.stage-intro strong{color:var(--text)}

.lesson-list{display:flex;flex-direction:column;gap:12px}
.lesson{border:1px solid var(--border);border-radius:var(--radius-md);overflow:hidden;background:var(--glass);transition:border-color .25s}
.lesson[open]{border-color:rgba(45,212,255,.35)}
.lesson summary{list-style:none;cursor:pointer;padding:16px 18px;display:flex;align-items:center;gap:13px;font-weight:700;font-size:15px;user-select:none}
.lesson summary::-webkit-details-marker{display:none}
.lesson-check{width:21px;height:21px;border-radius:6px;border:1.5px solid var(--border);flex-shrink:0;
  display:flex;align-items:center;justify-content:center;color:transparent;font-size:12.5px;transition:background .2s,border-color .2s,color .2s}
.lesson-check.checked{background:linear-gradient(135deg,var(--green),var(--cyan));border-color:transparent;color:#04150f}
.lesson-index{font-family:var(--font-mono);color:var(--text-faint);font-size:12.5px;min-width:24px;direction:ltr}
.lesson-title{flex:1}
.lesson-caret{color:var(--text-faint);transition:transform .25s var(--ease);flex-shrink:0}
.lesson[open] .lesson-caret{transform:rotate(180deg);color:var(--cyan)}
.lesson-body{padding:0 18px 20px 18px;color:var(--text-dim);font-size:14.5px}
.lesson-body h5{color:var(--text);font-family:var(--font-display);font-size:14.5px;margin:14px 0 6px}
.lesson-body p{margin-bottom:10px}
.lesson-body ul,.lesson-body ol{margin:0 0 10px 0;padding-inline-start:20px;list-style:disc}
.lesson-body li{margin-bottom:4px}
.lesson-body strong{color:var(--text)}
p code,li code,td code,.lesson-body code{direction:ltr;unicode-bidi:isolate;display:inline-block;background:rgba(45,212,255,.09);
  color:var(--cyan);padding:1px 7px;border-radius:5px;font-size:.92em}

.code-box{direction:ltr;unicode-bidi:isolate;text-align:left;position:relative;background:#060910;border:1px solid var(--border-soft);
  border-radius:10px;padding:14px 44px 14px 16px;overflow-x:auto;margin:10px 0;font-size:13px;color:#c9e6ff;border-inline-start:3px solid var(--cyan-dim)}
.code-box.math{border-inline-start-color:var(--purple-dim);color:#e4d7ff;font-family:var(--font-mono);padding-inline-end:16px;white-space:pre}
.code-copy{position:absolute;top:8px;right:8px;font-family:var(--font-body);font-size:11px;color:var(--text-faint);
  background:var(--panel-2);border:1px solid var(--border);border-radius:6px;padding:4px 9px;transition:color .2s,border-color .2s}
.code-copy:hover{color:var(--cyan);border-color:var(--cyan)}
.code-copy.copied{color:var(--green);border-color:var(--green)}

.mini-table{width:100%;border-collapse:collapse;margin:12px 0;font-size:13.5px}
.mini-table th,.mini-table td{border:1px solid var(--border);padding:9px 12px;text-align:right}
.mini-table th{background:rgba(45,212,255,.06);color:var(--cyan);font-family:var(--font-display)}
.mini-table td code,.mini-table th code{direction:ltr;display:inline-block}

.callout{border-radius:10px;padding:12px 14px;margin:12px 0;font-size:13.5px;border-inline-start:3px solid var(--green-dim);
  background:rgba(52,224,161,.06);color:var(--text-dim)}
.callout strong{color:var(--green)}
.callout.gold{border-inline-start-color:var(--gold);background:rgba(242,184,81,.07)}
.callout.gold strong{color:var(--gold)}
.callout.warn{border-inline-start-color:var(--danger);background:rgba(255,107,129,.07)}
.callout.warn strong{color:var(--danger)}
.callout.success{border-inline-start-color:var(--green);background:rgba(52,224,161,.1)}
.callout.success strong{color:var(--green)}

.part-divider{display:flex;align-items:center;gap:14px;margin:40px 0 22px;font-family:var(--font-mono);font-size:12.5px;color:var(--text-faint);letter-spacing:.08em}
.part-divider::before,.part-divider::after{content:"";flex:1;height:1px;background:var(--border)}

.ref-grid{display:grid;grid-template-columns:1fr 1fr;gap:20px}
@media (max-width:820px){.ref-grid{grid-template-columns:1fr}}

.progress-panel{padding:36px;display:grid;grid-template-columns:1.1fr .9fr;gap:40px;align-items:center}
.progress-ring-wrap{display:flex;align-items:center;justify-content:center;position:relative}
.progress-ring-label{position:absolute;text-align:center}
.progress-ring-label b{display:block;font-family:var(--font-display);font-size:38px;font-weight:900;direction:ltr}
.progress-ring-label span{font-size:12.5px;color:var(--text-faint)}
.progress-detail h3{font-family:var(--font-display);font-size:22px;font-weight:800;margin-bottom:10px}
.progress-detail p{color:var(--text-dim);margin-bottom:20px}
.progress-rows{display:flex;flex-direction:column;gap:15px}
.progress-row{display:flex;flex-direction:column;gap:6px}
.progress-row .row-top{display:flex;justify-content:space-between;font-size:13.5px}
.progress-row .row-top b{font-weight:700}
.progress-row .row-top span{color:var(--text-faint);font-family:var(--font-mono);direction:ltr}
.progress-actions{margin-top:24px;display:flex;gap:12px;flex-wrap:wrap}

.notes-list{display:flex;flex-direction:column;gap:14px}
.note-item{padding:18px 20px;display:flex;gap:14px;align-items:flex-start}
.note-num{flex-shrink:0;width:30px;height:30px;border-radius:8px;display:flex;align-items:center;justify-content:center;
  font-family:var(--font-mono);font-weight:700;font-size:13px;background:rgba(45,212,255,.1);border:1px solid rgba(45,212,255,.3);color:var(--cyan)}
.note-item p{color:var(--text-dim);font-size:14px}
.note-item strong{color:var(--text)}
.note-item.flag .note-num{background:rgba(255,180,84,.12);border-color:rgba(255,180,84,.35);color:var(--amber)}

/* QSilver (stage 5) reuses the same visual language as .section/.section-head/.stage-intro */
.stage-section{padding:90px 0;position:relative}
.stage-header{max-width:760px;margin-bottom:46px}
.stage-badge{display:inline-flex;align-items:center;gap:8px;font-family:var(--font-mono);font-size:12.5px;letter-spacing:.12em;
  color:var(--amber);background:rgba(255,180,84,.08);border:1px solid rgba(255,180,84,.28);border-radius:999px;
  padding:6px 14px;margin-bottom:18px;text-transform:uppercase}
.stage-header h2{font-family:var(--font-display);font-weight:800;font-size:clamp(26px,4vw,40px);margin-bottom:14px;letter-spacing:-.01em}
.stage-header p{color:var(--text-dim);font-size:16.5px;max-width:640px}
.stage-transition{padding:20px 22px;margin-top:30px;color:var(--text-dim);font-size:14.5px}
.stage-summary{margin-top:40px}
.stage-summary h3{font-family:var(--font-display);font-size:20px;font-weight:800;margin-bottom:18px}
.summary-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:16px}
@media (max-width:820px){.summary-grid{grid-template-columns:repeat(2,1fr)}}
@media (max-width:560px){.summary-grid{grid-template-columns:1fr}}
.summary-card{padding:18px;border-radius:var(--radius-md);background:var(--glass);border:1px solid var(--glass-brd);display:flex;flex-direction:column;gap:6px}
.summary-card strong{font-family:var(--font-mono);color:var(--amber);font-size:12.5px}
.summary-card span{font-family:var(--font-display);font-weight:800;font-size:15px}
.summary-card p{color:var(--text-dim);font-size:13px}
.step-flow{display:flex;flex-direction:column;gap:6px;margin:10px 0}
.step-flow li{position:relative;padding-inline-start:22px;color:var(--text-dim);font-size:14px}
.step-flow li::before{content:"›";position:absolute;inline-size:16px;right:0;color:var(--cyan);font-weight:800}
html[dir="rtl"] .step-flow li::before{right:auto;left:0}
.step-flow li::before{inset-inline-start:0}

footer{padding:50px 0 30px;border-top:1px solid var(--border-soft)}
.footer-grid{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:20px;margin-bottom:20px}
.footer-note{color:var(--text-faint);font-size:13px;text-align:center}

@media (max-width:980px){
  .hero-grid{grid-template-columns:1fr} .hero-visual{order:-1}
  .timeline{grid-template-columns:repeat(2,1fr)} .timeline::before{display:none}
  .progress-panel{grid-template-columns:1fr;padding:28px}
}
@media (max-width:720px){
  .nav-links{display:none} .nav-toggle{display:flex} .mobile-menu{display:flex}
  .section,.stage-section{padding:64px 0} .hero{padding-top:96px}
  .timeline{grid-template-columns:1fr}
  .circuit-card{padding:16px}
}

/* Hard safety net: if JavaScript never runs (disabled/blocked/erroring),
   nothing above ever put .reveal into a hidden state, so no rule is
   needed here to "unhide" it — this comment documents that guarantee. */
</style>
</head>
<body>

<div class="quantum-grid-bg"></div>
<div class="noise-overlay"></div>

<div class="scroll-progress">
  <div class="scroll-progress-bar" id="scrollBar"></div>
</div>

<header class="navbar">
  <div class="container nav-inner">

    <a href="#home" class="brand">
      <span class="brand-mark" aria-hidden="true"></span>
      <span>رحلة الحوسبة الكمية</span>
    </a>

    <nav class="nav-links" aria-label="روابط التنقل الرئيسية">
      <a href="#home" data-nav class="active">الرئيسية</a>
      <a href="#python" data-nav>بايثون</a>
      <a href="#linalg" data-nav>الجبر الخطي</a>
      <a href="#prob" data-nav>الأنظمة الاحتمالية</a>
      <a href="#quantum" data-nav>الأنظمة الكمية</a>
      <a href="#qsilver" data-nav>الخوارزميات الكمومية</a>
      <a href="#reference" data-nav>مرجع سريع</a>
      <a href="#notes" data-nav>ملاحظات</a>
    </nav>

    <button
      class="nav-toggle"
      id="navToggle"
      type="button"
      aria-expanded="false"
      aria-controls="mobileMenu"
      aria-label="فتح القائمة"
    >
      <span></span><span></span><span></span>
    </button>

  </div>
</header>

<nav class="mobile-menu" id="mobileMenu" aria-label="القائمة المتنقلة" inert>
  <a href="#home" tabindex="-1">الرئيسية</a>
  <a href="#python" tabindex="-1">بايثون</a>
  <a href="#linalg" tabindex="-1">الجبر الخطي</a>
  <a href="#prob" tabindex="-1">الأنظمة الاحتمالية</a>
  <a href="#quantum" tabindex="-1">الأنظمة الكمية</a>
  <a href="#qsilver" tabindex="-1">الخوارزميات الكمومية</a>
  <a href="#reference" tabindex="-1">مرجع سريع</a>
  <a href="#notes" tabindex="-1">ملاحظات</a>
</nav>

<!-- =========================================================
     HERO
========================================================= -->
<main>
<section class="hero" id="home">
  <div class="container hero-grid">

    <div class="hero-copy">
      <span class="eyebrow">ملخص معاد تنظيمه · QPrep → QBronze → QSilver</span>

      <h1>
        من بايثون إلى
        <span class="glow-text">الخوارزميات الكمومية</span>
      </h1>

      <p class="lead">
        هذا الملخص يسير بتسلسل تعليمي ثابت قدر الإمكان لكل مفهوم:
        <strong style="color:var(--text)">
          الفكرة الكمية ← الأساس الرياضي ← المعادلة ← معنى الرموز
          ← التفسير الكمي ← المثال ← تطبيق Python/Qiskit
        </strong>.
        تم دمج الشروحات الرياضية المتكررة وربط المفاهيم الرياضية مباشرة
        بتطبيقاتها في الحوسبة الكمية، بدءًا من الأساس البرمجي والرياضي،
        مرورًا بأساسيات الكم، وصولًا إلى خوارزميات مثل QFT وShor.
      </p>

      <div class="hero-actions">
        <a href="#python" class="btn btn-primary">ابدأ الرحلة</a>
      </div>

      <div class="hero-stats">
        <div class="hero-stat">
          <b id="statSections">5</b>
          <span>أقسام رئيسية</span>
        </div>

        <div class="hero-stat">
          <b id="statLessons">32</b>
          <span>درسًا منظّمًا</span>
        </div>

        <div class="hero-stat">
          <b>12</b>
          <span>ملاحظات وتصحيحات</span>
        </div>
      </div>
    </div>

    <div class="hero-visual">
      <div class="circuit-card glass">

        <div class="tag">
          <span>QUANTUM CIRCUIT · تعليمي</span>
          <span>|0⟩ → H → Measure</span>
        </div>

        <div class="circuit-svg-wrap">
          <svg
            viewBox="0 0 360 140"
            width="100%"
            role="img"
            aria-label="دائرة كمية بسيطة: كيوبت في الحالة صفر يمر ببوابة هادامارد ثم يُقاس"
          >

            <line
              x1="20"
              y1="70"
              x2="340"
              y2="70"
              stroke="var(--border)"
              stroke-width="2"
            />

            <g class="gate-pulse">
              <rect
                x="20"
                y="50"
                width="52"
                height="40"
                rx="8"
                fill="#0e1530"
                stroke="var(--cyan)"
                stroke-width="1.4"
              />
              <text
                x="46"
                y="75"
                fill="#e9eefb"
                font-family="JetBrains Mono, monospace"
                font-size="16"
                text-anchor="middle"
              >|0⟩</text>
            </g>

            <g class="gate-pulse" style="animation-delay:.4s">
              <rect
                x="150"
                y="45"
                width="54"
                height="50"
                rx="10"
                fill="rgba(45,212,255,0.12)"
                stroke="var(--cyan)"
                stroke-width="1.6"
              />
              <text
                x="177"
                y="76"
                fill="var(--cyan)"
                font-family="Tajawal, sans-serif"
                font-weight="800"
                font-size="20"
                text-anchor="middle"
              >H</text>
            </g>

            <g class="gate-pulse" style="animation-delay:.8s">
              <rect
                x="284"
                y="45"
                width="56"
                height="50"
                rx="10"
                fill="rgba(155,107,255,0.12)"
                stroke="var(--purple)"
                stroke-width="1.6"
              />
              <path
                d="M296 80 a16 14 0 0 1 32 0"
                fill="none"
                stroke="var(--purple)"
                stroke-width="2"
              />
              <line
                x1="312"
                y1="80"
                x2="322"
                y2="62"
                stroke="var(--purple)"
                stroke-width="2"
              />
            </g>

            <circle
              r="6"
              fill="var(--green)"
              class="qubit-dot"
            >
              <animateMotion
                dur="3.6s"
                repeatCount="indefinite"
                path="M20,70 L340,70"
              />
            </circle>

          </svg>
        </div>

        <p style="font-size:12px;color:var(--text-faint);margin-top:6px;">
          توضيح تعليمي — وليس محاكاة كمية حقيقية.
        </p>

      </div>
    </div>

  </div>
</section>


<!-- =========================================================
     SCOPE
========================================================= -->
<section class="section" style="padding-top:0">
  <div class="container">

    <div class="stage-intro glass reveal">
      <span class="badge">i</span>

      <p>
        <strong>تنبيه على النطاق:</strong>
        يغطي هذا الملخص البتات، الأنظمة الاحتمالية، المتجهات والمصفوفات،
        الجداء التنسوري، الكيوبت، التراكب، القياس، والبوابات الأساسية
        (H, X, Z, RY, CNOT, Toffoli)، إضافة إلى الأنظمة متعددة الكيوبتات،
        حالة Bell، والتشابك الكمي، ثم ينتقل إلى مستوى الخوارزميات الكمومية:
        الطور، تحويل فورييه الكمومي (QFT)، تقدير الطور (QPE)،
        إيجاد المرتبة، وخوارزمية شور.
        المادة الأصلية أوسع وتشمل أيضًا العمليات المتقدمة على دائرة الوحدة،
        الدورانات والانعكاسات، التصوير المقطعي الكمي،
        الترميز فائق الكثافة، الانتقال الآني الكمي،
        ورمي العملة الكمية بالفوتونات — وهذه غير مُغطاة هنا.
      </p>
    </div>


    <div class="timeline">

      <div class="path-card glass reveal" data-color="cyan">
        <div class="path-num">1</div>
        <h3>بايثون</h3>
        <p>
          الأدوات البرمجية الأساسية:
          المتغيرات، القوائم، الحلقات، الدوال، والرسم البياني.
        </p>
        <span class="path-status active" id="statusPython">لم تبدأ</span>
        <div class="path-progress-track">
          <div
            class="path-progress-fill"
            id="fillPython"
            style="width:0%"
          ></div>
        </div>
        <span class="path-pct" id="pctPython">0% مكتمل</span>
        <a href="#python" class="btn btn-primary btn-sm">ابدأ</a>
      </div>


      <div class="path-card glass reveal" data-color="purple">
        <div class="path-num">2</div>
        <h3>الجبر الخطي</h3>
        <p>
          المتجهات، طول المتجه، الضرب النقطي،
          المصفوفات، والجداء التنسوري ⊗ — أساس كل ما يليها.
        </p>
        <span class="path-status" id="statusLinalg">لم تبدأ</span>
        <div class="path-progress-track">
          <div
            class="path-progress-fill"
            id="fillLinalg"
            style="width:0%"
          ></div>
        </div>
        <span class="path-pct" id="pctLinalg">0% مكتمل</span>
        <a href="#linalg" class="btn btn-ghost btn-sm">ابدأ</a>
      </div>


      <div class="path-card glass reveal" data-color="green">
        <div class="path-num">3</div>
        <h3>الأنظمة الاحتمالية</h3>
        <p>
          البت، الحالة الاحتمالية، مصفوفة الانتقال،
          والارتباط الكلاسيكي — الجسر الحدسي نحو الكم.
        </p>
        <span class="path-status" id="statusProb">لم تبدأ</span>
        <div class="path-progress-track">
          <div
            class="path-progress-fill"
            id="fillProb"
            style="width:0%"
          ></div>
        </div>
        <span class="path-pct" id="pctProb">0% مكتمل</span>
        <a href="#prob" class="btn btn-ghost btn-sm">ابدأ</a>
      </div>


      <div class="path-card glass reveal" data-color="amber">
        <div class="path-num">4</div>
        <h3>الأنظمة الكمية</h3>
        <p>
          الكيوبت، التراكب، البوابات، القياس،
          الأنظمة متعددة الكيوبتات، Bell، والتشابك الكمي.
        </p>
        <span class="path-status" id="statusQuantum">لم تبدأ</span>
        <div class="path-progress-track">
          <div
            class="path-progress-fill"
            id="fillQuantum"
            style="width:0%"
          ></div>
        </div>
        <span class="path-pct" id="pctQuantum">0% مكتمل</span>
        <a href="#quantum" class="btn btn-ghost btn-sm">ابدأ</a>
      </div>


      <div class="path-card glass reveal" data-color="amber">
        <div class="path-num">5</div>
        <h3>الخوارزميات الكمومية</h3>
        <p>
          الطور والتداخل، تحويل فورييه الكمومي، تقدير الطور،
          إيجاد المرتبة، وخوارزمية شور.
        </p>
        <span class="path-status" id="statusQsilver">لم تبدأ</span>
        <div class="path-progress-track">
          <div
            class="path-progress-fill"
            id="fillQsilver"
            style="width:0%"
          ></div>
        </div>
        <span class="path-pct" id="pctQsilver">0% مكتمل</span>
        <a href="#qsilver" class="btn btn-ghost btn-sm">ابدأ</a>
      </div>

    </div>

  </div>
</section>


<!-- =========================================================
     PART 1 · PYTHON
========================================================= -->
<section class="section" id="python">
  <div class="container">

    <div class="section-head reveal">
      <span class="eyebrow">القسم 1 · تحضيري</span>
      <h2>أساسيات بايثون</h2>
      <p>
        قسم برمجي تمهيدي يجهّزك بالأدوات التي ستستخدمها
        لاحقًا لتمثيل المتجهات والمصفوفات والحالات الكمية.
      </p>
    </div>


    <div class="lesson-list reveal" id="listPython">

      <!-- Python 01 -->
      <details class="lesson" data-lesson="python-01" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">01</span>
          <span class="lesson-title">Jupyter Notebook</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            بيئة العمل الأساسية لتجربة الأكواد وكتابة الملاحظات،
            وتتكون أساسًا من نوعين من الخلايا:
          </p>

          <ul>
            <li>
              <strong>Code</strong>
              — لكتابة كود Python وتشغيله.
            </li>
            <li>
              <strong>Markdown</strong>
              — للتوثيق والشرح وكتابة المعادلات.
            </li>
          </ul>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
# Shift + Enter : تشغيل الخلية والانتقال للتالية
print("Hello Quantum World!")
          </div>

          <div class="callout gold">
            <strong>تنبيه عملي:</strong>
            شغّل الخلايا بالتسلسل من الأعلى للأسفل لتفادي
            أخطاء المتغيرات المفقودة.
          </div>

        </div>
      </details>


      <!-- Python 02 -->
      <details class="lesson" data-lesson="python-02" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">02</span>
          <span class="lesson-title">المتغيرات وأنواع البيانات</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <table class="mini-table">
            <thead>
              <tr>
                <th>نوع البيانات</th>
                <th>النوع في Python</th>
                <th>مثال</th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <td>أعداد صحيحة</td>
                <td><code>int</code></td>
                <td><code>qubits_count = 5</code></td>
              </tr>

              <tr>
                <td>أعداد عشرية</td>
                <td><code>float</code></td>
                <td><code>probability = 0.85</code></td>
              </tr>

              <tr>
                <td>سلاسل نصية</td>
                <td><code>str</code></td>
                <td><code>circuit_name = "Bell"</code></td>
              </tr>

              <tr>
                <td>قيم منطقية</td>
                <td><code>bool</code></td>
                <td><code>is_entangled = True</code></td>
              </tr>
            </tbody>
          </table>

          <div class="callout">
            <strong>انتبه:</strong>
            <code>=</code> تعني إسناد قيمة،
            بينما <code>==</code> تستخدم للمقارنة بين قيمتين.
          </div>

        </div>
      </details>


      <!-- Python 03 -->
      <details class="lesson" data-lesson="python-03" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">03</span>
          <span class="lesson-title">العمليات الحسابية</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
a = 13
b = 5

a / b    # 2.6   قسمة عادية
a // b   # 2     قسمة صحيحة مع تقريب للأسفل
a % b    # 3     باقي القسمة
a ** 2   # 169   أس / تربيع
          </div>

        </div>
      </details>


      <!-- Python 04 -->
      <details class="lesson" data-lesson="python-04" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">04</span>
          <span class="lesson-title">Strings — النصوص</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            كل حرف داخل النص يمتلك فهرسًا رقميًا
            (Index) يبدأ من الصفر.
          </p>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
name = "Ibrahim"

print(name[0])   # "I"
print(name[6])   # "m"
print(len(name)) # 7
          </div>

        </div>
      </details>


      <!-- Python 05 -->
      <details class="lesson" data-lesson="python-05" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">05</span>
          <span class="lesson-title">Lists — القوائم</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            القوائم من أبسط الطرق لتمثيل مجموعة من القيم،
            ويمكن استخدامها تمهيدًا لتمثيل المتجهات.
          </p>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
state_vector = [0.707, 0.707]

alpha = state_vector[0]

state_vector.append(0.0)
          </div>

        </div>
      </details>


      <!-- Python 06 -->
      <details class="lesson" data-lesson="python-06" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">06</span>
          <span class="lesson-title">Loops &amp; Conditions</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            تستخدم الحلقات والشروط لمعالجة نتائج القياسات
            المتكررة (Shots).
          </p>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
results = ["0", "1", "0", "0", "1"]

zeros_count = 0

for shot in results:
    if shot == "0":
        zeros_count += 1

print(f"Total zero states: {zeros_count}")
          </div>

        </div>
      </details>


      <!-- Python 07 -->
      <details class="lesson" data-lesson="python-07" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">07</span>
          <span class="lesson-title">Functions — الدوال</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
def check_normalization(alpha, beta):
    prob_sum = abs(alpha)**2 + abs(beta)**2
    return abs(prob_sum - 1.0) < 1e-5

print(check_normalization(1/np.sqrt(2), 1/np.sqrt(2)))  # True
          </div>

          <div class="callout">
            <strong>ملاحظة:</strong>
            استخدام <code>abs(z)**2</code> يجعل الدالة مناسبة
            للسعات الحقيقية والمركّبة معًا.
          </div>

        </div>
      </details>


      <!-- Python 08 -->
      <details class="lesson" data-lesson="python-08" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">08</span>
          <span class="lesson-title">Matplotlib — الرسم البياني</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            يمكن استخدام الرسم البياني لعرض تكرارات نتائج القياس.
          </p>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import matplotlib.pyplot as plt

counts = {'00': 512, '11': 488}

plt.bar(counts.keys(), counts.values())
plt.xlabel('State')
plt.ylabel('Counts')
plt.show()
          </div>

        </div>
      </details>

    </div>
  </div>
</section>


<!-- =========================================================
     PART 2 · LINEAR ALGEBRA
========================================================= -->
<section class="section" id="linalg">
  <div class="container">

    <div class="section-head reveal">
      <span class="eyebrow purple">القسم 2 · أساس رياضي موحّد</span>

      <h2>الجبر الخطي للحوسبة الكمية</h2>

      <p>
        العلاقة الأساسية التي ستتكرر طوال هذا القسم:
        <strong style="color:var(--text)">
          مصفوفة Matrix ← بوابة كمية Quantum Gate ← تحويل حالة الكيوبت
        </strong>
      </p>
    </div>


    <div class="stage-intro glass reveal">

      <span class="badge">Σ</span>

      <div>

        <p style="margin-bottom:10px">
          <strong>
            قاموس الرموز — من الرياضيات إلى Python:
          </strong>
          الرمز يعبّر عن الفكرة الرياضية،
          والكود يترجمها إلى عملية برمجية.
        </p>

        <table class="mini-table">

          <thead>
            <tr>
              <th>الرمز</th>
              <th>المعنى</th>
              <th>في Python</th>
            </tr>
          </thead>

          <tbody>

            <tr>
              <td><code>×</code></td>
              <td>ضرب عددي</td>
              <td><code>*</code></td>
            </tr>

            <tr>
              <td><code>·</code></td>
              <td>ضرب نقطي</td>
              <td><code>np.dot(u, v)</code></td>
            </tr>

            <tr>
              <td><code>@</code></td>
              <td>ضرب مصفوفة في متجه</td>
              <td><code>M @ v</code></td>
            </tr>

            <tr>
              <td><code>⊗</code></td>
              <td>الجداء التنسوري</td>
              <td><code>np.kron(a, b)</code></td>
            </tr>

            <tr>
              <td><code>≈</code></td>
              <td>تقريبًا يساوي</td>
              <td><code>np.isclose()</code></td>
            </tr>

            <tr>
              <td><code>|0⟩</code></td>
              <td>حالة الأساس صفر</td>
              <td><code>np.array([[1],[0]])</code></td>
            </tr>

          </tbody>

        </table>

      </div>
    </div>


    <div class="lesson-list reveal" id="listLinalg">

      <!-- Linalg 01 -->
      <details class="lesson" data-lesson="linalg-01" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">01</span>
          <span class="lesson-title">المتجه (Vector)</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            المتجه هو ترتيب من القيم يستخدم لتمثيل المعلومات.
            وفي الحوسبة الكمية سنستخدم متجهات الحالة لتمثيل حالة الكيوبت.
          </p>

          <h5>مثال رياضي</h5>

          <div class="code-box math">
v =
[ 1  -2   0   5 ]ᵀ

3v =
[  3  -6   0  15 ]ᵀ
          </div>

          <p>
            ضرب المتجه في عدد Scalar يعني ضرب كل عنصر في ذلك العدد.
          </p>

          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np

x, y = 0.6, 0.4

v = np.array([
    [x],
    [y]
])
          </div>

          <div class="callout">
            <strong>انتبه:</strong>
            <code>[1, 2]</code> متجه أحادي البعد،
            بينما <code>[[1], [2]]</code> مصفوفة أبعادها
            <code>(2, 1)</code>.
            هذا الفرق يصبح مهمًا عند استخدام <code>@</code>.
          </div>

        </div>
      </details>


      <!-- Linalg 02 -->
      <details class="lesson" data-lesson="linalg-02" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">02</span>
          <span class="lesson-title">طول المتجه (Norm)</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            الـNorm يقيس طول أو حجم المتجه.
            وفي الحوسبة الكمية يرتبط مباشرة بشرط تطبيع متجه الحالة.
          </p>

          <h5>المعادلة</h5>

          <div class="code-box math">
إذا كان:

v = [ x  y ]ᵀ

فإن:

‖v‖ = √(|x|² + |y|²)
          </div>

          <h5>مثال</h5>

          <div class="code-box math">
v = [ 3  4 ]ᵀ

‖v‖ = √(3² + 4²)

‖v‖ = √25 = 5
          </div>

          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
v = np.array([3.0, 4.0])

norm = np.linalg.norm(v)

print(norm)   # 5.0
          </div>

          <div class="callout">
            <strong>الربط بالكم:</strong>
            متجه الحالة الكمية يجب أن يكون مُطبّعًا،
            أي أن معياره يساوي 1.
          </div>

        </div>
      </details>


      <!-- Linalg 03 -->
      <details class="lesson" data-lesson="linalg-03" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">03</span>
          <span class="lesson-title">الضرب النقطي وInner Product</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            في المتجهات الحقيقية يمكن استخدام الضرب النقطي المعتاد.
            أما في الفضاء المركب المستخدم في الحوسبة الكمية،
            فيُستخدم الـInner Product مع المرافق المركب.
          </p>

          <h5>الضرب النقطي للمتجهات الحقيقية</h5>

          <div class="code-box math">
u = [ u₁  u₂  u₃ ]

v = [ v₁  v₂  v₃ ]

u · v = u₁v₁ + u₂v₂ + u₃v₃
          </div>

          <h5>مثال</h5>

          <div class="code-box math">
u = [1  2  3]

v = [4  5  6]

u · v
= (1×4) + (2×5) + (3×6)
= 4 + 10 + 18
= 32
          </div>

          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
u = np.array([1, 2, 3])
v = np.array([4, 5, 6])

result = np.dot(u, v)

print(result)   # 32
          </div>

          <div class="callout">
            <strong>الربط بالكم:</strong>
            يُستخدم الـInner Product لمقارنة الحالات الكمية،
            ومنه يمكن التحقق من التعامد بين الحالات.
          </div>

        </div>
      </details>


      <!-- Linalg 04 -->
      <details class="lesson" data-lesson="linalg-04" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">04</span>
          <span class="lesson-title">المصفوفة (Matrix) وعملياتها</span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            المصفوفة ترتيب مستطيل من الأعداد.
            وفي الحوسبة الكمية تستخدم المصفوفات لتمثيل البوابات
            والتحويلات التي تؤثر في متجه الحالة.
          </p>

          <h5>مثال على مصفوفة</h5>

          <div class="code-box math">
M =
[ 1   0 ]
[ 0  -1 ]
          </div>

          <h5>المعادلة الأساسية</h5>

          <div class="code-box math">
v' = Mv
          </div>

          <p>
            حيث:
          </p>

          <ul>
            <li><code>v</code> متجه الحالة قبل التحويل.</li>
            <li><code>M</code> مصفوفة التحويل.</li>
            <li><code>v'</code> متجه الحالة بعد التحويل.</li>
          </ul>

          <h5>في Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
M = np.array([
    [1,  0],
    [0, -1]
])

v_new = M @ v
          </div>

          <div class="callout warn">
            <strong>خاصية مهمة:</strong>
            ضرب المصفوفات ليس تبادليًا بشكل عام:

            <div class="code-box math">
AB ≠ BA
            </div>

            لذلك يمكن أن يؤدي تغيير ترتيب تطبيق التحويلات
            إلى تغيير النتيجة النهائية.
          </div>

        </div>
      </details>


      <!-- Linalg 05 -->
      <details class="lesson" data-lesson="linalg-05" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">05</span>
          <span class="lesson-title">
            الجداء التنسوري ⊗ (Tensor Product)
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            الجداء التنسوري هو الأداة الأساسية لبناء
            الأنظمة المركبة من أكثر من عنصر،
            ويصبح مهمًا جدًا عند الانتقال من كيوبت واحد
            إلى عدة كيوبتات.
          </p>

          <h5>مثال رياضي</h5>

          <div class="code-box math">
u = [ -2   3 ]

v = [ 1   2  -3 ]

u ⊗ v
=
[ -2×1
  -2×2
  -2×(-3)
   3×1
   3×2
   3×(-3) ]

=
[ -2
  -4
   6
   3
   6
  -9 ]
          </div>

          <p>
            إذا كان طول المتجه الأول <code>2</code>
            وطول المتجه الثاني <code>3</code>،
            فإن طول الناتج يساوي:

            <code>2 × 3 = 6</code>.
          </p>

          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
u = np.array([-2, 3])
v = np.array([1, 2, -3])

uv = np.kron(u, v)

print(uv)
# [-2 -4  6  3  6 -9]
          </div>

          <div class="callout">
            <strong>الربط بالكم:</strong>
            عند وجود <code>n</code> كيوبتات،
            يحتوي متجه الحالة العام على
            <code>2ⁿ</code> سعة.
          </div>

        </div>
      </details>

    </div>
  </div>
</section>


<!-- =========================================================
     PART 3 · CLASSICAL PROBABILISTIC SYSTEMS
========================================================= -->
<section class="section" id="prob">
  <div class="container">

    <div class="section-head reveal">

      <span class="eyebrow green">
        القسم 3 · جسر نحو الكم
      </span>

      <h2>الأنظمة الاحتمالية الكلاسيكية</h2>

      <p>
        قبل الانتقال إلى الكيوبت،
        نبني حدسًا باستخدام الأنظمة الاحتمالية الكلاسيكية.
        ستتكرر أفكار المتجهات والمصفوفات والجداء التنسوري
        لاحقًا في الأنظمة الكمية، لكن مع اختلاف مهم:
        الأنظمة الكمية تستخدم السعات وليس الاحتمالات مباشرة.
      </p>

    </div>


    <div class="lesson-list reveal" id="listProb">


      <!-- Prob 01 -->
      <details class="lesson" data-lesson="prob-01" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">01</span>
          <span class="lesson-title">
            البت الكلاسيكي والمؤثرات أحادية البت
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            البت الكلاسيكي له حالتان فقط:
            <code>0</code> أو <code>1</code>.
            توجد أربع دوال Boolean ممكنة على بت واحد.
          </p>

          <table class="mini-table">

            <thead>
              <tr>
                <th>المؤثر</th>
                <th>التأثير</th>
                <th>المصفوفة</th>
                <th>قابل للعكس؟</th>
              </tr>
            </thead>

            <tbody>

              <tr>
                <td>Identity (I)</td>
                <td>0→0 ، 1→1</td>
                <td><code>[[1,0],[0,1]]</code></td>
                <td>نعم</td>
              </tr>

              <tr>
                <td>NOT</td>
                <td>0→1 ، 1→0</td>
                <td><code>[[0,1],[1,0]]</code></td>
                <td>نعم</td>
              </tr>

              <tr>
                <td>Constant ZERO</td>
                <td>0→0 ، 1→0</td>
                <td><code>[[1,1],[0,0]]</code></td>
                <td>لا</td>
              </tr>

              <tr>
                <td>Constant ONE</td>
                <td>0→1 ، 1→1</td>
                <td><code>[[0,0],[1,1]]</code></td>
                <td>لا</td>
              </tr>

            </tbody>

          </table>


          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
NOT = np.array([
    [0, 1],
    [1, 0]
])

zero = np.array([
    [1],
    [0]
])

one = NOT @ zero

print(one)
# [[0],
#  [1]]
          </div>


          <div class="callout">
            <strong>الربط بالكم:</strong>
            التطور الكمي المغلق يستخدم عمليات قابلة للعكس
            تمثلها مصفوفات Unitary.
          </div>

        </div>
      </details>


      <!-- Prob 02 -->
      <details class="lesson" data-lesson="prob-02" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">02</span>
          <span class="lesson-title">
            الحالة الاحتمالية (Probabilistic State)
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <h5>المعادلة</h5>

          <div class="code-box math">
v =
[ p₀ ]
[ p₁ ]

حيث:

p₀ ≥ 0
p₁ ≥ 0
p₀ + p₁ = 1
          </div>


          <table class="mini-table">

            <thead>
              <tr>
                <th>الحالة</th>
                <th>المتجه</th>
              </tr>
            </thead>

            <tbody>

              <tr>
                <td>البت مؤكد = 0</td>
                <td><code>[1, 0]ᵀ</code></td>
              </tr>

              <tr>
                <td>البت مؤكد = 1</td>
                <td><code>[0, 1]ᵀ</code></td>
              </tr>

              <tr>
                <td>عملة عادلة</td>
                <td><code>[0.5, 0.5]ᵀ</code></td>
              </tr>

            </tbody>

          </table>


          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
p0, p1 = 0.5, 0.5

v = np.array([
    [p0],
    [p1]
])
          </div>


          <div class="callout warn">
            <strong>تنبيه:</strong>
            هذه قيم احتمالات كلاسيكية.
            لا تخلط بينها وبين السعات (Amplitudes)
            التي سنستخدمها في الحالة الكمية.
          </div>

        </div>
      </details>


      <!-- Prob 03 -->
      <details class="lesson" data-lesson="prob-03" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">03</span>
          <span class="lesson-title">
            مصفوفة الانتقال (Transition Matrix)
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <h5>المعادلة</h5>

          <div class="code-box math">
M =
[ 0.5   0.5 ]
[ 0.5   0.5 ]

v =
[ 1 ]
[ 0 ]

v_new = Mv

v_new =
[ 0.5 ]
[ 0.5 ]
          </div>


          <p>
            مع استخدام متجه حالة عمودي،
            يجب أن يكون مجموع عناصر كل عمود في مصفوفة الانتقال
            مساويًا لـ <code>1</code>، مع كون جميع العناصر غير سالبة.
          </p>


          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
M = np.array([
    [0.5, 0.5],
    [0.5, 0.5]
])

v = np.array([
    [1.0],
    [0.0]
])

v_new = M @ v
          </div>


          <h5>مثال تطبيقي — لعبة عملتين منحازتين</h5>

          <div class="code-box math">
GameCoins =
[ 0.6   0.3 ]
[ 0.4   0.7 ]
          </div>


          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
new_head = head * 0.6 + tail * 0.3
new_tail = head * 0.4 + tail * 0.7

head, tail = new_head, new_tail
          </div>


          <div class="callout">
            نستخدم متغيرين جديدين لأن
            <code>new_tail</code>
            يجب أن يعتمد على القيم القديمة،
            وليس على قيمة <code>head</code>
            بعد تحديثها.
          </div>


          <h5>محاكاة عملة منحازة بنسبة 60%</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from random import randrange

heads = tails = 0

for _ in range(1000):
    r = randrange(10)

    if r < 6:
        heads += 1
    else:
        tails += 1

print("heads ratio =", heads / 1000)
          </div>

        </div>
      </details>


      <!-- Prob 04 -->
      <details class="lesson" data-lesson="prob-04" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">04</span>
          <span class="lesson-title">
            الارتباط الكلاسيكي بين بتين
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            نظام من بتين يمتلك أربع حالات:
            <code>00</code>،
            <code>01</code>،
            <code>10</code>،
            <code>11</code>.
          </p>


          <h5>تمثيل الحالة</h5>

          <div class="code-box math">
v =
[ p₀₀ ]
[ p₀₁ ]
[ p₁₀ ]
[ p₁₁ ]
          </div>


          <p>
            إذا كان البتان مستقلين،
            يمكن كتابة التوزيع المشترك باستخدام الجداء التنسوري:
          </p>


          <div class="code-box math">
v = v_A ⊗ v_B
          </div>


          <h5>مثال — بتان مستقلان</h5>

          <div class="code-box math">
[0.5, 0.5]ᵀ ⊗ [0.5, 0.5]ᵀ

=

[0.25, 0.25, 0.25, 0.25]ᵀ
          </div>


          <h5>مثال — ارتباط كلاسيكي</h5>

          <div class="code-box math">
v =
[0.5,
 0,
 0,
 0.5]ᵀ
          </div>


          <p>
            هذا التوزيع لا يمكن كتابته كجداء تنسوري
            لتوزيعين مستقلين.
          </p>


          <div class="callout">
            <strong>ملاحظة مهمة:</strong>
            الارتباط الكلاسيكي ليس هو التشابك الكمي،
            لكنه يقدم حدسًا أوليًا لفكرة وجود ترابط
            بين مكونات نظام مركب.
          </div>

        </div>
      </details>


      <!-- Prob 05 -->
      <details class="lesson" data-lesson="prob-05" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">05</span>
          <span class="lesson-title">
            مراجعة سريعة والانتقال للكم
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <ul>

            <li>
              <strong>Bit:</strong>
              يأخذ القيمة <code>0</code> أو <code>1</code>.
            </li>

            <li>
              <strong>Probabilistic State:</strong>
              متجه احتمالات غير سالبة مجموعها <code>1</code>.
            </li>

            <li>
              <strong>Transition Matrix:</strong>
              <code>v_new = M @ v</code>.
            </li>

            <li>
              <strong>Tensor Product:</strong>
              <code>np.kron()</code>
              لبناء الأنظمة المركبة.
            </li>

            <li>
              <strong>Correlation:</strong>
              التوزيع المشترك لا يساوي بالضرورة
              جداء التوزيعين الهامشيين.
            </li>

          </ul>


          <div class="callout gold">

            <strong>الانتقال للكم:</strong>

            في النظام الاحتمالي نتعامل مباشرة مع احتمالات
            غير سالبة ومجموعها يساوي <code>1</code>.

            في النظام الكمي نتعامل مع
            <strong>السعات (Amplitudes)</strong>،
            ويمكن أن تكون السعات سالبة أو مركبة،
            ثم نحصل على الاحتمالات من مربع القيمة المطلقة للسعة.

          </div>

        </div>
      </details>

    </div>
  </div>
</section>


<!-- =========================================================
     PART 4 · QUANTUM SYSTEMS
========================================================= -->
<section class="section" id="quantum">

  <div class="container">

    <div class="section-head reveal">

      <span class="eyebrow amber">
        القسم 4 · التطبيق الكمي
      </span>

      <h2>الأنظمة الكمية</h2>

      <p>
        من الكيوبت والتراكب إلى البوابات،
        القياس، الأنظمة متعددة الكيوبتات،
        حالة Bell، والتشابك الكمي.
      </p>

    </div>


    <div class="lesson-list reveal" id="listQuantum">


      <!-- Quantum 01 -->
      <details class="lesson" data-lesson="quantum-01" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">01</span>
          <span class="lesson-title">
            الكيوبت والتراكب الكمي
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            الكيوبت هو الوحدة الأساسية للمعلومات الكمية.
            بخلاف البت الكلاسيكي، يمكن وصف حالته
            بتركيب خطي من حالتي الأساس
            <code>|0⟩</code> و<code>|1⟩</code>.
          </p>


          <h5>التمثيل الرياضي لحالتي الأساس</h5>

          <div class="code-box math">
|0⟩ =
[ 1 ]
[ 0 ]

|1⟩ =
[ 0 ]
[ 1 ]
          </div>


          <h5>المعادلة العامة لحالة كيوبت</h5>

          <div class="code-box math">
|ψ⟩ = α|0⟩ + β|1⟩
          </div>


          <h5>معنى الرموز</h5>

          <ul>

            <li>
              <code>|ψ⟩</code>:
              متجه حالة الكيوبت.
            </li>

            <li>
              <code>|0⟩</code> و<code>|1⟩</code>:
              حالتا الأساس الحسابي.
            </li>

            <li>
              <code>α</code> و<code>β</code>:
              السعات الكمية (Amplitudes).
            </li>

          </ul>


          <h5>شرط التطبيع</h5>

          <div class="code-box math">
|α|² + |β|² = 1
          </div>


          <p>
            شرط التطبيع يعني أن مجموع احتمالات نتائج القياس
            في الأساس الحسابي يساوي <code>1</code>.
          </p>


          <h5>التفسير الكمي</h5>

          <div class="code-box math">
P(0) = |α|²

P(1) = |β|²
          </div>


          <p>
            عند القياس في الأساس الحسابي،
            نحصل على نتيجة كلاسيكية واحدة:
            <code>0</code> أو <code>1</code>.
            ويحدد مربع القيمة المطلقة لكل سعة احتمال ظهور النتيجة المقابلة.
          </p>


          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
alpha = 1 / np.sqrt(2)
beta  = 1 / np.sqrt(2)

psi = np.array([
    [alpha],
    [beta]
])
          </div>

        </div>
      </details>


      <!-- Quantum 02 -->
      <details class="lesson" data-lesson="quantum-02" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">02</span>
          <span class="lesson-title">
            التمثيل بزاوية — دائرة الوحدة
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            عندما تكون السعات حقيقية،
            يمكن تمثيل الحالة باستخدام زاوية واحدة.
          </p>


          <h5>المعادلة</h5>

          <div class="code-box math">
|ψ⟩ = cos(θ)|0⟩ + sin(θ)|1⟩
          </div>


          <h5>أمثلة</h5>

          <div class="code-box math">
θ = 0
→ |ψ⟩ = |0⟩

θ = π/2
→ |ψ⟩ = |1⟩

θ = π/4
→ |ψ⟩ = (|0⟩ + |1⟩)/√2
          </div>


          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from math import sin, cos, pi

theta = pi / 4

alpha = cos(theta)
beta  = sin(theta)
          </div>


          <div class="callout warn">

            <strong>مهم:</strong>

            الدوال المثلثية في Python وQiskit
            تستخدم الزوايا بوحدة الراديان.

            <br><br>

            انتبه إلى أن الزاوية المستخدمة هنا
            تختلف عن معامل الزاوية في بوابة
            <code>RY(θ)</code>، حيث تظهر
            <code>θ/2</code> داخل الجيب وجيب التمام.

          </div>

        </div>
      </details>


      <!-- Quantum 03 -->
      <details class="lesson" data-lesson="quantum-03" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">03</span>
          <span class="lesson-title">
            بوابات الكيوبت الواحد: H, X, Z
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            البوابة الكمية تمثل تحويلًا رياضيًا لحالة الكيوبت.
            وفي تمثيل المصفوفات، تطبق البوابة على متجه الحالة
            باستخدام ضرب المصفوفة في المتجه.
          </p>


          <!-- H -->
          <h5>Hadamard (H)</h5>

          <div class="code-box math">
H =
1/√2
[  1   1 ]
[  1  -1 ]
          </div>


          <h5>تأثير H على حالات الأساس</h5>

          <div class="code-box math">
H|0⟩ = (|0⟩ + |1⟩)/√2

H|1⟩ = (|0⟩ - |1⟩)/√2
          </div>


          <p>
            عند تطبيق H على <code>|0⟩</code>
            نحصل على تراكب متساوي،
            وبالتالي يكون احتمال كل من
            <code>0</code> و<code>1</code>
            عند القياس مساويًا لـ <code>50%</code>.
          </p>


          <!-- X -->
          <h5>Pauli-X — النظير الكمي لـ NOT</h5>

          <div class="code-box math">
X =
[ 0   1 ]
[ 1   0 ]
          </div>


          <div class="code-box math">
X|0⟩ = |1⟩

X|1⟩ = |0⟩
          </div>


          <!-- Z -->
          <h5>Pauli-Z</h5>

          <div class="code-box math">
Z =
[ 1   0 ]
[ 0  -1 ]
          </div>


          <div class="code-box math">
Z|0⟩ = |0⟩

Z|1⟩ = -|1⟩
          </div>


          <p>
            لا تبدّل بوابة Pauli-Z بين
            <code>|0⟩</code> و<code>|1⟩</code>،
            وإنما تغيّر إشارة سعة الحالة
            <code>|1⟩</code>، أي تغيّر طورها.
          </p>


          <h5>Qiskit</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
qc.h(0)
qc.x(0)
qc.z(0)
          </div>


          <h5>مثال — ربط المعادلة بالكود</h5>

          <div class="code-box math">
X|0⟩ = |1⟩
          </div>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
X = np.array([
    [0, 1],
    [1, 0]
])

zero = np.array([
    [1],
    [0]
])

one = X @ zero
          </div>


          <div class="code-box math">
H|0⟩ = (|0⟩ + |1⟩)/√2
          </div>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
H = (1 / np.sqrt(2)) * np.array([
    [1,  1],
    [1, -1]
])

plus = H @ zero
          </div>

        </div>
      </details>


      <!-- Quantum 04 -->
      <details class="lesson" data-lesson="quantum-04" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">04</span>
          <span class="lesson-title">
            بوابة الدوران RY(θ)
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            تسمح بوابة <code>RY</code>
            بالتحكم المستمر في الحالة
            باستخدام زاوية دوران.
          </p>


          <h5>المعادلة</h5>

          <div class="code-box math">
RY(θ) =
[ cos(θ/2)   -sin(θ/2) ]
[ sin(θ/2)    cos(θ/2) ]
          </div>


          <h5>تطبيقها على |0⟩</h5>

          <div class="code-box math">
RY(θ)|0⟩
=
[ cos(θ/2) ]
[ sin(θ/2) ]
          </div>


          <h5>الاحتمالات الناتجة</h5>

          <div class="code-box math">
P(0) = cos²(θ/2)

P(1) = sin²(θ/2)
          </div>


          <h5>Qiskit</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
qc.ry(angle, 0)
          </div>


          <div class="callout warn">

            <strong>ملاحظة مهمة حول الزاوية:</strong>

            إذا كانت الحالة المطلوبة هي:

            <div class="code-box math">
|ψ⟩ = cos(φ)|0⟩ + sin(φ)|1⟩
            </div>

            فإن بوابة <code>RY</code>
            تحتاج إلى الزاوية:

            <div class="code-box math">
θ = 2φ
            </div>

          </div>


          <h5>مثال — احتمال 75%</h5>

          <p>
            نريد الحالة:
          </p>

          <div class="code-box math">
|ψ⟩
=
cos(π/3)|0⟩
+
sin(π/3)|1⟩
          </div>


          <div class="code-box math">
P(0)
=
cos²(π/3)
=
1/4
=
0.25

P(1)
=
sin²(π/3)
=
3/4
=
0.75
          </div>


          <h5>Qiskit</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from math import pi
from qiskit import QuantumCircuit

phi = pi / 3

qc = QuantumCircuit(1, 1)

qc.ry(2 * phi, 0)

qc.measure(0, 0)
          </div>

        </div>
      </details>


      <!-- Quantum 05 -->
      <details class="lesson" data-lesson="quantum-05" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">05</span>
          <span class="lesson-title">
            المؤثرات الوحدوية (Unitary)
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            في التطور الكمي لنظام مغلق،
            تمثل البوابات الكمية بتحويلات وحدوية
            تحافظ على معيار متجه الحالة.
          </p>


          <h5>المعادلة</h5>

          <div class="code-box math">
U†U = I
          </div>


          <p>
            حيث:
          </p>

          <ul>

            <li>
              <code>U</code>
              هي المصفوفة الوحدوية.
            </li>

            <li>
              <code>U†</code>
              هو المرافق المنقول (Conjugate Transpose).
            </li>

            <li>
              <code>I</code>
              هي مصفوفة الوحدة.
            </li>

          </ul>


          <h5>عندما تكون المصفوفة حقيقية</h5>

          <div class="code-box math">
UᵀU = I
          </div>


          <p>
            يضمن هذا الشرط الحفاظ على Norm متجه الحالة،
            وبالتالي يبقى شرط التطبيع محفوظًا بعد تطبيق البوابة.
          </p>


          <div class="callout">
            <strong>فكرة للحفظ:</strong>
            في النظام الكلاسيكي توجد دوال غير قابلة للعكس،
            مثل الدوال الثابتة ZERO وONE.
            أما البوابات المستخدمة في التطور الكمي المغلق
            فتمثل بتحويلات Unitary قابلة للعكس.
          </div>

        </div>
      </details>


      <!-- Quantum 06 -->
      <details class="lesson" data-lesson="quantum-06" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">06</span>
          <span class="lesson-title">
            القياس (Measurement) والـ Shots
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            قبل القياس يمكن أن تكون حالة الكيوبت في تراكب.
            عند القياس نحصل على نتيجة كلاسيكية واحدة.
            وبإعادة تشغيل الدائرة عدة مرات،
            أو ما يسمى <strong>Shots</strong>،
            يمكن تقدير توزيع النتائج تجريبيًا.
          </p>


          <h5>مثال Qiskit</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator

qc = QuantumCircuit(1, 1)

qc.h(0)
qc.measure(0, 0)

simulator = AerSimulator()

job = simulator.run(
    qc,
    shots=1000
)

counts = job.result().get_counts()

print(counts)
# مثال:
# {'0': 503, '1': 497}
          </div>


          <div class="callout">
            الأعداد الناتجة ليست ثابتة لأن القياس احتمالي.
            قد تختلف النتائج من تشغيل إلى آخر،
            مع بقاء التوزيع قريبًا من التوقع النظري.
          </div>

        </div>
      </details>


      <!-- Quantum 07 -->
      <details class="lesson" data-lesson="quantum-07" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">07</span>
          <span class="lesson-title">
            الأنظمة متعددة الكيوبتات والجداء التنسوري
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            كما استخدمنا الجداء التنسوري لبناء نظام مركب
            في الأنظمة الاحتمالية،
            نستخدمه في الحوسبة الكمية لبناء حالة نظام
            مكوّن من عدة كيوبتات.
          </p>


          <p>
            كيوبتان يمتلكان أربع حالات أساس:
          </p>

          <div class="code-box math">
|00⟩
|01⟩
|10⟩
|11⟩
          </div>


          <p>
            وبشكل عام، يحتوي نظام من <code>n</code> كيوبتات
            على فضاء حالة ذي بُعد:
          </p>

          <div class="code-box math">
Dimension = 2ⁿ
          </div>


          <h5>المعادلة</h5>

          <div class="code-box math">
|ψ⟩ = α|0⟩ + β|1⟩

|φ⟩ = γ|0⟩ + δ|1⟩
          </div>


          <div class="code-box math">
|ψ⟩ ⊗ |φ⟩

=

αγ|00⟩
+
αδ|01⟩
+
βγ|10⟩
+
βδ|11⟩
          </div>


          <h5>Python</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
psi_phi = np.kron(psi, phi)
          </div>


          <div class="callout">
            <strong>تنبيه:</strong>
            هذا التمثيل بالجداء التنسوري صالح فقط عندما تكون
            حالة النظام المركب <strong>قابلة للفصل</strong>
            (Separable/Product State)، أي يمكن كتابتها كحاصل
            ضرب حالتي كيوبت منفردتين. في الحالة العامة، وخصوصًا
            عند وجود تشابك كمي، لا يمكن كتابة الحالة على هذا
            الشكل — وهو ما سنراه لاحقًا في حالة Bell.
            كذلك انتبه إلى أن ترتيب عناصر متجه الحالة يعتمد على
            اتفاقية ترتيب الحالات، وفي Qiskit يجب الانتباه أيضًا
            إلى ترتيب البتات عند قراءة نتائج القياس.
          </div>

        </div>
      </details>


      <!-- Quantum 08 -->
      <details class="lesson" data-lesson="quantum-08" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">08</span>
          <span class="lesson-title">
            بوابة CNOT وحالة Bell
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            CNOT هي بوابة ثنائية الكيوبت.
            تحتوي على كيوبت تحكم وكيوبت هدف.
            إذا كانت حالة كيوبت التحكم تساوي <code>1</code>،
            تُطبّق عملية X على كيوبت الهدف.
          </p>


          <h5>تأثير CNOT على حالات الأساس</h5>

          <div class="code-box math">
|00⟩ → |00⟩

|01⟩ → |01⟩

|10⟩ → |11⟩

|11⟩ → |10⟩
          </div>


          <h5>بناء حالة Bell</h5>

          <p>
            نبدأ بالحالة:
          </p>

          <div class="code-box math">
|00⟩
          </div>

          <p>
            ثم نطبّق H على كيوبت التحكم،
            وبعدها CNOT.
          </p>


          <div class="code-box math">
|00⟩

→ H على الكيوبت الأول

→ (|00⟩ + |10⟩)/√2

→ CNOT

→ (|00⟩ + |11⟩)/√2
          </div>


          <h5>حالة Bell الناتجة</h5>

          <div class="code-box math">
|Φ⁺⟩ = (|00⟩ + |11⟩)/√2
          </div>


          <h5>Qiskit</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit

qc = QuantumCircuit(2, 2)

qc.h(0)
qc.cx(0, 1)

qc.measure([0, 1], [0, 1])
          </div>


          <div class="callout">
            في حالة Bell المثالية،
            تكون نتائج القياس الممكنة
            <code>00</code> و<code>11</code>،
            مع احتمال يقارب <code>50%</code> لكل منهما.
          </div>

        </div>
      </details>


      <!-- Quantum 09 -->
      <details class="lesson" data-lesson="quantum-09" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">09</span>
          <span class="lesson-title">
            التشابك الكمي (Entanglement)
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <p>
            يكون نظام كمي مركب في حالة متشابكة
            عندما لا يمكن تمثيل حالته كجداء تنسوري
            لحالتين مستقلتين.
          </p>


          <h5>المعادلة</h5>

          <div class="code-box math">
|ψ_AB⟩ ≠ |ψ_A⟩ ⊗ |ψ_B⟩
          </div>


          <p>
            حالة Bell:
          </p>

          <div class="code-box math">
|Φ⁺⟩ = (|00⟩ + |11⟩)/√2
          </div>


          <p>
            مثال على حالة Bell المتشابكة:
            عند القياس في الأساس الحسابي،
            تظهر النتيجتان <code>00</code> أو <code>11</code>
            في الحالة المثالية.
          </p>


          <div class="callout warn">

            <strong>تنبيه:</strong>

            التشابك الكمي لا يعني إمكانية إرسال
            معلومات كلاسيكية أسرع من الضوء.
            الترابط بين النتائج لا يوفر وحده قناة
            لإرسال رسالة فورية.

          </div>

        </div>
      </details>


      <!-- Quantum 10 -->
      <details class="lesson" data-lesson="quantum-10" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">10</span>
          <span class="lesson-title">
            بوابة Toffoli وترتيب البتات (Little-Endian)
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <h5>Toffoli (CCNOT)</h5>

          <p>
            بوابة Toffoli تستخدم كيوبتي تحكم
            وكيوبتًا هدفًا.
            تقلب حالة الكيوبت الهدف فقط عندما يكون
            كيوبتا التحكم كلاهما في الحالة <code>1</code>.
          </p>


          <h5>Qiskit</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
qc.ccx(control1, control2, target)
          </div>


          <h5>ترتيب البتات في Qiskit</h5>

          <p>
            تستخدم Qiskit اتفاقية
            <strong>Little-Endian</strong>
            في عرض نتائج القياس،
            ولذلك يظهر <code>q0</code>
            عادةً في أقصى يمين سلسلة النتائج.
          </p>


          <div class="callout warn">

            <strong>تنبيه مهم:</strong>

            عند مقارنة متجهات الحالة النظرية
            بمفاتيح <code>counts</code>،
            يجب الانتباه إلى ترتيب البتات.
            لا تفترض أن ترتيب سلسلة القياس
            يطابق ترتيب أسماء الكيوبتات من اليسار إلى اليمين.

          </div>

        </div>
      </details>

    </div>


    <div class="stage-transition reveal">
      <p>
        أصبحت الآن تملك الأساس اللازم لتمثيل الحالات الكمية
        والبوابات والتشابك. في القسم التالي سننتقل من هذه
        الأدوات إلى استخدامها في بناء خوارزميات كمومية كاملة،
        بدءًا من فكرة التداخل الكمومي وصولًا إلى خوارزمية شور.
      </p>
    </div>

  </div>
</section>


<!-- =========================================================
     STAGE 5 — QSILVER — الخوارزميات الكمومية المتقدمة
========================================================= -->

<section id="qsilver" class="stage-section">

  <div class="container">

    <div class="stage-header reveal">
      <span class="stage-badge">القسم 5 · مستوى متقدم</span>
      <h2>الخوارزميات الكمومية</h2>
      <p>
        الانتقال من أساسيات الأنظمة الكمومية إلى فهم الخوارزميات
        الكمومية التي تعتمد على التداخل، وتحويل فورييه الكمومي،
        وتقدير الطور، وصولًا إلى خوارزمية شور.
      </p>
    </div>


    <div class="lesson-list reveal" id="listQsilver">

      <!-- ===============================================
           DAY 1
      ================================================ -->

      <details class="lesson" data-lesson="qsilver-01" open>

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">01</span>
          <span class="lesson-title">
            اليوم الأول — التداخل والحوسبة الهجينة
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف اليوم:</strong>
            الانتقال من مفهوم الكيوبت والبوابات (الذي تمت
            تغطيته في قسم الأنظمة الكمية) إلى فكرة التداخل
            الكمومي ومكان الحوسبة الكمومية اليوم ضمن نظرية
            التعقيد الحسابي.
          </div>


          <h5>مراجعة سريعة</h5>

          <p>
            سبق أن رأينا أن حالة الكيوبت تُمثَّل بمتجه مركّب
            <code>|ψ⟩ = α|0⟩ + β|1⟩</code>
            يحقق شرط التطبيع
            <code>|α|² + |β|² = 1</code>،
            وأن البوابات الكمومية تمثَّل بمؤثرات وحدوية تحقق
            <code>U†U = I</code>.
            في هذا القسم سنستخدم هذا التمثيل لفهم كيف يمكن
            للتداخل بين السعات أن يُنتج خوارزميات أسرع من
            نظيرتها الكلاسيكية.
          </p>


          <h4>أين تقف الحوسبة الكمومية اليوم؟</h4>

          <p>
            الحوسبة الكمومية هي نموذج حوسبة يعتمد على مبادئ
            ميكانيكا الكم، ويستخدم حالات كمومية لتنفيذ عمليات
            حسابية بطريقة تختلف جذريًا عن الحوسبة الكلاسيكية.
          </p>

          <p>
            وعلى الرغم من التطور السريع في العتاد الكمومي
            والبرمجيات الكمومية، فإن الحواسيب الكمومية الحالية
            ما زالت محدودة بسبب الضوضاء، وفقدان الترابط،
            ومحدودية عدد الكيوبتات عالية الجودة.
          </p>


          <h4>لماذا تأتي الميزة الكمومية من التداخل؟</h4>

          <p>
            لا يكفي أن يمتلك النظام الكمومي عددًا كبيرًا من
            الحالات الممكنة. الفكرة الأساسية في العديد من
            الخوارزميات الكمومية هي التحكم في
            <strong>السعات</strong> بحيث تتداخل بعض المسارات
            بشكل بنّاء (تزيد احتمال النتيجة الصحيحة)، بينما
            يحدث تداخل هدّام للمسارات غير المرغوبة (يُلغي
            احتمالها تقريبًا).
          </p>


          <h4>من P وNP إلى BQP</h4>

          <p>
            في نظرية التعقيد الحسابي، تُستخدم الفئات الحسابية
            لوصف أنواع المسائل التي يمكن حلها بكفاءة باستخدام
            نماذج مختلفة من الحوسبة.
          </p>

          <table class="mini-table">
            <thead>
              <tr>
                <th>الفئة</th>
                <th>التعريف</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>P</code></td>
                <td>
                  مسائل يمكن حلها بكفاءة باستخدام خوارزمية
                  حتمية على حاسوب كلاسيكي.
                </td>
              </tr>
              <tr>
                <td><code>NP</code></td>
                <td>
                  مسائل يمكن التحقق من صحة حلها بكفاءة، حتى لو
                  لم يكن معروفًا وجود خوارزمية كلاسيكية فعالة
                  لحلها.
                </td>
              </tr>
              <tr>
                <td><code>BQP</code></td>
                <td>
                  مسائل يمكن لحاسوب كمومي حلها بكفاءة باحتمال
                  خطأ محدود.
                </td>
              </tr>
            </tbody>
          </table>


          <h4>حوسبة NISQ والنموذج الهجين</h4>

          <p>
            يشير مصطلح
            <strong>NISQ — Noisy Intermediate-Scale Quantum</strong>
            إلى الجيل الحالي من الأجهزة الكمومية التي تمتلك
            عددًا متوسطًا من الكيوبتات لكنها ما زالت متأثرة
            بالضوضاء والأخطاء. لذلك تعتمد العديد من التطبيقات
            الحالية على خوارزميات هجينة تجمع بين الحاسوب
            الكلاسيكي والمعالج الكمومي، حيث ينفذ الحاسوب
            الكلاسيكي عمليات التحسين والتحكم، بينما ينفذ
            المعالج الكمومي الجزء الكمومي من الحساب.
          </p>


          <h5>Qiskit — تذكير سريع</h5>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit

qc = QuantumCircuit(1, 1)

qc.h(0)
qc.measure(0, 0)
          </div>

        </div>
      </details>


      <!-- ===============================================
           DAY 2
      ================================================ -->

      <details class="lesson" data-lesson="qsilver-02">

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">02</span>
          <span class="lesson-title">
            اليوم الثاني — الطور، كرة بلوخ، وتحويل فورييه الكمومي
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف اليوم:</strong>
            فهم الطور الكمومي، وتمثيل الكيوبت على كرة بلوخ،
            ثم الانتقال من تحويل فورييه المتقطع الكلاسيكي إلى
            تحويل فورييه الكمومي (QFT).
          </div>


          <h4>الطور الكلي والطور النسبي</h4>

          <p>
            يمكن أن تحتوي الحالة الكمومية على عامل طور كلي
            لا يؤثر في نتائج القياس:
          </p>

          <div class="code-box math">
|ψ⟩          و          e^(iφ)|ψ⟩
          </div>

          <p>
            تمثل هاتان الحالتان الحالة الفيزيائية نفسها من
            ناحية نتائج القياس عندما يختلفان فقط بعامل طور
            كلي. أما الطور النسبي بين مكونات الحالة فيمكن أن
            يؤثر في التداخل وبالتالي في نتائج الخوارزمية
            الكمومية.
          </p>


          <h4>كرة بلوخ — Bloch Sphere</h4>

          <p>
            يمكن تمثيل أي حالة كيوبت واحد نقية هندسيًا باستخدام
            كرة بلوخ:
          </p>

          <div class="code-box math">
|ψ⟩ = cos(θ/2)|0⟩ + e^(iφ) sin(θ/2)|1⟩
          </div>

          <p>
            تحدد الزاوية θ موقع الحالة بالنسبة للمحور Z، بينما
            تحدد φ الطور النسبي حول المحور.
          </p>

          <div class="callout gold">
            <strong>مراجعة:</strong>
            هذا تعميم لبوابة <code>RY(θ)</code> التي رأيناها
            سابقًا (<code>RY(θ)|0⟩ = cos(θ/2)|0⟩ + sin(θ/2)|1⟩</code>)،
            مع إضافة الطور النسبي <code>e^(iφ)</code> على
            مركبة <code>|1⟩</code>.
          </div>


          <h4>الأنظمة متعددة الكيوبتات — مراجعة</h4>

          <p>
            عند الانتقال من كيوبت واحد إلى عدة كيوبتات، تُبنى
            الحالة العامة باستخدام الضرب التنسوري
            <code>|ψ⟩ = |ψ₁⟩ ⊗ |ψ₂⟩</code>
            في حالة الحالات القابلة للفصل، مع نمو أبعاد فضاء
            الحالة أُسّيًا مع عدد الكيوبتات.
          </p>


          <h4>تحويل فورييه المتقطع — DFT</h4>

          <p>
            تحويل فورييه يسمح بتمثيل الإشارة في مجال التردد
            بدلًا من المجال الأصلي. لتسلسل من N عينة
            <code>x₀, ..., x_(N-1)</code>، يُعرَّف تحويل فورييه
            المتقطع بالعينة رقم k كالتالي:
          </p>

          <div class="code-box math">
X_k = (1/√N) · Σ_(n=0)^(N-1) x_n · e^(-2πikn/N)
          </div>

          <p>
            حيث يمثّل <code>N</code> عدد العينات (ثابت)،
            و<code>n</code> متغير الجمع على العينات المدخلة،
            و<code>k</code> رقم مركبة التردد الناتجة.
          </p>


          <h4>تحويل فورييه الكمومي — QFT</h4>

          <p>
            تحويل فورييه الكمومي هو النظير الكمومي لتحويل
            فورييه المتقطع، ويعمل على سعات الحالة الكمومية
            بدل قيم إشارة كلاسيكية:
          </p>

          <div class="code-box math">
QFT|x⟩ = (1/√N) · Σ_(y=0)^(N-1) e^(2πixy/N) |y⟩
          </div>

          <p>
            حيث <code>N = 2ⁿ</code> لعدد <code>n</code> من
            الكيوبتات، و<code>x</code> هي الحالة المدخلة،
            و<code>y</code> متغير الجمع على حالات الأساس
            الناتجة. ويُعد QFT مكوّنًا أساسيًا في خوارزميات
            مهمة، من أبرزها تقدير الطور الكمومي وخوارزمية شور.
          </p>

          <div class="callout">
            <strong>الفكرة الأساسية لـ QFT:</strong>
            لا تكمن أهميته فقط في تحويل الحالة، بل في قدرته
            على تحويل معلومات مرتبطة بالطور إلى معلومات يمكن
            استخراجها من القياس المباشر.
          </div>

        </div>
      </details>


      <!-- ===============================================
           DAY 3
      ================================================ -->

      <details class="lesson" data-lesson="qsilver-03">

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">03</span>
          <span class="lesson-title">
            اليوم الثالث — تقدير الطور وإيجاد المرتبة
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف اليوم:</strong>
            فهم Quantum Phase Estimation باعتباره أحد أهم
            المكونات التي تعتمد عليها خوارزمية شور، ثم فهم
            مشكلة إيجاد المرتبة وعلاقتها بتحليل الأعداد.
          </div>


          <h4>القيم الذاتية والطور الكمومي</h4>

          <p>
            إذا كان <code>|ψ⟩</code> متجهًا ذاتيًا
            (Eigenvector) لمؤثر وحدوي <code>U</code>، فإن قيمته
            الذاتية (Eigenvalue) تكون عددًا مركبًا مقياسه واحد،
            ويمكن كتابتها بالشكل
            <code>e^(2πiφ)</code>. تطبيق U على هذا المتجه
            الذاتي يعطي:
          </p>

          <div class="code-box math">
U|ψ⟩ = e^(2πiφ) |ψ⟩
          </div>

          <p>
            تسمى <code>φ</code> بالطور أو الطور النسبي المرتبط
            بالقيمة الذاتية (Eigenphase)، وهي القيمة التي تسعى
            خوارزمية QPE لتقديرها.
          </p>


          <h4>تقدير الطور الكمومي — QPE</h4>

          <p>
            تهدف خوارزمية QPE إلى تقدير قيمة الطور
            <code>φ</code> المرتبطة بالقيمة الذاتية لمؤثر
            وحدوي. تعتمد الخوارزمية على ثلاثة مكونات أساسية:
          </p>

          <ul>
            <li>سجل كيوبتات للتحكم، يبدأ في حالة تراكب.</li>
            <li>
              تطبيق متحكَّم به لقوى متتالية من المؤثر
              <code>U</code> (Controlled-U).
            </li>
            <li>تحويل فورييه الكمومي العكسي (Inverse QFT).</li>
          </ul>

          <div class="code-box math">
|0⟩ → Superposition → Controlled-U → Phase Information → Inverse QFT → Measurement
          </div>

          <p>
            يتم بذلك تحويل معلومات الطور — التي كانت مخزَّنة في
            طور السعات الكمومية ولا يمكن قراءتها مباشرة من
            القياس — إلى تمثيل ثنائي يمكن قراءته من خلال
            القياس.
          </p>

          <p>
            تظهر QPE كمكوّن أساسي أو فرعي في عدد من التطبيقات
            والخوارزميات الكمومية، ومنها خوارزمية شور وبعض
            تطبيقات المحاكاة والكيمياء الكمومية.
          </p>


          <h4>إيجاد المرتبة — Order Finding</h4>

          <p>
            تعتمد مشكلة إيجاد المرتبة على إيجاد أصغر عدد صحيح
            موجب <code>r</code> يحقق:
          </p>

          <div class="code-box math">
a^r ≡ 1 (mod N)
          </div>

          <p>
            حيث يكون <code>a</code> عددًا صحيحًا لا يشترك مع
            <code>N</code> في أي عامل مشترك غير الواحد
            (أي <code>gcd(a, N) = 1</code>).
          </p>

          <h5>مثال بسيط</h5>

          <div class="code-box math">
a = 2 ,  N = 15

2¹ ≡ 2  (mod 15)
2² ≡ 4  (mod 15)
2³ ≡ 8  (mod 15)
2⁴ ≡ 1  (mod 15)

r = 4
          </div>


          <h4>العلاقة بين Order Finding وRSA</h4>

          <p>
            تعتمد خوارزمية شور على تحويل مشكلة تحليل الأعداد
            إلى مشكلة إيجاد المرتبة. هذه الخطوة هي جوهر
            التسارع الكمومي في خوارزمية شور؛ إذ يتم استخدام
            البنية الدورية للمشكلة بدل البحث الكلاسيكي المباشر
            عن عوامل العدد — وهذا الترابط بالتحديد هو ما يجعل
            إيجاد المرتبة كمّيًا وثيق الصلة بأمن نظام RSA.
          </p>

          <div class="code-box math">
Modular Exponentiation
↓
Periodic Structure
↓
Quantum Phase Estimation
↓
Inverse QFT
↓
Classical Post-Processing
↓
Order r
          </div>

        </div>
      </details>


      <!-- ===============================================
           DAY 4
      ================================================ -->

      <details class="lesson" data-lesson="qsilver-04">

        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">04</span>
          <span class="lesson-title">
            اليوم الرابع — خوارزمية شور وإغلاق الحلقة
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف اليوم:</strong>
            جمع المفاهيم السابقة في خوارزمية كمومية متكاملة
            لفهم خوارزمية شور وآلية استخدامها لإيجاد عوامل عدد
            صحيح.
          </div>


          <h4>ما المشكلة التي تحلها خوارزمية شور؟</h4>

          <p>
            تهدف خوارزمية شور إلى تحليل عدد صحيح كبير
            <code>N</code> إلى عوامله الأولية بكفاءة كمومية.
            تكمن أهمية الخوارزمية في أن التحليل إلى العوامل
            الأولية يرتبط بأمن بعض أنظمة التشفير الكلاسيكية،
            ومنها RSA.
          </p>


          <h4>الفكرة الأساسية لخوارزمية شور</h4>

          <p>
            بدل محاولة إيجاد العامل مباشرة، تحوّل خوارزمية شور
            المشكلة إلى مشكلة إيجاد دور الدالة:
          </p>

          <div class="code-box math">
f(x) = a^x mod N
          </div>

          <p>
            ثم تُستخدم الحوسبة الكمومية (عبر QPE وQFT العكسي)
            لاستخراج البنية الدورية لهذه الدالة.
          </p>

          <ul class="step-flow">
            <li>اختيار العدد المراد تحليله N</li>
            <li>اختيار عدد صحيح a يحقق gcd(a, N) = 1</li>
            <li>إيجاد المرتبة r باستخدام الأدوات الكمومية</li>
            <li>التحقق من كون r عددًا زوجيًا</li>
            <li>حساب a^(r/2)</li>
            <li>استخراج العوامل عبر GCD</li>
          </ul>


          <h4>مثال تعليمي — تحليل 15</h4>

          <p>
            نريد تحليل <code>N = 15</code>، ونختار
            <code>a = 2</code>. من الدرس السابق نعلم أن
            المرتبة هي <code>r = 4</code> (زوجية، وهذا مطلوب
            لتكملة الخوارزمية).
          </p>

          <div class="code-box math">
a^(r/2) = 2² = 4

gcd(4 − 1, 15) = gcd(3, 15) = 3

gcd(4 + 1, 15) = gcd(5, 15) = 5
          </div>

          <div class="callout success">
            تمكنّا من الحصول على العاملين:
            <strong>3 × 5 = 15</strong>
          </div>


          <h4>أين توجد الحوسبة الكمومية بالضبط؟</h4>

          <p>
            من المهم التمييز بين الجزء الكمومي والجزء
            الكلاسيكي في خوارزمية شور:
          </p>

          <ul>
            <li>
              الحاسوب الكمومي يساعد في استخراج المعلومة
              الدورية (إيجاد المرتبة) عبر QPE وQFT العكسي.
            </li>
            <li>
              تتم معالجة النتائج واستخراج العوامل النهائية
              باستخدام خطوات كلاسيكية (حساب GCD).
            </li>
          </ul>


          <h4>من QPrep إلى QBronze ثم إلى الخوارزميات الكمومية</h4>

          <ul class="step-flow">
            <li>Python + الجبر الخطي (الأساس البرمجي والرياضي)</li>
            <li>الكيوبتات والبوابات والدوائر والتشابك (الأساس الكمومي)</li>
            <li>QFT + QPE + Order Finding + خوارزمية شور</li>
          </ul>


          <h4>أين نقف اليوم؟</h4>

          <p>
            تمثل خوارزمية شور مثالًا مهمًا على القوة النظرية
            للحوسبة الكمومية، لكنها لا تعني أن أجهزة الحوسبة
            الكمومية الحالية قادرة على كسر أنظمة التشفير واسعة
            النطاق عمليًا. ما زالت هناك تحديات كبيرة مرتبطة
            بعدد الكيوبتات، ومعدلات الخطأ، وتصحيح الأخطاء
            الكمومية، وقابلية توسيع الأنظمة.
          </p>

          <p>
            تمثل أجهزة NISQ مرحلة انتقالية في تطور الحوسبة
            الكمومية، ويُعد الوصول إلى حواسيب كمومية متسامحة مع
            الأخطاء
            <strong>Fault-Tolerant Quantum Computers</strong>
            خطوة أساسية نحو تشغيل خوارزميات كمومية واسعة النطاق
            بصورة عملية.
          </p>


          <div class="callout">
            <strong>الفكرة المركزية لهذا القسم:</strong>
            لا تعتمد خوارزميات مثل شور على "التوازي الكمومي"
            وحده، وإنما تستفيد من القدرة على التحكم في التراكب
            والطور والتداخل لاستخراج البنية الرياضية المخفية
            داخل المشكلة.
          </div>

        </div>
      </details>

    </div>


    <!-- QSILVER SUMMARY -->
    <div class="stage-summary reveal">

      <h3>ماذا تتعلم في هذا القسم؟</h3>

      <div class="summary-grid">

        <div class="summary-card">
          <strong>01</strong>
          <span>التداخل وBQP</span>
          <p>التداخل الكمومي، وموقع BQP بين P وNP</p>
        </div>

        <div class="summary-card">
          <strong>02</strong>
          <span>Bloch Sphere</span>
          <p>الطور الكلي والنسبي، وتمثيل الكيوبت هندسيًا</p>
        </div>

        <div class="summary-card">
          <strong>03</strong>
          <span>QFT</span>
          <p>تحويل فورييه الكمومي وعلاقته بـ DFT</p>
        </div>

        <div class="summary-card">
          <strong>04</strong>
          <span>QPE</span>
          <p>تقدير الطور الكمومي والقيم الذاتية</p>
        </div>

        <div class="summary-card">
          <strong>05</strong>
          <span>Order Finding</span>
          <p>إيجاد المرتبة والبنية الدورية</p>
        </div>

        <div class="summary-card">
          <strong>06</strong>
          <span>Shor's Algorithm</span>
          <p>تطبيق المفاهيم السابقة في خوارزمية شور</p>
        </div>

      </div>

    </div>

  </div>
</section>


<!-- =========================================================
     QUICK REFERENCE
========================================================= -->
<section class="section" id="reference">

  <div class="container">

    <div class="section-head reveal">

      <span class="eyebrow purple">
        مرجع سريع
      </span>

      <h2>الرموز والبوابات في لمحة</h2>

      <p>
        للمراجعة السريعة قبل الاختبار أو أثناء كتابة الكود.
      </p>

    </div>


    <div class="ref-grid reveal">

      <div class="glass" style="padding:22px">

        <h3
          style="
            font-family:var(--font-display);
            font-size:16px;
            margin-bottom:12px;
            color:var(--cyan)
          "
        >
          جدول البوابات
        </h3>


        <table class="mini-table">

          <thead>
            <tr>
              <th>المفهوم</th>
              <th>الرمز</th>
              <th>Qiskit / Python</th>
            </tr>
          </thead>

          <tbody>

            <tr>
              <td>حالة الصفر</td>
              <td><code>|0⟩</code></td>
              <td><code>QuantumCircuit(1)</code></td>
            </tr>

            <tr>
              <td>Pauli-X</td>
              <td><code>X</code></td>
              <td><code>qc.x(0)</code></td>
            </tr>

            <tr>
              <td>Hadamard</td>
              <td><code>H</code></td>
              <td><code>qc.h(0)</code></td>
            </tr>

            <tr>
              <td>Pauli-Z</td>
              <td><code>Z</code></td>
              <td><code>qc.z(0)</code></td>
            </tr>

            <tr>
              <td>دوران Y</td>
              <td><code>RY(θ)</code></td>
              <td><code>qc.ry(theta, 0)</code></td>
            </tr>

            <tr>
              <td>CNOT</td>
              <td><code>CNOT</code></td>
              <td><code>qc.cx(c, t)</code></td>
            </tr>

            <tr>
              <td>Toffoli</td>
              <td><code>CCNOT</code></td>
              <td><code>qc.ccx(c1, c2, t)</code></td>
            </tr>

            <tr>
              <td>قياس</td>
              <td>Measurement</td>
              <td><code>qc.measure(q, c)</code></td>
            </tr>

            <tr>
              <td>ضرب مصفوفة</td>
              <td><code>Mv</code></td>
              <td><code>M @ v</code></td>
            </tr>

            <tr>
              <td>جداء تنسوري</td>
              <td><code>u⊗v</code></td>
              <td><code>np.kron(u, v)</code></td>
            </tr>

            <tr>
              <td>تحويل فورييه الكمومي</td>
              <td><code>QFT</code></td>
              <td><code>QFT(n)</code> (qiskit.circuit.library)</td>
            </tr>

            <tr>
              <td>إيجاد المرتبة</td>
              <td><code>a^r ≡ 1 (mod N)</code></td>
              <td>—</td>
            </tr>

          </tbody>

        </table>

      </div>


      <div class="glass" style="padding:22px">

        <h3
          style="
            font-family:var(--font-display);
            font-size:16px;
            margin-bottom:12px;
            color:var(--cyan)
          "
        >
          أهم القواعد للحفظ
        </h3>


        <ul
          style="
            padding-inline-start:18px;
            list-style:disc;
            color:var(--text-dim);
            font-size:14px;
            line-height:2
          "
        >

          <li>
            الاحتمال ليس هو السعة الكمية:
            <code>P = |amplitude|²</code>.
          </li>

          <li>
            السعات الكمية يمكن أن تكون حقيقية أو مركبة.
          </li>

          <li>
            شرط تطبيع الكيوبت:
            <code>|α|² + |β|² = 1</code>.
          </li>

          <li>
            زوايا Python وQiskit المثلثية بالراديان.
          </li>

          <li>
            الحالة
            <code>cos(φ)|0⟩ + sin(φ)|1⟩</code>
            تحتاج
            <code>RY(2φ)</code>.
          </li>

          <li>
            للمصفوفة الوحدوية:
            <code>U†U = I</code>.
          </li>

          <li>
            ضرب المصفوفات ليس تبادليًا عمومًا:
            <code>AB ≠ BA</code>.
          </li>

          <li>
            لـ <code>n</code> كيوبتات،
            بُعد فضاء الحالة هو
            <code>2ⁿ</code>.
          </li>

          <li>
            Qiskit تستخدم Little-Endian في عرض نتائج القياس.
          </li>

          <li>
            <code>U|ψ⟩ = e^(2πiφ)|ψ⟩</code> — الطور φ هو ما
            تقدّره خوارزمية QPE.
          </li>

          <li>
            خوارزمية شور تحوّل مشكلة التحليل إلى مشكلة إيجاد
            المرتبة <code>aʳ ≡ 1 (mod N)</code>.
          </li>

        </ul>

      </div>

    </div>
  </div>
</section>


<!-- =========================================================
     PROGRESS
========================================================= -->
<section class="section" id="progress-section">

  <div class="container">

    <div class="section-head reveal">

      <span class="eyebrow green">
        نظام التقدم
      </span>

      <h2>تقدّمك في الرحلة</h2>

      <p>
        يُحفظ تقدمك تلقائيًا،
        ويمكن تحديد الدروس المكتملة من داخل كل قسم.
      </p>

    </div>


    <div class="progress-panel glass reveal">

      <div class="progress-detail">

        <h3>ملخص الإنجاز</h3>

        <p id="progressSummaryText">
          عدد الدروس المكتملة من إجمالي 32 درسًا
          موزعة على 5 أقسام.
        </p>


        <div class="progress-rows">

          <div class="progress-row">

            <div class="row-top">
              <b>بايثون</b>
              <span id="rowPython">0 / 8</span>
            </div>

            <div class="path-progress-track">
              <div
                class="path-progress-fill"
                id="rowFillPython"
                style="width:0%"
              ></div>
            </div>

          </div>


          <div class="progress-row">

            <div class="row-top">
              <b>الجبر الخطي</b>
              <span id="rowLinalg">0 / 5</span>
            </div>

            <div class="path-progress-track">
              <div
                class="path-progress-fill"
                id="rowFillLinalg"
                style="width:0%"
              ></div>
            </div>

          </div>


          <div class="progress-row">

            <div class="row-top">
              <b>الأنظمة الاحتمالية</b>
              <span id="rowProb">0 / 5</span>
            </div>

            <div class="path-progress-track">
              <div
                class="path-progress-fill"
                id="rowFillProb"
                style="width:0%"
              ></div>
            </div>

          </div>


          <div class="progress-row">

            <div class="row-top">
              <b>الأنظمة الكمية</b>
              <span id="rowQuantum">0 / 10</span>
            </div>

            <div class="path-progress-track">
              <div
                class="path-progress-fill"
                id="rowFillQuantum"
                style="width:0%"
              ></div>
            </div>

          </div>


          <div class="progress-row">

            <div class="row-top">
              <b>الخوارزميات الكمومية</b>
              <span id="rowQsilver">0 / 4</span>
            </div>

            <div class="path-progress-track">
              <div
                class="path-progress-fill"
                id="rowFillQsilver"
                style="width:0%"
              ></div>
            </div>

          </div>

        </div>


        <div class="progress-actions">

          <a
            href="#python"
            class="btn btn-primary btn-sm"
          >
            متابعة الدروس
          </a>

          <button
            class="btn btn-ghost btn-sm"
            id="resetProgress"
          >
            إعادة تعيين التقدم
          </button>

        </div>

      </div>


      <div class="progress-ring-wrap">

        <svg
          width="210"
          height="210"
          viewBox="0 0 220 220"
          role="img"
          aria-label="نسبة التقدم الإجمالية"
        >

          <circle
            cx="110"
            cy="110"
            r="92"
            fill="none"
            stroke="rgba(255,255,255,0.06)"
            stroke-width="16"
          />

          <circle
            id="ringFill"
            cx="110"
            cy="110"
            r="92"
            fill="none"
            stroke="url(#ringGrad)"
            stroke-width="16"
            stroke-linecap="round"
            stroke-dasharray="578"
            stroke-dashoffset="578"
            transform="rotate(-90 110 110)"
            style="
              transition:
              stroke-dashoffset .7s var(--ease)
            "
          />

          <defs>

            <linearGradient
              id="ringGrad"
              x1="0%"
              y1="0%"
              x2="100%"
              y2="100%"
            >

              <stop
                offset="0%"
                stop-color="#2dd4ff"
              />

              <stop
                offset="55%"
                stop-color="#9b6bff"
              />

              <stop
                offset="100%"
                stop-color="#34e0a1"
              />

            </linearGradient>

          </defs>

        </svg>


        <div class="progress-ring-label">

          <b id="ringPct">0%</b>

          <span id="ringSub">
            0 من 32 درسًا
          </span>

        </div>

      </div>

    </div>
  </div>
</section>

</main>


<footer>
  <div class="container">
    <div class="footer-grid">
      <div class="brand"><span class="brand-mark" aria-hidden="true"></span><span>رحلة الحوسبة الكمية</span></div>
      <nav class="nav-links" aria-label="روابط الفوتر">
        <a href="#home">الرئيسية</a><a href="#python">بايثون</a><a href="#linalg">الجبر الخطي</a>
        <a href="#prob">الأنظمة الاحتمالية</a><a href="#quantum">الأنظمة الكمية</a><a href="#qsilver">الخوارزميات الكمومية</a>
      </nav>
    </div>
    <p class="footer-note">محتوى تعليمي مبني على منهج QWorld — QPrep &amp; QBronze &amp; QSilver. الدوائر الكمية هنا توضيحية بغرض التعلّم وليست محاكاة كمية حقيقية.</p>
  </div>
</footer>

<script>
(function(){
  "use strict";

  // ---------------------------------------------------------------
  // Small defensive helpers: nothing below should ever throw and
  // stop the rest of the script from running. Every DOM lookup is
  // guarded, and every optional browser API (IntersectionObserver,
  // window.storage, clipboard) is feature-detected before use.
  // ---------------------------------------------------------------
  function $(id){ return document.getElementById(id); }
  function on(el, evt, fn){ if(el) el.addEventListener(evt, fn); }

  try {
    var navToggle = $('navToggle');
    var mobileMenu = $('mobileMenu');
    on(navToggle, 'click', function(){
      if(!mobileMenu) return;
      var isOpen = mobileMenu.classList.toggle('open');
      navToggle.classList.toggle('open', isOpen);
      navToggle.setAttribute('aria-expanded', isOpen ? 'true' : 'false');
      if(isOpen){
        mobileMenu.removeAttribute('inert');
        mobileMenu.querySelectorAll('a').forEach(function(a){ a.removeAttribute('tabindex'); });
      } else {
        mobileMenu.setAttribute('inert','');
        mobileMenu.querySelectorAll('a').forEach(function(a){ a.setAttribute('tabindex','-1'); });
      }
    });
    document.querySelectorAll('.mobile-menu a').forEach(function(a){
      a.addEventListener('click', function(){
        if(mobileMenu) mobileMenu.classList.remove('open');
        if(navToggle){ navToggle.classList.remove('open'); navToggle.setAttribute('aria-expanded','false'); }
        if(mobileMenu){
          mobileMenu.setAttribute('inert','');
          mobileMenu.querySelectorAll('a').forEach(function(x){ x.setAttribute('tabindex','-1'); });
        }
      });
    });
  } catch(e){ /* nav toggle is a UI nicety; never let it block the rest of the page */ }

  // ---- Scroll-spy navigation highlighting ----
  try {
    var navLinks = document.querySelectorAll('[data-nav]');
    var sectionIds = ['home','python','linalg','prob','quantum','qsilver','reference','notes'];
    var sections = sectionIds.map(function(id){ return document.getElementById(id); }).filter(Boolean);
    function setActive(id){
      navLinks.forEach(function(a){ a.classList.toggle('active', a.getAttribute('href') === '#' + id); });
    }
    if(typeof IntersectionObserver === 'function' && sections.length){
      var spyObserver = new IntersectionObserver(function(entries){
        entries.forEach(function(entry){ if(entry.isIntersecting){ setActive(entry.target.id); } });
      }, { rootMargin: '-45% 0px -50% 0px', threshold: 0 });
      sections.forEach(function(s){ spyObserver.observe(s); });
    }
    // Also react to direct hash navigation / clicks so #quantum works
    // even without IntersectionObserver support.
    function setActiveFromHash(){
      var id = (location.hash || '#home').slice(1);
      if(sectionIds.indexOf(id) !== -1) setActive(id);
    }
    window.addEventListener('hashchange', setActiveFromHash);
    setActiveFromHash();
  } catch(e){ /* nav highlighting is cosmetic only */ }

  // ---- Scroll progress bar ----
  try {
    var scrollBar = $('scrollBar');
    function updateScrollBar(){
      if(!scrollBar) return;
      var h = document.documentElement;
      var scrolled = (h.scrollTop) / (h.scrollHeight - h.clientHeight) * 100;
      scrollBar.style.width = (isFinite(scrolled) ? scrolled : 0) + '%';
    }
    document.addEventListener('scroll', updateScrollBar, { passive: true });
    updateScrollBar();
  } catch(e){ /* progress bar is cosmetic only */ }

  // ---- Reveal-on-scroll animation (progressive enhancement) ----
  // .reveal elements are opacity:1 by default in CSS, so this only
  // ever ADDS a subtle entrance animation class; it never controls
  // whether content is visible. If IntersectionObserver is missing
  // or throws, the elements simply stay as they already are: visible.
  try {
    if(typeof IntersectionObserver === 'function'){
      var revealObserver = new IntersectionObserver(function(entries){
        entries.forEach(function(entry){
          if(entry.isIntersecting){ entry.target.classList.add('is-visible'); revealObserver.unobserve(entry.target); }
        });
      }, { threshold: 0.12 });
      document.querySelectorAll('.reveal').forEach(function(el){ revealObserver.observe(el); });
    }
  } catch(e){ /* content already visible via CSS default; nothing to fix */ }

  // ---- Copy-to-clipboard for code boxes ----
  try {
    document.querySelectorAll('.code-box:not(.math)').forEach(function(box){
      var btn = box.querySelector('.code-copy');
      if(!btn) return;
      btn.addEventListener('click', function(e){
        e.preventDefault(); e.stopPropagation();
        var text = box.textContent.replace(btn.textContent, '').trim();
        if(navigator.clipboard && navigator.clipboard.writeText){
          navigator.clipboard.writeText(text).then(function(){
            var original = btn.textContent;
            btn.textContent = 'تم النسخ!'; btn.classList.add('copied');
            setTimeout(function(){ btn.textContent = original; btn.classList.remove('copied'); }, 1800);
          }).catch(function(){});
        }
      });
    });
  } catch(e){ /* copy buttons are a convenience only */ }

  // ---- Progress storage: Claude-artifact-safe (window.storage), with
  // an in-memory fallback for standalone use outside claude.ai ----
  var STORAGE_KEY = 'quantum_summary_progress_v3';
  var hasClaudeStorage = (typeof window.storage !== 'undefined');
  var memoryStore = null; // in-memory fallback, lost on reload outside Claude

  async function loadCompleted(){
    if(hasClaudeStorage){
      try{
        var res = await window.storage.get(STORAGE_KEY, false);
        return res && res.value ? JSON.parse(res.value) : [];
      }catch(e){ return []; }
    }
    return memoryStore ? memoryStore.slice() : [];
  }
  async function saveCompleted(list){
    if(hasClaudeStorage){
      try{ await window.storage.set(STORAGE_KEY, JSON.stringify(list), false); }catch(e){}
    } else {
      memoryStore = list.slice();
    }
  }

  var allLessons = Array.prototype.slice.call(document.querySelectorAll('.lesson[data-lesson]'))
      .map(function(el){ return el.getAttribute('data-lesson'); });
  var groups = {
    python:  allLessons.filter(function(id){ return id.indexOf('python-') === 0; }),
    linalg:  allLessons.filter(function(id){ return id.indexOf('linalg-') === 0; }),
    prob:    allLessons.filter(function(id){ return id.indexOf('prob-') === 0; }),
    quantum: allLessons.filter(function(id){ return id.indexOf('quantum-') === 0; }),
    qsilver: allLessons.filter(function(id){ return id.indexOf('qsilver-') === 0; })
  };
  var totalCount = allLessons.length;
  var totalSections = Object.keys(groups).length;
  var completed = [];

  // Keep the hero stat numbers and every "X / Y" label perfectly in
  // sync with the real number of .lesson[data-lesson] elements in the
  // DOM, instead of relying on hand-typed counts scattered across the
  // page (hero stats, timeline, progress rows, progress summary).
  try {
    var statSections = $('statSections');
    var statLessons = $('statLessons');
    if(statSections) statSections.textContent = String(totalSections);
    if(statLessons) statLessons.textContent = String(totalCount);
  } catch(e){}

  function isDone(id){ return completed.indexOf(id) !== -1; }
  async function toggleDone(id){
    var idx = completed.indexOf(id);
    if(idx === -1){ completed.push(id); } else { completed.splice(idx, 1); }
    await saveCompleted(completed);
    renderProgress();
  }
  function countDone(ids){ return ids.filter(isDone).length; }
  function pct(done, total){ return total ? Math.round((done/total)*100) : 0; }

  var GROUP_META = {
    python:  { fill:'fillPython',  pct:'pctPython',  status:'statusPython',  row:'rowPython',  rowFill:'rowFillPython' },
    linalg:  { fill:'fillLinalg',  pct:'pctLinalg',  status:'statusLinalg',  row:'rowLinalg',  rowFill:'rowFillLinalg' },
    prob:    { fill:'fillProb',    pct:'pctProb',    status:'statusProb',    row:'rowProb',    rowFill:'rowFillProb' },
    quantum: { fill:'fillQuantum', pct:'pctQuantum', status:'statusQuantum', row:'rowQuantum', rowFill:'rowFillQuantum' },
    qsilver: { fill:'fillQsilver', pct:'pctQsilver', status:'statusQsilver', row:'rowQsilver', rowFill:'rowFillQsilver' }
  };

  function renderProgress(){
    try {
      document.querySelectorAll('.lesson[data-lesson]').forEach(function(lesson){
        var id = lesson.getAttribute('data-lesson');
        var check = lesson.querySelector('[data-check]');
        if(!check) return;
        var done = isDone(id);
        check.classList.toggle('checked', done);
        check.setAttribute('aria-checked', done ? 'true' : 'false');
        check.innerHTML = done ? '✓' : '';
      });

      var dTotal = 0;
      Object.keys(groups).forEach(function(key){
        var ids = groups[key], meta = GROUP_META[key];
        var d = countDone(ids), t = ids.length, p = pct(d, t);
        dTotal += d;
        var fillEl = $(meta.fill);
        if(fillEl) fillEl.style.width = p + '%';
        var pctEl = $(meta.pct);
        if(pctEl) pctEl.textContent = p + '% مكتمل';
        var statusEl = $(meta.status);
        if(statusEl){
          statusEl.textContent = p === 0 ? 'لم تبدأ' : (p === 100 ? 'مكتملة' : 'قيد التقدم');
          statusEl.className = 'path-status' + (p === 100 ? ' done' : (p > 0 ? ' active' : ''));
        }
        var rowEl = $(meta.row);
        if(rowEl) rowEl.textContent = d + ' / ' + t;
        var rowFillEl = $(meta.rowFill);
        if(rowFillEl) rowFillEl.style.width = p + '%';
      });

      var overallPct = pct(dTotal, totalCount);
      var circumference = 578;
      var offset = circumference - (overallPct/100)*circumference;
      var ringFill = $('ringFill');
      if(ringFill) ringFill.style.strokeDashoffset = offset;
      var ringPct = $('ringPct');
      if(ringPct) ringPct.textContent = overallPct + '%';
      var ringSub = $('ringSub');
      if(ringSub) ringSub.textContent = dTotal + ' من ' + totalCount + ' درسًا';
      var summaryEl = $('progressSummaryText');
      if(summaryEl){
        summaryEl.textContent = 'عدد الدروس المكتملة من إجمالي ' + totalCount + ' درسًا موزعة على ' + totalSections + ' أقسام.';
      }
    } catch(e){ /* progress rendering must never take down the page */ }
  }

  try {
    document.querySelectorAll('.lesson[data-lesson] [data-check]').forEach(function(check){
      check.setAttribute('role','checkbox');
      check.setAttribute('aria-checked','false');
      check.setAttribute('tabindex','0');
      check.setAttribute('aria-label','وضع علامة مكتمل على هذا الدرس');
      check.addEventListener('click', function(e){
        e.preventDefault(); e.stopPropagation();
        var lesson = check.closest('.lesson');
        if(lesson) toggleDone(lesson.getAttribute('data-lesson'));
      });
      check.addEventListener('keydown', function(e){
        if(e.key === 'Enter' || e.key === ' '){
          e.preventDefault(); e.stopPropagation();
          check.click();
        }
      });
    });
  } catch(e){}

  on($('resetProgress'), 'click', async function(){
    completed = [];
    await saveCompleted(completed);
    renderProgress();
  });

  (async function init(){
    try {
      completed = await loadCompleted();
    } catch(e) {
      completed = [];
    }
    renderProgress();
  })();
})();
</script>
</body>
</html>

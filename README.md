<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>منهج الحوسبة الكمية — QPrep → QBronze → QSilver</title>
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
body{background:var(--bg);color:var(--text);font-family:var(--font-body);line-height:1.85;overflow-x:hidden;direction:rtl;-webkit-text-size-adjust:100%;text-size-adjust:100%}
a{color:inherit;text-decoration:none}
button{font:inherit;color:inherit;background:none;border:none;cursor:pointer;-webkit-tap-highlight-color:transparent}
a,button,[role="checkbox"]{-webkit-tap-highlight-color:transparent}
ul,ol{list-style:none}
code,pre{font-family:var(--font-mono)}
img,svg{max-width:100%;height:auto}
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
.reveal{opacity:1;transform:none;transition:opacity .7s var(--ease),transform .7s var(--ease)}
.reveal.is-visible{opacity:1;transform:none}
.glass{background:var(--glass);border:1px solid var(--glass-brd);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);border-radius:var(--radius-md)}

.btn{display:inline-flex;align-items:center;justify-content:center;gap:10px;padding:13px 26px;border-radius:999px;font-weight:700;font-size:15px;
  transition:transform .25s var(--ease),box-shadow .25s var(--ease),background .25s var(--ease),border-color .25s var(--ease);white-space:nowrap;min-height:44px}
.btn:focus-visible{outline:2px solid var(--cyan);outline-offset:3px}
.btn-primary{background:linear-gradient(90deg,var(--cyan),var(--purple));color:#051019;box-shadow:0 8px 30px -8px var(--cyan-glow)}
.btn-primary:hover{transform:translateY(-2px);box-shadow:0 14px 36px -8px var(--purple-glow)}
.btn-ghost{border:1px solid var(--border);color:var(--text);background:rgba(255,255,255,.02)}
.btn-ghost:hover{border-color:var(--cyan);color:var(--cyan);background:rgba(45,212,255,.06)}
.btn-sm{padding:9px 18px;font-size:13.5px;min-height:40px}

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
.nav-toggle{display:none;width:44px;height:44px;border-radius:10px;border:1px solid var(--border);align-items:center;justify-content:center;flex-direction:column;gap:5px}
.nav-toggle span{width:20px;height:2px;background:var(--text);border-radius:2px;transition:transform .25s,opacity .25s}
.nav-toggle.open span:nth-child(1){transform:translateY(7px) rotate(45deg)}
.nav-toggle.open span:nth-child(2){opacity:0}
.nav-toggle.open span:nth-child(3){transform:translateY(-7px) rotate(-45deg)}
.mobile-menu{display:none;position:fixed;top:66px;inset-inline:12px;z-index:499;border-radius:var(--radius-md);padding:10px;
  flex-direction:column;gap:4px;opacity:0;transform:translateY(-12px);pointer-events:none;transition:opacity .25s var(--ease),transform .25s var(--ease);
  max-height:calc(100vh - 82px);overflow-y:auto}
.mobile-menu.open{opacity:1;transform:none;pointer-events:auto}
.mobile-menu a{padding:13px 16px;border-radius:10px;font-weight:600;color:var(--text-dim);min-height:44px;display:flex;align-items:center}
.mobile-menu a.active,.mobile-menu a:hover{color:var(--cyan);background:rgba(45,212,255,.08)}
.scroll-progress{position:fixed;top:0;inset-inline:0;height:3px;z-index:600;background:transparent}
.scroll-progress-bar{height:100%;width:0%;background:linear-gradient(90deg,var(--cyan),var(--purple),var(--green));transition:width .1s linear}

.hero{min-height:92vh;min-height:92dvh;display:flex;align-items:center;padding-top:110px;padding-bottom:50px;position:relative;overflow:hidden}
.hero-grid{display:grid;grid-template-columns:1.05fr .95fr;gap:50px;align-items:center}
.hero-copy h1{font-family:var(--font-display);font-weight:900;font-size:clamp(32px,5vw,56px);line-height:1.2;letter-spacing:-.01em;margin-bottom:20px}
.hero-copy p.lead{font-size:17.5px;color:var(--text-dim);max-width:560px;margin-bottom:30px}
.hero-actions{display:flex;flex-wrap:wrap;gap:14px;margin-bottom:36px}
.hero-stats{display:flex;gap:28px;flex-wrap:wrap}
.hero-stat b{display:block;font-family:var(--font-display);font-size:25px;font-weight:800;
  background:linear-gradient(90deg,var(--cyan),var(--green));-webkit-background-clip:text;background-clip:text;color:transparent}
.hero-stat span{font-size:12.5px;color:var(--text-faint)}
.hero-visual{position:relative;min-width:0}
.circuit-card{padding:24px;position:relative}
.circuit-card .tag{font-family:var(--font-mono);font-size:12px;color:var(--text-faint);margin-bottom:14px;display:flex;justify-content:space-between;flex-wrap:wrap;gap:4px;direction:ltr}
.circuit-svg-wrap{direction:ltr}
@keyframes travel{0%{offset-distance:0%;opacity:0}8%{opacity:1}92%{opacity:1}100%{offset-distance:100%;opacity:0}}
.qubit-dot{offset-path:path("M20,70 L340,70");animation:travel 3.6s linear infinite}
@keyframes pulseGate{0%,100%{filter:drop-shadow(0 0 2px var(--cyan))}50%{filter:drop-shadow(0 0 10px var(--cyan))}}
.gate-pulse{animation:pulseGate 2.4s ease-in-out infinite}

.flow-strip{display:flex;align-items:center;gap:8px;flex-wrap:wrap;direction:ltr;padding:0}
.flow-node{font-family:var(--font-mono);font-size:12.5px;padding:8px 13px;border-radius:8px;background:var(--panel-2);border:1px solid var(--border);white-space:nowrap}
.flow-node.hi{color:var(--cyan);border-color:rgba(45,212,255,.4);background:rgba(45,212,255,.08);font-weight:700}
.flow-arrow{color:var(--text-faint);font-size:14px}

.timeline{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;position:relative}
.timeline::before{content:"";position:absolute;top:32px;inset-inline:6%;height:2px;
  background:linear-gradient(90deg,var(--cyan),var(--purple),var(--amber));opacity:.35;z-index:0}
.path-card{position:relative;z-index:1;padding:22px;display:flex;flex-direction:column;gap:11px;min-width:0;
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
.lesson summary{list-style:none;cursor:pointer;padding:16px 18px;display:flex;align-items:center;gap:13px;font-weight:700;font-size:15px;user-select:none;min-height:44px}
.lesson summary::-webkit-details-marker{display:none}
.lesson-check{width:26px;height:26px;border-radius:6px;border:1.5px solid var(--border);flex-shrink:0;
  display:flex;align-items:center;justify-content:center;color:transparent;font-size:12.5px;transition:background .2s,border-color .2s,color .2s}
.lesson-check.checked{background:linear-gradient(135deg,var(--green),var(--cyan));border-color:transparent;color:#04150f}
.lesson-index{font-family:var(--font-mono);color:var(--text-faint);font-size:12.5px;min-width:24px;direction:ltr}
.lesson-title{flex:1;min-width:0}
.lesson-caret{color:var(--text-faint);transition:transform .25s var(--ease);flex-shrink:0}
.lesson[open] .lesson-caret{transform:rotate(180deg);color:var(--cyan)}
.lesson-body{padding:0 18px 20px 18px;color:var(--text-dim);font-size:14.5px}
.lesson-body h4,.lesson-body h5{color:var(--text);font-family:var(--font-display);font-size:14.5px;margin:14px 0 6px}
.lesson-body p{margin-bottom:10px}
.lesson-body ul,.lesson-body ol{margin:0 0 10px 0;padding-inline-start:20px;list-style:disc}
.lesson-body li{margin-bottom:4px}
.lesson-body strong{color:var(--text)}
p code,li code,td code,.lesson-body code{direction:ltr;unicode-bidi:isolate;display:inline-block;background:rgba(45,212,255,.09);
  color:var(--cyan);padding:1px 7px;border-radius:5px;font-size:.92em;max-width:100%;overflow-wrap:break-word}

.code-box{direction:ltr;unicode-bidi:isolate;text-align:left;position:relative;background:#060910;border:1px solid var(--border-soft);
  border-radius:10px;padding:14px 44px 14px 16px;overflow-x:auto;-webkit-overflow-scrolling:touch;margin:10px 0;font-size:13px;color:#c9e6ff;border-inline-start:3px solid var(--cyan-dim);max-width:100%}
.code-box.math{border-inline-start-color:var(--purple-dim);color:#e4d7ff;font-family:var(--font-mono);padding-inline-end:16px;white-space:pre}
.code-copy{position:absolute;top:8px;right:8px;font-family:var(--font-body);font-size:11px;color:var(--text-faint);
  background:var(--panel-2);border:1px solid var(--border);border-radius:6px;padding:4px 9px;transition:color .2s,border-color .2s;min-height:28px}
.code-copy:hover{color:var(--cyan);border-color:var(--cyan)}
.code-copy.copied{color:var(--green);border-color:var(--green)}

.mini-table{width:100%;table-layout:fixed;border-collapse:collapse;margin:12px 0;font-size:13.5px}
.mini-table th,.mini-table td{border:1px solid var(--border);padding:9px 12px;text-align:right;overflow-wrap:anywhere;word-break:break-word}
.mini-table th{background:rgba(45,212,255,.06);color:var(--cyan);font-family:var(--font-display)}
.mini-table td code,.mini-table th code{direction:ltr;display:inline-block;white-space:normal;word-break:break-word;overflow-wrap:anywhere;max-width:100%}
.table-scroll{width:100%;overflow-x:auto;-webkit-overflow-scrolling:touch}

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
.progress-ring-wrap svg{width:100%;max-width:210px;height:auto}
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

/* QSilver (protected stage) reuses .section / .section-head / .eyebrow.amber directly — see the
   #qsilver section below. Do not add stage-specific rules for that section's own shell; only
   rules that are genuinely new for surrounding stages (QPrep/QBronze) belong here. */

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
.step-flow li::before{content:"›";position:absolute;inset-inline-start:0;color:var(--cyan);font-weight:800}

.project-meta{display:flex;flex-wrap:wrap;gap:8px;margin:8px 0 14px}
.project-tag{font-family:var(--font-mono);font-size:11.5px;padding:5px 11px;border-radius:999px;border:1px solid var(--border);color:var(--text-faint);background:rgba(255,255,255,.03)}

footer{padding:50px 0 30px;border-top:1px solid var(--border-soft)}
.footer-grid{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:20px;margin-bottom:20px}
.footer-links{display:flex;align-items:center;gap:4px;flex-wrap:wrap}
.footer-links a{padding:8px 13px;border-radius:999px;font-size:14px;font-weight:600;color:var(--text-dim);transition:color .2s,background .2s}
.footer-links a:hover{color:var(--text);background:rgba(255,255,255,.04)}
.footer-note{color:var(--text-faint);font-size:13px;text-align:center}

@media (max-width:980px){
  .hero-grid{grid-template-columns:1fr} .hero-visual{order:-1}
  .timeline{grid-template-columns:1fr} .timeline::before{display:none}
  .progress-panel{grid-template-columns:1fr;padding:28px}
}
@media (max-width:720px){
  .nav-links{display:none} .nav-toggle{display:flex} .mobile-menu{display:flex}
  .section{padding:64px 0} .hero{padding-top:96px;min-height:auto}
  .circuit-card{padding:16px}
  .container{padding-inline:18px}
  .hero-actions .btn{width:100%}
}
@media (max-width:480px){
  .hero-stats{gap:18px}
  .hero-stat b{font-size:21px}
  .section-head p{font-size:15px}
  .lesson summary{padding:14px}
  .lesson-body{padding:0 14px 16px 14px}
  .progress-panel{padding:20px}
  .mini-table{font-size:12.5px}
  .mini-table th,.mini-table td{padding:7px 8px}
}
@media (max-width:360px){
  .hero-copy h1{font-size:26px}
  .path-card{padding:16px}
  .code-box{font-size:12px;padding:12px 38px 12px 12px}
}
@media (hover:none){
  .path-card:hover{transform:none}
}
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
      <span> الحوسبة الكمية</span>
    </a>

    <nav class="nav-links" aria-label="روابط التنقل الرئيسية">
      <a href="#home" data-nav class="active">الرئيسية</a>
      <a href="#qprep" data-nav>QPrep</a>
      <a href="#qbronze" data-nav>QBronze</a>
      <a href="#qbronze-projects" data-nav>مشاريع QBronze</a>
      <a href="#qsilver" data-nav>QSilver</a>
      <a href="#reference" data-nav>مرجع سريع</a>
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
  <a href="#qprep" tabindex="-1">QPrep</a>
  <a href="#qbronze" tabindex="-1">QBronze</a>
  <a href="#qbronze-projects" tabindex="-1">مشاريع QBronze</a>
  <a href="#qsilver" tabindex="-1">QSilver</a>
  <a href="#reference" tabindex="-1">مرجع سريع</a>
</nav>

<main>
  
<section class="hero" id="home">
  <div class="container hero-grid">

    <div class="hero-copy">
      <span class="eyebrow">منهج متكامل · QPrep → QBronze → QSilver</span>

      <h1>
        من أول سطر بايثون إلى
        <span class="glow-text">الخوارزميات الكمومية</span>
      </h1>

      <p class="lead">
        رحلة تعليمية كاملة على ثلاث مراحل:
        <strong style="color:var(--text)">QPrep</strong>
        يؤسسك في بايثون والجبر الخطي من الصفر،
        <strong style="color:var(--text)">QBronze</strong>
        ينقلك من البت الكلاسيكي إلى الكيوبت والتشابك والبروتوكولات الكمية
        مع سبعة مشاريع تطبيقية كاملة، ثم
        <strong style="color:var(--text)">QSilver</strong>
        يأخذك إلى الطور، تحويل فورييه الكمومي (QFT) — تعقيده O(n^2) بوابات في الدائرة القياسية، ويُستخدم كعنصر فرعي في QPE وشور، وخوارزمية شور.
      </p>

      <div class="hero-actions">
        <a href="#qprep" class="btn btn-primary">ابدأ من QPrep</a>
        <a href="#qbronze" class="btn btn-ghost">انتقل إلى QBronze</a>
      </div>

      <div class="hero-stats">
        <div class="hero-stat">
          <b id="statSections">3</b>
          <span>مراحل رئيسية</span>
        </div>

        <div class="hero-stat">
          <b id="statLessons">48</b>
          <span>درسًا ومشروعًا</span>
        </div>

        <div class="hero-stat">
          <b>7</b>
          <span>مشاريع QBronze الأصلية</span>
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

            <line x1="20" y1="70" x2="340" y2="70" stroke="var(--border)" stroke-width="2" />

            <g class="gate-pulse">
              <rect x="20" y="50" width="52" height="40" rx="8" fill="#0e1530" stroke="var(--cyan)" stroke-width="1.4" />
              <text x="46" y="75" fill="#e9eefb" font-family="JetBrains Mono, monospace" font-size="16" text-anchor="middle">|0⟩</text>
            </g>

            <g class="gate-pulse" style="animation-delay:.4s">
              <rect x="150" y="45" width="54" height="50" rx="10" fill="rgba(45,212,255,0.12)" stroke="var(--cyan)" stroke-width="1.6" />
              <text x="177" y="76" fill="var(--cyan)" font-family="Tajawal, sans-serif" font-weight="800" font-size="20" text-anchor="middle">H</text>
            </g>

            <g class="gate-pulse" style="animation-delay:.8s">
              <rect x="284" y="45" width="56" height="50" rx="10" fill="rgba(155,107,255,0.12)" stroke="var(--purple)" stroke-width="1.6" />
              <path d="M296 80 a16 14 0 0 1 32 0" fill="none" stroke="var(--purple)" stroke-width="2" />
              <line x1="312" y1="80" x2="322" y2="62" stroke="var(--purple)" stroke-width="2" />
            </g>

            <circle r="6" fill="var(--green)" class="qubit-dot">
              <animateMotion dur="3.6s" repeatCount="indefinite" path="M20,70 L340,70" />
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


<section class="section" style="padding-top:0">
  <div class="container">

    <div class="stage-intro glass reveal">
      <span class="badge">i</span>
      <p>
        <strong>خريطة المنهج:</strong>
        <strong>QPrep</strong> (بايثون، Jupyter، أنواع البيانات، القوائم والقواميس،
        الحلقات، الشروط، الدوال، NumPy، والمصفوفات) ثم
        <strong>QBronze</strong> (البت الكلاسيكي، الأنظمة الاحتمالية، Qiskit، الكيوبت،
        التراكب، القياس، الدورانات، التصوير المقطعي، حالات Bell والتشابك،
        الترميز فائق الكثافة، الانتقال الآني، البوابات متعددة التحكم،
        رمي العملة الكمية بالفوتونات، وسبعة مشاريع تطبيقية كاملة)
        ثم <strong>QSilver</strong> (الطور، كرة بلوخ، QFT، QPE، إيجاد المرتبة (Order Finding) كجزء من خوارزمية شور، ثم الخوارزمية الكاملة مع المعالجة الكلاسيكية) —
        محفوظ كما هو دون أي تعديل.
      </p>
    </div>

    <div class="timeline">

      <div class="path-card glass reveal" data-color="cyan">
        <div class="path-num">1</div>
        <h3>QPrep</h3>
        <p>
          بايثون وJupyter من الصفر، أنواع البيانات، القوائم/الصفوف/القواميس،
          الحلقات والشروط والدوال، NumPy، والمصفوفات.
        </p>
        <span class="path-status active" id="statusQprep">لم تبدأ</span>
        <div class="path-progress-track"><div class="path-progress-fill" id="fillQprep" style="width:0%"></div></div>
        <span class="path-pct" id="pctQprep">0% مكتمل</span>
        <a href="#qprep" class="btn btn-primary btn-sm">ابدأ</a>
      </div>

      <div class="path-card glass reveal" data-color="purple">
        <div class="path-num">2</div>
        <h3>QBronze</h3>
        <p>
          من البت الكلاسيكي إلى الكيوبت، Qiskit، القياس، الدورانات، Bell،
          التشابك، الانتقال الآني، والمشاريع السبعة.
        </p>
        <span class="path-status" id="statusQbronze">لم تبدأ</span>
        <div class="path-progress-track"><div class="path-progress-fill" id="fillQbronze" style="width:0%"></div></div>
        <span class="path-pct" id="pctQbronze">0% مكتمل</span>
        <a href="#qbronze" class="btn btn-ghost btn-sm">ابدأ</a>
      </div>

      <div class="path-card glass reveal" data-color="amber">
        <div class="path-num">3</div>
        <h3>QSilver</h3>
        <p>
          الطور والتداخل، تحويل فورييه الكمومي (QFT) — تعقيده O(n^2) بوابات في الدائرة القياسية، ويُستخدم كعنصر فرعي في QPE وشور، تقدير الطور الكمومي (QPE) — يقدّر الطور φ لمؤثر وحدوي U حيث U|ψ⟩=e^(2πiφ)|ψ⟩، ومنه يمكن استنتاج القيمة الذاتية λ=e^(2πiφ)،
          إيجاد المرتبة (Order Finding) كجزء من خوارزمية شور، ثم الخوارزمية الكاملة مع المعالجة الكلاسيكية.
        </p>
        <span class="path-status" id="statusQsilver">لم تبدأ</span>
        <div class="path-progress-track"><div class="path-progress-fill" id="fillQsilver" style="width:0%"></div></div>
        <span class="path-pct" id="pctQsilver">0% مكتمل</span>
        <a href="#qsilver" class="btn btn-ghost btn-sm">ابدأ</a>
      </div>

    </div>

  </div>
</section>

<!-- =========================================================
     QPREP — القسم التحضيري الكامل
========================================================= -->
<section class="section" id="qprep">
  <div class="container">

    <div class="section-head reveal">
      <span class="eyebrow">المرحلة 1 · QPrep</span>
      <h2>الأساس البرمجي والرياضي</h2>
      <p>
        قبل أي حديث عن الكيوبت، تحتاج أدوات: بايثون لكتابة الكود،
        وJupyter لتشغيله، وبنى بيانات لتخزين النتائج، وNumPy والمصفوفات
        لتمثيل الحالات الكمية رياضيًا. هذا القسم يبنيها من الصفر.
      </p>
    </div>

    <div class="lesson-list reveal" id="listQprep">

      <!-- QPrep 01 : Python -->
      <details class="lesson" data-lesson="qprep-01" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">01</span>
          <span class="lesson-title">بايثون: لماذا هي لغة الحوسبة الكمية؟</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <h4>1. المقدمة</h4>
          <p>
            بايثون لغة برمجة عامة الغرض، سهلة القراءة، وتمتلك مكتبات علمية
            ضخمة (NumPy وMatplotlib وQiskit وغيرها)، وهذا ما يجعلها الخيار
            شبه الحصري في تعليم وتطبيق الحوسبة الكمية.
          </p>

          <h4>2. لماذا يهم؟</h4>
          <p>
            كل مفهوم كمي سنشرحه — متجه الحالة، البوابة، القياس — سيُترجم في
            النهاية إلى كود بايثون فعلي تشغّله وتراقب نتيجته. بدون إتقان
            الأساسيات هنا، سيصعب متابعة أي درس لاحق في QBronze أو QSilver.
          </p>

          <h4>3. أول برنامج</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
print("Hello Quantum World!")
          </div>
          <p>
            الدالة <code>print()</code> تعرض قيمة أو نصًا على الشاشة،
            وهي أول أداة ستستخدمها لمراقبة نتائج أي كود.
          </p>

          <h4>4. المتغيرات والتعليقات</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
qubits_count = 2      # متغير عددي
circuit_name = "Bell" # متغير نصي

# هذا سطر تعليق: لا يُنفَّذ، ويُستخدم للتوثيق فقط
print(qubits_count, circuit_name)
          </div>

          <h4>5. أخطاء المبتدئين الشائعة</h4>
          <ul>
            <li>نسيان علامات التنصيص حول النصوص: <code>name = Ali</code> خطأ، الصحيح <code>name = "Ali"</code>.</li>
            <li>الخلط بين حروف كبيرة وصغيرة في أسماء المتغيرات (بايثون حساسة لحالة الأحرف).</li>
            <li>عدم محاذاة المسافات البادئة (Indentation)، وهي جزء من بنية اللغة وليست تجميلًا فقط.</li>
          </ul>

          <div class="callout">
            <strong>تمرين:</strong>
            أنشئ متغيرًا باسمك، وآخر لعمرك، واطبعهما في جملة واحدة باستخدام
            <code>f"..."</code> (f-string).
          </div>

        </div>
      </details>

      <!-- QPrep 02 : Jupyter -->
      <details class="lesson" data-lesson="qprep-02" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">02</span>
          <span class="lesson-title">Jupyter Notebook: بيئة العمل التفاعلية</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <h4>ما هو Jupyter؟</h4>
          <p>
            دفتر تفاعلي يتكون من خلايا (Cells) يمكن تشغيلها بشكل منفصل،
            مع الاحتفاظ بالمتغيرات في الذاكرة بين الخلايا.
          </p>

          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>نوع الخلية</th><th>الاستخدام</th></tr></thead>
            <tbody>
              <tr><td>Code</td><td>كتابة وتشغيل كود بايثون فعلي</td></tr>
              <tr><td>Markdown</td><td>كتابة نصوص توثيقية ومعادلات ($e^{i\pi}$)</td></tr>
            </tbody>
          </table>
          </div>

          <h4>تشغيل الخلايا وترتيب التنفيذ</h4>
          <ul>
            <li><code>Shift + Enter</code>: تشغيل الخلية الحالية والانتقال للتالية.</li>
            <li>الرقم بين قوسين يسار الخلية <code>[3]</code> يشير لترتيب التنفيذ الفعلي، وليس ترتيب الخلايا في الصفحة.</li>
            <li>يمكن تشغيل خلية متأخرة قبل خلية سابقة — وهذا مصدر شائع للأخطاء المربكة.</li>
          </ul>

          <h4>Kernel وRestart Kernel</h4>
          <p>
            الـKernel هو العملية التي تنفذ الكود وتحتفظ بحالة المتغيرات.
            عند حدوث سلوك غريب (متغير قديم، تعريف متضارب)، استخدم
            <strong>Restart Kernel</strong> ثم أعد تشغيل كل الخلايا من الأعلى
            بالترتيب — هذه أول خطوة تشخيصية دائمًا.
          </p>

          <div class="callout warn">
            <strong>خطأ شائع:</strong>
            تعديل خلية في المنتصف وتشغيلها منفردة دون إعادة تشغيل ما بعدها،
            فتبقى النتائج المعروضة قديمة ولا تعكس الكود الحالي فعليًا.
          </div>

          <h4>تنظيم الدفتر</h4>
          <ul>
            <li>ابدأ بخلية Markdown تشرح هدف الدفتر.</li>
            <li>اجعل الاستيراد (imports) في أول خلية كود.</li>
            <li>قسّم الدفتر بعناوين Markdown (##) بين كل تجربة ومشروع.</li>
          </ul>

        </div>
      </details>

      <!-- QPrep 03 : Data Types -->
      <details class="lesson" data-lesson="qprep-03" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">03</span>
          <span class="lesson-title">أنواع البيانات الأساسية</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>النوع</th><th>في بايثون</th><th>مثال</th></tr></thead>
            <tbody>
              <tr><td>عدد صحيح</td><td><code>int</code></td><td><code>n = 5</code></td></tr>
              <tr><td>عدد عشري</td><td><code>float</code></td><td><code>p = 0.85</code></td></tr>
              <tr><td>نص</td><td><code>str</code></td><td><code>name = "Bell"</code></td></tr>
              <tr><td>منطقي</td><td><code>bool</code></td><td><code>flag = True</code></td></tr>
            </tbody>
          </table>
          </div>

          <h4>type() وتحويل الأنواع</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
x = 5
print(type(x))          # <class 'int'>

y = float(x)             # تحويل صريح إلى float
print(y, type(y))        # 5.0 <class 'float'>

z = str(x) + " qubits"   # تحويل إلى نص قبل الدمج
print(z)
          </div>

          <h4>العمليات بين الأنواع والأخطاء الشائعة</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
"5" + 3        # TypeError: لا يمكن جمع نص وعدد مباشرة
str(5) + "3"   # "53"  (دمج نصوص)
int("5") + 3   # 8     (تحويل ثم جمع)
          </div>

          <div class="callout warn">
            <strong>خطأ شائع جدًا:</strong>
            الدالة input() تُرجع دائمًا نصًا، وكثير من عمليات القراءة النصية تُرجع نصوصًا أيضًا
            <code>str</code>، حتى لو كانت "تبدو" رقمًا — يجب تحويلها صراحة.
          </div>

        </div>
      </details>

      <!-- QPrep 04 : Strings -->
      <details class="lesson" data-lesson="qprep-04" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">04</span>
          <span class="lesson-title">النصوص (Strings): الإنشاء، الفهرسة، والتقطيع</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <p>لكل حرف في النص فهرس رقمي يبدأ من الصفر (Positive Indexing)، ويمكن العد من النهاية بفهارس سالبة (Negative Indexing).</p>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
name = "Qiskit"

print(name[0])     # 'Q'   فهرسة موجبة
print(name[-1])    # 't'   فهرسة سالبة (آخر حرف)
print(len(name))   # 6     عدد الحروف

print(name[1:4])   # 'isk'  تقطيع Slicing: من 1 حتى 4 (غير شامل)
print(name[:3])    # 'Qis'
print(name[3:])    # 'kit'

full = name + " Course"   # Concatenation دمج نصوص
print(full)
          </div>

          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>عملية</th><th>مثال</th><th>الناتج</th></tr></thead>
            <tbody>
              <tr><td>الطول</td><td><code>len("Bell")</code></td><td><code>4</code></td></tr>
              <tr><td>تكرار</td><td><code>"ab" * 3</code></td><td><code>"ababab"</code></td></tr>
              <tr><td>تحويل لحروف كبيرة</td><td><code>"h".upper()</code></td><td><code>"H"</code></td></tr>
            </tbody>
          </table>
          </div>

          <div class="callout">
            <strong>تمرين:</strong>
            من النص <code>"superposition"</code> استخرج الكلمة
            <code>"position"</code> باستخدام Slicing فقط.
          </div>

        </div>
      </details>

      <!-- QPrep 05 : Operators -->
      <details class="lesson" data-lesson="qprep-05" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">05</span>
          <span class="lesson-title">العمليات (Operators): الحسابية والمقارنة</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="code-box math">
+   جمع            a + b
-   طرح            a - b
*   ضرب            a * b
/   قسمة عادية      a / b
//  قسمة صحيحة      a // b   (تقريب للأسفل)
%   باقي القسمة     a % b
**  أس / تربيع      a ** b
          </div>

          <h4>الفرق الحرج بين = و==</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
alpha = 0.7          # إسناد قيمة إلى متغير

alpha == 0.7         # مقارنة: هل alpha تساوي 0.7؟ يُرجع True أو False
          </div>
          <div class="callout warn">
            <strong>خطأ شائع:</strong>
            كتابة <code>if alpha = 0.7:</code> بدلًا من
            <code>if alpha == 0.7:</code> — الأول خطأ syntax في بايثون
            أصلًا، لكنه من أكثر الأخطاء التي يقع فيها القادمون من لغات أخرى.
          </div>

          <h4>عمليات المقارنة</h4>
          <div class="code-box math">
==   يساوي
!=   لا يساوي
>    أكبر من
<    أصغر من
>=   أكبر من أو يساوي
<=   أصغر من أو يساوي
          </div>

          <p>
            هذه العمليات ستُستخدم لاحقًا بكثرة: للتحقق من شرط التطبيع
            <code>|α|² + |β|² == 1</code> (عمليًا بفارق صغير بسبب دقة
            الأعداد العشرية)، ولمقارنة نتائج القياس بالقيم المتوقعة.
          </p>

        </div>
      </details>

      <!-- QPrep 06 : Lists / Tuples / Dicts -->
      <details class="lesson" data-lesson="qprep-06" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">06</span>
          <span class="lesson-title">القوائم والصفوف والقواميس</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <h4>Lists — قابلة للتعديل</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
state = [0.707, 0.707]  # تقريب عددي لـ 1/√2

state.append(0.0)     # إضافة عنصر:      [0.707, 0.707, 0.0]
state.remove(0.0)     # حذف قيمة معيّنة:  [0.707, 0.707]
last = state.pop()    # إزالة وإرجاع آخر عنصر

for amp in state:     # المرور على العناصر (iteration)
    print(amp)

print(state[0:1])     # تقطيع القوائم يعمل كما في النصوص
          </div>

          <h4>Tuples — غير قابلة للتعديل</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
basis = ("0", "1")
print(basis[0])   # "0"
# basis[0] = "x"  # خطأ: TypeError، الـtuple غير قابل للتعديل
          </div>

          <h4>Dictionaries — key/value</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
counts = {"00": 512, "11": 488}

print(counts["00"])        # الوصول بالمفتاح: 512
counts["01"] = 3            # إضافة مفتاح جديد
del counts["01"]             # حذف مفتاح
counts["00"] = 500           # تعديل قيمة موجودة

for state, freq in counts.items():
    print(state, freq)
          </div>

          <h4>متى أستخدم أيًا منها؟</h4>
          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>الحالة</th><th>البنية المناسبة</th></tr></thead>
            <tbody>
              <tr><td>بيانات ستتغير أثناء التشغيل (متجه حالة قيد البناء)</td><td>List</td></tr>
              <tr><td>بيانات ثابتة لا يجب تعديلها (أسماء حالات الأساس)</td><td>Tuple</td></tr>
              <tr><td>ربط تسمية بقيمة (نتائج القياس counts)</td><td>Dictionary</td></tr>
            </tbody>
          </table>
          </div>

        </div>
      </details>

      <!-- QPrep 07 : len() -->
      <details class="lesson" data-lesson="qprep-07" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">07</span>
          <span class="lesson-title">len(): قياس حجم أي بنية بيانات</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
len("Qiskit")              # 6   عدد الحروف
len([1, 2, 3])              # 3   عدد عناصر القائمة
len((0, 1))                  # 2   عدد عناصر الصف
len({"00": 1, "11": 1})       # 2   عدد المفاتيح في القاموس

matrix = [[1, 2], [3, 4], [5, 6]]
len(matrix)                  # 3   عدد الصفوف (القوائم الداخلية)
len(matrix[0])                # 2   عدد الأعمدة في الصف الأول
          </div>

          <p>
            <code>len()</code> دالة عامة تعمل على أي بنية بيانات قابلة
            للعد، وستستخدمها لاحقًا للتحقق من عدد السعات في متجه حالة
            كمي، أو عدد الصفوف/الأعمدة في مصفوفة ممثَّلة كقائمة متداخلة.
          </p>

          <div class="callout warn">
            <strong>انتبه:</strong>
            <code>len()</code> على قاموس تُرجع عدد المفاتيح وليس مجموع
            القيم — خطأ شائع عند حساب إجمالي عدد القياسات (Shots) من
            <code>counts</code>.
          </div>

        </div>
      </details>

      <!-- QPrep 08 : Loops -->
      <details class="lesson" data-lesson="qprep-08" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">08</span>
          <span class="lesson-title">الحلقات: for وwhile وrange()</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
for i in range(5):        # 0,1,2,3,4
    print(i)

results = ["0", "1", "0"]
for shot in results:
    print(shot)

n = 0
while n < 3:
    print("محاولة", n)
    n += 1

for i in range(10):
    if i == 3:
        continue    # تخطي هذه القيمة والاستمرار
    if i == 6:
        break        # إيقاف الحلقة كليًا
    print(i)
          </div>

          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>الأداة</th><th>الاستخدام النموذجي</th></tr></thead>
            <tbody>
              <tr><td><code>for</code></td><td>عدد تكرارات معروف مسبقًا (المرور على Shots)</td></tr>
              <tr><td><code>while</code></td><td>التكرار حتى تحقق شرط (إعادة محاولة شور حتى نجاح)</td></tr>
              <tr><td><code>break</code> / <code>continue</code></td><td>إيقاف مبكر / تخطي حالة معينة</td></tr>
            </tbody>
          </table>
          </div>

        </div>
      </details>

      <!-- QPrep 09 : Conditions -->
      <details class="lesson" data-lesson="qprep-09" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">09</span>
          <span class="lesson-title">الشروط: if / elif / else</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
prob = 0.75

if prob > 0.9:
    print("احتمال مرتفع جدًا")
elif prob > 0.5:
    print("احتمال متوسط إلى مرتفع")
else:
    print("احتمال منخفض")

# شرط متداخل Nested Condition
shot = "01"
if len(shot) == 2:
    if shot == "00" or shot == "11":
        print("نتيجة مترابطة (Bell)")
    else:
        print("نتيجة غير مترابطة")
          </div>

          <p>
            ستستخدم الشروط لاحقًا لتصنيف نتائج القياس (هل كانت الحالة
            <code>00</code> أو <code>11</code> كما هو متوقع من حالة Bell؟)،
            ولاختيار قيمة <code>a</code> جديدة في خوارزمية شور عند فشل محاولة.
          </p>

        </div>
      </details>

      <!-- QPrep 10 : Logic -->
      <details class="lesson" data-lesson="qprep-10" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">10</span>
          <span class="lesson-title">المنطق: and / or / not</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
a, b = True, False

a and b   # False  (يجب أن يكون كلاهما True)
a or b    # True   (يكفي أن يكون أحدهما True)
not a     # False  (نفي القيمة)

# مثال: هل النتيجة تطابق إحدى نتيجتي Bell المتوقعتين؟
shot = "11"
is_bell = (shot == "00") or (shot == "11")
print(is_bell)   # True
          </div>

          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>A</th><th>B</th><th>A and B</th><th>A or B</th></tr></thead>
            <tbody>
              <tr><td>True</td><td>True</td><td>True</td><td>True</td></tr>
              <tr><td>True</td><td>False</td><td>False</td><td>True</td></tr>
              <tr><td>False</td><td>False</td><td>False</td><td>False</td></tr>
            </tbody>
          </table>
          </div>

          <div class="callout">
            <strong>تمرين:</strong>
            اكتب تعبيرًا منطقيًا يتحقق من أن <code>gcd(a, N) == 1</code>
            <strong>و</strong> أن <code>a</code> أكبر من 1 — شرط أساسي عند
            اختيار <code>a</code> في خوارزمية شور.
          </div>

        </div>
      </details>

      <!-- QPrep 11 : Functions -->
      <details class="lesson" data-lesson="qprep-11" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">11</span>
          <span class="lesson-title">الدوال (Functions): تغليف المنطق القابل لإعادة الاستخدام</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np

def check_normalization(alpha, beta):
    # ملاحظة: alpha وbeta قد يكونان أعدادًا مركبة (complex)
    """يتحقق من أن مجموع مربعات السعات يساوي 1 تقريبًا."""
    prob_sum = abs(alpha)**2 + abs(beta)**2
    return abs(prob_sum - 1.0) < 1e-9

# alpha, beta: parameters (المعاملات كما عُرِّفت في الدالة)
# القيم الممرَّرة عند الاستدعاء تسمى arguments

result = check_normalization(1/np.sqrt(2), 1/np.sqrt(2))  # استدعاء
print(result)   # True — الناتج تمت إعادته عبر return
          </div>

          <h4>Scope (نطاق المتغير) — مبسّط</h4>
          <p>
            المتغير المُعرَّف داخل دالة (كـ<code>prob_sum</code> أعلاه) محلي
            لها ولا يمكن الوصول إليه خارجها. أما المتغيرات المعرّفة خارج أي
            دالة فتُعد عامة (Global) ويمكن قراءتها من الداخل.
          </p>

          <h4>دالة رياضية بسيطة</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
def probability(amplitude):
    return abs(amplitude) ** 2

print(probability(0.6))   # 0.36
          </div>

          <div class="callout">
            <strong>تمرين:</strong>
            اكتب دالة <code>is_unitary(M)</code> تتحقق باستخدام NumPy من أن
            <code>M† @ M (المرافق المنقول)</code> يساوي مصفوفة الوحدة تقريبًا (ستحتاجها في QBronze).
          </div>

        </div>
      </details>

      <!-- QPrep 12 : Nested Lists -->
      <details class="lesson" data-lesson="qprep-12" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">12</span>
          <span class="lesson-title">القوائم المتداخلة: الجسر نحو المصفوفات</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <p>
            القائمة المتداخلة (قائمة من قوائم) هي أبسط طريقة لتمثيل جدول
            ثنائي الأبعاد قبل الانتقال إلى NumPy.
          </p>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
matrix = [
    [1, 2],
    [3, 4]
]

print(matrix[0])       # الصف الأول:  [1, 2]
print(matrix[0][1])    # العنصر (صف 0، عمود 1): 2
print(matrix[1][0])    # العنصر (صف 1، عمود 0): 3

# Loop داخل Loop: المرور على كل عنصر
for row in matrix:
    for value in row:
        print(value, end=" ")
    print()
          </div>

          <p>
            الفهرس الأول <code>matrix[i]</code> يحدد <strong>الصف</strong>،
            والفهرس الثاني <code>matrix[i][j]</code> يحدد
            <strong>العمود</strong> داخل ذلك الصف. هذا بالضبط ما ستمثله
            المصفوفة الرياضية <code>M</code>، وهو سبب اعتبار القوائم
            المتداخلة تمهيدًا مباشرًا لمفهوم المصفوفة.
          </p>

          <div class="callout gold">
            <strong>لماذا هذا مهم؟</strong>
            بوابة كمية على كيوبتين تُمثَّل بمصفوفة <code>4×4</code>؛
            فهم الفهرسة الثنائية هنا يجعل قراءة تلك المصفوفة لاحقًا مباشرة.
          </div>

        </div>
      </details>

      <!-- QPrep 13 : NumPy -->
      <details class="lesson" data-lesson="qprep-13" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">13</span>
          <span class="lesson-title">NumPy: من القوائم إلى المصفوفات الحقيقية</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <p>
            NumPy توفر بنية <code>ndarray</code> التي تدعم مباشرة العمليات
            الرياضية (جمع، ضرب، ضرب مصفوفة في متجه) التي لا تدعمها قوائم
            بايثون العادية بكفاءة.
          </p>

          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np

v = np.array([0.6, 0.8])      # متجه بشكل (2,) — للحالات الكمية استخدم dtype=complex
M = np.array([[1, 0], [0, -1]]) # مصفوفة

print(v.shape)   # (2,)      شكل المتجه
print(M.shape)   # (2, 2)    شكل المصفوفة
print(M.ndim)    # 2         عدد الأبعاد
print(M.dtype)   # dtype('int64')  نوع العناصر

print(v[0])      # فهرسة عادية: 0.6
print(v[0:1])    # تقطيع: array([0.6])
          </div>

          <h4>العمليات الحسابية والمتجهية</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
u = np.array([1, 2, 3])
w = np.array([4, 5, 6])

u + w          # جمع عنصرًا بعنصر: [5 7 9]
u * 2          # ضرب في عدد: [2 4 6]
np.dot(u, w)   # الضرب النقطي: 32

M @ v          # ضرب مصفوفة في متجه
          </div>

          <h4>np.linalg وnp.kron</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
np.linalg.norm(v)      # طول المتجه (Norm)
np.linalg.inv(M)        # معكوس المصفوفة (إن وُجد)
np.linalg.eig(M)         # القيم والمتجهات الذاتية Eigenvalues/Eigenvectors

a = np.array([1, 0])
b = np.array([0, 1])
np.kron(a, b)             # الجداء التنسوري: [0 1 0 0]
          </div>

          <div class="callout gold">
            <strong>الربط بالحوسبة الكمية:</strong>
            متجه الحالة الكمي = <code>np.array</code> عمودي، البوابة الكمية
            = مصفوفة NumPy، تطبيق البوابة = <code>M @ v</code>، وبناء نظام
            من عدة كيوبتات = <code>np.kron</code>. هذه الأربعة ستتكرر
            في كل درس من QBronze تقريبًا.
          </div>

        </div>
      </details>

      <!-- QPrep 14 : Matrices -->
      <details class="lesson" data-lesson="qprep-14" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">14</span>
          <span class="lesson-title">المصفوفات: الصفوف، الأعمدة، والعمليات الأساسية</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <h4>ما هي المصفوفة؟</h4>
          <p>
            ترتيب مستطيل من الأعداد بأبعاد <code>(rows × columns)</code>.
            المتجه نفسه حالة خاصة من المصفوفة ببعد <code>(n × 1)</code>.
          </p>

          <div class="code-box math">
M (2×2) =
[ 1   0 ]
[ 0  -1 ]

v (2×1) =
[ 1 ]
[ 0 ]

Mv (2×1) =
[ 1 ]
[ 0 ]
          </div>

          <h4>ضرب مصفوفة في مصفوفة</h4>
          <div class="code-box math">
A(2×2) · B(2×2) = C(2×2)

C[i][j] = Σₖ A[i][k] · B[k][j]
          </div>

          <h4>Transpose وIdentity</h4>
          <div class="code-box math">
Mᵀ : تبديل الصفوف بالأعمدة (Transpose)
M† : المرافق المنقول (Conjugate Transpose) = (M*)ᵀ

I (2×2) =
[ 1   0 ]
[ 0   1 ]

IM = MI = M
          </div>

          <h4>Python</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np

A = np.array([[1, 0], [0, -1]])
B = np.array([[0, 1], [1, 0]])

C = A @ B            # ضرب مصفوفتين
A_T = A.T             # المنقولة Transpose
I = np.identity(2)    # مصفوفة الوحدة

print(np.allclose(A @ I, A))   # True
          </div>

          <h4>مقدمة إلى Eigenvalues / Eigenvectors</h4>
          <p>
            إذا كان <code>Mv = λv</code> لعدد <code>λ</code> ومتجه غير صفري
            <code>v</code>، فإن <code>v</code> متجه ذاتي (Eigenvector)
            و<code>λ</code> قيمته الذاتية (Eigenvalue). هذا المفهوم أساسي
            لفهم Phase Kickback وQPE لاحقًا، حيث يظهر الطور كقيمة ذاتية
            لمؤثر وحدوي.
          </p>

          <div class="callout success">
            <strong>خلاصة QPrep:</strong>
            الآن تمتلك كل ما تحتاجه رياضيًا وبرمجيًا: متغيرات، بنى بيانات،
            تحكم في التدفق، دوال، ومصفوفات NumPy. القسم القادم (QBronze)
            سيستخدم هذه الأدوات لتمثيل أول نظام احتمالي ثم أول كيوبت فعلي.
          </div>

        </div>
      </details>

    </div>
  </div>
</section>

<!-- =========================================================
     QBRONZE — من البت الكلاسيكي إلى بروتوكولات التشابك
========================================================= -->
<section class="section" id="qbronze">
  <div class="container">

    <div class="section-head reveal">
      <span class="eyebrow purple">المرحلة 2 · QBronze</span>
      <h2>من البت الكلاسيكي إلى الحوسبة الكمية</h2>
      <p>
        نبدأ بالبت الكلاسيكي والأنظمة الاحتمالية لبناء حدس رياضي، ثم ننتقل
        إلى Qiskit والكيوبت والتراكب والقياس، ثم إلى الأنظمة متعددة
        الكيوبتات والتشابك والبروتوكولات الكمية الشهيرة.
      </p>
    </div>

    <div class="lesson-list reveal" id="listQbronzeA">

      <!-- 01 Classical Bit -->
      <details class="lesson" data-lesson="qbronze-01" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">01</span>
          <span class="lesson-title">البت الكلاسيكي وأربع دوال ممكنة عليه</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>البت الكلاسيكي له حالتان فقط: <code>0</code> أو <code>1</code> — أساس التمثيل الثنائي (Binary) لكل معلومة كلاسيكية.</p>
          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>المؤثر</th><th>0→</th><th>1→</th><th>المصفوفة</th><th>قابل للعكس؟</th></tr></thead>
            <tbody>
              <tr><td>Identity</td><td>0</td><td>1</td><td><code>[[1,0],[0,1]]</code></td><td>نعم</td></tr>
              <tr><td>NOT</td><td>1</td><td>0</td><td><code>[[0,1],[1,0]]</code></td><td>نعم</td></tr>
              <tr><td>Constant ZERO</td><td>0</td><td>0</td><td><code>[[1,1],[0,0]]</code></td><td>لا</td></tr>
              <tr><td>Constant ONE</td><td>1</td><td>1</td><td><code>[[0,0],[1,1]]</code></td><td>لا</td></tr>
            </tbody>
          </table>
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
NOT = np.array([[0, 1], [1, 0]])
zero = np.array([[1], [0]])
one = NOT @ zero
print(one)   # [[0],[1]]
          </div>
          <div class="callout"><strong>الربط بالكم:</strong> التطور الكمي المغلق يستخدم عمليات قابلة للعكس فقط (Unitary) — تمامًا كـIdentity وNOT هنا، بخلاف الدالتين الثابتتين (غير القابلتين للعكس).</div>
        </div>
      </details>

      <!-- 02 Coin Flipping -->
      <details class="lesson" data-lesson="qbronze-02" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">02</span>
          <span class="lesson-title">رمي العملة الكلاسيكية: أول نموذج احتمالي</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>عملة عادلة: احتمال الصورة (Heads) والكتابة (Tails) متساويان. عملة منحازة: الاحتمالان مختلفان لكن مجموعهما دائمًا 1.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from random import randrange
heads = tails = 0
for _ in range(1000):
    r = randrange(10)
    if r < 6:      # عملة منحازة بنسبة 60% صورة
        heads += 1
    else:
        tails += 1
print("heads ratio =", heads / 1000)
          </div>
          <div class="callout gold"><strong>لماذا نبدأ بهذا؟</strong> رمي العملة هو أبسط نظام "غير حتمي" يمكن بناء حدس رياضي عليه قبل الانتقال لحالة كمية، حيث تصبح "الاحتمالات" لاحقًا "سعات" قابلة للتداخل.</div>
        </div>
      </details>

      <!-- 03 Probabilistic States -->
      <details class="lesson" data-lesson="qbronze-03" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">03</span>
          <span class="lesson-title">الحالة الاحتمالية كمتجه</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
v = [p₀, p₁]ᵀ   حيث p₀,p₁ ≥ 0  و  p₀ + p₁ = 1
          </div>
          <p>هذا الشرط يسمى Normalization — يتكرر في الحالة الكمية لكن على مربعات مقادير السعات المركبة: Σ|αᵢ|₂ = 1</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
v = np.array([[0.5], [0.5]])
print(np.isclose(v.sum(), 1.0))  # True
          </div>
          <h4>مصفوفة الانتقال (Transition Matrix)</h4>
          <div class="code-box math">
v_new = M v
كل عمود في M يجب أن يجمع إلى 1، وكل عناصره غير سالبة.
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
M = np.array([[0.6, 0.3], [0.4, 0.7]])
v = np.array([[1.0], [0.0]])
v_new = M @ v
print(v_new)
          </div>
          <div class="callout"><strong>تمرين:</strong> ابدأ من عملة بحالة <code>[1,0]ᵀ</code> وطبّق مصفوفة الانتقال أعلاه 5 مرات متتالية. ماذا يحدث للتوزيع مع تكرار العملية؟</div>
        </div>
      </details>

      <!-- 04 Operators -->
      <details class="lesson" data-lesson="qbronze-04" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">04</span>
          <span class="lesson-title">المؤثرات (Operators) على الحالات</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>المؤثر (Operator) هو أي تحويل رياضي يأخذ حالة ويُنتج حالة جديدة. في التمثيل بالمصفوفات، تطبيق المؤثر = ضرب مصفوفة في متجه.</p>
          <div class="code-box math">
State Transformation:  v' = M v
          </div>
          <p>هذا هو نفس القالب الذي سنستخدمه لاحقًا لكل بوابة كمية: البوابة مصفوفة، وتطبيقها على الحالة هو ضرب مصفوفة × متجه.</p>
          <div class="callout warn"><strong>خاصية مهمة:</strong> ضرب المصفوفات ليس تبادليًا عمومًا: <code>AB ≠ BA</code>. تغيير ترتيب تطبيق مؤثرين قد يغيّر النتيجة النهائية تمامًا.</div>
        </div>
      </details>

      <!-- 05 Multiple Bits -->
      <details class="lesson" data-lesson="qbronze-05" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">05</span>
          <span class="lesson-title">أكثر من بت: فضاء الحالة يتوسّع</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>نظام من بتين له 4 حالات أساس: <code>00, 01, 10, 11</code>. نظام من n بتات له <code>2ⁿ</code> حالة.</p>
          <div class="code-box math">
v = [p₀₀, p₀₁, p₁₀, p₁₁]ᵀ
          </div>
          <p>إذا كان البتان مستقلين تمامًا، يمكن كتابة توزيعهما المشترك كجداء تنسوري لتوزيعيهما المنفردين: <code>v = v_A ⊗ v_B</code>.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
vA = np.array([0.5, 0.5])
vB = np.array([0.5, 0.5])
v = np.kron(vA, vB)
print(v)   # [0.25 0.25 0.25 0.25]
          </div>
        </div>
      </details>

      <!-- 06 Correlation -->
      <details class="lesson" data-lesson="qbronze-06" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">06</span>
          <span class="lesson-title">الارتباط الكلاسيكي مقابل الاستقلالية</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>بتان مستقلان: التوزيع المشترك = جداء تنسوري للتوزيعين. بتان مرتبطان: لا يمكن كتابة التوزيع كجداء تنسوري.</p>
          <div class="code-box math">
مستقلان:   v = [0.25, 0.25, 0.25, 0.25]ᵀ  (قابل للفصل)
مرتبطان:  v = [0.5,  0,    0,    0.5 ]ᵀ  (غير قابل للفصل)
          </div>
          <div class="callout warn"><strong>تنبيه مهم:</strong> الارتباط الكلاسيكي هنا ليس التشابك الكمي؛ الفرق العميق يكمن في وجود سعات وطور وتداخل في الحالة الكمية، وهو ما لا وجود له في الاحتمالات الكلاسيكية. هذا الدرس حدسي تمهيدي فقط.</div>
        </div>
      </details>

      <!-- 07 Qiskit -->
      <details class="lesson" data-lesson="qbronze-07" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">07</span>
          <span class="lesson-title">مدخل عملي إلى Qiskit</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>Qiskit مكتبة بايثون لبناء دوائر كمية وتشغيلها على محاكيات أو أجهزة حقيقية.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator

qc = QuantumCircuit(1, 1)   # كيوبت واحد، بت كلاسيكي واحد لتخزين القياس
qc.h(0)                      # بوابة Hadamard على الكيوبت 0
qc.measure(0, 0)              # قياس الكيوبت 0 وتخزينه في البت الكلاسيكي 0

print(qc.draw())               # رسم الدائرة نصيًا

sim = AerSimulator()
job = sim.run(qc, shots=1000)   # تشغيل 1000 مرة (Shots)
counts = job.result().get_counts()
print(counts)   # مثال: {'0': 498, '1': 502}
          </div>
          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>المفهوم</th><th>المعنى</th></tr></thead>
            <tbody>
              <tr><td>Quantum Circuit</td><td>تسلسل من البوابات المطبَّقة على كيوبتات</td></tr>
              <tr><td>Shots</td><td>عدد مرات تكرار تشغيل الدائرة وقياسها</td></tr>
              <tr><td>Counts</td><td>قاموس يربط كل نتيجة قياس بعدد مرات ظهورها</td></tr>
            </tbody>
          </table>
          </div>
          <div class="callout gold"><strong>ملاحظة نسخة:</strong> في نسخ Qiskit الحديثة أصبح المحاكي في حزمة منفصلة <code>qiskit_aer</code>، ولم يعد يُستدعى عبر <code>Aer.get_backend()</code> من الحزمة الأساسية كما في نسخ أقدم.</div>
        </div>
      </details>

      <!-- 08 Quantum Bit -->
      <details class="lesson" data-lesson="qbronze-08" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">08</span>
          <span class="lesson-title">الكيوبت: الفرق الجوهري عن البت</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
|0⟩ = [1,0]ᵀ      |1⟩ = [0,1]ᵀ
          </div>
          <p>البت الكلاسيكي يأخذ قيمة واحدة محددة دائمًا. الكيوبت يمكن أن يكون في تراكب من <code>|0⟩</code> و<code>|1⟩</code> في آنٍ واحد قبل القياس.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
zero = np.array([[1],[0]])
one  = np.array([[0],[1]])
          </div>
        </div>
      </details>

      <!-- 09 Quantum State -->
      <details class="lesson" data-lesson="qbronze-09" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">09</span>
          <span class="lesson-title">حالة الكيوبت العامة وشرط التطبيع</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
|ψ⟩ = α|0⟩ + β|1⟩          |α|² + |β|² = 1
          </div>
          <p><code>α</code>,<code>β</code>: سعتان كميتان (Amplitudes)، يمكن أن تكونا سالبتين أو مركبتين. <code>|α|²</code>,<code>|β|²</code>: احتمالا الحصول على 0 أو 1 عند القياس.</p>
          <h4>مثال رقمي</h4>
          <div class="code-box math">
α = 0.6   β = 0.8
0.6² + 0.8² = 0.36 + 0.64 = 1  ✓ حالة مُطبَّعة
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
alpha, beta = 0.6, 0.8  # سعات حقيقية
# مثال بسعة مركبة: alpha = 1/np.sqrt(2), beta = 1j/np.sqrt(2)
print(alpha**2 + beta**2)   # 1.0
          </div>
        </div>
      </details>

      <!-- 10 Bloch / Unit Circle -->
      <details class="lesson" data-lesson="qbronze-10" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">10</span>
          <span class="lesson-title">من دائرة الوحدة إلى كرة بلوخ</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>عندما تكون السعات حقيقية، يمكن تمثيل الحالة بزاوية واحدة على دائرة الوحدة:</p>
          <div class="code-box math">
|ψ⟩ = cos(θ)|0⟩ + sin(θ)|1⟩
          </div>
          <p>عند السماح بسعات مركّبة (تحتوي طورًا)، يصبح التمثيل الهندسي الكامل كرة بلوخ:</p>
          <div class="code-box math">
|ψ⟩ = cos(θ/2)|0⟩ + e^(iφ) sin(θ/2)|1⟩  (مع تجاهل الطور العالمي)
          </div>
          <p><code>θ</code>: زاوية القطب (الميل عن محور Z). <code>φ</code>: الطور النسبي (الدوران حول محور Z).</p>
          <div class="callout warn"><strong>انتبه:</strong> الزاوية θ هنا نصف زاوية الدوران الفعلية التي تستخدمها بوابة <code>RY(θ)</code> في Qiskit — تفصيل سنعود له في درس الدورانات.</div>
        </div>
      </details>

      <!-- 11 Superposition -->
      <details class="lesson" data-lesson="qbronze-11" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">11</span>
          <span class="lesson-title">التراكب (Superposition) وبوابة Hadamard</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
H = 1/√2 [ 1  1 ; 1 -1 ]

H|0⟩ = (|0⟩ + |1⟩)/√2       H|1⟩ = (|0⟩ - |1⟩)/√2
          </div>
          <p>بعد تطبيق H على <code>|0⟩</code>، يصبح احتمال القياس 0 واحتمال القياس 1 متساويين: <code>50%</code> لكل منهما.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
qc = QuantumCircuit(1, 1)
qc.h(0)
qc.measure(0, 0)
          </div>
          <div class="callout gold"><strong>حدس:</strong> التراكب ليس "عدم معرفة" الحالة كما في الاحتمال الكلاسيكي، بل هي حالة فعلية واحدة قادرة على التداخل مع نفسها — وهذا ما تستغله كل الخوارزميات الكمومية.</div>
        </div>
      </details>

      <!-- 12 Measurement -->
      <details class="lesson" data-lesson="qbronze-12" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">12</span>
          <span class="lesson-title">القياس والانهيار (Collapse)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>قبل القياس: تراكب من السعات. عند القياس في الأساس الحسابي: في نموذج القياس الإسقاطي، تنهار الحالة إلى نتيجة كلاسيكية واحدة (0 أو 1)، ولا يمكن استرجاع التراكب الأصلي بعدها من نفس الكيوبت.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator
qc = QuantumCircuit(1, 1)
qc.h(0); qc.measure(0, 0)
counts = AerSimulator().run(qc, shots=1000).result().get_counts()
print(counts)   # {'0': ~500, '1': ~500}
          </div>
          <div class="callout warn"><strong>الفرق المهم:</strong> "الحالة" (State) وصف رياضي كامل قبل القياس. "نتيجة القياس" (Measurement Outcome) رقم كلاسيكي واحد فقط، تحصل عليه بعد الانهيار — لا تخلط بينهما.</div>
        </div>
      </details>

      <!-- 13 Unitary Operations -->
      <details class="lesson" data-lesson="qbronze-13" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">13</span>
          <span class="lesson-title">العمليات الوحدوية (Unitary)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
U†U = I
          </div>
          <p><code>U†</code>: المرافق المنقول (Conjugate Transpose). <code>I</code>: مصفوفة الوحدة. هذا الشرط يضمن الحفاظ على معيار (Norm) متجه الحالة، وبالتالي بقاء شرط التطبيع محققًا بعد أي بوابة.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
H = (1/np.sqrt(2)) * np.array([[1, 1], [1, -1]])
I_check = H.conj().T @ H
print(np.allclose(I_check, np.identity(2)))   # True
          </div>
          <div class="callout"><strong>فكرة للحفظ:</strong> كل بوابة كمية "منفردة" (بدون قياس) يجب أن تكون Unitary وبالتالي قابلة للعكس تمامًا — بخلاف القياس نفسه، الذي ليس عملية وحدوية.</div>
        </div>
      </details>

      <!-- 14 Rotations -->
      <details class="lesson" data-lesson="qbronze-14" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">14</span>
          <span class="lesson-title">بوابات الدوران: RX وRY وRZ</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
RY(θ) =
[ cos(θ/2)  -sin(θ/2) ]
[ sin(θ/2)   cos(θ/2) ]

RY(θ)|0⟩ = [ cos(θ/2), sin(θ/2) ]ᵀ
P(0) = cos²(θ/2)     P(1) = sin²(θ/2)
          </div>
          <p>RX وRZ تدوّران الحالة حول محوري X وZ في كرة بلوخ بنفس المنطق، بمصفوفات مختلفة تتضمن أعدادًا مركبة في حالة RZ.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from math import pi
from qiskit import QuantumCircuit
qc = QuantumCircuit(1, 1)
qc.ry(2 * (pi/3), 0)   # لإنتاج cos(pi/3)|0>+sin(pi/3)|1>: زاوية RY = 2φ
qc.measure(0, 0)
          </div>
          <div class="callout warn"><strong>تنبيه على الزاوية:</strong> إذا أردت الحالة <code>cos(φ)|0⟩+sin(φ)|1⟩</code>، فبوابة <code>RY</code> تحتاج الزاوية <code>θ=2φ</code> — خطأ شائع جدًا عند برمجة تراكب باحتمال محدد مسبقًا.</div>
        </div>
      </details>

      <!-- 15 Reflections -->
      <details class="lesson" data-lesson="qbronze-15" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">15</span>
          <span class="lesson-title">الانعكاسات (Reflections)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>الانعكاس تحويل هندسي يعكس متجه الحالة حول محور أو حول متجه آخر، وهو Unitary أيضًا. بوابة Pauli-Z مثال بسيط: انعكاس حول محور <code>|0⟩</code>.</p>
          <div class="code-box math">
Z = [ 1  0 ; 0  -1 ]     Z|0⟩=|0⟩   Z|1⟩=-|1⟩
          </div>
          <p>هندسيًا، الانعكاس حول متجه <code>|φ⟩</code> يُكتب كمؤثر: <code>R = 2|φ⟩⟨φ| - I</code>، وهذه الفكرة أساس خوارزمية Grover (خارج نطاق QBronze لكنها تعتمد مباشرة على هذا الدرس).</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
phi = np.array([[1],[0]])
R = 2 * (phi @ phi.conj().T) - np.identity(2)
print(R)   # نفس مصفوفة Z
          </div>
        </div>
      </details>

      <!-- 16 Tomography -->
      <details class="lesson" data-lesson="qbronze-16" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">16</span>
          <span class="lesson-title">التصوير المقطعي الكمي (Quantum State Tomography)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>قياس واحد يعطي نتيجة كلاسيكية واحدة فقط، ولا يكشف عن السعات الكاملة (بما فيها الطور). لإعادة بناء الحالة نحتاج قياسات متعددة على أسس مختلفة (X, Y, Z) وعلى نسخ متطابقة كثيرة من نفس الحالة.</p>
          <div class="code-box math">
قياس على أساس Z → يعطي |α|² و|β|²
قياس على أساس X → يعطي معلومة عن الطور النسبي
          </div>
          <h4>مثال مبسط لإعادة بناء حالة حقيقية</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator

def measure_basis(state_prep, basis_gate=None, shots=2000):
    qc = QuantumCircuit(1, 1)
    state_prep(qc)
    if basis_gate == "X":
        qc.h(0)          # تدوير أساس X إلى أساس Z قبل القياس
    qc.measure(0, 0)
    counts = AerSimulator().run(qc, shots=shots).result().get_counts()
    return counts

def prep(qc):
    qc.ry(1.0, 0)   # حالة مجهولة نريد "تصويرها"

z_counts = measure_basis(prep, basis_gate=None)
x_counts = measure_basis(prep, basis_gate="X")
# لإكمال التصوير المقطعي نحتاج أيضًا قياس Y:
# y_counts = measure_basis(prep, basis_gate="Y")  # عبر S† ثم H
print("Z basis:", z_counts)
print("X basis:", x_counts)
          </div>
          <div class="callout gold"><strong>الفكرة الأساسية:</strong> نستخدم إحصائيات القياس على الأسس X وY وZ لإعادة بناء متجه بلوخ (x,y,z) ومنه مصفوفة الكثافة ρ = 0.5(I + xX + yY + zZ) — هذا هو جوهر Tomography، وسنطبقه على كيوبتين في المشروع الخامس.</div>
        </div>
      </details>

      <!-- 17 Two Qubits -->
      <details class="lesson" data-lesson="qbronze-17" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">17</span>
          <span class="lesson-title">نظام كيوبتين: الجداء التنسوري في العمل</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
|00⟩  |01⟩  |10⟩  |11⟩     (بُعد الفضاء = 4)

|ψ⟩⊗|φ⟩ = αγ|00⟩+αδ|01⟩+βγ|10⟩+βδ|11⟩  (مع تثبيت اصطلاح ترتيب الكيوبتات في Qiskit)
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
psi = np.array([1, 0])       # |0>
phi = np.array([1, 0])       # |0>
psi_phi = np.kron(psi, phi)  # |00>
print(psi_phi)   # [1 0 0 0]
          </div>
          <div class="callout warn"><strong>تنبيه:</strong> هذا التمثيل بالجداء التنسوري صالح فقط للحالات القابلة للفصل (Product States). في الحالة العامة — وخاصة عند التشابك — لا يمكن كتابة الحالة على هذا الشكل، كما سنرى في حالة Bell.</div>
        </div>
      </details>

      <!-- 18 Phase Kickback -->
      <details class="lesson" data-lesson="qbronze-18" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">18</span>
          <span class="lesson-title">Phase Kickback: كيف "يرتد" الطور نحو كيوبت التحكم؟</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>إذا كان <code>|φ⟩</code> متجهًا ذاتيًا لمؤثر وحدوي <code>U</code> بقيمة ذاتية <code>e^(iθ)</code>، وطبّقنا نسخة متحكَّم بها من <code>U</code> (Controlled-U) على كيوبت هدف في الحالة <code>|φ⟩</code>، مع كيوبت تحكم في تراكب:</p>
          <div class="code-box math">
U|φ⟩ = e^(iθ)|φ⟩

(|0⟩+|1⟩)/√2 ⊗ |φ⟩  --C-U-->  (|0⟩ + e^(iθ)|1⟩)/√2 ⊗ |φ⟩
          </div>
          <p>الطور <code>θ</code> "ارتد" من كيوبت الهدف (الذي بقيت حالته دون تغيير) إلى كيوبت التحكم، حيث أصبح طورًا نسبيًا قابلًا للقياس عبر H ثم قياس أساس Z. هذه الفكرة هي حجر الأساس لخوارزمية QPE في QSilver.</p>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
qc = QuantumCircuit(2, 1)
qc.x(1)              # تحضير كيوبت الهدف في حالة ذاتية لـ Z (|1>)
qc.h(0)               # تراكب على كيوبت التحكم
qc.cz(0, 1)            # Controlled-Z: مثال على Controlled-U
qc.h(0)                 # لإرجاع الطور إلى فارق قابل للقياس على أساس Z
qc.measure(0, 0)
          </div>
        </div>
      </details>

      <!-- 19 Bell States / Entanglement -->
      <details class="lesson" data-lesson="qbronze-19" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">19</span>
          <span class="lesson-title">حالات Bell والتشابك الكمي</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
|00⟩ --H(q0)--> (|00⟩+|10⟩)/√2 --CNOT(0,1)--> (|00⟩+|11⟩)/√2 = |Φ⁺⟩
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
qc = QuantumCircuit(2, 2)
qc.h(0)
qc.cx(0, 1)
qc.measure([0, 1], [0, 1])
          </div>
          <p>حالة Bell متشابكة لأنه لا يمكن كتابتها كجداء تنسوري لحالتي كيوبت منفردتين: <code>|Φ⁺⟩ ≠ |ψ_A⟩⊗|ψ_B⟩</code>. عند القياس، تظهر النتيجتان <code>00</code> أو <code>11</code> فقط (في الحالة المثالية)، بارتباط تام بين الكيوبتين.</p>
          <div class="callout warn"><strong>تنبيه مهم:</strong> التشابك الكمي لا يعني إمكانية إرسال معلومة كلاسيكية أسرع من الضوء؛ الترابط بين النتائج لا يوفر وحده قناة اتصال فورية.</div>
        </div>
      </details>

      <!-- 20 Superdense Coding -->
      <details class="lesson" data-lesson="qbronze-20" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">20</span>
          <span class="lesson-title">الترميز فائق الكثافة: بتان في كيوبت واحد</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>باستخدام زوج Bell مُشترك مسبقًا بين Alice وBob، يمكن لـAlice إرسال بتين كلاسيكيين إلى Bob بإرسال كيوبتها فقط (كيوبت واحد)، شرط أن يكون زوج التشابك قد أُنشئ مسبقًا — وهذا هو "المورد" الذي يجعل البروتوكول ممكنًا.</p>
          <div class="code-box math">
Encoding (Alice):
00 → I     01 → X     10 → Z     11 → XZ

Decoding (Bob): CNOT ثم H، ثم قياس الكيوبتين
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
bits = "10"   # الرسالة المراد إرسالها

qc = QuantumCircuit(2, 2)
qc.h(0); qc.cx(0, 1)     # تحضير زوج Bell مشترك

if bits == "01": qc.x(0)
elif bits == "10": qc.z(0)
elif bits == "11": qc.x(0); qc.z(0)

qc.cx(0, 1); qc.h(0)      # فك الترميز عند Bob
qc.measure([0, 1], [0, 1])
          </div>
          <p>هذا التفصيل يوضح لماذا "يكفي كيوبت واحد": التشابك المُنشأ مسبقًا يحمل بالفعل نصف المعلومة، وإرسال الكيوبت الآخر يكمل استخلاص البتين الكاملين.</p>
        </div>
      </details>

      <!-- 21 Teleportation -->
      <details class="lesson" data-lesson="qbronze-21" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">21</span>
          <span class="lesson-title">الانتقال الآني الكمي (Teleportation)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>ينقل بروتوكول Teleportation حالة كيوبت غير معروفة من Alice إلى Bob، باستخدام زوج Bell مشترك مسبقًا واتصال كلاسيكي (وليس نقلًا للمادة أو للمعلومة أسرع من الضوء).</p>
          <div class="code-box math">
1. Alice وBob يتشاركان زوج Bell.
2. Alice تطبّق CNOT ثم H بين كيوبت الرسالة وكيوبتها من الزوج.
3. Alice تقيس كيوبتيها وترسل النتيجتين (بتين كلاسيكيين) إلى Bob.
4. Bob يطبّق X و/أو Z على كيوبته حسب النتيجتين المستلمتين.
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
qc = QuantumCircuit(3, 3)
qc.ry(0.9, 0)          # الحالة المراد نقلها على q0

qc.h(1); qc.cx(1, 2)    # زوج Bell بين q1 (Alice) وq2 (Bob)
qc.cx(0, 1); qc.h(0)     # عمليات Alice على q0 وq1
qc.measure([0, 1], [0, 1])

qc.cx(1, 2)               # تصحيح Bob بناءً على q1
qc.cz(0, 2)                # تصحيح Bob بناءً على q0
qc.measure(2, 2)
          </div>
          <p>الاتصال الكلاسيكي (إرسال نتيجتي القياس) ضروري ولا يمكن الاستغناء عنه؛ بدونه لا يعرف Bob أي تصحيح يطبّق، وهذا بالضبط ما يمنع البروتوكول من مخالفة مبدأ عدم تجاوز سرعة الضوء.</p>
        </div>
      </details>

      <!-- 22 Multi-Control Gates -->
      <details class="lesson" data-lesson="qbronze-22" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">22</span>
          <span class="lesson-title">البوابات متعددة التحكم: CNOT وToffoli</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <div class="code-box math">
CNOT: |10⟩→|11⟩  |11⟩→|10⟩  (تحكم ثم هدف، تبسيطًا)
Toffoli (CCX): يقلب الهدف فقط إذا كان كلا كيوبتي التحكم = 1
          </div>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
qc.cx(0, 1)             # CNOT
qc.ccx(0, 1, 2)          # Toffoli (كيوبتا تحكم: 0 و1، هدف: 2)
          </div>
          <div class="callout warn"><strong>Little-Endian في Qiskit:</strong> تعرض Qiskit نتائج القياس بحيث يظهر <code>q0</code> في أقصى يمين السلسلة. عند مقارنة متجه الحالة النظري بمفاتيح <code>counts</code>، لا تفترض تطابق الترتيب دون التحقق.</div>
        </div>
      </details>

      <!-- 23 Photonic Quantum Coin -->
      <details class="lesson" data-lesson="qbronze-23" open>
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">23</span>
          <span class="lesson-title">رمي العملة الكمية بالفوتونات</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">
          <p>يمكن تحقيق "عملة كمية" فيزيائيًا باستخدام فوتون واحد يمر على مقسّم شعاع (Beam Splitter): يوضع الفوتون في تراكب بين مسارين محتملين (مكافئ لـ<code>|0⟩</code> و<code>|1⟩</code>)، ثم يُكتشف في أحد كاشفين.</p>
          <div class="code-box math">
Beam Splitter  ≈  بوابة Hadamard على الفوتون
كاشف 1 / كاشف 2  ≈  نتيجة القياس 0 / 1
          </div>
          <p>هذا النموذج الفيزيائي مطابق رياضيًا لما درسناه مع H والقياس: التراكب قبل الكشف، والانهيار إلى نتيجة واحدة عند الكشف، مع احتمال 50/50 عند مقسّم شعاع متوازن.</p>
          <div class="callout gold"><strong>لماذا يهم هذا المثال؟</strong> يوضح أن الحوسبة الكمية ليست حصرًا على الكيوبتات الفائقة التوصيل؛ نفس الرياضيات (متجهات الحالة، Unitary، القياس) تصف أنظمة فيزيائية مختلفة تمامًا مثل الفوتونات.</div>
        </div>
      </details>

    </div>

    <span class="stage-anchor" id="qbronze-projects"></span>
    <div class="part-divider">المشاريع التطبيقية السبعة — الجزء الرابع من QBronze (32–38)</div>

    <div class="lesson-list reveal" id="listQbronzeProjects">

      <!-- Project 1 -->
      <details class="lesson" data-lesson="qbronze-p1">
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">P1</span>
          <span class="lesson-title">مشروع 1 — لعبة الترابط (Correlation Game)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="project-meta">
            <span class="project-tag">Python + NumPy</span>
            <span class="project-tag">مبني على: قسم 3 و6 من QBronze</span>
          </div>

          <h4>الهدف</h4>
          <p>بناء محاكاة كلاسيكية بسيطة تُظهر كيف تنشأ حالة "ترابط" بين بتين، ومقارنتها بحالة استقلال تام، لبناء حدس تمهيدي لفهم التشابك الكمي لاحقًا.</p>

          <h4>المتطلبات</h4>
          <ul><li>بايثون + NumPy</li><li>فهم متجه الحالة الاحتمالي والجداء التنسوري</li></ul>

          <h4>المفاهيم السابقة</h4>
          <p>الحالة الاحتمالية (QBronze-03)، الارتباط الكلاسيكي (QBronze-06)، الجداء التنسوري (QPrep-13).</p>

          <h4>شرح فكرة المشروع</h4>
          <p>"اللعبة" تتكون من مصدر عشوائي واحد يتحكم في حالتي بتين معًا (بدلًا من مصدرين مستقلين)، بحيث تظهر نتائج البتين دائمًا متطابقة: <code>00</code> أو <code>11</code> فقط. هذا يحاكي — بشكل كلاسيكي بحت — "الترابط" الذي سنراه لاحقًا بصورته الكمية الحقيقية في حالة Bell.</p>

          <h4>خطوات التنفيذ</h4>
          <ol>
            <li>ولّد قيمة عشوائية واحدة مشتركة (0 أو 1).</li>
            <li>اجعل حالة كلا البتين تساوي تلك القيمة نفسها.</li>
            <li>كرر التجربة 1000 مرة وسجّل توزيع النتائج الأربع الممكنة.</li>
            <li>قارن التوزيع الناتج بتوزيع بتين مستقلين تمامًا.</li>
          </ol>

          <h4>الكود الكامل</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from random import randrange

def correlated_trial():
    shared = randrange(2)          # مصدر عشوائي واحد يتحكم في الاثنين
    return f"{shared}{shared}"      # "00" أو "11" فقط

def independent_trial():
    bit_a = randrange(2)
    bit_b = randrange(2)
    return f"{bit_a}{bit_b}"

def run_experiment(trial_fn, n=2000):
    counts = {"00": 0, "01": 0, "10": 0, "11": 0}
    for _ in range(n):
        counts[trial_fn()] += 1
    return counts

print("مترابط:  ", run_experiment(correlated_trial))
print("مستقل:   ", run_experiment(independent_trial))
          </div>

          <h4>شرح الكود</h4>
          <p><code>correlated_trial</code> تستخدم متغيرًا عشوائيًا واحدًا فقط لكلا البتين، فتظهر النتائج دائمًا متطابقة. <code>independent_trial</code> تستخدم متغيرين عشوائيين منفصلين، فتوزَّع النتائج الأربع بالتساوي تقريبًا.</p>

          <h4>النتيجة المتوقعة</h4>
          <p>في التجربة المترابطة: تقريبًا نصف النتائج <code>00</code> والنصف الآخر <code>11</code>، وصفر تقريبًا لـ<code>01</code> و<code>10</code>. في التجربة المستقلة: توزيع شبه متساوٍ على الحالات الأربع.</p>

          <h4>أسئلة للفهم</h4>
          <ul>
            <li>لماذا لا يمكن كتابة توزيع الحالة المترابطة كجداء تنسوري لتوزيعين منفردين؟</li>
            <li>ما الفرق الجوهري بين هذا "الترابط" الكلاسيكي والتشابك الكمي الذي سنراه في المشروع السادس والسابع؟</li>
          </ul>

          <h4>تحدٍ إضافي</h4>
          <p>عدّل الكود لإنشاء ترابط "جزئي" (مثلًا: تطابق في 80% من الحالات فقط)، ثم احسب مصفوفة الانتقال المكافئة لهذا النظام.</p>

        </div>
      </details>

      <!-- Project 2 -->
      <details class="lesson" data-lesson="qbronze-p2">
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">P2</span>
          <span class="lesson-title">مشروع 2 — تبديل الحالات الكمية (Quantum State Swap)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="project-meta">
            <span class="project-tag">Qiskit</span>
            <span class="project-tag">مبني على: قسم 17، 19، 22 من QBronze</span>
          </div>

          <h4>الهدف</h4>
          <p>بناء دائرة كمية تبادل حالتي كيوبتين مع بعضهما بالكامل، والتحقق من صحة التبديل عبر القياس.</p>

          <h4>المتطلبات</h4>
          <ul><li>Qiskit وqiskit_aer</li><li>فهم CNOT وأنظمة الكيوبتين</li></ul>

          <h4>المفاهيم السابقة</h4>
          <p>نظام كيوبتين (QBronze-17)، CNOT (QBronze-22)، القياس (QBronze-12).</p>

          <h4>شرح فكرة المشروع</h4>
          <p>بوابة SWAP تبادل حالتي كيوبتين بالكامل. يمكن بناؤها من ثلاث بوابات CNOT متتالية بترتيب تحكم/هدف متبادل: <code>CNOT(a,b) → CNOT(b,a) → CNOT(a,b)</code>.</p>

          <h4>خطوات التنفيذ</h4>
          <ol>
            <li>حضّر كيوبت 0 في حالة <code>|1⟩</code> وكيوبت 1 في حالة <code>|0⟩</code>.</li>
            <li>طبّق ثلاث بوابات CNOT متتالية بالترتيب المذكور أعلاه (أو استخدم <code>qc.swap()</code> مباشرة).</li>
            <li>قِس الكيوبتين وتحقق من أن الحالتين تبادلتا.</li>
          </ol>

          <h4>الكود الكامل</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator

qc = QuantumCircuit(2, 2)
qc.x(0)                 # q0 = |1>, q1 = |0>

qc.cx(0, 1)              # بناء SWAP يدويًا من 3 CNOT
qc.cx(1, 0)
qc.cx(0, 1)
# البديل المباشر: qc.swap(0, 1)

qc.measure([0, 1], [0, 1])

sim = AerSimulator()
counts = sim.run(qc, shots=1000).result().get_counts()
print(counts)   # متوقع: {'01': ~1000}  (q0=0, q1=1 بترتيب Little-Endian)
          </div>

          <h4>شرح الكود</h4>
          <p>بعد بناء الحالة الابتدائية <code>|10⟩</code> (q1=1, q0=0 حسب اتفاقية الكتابة q1q0)، تبادل بوابات CNOT الثلاث محتوى الكيوبتين، فتصبح q0=1 وq1=0.</p>

          <h4>النتيجة المتوقعة والتحليل</h4>
          <p>يجب أن تظهر نتيجة واحدة فقط بشكل شبه كامل في <code>counts</code>، مطابقة للحالة بعد التبديل. أي انحراف كبير يشير لخطأ في ترتيب CNOT أو في قراءة ترتيب Little-Endian.</p>

          <h4>أسئلة للفهم</h4>
          <ul>
            <li>لماذا تعيد ثلاث بوابات CNOT متتالية (وليس اثنتان) التبديل الصحيح؟</li>
            <li>هل بوابة SWAP وحدوية (Unitary)؟ برهن ذلك عدديًا بضرب مصفوفتها في منقولتها المرافقة.</li>
          </ul>

          <h4>تحدٍ إضافي</h4>
          <p>طبّق SWAP على حالة تراكب (وليس حالة أساس نقية) وتحقق أن السعات نفسها تبادلت باستخدام <code>Statevector</code> بدلًا من القياس المباشر.</p>

        </div>
      </details>

      <!-- Project 3 -->
      <details class="lesson" data-lesson="qbronze-p3">
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">P3</span>
          <span class="lesson-title">مشروع 3 — محاكاة كيوبت ذي قيم حقيقية (Real-Valued Qubit)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="project-meta">
            <span class="project-tag">Python + NumPy + Matplotlib</span>
            <span class="project-tag">مبني على: قسم 9، 10 من QBronze</span>
          </div>

          <h4>الهدف</h4>
          <p>بناء تمثيل برمجي كامل لكيوبت ذي سعات حقيقية (بدون طور مركّب)، وتصوره كنقطة على دائرة الوحدة، مع دالة قياس تجريبية.</p>

          <h4>المتطلبات</h4>
          <ul><li>NumPy وMatplotlib</li><li>فهم <code>|ψ⟩=cos(θ)|0⟩+sin(θ)|1⟩</code></li></ul>

          <h4>شرح فكرة المشروع</h4>
          <p>بما أن السعات حقيقية، تُوصف الحالة بزاوية واحدة فقط <code>θ</code> على دائرة الوحدة. سنبني كلاسًا بسيطًا يمثّل هذه الحالة، ويحاكي القياس عبر توليد عينات عشوائية موزونة باحتمالات <code>cos²(θ)</code> و<code>sin²(θ)</code>.</p>

          <h4>المطلوب من الطالب</h4>
          <ul>
            <li>تمثيل الحالة كزوج <code>(alpha, beta)</code> مع التحقق من شرط التطبيع.</li>
            <li>دالة <code>measure()</code> تُرجع 0 أو 1 باحتمالات صحيحة.</li>
            <li>رسم بياني لتوزيع 1000 قياس مقابل التوقع النظري.</li>
          </ul>

          <h4>الكود الكامل</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np
import matplotlib.pyplot as plt

class RealQubit:
    def __init__(self, theta):
        self.theta = theta
        self.alpha = np.cos(theta)
        self.beta = np.sin(theta)
        assert abs(self.alpha**2 + self.beta**2 - 1) < 1e-9, "الحالة غير مُطبَّعة"

    def probabilities(self):
        return self.alpha**2, self.beta**2

    def measure(self):
        p0, p1 = self.probabilities()
        return np.random.choice([0, 1], p=[p0, p1])

q = RealQubit(theta=np.pi/3)
results = [q.measure() for _ in range(1000)]

p0_theory, p1_theory = q.probabilities()
p0_exp = results.count(0) / len(results)

print(f"P(0) نظري = {p0_theory:.3f} | تجريبي = {p0_exp:.3f}")

plt.bar(["0", "1"], [results.count(0), results.count(1)])
plt.title("توزيع نتائج قياس RealQubit")
plt.show()
          </div>

          <h4>شرح الكود</h4>
          <p>الكلاس <code>RealQubit</code> يخزن الزاوية ويحسب السعتين تلقائيًا، ويتحقق من صحة التطبيع فور الإنشاء عبر <code>assert</code>. دالة <code>measure()</code> تستخدم <code>np.random.choice</code> لمحاكاة القياس الاحتمالي دون استخدام Qiskit على الإطلاق.</p>

          <h4>النتيجة المتوقعة</h4>
          <p>قيمتا P(0) النظرية والتجريبية يجب أن تتقاربا مع زيادة عدد القياسات (قانون الأعداد الكبيرة)، مع فارق طبيعي صغير بسبب العشوائية.</p>

          <h4>أسئلة للفهم</h4>
          <ul><li>ماذا يحدث لو مررت <code>theta</code> بحيث لا يتحقق شرط التطبيع؟ ولماذا وضعنا <code>assert</code>؟</li></ul>

          <h4>تحدٍ إضافي</h4>
          <p>وسّع الكلاس لدعم سعات مركّبة (أضف معامل <code>phi</code> للطور)، مع العلم أن احتمالات القياس على أساس Z لا تتأثر بالطور الكلي، لكنها قد تحتاج تعديل دالة القياس على أسس أخرى.</p>

        </div>
      </details>

      <!-- Project 4 -->
      <details class="lesson" data-lesson="qbronze-p4">
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">P4</span>
          <span class="lesson-title">مشروع 4 — محاكي كمي خاص بك (Build Your Own Simulator)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="project-meta">
            <span class="project-tag">Python + NumPy فقط (بدون Qiskit)</span>
            <span class="project-tag">مبني على: كل دروس QBronze السابقة</span>
          </div>

          <h4>الهدف</h4>
          <p>بناء محاكي كمي بسيط من الصفر بلغة بايثون وNumPy، يدعم عدة كيوبتات، بوابات أساسية، والقياس — دون استخدام Qiskit إطلاقًا. هذا يثبت الفهم العميق لكل ما سبق.</p>

          <h4>المتطلبات</h4>
          <ul><li>NumPy</li><li>فهم كامل لتمثيل الحالة، الجداء التنسوري، وتطبيق المصفوفات</li></ul>

          <h4>التصميم المقترح</h4>
          <ul>
            <li>تمثيل الحالة: متجه NumPy واحد ببعد <code>2ⁿ</code> لعدد <code>n</code> من الكيوبتات، يبدأ كـ<code>|00...0⟩</code>.</li>
            <li>تمثيل العمليات: تمديد مصفوفة البوابة (2×2) إلى مصفوفة كاملة بحجم <code>2ⁿ×2ⁿ</code> باستخدام الجداء التنسوري مع مصفوفات الوحدة على بقية الكيوبتات.</li>
            <li>القياس: أخذ مربعات القيم المطلقة للسعات كاحتمالات، ثم استخدام <code>np.random.choice</code>.</li>
          </ul>

          <h4>بنية المحاكي وخطوات البناء</h4>
          <ol>
            <li>دالة إنشاء الحالة الابتدائية.</li>
            <li>دالة لتمديد بوابة كيوبت واحد إلى النظام الكامل عبر <code>np.kron</code>.</li>
            <li>دالة تطبيق بوابة على الحالة (<code>state = full_gate @ state</code>).</li>
            <li>دالة قياس تعيد نتيجة واحدة وفق الاحتمالات.</li>
            <li>واجهة بسيطة تشبه Qiskit: <code>simulator.h(0)</code>، <code>simulator.cx(0,1)</code>، <code>simulator.measure()</code>.</li>
          </ol>

          <h4>كود أساسي</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
import numpy as np

I = np.identity(2)
H = (1/np.sqrt(2)) * np.array([[1, 1], [1, -1]])
X = np.array([[0, 1], [1, 0]])

class MiniQuantumSimulator:
    def __init__(self, n_qubits):
        self.n = n_qubits
        self.state = np.zeros(2**n_qubits)
        self.state[0] = 1.0   # |00...0>

    def _expand(self, gate, target):
        """تمديد بوابة كيوبت واحد إلى مصفوفة كاملة عبر np.kron."""
        full = None
        for q in range(self.n):
            op = gate if q == target else I
            full = op if full is None else np.kron(full, op)
        return full

    def h(self, target):
        self.state = self._expand(H, target) @ self.state

    def x(self, target):
        self.state = self._expand(X, target) @ self.state

    def cx(self, control, target):
        n = self.n
        dim = 2**n
        full = np.identity(dim)
        for i in range(dim):
            bits = list(format(i, f"0{n}b"))
            # اتفاقية: bits[0] يمثل الكيوبت الأخير (n-1) ... تبسيطًا نستخدم فهرسة مباشرة
            idx_c = n - 1 - control
            idx_t = n - 1 - target
            if bits[idx_c] == "1":
                bits[idx_t] = "1" if bits[idx_t] == "0" else "0"
            j = int("".join(bits), 2)
            full[j, i] = 1
            if j != i:
                full[i, i] = 0
        self.state = full @ self.state

    def probabilities(self):
        return np.abs(self.state) ** 2

    def measure(self, shots=1000):
        probs = self.probabilities()
        outcomes = np.random.choice(len(probs), size=shots, p=probs)
        counts = {}
        for o in outcomes:
            key = format(o, f"0{self.n}b")
            counts[key] = counts.get(key, 0) + 1
        return counts

# اختبار: بناء حالة Bell يدويًا
sim = MiniQuantumSimulator(2)
sim.h(0)
sim.cx(0, 1)
print(sim.probabilities())   # متوقع: [0.5, 0, 0, 0.5]
print(sim.measure())
          </div>

          <h4>شرح الكود</h4>
          <p><code>_expand</code> تبني المصفوفة الكاملة لأي بوابة كيوبت واحد عبر ضربها تنسوريًا مع مصفوفات الوحدة على بقية الكيوبتات، بنفس منطق درس QPrep-13 وQBronze-17. دالة <code>cx</code> أكثر تعقيدًا لأنها بوابة ثنائية الكيوبت؛ تبني مصفوفة تبديل صريحة بالمرور على كل حالة أساس والتحقق من قيمة كيوبت التحكم.</p>

          <h4>النتيجة المتوقعة</h4>
          <p>بعد <code>h(0)</code> ثم <code>cx(0,1)</code>، يجب أن تكون الاحتمالات <code>[0.5, 0, 0, 0.5]</code> بالضبط — أي حالة Bell كما اشتُقت رياضيًا في QBronze-19.</p>

          <h4>تطويرات اختيارية</h4>
          <ul>
            <li>إضافة دعم لبوابات <code>RY</code> و<code>Z</code> و<code>CCX (Toffoli)</code>.</li>
            <li>دعم السعات المركّبة (Complex) بدلًا من الحقيقية فقط.</li>
            <li>إضافة دالة <code>draw()</code> نصية بسيطة تطبع تسلسل البوابات المطبَّقة.</li>
          </ul>

          <div class="callout gold"><strong>تحدٍ إضافي:</strong> استخدم محاكيك الخاص لإعادة بناء بروتوكول الترميز فائق الكثافة (المشروع 7) بالكامل دون Qiskit، وقارن النتائج.</div>

        </div>
      </details>

      <!-- Project 5 -->
      <details class="lesson" data-lesson="qbronze-p5">
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">P5</span>
          <span class="lesson-title">مشروع 5 — التصوير المقطعي الكمي بكيوبتات متعددة</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="project-meta">
            <span class="project-tag">Qiskit</span>
            <span class="project-tag">مبني على: قسم 16، 17 من QBronze</span>
          </div>

          <h4>الهدف</h4>
          <p>توسيع فكرة Tomography (QBronze-16) من كيوبت واحد إلى نظام كيوبتين، لإعادة بناء تقدير لتوزيع الاحتمالات الكاملة لحالة مجهولة.</p>

          <h4>لماذا نحتاج عدة قياسات؟</h4>
          <p>قياس واحد على أساس واحد لا يكشف التوزيع الكامل، خصوصًا مع وجود ارتباط/تشابك محتمل بين الكيوبتين. لذلك نكرر التحضير نفسه عدة مرات ونقيس على أسس مختلفة، ثم نجمع الإحصائيات.</p>

          <h4>جمع بيانات القياس والتعامل مع أكثر من كيوبت</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator

def prepare_unknown_state(qc):
    qc.h(0)
    qc.cx(0, 1)   # حالة Bell "مجهولة" لأغراض التمرين

def measure_in_basis(basis_q0, basis_q1, shots=2000):
    qc = QuantumCircuit(2, 2)
    prepare_unknown_state(qc)
    for q, basis in enumerate([basis_q0, basis_q1]):
        if basis == "X":
            qc.h(q)
    qc.measure([0, 1], [0, 1])
    return AerSimulator().run(qc, shots=shots).result().get_counts()

zz = measure_in_basis("Z", "Z")
xx = measure_in_basis("X", "X")
zx = measure_in_basis("Z", "X")

print("ZZ:", zz)
print("XX:", xx)
print("ZX:", zx)
          </div>

          <h4>إعادة بناء الحالة وتحليل النتائج</h4>
          <p>من قياسات <code>ZZ</code> نتوقع فقط <code>00</code> و<code>11</code> (ترابط تام على أساس Z). من قياسات <code>XX</code> نتوقع أيضًا نمطًا محددًا (ترابط على أساس X) يميز حالة Bell عن حالة كلاسيكية مرتبطة فقط على أساس Z — وهذا بالضبط ما يكشف وجود تشابك حقيقي وليس مجرد ارتباط كلاسيكي.</p>

          <h4>أسئلة للفهم</h4>
          <ul><li>لماذا لا يكفي قياس <code>ZZ</code> وحده لإثبات وجود تشابك كمي حقيقي (بدلًا من ارتباط كلاسيكي)؟</li></ul>

          <h4>تحدٍ إضافي</h4>
          <p>أضف قياس أساس Y (باستخدام <code>qc.sdg(q); qc.h(q)</code> قبل القياس) لإكمال مجموعة قياسات كافية لتصوير مقطعي أكثر اكتمالًا.</p>

        </div>
      </details>

      <!-- Project 6 -->
      <details class="lesson" data-lesson="qbronze-p6">
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">P6</span>
          <span class="lesson-title">مشروع 6 — تنفيذ الانتقال الآني الكمي (Teleportation)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="project-meta">
            <span class="project-tag">Qiskit</span>
            <span class="project-tag">مبني على: قسم 19، 21 من QBronze</span>
          </div>

          <h4>الهدف</h4>
          <p>بناء بروتوكول الانتقال الآني الكامل ونقل حالة كيوبت عشوائية من Alice إلى Bob، والتحقق من نجاح النقل.</p>

          <h4>المكونات: Alice وBob وQubit المراد نقله</h4>
          <ul>
            <li><code>q0</code>: الحالة المجهولة المراد نقلها (تخص Alice).</li>
            <li><code>q1</code>: نصف زوج Bell (تخص Alice).</li>
            <li><code>q2</code>: النصف الآخر من زوج Bell (يخص Bob، بعيدًا فيزيائيًا).</li>
          </ul>

          <h4>خطوات البروتوكول</h4>
          <ol>
            <li>تحضير <code>q0</code> بحالة عشوائية عبر <code>RY</code> بزاوية عشوائية.</li>
            <li>بناء زوج Bell بين <code>q1</code> و<code>q2</code>.</li>
            <li>Alice تطبّق <code>CNOT(q0,q1)</code> ثم <code>H(q0)</code>.</li>
            <li>Alice تقيس <code>q0</code> و<code>q1</code> (اتصال كلاسيكي لاحقًا).</li>
            <li>Bob يطبّق <code>X</code> إذا كان قياس <code>q1</code>=1، و<code>Z</code> إذا كان قياس <code>q0</code>=1.</li>
          </ol>

          <h4>الدائرة الكمية والتنفيذ باستخدام Qiskit</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator
from math import pi

qc = QuantumCircuit(3, 3)

qc.ry(pi/5, 0)          # حالة عشوائية على q0 (نصها معروف هنا للتحقق فقط)

qc.h(1); qc.cx(1, 2)     # زوج Bell بين q1 وq2

qc.cx(0, 1); qc.h(0)      # عمليات Alice
qc.measure([0, 1], [0, 1])

qc.cx(1, 2)                # تصحيح Bob الشرطي (مكافئ لـ classically-controlled X)
qc.cz(0, 2)                 # تصحيح Bob الشرطي (مكافئ لـ classically-controlled Z)

qc.measure(2, 2)

counts = AerSimulator().run(qc, shots=2000).result().get_counts()
print(counts)
          </div>

          <h4>تحليل النتيجة</h4>
          <p>احتمال قياس <code>q2</code>=1 في النتيجة النهائية يجب أن يقارب <code>sin²(π/10)</code> — أي نفس احتمال الحالة الأصلية على <code>q0</code>، رغم أن Bob لم يتفاعل مباشرة مع الكيوبت الأصلي إطلاقًا. هذا هو التحقق العملي من نجاح النقل.</p>

          <div class="callout warn"><strong>ملاحظة تصميم:</strong> استخدام <code>cx</code> و<code>cz</code> الشرطيين هنا بديل مكافئ (يعمل بنفس النتيجة إحصائيًا) لاستخدام بوابات X/Z محكومة كلاسيكيًا (classically-controlled) بعد القياس المباشر، وهو أسلوب شائع عند التحقق بالمحاكاة.</div>

          <h4>لماذا لا يخالف هذا سرعة الضوء؟</h4>
          <p>خطوتا التصحيح الشرطي تعتمدان على نتيجتي قياس Alice، والتي يجب إرسالها إلى Bob عبر قناة كلاسيكية (بسرعة الضوء كحد أقصى). بدون هذه المعلومة الكلاسيكية، حالة <code>q2</code> عند Bob تبدو عشوائية تمامًا ولا تحمل أي معلومة قابلة للاستخدام.</p>

          <h4>أسئلة تدريبية</h4>
          <ul><li>ماذا يحدث للنتيجة إذا حذفنا خطوة تصحيح Bob بالكامل؟</li></ul>

          <h4>تحدٍ إضافي</h4>
          <p>وسّع البروتوكول لنقل حالة كيوبت ذات سعات مركّبة (استخدم <code>U</code> بدل <code>RY</code>) وتحقق من النقل باستخدام <code>Statevector</code> بدل القياس الإحصائي.</p>

        </div>
      </details>

      <!-- Project 7 -->
      <details class="lesson" data-lesson="qbronze-p7">
        <summary>
          <span class="lesson-check" data-check></span>
          <span class="lesson-index">P7</span>
          <span class="lesson-title">مشروع 7 — الاتصال عبر الترميز فائق الكثافة (Superdense Coding)</span>
          <span class="lesson-caret">⌄</span>
        </summary>
        <div class="lesson-body">

          <div class="project-meta">
            <span class="project-tag">Qiskit</span>
            <span class="project-tag">مبني على: قسم 19، 20 من QBronze</span>
          </div>

          <h4>الهدف</h4>
          <p>بناء بروتوكول كامل يرسل بموجبه Alice رسالة من بتين كلاسيكيين إلى Bob، بإرسال كيوبت واحد فقط، معتمدة على زوج تشابك مُشترك مسبقًا.</p>

          <h4>الفكرة</h4>
          <p>Alice وBob يتشاركان زوج Bell. تُرمّز Alice رسالتها (00، 01، 10، أو 11) بتطبيق إحدى أربع بوابات على كيوبتها فقط، ثم ترسل ذلك الكيوبت إلى Bob، الذي يفك الترميز بتطبيق CNOT وH ثم القياس.</p>

          <h4>Encoding عند Alice</h4>
          <div class="code-box math">
00 → I     01 → X     10 → Z     11 → X ثم Z
          </div>

          <h4>الدائرة الكمية الكاملة</h4>
          <div class="code-box">
            <button class="code-copy" data-copy>نسخ</button>
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator

def superdense_coding(bits):
    qc = QuantumCircuit(2, 2)

    qc.h(0); qc.cx(0, 1)      # زوج Bell مشترك (المورد المطلوب مسبقًا)

    # ---- Encoding عند Alice على كيوبتها (q0) فقط ----
    if bits == "01":
        qc.x(0)
    elif bits == "10":
        qc.z(0)
    elif bits == "11":
        qc.x(0); qc.z(0)
    # bits == "00" → لا شيء (Identity)

    # ---- إرسال q0 إلى Bob (خطوة فيزيائية، هنا ضمنية) ----

    # ---- Decoding عند Bob ----
    qc.cx(0, 1)
    qc.h(0)
    qc.measure([0, 1], [0, 1])
    return qc

for message in ["00", "01", "10", "11"]:
    qc = superdense_coding(message)
    counts = AerSimulator().run(qc, shots=1000).result().get_counts()
    print(f"الرسالة المرسلة: {message} → النتيجة المُستقبلة: {counts}")
          </div>

          <h4>شرح الكود</h4>
          <p>خطوة Encoding تُطبَّق فقط على كيوبت Alice (<code>q0</code>)، ولا تلمس كيوبت Bob (<code>q1</code>) إطلاقًا — ومع ذلك فإن معلومة الرسالة تنتقل بالكامل بمجرد إرسال هذا الكيوبت الواحد، لأن كيوبت Bob كان متشابكًا معه مسبقًا. خطوة Decoding تعكس عمليتي CNOT وH المستخدمتين في بناء زوج Bell أصلًا، فتحوّل كل رسالة إلى نمط قياس مختلف تمامًا.</p>

          <h4>النتائج المتوقعة</h4>
          <div class="table-scroll">
          <table class="mini-table">
            <thead><tr><th>الرسالة المرسلة</th><th>نتيجة القياس المتوقعة (~100%)</th></tr></thead>
            <tbody>
              <tr><td><code>00</code></td><td><code>00</code></td></tr>
              <tr><td><code>01</code></td><td><code>01</code></td></tr>
              <tr><td><code>10</code></td><td><code>10</code></td></tr>
              <tr><td><code>11</code></td><td><code>11</code></td></tr>
            </tbody>
          </table>
          </div>

          <h4>لماذا يكفي كيوبت واحد وزوج تشابك؟</h4>
          <p>زوج Bell المشترك مسبقًا يحمل بالفعل "نصف" المعلومة الهيكلية اللازمة للتفريق بين الحالات الأربع. تطبيق إحدى البوابات الأربع على كيوبت Alice فقط ينقل النظام المشترك بأكمله إلى واحدة من أربع حالات Bell متعامدة تمامًا، وهذه الحالات الأربع قابلة للتمييز الكامل عند القياس المشترك — رغم أن الكيوبت المُرسَل فعليًا واحد فقط.</p>

          <h4>أسئلة تدريبية</h4>
          <ul>
            <li>ماذا يحدث للنتيجة إذا لم يُبنَ زوج Bell أصلًا (حذفنا <code>h(0);cx(0,1)</code> الأولى)؟</li>
            <li>لماذا لا يمكن لـAlice إرسال بتين كلاسيكيين بكيوبت واحد <strong>بدون</strong> تشابك مسبق مع Bob؟</li>
          </ul>

          <h4>تحدٍ إضافي</h4>
          <p>قارن هذا المشروع بالمشروع السادس (Teleportation): كلاهما يستخدم زوج Bell، لكن أحدهما ينقل كيوبتًا كاملًا ببتين كلاسيكيين، والآخر ينقل بتين كلاسيكيين بكيوبت واحد. اشرح كتابيًا لماذا يُنظر إليهما أحيانًا كبروتوكولين "متكاملين" (Dual Protocols).</p>

        </div>
      </details>

    </div>

    <div class="stage-transition glass reveal">
      <p>
        بهذا تكون قد أنهيت QBronze بالكامل: من البت الكلاسيكي إلى الكيوبت،
        من التراكب إلى التشابك، ومن Bell إلى الانتقال الآني والترميز فائق
        الكثافة، مرورًا بسبعة مشاريع تطبيقية كاملة. القسم التالي (QSilver)
        محفوظ كما هو دون أي تعديل، وينقلك من هذه الأساسيات إلى الطور
        وتحويل فورييه الكمومي (QFT) — تعقيده O(n^2) بوابات في الدائرة القياسية، ويُستخدم كعنصر فرعي في QPE وشور وخوارزمية شور.
      </p>
    </div>

  </div>
</section>


<!-- =========================================================
     STAGE 5 — QSILVER — ملخص الخوارزميات الكمومية
     ملاحظة: هذا القسم ملخص للمراجعة وليس بديلاً عن المادة الأصلية.
     (مراجعة الكود: هذا القسم كان يستخدم كلاسات .stage-section /
     .stage-header / .stage-badge الخاصة به، وقد تحققنا أنها كانت
     مطابقة تمامًا لكلاسات .section / .section-head / .eyebrow.amber
     الموجودة أصلاً في الصفحة، لذلك تم توحيدها لاستخدام نفس الكلاسات
     المشتركة دون أي تغيير في الشكل النهائي.)
========================================================= -->

<section id="qsilver" class="section">

  <div class="container">

    <div class="section-head reveal">
      <span class="eyebrow amber">القسم 5 · QSilver</span>
      <h2> الخوارزميات الكمومية</h2>
      <p>
         مركز لأهم أفكار المرحلة الفضية: التداخل، الطور،
        كرة بلوخ، تحويل فورييه الكمومي (QFT) — تعقيده O(n^2) بوابات في الدائرة القياسية، ويُستخدم كعنصر فرعي في QPE وشور، تقدير الطور الكمومي (QPE) — يقدّر الطور φ لمؤثر وحدوي U حيث U|ψ⟩=e^(2πiφ)|ψ⟩، ومنه يمكن استنتاج القيمة الذاتية λ=e^(2πiφ)، إيجاد المرتبة،
        وخوارزمية شور، مع أمثلة قصيرة للمراجعة.
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
            التداخل والطور: كيف تتحكم الحوسبة الكمومية في الاحتمالات؟
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف الملخص:</strong>
            فهم لماذا تُعد السعة والطور والتداخل عناصر أساسية
            في الخوارزميات الكمومية.
          </div>

          <h4>مراجعة الكيوبت</h4>

          <p>
            تمثل حالة كيوبت واحد بصورة عامة:
          </p>

          <div class="code-box math">
|ψ⟩ = α|0⟩ + β|1⟩

|α|² + |β|² = 1
          </div>

          <p>
            تمثل <code>|α|²</code> و<code>|β|²</code> احتمالي الحصول
            على <code>0</code> أو <code>1</code> عند القياس.
          </p>

          <h4>التداخل الكمومي</h4>

          <p>
            السعات الكمومية يمكن أن تتداخل. قد يكون التداخل
            <strong>بنّاءً</strong> فيزيد سعة بعض النتائج،
            أو <strong>هدّامًا</strong> فيقلل سعة نتائج أخرى.
            لذلك لا تعني الحوسبة الكمومية مجرد وجود حالات كثيرة،
            بل تعتمد على التحكم في السعات والطور.
          </p>

          <div class="code-box math">
تداخل بنّاء  → زيادة السعة
تداخل هدّام   → تقليل السعة
          </div>

          <h4>الطور</h4>

          <p>
            الطور الكلي لا يغير نتائج القياس:
          </p>

          <div class="code-box math">
|ψ⟩  و  e^(iφ)|ψ⟩
          </div>

          <p>
            بينما <strong>الطور النسبي</strong> بين مكونات الحالة
            يمكن أن يؤثر في التداخل، وبالتالي في نتائج الخوارزمية.
          </p>

          <h4>موقع الحوسبة الكمومية اليوم</h4>

          <p>
            الأجهزة الحالية تتأثر بالضوضاء والأخطاء وفقدان الترابط،
            لذلك ما زالت الخوارزميات العملية محدودة مقارنة بما
            تصفه النماذج النظرية. ويُستخدم النموذج الهجين في كثير
            من التطبيقات، حيث يتعاون المعالج الكلاسيكي مع المعالج الكمومي.
          </p>

          <h4>التعقيد: P وNP وBQP</h4>

          <div class="table-scroll">
          <table class="mini-table">
            <thead>
              <tr>
                <th>الفئة</th>
                <th>الفكرة المختصرة</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td><code>P</code></td>
                <td>مسائل يمكن حلها بكفاءة بخوارزميات كلاسيكية حتمية.</td>
              </tr>
              <tr>
                <td><code>NP</code></td>
                <td>مسائل يمكن التحقق من صحة حلها بكفاءة.</td>
              </tr>
              <tr>
                <td><code>BQP</code></td>
                <td>مسائل يمكن حلها بكفاءة بواسطة حاسوب كمومي مع احتمال خطأ محدود.</td>
              </tr>
            </tbody>
          </table>
          </div>

          <div class="callout gold">
            <strong>ملاحظة مهمة:</strong>
            لا يصح وصف BQP ببساطة بأنها "بين P وNP"؛ العلاقات الدقيقة
            بين فئات التعقيد الكمومية والكلاسيكية موضوع رياضي أعمق.
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
            كرة بلوخ وتحويل فورييه الكمومي (QFT) — تعقيده O(n^2) بوابات في الدائرة القياسية، ويُستخدم كعنصر فرعي في QPE وشور: من الهندسة إلى QFT
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف الملخص:</strong>
            ربط الطور بتمثيل الكيوبت على كرة بلوخ، ثم فهم الفكرة
            الأساسية لـ DFT وQFT.
          </div>

          <h4>كرة بلوخ — Bloch Sphere</h4>

          <p>
            يمكن تمثيل أي حالة نقية لكيوبت واحد على كرة بلوخ:
          </p>

          <div class="code-box math">
|ψ⟩ = cos(θ/2)|0⟩ + e^(iφ) sin(θ/2)|1⟩  (مع تجاهل الطور العالمي)
          </div>

          <ul>
            <li><code>θ</code>: تحدد الموقع بالنسبة لمحور Z.</li>
            <li><code>φ</code>: تمثل الطور النسبي حول محور Z.</li>
          </ul>

          <p>
            تستخدم البوابات الدورانية مثل <code>RX</code> و<code>RY</code>
            و<code>RZ</code> لتغيير اتجاه الحالة على الكرة.
          </p>

          <h4>الأنظمة متعددة الكيوبتات</h4>

          <p>
            عند دمج كيوبتين أو أكثر نستخدم الضرب التنسوري:
          </p>

          <div class="code-box math">
|ψ⟩ = |ψ₁⟩ ⊗ |ψ₂⟩

|0⟩ ⊗ |1⟩ = |01⟩
          </div>

          <p>
            يزداد بُعد فضاء الحالة إلى <code>2ⁿ</code> لعدد
            <code>n</code> من الكيوبتات.
          </p>

          <h4>DFT — تحويل فورييه المتقطع</h4>

          <p>
            يحول DFT التمثيل من المجال الأصلي إلى تمثيل يعتمد على
            مكونات التردد. ومن الصيغ الشائعة:
          </p>

          <div class="code-box math">
Xₖ = (1/√N) Σₙ xₙ e^(-2πikn/N)
          </div>

          <div class="callout gold">
            <strong>تنبيه:</strong>
            توجد اتفاقيات مختلفة لتطبيع DFT وإشارة الأس في المراجع.
            المهم معرفة الاتفاقية المستخدمة في الحساب أو الكتاب.
          </div>

          <h4>QFT — تحويل فورييه الكمومي (QFT) — تعقيده O(n^2) بوابات في الدائرة القياسية، ويُستخدم كعنصر فرعي في QPE وشور</h4>

          <p>
            يعمل QFT على سعات الحالة الكمومية. إذا كان
            <code>N = 2ⁿ</code>:
          </p>

          <div class="code-box math">
QFT|x⟩ =
(1/√N) Σᵧ e^(2πixy/N)|y⟩
          </div>

          <p>
            الفكرة المهمة للمراجعة: QFT يحول البنية المرتبطة بالطور
            والدورية إلى تمثيل يمكن استخدامه مع القياس لاستخراج معلومات
            مفيدة في خوارزميات مثل QPE وشور.
          </p>

          <h4>فكرة دائرة QFT</h4>

          <div class="code-box math">
Hadamard
   ↓
Controlled-Phase
   ↓
Hadamard
   ↓
Controlled-Phase
   ↓
Swap
          </div>

          <p>
            الدائرة الفعلية تعتمد على عدد الكيوبتات، ويُستخدم
            <strong>Inverse QFT</strong> في الاتجاه العكسي عند الحاجة
            إلى استخراج معلومات الطور، كما في QPE.
          </p>

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
            تقدير الطور الكمومي (QPE) — يقدّر الطور φ لمؤثر وحدوي U حيث U|ψ⟩=e^(2πiφ)|ψ⟩، ومنه يمكن استنتاج القيمة الذاتية λ=e^(2πiφ) الكمومي (QPE) وإيجاد المرتبة
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف الملخص:</strong>
            فهم العلاقة بين القيم الذاتية والطور، ثم معرفة كيف تستخدم
            QPE لاستخراج الطور، ولماذا يرتبط ذلك بمشكلة Order Finding.
          </div>

          <h4>القيمة الذاتية والطور</h4>

          <p>
            إذا كان <code>|ψ⟩</code> متجهًا ذاتيًا لمؤثر وحدوي <code>U</code>:
          </p>

          <div class="code-box math">
U|ψ⟩ = e^(2πiφ)|ψ⟩
          </div>

          <p>
            هنا <code>φ</code> هو <strong>Eigenphase</strong> الذي تحاول
            خوارزمية QPE تقديره.
          </p>

          <h4>QPE — Quantum Phase Estimation</h4>

          <p>
            الفكرة المختصرة:
          </p>

          <div class="code-box math">
Control Register
      ↓
Superposition
      ↓
Controlled-U, U², U⁴, ...
      ↓
Phase Information
      ↓
Inverse QFT
      ↓
Measurement
          </div>

          <p>
            الهدف هو تحويل معلومات الطور الموجودة في السعات إلى قيمة
            ثنائية تقريبية يمكن الحصول عليها من القياس.
          </p>

          <h4>مثال مبسط</h4>

          <p>
            إذا كان الطور له تمثيل ثنائي منتهٍ مثل:
          </p>

          <div class="code-box math">
φ = 0.11₂ = 3/4
          </div>

          <p>
            فإن سجل التحكم يمكنه، في الحالة المثالية المناسبة، تمثيل
            القيمة <code>11</code> بعد تطبيق Inverse QFT والقياس.
          </p>

          <div class="callout gold">
            <strong>الفكرة:</strong>
            QPE لا "تقيس الطور مباشرة"، بل تستخدم التداخل وInverse QFT
            لتحويل معلومات الطور إلى نمط قياس قابل للقراءة.
          </div>

          <h4>Order Finding</h4>

          <p>
            المطلوب إيجاد أصغر عدد صحيح موجب <code>r</code> يحقق:
          </p>

          <div class="code-box math">
aʳ ≡ 1 (mod N)
          </div>

          <p>
            ويشترط عادةً في اختيار <code>a</code> أن:
          </p>

          <div class="code-box math">
gcd(a, N) = 1
          </div>

          <h4>مثال: N = 15</h4>

          <div class="code-box math">
a = 2

2¹ mod 15 = 2
2² mod 15 = 4
2³ mod 15 = 8
2⁴ mod 15 = 1

إذن r = 4
          </div>

          <p>
            هذه الدورية هي المعلومة التي تستفيد منها خوارزمية شور
            للوصول إلى عوامل العدد.
          </p>

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
            خوارزمية شور: من إيجاد المرتبة إلى تحليل الأعداد
          </span>
          <span class="lesson-caret">⌄</span>
        </summary>

        <div class="lesson-body">

          <div class="callout">
            <strong>هدف الملخص:</strong>
            جمع QFT وQPE وOrder Finding داخل الصورة العامة لخوارزمية شور،
            مع معرفة الحالات التي تحتاج إلى إعادة المحاولة.
          </div>

          <h4>ما المشكلة التي تحلها شور؟</h4>

          <p>
            خوارزمية شور هي خوارزمية كمومية لتحليل عدد صحيح
            إلى عوامله الأولية بكفاءة نظرية، وتعتمد على إيجاد دورية
            دالة الأسّ المتكرر:
          </p>

          <div class="code-box math">
f(x) = aˣ mod N
          </div>

          <h4>المسار المختصر للخوارزمية</h4>

          <ul class="step-flow">
            <li>اختيار العدد <code>N</code> المراد تحليله.</li>
            <li>اختيار <code>a</code> بحيث <code>1 &lt; a &lt; N</code>.</li>
            <li>حساب <code>gcd(a,N)</code>.</li>
            <li>إذا كان <code>gcd(a,N) ≠ 1</code> فقد حصلنا على عامل غير تافه مباشرة.</li>
            <li>إيجاد المرتبة <code>r</code> باستخدام الجزء الكمومي.</li>
            <li>إذا كان <code>r</code> فرديًا، نعيد المحاولة باختيار <code>a</code> آخر.</li>
            <li>إذا كان <code>a^(r/2) ≡ -1 (mod N)</code>، قد لا نحصل على عامل مفيد ونعيد المحاولة.</li>
            <li>استخدام GCD لاستخراج العوامل.</li>
          </ul>

          <h4>مثال تعليمي: تحليل 15</h4>

          <div class="code-box math">
N = 15
a = 2
r = 4

a^(r/2) = 2² = 4

gcd(4 − 1, 15) = 3
gcd(4 + 1, 15) = 5

15 = 3 × 5
          </div>

          <h4>أين يوجد الجزء الكمومي؟</h4>

          <div class="code-box math">
Modular Exponentiation
        ↓
Periodic Information
        ↓
Quantum Phase Estimation / QFT
        ↓
Measurement
        ↓
Classical Post-Processing
        ↓
Order r
        ↓
GCD
        ↓
Factors
          </div>

          <p>
            الجزء الكمومي يساعد على استخراج المعلومات الدورية،
            بينما توجد خطوات كلاسيكية مهمة لمعالجة النتيجة واستخراج العوامل.
          </p>

          <h4>ما الذي يجب أن تتذكره؟</h4>

          <div class="callout success">
            <strong>الخلاصة:</strong>
            قوة هذه السلسلة من الخوارزميات لا تأتي من "وجود حالات كثيرة"
            وحده، وإنما من التحكم في التراكب والطور والتداخل لاستخراج
            بنية رياضية مفيدة من المشكلة.
          </div>

          <div class="code-box math">
QFT
 ↓
QPE
 ↓
Order Finding
 ↓
Shor
          </div>

          <h4>مراجعة سريعة قبل الاختبار</h4>

          <ul>
            <li>ما الفرق بين Global Phase وRelative Phase؟</li>
            <li>ما الذي تمثله θ وφ في Bloch Sphere؟</li>
            <li>لماذا نستخدم Inverse QFT في QPE؟</li>
            <li>ما تعريف Order <code>r</code>؟</li>
            <li>لماذا نحتاج <code>gcd(a,N)=1</code> في المسار المعتاد لشور؟</li>
            <li>ماذا يحدث إذا كان <code>r</code> فرديًا؟</li>
            <li>ما دور الجزء الكمومي وما دور المعالجة الكلاسيكية في شور؟</li>
          </ul>

          <div class="callout gold">
            <strong>للتطبيق:</strong>
            هذا الملخص يثبت المفاهيم الأساسية، أما بناء الدوائر وتنفيذ
            QFT وQPE وشور باستخدام Qiskit فيحتاج الرجوع إلى الدروس العملية
            والتمارين الأصلية.
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
          <span>التداخل والطور</span>
          <p>كيف يؤثر الطور والتداخل في احتمالات نتائج القياس.</p>
        </div>

        <div class="summary-card">
          <strong>02</strong>
          <span>Bloch Sphere</span>
          <p>تمثيل حالة كيوبت واحد وفهم θ وφ.</p>
        </div>

        <div class="summary-card">
          <strong>03</strong>
          <span>QFT</span>
          <p>تحويل فورييه الكمومي (QFT) — تعقيده O(n^2) بوابات في الدائرة القياسية، ويُستخدم كعنصر فرعي في QPE وشور وعلاقته بالبنية الدورية.</p>
        </div>

        <div class="summary-card">
          <strong>04</strong>
          <span>QPE</span>
          <p>تقدير الطور الكمومي (QPE) — يقدّر الطور φ لمؤثر وحدوي U حيث U|ψ⟩=e^(2πiφ)|ψ⟩، ومنه يمكن استنتاج القيمة الذاتية λ=e^(2πiφ) المرتبط بالقيمة الذاتية لمؤثر وحدوي.</p>
        </div>

        <div class="summary-card">
          <strong>05</strong>
          <span>Order Finding</span>
          <p>إيجاد أصغر r يحقق aʳ ≡ 1 (mod N).</p>
        </div>

        <div class="summary-card">
          <strong>06</strong>
          <span>Shor's Algorithm</span>
          <p>استخدام المعلومات الدورية للوصول إلى عوامل العدد.</p>
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
      <span class="eyebrow purple">مرجع سريع</span>
      <h2>الرموز والبوابات والأكواد في لمحة</h2>
      <p>للمراجعة السريعة قبل الاختبار أو أثناء كتابة الكود، عبر المراحل الثلاث.</p>
    </div>

    <div class="ref-grid reveal">

      <div class="glass" style="padding:22px">
        <h3 style="font-family:var(--font-display);font-size:16px;margin-bottom:12px;color:var(--cyan)">بايثون وNumPy (QPrep)</h3>
        <div class="table-scroll">
        <table class="mini-table">
          <thead><tr><th>المفهوم</th><th>الكود</th></tr></thead>
          <tbody>
            <tr><td>طول أي بنية</td><td><code>len(x)</code></td></tr>
            <tr><td>حلقة for</td><td><code>for i in range(n):</code></td></tr>
            <tr><td>دالة</td><td><code>def f(x): return x**2</code></td></tr>
            <tr><td>متجه NumPy</td><td><code>np.array([a, b])</code></td></tr>
            <tr><td>ضرب مصفوفة في متجه</td><td><code>M @ v</code></td></tr>
            <tr><td>الجداء التنسوري</td><td><code>np.kron(u, v)</code></td></tr>
            <tr><td>طول المتجه (Norm)</td><td><code>np.linalg.norm(v)</code></td></tr>
          </tbody>
        </table>
        </div>
      </div>

      <div class="glass" style="padding:22px">
        <h3 style="font-family:var(--font-display);font-size:16px;margin-bottom:12px;color:var(--cyan)">البوابات وQiskit (QBronze)</h3>
        <div class="table-scroll">
        <table class="mini-table">
          <thead><tr><th>المفهوم</th><th>Qiskit</th></tr></thead>
          <tbody>
            <tr><td>حالة الصفر</td><td><code>QuantumCircuit(1)</code></td></tr>
            <tr><td>Pauli-X</td><td><code>qc.x(0)</code></td></tr>
            <tr><td>Hadamard</td><td><code>qc.h(0)</code></td></tr>
            <tr><td>Pauli-Z</td><td><code>qc.z(0)</code></td></tr>
            <tr><td>دوران Y</td><td><code>qc.ry(theta, 0)</code></td></tr>
            <tr><td>CNOT</td><td><code>qc.cx(c, t)</code></td></tr>
            <tr><td>Toffoli</td><td><code>qc.ccx(c1, c2, t)</code></td></tr>
            <tr><td>قياس</td><td><code>qc.measure(q, c)</code></td></tr>
            <tr><td>تشغيل على محاكي</td><td><code>AerSimulator().run(qc, shots=1000)</code></td></tr>
          </tbody>
        </table>
        </div>
      </div>

    </div>

    <div class="glass reveal" style="padding:22px;margin-top:20px">
      <h3 style="font-family:var(--font-display);font-size:16px;margin-bottom:12px;color:var(--cyan)">أهم القواعد للحفظ</h3>
      <ul style="padding-inline-start:18px;list-style:disc;color:var(--text-dim);font-size:14px;line-height:2">
        <li>الاحتمال ليس هو السعة الكمية: <code>P = |amplitude|²</code>.</li>
        <li>شرط تطبيع الكيوبت: <code>|α|² + |β|² = 1</code>.</li>
        <li>زوايا Python وQiskit المثلثية بالراديان، والحالة <code>cos(φ)|0⟩+sin(φ)|1⟩</code> تحتاج <code>RY(2φ)</code>.</li>
        <li>للمصفوفة الوحدوية: <code>U†U = I</code>، وضرب المصفوفات ليس تبادليًا عمومًا: <code>AB ≠ BA</code>.</li>
        <li>لـ<code>n</code> كيوبتات، بُعد فضاء الحالة هو <code>2ⁿ</code>، وQiskit تستخدم Little-Endian في عرض النتائج.</li>
        <li>التشابك لا يعني إرسال معلومات أسرع من الضوء — الانتقال الآني والترميز فائق الكثافة يحتاجان دائمًا اتصالًا كلاسيكيًا مصاحبًا.</li>
        <li><code>U|ψ⟩ = e^(2πiφ)|ψ⟩</code> — الطور φ هو ما تقدّره خوارزمية QPE، وخوارزمية شور تحوّل التحليل إلى مشكلة إيجاد المرتبة <code>aʳ ≡ 1 (mod N)</code>.</li>
      </ul>
    </div>

  </div>
</section>


<!-- =========================================================
     PROGRESS
========================================================= -->
<section class="section" id="progress-section">

  <div class="container">

    <div class="section-head reveal">
      <span class="eyebrow green">نظام التقدم</span>
      <h2>تقدّمك في الرحلة</h2>
      <p>يُحفظ تقدمك تلقائيًا، ويمكن تحديد الدروس والمشاريع المكتملة من داخل كل قسم.</p>
    </div>

    <div class="progress-panel glass reveal">

      <div class="progress-detail">

        <h3>ملخص الإنجاز</h3>
        <p id="progressSummaryText">عدد الدروس المكتملة من الإجمالي، موزعة على 3 مراحل.</p>

        <div class="progress-rows">

          <div class="progress-row">
            <div class="row-top"><b>QPrep</b><span id="rowQprep">0 / 14</span></div>
            <div class="path-progress-track"><div class="path-progress-fill" id="rowFillQprep" style="width:0%"></div></div>
          </div>

          <div class="progress-row">
            <div class="row-top"><b>QBronze (دروس ومشاريع)</b><span id="rowQbronze">0 / 30</span></div>
            <div class="path-progress-track"><div class="path-progress-fill" id="rowFillQbronze" style="width:0%"></div></div>
          </div>

          <div class="progress-row">
            <div class="row-top"><b>QSilver</b><span id="rowQsilver">0 / 4</span></div>
            <div class="path-progress-track"><div class="path-progress-fill" id="rowFillQsilver" style="width:0%"></div></div>
          </div>

        </div>

        <div class="progress-actions">
          <a href="#qprep" class="btn btn-primary btn-sm">متابعة الدروس</a>
          <button class="btn btn-ghost btn-sm" id="resetProgress">إعادة تعيين التقدم</button>
        </div>

      </div>

      <div class="progress-ring-wrap">
        <svg width="210" height="210" viewBox="0 0 220 220" role="img" aria-label="نسبة التقدم الإجمالية">
          <circle cx="110" cy="110" r="92" fill="none" stroke="rgba(255,255,255,0.06)" stroke-width="16" />
          <circle id="ringFill" cx="110" cy="110" r="92" fill="none" stroke="url(#ringGrad)" stroke-width="16"
            stroke-linecap="round" stroke-dasharray="578" stroke-dashoffset="578"
            transform="rotate(-90 110 110)" style="transition:stroke-dashoffset .7s var(--ease)" />
          <defs>
            <linearGradient id="ringGrad" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#2dd4ff" />
              <stop offset="55%" stop-color="#9b6bff" />
              <stop offset="100%" stop-color="#34e0a1" />
            </linearGradient>
          </defs>
        </svg>
        <div class="progress-ring-label">
          <b id="ringPct">0%</b>
          <span id="ringSub">0 من 48 درسًا</span>
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
      <nav class="footer-links" aria-label="روابط الفوتر">
        <a href="#home">الرئيسية</a><a href="#qprep">QPrep</a><a href="#qbronze">QBronze</a>
        <a href="#qbronze-projects">مشاريع QBronze</a><a href="#qsilver">QSilver</a><a href="#reference">مرجع سريع</a>
      </nav>
    </div>
    <p class="footer-note">محتوى تعليمي مبني على منهج QWorld — QPrep &amp; QBronze &amp; QSilver. الدوائر الكمية هنا توضيحية بغرض التعلّم، وتحتاج بيئة Qiskit فعلية للتشغيل الحقيقي.</p>
  </div>
</footer>

<script>
(function(){
  "use strict";

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
      navToggle.setAttribute('aria-label', isOpen ? 'إغلاق القائمة' : 'فتح القائمة');
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
        if(navToggle){
          navToggle.classList.remove('open');
          navToggle.setAttribute('aria-expanded','false');
          navToggle.setAttribute('aria-label','فتح القائمة');
        }
        if(mobileMenu){
          mobileMenu.setAttribute('inert','');
          mobileMenu.querySelectorAll('a').forEach(function(x){ x.setAttribute('tabindex','-1'); });
        }
      });
    });
  } catch(e){}

  try {
    var navLinks = document.querySelectorAll('[data-nav]');
    var sectionIds = ['home','qprep','qbronze','qsilver','reference'];
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
    function setActiveFromHash(){
      var id = (location.hash || '#home').slice(1);
      if(sectionIds.indexOf(id) !== -1) setActive(id);
    }
    window.addEventListener('hashchange', setActiveFromHash);
    setActiveFromHash();
  } catch(e){}

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
  } catch(e){}

  try {
    if(typeof IntersectionObserver === 'function'){
      var revealObserver = new IntersectionObserver(function(entries){
        entries.forEach(function(entry){
          if(entry.isIntersecting){ entry.target.classList.add('is-visible'); revealObserver.unobserve(entry.target); }
        });
      }, { threshold: 0.12 });
      document.querySelectorAll('.reveal').forEach(function(el){ revealObserver.observe(el); });
    }
  } catch(e){}

  try {
    document.querySelectorAll('.code-box:not(.math)').forEach(function(box){
      var btn = box.querySelector('.code-copy');
      if(!btn) return;
      btn.addEventListener('click', function(e){
        e.preventDefault(); e.stopPropagation();
        var clone = box.cloneNode(true);
        var cloneBtn = clone.querySelector('.code-copy');
        if(cloneBtn) cloneBtn.remove();
        var text = clone.textContent.trim();
        if(navigator.clipboard && navigator.clipboard.writeText){
          navigator.clipboard.writeText(text).then(function(){
            var original = btn.textContent;
            btn.textContent = 'تم النسخ!'; btn.classList.add('copied');
            setTimeout(function(){ btn.textContent = original; btn.classList.remove('copied'); }, 1800);
          }).catch(function(){});
        }
      });
    });
  } catch(e){}

  var STORAGE_KEY = 'quantum_curriculum_progress_v1';
  var hasClaudeStorage = (typeof window.storage !== 'undefined');
  var memoryStore = null;

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
    qprep:   allLessons.filter(function(id){ return id.indexOf('qprep-') === 0; }),
    qbronze: allLessons.filter(function(id){ return id.indexOf('qbronze-') === 0; }),
    qsilver: allLessons.filter(function(id){ return id.indexOf('qsilver-') === 0; })
  };
  var totalCount = allLessons.length;
  var totalSections = Object.keys(groups).length;
  var completed = [];

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
    qprep:   { fill:'fillQprep',   pct:'pctQprep',   status:'statusQprep',   row:'rowQprep',   rowFill:'rowFillQprep' },
    qbronze: { fill:'fillQbronze', pct:'pctQbronze', status:'statusQbronze', row:'rowQbronze', rowFill:'rowFillQbronze' },
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
        summaryEl.textContent = 'عدد الدروس المكتملة من إجمالي ' + totalCount + ' درسًا ومشروعًا موزعة على ' + totalSections + ' مراحل.';
      }
    } catch(e){}
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

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Narendaran M | Full-Stack Engineer</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Noto+Sans+JP:wght@500;700;900&family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">

<style>
:root{
  --ink:#0B0B0E;
  --ink-soft:#17171C;
  --paper:#F4EEE0;
  --paper-dim:#E9E0CC;
  --red:#E63E2E;
  --red-dark:#A8281B;
  --cyan:#26D3E0;
  --gold:#F2B705;
  --line-on-paper: rgba(11,11,14,.16);
  --line-on-ink: rgba(244,238,224,.16);
  --text-on-paper: #17171C;
  --text-on-paper-dim: #55524A;
  --text-on-ink: #F4EEE0;
  --text-on-ink-dim: #A9A597;
}
*{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{
  font-family:'Inter',sans-serif;
  background:var(--paper);
  color:var(--text-on-paper);
  overflow-x:hidden;
}
@media (prefers-reduced-motion: reduce){
  *{animation-duration:.001ms !important; animation-iteration-count:1 !important; transition-duration:.001ms !important; scroll-behavior:auto !important;}
}
::-webkit-scrollbar{width:8px;}
::-webkit-scrollbar-track{background:var(--paper-dim);}
::-webkit-scrollbar-thumb{background:var(--ink);border:2px solid var(--paper-dim);}
a{color:inherit;}
:focus-visible{outline:3px solid var(--red); outline-offset:2px;}

.jp{font-family:'Noto Sans JP',sans-serif;}

/* halftone dot texture */
.halftone{
  background-image: radial-gradient(currentColor 1px, transparent 1.4px);
  background-size: 7px 7px;
}

/* ═══ LOADER ═══ */
#loader{
  position:fixed;inset:0;background:var(--ink);
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  z-index:10000; transition:opacity .5s ease, visibility .5s ease;
}
#loader.hidden{opacity:0;visibility:hidden;}
.loader-mark{
  font-family:'Anton',sans-serif; font-size:64px; color:var(--paper);
  letter-spacing:2px; position:relative;
}
.loader-mark::after{
  content:'';position:absolute;left:0;bottom:-6px;height:6px;width:100%;
  background:var(--red);
  animation: loadSweep 1.1s ease-in-out infinite;
}
@keyframes loadSweep{0%,100%{transform:scaleX(.15);transform-origin:left;}50%{transform:scaleX(1);transform-origin:left;}}
.loader-sub{margin-top:18px;font-family:'JetBrains Mono',monospace;font-size:11px;letter-spacing:5px;color:var(--cyan);text-transform:uppercase;}

/* ═══ NAV ═══ */
.nav{
  position:fixed;top:0;left:0;right:0;z-index:1000;
  padding:18px 50px;display:flex;align-items:center;justify-content:space-between;
  background:var(--paper); border-bottom:3px solid var(--ink);
  transition: padding .3s ease;
}
.nav-logo{
  display:flex;align-items:center;gap:10px;text-decoration:none;
}
.hanko{
  width:34px;height:34px;background:var(--red);color:var(--paper);
  display:flex;align-items:center;justify-content:center;
  font-family:'Anton',sans-serif;font-size:17px;border:2px solid var(--ink);
  transform:rotate(-4deg);
}
.nav-logo-text{font-family:'Anton',sans-serif;font-size:19px;letter-spacing:1px;color:var(--ink);}
.nav-links{display:flex;gap:6px;list-style:none;}
.nav-links a{
  padding:8px 14px; text-decoration:none;color:var(--ink);
  font-size:13px;font-weight:700;letter-spacing:.5px;text-transform:uppercase;
  border:2px solid transparent; transition:all .2s ease;
}
.nav-links a:hover{border-color:var(--ink);background:var(--ink);color:var(--paper);}
.nav-cta{
  padding:10px 22px;background:var(--ink);color:var(--paper);
  font-size:12px;font-weight:800;letter-spacing:1px;text-transform:uppercase;
  text-decoration:none;border:2px solid var(--ink);position:relative;
}
.nav-cta:hover{background:var(--red);border-color:var(--red);}
.menu-toggle{display:none;flex-direction:column;gap:5px;cursor:pointer;padding:6px;}
.menu-toggle span{width:24px;height:3px;background:var(--ink);}

/* ═══ BASE SECTION ═══ */
section{position:relative;z-index:1;}
.section-container{max-width:1280px;margin:0 auto;padding:0 50px;}
.eyebrow{
  display:inline-flex;align-items:center;gap:12px;
  font-family:'JetBrains Mono',monospace;font-size:12px;letter-spacing:4px;
  text-transform:uppercase;margin-bottom:16px;color:var(--red);font-weight:700;
}
.eyebrow .bar{width:34px;height:3px;background:var(--red);}
.section-title{
  font-family:'Anton',sans-serif;font-size:clamp(34px,5vw,58px);
  line-height:1.02;letter-spacing:.5px;text-transform:uppercase;margin-bottom:8px;
}
.section-title .mark{color:var(--red);}
.section-sub-jp{font-family:'Noto Sans JP',sans-serif;font-weight:700;color:var(--text-on-paper-dim);font-size:14px;margin-bottom:36px;}
.panel-divider{
  height:14px;width:100%;
  background: repeating-linear-gradient(-45deg, var(--ink), var(--ink) 10px, var(--paper) 10px, var(--paper) 20px);
  border-top:3px solid var(--ink);border-bottom:3px solid var(--ink);
}

/* reveal */
.reveal{opacity:0;transform:translateY(30px);transition:all .6s cubic-bezier(.16,1,.3,1);}
.reveal.active{opacity:1;transform:translateY(0);}
.reveal-scale{opacity:0;transform:scale(.94);transition:all .6s cubic-bezier(.16,1,.3,1);}
.reveal-scale.active{opacity:1;transform:scale(1);}

/* ═══ HERO ═══ */
.hero{
  min-height:100vh;display:flex;align-items:center;position:relative;overflow:hidden;
  background:var(--ink); color:var(--text-on-ink); padding-top:90px;
}
.hero::before{
  content:'';position:absolute;inset:0;color:var(--text-on-ink-dim);opacity:.25;
  background-image: radial-gradient(currentColor 1.4px, transparent 1.6px);
  background-size:16px 16px;
  mask-image: radial-gradient(circle at 78% 35%, black 0%, transparent 62%);
}
.speedlines{position:absolute;inset:0;pointer-events:none;opacity:.5;}
.hero-grid{
  display:grid;grid-template-columns:1.15fr .85fr;gap:40px;align-items:center;
  position:relative;z-index:2;
}
.hero-tag{
  display:inline-flex;align-items:center;gap:10px;padding:7px 16px;
  background:var(--red);color:var(--paper);
  font-family:'JetBrains Mono',monospace;font-size:11px;font-weight:700;
  letter-spacing:2px;text-transform:uppercase;margin-bottom:26px;
  clip-path: polygon(0 0, 100% 0, 96% 100%, 4% 100%);
}
.hero-tag .pulse{width:7px;height:7px;background:var(--paper);border-radius:50%;animation:pulse 1.6s infinite;}
@keyframes pulse{0%,100%{opacity:1;}50%{opacity:.3;}}
.hero-title{
  font-family:'Anton',sans-serif; text-transform:uppercase;
  font-size:clamp(46px,7.5vw,92px); line-height:.98; letter-spacing:.5px;
  -webkit-text-stroke: 1.5px var(--ink);
  text-shadow: 5px 5px 0 var(--red), 9px 9px 0 var(--ink);
}
.hero-role-jp{font-family:'Noto Sans JP',sans-serif;font-weight:700;color:var(--cyan);font-size:16px;letter-spacing:3px;margin:18px 0 6px;}
.hero-role{
  font-family:'JetBrains Mono',monospace;font-size:20px;font-weight:700;color:var(--paper);
  min-height:28px;
}
.hero-role .cursor-bar{display:inline-block;width:11px;height:20px;background:var(--red);vertical-align:middle;margin-left:2px;animation:blink 1s step-end infinite;}
@keyframes blink{50%{opacity:0;}}
.hero-subtitle{
  font-size:16px;color:var(--text-on-ink-dim);max-width:540px;line-height:1.75;
  margin:26px 0 36px; padding-left:16px; border-left:3px solid var(--cyan);
}
.hero-buttons{display:flex;gap:16px;flex-wrap:wrap;}
.btn-primary{
  padding:16px 32px;background:var(--red);color:var(--paper);
  font-family:'Inter',sans-serif;font-size:13px;font-weight:800;letter-spacing:1px;
  text-transform:uppercase;border:2px solid var(--ink);cursor:pointer;
  text-decoration:none;display:inline-flex;align-items:center;gap:10px;
  box-shadow:5px 5px 0 var(--paper); transition:transform .15s ease, box-shadow .15s ease;
}
.btn-primary:hover{transform:translate(3px,3px);box-shadow:2px 2px 0 var(--paper);}
.btn-secondary{
  padding:16px 32px;background:transparent;color:var(--paper);
  font-family:'Inter',sans-serif;font-size:13px;font-weight:800;letter-spacing:1px;
  text-transform:uppercase;border:2px solid var(--paper);cursor:pointer;
  text-decoration:none;display:inline-flex;align-items:center;gap:10px;
  transition: all .2s ease;
}
.btn-secondary:hover{background:var(--paper);color:var(--ink);}

/* hero status card */
.hero-status{
  background:var(--ink-soft); border:2px solid var(--text-on-ink-dim);
  padding:22px; position:relative;
}
.hero-status::before,.hero-status::after,.status-corner-tl,.status-corner-br{content:'';position:absolute;width:16px;height:16px;border:2px solid var(--cyan);}
.hero-status::before{top:-2px;left:-2px;border-right:none;border-bottom:none;}
.hero-status::after{bottom:-2px;right:-2px;border-left:none;border-top:none;}
.status-head{display:flex;justify-content:space-between;align-items:baseline;border-bottom:2px dashed var(--text-on-ink-dim);padding-bottom:12px;margin-bottom:16px;}
.status-head .label{font-family:'JetBrains Mono',monospace;font-size:11px;letter-spacing:3px;color:var(--cyan);}
.status-head .lv{font-family:'Anton',sans-serif;font-size:22px;color:var(--gold);}
.status-row{margin-bottom:14px;}
.status-row-top{display:flex;justify-content:space-between;font-family:'JetBrains Mono',monospace;font-size:12px;margin-bottom:6px;color:var(--text-on-ink-dim);}
.status-row-top b{color:var(--paper);}
.status-bar{height:9px;background:rgba(255,255,255,.08);border:1px solid var(--text-on-ink-dim);position:relative;overflow:hidden;}
.status-bar-fill{height:100%;background:linear-gradient(90deg,var(--red),var(--cyan));}

.scroll-indicator{
  position:absolute;bottom:32px;left:50%;transform:translateX(-50%);
  display:flex;flex-direction:column;align-items:center;gap:8px;z-index:2;
}
.scroll-indicator span{font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:4px;text-transform:uppercase;color:var(--text-on-ink-dim);}
.scroll-chevron{font-size:14px;color:var(--red);animation:chevBounce 1.6s ease-in-out infinite;}
@keyframes chevBounce{0%,100%{transform:translateY(0);}50%{transform:translateY(8px);}}

/* ═══ ABOUT ═══ */
.about{padding:110px 0;}
.about-grid{display:grid;grid-template-columns:.85fr 1.15fr;gap:60px;align-items:center;}
.about-panel{position:relative;border:3px solid var(--ink);}
.about-panel img{width:100%;height:480px;object-fit:cover;display:block;filter:grayscale(1) contrast(1.15);}
.about-panel .duotone{position:absolute;inset:0;background:linear-gradient(160deg, rgba(230,62,46,.55), rgba(38,211,224,.4));mix-blend-mode:color;}
.about-panel .halftone-edge{position:absolute;bottom:0;right:0;width:120px;height:120px;color:var(--ink);opacity:.5;}
.about-badge{
  position:absolute;bottom:-22px;right:-22px;background:var(--ink);color:var(--paper);
  border:3px solid var(--red);padding:16px 20px;transform:rotate(-3deg);
}
.about-badge .num{font-family:'Anton',sans-serif;font-size:40px;line-height:1;color:var(--gold);}
.about-badge .txt{font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:1px;text-transform:uppercase;margin-top:4px;color:var(--text-on-ink-dim);}
.about-text p{font-size:16px;line-height:1.85;color:var(--text-on-paper-dim);margin-bottom:20px;}
.about-quote{
  padding:20px 24px;background:var(--ink);color:var(--paper);
  border-left:5px solid var(--red);margin:26px 0;font-weight:600;font-size:16px;
  position:relative;
}
.about-quote::before{content:'"';font-family:'Anton',sans-serif;color:var(--red);font-size:30px;margin-right:4px;}
.about-highlights{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-top:28px;}
.highlight-item{
  display:flex;align-items:center;gap:12px;padding:14px;background:var(--paper-dim);
  border:2px solid var(--ink); transition:transform .2s ease;
}
.highlight-item:hover{transform:translate(-3px,-3px);box-shadow:4px 4px 0 var(--red);}
.highlight-icon{
  width:38px;height:38px;display:flex;align-items:center;justify-content:center;
  background:var(--ink);color:var(--paper);font-size:15px;flex-shrink:0;
}
.highlight-text{font-size:12.5px;color:var(--text-on-paper-dim);}
.highlight-text strong{color:var(--ink);display:block;margin-bottom:2px;font-size:13.5px;}

/* ═══ SKILLS — STATUS WINDOW ═══ */
.skills{padding:110px 0;background:var(--ink);color:var(--text-on-ink);}
.skills .eyebrow{color:var(--cyan);}
.skills .eyebrow .bar{background:var(--cyan);}
.status-window{
  border:2px solid var(--text-on-ink-dim); margin-top:20px; position:relative;
  background:var(--ink-soft);
}
.status-window-top{
  display:flex;justify-content:space-between;align-items:center;
  padding:16px 26px;border-bottom:2px solid var(--text-on-ink-dim);
  font-family:'JetBrains Mono',monospace;
}
.status-window-top .sw-name{font-size:15px;font-weight:700;color:var(--paper);}
.status-window-top .sw-lv{color:var(--gold);font-weight:700;}
.sw-grid{display:grid;grid-template-columns:1fr 1fr;}
.sw-stat{padding:26px; border-bottom:1px solid rgba(255,255,255,.08);}
.sw-stat:nth-child(odd){border-right:1px solid rgba(255,255,255,.08);}
.sw-stat-head{display:flex;align-items:center;gap:12px;margin-bottom:12px;}
.sw-stat-icon{width:36px;height:36px;display:flex;align-items:center;justify-content:center;background:rgba(255,255,255,.06);border:1px solid var(--text-on-ink-dim);color:var(--cyan);font-size:15px;}
.sw-stat-name{font-family:'Anton',sans-serif;font-size:16px;letter-spacing:.5px;text-transform:uppercase;}
.sw-stat-jp{font-family:'Noto Sans JP',sans-serif;font-size:10px;color:var(--text-on-ink-dim);}
.sw-bar-row{display:flex;align-items:center;gap:12px;margin-bottom:14px;}
.sw-bar-track{flex:1;height:8px;background:rgba(255,255,255,.08);position:relative;overflow:hidden;}
.sw-bar-fill{height:100%;background:linear-gradient(90deg,var(--red),var(--gold));transform-origin:left;transform:scaleX(0);transition:transform 1.1s cubic-bezier(.16,1,.3,1);}
.sw-bar-fill.filled{transform:scaleX(1);}
.sw-bar-pct{font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--text-on-ink-dim);width:34px;text-align:right;}
.sw-tags{display:flex;flex-wrap:wrap;gap:7px;}
.sw-tag{
  padding:5px 10px;background:rgba(38,211,224,.08);border:1px solid rgba(38,211,224,.35);
  font-family:'JetBrains Mono',monospace;font-size:11px;color:var(--cyan);
}

/* ═══ PROJECTS — CHAPTERS ═══ */
.projects{padding:110px 0;}
.chapter{border:3px solid var(--ink);margin-bottom:34px;position:relative;}
.chapter-num{
  position:absolute;top:-18px;left:26px;background:var(--red);color:var(--paper);
  font-family:'Anton',sans-serif;font-size:14px;padding:6px 16px;letter-spacing:1px;
  border:2px solid var(--ink);
}
.chapter-grid{display:grid;grid-template-columns:1fr 1fr;}
.chapter.featured .chapter-grid{grid-template-columns:1.1fr .9fr;}
.chapter-image{position:relative;overflow:hidden;min-height:280px;border-right:3px solid var(--ink);}
.chapter-image img{width:100%;height:100%;object-fit:cover;filter:grayscale(.5) contrast(1.1);position:absolute;inset:0;}
.chapter-image .duotone{position:absolute;inset:0;background:linear-gradient(200deg, rgba(230,62,46,.5), rgba(38,211,224,.35));mix-blend-mode:color;}
.chapter-featured-badge{
  position:absolute;top:16px;right:16px;z-index:2;background:var(--gold);color:var(--ink);
  padding:6px 14px;font-family:'JetBrains Mono',monospace;font-size:11px;font-weight:800;
  letter-spacing:1px;text-transform:uppercase;border:2px solid var(--ink);
}
.chapter-content{padding:38px 34px;display:flex;flex-direction:column;justify-content:center;}
.chapter-title{
  font-family:'Anton',sans-serif;font-size:24px;text-transform:uppercase;
  display:flex;align-items:center;gap:12px;margin-bottom:12px;
}
.chapter-title i{color:var(--red);font-size:19px;}
.chapter-desc{font-size:14.5px;color:var(--text-on-paper-dim);line-height:1.75;margin-bottom:20px;}
.chapter-tech{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:24px;}
.chapter-tech span{
  padding:5px 11px;background:var(--paper-dim);border:1px solid var(--ink);
  font-family:'JetBrains Mono',monospace;font-size:11px;
}
.chapter-links{display:flex;gap:14px;flex-wrap:wrap;}
.chapter-link{
  display:inline-flex;align-items:center;gap:8px;padding:10px 18px;font-size:12.5px;
  font-weight:800;text-decoration:none;border:2px solid var(--ink);text-transform:uppercase;
  letter-spacing:.5px; transition:all .2s ease;
}
.chapter-link.primary{background:var(--ink);color:var(--paper);}
.chapter-link.primary:hover{background:var(--red);border-color:var(--red);}
.chapter-link.secondary{background:transparent;color:var(--ink);}
.chapter-link.secondary:hover{background:var(--ink);color:var(--paper);}
.projects-cta{text-align:center;margin-top:10px;}

@media (max-width:900px){
  .chapter-grid, .chapter.featured .chapter-grid{grid-template-columns:1fr;}
  .chapter-image{border-right:none;border-bottom:3px solid var(--ink);min-height:220px;}
}

/* ═══ LEETCODE — BATTLE RECORD ═══ */
.record{padding:110px 0;background:var(--ink);color:var(--text-on-ink);}
.record .eyebrow{color:var(--gold);}
.record .eyebrow .bar{background:var(--gold);}
.record-container{display:grid;grid-template-columns:1fr 1fr;gap:30px;margin-top:20px;}
.record-card{border:2px solid var(--text-on-ink-dim);padding:24px;background:var(--ink-soft);}
.record-card img{max-width:100%;border:1px solid rgba(255,255,255,.1);}
.enemy-log{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;margin-top:36px;}
.enemy{
  border:2px solid var(--text-on-ink-dim); padding:26px 18px; text-align:center;
  background:var(--ink-soft); position:relative; transition:transform .2s ease;
}
.enemy:hover{transform:translateY(-6px);}
.enemy .tier{font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:2px;text-transform:uppercase;color:var(--text-on-ink-dim);margin-bottom:10px;}
.enemy .count{font-family:'Anton',sans-serif;font-size:38px;line-height:1;}
.enemy.grunt .count{color:var(--cyan);}
.enemy.elite .count{color:var(--gold);}
.enemy.boss .count{color:var(--red);}
.enemy .name{font-size:12px;color:var(--text-on-ink-dim);margin-top:8px;text-transform:uppercase;letter-spacing:1px;}
.record-cta{text-align:center;margin-top:40px;}
.btn-gold{
  padding:16px 34px;background:var(--gold);color:var(--ink);
  font-family:'Inter',sans-serif;font-size:13px;font-weight:800;letter-spacing:1px;
  text-transform:uppercase;border:2px solid var(--ink);cursor:pointer;
  text-decoration:none;display:inline-flex;align-items:center;gap:10px;
  box-shadow:5px 5px 0 var(--paper); transition:all .15s ease;
}
.btn-gold:hover{transform:translate(3px,3px);box-shadow:2px 2px 0 var(--paper);}

@media (max-width:900px){
  .record-container{grid-template-columns:1fr;}
}

/* ═══ CONTACT ═══ */
.contact{padding:110px 0;}
.contact-grid{display:grid;grid-template-columns:1fr 1fr;gap:60px;margin-top:20px;}
.contact-item{
  display:flex;align-items:flex-start;gap:18px;padding:20px;
  background:var(--paper-dim);border:2px solid var(--ink);margin-bottom:16px;
  transition:transform .2s ease;
}
.contact-item:hover{transform:translate(4px,-4px);box-shadow:-4px 4px 0 var(--red);}
.contact-icon{
  width:44px;height:44px;display:flex;align-items:center;justify-content:center;
  background:var(--ink);color:var(--paper);font-size:17px;flex-shrink:0;
}
.contact-item h4{font-family:'Anton',sans-serif;font-size:15px;letter-spacing:.5px;text-transform:uppercase;margin-bottom:4px;}
.contact-item p{font-size:13.5px;color:var(--text-on-paper-dim);}
.contact-item a{text-decoration:none;color:var(--red);font-weight:600;}
.contact-form{display:flex;flex-direction:column;gap:16px;position:relative;}
.speech-tip{
  font-family:'JetBrains Mono',monospace;font-size:11px;letter-spacing:2px;color:var(--red);
  text-transform:uppercase;margin-bottom:6px;
}
.form-group input,.form-group textarea{
  width:100%;padding:16px 18px;background:var(--paper);border:2px solid var(--ink);
  color:var(--ink);font-family:'Inter',sans-serif;font-size:14.5px;outline:none;
  transition:box-shadow .2s ease;
}
.form-group input:focus,.form-group textarea:focus{box-shadow:4px 4px 0 var(--cyan);}
.form-group textarea{min-height:140px;resize:vertical;}
.form-submit{
  padding:17px 34px;background:var(--red);color:var(--paper);
  font-family:'Inter',sans-serif;font-size:14px;font-weight:800;letter-spacing:1px;
  text-transform:uppercase;border:2px solid var(--ink);cursor:pointer;
  display:inline-flex;align-items:center;justify-content:center;gap:10px;
  box-shadow:5px 5px 0 var(--ink); transition:all .15s ease;
}
.form-submit:hover{transform:translate(3px,3px);box-shadow:2px 2px 0 var(--ink);}

/* ═══ FOOTER ═══ */
.footer{padding:44px 0;background:var(--ink);color:var(--text-on-ink-dim);border-top:3px solid var(--red);}
.footer-content{display:flex;justify-content:space-between;align-items:center;}
.footer-text span{color:var(--paper);font-weight:700;}
.footer-socials{display:flex;gap:12px;}
.footer-social{
  width:40px;height:40px;display:flex;align-items:center;justify-content:center;
  background:var(--ink-soft);border:1px solid var(--text-on-ink-dim);color:var(--text-on-ink-dim);
  text-decoration:none;transition:all .2s ease;
}
.footer-social:hover{border-color:var(--red);color:var(--red);}

/* ═══ RESPONSIVE ═══ */
@media (max-width:1024px){
  .hero-grid{grid-template-columns:1fr;}
  .hero-status{max-width:420px;}
  .skills-grid,.sw-grid{grid-template-columns:1fr;}
  .sw-stat:nth-child(odd){border-right:none;}
}
@media (max-width:768px){
  .nav{padding:14px 22px;}
  .nav-links{display:none;}
  .menu-toggle{display:flex;}
  .section-container{padding:0 22px;}
  .about-grid,.contact-grid{grid-template-columns:1fr;gap:36px;}
  .about-highlights{grid-template-columns:1fr;}
  .enemy-log{gap:10px;}
  .footer-content{flex-direction:column;gap:20px;text-align:center;}
}
</style>
</head>
<body>

<div id="loader">
  <div class="loader-mark">NAREN</div>
  <div class="loader-sub">LOADING CHAPTER</div>
</div>

<nav class="nav" id="nav">
  <a href="#" class="nav-logo">
    <span class="hanko">那</span>
    <span class="nav-logo-text">NAREN.DEV</span>
  </a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#skills">Status</a></li>
    <li><a href="#projects">Chapters</a></li>
    <li><a href="#record">Record</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="#contact" class="nav-cta">Let's Talk</a>
  <div class="menu-toggle" id="menuToggle"><span></span><span></span><span></span></div>
</nav>

<!-- HERO -->
<section class="hero" id="hero">
  <svg class="speedlines" viewBox="0 0 1000 800" preserveAspectRatio="none" aria-hidden="true">
    <g stroke="#26D3E0" stroke-width="1" opacity="0.35">
      <line x1="1000" y1="60" x2="500" y2="120"/>
      <line x1="1000" y1="110" x2="480" y2="180"/>
      <line x1="1000" y1="160" x2="520" y2="240"/>
      <line x1="1000" y1="210" x2="470" y2="300"/>
      <line x1="1000" y1="260" x2="510" y2="360"/>
    </g>
    <g stroke="#E63E2E" stroke-width="1.5" opacity="0.25">
      <line x1="1000" y1="330" x2="440" y2="420"/>
      <line x1="1000" y1="390" x2="460" y2="480"/>
      <line x1="1000" y1="450" x2="430" y2="540"/>
    </g>
  </svg>
  <div class="section-container">
    <div class="hero-grid">
      <div class="hero-content">
        <div class="hero-tag reveal"><span class="pulse"></span>Available for opportunities</div>
        <h1 class="hero-title reveal">Narendaran</h1>
        <div class="hero-role-jp reveal">フルスタックエンジニア</div>
        <div class="hero-role reveal" id="typedRole">Full-Stack Engineer<span class="cursor-bar"></span></div>
        <p class="hero-subtitle reveal">
          I deeply understand a problem before writing a single line — then ship something that holds up in production. Architecting resilient systems with clean code.
        </p>
        <div class="hero-buttons reveal">
          <a href="#projects" class="btn-primary"><i class="fas fa-book-open"></i> Read Chapters</a>
          <a href="#contact" class="btn-secondary"><i class="fas fa-envelope"></i> Get in Touch</a>
        </div>
      </div>

      <div class="hero-status reveal-scale">
        <div class="status-head">
          <span class="label">STATUS WINDOW</span>
          <span class="lv">LV. 99</span>
        </div>
        <div class="status-row">
          <div class="status-row-top"><span>CLASS</span><b>Full-Stack Engineer</b></div>
        </div>
        <div class="status-row">
          <div class="status-row-top"><span>PROBLEMS CLEARED</span><b>315</b></div>
        </div>
        <div class="status-row">
          <div class="status-row-top"><span>POWER — BACKEND</span><b>92%</b></div>
          <div class="status-bar"><div class="status-bar-fill" style="width:92%"></div></div>
        </div>
        <div class="status-row">
          <div class="status-row-top"><span>POWER — FRONTEND</span><b>85%</b></div>
          <div class="status-bar"><div class="status-bar-fill" style="width:85%"></div></div>
        </div>
        <div class="status-row">
          <div class="status-row-top"><span>POWER — SECURITY</span><b>80%</b></div>
          <div class="status-bar"><div class="status-bar-fill" style="width:80%"></div></div>
        </div>
      </div>
    </div>
  </div>
  <div class="scroll-indicator">
    <span>Scroll</span>
    <i class="fas fa-chevron-down scroll-chevron"></i>
  </div>
</section>

<div class="panel-divider"></div>

<!-- ABOUT -->
<section class="about" id="about">
  <div class="section-container">
    <div class="about-grid">
      <div class="about-panel reveal">
        <img src="https://picsum.photos/seed/naren-dev/600/500.jpg" alt="Narendaran M">
        <div class="duotone"></div>
        <div class="about-badge">
          <div class="num">30+</div>
          <div class="txt">Projects Cleared</div>
        </div>
      </div>
      <div class="about-text reveal">
        <div class="eyebrow"><span class="bar"></span>Profile — 経歴</div>
        <h2 class="section-title">Building <span class="mark">Resilient</span> Systems</h2>
        <p>
          I'm a full-stack engineer who deeply understands a problem before writing a single line — then ships something that holds up in production. My work spans web platforms, mobile apps, applied cryptography, and lightweight AI tooling.
        </p>
        <div class="about-quote">I'd rather rebuild it from scratch than patch it.</div>
        <p>
          Currently building an AI-assisted incident management platform and deepening my expertise in applied cryptography, NLP, and system design.
        </p>
        <div class="about-highlights">
          <div class="highlight-item"><div class="highlight-icon"><i class="fas fa-code"></i></div><div class="highlight-text"><strong>Clean Code</strong>Production-grade standards</div></div>
          <div class="highlight-item"><div class="highlight-icon"><i class="fas fa-shield-halved"></i></div><div class="highlight-text"><strong>Security</strong>Cryptography & Auth</div></div>
          <div class="highlight-item"><div class="highlight-icon"><i class="fas fa-brain"></i></div><div class="highlight-text"><strong>AI/ML</strong>NLP & Applied AI</div></div>
          <div class="highlight-item"><div class="highlight-icon"><i class="fas fa-server"></i></div><div class="highlight-text"><strong>Systems</strong>Scalable Architecture</div></div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="panel-divider"></div>

<!-- SKILLS — STATUS WINDOW -->
<section class="skills" id="skills">
  <div class="section-container">
    <div class="eyebrow reveal"><span class="bar"></span>Ability Sheet — 技術</div>
    <h2 class="section-title reveal">Skill <span class="mark">Tree</span></h2>

    <div class="status-window reveal">
      <div class="status-window-top">
        <span class="sw-name">NARENDARAN_M.status</span>
        <span class="sw-lv">EQUIPPED SKILLS</span>
      </div>
      <div class="sw-grid">
        <div class="sw-stat">
          <div class="sw-stat-head">
            <div class="sw-stat-icon"><i class="fab fa-react"></i></div>
            <div><div class="sw-stat-name">Frontend</div><div class="sw-stat-jp">フロントエンド</div></div>
          </div>
          <div class="sw-bar-row"><div class="sw-bar-track"><div class="sw-bar-fill" data-pct="85"></div></div><span class="sw-bar-pct">85</span></div>
          <div class="sw-tags">
            <span class="sw-tag">React / Next.js</span><span class="sw-tag">Flutter</span>
            <span class="sw-tag">Tailwind CSS</span><span class="sw-tag">Redux</span><span class="sw-tag">Socket.io</span>
          </div>
        </div>
        <div class="sw-stat">
          <div class="sw-stat-head">
            <div class="sw-stat-icon"><i class="fab fa-node-js"></i></div>
            <div><div class="sw-stat-name">Backend</div><div class="sw-stat-jp">バックエンド</div></div>
          </div>
          <div class="sw-bar-row"><div class="sw-bar-track"><div class="sw-bar-fill" data-pct="92"></div></div><span class="sw-bar-pct">92</span></div>
          <div class="sw-tags">
            <span class="sw-tag">Node.js / Express</span><span class="sw-tag">Python / Flask</span>
            <span class="sw-tag">Django / FastAPI</span><span class="sw-tag">REST APIs</span><span class="sw-tag">GraphQL</span>
          </div>
        </div>
        <div class="sw-stat">
          <div class="sw-stat-head">
            <div class="sw-stat-icon"><i class="fas fa-database"></i></div>
            <div><div class="sw-stat-name">Data & Infra</div><div class="sw-stat-jp">インフラ</div></div>
          </div>
          <div class="sw-bar-row"><div class="sw-bar-track"><div class="sw-bar-fill" data-pct="75"></div></div><span class="sw-bar-pct">75</span></div>
          <div class="sw-tags">
            <span class="sw-tag">MongoDB</span><span class="sw-tag">PostgreSQL</span>
            <span class="sw-tag">Redis</span><span class="sw-tag">Docker</span><span class="sw-tag">GCP / Vercel</span>
          </div>
        </div>
        <div class="sw-stat">
          <div class="sw-stat-head">
            <div class="sw-stat-icon"><i class="fas fa-lock"></i></div>
            <div><div class="sw-stat-name">Specialized</div><div class="sw-stat-jp">特殊技能</div></div>
          </div>
          <div class="sw-bar-row"><div class="sw-bar-track"><div class="sw-bar-fill" data-pct="80"></div></div><span class="sw-bar-pct">80</span></div>
          <div class="sw-tags">
            <span class="sw-tag">JWT / OAuth 2.0</span><span class="sw-tag">Cryptography</span>
            <span class="sw-tag">NLP</span><span class="sw-tag">scikit-learn</span><span class="sw-tag">Git / CI/CD</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="panel-divider"></div>

<!-- PROJECTS — CHAPTERS -->
<section class="projects" id="projects">
  <div class="section-container">
    <div class="eyebrow reveal"><span class="bar"></span>Works — 代表作</div>
    <h2 class="section-title reveal">Chapters I've <span class="mark">Written</span></h2>

    <div class="chapter featured reveal-scale">
      <span class="chapter-num">CHAPTER 01</span>
      <div class="chapter-grid">
        <div class="chapter-image">
          <img src="https://picsum.photos/seed/ai-devops/1200/500.jpg" alt="AI DevOps Incident Management">
          <div class="duotone"></div>
          <span class="chapter-featured-badge">Featured</span>
        </div>
        <div class="chapter-content">
          <h3 class="chapter-title"><i class="fas fa-robot"></i>AI DevOps Incident Management</h3>
          <p class="chapter-desc">Full-stack incident management platform with AI-assisted severity classification, live dashboards, and complete lifecycle tracking. Deployed and live in production.</p>
          <div class="chapter-tech"><span>React</span><span>Flask</span><span>PostgreSQL</span><span>JWT</span><span>AI/NLP</span></div>
          <div class="chapter-links">
            <a href="https://github.com/NAREN-105/AI-DevOps-Incident-Management" class="chapter-link primary" target="_blank"><i class="fab fa-github"></i> Source Code</a>
            <a href="https://ai-dev-ops-incident-management.vercel.app" class="chapter-link secondary" target="_blank"><i class="fas fa-external-link-alt"></i> Live Demo</a>
          </div>
        </div>
      </div>
    </div>

    <div class="chapter reveal-scale">
      <span class="chapter-num">CHAPTER 02</span>
      <div class="chapter-grid">
        <div class="chapter-image">
          <img src="https://picsum.photos/seed/chatbot-nlp/700/500.jpg" alt="Final Review Chatbot">
          <div class="duotone"></div>
        </div>
        <div class="chapter-content">
          <h3 class="chapter-title"><i class="fas fa-comments"></i>Final Review Chatbot</h3>
          <p class="chapter-desc">Document Q&A chatbot with a custom NLP pipeline — zero ML models, zero external APIs, 91% accuracy. Auto-generates presentation slides.</p>
          <div class="chapter-tech"><span>Python</span><span>NLP</span><span>Tkinter</span></div>
          <div class="chapter-links">
            <a href="https://github.com/NAREN-105/FINAL_REVIEW_CHATBOT" class="chapter-link primary" target="_blank"><i class="fab fa-github"></i> View Repo</a>
          </div>
        </div>
      </div>
    </div>

    <div class="chapter reveal-scale">
      <span class="chapter-num">CHAPTER 03</span>
      <div class="chapter-grid">
        <div class="chapter-image">
          <img src="https://picsum.photos/seed/crypto-api/700/500.jpg" alt="Shamir's Secret Sharing API">
          <div class="duotone"></div>
        </div>
        <div class="chapter-content">
          <h3 class="chapter-title"><i class="fas fa-key"></i>Shamir's Secret Sharing API</h3>
          <p class="chapter-desc">Production-style API implementing Shamir's Secret Sharing with mathematical reconstruction via Lagrange interpolation.</p>
          <div class="chapter-tech"><span>JavaScript</span><span>Cryptography</span><span>REST API</span></div>
          <div class="chapter-links">
            <a href="https://github.com/NAREN-105/REST_API_USING_SSS" class="chapter-link primary" target="_blank"><i class="fab fa-github"></i> View Repo</a>
          </div>
        </div>
      </div>
    </div>

    <div class="projects-cta reveal">
      <a href="https://github.com/NAREN-105?tab=repositories" class="btn-secondary" style="color:var(--ink);border-color:var(--ink);" target="_blank"><i class="fab fa-github"></i> View All Repositories</a>
    </div>
  </div>
</section>

<div class="panel-divider"></div>

<!-- LEETCODE — BATTLE RECORD -->
<section class="record" id="record">
  <div class="section-container">
    <div class="eyebrow reveal"><span class="bar"></span>Quest Log — 記録</div>
    <h2 class="section-title reveal">Battle <span class="mark">Record</span></h2>

    <div class="record-container reveal">
      <div class="record-card"><img src="https://leetcode-stats.vercel.app/api?username=NARENDARAN_M&theme=dark&border_radius=4&hide_rank=true" alt="LeetCode Stats"></div>
      <div class="record-card"><img src="https://leetcard.jacoblin.cool/NARENDARAN_M?theme=dark&font=roboto&border_radius=4" alt="LeetCode Card"></div>
    </div>

    <div class="enemy-log reveal">
      <div class="enemy grunt"><div class="tier">Grunts Defeated</div><div class="count">222</div><div class="name">Easy</div></div>
      <div class="enemy elite"><div class="tier">Elites Defeated</div><div class="count">85</div><div class="name">Medium</div></div>
      <div class="enemy boss"><div class="tier">Bosses Defeated</div><div class="count">8</div><div class="name">Hard</div></div>
    </div>

    <div class="record-cta reveal">
      <a href="https://leetcode.com/u/NARENDARAN_M/" class="btn-gold" target="_blank"><i class="fas fa-trophy"></i> View LeetCode Profile</a>
    </div>
  </div>
</section>

<div class="panel-divider"></div>

<!-- CONTACT -->
<section class="contact" id="contact">
  <div class="section-container">
    <div class="eyebrow reveal"><span class="bar"></span>Transmission — 連絡先</div>
    <h2 class="section-title reveal">Let's <span class="mark">Connect</span></h2>

    <div class="contact-grid">
      <div class="contact-info reveal">
        <div class="contact-item"><div class="contact-icon"><i class="fas fa-envelope"></i></div><div><h4>Email</h4><p><a href="mailto:narenrdkn@gmail.com">narenrdkn@gmail.com</a></p></div></div>
        <div class="contact-item"><div class="contact-icon"><i class="fab fa-linkedin"></i></div><div><h4>LinkedIn</h4><p><a href="https://www.linkedin.com/in/narendaran-m-rdknnkdr" target="_blank">Connect with me</a></p></div></div>
        <div class="contact-item"><div class="contact-icon"><i class="fas fa-globe"></i></div><div><h4>Portfolio</h4><p><a href="https://naren-105.github.io" target="_blank">naren-105.github.io</a></p></div></div>
        <div class="contact-item"><div class="contact-icon"><i class="fab fa-dev"></i></div><div><h4>Dev.to</h4><p><a href="https://dev.to/narendaran_m" target="_blank">Read my blogs</a></p></div></div>
      </div>
      <form class="contact-form reveal" id="contactForm">
        <div class="speech-tip">// send a signal</div>
        <div class="form-group"><input type="text" placeholder="Your Name" required></div>
        <div class="form-group"><input type="email" placeholder="Your Email" required></div>
        <div class="form-group"><input type="text" placeholder="Subject"></div>
        <div class="form-group"><textarea placeholder="Your Message" required></textarea></div>
        <button type="submit" class="form-submit"><i class="fas fa-paper-plane"></i> Send Message</button>
      </form>
    </div>
  </div>
</section>

<footer class="footer">
  <div class="section-container">
    <div class="footer-content">
      <div class="footer-text">© 2024 <span>Narendaran M</span>. Built with passion & clean code.</div>
      <div class="footer-socials">
        <a href="https://github.com/NAREN-105" class="footer-social" target="_blank"><i class="fab fa-github"></i></a>
        <a href="https://www.linkedin.com/in/narendaran-m-rdknnkdr" class="footer-social" target="_blank"><i class="fab fa-linkedin"></i></a>
        <a href="https://leetcode.com/u/NARENDARAN_M/" class="footer-social" target="_blank"><i class="fas fa-code"></i></a>
        <a href="https://dev.to/narendaran_m" class="footer-social" target="_blank"><i class="fab fa-dev"></i></a>
        <a href="https://www.instagram.com/__naren_03" class="footer-social" target="_blank"><i class="fab fa-instagram"></i></a>
      </div>
    </div>
  </div>
</footer>

<script>
// LOADER
window.addEventListener('load', () => {
  setTimeout(() => document.getElementById('loader').classList.add('hidden'), 500);
});

// NAV scroll shrink border (kept simple)
const nav = document.getElementById('nav');
window.addEventListener('scroll', () => {
  nav.style.boxShadow = window.scrollY > 40 ? '0 4px 0 rgba(0,0,0,.05)' : 'none';
});

// MOBILE MENU
const menuToggle = document.getElementById('menuToggle');
const navLinks = document.querySelector('.nav-links');
menuToggle.addEventListener('click', () => {
  menuToggle.classList.toggle('active');
  navLinks.style.display = navLinks.style.display === 'flex' ? 'none' : 'flex';
});

// SCROLL REVEAL
const revealEls = document.querySelectorAll('.reveal, .reveal-scale');
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => { if (entry.isIntersecting) entry.target.classList.add('active'); });
}, { threshold: 0.12 });
revealEls.forEach(el => revealObserver.observe(el));

// STATUS BARS fill on view
const bars = document.querySelectorAll('.sw-bar-fill');
const barObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const el = entry.target;
      el.style.width = el.dataset.pct + '%';
      el.classList.add('filled');
    }
  });
}, { threshold: 0.4 });
bars.forEach(b => barObserver.observe(b));

// SMOOTH SCROLL
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function(e) {
    const target = document.querySelector(this.getAttribute('href'));
    if (target) {
      e.preventDefault();
      target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      navLinks.style.display = '';
      menuToggle.classList.remove('active');
    }
  });
});

// CONTACT FORM
document.getElementById('contactForm').addEventListener('submit', (e) => {
  e.preventDefault();
  const btn = e.target.querySelector('.form-submit');
  const original = btn.innerHTML;
  btn.innerHTML = '<i class="fas fa-check"></i> Message Sent!';
  btn.style.background = '#26D3E0';
  setTimeout(() => { btn.innerHTML = original; btn.style.background = ''; e.target.reset(); }, 2500);
});

// TYPED ROLE
const roles = ['Full-Stack Engineer', 'System Designer', 'Problem Solver', 'Security Enthusiast'];
let roleIndex = 0, charIndex = 0, isDeleting = false;
const roleEl = document.getElementById('typedRole');
function typeRole() {
  const current = roles[roleIndex];
  const text = isDeleting ? current.substring(0, charIndex - 1) : current.substring(0, charIndex + 1);
  roleEl.innerHTML = text + '<span class="cursor-bar"></span>';
  charIndex += isDeleting ? -1 : 1;
  let speed = isDeleting ? 45 : 95;
  if (!isDeleting && charIndex === current.length) { speed = 1800; isDeleting = true; }
  else if (isDeleting && charIndex === 0) { isDeleting = false; roleIndex = (roleIndex + 1) % roles.length; speed = 400; }
  setTimeout(typeRole, speed);
}
setTimeout(typeRole, 1200);
</script>
</body>
</html>

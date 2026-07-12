[index.html](https://github.com/user-attachments/files/29943649/index.html)
# spin-kingdom<!DOCTYPE html>
<html lang="ro">
<head>
<!-- skill:chrome -->
<style>
/* Credit line — bottom-right */
.design-ui-credit {
  position: fixed;
  bottom: 12px;
  right: 12px;
  font: 11px/1 system-ui, sans-serif;
  color: rgba(128,128,128,0.5);
  pointer-events: none;
  z-index: 2147483647;
  transition: opacity 0.4s ease;
  user-select: none;
  letter-spacing: 0.02em;
}

/* Hide chrome on touch devices */
@media (hover: none) {
  .design-ui-credit { display: none; }
}

/* Print fixes */
@media print {
  * {
    transition: none !important;
    animation: none !important;
    box-shadow: none !important;
  }
  body {
    print-color-adjust: exact;
    -webkit-print-color-adjust: exact;
  }
  .design-ui-credit { display: none !important; }
}

</style>
<script>
(function () {
    // Design-ui pages are single compositions, so the whole body is editable.
    function markEditable() {
        document.body.classList.add('artifact-editable');
    }

    // Credit badge with idle-fade. Hover devices only.
    function initChromeUI() {
        if (!matchMedia('(hover: hover)').matches) return;

        var credit = document.createElement('div');
        credit.className = 'design-ui-credit';
        credit.setAttribute('aria-hidden', 'true');
        credit.innerHTML = '\u{1F49C} by ClickUp Brain';
        document.body.appendChild(credit);

        var timer = null;
        var fade = function (out) { credit.style.opacity = out ? '0' : ''; };
        fade(true);
        var show = function () {
            fade(false);
            clearTimeout(timer);
            timer = setTimeout(function () { fade(true); }, 3000);
        };
        document.addEventListener('mousemove', show);
        show();
    }

    function init() {
        markEditable();
        initChromeUI();
    }

    if (document.readyState === 'loading') {
        document.addEventListener('DOMContentLoaded', init);
    } else {
        init();
    }
})();

</script>
<!-- /skill:chrome -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="theme-color" content="#1a0d40">
<meta name="mobile-web-app-capable" content="yes">
<title>Spin Kingdom</title>
<link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Lilita+One&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%;overflow:hidden}
body{font-family:'Fredoka',sans-serif;background:#1a0d40;color:#fff;-webkit-tap-highlight-color:transparent;overscroll-behavior:none}
h1,h2,h3{font-family:'Lilita One',cursive}

.app{height:100%;max-width:480px;margin:0 auto;display:flex;flex-direction:column;overflow:hidden;position:relative}

.hud{display:flex;align-items:center;justify-content:space-between;padding:10px 12px 6px;z-index:50;background:linear-gradient(180deg,rgba(26,13,64,0.97),rgba(26,13,64,0.85));backdrop-filter:blur(6px)}
.h-coins{display:flex;align-items:center;gap:4px;padding:5px 12px 5px 6px;background:linear-gradient(90deg,#2e7d32,#388e3c);border-radius:14px;border:2px solid #66bb6a;font-weight:700;font-size:0.85rem;cursor:pointer}
.h-coin-i{width:20px;height:20px;background:radial-gradient(circle at 35% 35%,#fff176,#f9a825);border-radius:50%;border:2px solid #ffee58;font-size:0.5rem;display:flex;align-items:center;justify-content:center}
.h-spins{display:flex;align-items:center;gap:4px;padding:5px 10px 5px 6px;background:linear-gradient(90deg,#4a148c,#6a1b9a);border-radius:14px;border:2px solid #9c27b0;font-size:0.78rem;font-weight:600;color:#e1bee7}
.h-spin-i{width:18px;height:18px;background:linear-gradient(135deg,#ce93d8,#7b1fa2);border-radius:50%;border:1.5px solid #e1bee7}
.h-btn{width:34px;height:34px;border-radius:10px;background:rgba(255,255,255,0.06);border:1.5px solid rgba(255,255,255,0.12);display:flex;align-items:center;justify-content:center;font-size:1rem;cursor:pointer}

.dots{display:flex;justify-content:center;gap:5px;padding:5px 0;background:rgba(26,13,64,0.7)}
.dot{width:7px;height:7px;border-radius:50%;background:rgba(255,255,255,0.12);transition:all 0.3s}
.dot.on{width:22px;border-radius:4px;background:linear-gradient(90deg,#fbbf24,#f97316)}

.pages{flex:1;display:flex;transition:transform 0.35s cubic-bezier(0.16,1,0.3,1);will-change:transform}
.pg{min-width:100%;height:100%;overflow-y:auto;overflow-x:hidden;display:flex;flex-direction:column;-webkit-overflow-scrolling:touch}

/* SPIN PAGE */
.pg-spin{background:linear-gradient(180deg,#4fc3f7 0%,#29b6f6 40%,#81d4fa 100%);position:relative}
.spin-sky{position:absolute;inset:0;pointer-events:none;overflow:hidden}
.spin-cloud{position:absolute;background:rgba(255,255,255,0.5);border-radius:50px;animation:cloudDrift 25s linear infinite}
@keyframes cloudDrift{from{transform:translateX(-150px)}to{transform:translateX(calc(480px + 150px))}}
.spin-top{text-align:center;padding:12px 0 6px;position:relative;z-index:1}
.spin-avatar{font-size:3.5rem;filter:drop-shadow(0 6px 12px rgba(0,0,0,0.2));animation:avatarBob 3s ease-in-out infinite}
@keyframes avatarBob{0%,100%{transform:translateY(0)}50%{transform:translateY(-6px)}}
.spin-name{font-size:0.75rem;color:#0d47a1;font-weight:600;margin-top:2px}
.spin-coins{font-size:0.9rem;font-weight:700;color:#1b5e20}

.slot-wrap{padding:8px 14px;position:relative;z-index:1;flex:1;display:flex;flex-direction:column;justify-content:center}
.slot-machine{background:linear-gradient(145deg,#ef6c00,#e65100);border:4px solid #ffb300;border-radius:22px;padding:14px;box-shadow:0 8px 40px rgba(230,81,0,0.4),inset 0 2px 0 rgba(255,255,255,0.15);position:relative}
.slot-machine::after{content:'';position:absolute;inset:4px;border:2px solid rgba(255,179,0,0.25);border-radius:18px;pointer-events:none}
.sl-header{display:flex;justify-content:space-between;align-items:center;padding:0 4px 8px;font-size:0.72rem;color:#fff;font-weight:600;text-shadow:1px 1px 2px rgba(0,0,0,0.3)}
.sl-reels-wrap{background:#2e1b05;border-radius:14px;padding:10px 8px;border:3px solid #4e342e;box-shadow:inset 0 4px 15px rgba(0,0,0,0.6);margin-bottom:10px}
.sl-reels{display:flex;gap:6px;justify-content:center}
.sl-reel{width:74px;height:74px;background:linear-gradient(180deg,#fffde7,#fff9c4);border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:2.4rem;border:2.5px solid #bcaaa4;box-shadow:inset 0 2px 6px rgba(0,0,0,0.08);position:relative;overflow:hidden}
.sl-reel::before{content:'';position:absolute;top:0;left:0;right:0;height:30%;background:linear-gradient(180deg,rgba(255,255,255,0.5),transparent);pointer-events:none;border-radius:10px 10px 0 0}
.sl-reel.spin .ri{animation:reelSpin 0.06s linear infinite}
.sl-reel.win{border-color:#ffd600;box-shadow:0 0 20px rgba(255,214,0,0.7);animation:winPop 0.5s ease}
@keyframes reelSpin{0%{transform:translateY(-130%);opacity:0}50%{transform:translateY(0);opacity:1}100%{transform:translateY(130%);opacity:0}}
@keyframes winPop{0%,100%{transform:scale(1)}50%{transform:scale(1.1)}}
.sl-spin-btn{display:block;width:100%;padding:15px;border:none;border-radius:16px;background:linear-gradient(180deg,#c62828,#b71c1c);color:#fff;font-family:'Lilita One',cursive;font-size:1.6rem;cursor:pointer;box-shadow:0 5px 20px rgba(198,40,40,0.4),inset 0 2px 0 rgba(255,255,255,0.15);transition:all 0.15s;position:relative;overflow:hidden}
.sl-spin-btn::after{content:'';position:absolute;top:0;left:-100%;width:60%;height:100%;background:linear-gradient(90deg,transparent,rgba(255,255,255,0.12),transparent);animation:shine 3s ease infinite}
@keyframes shine{0%,100%{left:-100%}50%{left:100%}}
.sl-spin-btn:active{transform:scale(0.96)}
.sl-spin-btn:disabled{background:#616161;box-shadow:none}.sl-spin-btn:disabled::after{display:none}
.sl-multi{display:flex;justify-content:center;gap:8px;margin-top:8px}
.ml-btn{padding:5px 14px;border-radius:10px;border:2px solid rgba(255,255,255,0.2);background:rgba(255,255,255,0.08);color:#fff;font-weight:700;font-size:0.72rem;cursor:pointer;font-family:inherit;transition:all 0.15s}
.ml-btn.on{border-color:#ffd600;background:rgba(255,214,0,0.15);color:#ffd600}

/* VILLAGE PAGE */
.pg-village{background:linear-gradient(180deg,#81c784,#66bb6a);position:relative}
.vil-header{text-align:center;padding:12px 10px 8px;position:relative;z-index:2}
.vil-name{font-size:1.1rem;color:#1b5e20;text-shadow:0 1px 2px rgba(255,255,255,0.3)}
.vil-prog{font-size:0.65rem;color:#2e7d32;margin-top:2px}
.vil-bar-wrap{width:55%;height:6px;background:rgba(0,0,0,0.12);border-radius:3px;margin:5px auto 0;overflow:hidden}
.vil-bar-fill{height:100%;background:linear-gradient(90deg,#fdd835,#ff8f00);border-radius:3px;transition:width 0.5s cubic-bezier(0.16,1,0.3,1)}
.vil-scene{flex:1;position:relative;overflow:hidden}
.vil-ground{position:absolute;bottom:0;left:0;right:0;height:65%;background:linear-gradient(180deg,#7cb342,#558b2f);border-radius:35% 35% 0 0}
.vil-water{position:absolute;bottom:0;right:-5%;width:40%;height:16%;background:linear-gradient(135deg,#4fc3f7,#0288d1);border-radius:50% 0 0 0;opacity:0.6}
.vil-trees{position:absolute;left:3%;top:28%;font-size:1.6rem;display:flex;flex-direction:column;gap:3px;z-index:1}
.vil-trees span{animation:treeW 4s ease-in-out infinite}
@keyframes treeW{0%,100%{transform:rotate(0)}50%{transform:rotate(2deg)}}
.vil-bldgs{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;flex-wrap:wrap;gap:14px;padding:16px 44px;z-index:3}
.vb{display:flex;flex-direction:column;align-items:center;cursor:pointer;transition:all 0.2s}
.vb:active{transform:scale(0.88)}
.vb-icon{font-size:2.8rem;filter:drop-shadow(0 5px 10px rgba(0,0,0,0.25));animation:vbBob 3.5s ease-in-out infinite}
@keyframes vbBob{0%,100%{transform:translateY(0)}50%{transform:translateY(-5px)}}
.vb-stars{display:flex;gap:1px;font-size:0.5rem;margin-top:3px}
.vb-stars .s-on{color:#fdd835;text-shadow:0 0 3px rgba(253,216,53,0.5)}.vb-stars .s-off{color:rgba(0,0,0,0.12)}
.vil-panel{position:absolute;right:0;top:0;bottom:0;width:43%;background:rgba(255,253,231,0.97);border-radius:18px 0 0 18px;padding:10px 7px;display:flex;flex-direction:column;gap:5px;overflow-y:auto;box-shadow:-3px 0 15px rgba(0,0,0,0.12);border-left:3px solid #fdd835;z-index:5}
.vp-item{display:flex;align-items:center;gap:7px;padding:7px 6px;background:#fff;border-radius:10px;border:1.5px solid #e8e8e8;cursor:pointer;transition:all 0.12s}
.vp-item:active{transform:scale(0.96);background:#f5f5f5}
.vp-item.maxed{border-color:#66bb6a;background:#e8f5e9}
.vpi-icon{font-size:1.3rem}
.vpi-info{flex:1}
.vpi-name{font-size:0.65rem;font-weight:600;color:#3e2723}
.vpi-stars{font-size:0.48rem;color:#fdd835;margin-top:1px}
.vpi-cost{display:inline-flex;align-items:center;gap:3px;font-size:0.6rem;font-weight:700;color:#fff;background:linear-gradient(90deg,#43a047,#2e7d32);padding:3px 9px;border-radius:7px;margin-top:3px}
.vpi-cost.cant{background:linear-gradient(90deg,#e53935,#c62828)}
.vpi-done{font-size:0.55rem;color:#43a047;font-weight:700}

/* CARDS PAGE */
.pg-cards{background:linear-gradient(180deg,#4a148c,#311b92);padding:14px}
.cards-header{text-align:center;margin-bottom:16px}
.cards-header h2{font-size:1.3rem;color:#ffd600}
.cards-header p{font-size:0.72rem;color:#b39ddb;margin-top:2px}
.card-set{background:rgba(255,255,255,0.04);border:1.5px solid rgba(255,255,255,0.08);border-radius:16px;padding:12px;margin-bottom:12px}
.cs-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:8px}
.cs-name{font-weight:600;font-size:0.85rem;color:#fff}
.cs-prog{font-size:0.7rem;color:#b39ddb}
.cs-reward{font-size:0.55rem;color:#ffd600;background:rgba(255,214,0,0.1);padding:2px 8px;border-radius:6px}
.cs-cards{display:flex;gap:5px;flex-wrap:wrap}
.cs-card{width:46px;height:56px;border-radius:8px;display:flex;flex-direction:column;align-items:center;justify-content:center;font-size:1.3rem;position:relative;cursor:pointer;transition:all 0.2s;border:2px solid rgba(255,255,255,0.1);background:rgba(255,255,255,0.03)}
.cs-card:active{transform:scale(0.9)}
.cs-card.has{border-color:#ffd600;background:rgba(255,214,0,0.06);box-shadow:0 0 8px rgba(255,214,0,0.15)}
.cs-card.no{opacity:0.2;cursor:default}
.cs-card .cc-count{position:absolute;bottom:2px;right:3px;font-size:0.45rem;background:#ffd600;color:#311b92;padding:1px 4px;border-radius:4px;font-weight:700}
.cs-card .cc-trade{position:absolute;top:-4px;right:-4px;width:14px;height:14px;background:#4caf50;border-radius:50%;font-size:0.45rem;display:flex;align-items:center;justify-content:center;color:#fff;font-weight:700;border:1.5px solid #1b5e20}
.cs-complete{text-align:center;padding:8px;margin-top:6px}
.cs-complete-btn{padding:8px 18px;border:none;border-radius:10px;background:linear-gradient(135deg,#ffd600,#ff8f00);color:#311b92;font-weight:700;font-size:0.75rem;cursor:pointer;font-family:inherit;box-shadow:0 3px 10px rgba(255,214,0,0.3)}
.cs-complete-btn:active{transform:scale(0.95)}

/* FRIENDS PAGE */
.pg-friends{background:linear-gradient(180deg,#1565c0,#0d47a1);padding:14px}
.fr-header{text-align:center;margin-bottom:16px}
.fr-header h2{font-size:1.3rem;color:#fff}
.fr-header p{font-size:0.72rem;color:#90caf9;margin-top:2px}
.fr-invite{background:rgba(255,255,255,0.06);border:2px solid rgba(255,255,255,0.12);border-radius:18px;padding:18px;text-align:center;margin-bottom:16px}
.fr-invite h3{font-size:0.95rem;color:#fff;margin-bottom:3px}
.fr-invite p{font-size:0.68rem;color:#90caf9;margin-bottom:12px}
.fr-invite-reward{display:inline-flex;align-items:center;gap:6px;padding:5px 12px;background:rgba(255,215,0,0.1);border:1px solid rgba(255,215,0,0.2);border-radius:8px;font-size:0.75rem;font-weight:700;color:#ffd600;margin-bottom:12px}
.fr-invite-btns{display:flex;gap:7px;justify-content:center;flex-wrap:wrap}
.fr-btn{padding:9px 16px;border:none;border-radius:10px;font-family:inherit;font-weight:700;font-size:0.75rem;cursor:pointer;display:flex;align-items:center;gap:5px}
.fr-btn:active{transform:scale(0.95)}
.fr-btn-fb{background:#1877f2;color:#fff}
.fr-btn-wa{background:#25d366;color:#fff}
.fr-btn-lk{background:rgba(255,255,255,0.1);color:#fff;border:1px solid rgba(255,255,255,0.2)}
.fr-list-title{font-size:0.7rem;color:#90caf9;margin-bottom:8px;text-transform:uppercase;letter-spacing:0.04em}
.fr-list{display:flex;flex-direction:column;gap:7px}
.fr-card{display:flex;align-items:center;gap:10px;padding:10px;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.08);border-radius:12px}
.fr-av{width:36px;height:36px;border-radius:50%;background:linear-gradient(135deg,#7c4dff,#e040fb);display:flex;align-items:center;justify-content:center;font-size:1rem}
.fr-info{flex:1}.fr-nm{font-size:0.78rem;font-weight:600}.fr-lv{font-size:0.62rem;color:#90caf9}
.fr-act{padding:5px 10px;border:none;border-radius:7px;background:rgba(255,255,255,0.1);color:#fff;font-size:0.62rem;font-weight:600;cursor:pointer;font-family:inherit}

/* Bottom nav */
.bnav{display:flex;padding:5px 8px 10px;gap:3px;background:rgba(15,8,35,0.96);backdrop-filter:blur(6px);z-index:50}
.nb{flex:1;padding:7px 3px;border:none;border-radius:11px;background:transparent;color:rgba(255,255,255,0.35);font-family:inherit;font-size:0.52rem;font-weight:600;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:2px;transition:all 0.2s}
.nb.on{color:#fbbf24}
.nb .nbi{font-size:1.1rem}

/* Popup overlay */
.ov{position:fixed;inset:0;background:rgba(10,5,25,0.92);display:none;align-items:center;justify-content:center;z-index:200;backdrop-filter:blur(5px)}
.ov.show{display:flex}
.pop{background:linear-gradient(145deg,#ef6c00,#e65100);border:3px solid #ffb300;border-radius:22px;padding:22px;text-align:center;max-width:290px;width:88%;animation:popIn 0.3s cubic-bezier(0.16,1,0.3,1);box-shadow:0 20px 60px rgba(0,0,0,0.5)}
@keyframes popIn{0%{transform:scale(0.5);opacity:0}100%{transform:scale(1);opacity:1}}
.pop-i{font-size:3rem;margin-bottom:6px}
.pop-t{font-size:1.1rem;color:#fff;margin-bottom:4px}
.pop-d{font-size:0.8rem;color:#ffe0b2;margin-bottom:14px;line-height:1.4;white-space:pre-line}
.pop-b{padding:10px 24px;border:none;border-radius:11px;background:linear-gradient(135deg,#fdd835,#f9a825);color:#3e2723;font-weight:700;font-size:0.88rem;cursor:pointer;font-family:inherit}
.pop-b:active{transform:scale(0.95)}

/* Trade overlay */
.trade-ov{position:fixed;inset:0;background:rgba(10,5,25,0.94);display:none;align-items:center;justify-content:center;z-index:300}
.trade-ov.show{display:flex}
.trade-box{background:#1a0d40;border:2px solid #7c4dff;border-radius:20px;padding:22px;text-align:center;max-width:300px;width:88%;animation:popIn 0.3s cubic-bezier(0.16,1,0.3,1)}
.trade-box h3{font-size:1rem;color:#fff;margin-bottom:10px}
.trade-card-big{font-size:3rem;margin:10px 0}
.trade-info{font-size:0.75rem;color:#b39ddb;margin-bottom:14px}
.trade-btns{display:flex;gap:8px;justify-content:center}
.trade-btn{padding:9px 18px;border:none;border-radius:10px;font-family:inherit;font-weight:700;font-size:0.78rem;cursor:pointer}
.trade-btn-give{background:#4caf50;color:#fff}
.trade-btn-close{background:rgba(255,255,255,0.08);color:#b39ddb;border:1px solid rgba(255,255,255,0.15)}

/* GM */
.gm-ov{position:fixed;inset:0;background:rgba(10,5,25,0.98);display:none;flex-direction:column;padding:20px;z-index:600;overflow-y:auto}
.gm-ov.show{display:flex}
.gm-x{position:absolute;top:14px;right:14px;background:none;border:none;color:#f44336;font-size:1.4rem;cursor:pointer}
.gm-t{font-family:'Lilita One',cursive;color:#f44336;text-align:center;font-size:1.1rem;margin:16px 0}
.gm-s{margin-bottom:12px}.gm-s h4{font-size:0.65rem;color:#ff8f00;margin-bottom:5px;text-transform:uppercase}
.gm-r{display:flex;gap:4px;flex-wrap:wrap}
.gm-b{padding:6px 10px;border:1px solid #7c4dff;background:rgba(124,77,255,0.12);color:#e0e0e0;border-radius:7px;font-size:0.62rem;font-weight:600;cursor:pointer;font-family:inherit}
.gm-b:active{transform:scale(0.93)}
.gm-i{padding:6px;width:70px;background:#0f0a2a;border:1px solid #7c4dff;border-radius:5px;color:#fff;font-family:inherit;font-size:0.68rem}

.coin-fly{position:fixed;pointer-events:none;z-index:400;font-size:1.1rem;animation:cUp 0.8s cubic-bezier(0.16,1,0.3,1) forwards}
@keyframes cUp{0%{opacity:1;transform:scale(1) translateY(0)}100%{opacity:0;transform:scale(0.3) translateY(-70px)}}
.confetti{position:fixed;pointer-events:none;z-index:350;border-radius:2px;animation:cf 2.5s ease-in forwards}
@keyframes cf{0%{transform:translateY(0) rotate(0) scale(1);opacity:1}100%{transform:translateY(100vh) rotate(900deg) scale(0.3);opacity:0}}

::-webkit-scrollbar{width:3px}::-webkit-scrollbar-thumb{background:rgba(255,255,255,0.1);border-radius:2px}
</style>
</head>
<body>
<div class="app">
  <div class="hud">
    <div class="h-coins" id="hud-coins"><div class="h-coin-i">$</div><span id="hc">1,500,000</span></div>
    <div class="h-spins"><div class="h-spin-i"></div><span id="hs">50</span>/50</div>
    <div class="h-btn" onclick="showDaily()">🎁</div>
  </div>
  <div class="dots"><div class="dot on" id="d0"></div><div class="dot" id="d1"></div><div class="dot" id="d2"></div><div class="dot" id="d3"></div></div>

  <div class="pages" id="pages">
    <!-- SPIN -->
    <div class="pg pg-spin" id="pg0">
      <div class="spin-sky"><div class="spin-cloud" style="width:100px;height:28px;top:8%;animation-duration:22s"></div><div class="spin-cloud" style="width:70px;height:20px;top:20%;animation-duration:28s;animation-delay:6s"></div><div class="spin-cloud" style="width:110px;height:32px;top:4%;animation-duration:25s;animation-delay:12s"></div></div>
      <div class="spin-top"><div class="spin-avatar">🧙‍♂️</div><div class="spin-name">Andra</div><div class="spin-coins" id="sc-coins">🪙 1,500,000</div></div>
      <div class="slot-wrap"><div class="slot-machine"><div class="sl-header"><span><span id="sl-n">50</span>/50 ⚡</span><span id="sl-t">Full!</span></div><div class="sl-reels-wrap"><div class="sl-reels"><div class="sl-reel" id="r0"><span class="ri">🪙</span></div><div class="sl-reel" id="r1"><span class="ri">💰</span></div><div class="sl-reel" id="r2"><span class="ri">🪙</span></div></div></div><button class="sl-spin-btn" id="sbtn" onclick="doSpin()">SPIN</button><div class="sl-multi"><div class="ml-btn on" onclick="setM(1,this)">x1</div><div class="ml-btn" onclick="setM(3,this)">x3</div><div class="ml-btn" onclick="setM(5,this)">x5</div></div></div></div>
    </div>

    <!-- VILLAGE -->
    <div class="pg pg-village" id="pg1">
      <div class="vil-header"><div class="vil-name" id="vn">🏘️ Satul Zorilor</div><div class="vil-prog" id="vp">0/25</div><div class="vil-bar-wrap"><div class="vil-bar-fill" id="vf" style="width:0%"></div></div></div>
      <div class="vil-scene"><div class="vil-ground"></div><div class="vil-water"></div><div class="vil-trees"><span>🌲</span><span style="animation-delay:1s">🌳</span><span style="animation-delay:2s">🌲</span></div><div class="vil-bldgs" id="vbl"></div><div class="vil-panel" id="vpnl"></div></div>
    </div>

    <!-- CARDS -->
    <div class="pg pg-cards" id="pg2"></div>

    <!-- FRIENDS -->
    <div class="pg pg-friends" id="pg3">
      <div class="fr-header"><h2>👥 Prieteni</h2><p>Invită și câștigă!</p></div>
      <div class="fr-invite"><h3>🎁 Invită = 50 Spins!</h3><p>Fiecare prieten nou = recompense pentru amândoi</p><div class="fr-invite-reward">⚡ 50 Spins + 🪙 5,000</div><div class="fr-invite-btns"><button class="fr-btn fr-btn-fb" onclick="invFB()">📘 Facebook</button><button class="fr-btn fr-btn-wa" onclick="invWA()">💬 WhatsApp</button><button class="fr-btn fr-btn-lk" onclick="invLk()">🔗 Link</button></div></div>
      <div class="fr-list-title">Prieteni</div>
      <div class="fr-list" id="frl"></div>
    </div>
  </div>

  <div class="bnav"><button class="nb on" onclick="goPg(0)"><span class="nbi">🎰</span>Spin</button><button class="nb" onclick="goPg(1)"><span class="nbi">🏘️</span>Sat</button><button class="nb" onclick="goPg(2)"><span class="nbi">🃏</span>Cărți</button><button class="nb" onclick="goPg(3)"><span class="nbi">👥</span>Social</button></div>
</div>

<!-- Popup -->
<div class="ov" id="pov"><div class="pop"><div class="pop-i" id="pi">🎉</div><div class="pop-t" id="pt"></div><div class="pop-d" id="pd"></div><button class="pop-b" onclick="closePop()">OK!</button></div></div>

<!-- Trade -->
<div class="trade-ov" id="tov"><div class="trade-box"><h3>📤 Trimite Carte</h3><div class="trade-card-big" id="tc-icon"></div><div class="trade-info" id="tc-info"></div><div class="trade-btns"><button class="trade-btn trade-btn-give" onclick="doTrade()">Trimite</button><button class="trade-btn trade-btn-close" onclick="closeTrade()">Închide</button></div></div></div>

<!-- GM (secret: tap coins 7x) -->
<div class="gm-ov" id="gmov"><button class="gm-x" onclick="closeGM()">✕</button><div class="gm-t">🔧 GM · Andra</div><div class="gm-s"><h4>Resurse</h4><div class="gm-r"><input class="gm-i" id="gci" value="1000000" type="number"><button class="gm-b" onclick="gmAddCoins()">+Coins</button><input class="gm-i" id="gsi" value="200" type="number"><button class="gm-b" onclick="gmAddSpins()">+Spins</button></div></div><div class="gm-s"><h4>Sat</h4><div class="gm-r"><button class="gm-b" onclick="gmMaxBldg()">Max</button><button class="gm-b" onclick="gmSkipVil()">Skip→</button></div></div><div class="gm-s"><h4>Cărți</h4><div class="gm-r"><button class="gm-b" onclick="gmAddCards()">+1 fiecare</button></div></div></div>

<script>
// ===== STATE =====
var S = {
  coins: 1500000,
  spins: 50,
  maxS: 50,
  village: 1,
  buildings: [],
  multi: 1,
  cards: []
};

var SYMS = ['🪙','🪙','🪙','💰','💰','⚔️','⚔️','🛡️','🐷','🐷','⚡','⚡','🎁','🃏'];
var VN = ['Satul Zorilor','Cetatea Lunii','Regatul Stelelor','Imperiul Focului','Ținutul Dragonilor','Domeniul Zeilor','Oaza Vântului','Fortul Tunetului','Insula Misterelor','Orașul Cristal'];

// Village generator
function genV(lv) {
  var icons = ['🏠','🌾','⛏️','🏰','👑','🏪','🗼','⛪','🏯','🏛️','⚓','🏟️'];
  var names = ['Casă','Fermă','Mină','Fort','Palat','Piață','Turn','Templu','Castel','Academie','Port','Arenă'];
  var base = Math.floor(800 * Math.pow(1.5, lv - 1));
  var arr = [];
  for (var i = 0; i < 5; i++) {
    var idx = ((lv - 1) * 5 + i) % icons.length;
    var costs = [];
    for (var l = 0; l < 5; l++) costs.push(Math.floor(base * (1 + i * 0.3) * Math.pow(2.2, l)));
    arr.push({ name: names[idx], icon: icons[idx], level: 0, costs: costs });
  }
  return arr;
}
S.buildings = genV(1);

// Cards system
function initCards() {
  S.cards = [
    { name: 'Animale Magice', reward: 50, cards: ['🐺','🦊','🐻','🦁','🐉','🦅','🐲'], inv: {}, claimed: false },
    { name: 'Comori Antice', reward: 75, cards: ['💎','👑','🏆','💰','🗝️','🔮','📿'], inv: {}, claimed: false },
    { name: 'Elemente', reward: 60, cards: ['🔥','💧','⚡','🌍','💨','❄️','☀️'], inv: {}, claimed: false },
    { name: 'Lumi Paralele', reward: 100, cards: ['🌌','🪐','⭐','🌙','☄️','🌈','🌊'], inv: {}, claimed: false },
    { name: 'Creaturi', reward: 80, cards: ['🧙','🧛','🧜','🧝','🧞','🦄','👻'], inv: {}, claimed: false }
  ];
}
initCards();

// ===== SWIPE =====
var curPage = 0;
var pagesEl = document.getElementById('pages');
var touchX = 0, touchDelta = 0, isSwiping = false;

pagesEl.addEventListener('touchstart', function(e) {
  touchX = e.touches[0].clientX;
  isSwiping = true;
  pagesEl.style.transition = 'none';
});

pagesEl.addEventListener('touchmove', function(e) {
  if (!isSwiping) return;
  touchDelta = e.touches[0].clientX - touchX;
  var offset = -curPage * 100 + (touchDelta / pagesEl.clientWidth) * 100;
  pagesEl.style.transform = 'translateX(' + offset + '%)';
});

pagesEl.addEventListener('touchend', function() {
  isSwiping = false;
  pagesEl.style.transition = 'transform 0.35s cubic-bezier(0.16,1,0.3,1)';
  if (Math.abs(touchDelta) > 50) {
    if (touchDelta < 0 && curPage < 3) curPage++;
    else if (touchDelta > 0 && curPage > 0) curPage--;
  }
  touchDelta = 0;
  updatePage();
});

function goPg(p) { curPage = p; updatePage(); }

function updatePage() {
  pagesEl.style.transition = 'transform 0.35s cubic-bezier(0.16,1,0.3,1)';
  pagesEl.style.transform = 'translateX(-' + (curPage * 100) + '%)';
  var dots = document.querySelectorAll('.dot');
  var navs = document.querySelectorAll('.nb');
  for (var i = 0; i < dots.length; i++) {
    dots[i].classList.toggle('on', i === curPage);
    navs[i].classList.toggle('on', i === curPage);
  }
  if (curPage === 2) renderCards();
}

// ===== FORMAT =====
function fmtC(n) {
  if (n >= 1e6) return (n / 1e6).toFixed(1) + 'M';
  if (n >= 1e3) return Math.floor(n / 1e3) + 'K';
  return n.toLocaleString();
}

// ===== RENDER =====
function render() {
  document.getElementById('hc').textContent = fmtC(S.coins);
  document.getElementById('hs').textContent = S.spins;
  document.getElementById('sl-n').textContent = S.spins;
  document.getElementById('sc-coins').textContent = '🪙 ' + fmtC(S.coins);
  document.getElementById('vn').textContent = VN[Math.min(S.village - 1, VN.length - 1)] || ('Sat ' + S.village);

  var tot = 0, max = S.buildings.length * 5;
  for (var i = 0; i < S.buildings.length; i++) tot += S.buildings[i].level;
  document.getElementById('vp').textContent = tot + '/' + max;
  document.getElementById('vf').style.width = (tot / max * 100) + '%';

  // Village buildings
  var bhtml = '';
  for (var i = 0; i < S.buildings.length; i++) {
    var b = S.buildings[i];
    var stars = '';
    for (var si = 0; si < 5; si++) stars += '<span class="' + (si < b.level ? 's-on' : 's-off') + '">★</span>';
    bhtml += '<div class="vb" onclick="upg(' + i + ')" style="animation-delay:' + (i * 0.3) + 's"><div class="vb-icon" style="animation-delay:' + (i * 0.5) + 's">' + b.icon + '</div><div class="vb-stars">' + stars + '</div></div>';
  }
  document.getElementById('vbl').innerHTML = bhtml;

  // Panel
  var phtml = '';
  for (var i = 0; i < S.buildings.length; i++) {
    var b = S.buildings[i];
    var mx = b.level >= 5;
    var cost = mx ? 0 : b.costs[b.level];
    var can = S.coins >= cost;
    var stars2 = '';
    for (var si = 0; si < 5; si++) stars2 += (si < b.level ? '★' : '☆');
    if (mx) {
      phtml += '<div class="vp-item maxed"><span class="vpi-icon">' + b.icon + '</span><div class="vpi-info"><div class="vpi-name">' + b.name + '</div><div class="vpi-stars">' + stars2 + '</div><div class="vpi-done">✅ Complet</div></div></div>';
    } else {
      phtml += '<div class="vp-item" onclick="upg(' + i + ')"><span class="vpi-icon">' + b.icon + '</span><div class="vpi-info"><div class="vpi-name">' + b.name + '</div><div class="vpi-stars">' + stars2 + '</div><div class="vpi-cost ' + (can ? '' : 'cant') + '">' + fmtC(cost) + ' 🪙</div></div></div>';
    }
  }
  document.getElementById('vpnl').innerHTML = phtml;

  // Check village complete
  var allMax = true;
  for (var i = 0; i < S.buildings.length; i++) { if (S.buildings[i].level < 5) { allMax = false; break; } }
  if (allMax) setTimeout(nextV, 600);

  // Friends
  renderFriends();
}

// ===== UPGRADE =====
function upg(i) {
  var b = S.buildings[i];
  if (b.level >= 5) return;
  var cost = b.costs[b.level];
  if (S.coins < cost) return;
  S.coins -= cost;
  b.level++;
  if (b.level >= 5) {
    var bc = 50000 * S.village;
    var bs = 5 + S.village * 2;
    S.coins += bc;
    S.spins = Math.min(999, S.spins + bs);
    showPop('🎉', b.name + ' MAX!', '+' + fmtC(bc) + ' 🪙\n+' + bs + ' ⚡');
    doConf();
  }
  render();
}

function nextV() {
  S.village++;
  S.buildings = genV(S.village);
  var bc = 200000 * S.village;
  var bs = 15 + S.village * 3;
  S.coins += bc;
  S.spins = Math.min(999, S.spins + bs);
  showPop('🏆', 'Sat Nou!', VN[Math.min(S.village - 1, VN.length - 1)] + '\n+' + fmtC(bc) + ' 🪙 +' + bs + ' ⚡');
  doConf();
  render();
}

// ===== SLOT =====
var spinning = false;

function setM(m, el) {
  S.multi = m;
  var btns = document.querySelectorAll('.ml-btn');
  for (var i = 0; i < btns.length; i++) btns[i].classList.remove('on');
  el.classList.add('on');
}

function doSpin() {
  if (spinning || S.spins < S.multi) return;
  spinning = true;
  S.spins -= S.multi;
  document.getElementById('sbtn').disabled = true;

  var reels = [document.getElementById('r0'), document.getElementById('r1'), document.getElementById('r2')];
  for (var i = 0; i < 3; i++) reels[i].classList.add('spin');

  var res = [];
  for (var i = 0; i < 3; i++) res.push(SYMS[Math.floor(Math.random() * SYMS.length)]);
  if (Math.random() < 0.3) {
    var sym = SYMS[Math.floor(Math.random() * SYMS.length)];
    res[0] = sym; res[1] = sym;
    if (Math.random() < 0.35) res[2] = sym;
  }

  var delays = [500, 900, 1300];
  for (var i = 0; i < 3; i++) {
    (function(idx) {
      setTimeout(function() {
        reels[idx].classList.remove('spin');
        reels[idx].querySelector('.ri').textContent = res[idx];
        if (idx === 2) setTimeout(function() { evalSpin(res); }, 300);
      }, delays[idx]);
    })(i);
  }
  render();
}

function evalSpin(res) {
  spinning = false;
  document.getElementById('sbtn').disabled = false;
  var a = res[0], b = res[1], c = res[2];
  var m = S.multi, v = S.village;
  var els = document.querySelectorAll('.sl-reel');

  if (a === b && b === c) {
    for (var i = 0; i < els.length; i++) { els[i].classList.add('win'); }
    setTimeout(function() { for (var i = 0; i < els.length; i++) els[i].classList.remove('win'); }, 1200);

    switch (a) {
      case '🪙': S.coins += 80000 * v * m; showPop('🪙🪙🪙', 'JACKPOT!', '+' + fmtC(80000 * v * m)); doConf(); break;
      case '💰': S.coins += 250000 * v * m; showPop('💰💰💰', 'MEGA!', '+' + fmtC(250000 * v * m)); doConf(); break;
      case '⚔️': S.coins += 100000 * v * m; showPop('⚔️', 'ATAC!', '+' + fmtC(100000 * v * m)); break;
      case '🛡️': showPop('🛡️🛡️🛡️', 'Scuturi!', 'Protecție completă!'); break;
      case '🐷': S.coins += 150000 * v * m; showPop('🐷🐷🐷', 'RAID!', '+' + fmtC(150000 * v * m)); doConf(); break;
      case '⚡': var sp = (15 + v * 3) * m; S.spins = Math.min(999, S.spins + sp); showPop('⚡⚡⚡', 'FREE SPINS!', '+' + sp + ' rotiri!'); doConf(); break;
      case '🎁': S.coins += 200000 * v * m; S.spins = Math.min(999, S.spins + 10 * m); showPop('🎁🎁🎁', 'MEGA BONUS!', '+' + fmtC(200000 * v * m) + '\n+' + (10 * m) + ' ⚡'); doConf(); break;
      case '🃏': giveCards(3 * m); break;
    }
  } else if (a === b || b === c || a === c) {
    var match = (a === b) ? a : ((b === c) ? b : a);
    switch (match) {
      case '🪙': S.coins += 20000 * v * m; coinA(); break;
      case '💰': S.coins += 50000 * v * m; coinA(); break;
      case '⚔️': S.coins += 30000 * v * m; break;
      case '🐷': S.coins += 40000 * v * m; coinA(); break;
      case '⚡': var sp2 = (3 + v) * m; S.spins = Math.min(999, S.spins + sp2); showPop('⚡', 'Spins!', '+' + sp2 + ' rotiri!'); break;
      case '🎁': S.coins += 60000 * v * m; coinA(); break;
      case '🃏': giveCards(1 * m); break;
      default: S.coins += 10000 * v * m; break;
    }
  } else {
    S.coins += 5000 * v * m;
    if (Math.random() < 0.12) S.spins++;
  }
  render();
}

// ===== CARDS =====
function giveCards(n) {
  var earned = [];
  for (var i = 0; i < n; i++) {
    var si = Math.floor(Math.random() * S.cards.length);
    var set = S.cards[si];
    var ci = Math.floor(Math.random() * set.cards.length);
    var card = set.cards[ci];
    if (!set.inv[card]) set.inv[card] = 0;
    set.inv[card]++;
    earned.push(card);
  }
  if (earned.length) showPop('🃏', 'Cărți Noi!', earned.join(' '));
  if (curPage === 2) renderCards();
}

var tradeCard = null, tradeSetIdx = null;

function renderCards() {
  var pg = document.getElementById('pg2');
  var html = '<div class="cards-header"><h2>🃏 Colecție Cărți</h2><p>Completează seturi pentru spins bonus!</p></div>';

  for (var si = 0; si < S.cards.length; si++) {
    var set = S.cards[si];
    var collected = 0;
    for (var ci = 0; ci < set.cards.length; ci++) {
      if (set.inv[set.cards[ci]] && set.inv[set.cards[ci]] > 0) collected++;
    }
    var complete = collected >= set.cards.length;

    html += '<div class="card-set"><div class="cs-head"><span class="cs-name">' + set.name + '</span><span class="cs-prog">' + collected + '/' + set.cards.length + '</span><span class="cs-reward">🎁 ' + set.reward + ' ⚡</span></div><div class="cs-cards">';

    for (var ci = 0; ci < set.cards.length; ci++) {
      var card = set.cards[ci];
      var count = set.inv[card] || 0;
      var has = count > 0;
      var extra = count > 1;
      html += '<div class="cs-card ' + (has ? 'has' : 'no') + '" ' + (extra ? 'onclick="openTrade(' + si + ',\'' + card + '\')"' : '') + '>' + card;
      if (has && count > 1) html += '<span class="cc-count">x' + count + '</span>';
      if (extra) html += '<span class="cc-trade">↗</span>';
      html += '</div>';
    }
    html += '</div>';

    if (complete && !set.claimed) {
      html += '<div class="cs-complete"><button class="cs-complete-btn" onclick="claimSet(' + si + ')">🎁 Colectează ' + set.reward + ' Spins!</button></div>';
    } else if (set.claimed) {
      html += '<div class="cs-complete"><span style="font-size:0.7rem;color:#4caf50;font-weight:700">✅ Complet!</span></div>';
    }
    html += '</div>';
  }
  pg.innerHTML = html;
}

function claimSet(si) {
  var set = S.cards[si];
  if (set.claimed) return;
  set.claimed = true;
  S.spins = Math.min(999, S.spins + set.reward);
  showPop('📚', set.name + ' Complet!', '+' + set.reward + ' ⚡ Spins!');
  doConf();
  render();
  renderCards();
}

function openTrade(si, card) {
  tradeCard = card;
  tradeSetIdx = si;
  document.getElementById('tc-icon').textContent = card;
  document.getElementById('tc-info').textContent = 'Ai ' + S.cards[si].inv[card] + 'x din această carte.\nTrimite una unui prieten!';
  document.getElementById('tov').classList.add('show');
}

function doTrade() {
  if (!tradeCard) return;
  S.cards[tradeSetIdx].inv[tradeCard]--;
  if (S.cards[tradeSetIdx].inv[tradeCard] <= 0) delete S.cards[tradeSetIdx].inv[tradeCard];
  document.getElementById('tov').classList.remove('show');
  showPop('📤', 'Carte Trimisă!', tradeCard + ' trimis unui prieten!');
  tradeCard = null;
  renderCards();
}

function closeTrade() {
  document.getElementById('tov').classList.remove('show');
}

// ===== FRIENDS =====
function renderFriends() {
  var friends = [
    { n: 'Maria P.', lv: 5, a: '👩' },
    { n: 'Alex M.', lv: 3, a: '👦' },
    { n: 'Ioana D.', lv: 8, a: '👧' },
    { n: 'Mihai T.', lv: 12, a: '🧑' },
    { n: 'Elena R.', lv: 6, a: '👩‍🦰' }
  ];
  var html = '';
  for (var i = 0; i < friends.length; i++) {
    var f = friends[i];
    html += '<div class="fr-card"><div class="fr-av">' + f.a + '</div><div class="fr-info"><div class="fr-nm">' + f.n + '</div><div class="fr-lv">Sat ' + f.lv + '</div></div><button class="fr-act" onclick="atkFr()">⚔️</button></div>';
  }
  document.getElementById('frl').innerHTML = html;
}

function invFB() { S.spins = Math.min(999, S.spins + 50); showPop('📘', 'Invitație!', 'Când acceptă:\n+50 ⚡ pentru amândoi!'); doConf(); render(); }
function invWA() { S.spins = Math.min(999, S.spins + 50); showPop('💬', 'Link trimis!', '+50 ⚡ la înregistrare!'); doConf(); render(); }
function invLk() { if (navigator.clipboard) navigator.clipboard.writeText('https://spinkingdom.app/invite/andra'); showPop('🔗', 'Copiat!', 'Trimite-l prietenilor!'); }
function atkFr() { S.coins += 100000 * S.village; showPop('⚔️', 'Atac!', '+' + fmtC(100000 * S.village)); coinA(); render(); }

// ===== DAILY =====
function showDaily() {
  var rewards = [10000, 20000, 35000, 50000, 75000, 100000, 200000];
  var d = Math.floor(Math.random() * 7);
  var c = rewards[d] * S.village;
  var sp = 3 + d * 2;
  S.coins += c;
  S.spins = Math.min(999, S.spins + sp);
  showPop('📅', 'Bonus Zilnic!', 'Zi ' + (d + 1) + ':\n+' + fmtC(c) + ' 🪙\n+' + sp + ' ⚡');
  doConf();
  render();
}

// ===== POPUP (BUG FIX: separate function name) =====
function showPop(icon, title, desc) {
  document.getElementById('pi').textContent = icon;
  document.getElementById('pt').textContent = title;
  document.getElementById('pd').textContent = desc;
  document.getElementById('pov').classList.add('show');
}

function closePop() {
  document.getElementById('pov').classList.remove('show');
}

// ===== SECRET GM (tap coins 7x fast) =====
var gmTaps = 0, gmTimer = null;
document.getElementById('hud-coins').addEventListener('click', function() {
  gmTaps++;
  clearTimeout(gmTimer);
  gmTimer = setTimeout(function() { gmTaps = 0; }, 2000);
  if (gmTaps >= 7) {
    gmTaps = 0;
    document.getElementById('gmov').classList.add('show');
  }
});

function closeGM() { document.getElementById('gmov').classList.remove('show'); }
function gmAddCoins() { S.coins += parseInt(document.getElementById('gci').value) || 0; render(); }
function gmAddSpins() { S.spins += parseInt(document.getElementById('gsi').value) || 0; render(); }
function gmMaxBldg() { for (var i = 0; i < S.buildings.length; i++) S.buildings[i].level = 5; render(); }
function gmSkipVil() { S.village++; S.buildings = genV(S.village); render(); }
function gmAddCards() { for (var si = 0; si < S.cards.length; si++) { var set = S.cards[si]; for (var ci = 0; ci < set.cards.length; ci++) { var card = set.cards[ci]; if (!set.inv[card]) set.inv[card] = 0; set.inv[card]++; } } renderCards(); }

// ===== EFFECTS =====
function coinA() {
  for (var i = 0; i < 6; i++) {
    (function(idx) {
      setTimeout(function() {
        var e = document.createElement('div');
        e.className = 'coin-fly';
        e.textContent = '🪙';
        e.style.left = (20 + Math.random() * 60) + '%';
        e.style.top = (25 + Math.random() * 20) + '%';
        document.body.appendChild(e);
        setTimeout(function() { e.remove(); }, 800);
      }, idx * 50);
    })(i);
  }
}

function doConf() {
  var colors = ['#fbbf24','#ec4899','#7c3aed','#10b981','#3b82f6','#ef4444','#ff6f00'];
  for (var i = 0; i < 30; i++) {
    (function(idx) {
      setTimeout(function() {
        var e = document.createElement('div');
        e.className = 'confetti';
        e.style.left = Math.random() * 100 + '%';
        e.style.top = '-10px';
        e.style.background = colors[Math.floor(Math.random() * colors.length)];
        e.style.width = (4 + Math.random() * 8) + 'px';
        e.style.height = (4 + Math.random() * 8) + 'px';
        document.body.appendChild(e);
        setTimeout(function() { e.remove(); }, 3000);
      }, idx * 25);
    })(i);
  }
}

// Spin regen
setInterval(function() {
  if (S.spins < S.maxS) { S.spins++; render(); }
}, 60000);

// Init
render();
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>The Heartbeat Sync — PlayAh Her Feel</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;700;900&family=Dancing+Script:wght@600;700&display=swap" rel="stylesheet" />
  <style>
    :root {
      --fire:   #FF3B5C;
      --fire2:  #FF6B35;
      --fire3:  #FFD700;
      --water:  #4FC3F7;
      --water2: #87CEEB;
      --water3: #B3E5FC;
      --dark:   #0a0a18;
      --dark2:  #12122a;
      --card:   rgba(255,255,255,0.06);
      --glow-r: 0 0 30px rgba(255,59,92,0.6);
      --glow-b: 0 0 30px rgba(79,195,247,0.6);
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html, body {
      width: 100%; height: 100%; overflow: hidden;
      font-family: 'Montserrat', sans-serif;
      background: var(--dark); color: #fff;
    }

    .screen {
      position: absolute; inset: 0;
      display: flex; flex-direction: column;
      align-items: center; justify-content: center;
      opacity: 0; pointer-events: none;
      transition: opacity .6s ease;
    }
    .screen.active { opacity: 1; pointer-events: all; }

    /* ── WELCOME ── */
    #s-welcome { background: var(--dark); overflow: hidden; }
    .welcome-bg { position: absolute; inset: 0; display: flex; }
    .fire-half {
      flex: 1;
      background: linear-gradient(135deg, #3a0010 0%, #7a1020 40%, #c02030 70%, #FF3B5C 100%);
      position: relative; overflow: hidden;
    }
    .water-half {
      flex: 1;
      background: linear-gradient(225deg, #001a3a 0%, #0a2a5a 40%, #1a5080 70%, #4FC3F7 100%);
      position: relative; overflow: hidden;
    }
    .flame { position: absolute; bottom: 0; border-radius: 50% 50% 20% 20%; transform-origin: bottom center; }
    .flame-1 { width: 80px; height: 160px; background: linear-gradient(to top, #FF6B35, #FF3B5C, transparent); left: 20%; animation: flicker1 1.8s ease-in-out infinite; }
    .flame-2 { width: 120px; height: 220px; background: linear-gradient(to top, #FFD700, #FF6B35, transparent); left: 40%; animation: flicker2 2.2s ease-in-out infinite; opacity:.8; }
    .flame-3 { width: 60px; height: 130px; background: linear-gradient(to top, #FF3B5C, #FF6B35, transparent); left: 65%; animation: flicker1 1.5s ease-in-out infinite; }
    .flame-4 { width: 100px; height: 180px; background: linear-gradient(to top, #FF6B35, #FFD700, transparent); left: 10%; animation: flicker3 2s ease-in-out infinite; opacity:.7; }
    @keyframes flicker1 {
      0%,100% { transform: scaleX(1) scaleY(1) skewX(0); opacity:1; }
      25%      { transform: scaleX(.9) scaleY(1.08) skewX(-4deg); opacity:.9; }
      50%      { transform: scaleX(1.05) scaleY(.95) skewX(2deg); opacity:1; }
      75%      { transform: scaleX(.95) scaleY(1.03) skewX(-2deg); opacity:.95; }
    }
    @keyframes flicker2 {
      0%,100% { transform: scaleX(1) scaleY(1) skewX(0); }
      33%      { transform: scaleX(1.06) scaleY(.92) skewX(3deg); }
      66%      { transform: scaleX(.92) scaleY(1.1) skewX(-3deg); }
    }
    @keyframes flicker3 {
      0%,100% { transform: scaleX(1) scaleY(1); opacity:.7; }
      50%      { transform: scaleX(.88) scaleY(1.12); opacity:.85; }
    }
    .ember { position: absolute; border-radius: 50%; background: #FFD700; animation: rise linear infinite; }
    @keyframes rise {
      0%   { bottom: 0; opacity: 1; transform: translateX(0) scale(1); }
      100% { bottom: 100%; opacity: 0; transform: translateX(var(--dx,0)) scale(.2); }
    }
    .bubble { position: absolute; border-radius: 50%; border: 2px solid rgba(135,206,235,.6); animation: float ease-in-out infinite; }
    @keyframes float {
      0%,100% { transform: translateY(0) translateX(0); opacity:.6; }
      50%      { transform: translateY(-40px) translateX(10px); opacity:1; }
    }
    .ripple { position: absolute; border-radius: 50%; border: 2px solid rgba(79,195,247,.4); animation: ripple-out ease-out infinite; }
    @keyframes ripple-out {
      0%   { transform: scale(.5); opacity: .8; }
      100% { transform: scale(3.5); opacity: 0; }
    }

    .welcome-center {
      position: relative; z-index: 10; text-align: center;
      background: rgba(10,10,24,.75); backdrop-filter: blur(20px);
      border: 1px solid rgba(255,255,255,.15); border-radius: 28px;
      padding: 52px 70px;
      box-shadow: var(--glow-r), var(--glow-b), 0 30px 80px rgba(0,0,0,.6);
      max-width: 700px; width: 90%;
    }
    .brand-tag {
      font-family: 'Dancing Script', cursive;
      font-size: 1.1rem; letter-spacing: 2px; color: var(--water2); margin-bottom: 8px;
    }
    .campaign-title {
      font-size: clamp(2.8rem, 6vw, 4.5rem); font-weight: 900;
      text-transform: uppercase; letter-spacing: 3px;
      background: linear-gradient(135deg, var(--fire), #fff 40%, var(--water));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
      line-height: 1.1; margin-bottom: 12px;
    }
    .campaign-sub {
      font-size: 1rem; font-weight: 300; color: rgba(255,255,255,.7);
      margin-bottom: 36px; letter-spacing: 1px;
    }
    .fire-water-divider {
      display: flex; align-items: center; gap: 12px;
      justify-content: center; margin-bottom: 36px;
    }
    .divider-line { flex: 1; height: 1px; background: linear-gradient(to right, transparent, rgba(255,255,255,.3), transparent); }
    .divider-icon { font-size: 1.4rem; }

    /* ── Buttons ── */
    .btn {
      border: none; cursor: pointer; border-radius: 50px;
      font-family: 'Montserrat', sans-serif; font-weight: 700;
      text-transform: uppercase; letter-spacing: 2px;
      transition: transform .15s, box-shadow .15s;
      padding: 16px 44px; font-size: 1rem;
    }
    .btn:active { transform: scale(.96); }
    .btn-primary { background: linear-gradient(135deg, var(--fire), var(--fire2)); color: #fff; box-shadow: var(--glow-r); }
    .btn-primary:hover { box-shadow: 0 0 50px rgba(255,59,92,.8); transform: scale(1.03); }
    .btn-secondary { background: linear-gradient(135deg, var(--water), #1a7abf); color: #fff; box-shadow: var(--glow-b); }
    .btn-secondary:hover { box-shadow: 0 0 50px rgba(79,195,247,.8); transform: scale(1.03); }
    .btn-ghost { background: transparent; border: 2px solid rgba(255,255,255,.3); color: rgba(255,255,255,.7); font-size: .85rem; padding: 10px 28px; }
    .btn-ghost:hover { border-color: rgba(255,255,255,.6); color: #fff; }

    /* ── INSTRUCTIONS ── */
    #s-instructions { background: radial-gradient(ellipse at center, #12122a 0%, var(--dark) 100%); }
    .instr-title { font-size: clamp(1.8rem, 4vw, 2.8rem); font-weight: 900; text-transform: uppercase; letter-spacing: 3px; margin-bottom: 8px; }
    .instr-sub { color: rgba(255,255,255,.6); margin-bottom: 48px; font-size:.95rem; }
    .players-row { display: flex; gap: 32px; align-items: stretch; margin-bottom: 48px; width: 90%; max-width: 800px; }
    .player-card { flex: 1; border-radius: 20px; padding: 32px 24px; text-align: center; border: 1px solid rgba(255,255,255,.1); backdrop-filter: blur(10px); }
    .player-card.p1 { background: linear-gradient(135deg, rgba(255,59,92,.15), rgba(255,107,53,.1)); border-color: rgba(255,59,92,.3); }
    .player-card.p2 { background: linear-gradient(135deg, rgba(79,195,247,.15), rgba(135,206,235,.1)); border-color: rgba(79,195,247,.3); }
    .player-num { font-size: 3rem; margin-bottom: 8px; }
    .player-label { font-weight: 700; font-size: 1.1rem; text-transform: uppercase; letter-spacing: 2px; margin-bottom: 12px; }
    .p1 .player-label { color: var(--fire); }
    .p2 .player-label { color: var(--water); }
    .player-desc { font-size: .85rem; color: rgba(255,255,255,.6); line-height: 1.6; }
    .key-hint { display: inline-block; background: rgba(255,255,255,.1); border: 1px solid rgba(255,255,255,.2); border-radius: 8px; padding: 4px 12px; font-size: .8rem; font-weight: 700; margin-top: 10px; }
    .p1 .key-hint { color: var(--fire); border-color: rgba(255,59,92,.4); }
    .p2 .key-hint { color: var(--water); border-color: rgba(79,195,247,.4); }

    /* ── GAME ── */
    #s-game { flex-direction: row; background: var(--dark); padding: 0; overflow: hidden; }
    .game-zone { flex: 1; height: 100%; display: flex; flex-direction: column; align-items: center; justify-content: center; position: relative; overflow: hidden; gap: 20px; }
    .zone-fire { background: linear-gradient(to right, #1a0008, #2a0515, #3a0820); }
    .zone-water { background: linear-gradient(to left, #001020, #001830, #002540); }
    .zone-fire .flame-bg-1 { position: absolute; bottom: 0; left: 0; right: 0; height: 200px; background: linear-gradient(to top, rgba(255,59,92,.3), transparent); animation: flameBg 2s ease-in-out infinite; }
    .zone-water .wave-bg  { position: absolute; bottom: 0; left: 0; right: 0; height: 160px; background: linear-gradient(to top, rgba(79,195,247,.2), transparent); animation: waveBg 3s ease-in-out infinite; }
    @keyframes flameBg { 0%,100%{height:200px} 50%{height:260px} }
    @keyframes waveBg  { 0%,100%{height:160px} 50%{height:200px} }
    .player-tap-label { font-size: .8rem; font-weight: 600; text-transform: uppercase; letter-spacing: 3px; opacity: .7; }
    .player-name-game { font-size: 1.4rem; font-weight: 900; text-transform: uppercase; letter-spacing: 2px; }
    .zone-fire .player-name-game { color: var(--fire); }
    .zone-water .player-name-game { color: var(--water); }

    .tap-btn {
      width: 180px; height: 180px; border-radius: 50%; border: none; cursor: pointer;
      font-family: 'Montserrat', sans-serif; font-weight: 900;
      font-size: 1.5rem; letter-spacing: 2px; text-transform: uppercase;
      position: relative; transition: transform .1s;
      user-select: none; -webkit-user-select: none;
    }
    .tap-btn:active, .tap-btn.tapped { transform: scale(.88); }
    .tap-btn-fire  { background: radial-gradient(circle at 40% 35%, var(--fire3), var(--fire2), var(--fire)); color: #fff; box-shadow: 0 0 40px rgba(255,59,92,.5), 0 0 80px rgba(255,59,92,.2); }
    .tap-btn-water { background: radial-gradient(circle at 40% 35%, var(--water3), var(--water), #1a7abf); color: #fff; box-shadow: 0 0 40px rgba(79,195,247,.5), 0 0 80px rgba(79,195,247,.2); }
    .tap-btn::after { content: ''; position: absolute; inset: -8px; border-radius: 50%; border: 3px solid currentColor; opacity: 0; animation: tapRing 0s ease-out; }
    .tap-btn.tapped::after { animation: tapRing .5s ease-out; }
    @keyframes tapRing { 0%{transform:scale(1);opacity:.8} 100%{transform:scale(1.5);opacity:0} }
    .tap-count { font-size: .85rem; opacity: .5; }
    .mini-ecg { width: 180px; height: 50px; }

    .game-center { width: 220px; flex-shrink: 0; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 16px; z-index: 5; }
    .timer-circle { width: 90px; height: 90px; position: relative; }
    .timer-circle svg { width: 100%; height: 100%; transform: rotate(-90deg); }
    .timer-bg   { fill: none; stroke: rgba(255,255,255,.1); stroke-width: 5; }
    .timer-ring { fill: none; stroke: #fff; stroke-width: 5; stroke-linecap: round; stroke-dasharray: 245; stroke-dashoffset: 0; transition: stroke-dashoffset .1s linear; }
    .timer-text { position: absolute; inset: 0; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; font-weight: 900; }

    .sync-ring-wrap { position: relative; width: 120px; height: 120px; }
    .sync-ring-wrap svg { width: 100%; height: 100%; transform: rotate(-90deg); }
    .sync-bg-ring   { fill: none; stroke: rgba(255,255,255,.08); stroke-width: 8; }
    .sync-fill-ring { fill: none; stroke-width: 8; stroke-linecap: round; stroke-dasharray: 333; stroke-dashoffset: 333; transition: stroke-dashoffset .3s ease, stroke .3s ease; }
    .sync-center-label { position: absolute; inset: 0; display: flex; flex-direction: column; align-items: center; justify-content: center; }
    .sync-pct   { font-size: 1.3rem; font-weight: 900; }
    .sync-label { font-size: .6rem; text-transform: uppercase; letter-spacing: 1px; opacity: .6; }
    .center-title { font-size: .7rem; text-transform: uppercase; letter-spacing: 3px; opacity: .5; }

    .ecg-line-wrap { width: 200px; overflow: hidden; }
    .ecg-line-wrap svg { width: 100%; }
    .ecg-path { fill: none; stroke: rgba(255,255,255,.5); stroke-width: 2; stroke-dasharray: 600; stroke-dashoffset: 600; animation: ecgDraw 1.5s linear infinite; }
    @keyframes ecgDraw { 0%{stroke-dashoffset:600} 100%{stroke-dashoffset:0} }

    /* ── ANALYZING ── */
    #s-analyzing { background: radial-gradient(ellipse at center, #12122a, var(--dark)); }
    .analyzing-ring {
      width: 200px; height: 200px; border-radius: 50%;
      border: 4px solid transparent;
      border-top-color: var(--fire); border-right-color: var(--water);
      animation: spin 1s linear infinite; margin-bottom: 40px;
      box-shadow: var(--glow-r), var(--glow-b); position: relative;
    }
    .analyzing-ring::after {
      content: '❤'; position: absolute; inset: 0;
      display: flex; align-items: center; justify-content: center;
      font-size: 3rem; animation: heartPulse 1s ease-in-out infinite;
    }
    @keyframes spin { to { transform: rotate(360deg); } }
    @keyframes heartPulse {
      0%,100% { transform: scale(1); filter: drop-shadow(0 0 8px var(--fire)); }
      50%      { transform: scale(1.2); filter: drop-shadow(0 0 20px var(--fire)); }
    }
    .analyzing-text { font-size: 1.1rem; font-weight: 600; letter-spacing: 3px; text-transform: uppercase; color: rgba(255,255,255,.8); }
    .analyzing-dots span { animation: dotBlink 1.2s ease-in-out infinite; }
    .analyzing-dots span:nth-child(2) { animation-delay: .2s; }
    .analyzing-dots span:nth-child(3) { animation-delay: .4s; }
    @keyframes dotBlink { 0%,100%{opacity:.2} 50%{opacity:1} }

    /* ── RESULT ── */
    #s-result { background: var(--dark); overflow: hidden; }
    #mist-canvas { position: absolute; inset: 0; pointer-events: none; }
    .result-content { position: relative; z-index: 10; text-align: center; max-width: 720px; width: 90%; }
    .result-sync-display {
      width: 180px; height: 180px; border-radius: 50%; margin: 0 auto 36px;
      background: radial-gradient(circle, rgba(79,195,247,.15), transparent);
      border: 4px solid var(--water); box-shadow: var(--glow-b);
      display: flex; flex-direction: column; align-items: center; justify-content: center;
      animation: resultPulse 2s ease-in-out infinite;
    }
    @keyframes resultPulse {
      0%,100% { box-shadow: var(--glow-b), 0 0 60px rgba(79,195,247,.2); }
      50%      { box-shadow: 0 0 60px rgba(79,195,247,.8), 0 0 100px rgba(79,195,247,.3); }
    }
    .result-pct       { font-size: 2.8rem; font-weight: 900; color: var(--water); }
    .result-pct-label { font-size: .7rem; text-transform: uppercase; letter-spacing: 2px; color: var(--water2); opacity: .8; }
    .result-emoji     { font-size: 2rem; margin-bottom: 12px; }
    .result-headline  {
      font-size: clamp(1.6rem, 3.5vw, 2.4rem); font-weight: 900;
      text-transform: uppercase; letter-spacing: 2px; margin-bottom: 16px;
      background: linear-gradient(135deg, var(--fire), var(--water));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    }
    .result-message {
      font-family: 'Dancing Script', cursive;
      font-size: clamp(1.3rem, 2.5vw, 1.8rem);
      color: rgba(255,255,255,.9); line-height: 1.5; margin-bottom: 36px; font-weight: 600;
    }
    .result-message em { color: var(--water); font-style: normal; }

    /* ── REWARD ── */
    #s-reward { background: radial-gradient(ellipse at top, #0a1a2a, var(--dark)); overflow-y: auto; padding: 40px 20px; }
    .reward-inner  { max-width: 820px; width: 100%; margin: 0 auto; }
    .reward-header { text-align: center; margin-bottom: 40px; }
    .reward-header h2 {
      font-size: clamp(1.5rem, 4vw, 2.5rem); font-weight: 900;
      text-transform: uppercase; letter-spacing: 3px;
      background: linear-gradient(135deg, var(--fire), var(--water));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    }
    .reward-header p { color: rgba(255,255,255,.6); margin-top: 8px; }

    .coupon-card {
      background: linear-gradient(135deg, rgba(255,59,92,.12), rgba(79,195,247,.12));
      border: 2px dashed rgba(255,255,255,.3); border-radius: 20px;
      padding: 36px; text-align: center; margin-bottom: 40px;
      position: relative; overflow: hidden;
    }
    .coupon-card::before, .coupon-card::after {
      content: ''; position: absolute; width: 40px; height: 40px;
      background: var(--dark); border-radius: 50%; top: 50%; transform: translateY(-50%);
    }
    .coupon-card::before { left: -20px; }
    .coupon-card::after  { right: -20px; }
    .coupon-off {
      font-size: clamp(4rem, 10vw, 7rem); font-weight: 900; line-height: 1;
      background: linear-gradient(135deg, var(--fire), var(--water));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    }
    .coupon-label  { font-size: 1rem; text-transform: uppercase; letter-spacing: 4px; color: rgba(255,255,255,.7); margin-bottom: 16px; }
    .coupon-code   { display: inline-block; background: rgba(255,255,255,.1); border: 1px solid rgba(255,255,255,.3); border-radius: 10px; padding: 12px 28px; font-size: 1.4rem; font-weight: 900; letter-spacing: 5px; color: #fff; margin-bottom: 8px; font-family: monospace; }
    .coupon-expiry { font-size: .75rem; color: rgba(255,255,255,.4); }

    .section-title { font-size: 1rem; text-transform: uppercase; letter-spacing: 3px; color: rgba(255,255,255,.5); margin-bottom: 20px; text-align: center; }
    .product-card  { background: var(--card); border: 1px solid rgba(255,255,255,.1); border-radius: 20px; padding: 28px; display: flex; gap: 24px; align-items: center; margin-bottom: 24px; }
    .product-icon  { width: 80px; height: 80px; border-radius: 16px; flex-shrink: 0; background: linear-gradient(135deg, rgba(255,59,92,.3), rgba(79,195,247,.3)); display: flex; align-items: center; justify-content: center; font-size: 2.5rem; border: 1px solid rgba(255,255,255,.15); }
    .product-info h3 { font-size: 1.1rem; font-weight: 700; margin-bottom: 6px; }
    .product-info p  { font-size: .85rem; color: rgba(255,255,255,.6); line-height: 1.6; }
    .product-tags    { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 12px; }
    .tag       { font-size: .72rem; text-transform: uppercase; letter-spacing: 1px; padding: 4px 12px; border-radius: 20px; font-weight: 600; }
    .tag-fire  { background: rgba(255,59,92,.2);  color: var(--fire);  border: 1px solid rgba(255,59,92,.3); }
    .tag-water { background: rgba(79,195,247,.2); color: var(--water); border: 1px solid rgba(79,195,247,.3); }
    .tag-white { background: rgba(255,255,255,.1); color: rgba(255,255,255,.7); border: 1px solid rgba(255,255,255,.2); }

    .features      { display: grid; grid-template-columns: repeat(3, 1fr); gap: 16px; margin-bottom: 40px; }
    .feature-item  { background: var(--card); border: 1px solid rgba(255,255,255,.08); border-radius: 16px; padding: 20px; text-align: center; }
    .feature-icon  { font-size: 1.8rem; margin-bottom: 8px; }
    .feature-title { font-size: .8rem; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 4px; }
    .feature-desc  { font-size: .72rem; color: rgba(255,255,255,.5); line-height: 1.5; }
    .reward-footer { text-align: center; padding-bottom: 20px; }

    .row { display: flex; align-items: center; justify-content: center; gap: 16px; }

    ::-webkit-scrollbar { width: 6px; }
    ::-webkit-scrollbar-track { background: transparent; }
    ::-webkit-scrollbar-thumb { background: rgba(255,255,255,.2); border-radius: 3px; }

    @media (max-width: 768px) {
      #s-game { flex-direction: column; }
      .game-zone { flex: none; height: 40%; width: 100%; flex-direction: row; }
      .game-center { width: 100%; height: 20%; flex-direction: row; }
      .players-row { flex-direction: column; }
      .features { grid-template-columns: 1fr 1fr; }
      .product-card { flex-direction: column; text-align: center; }
    }
    @media (max-width: 480px) {
      .features { grid-template-columns: 1fr; }
      .welcome-center { padding: 36px 28px; }
    }
  </style>
</head>
<body>

<!-- SCREEN 1 — WELCOME -->
<section id="s-welcome" class="screen active">
  <div class="welcome-bg">
    <div class="fire-half" id="fireHalf">
      <div class="flame flame-1"></div>
      <div class="flame flame-2"></div>
      <div class="flame flame-3"></div>
      <div class="flame flame-4"></div>
    </div>
    <div class="water-half" id="waterHalf"></div>
  </div>
  <div class="welcome-center">
    <div class="brand-tag">PlayAh Her Feel presents</div>
    <h1 class="campaign-title">The Heartbeat<br/>Sync</h1>
    <p class="campaign-sub">Discover the invisible thread between two hearts</p>
    <div class="fire-water-divider">
      <div class="divider-line"></div>
      <span class="divider-icon">🔥</span>
      <span class="divider-icon">💧</span>
      <div class="divider-line"></div>
    </div>
    <button class="btn btn-primary" onclick="showScreen('s-instructions')">Begin the Journey</button>
  </div>
</section>

<!-- SCREEN 2 — INSTRUCTIONS -->
<section id="s-instructions" class="screen">
  <h2 class="instr-title">How it works</h2>
  <p class="instr-sub">Tap your button in rhythm — feel each other's pulse</p>
  <div class="players-row">
    <div class="player-card p1">
      <div class="player-num">🔥</div>
      <div class="player-label">Player 1</div>
      <p class="player-desc">Stand on the left side.<br/>Tap your button to the rhythm of your heartbeat.</p>
      <div class="key-hint">Left button / Key [A]</div>
    </div>
    <div class="player-card p2">
      <div class="player-num">💧</div>
      <div class="player-label">Player 2</div>
      <p class="player-desc">Stand on the right side.<br/>Tap your button to the rhythm of your heartbeat.</p>
      <div class="key-hint">Right button / Key [L]</div>
    </div>
  </div>
  <p style="color:rgba(255,255,255,.5);font-size:.85rem;margin-bottom:32px;text-align:center;">
    The session lasts <strong style="color:#fff;">15 seconds</strong>. Stay relaxed and feel the connection.
  </p>
  <div class="row">
    <button class="btn btn-ghost" onclick="showScreen('s-welcome')">← Back</button>
    <button class="btn btn-primary" onclick="startGame()">Start Syncing →</button>
  </div>
</section>

<!-- SCREEN 3 — GAME -->
<section id="s-game" class="screen">
  <div class="game-zone zone-fire">
    <div class="flame-bg-1"></div>
    <span class="player-tap-label">Player 1</span>
    <span class="player-name-game">🔥 Flame</span>
    <button class="tap-btn tap-btn-fire" id="tapBtn1"
      ontouchstart="handleTap(1,event)" onmousedown="handleTap(1,event)">TAP</button>
    <svg class="mini-ecg" viewBox="0 0 180 50">
      <polyline id="ecgLine1" fill="none" stroke="var(--fire)" stroke-width="2.5"
        points="0,25" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
    <span class="tap-count" id="tapCount1">0 taps</span>
  </div>

  <div class="game-center">
    <span class="center-title">Connection</span>
    <div class="timer-circle">
      <svg viewBox="0 0 90 90">
        <circle class="timer-bg" cx="45" cy="45" r="39"/>
        <circle class="timer-ring" id="timerRing" cx="45" cy="45" r="39"/>
      </svg>
      <div class="timer-text" id="timerText">15</div>
    </div>
    <div class="sync-ring-wrap">
      <svg viewBox="0 0 120 120">
        <circle class="sync-bg-ring" cx="60" cy="60" r="53"/>
        <circle class="sync-fill-ring" id="syncRing" cx="60" cy="60" r="53"/>
      </svg>
      <div class="sync-center-label">
        <span class="sync-pct" id="syncPct">0%</span>
        <span class="sync-label">Sync</span>
      </div>
    </div>
    <div class="ecg-line-wrap">
      <svg viewBox="0 0 200 40" height="40">
        <path class="ecg-path"
          d="M0,20 L30,20 L40,20 L45,5 L50,35 L55,20 L65,20 L70,20 L75,10 L80,30 L85,20
             L95,20 L100,20 L105,5 L110,35 L115,20 L125,20 L130,20 L135,10 L140,30 L145,20
             L155,20 L160,20 L165,5 L170,35 L175,20 L200,20"/>
      </svg>
    </div>
  </div>

  <div class="game-zone zone-water">
    <div class="wave-bg"></div>
    <span class="player-tap-label">Player 2</span>
    <span class="player-name-game">💧 Wave</span>
    <button class="tap-btn tap-btn-water" id="tapBtn2"
      ontouchstart="handleTap(2,event)" onmousedown="handleTap(2,event)">TAP</button>
    <svg class="mini-ecg" viewBox="0 0 180 50">
      <polyline id="ecgLine2" fill="none" stroke="var(--water)" stroke-width="2.5"
        points="0,25" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
    <span class="tap-count" id="tapCount2">0 taps</span>
  </div>
</section>

<!-- SCREEN 4 — ANALYZING -->
<section id="s-analyzing" class="screen">
  <div class="analyzing-ring"></div>
  <div class="analyzing-text">
    Analyzing your connection<span class="analyzing-dots"><span>.</span><span>.</span><span>.</span></span>
  </div>
  <p style="color:rgba(255,255,255,.4);margin-top:16px;font-size:.85rem;">
    Measuring the rhythm between your hearts
  </p>
</section>

<!-- SCREEN 5 — RESULT -->
<section id="s-result" class="screen">
  <canvas id="mist-canvas"></canvas>
  <div class="result-content">
    <div class="result-sync-display">
      <div class="result-pct" id="resultPct">—</div>
      <div class="result-pct-label">In Sync</div>
    </div>
    <div class="result-emoji">🌊✨🔥</div>
    <h2 class="result-headline">Your Hearts Are in Sync!</h2>
    <p class="result-message">
      "The rhythm is there — let <em>PlayAh</em> help you maintain the flow."
    </p>
    <div class="row">
      <button class="btn btn-secondary" onclick="showReward()">Claim Your Reward →</button>
    </div>
  </div>
</section>

<!-- SCREEN 6 — REWARD -->
<section id="s-reward" class="screen">
  <div class="reward-inner">
    <div class="reward-header">
      <h2>Your Connection Reward</h2>
      <p>Thank you for syncing your heartbeats with us 💙</p>
    </div>

    <div class="coupon-card">
      <div class="coupon-label">Special Offer for Your Connection</div>
      <div class="coupon-off">20% OFF</div>
      <div style="margin:16px 0;color:rgba(255,255,255,.6);font-size:.9rem;">
        Your next PlayAh Her Feel purchase
      </div>
      <div class="coupon-code" id="couponCode">SYNC-XXXX</div>
      <div class="coupon-expiry">Valid for 30 days · One redemption per couple</div>
    </div>

    <p class="section-title">Introducing PlayAh Her Feel</p>
    <div class="product-card">
      <div class="product-icon">💝</div>
      <div class="product-info">
        <h3>PlayAh Her Feel — Ultra-Thin Sensation Series</h3>
        <p>Engineered for deeper intimacy, PlayAh Her Feel is designed to keep you and your partner feeling every moment of your connection. Because the rhythm you just shared deserves to continue.</p>
        <div class="product-tags">
          <span class="tag tag-water">Ultra-Thin</span>
          <span class="tag tag-fire">Enhanced Sensation</span>
          <span class="tag tag-white">Natural Feel</span>
          <span class="tag tag-water">Water-Based Lubricated</span>
        </div>
      </div>
    </div>

    <div class="features">
      <div class="feature-item">
        <div class="feature-icon">🔥</div>
        <div class="feature-title">Heat-Sync Technology</div>
        <div class="feature-desc">Micro-thin barrier adapts to body heat for a seamless, natural feel.</div>
      </div>
      <div class="feature-item">
        <div class="feature-icon">💧</div>
        <div class="feature-title">Moisture-Flow Formula</div>
        <div class="feature-desc">Premium water-based lubrication keeps the connection smooth and uninterrupted.</div>
      </div>
      <div class="feature-item">
        <div class="feature-icon">❤️</div>
        <div class="feature-title">Sensation Design</div>
        <div class="feature-desc">Shaped to enhance sensation for both partners, amplifying every heartbeat.</div>
      </div>
    </div>

    <div class="reward-footer">
      <p style="color:rgba(255,255,255,.4);font-size:.8rem;margin-bottom:20px;">
        Available at participating pharmacies and online at playah.com
      </p>
      <div class="row" style="flex-wrap:wrap;">
        <button class="btn btn-ghost" onclick="restartGame()">← Play Again</button>
        <button class="btn btn-secondary" onclick="showScreen('s-welcome')">Back to Start</button>
      </div>
    </div>
  </div>
</section>

<script>
const state = {
  p1Taps: [], p2Taps: [],
  gameStart: 0,
  duration: 15000,
  finalSync: 0,
  ecg1Points: [], ecg2Points: [],
};

function showScreen(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

/* Welcome particle effects */
function spawnEmbers() {
  const half = document.getElementById('fireHalf');
  setInterval(() => {
    const e = document.createElement('div');
    e.classList.add('ember');
    const size = Math.random() * 6 + 3;
    e.style.cssText = `width:${size}px;height:${size}px;left:${Math.random()*100}%;animation-duration:${Math.random()*2+1.5}s;--dx:${(Math.random()-.5)*80}px;opacity:${Math.random()*.7+.3};`;
    half.appendChild(e);
    setTimeout(() => e.remove(), 3500);
  }, 300);
}

function spawnWaterFX() {
  const half = document.getElementById('waterHalf');
  setInterval(() => {
    const b = document.createElement('div');
    b.classList.add('bubble');
    const s = Math.random()*20+8;
    b.style.cssText = `width:${s}px;height:${s}px;left:${Math.random()*90}%;bottom:${Math.random()*60}%;animation-duration:${Math.random()*3+2}s;animation-delay:${Math.random()*2}s;`;
    half.appendChild(b);
    setTimeout(() => b.remove(), 6000);
  }, 400);
  setInterval(() => {
    const r = document.createElement('div');
    r.classList.add('ripple');
    const s = Math.random()*40+20;
    r.style.cssText = `width:${s}px;height:${s}px;left:${Math.random()*80}%;top:${Math.random()*80}%;animation-duration:${Math.random()*2+1.5}s;`;
    half.appendChild(r);
    setTimeout(() => r.remove(), 4000);
  }, 700);
}

/* Game */
function startGame() {
  state.p1Taps = []; state.p2Taps = [];
  state.ecg1Points = []; state.ecg2Points = [];
  state.gameStart = Date.now();
  state.finalSync = 0;
  document.getElementById('tapCount1').textContent = '0 taps';
  document.getElementById('tapCount2').textContent = '0 taps';
  document.getElementById('syncPct').textContent = '0%';
  document.getElementById('ecgLine1').setAttribute('points','0,25');
  document.getElementById('ecgLine2').setAttribute('points','0,25');
  setSyncRing(0);
  showScreen('s-game');
  runGameLoop();
}

function runGameLoop() {
  const iv = setInterval(() => {
    const elapsed = Date.now() - state.gameStart;
    const remaining = Math.max(0, Math.ceil((state.duration - elapsed) / 1000));
    updateTimer(remaining, elapsed);
    const sync = computeSync(elapsed);
    setSyncRing(sync);
    document.getElementById('syncPct').textContent = Math.round(sync) + '%';
    if (elapsed >= state.duration) { clearInterval(iv); endGame(sync); }
  }, 100);
}

function updateTimer(remaining, elapsed) {
  document.getElementById('timerText').textContent = remaining;
  const ring = document.getElementById('timerRing');
  ring.style.strokeDashoffset = 245 * (elapsed / state.duration);
  ring.style.stroke = remaining <= 5 ? 'var(--fire)' : remaining <= 10 ? 'var(--water)' : '#fff';
}

function handleTap(player, e) {
  e.preventDefault();
  if (Date.now() - state.gameStart > state.duration) return;
  const now = Date.now();
  if (player === 1) {
    state.p1Taps.push(now);
    document.getElementById('tapCount1').textContent = state.p1Taps.length + ' taps';
  } else {
    state.p2Taps.push(now);
    document.getElementById('tapCount2').textContent = state.p2Taps.length + ' taps';
  }
  flashBtn(player);
  appendECGSpike(player);
}

function flashBtn(player) {
  const btn = document.getElementById('tapBtn' + player);
  btn.classList.add('tapped');
  setTimeout(() => btn.classList.remove('tapped'), 300);
}

function appendECGSpike(player) {
  const line = document.getElementById('ecgLine' + player);
  const elapsed = (Date.now() - state.gameStart) / state.duration;
  const x = elapsed * 180;
  const arr = player === 1 ? state.ecg1Points : state.ecg2Points;
  arr.push({x:x-6,y:25},{x:x-3,y:7},{x:x,y:39},{x:x+3,y:25});
  line.setAttribute('points', '0,25 ' + arr.map(p=>`${p.x.toFixed(1)},${p.y.toFixed(1)}`).join(' '));
}

function computeSync(elapsed) {
  const t = elapsed / state.duration;
  return Math.min(100, 20 + 52 * t + tapSyncBonus());
}

function tapSyncBonus() {
  if (state.p1Taps.length < 2 || state.p2Taps.length < 2) return 0;
  const b1 = getBPM(state.p1Taps), b2 = getBPM(state.p2Taps);
  if (!b1 || !b2) return 0;
  return Math.max(0, 1 - Math.abs(b1-b2)/((b1+b2)/2)) * 28;
}

function getBPM(taps) {
  if (taps.length < 2) return 0;
  const ivs = taps.slice(1).map((t,i) => t - taps[i]);
  const avg = ivs.reduce((a,b)=>a+b,0) / ivs.length;
  return avg > 0 ? 60000 / avg : 0;
}

function setSyncRing(pct) {
  const ring = document.getElementById('syncRing');
  ring.style.strokeDashoffset = 333 * (1 - pct / 100);
  const r = Math.round(255 - (255-79)*(pct/100));
  const g = Math.round(59  + (195-59)*(pct/100));
  const b = Math.round(92  + (247-92)*(pct/100));
  ring.style.stroke = `rgb(${r},${g},${b})`;
}

function endGame(sync) {
  state.finalSync = Math.max(78, Math.round(sync));
  showScreen('s-analyzing');
  setTimeout(() => {
    document.getElementById('resultPct').textContent = state.finalSync + '%';
    showScreen('s-result');
    startMistEffect();
  }, 3200);
}

/* Mist canvas */
let mistRAF;
function startMistEffect() {
  const canvas = document.getElementById('mist-canvas');
  const ctx = canvas.getContext('2d');
  const particles = [];
  function resize() { canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
  resize();
  window.addEventListener('resize', resize);
  function spawn() {
    particles.push({
      x: Math.random()*canvas.width, y: canvas.height+10,
      r: Math.random()*8+3, vx:(Math.random()-.5)*1.5, vy:-(Math.random()*2+1),
      alpha: Math.random()*.6+.2, hue: Math.random()*30+185,
    });
  }
  const si = setInterval(spawn, 40);
  function tick() {
    ctx.clearRect(0,0,canvas.width,canvas.height);
    for (let i = particles.length-1; i >= 0; i--) {
      const p = particles[i];
      p.x += p.vx; p.y += p.vy; p.alpha -= 0.004;
      if (p.alpha <= 0 || p.y < -20) { particles.splice(i,1); continue; }
      ctx.beginPath();
      ctx.arc(p.x, p.y, p.r, 0, Math.PI*2);
      ctx.fillStyle = `hsla(${p.hue},80%,75%,${p.alpha})`;
      ctx.fill();
    }
    mistRAF = requestAnimationFrame(tick);
  }
  if (mistRAF) cancelAnimationFrame(mistRAF);
  tick();
  setTimeout(() => {
    clearInterval(si);
    setTimeout(() => { cancelAnimationFrame(mistRAF); ctx.clearRect(0,0,canvas.width,canvas.height); }, 4000);
  }, 8000);
}

/* Reward */
function showReward() {
  const chars = 'ABCDEFGHJKLMNPQRSTUVWXYZ23456789';
  let code = 'SYNC-';
  for (let i = 0; i < 6; i++) code += chars[Math.floor(Math.random()*chars.length)];
  document.getElementById('couponCode').textContent = code;
  showScreen('s-reward');
}

function restartGame() { showScreen('s-instructions'); }

/* Keyboard */
document.addEventListener('keydown', e => {
  if (!document.getElementById('s-game').classList.contains('active')) return;
  if (e.key.toLowerCase()==='a' || e.key==='ArrowLeft')  handleTap(1,{preventDefault:()=>{}});
  if (e.key.toLowerCase()==='l' || e.key==='ArrowRight') handleTap(2,{preventDefault:()=>{}});
});

spawnEmbers();
spawnWaterFX();
</script>
</body>
</html>

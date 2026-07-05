<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ratio — The Irrational Numbers Game</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,600;9..144,700&family=Inter:wght@400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg-deep:#0a0e1b;
    --bg-surface:#131a2e;
    --bg-surface-2:#1b2440;
    --border:rgba(255,255,255,0.08);
    --text-primary:#eceff7;
    --text-muted:#8b93ad;
    --gold:#f2c14e;
    --teal:#59d8c9;
    --rose:#ff6b81;
    --shadow:0 20px 60px rgba(0,0,0,0.45);
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:
      radial-gradient(ellipse at 20% -10%, rgba(89,216,201,0.10), transparent 45%),
      radial-gradient(ellipse at 90% 10%, rgba(242,193,78,0.08), transparent 40%),
      var(--bg-deep);
    color:var(--text-primary);
    font-family:'Inter', sans-serif;
    min-height:100vh;
    overflow-x:hidden;
  }
  h1,h2,h3,.display{font-family:'Fraunces', serif;}
  .mono{font-family:'Space Mono', monospace;}
  a{color:inherit;}

  /* ---------- NAV ---------- */
  nav{
    position:sticky; top:0; z-index:200;
    display:flex; align-items:center; justify-content:space-between;
    padding:18px 40px;
    background:rgba(10,14,27,0.75);
    backdrop-filter:blur(14px);
    border-bottom:1px solid var(--border);
  }
  .brand{display:flex; align-items:center; gap:10px; font-family:'Fraunces',serif; font-size:22px; font-weight:600; letter-spacing:0.5px;}
  .brand .glyph{
    display:inline-flex; align-items:center; justify-content:center;
    width:34px; height:34px; border-radius:10px;
    background:linear-gradient(135deg, var(--teal), var(--gold));
    color:#0a0e1b; font-family:'Space Mono',monospace; font-weight:700; font-size:18px;
  }
  .nav-links{display:flex; gap:12px; align-items:center;}
  .btn{
    font-family:'Inter', sans-serif; font-weight:600; font-size:14.5px;
    padding:10px 20px; border-radius:10px; border:1px solid var(--border);
    background:var(--bg-surface-2); color:var(--text-primary);
    cursor:pointer; transition:transform .15s ease, background .2s ease, border-color .2s ease, box-shadow .2s ease;
  }
  .btn:hover{transform:translateY(-2px); border-color:rgba(255,255,255,0.2);}
  .btn-primary{background:linear-gradient(135deg, var(--teal), #3fb6a8); color:#06231f; border:none;}
  .btn-primary:hover{box-shadow:0 8px 24px rgba(89,216,201,0.35);}
  .btn-gold{background:linear-gradient(135deg, var(--gold), #d99f2b); color:#2b1c00; border:none;}
  .btn-gold:hover{box-shadow:0 8px 24px rgba(242,193,78,0.35);}
  .btn-ghost{background:transparent;}
  .btn-danger{background:rgba(255,107,129,0.15); border:1px solid rgba(255,107,129,0.4); color:var(--rose);}
  .btn:active{transform:translateY(0);}

  /* ---------- HERO ---------- */
  .hero{
    position:relative;
    max-width:1180px; margin:0 auto; padding:90px 40px 60px;
    display:grid; grid-template-columns:1.1fr 0.9fr; gap:50px; align-items:center;
  }
  .eyebrow{
    display:inline-block; font-family:'Space Mono',monospace; font-size:12.5px; letter-spacing:2px;
    text-transform:uppercase; color:var(--teal); padding:6px 12px; border:1px solid rgba(89,216,201,0.35);
    border-radius:100px; margin-bottom:18px; background:rgba(89,216,201,0.06);
  }
  .hero h1{font-size:52px; line-height:1.08; font-weight:600; margin-bottom:20px;}
  .hero h1 em{font-style:normal; color:var(--gold);}
  .hero p.lead{color:var(--text-muted); font-size:17px; line-height:1.7; margin-bottom:30px; max-width:520px;}
  .hero-ctas{display:flex; gap:14px;}

  /* orbit signature element */
  .orbit-wrap{position:relative; width:100%; aspect-ratio:1/1; max-width:420px; margin:0 auto;}
  .orbit-core{
    position:absolute; top:50%; left:50%; transform:translate(-50%,-50%);
    width:110px; height:110px; border-radius:50%;
    background:radial-gradient(circle at 35% 30%, #fff7e0, var(--gold) 55%, #a97a1c 100%);
    box-shadow:0 0 60px rgba(242,193,78,0.55), inset 0 0 30px rgba(255,255,255,0.4);
    display:flex; align-items:center; justify-content:center;
    font-family:'Space Mono',monospace; font-size:28px; font-weight:700; color:#2b1c00;
    animation:pulse-core 3.5s ease-in-out infinite;
  }
  @keyframes pulse-core{0%,100%{box-shadow:0 0 60px rgba(242,193,78,0.55), inset 0 0 30px rgba(255,255,255,0.4);}50%{box-shadow:0 0 90px rgba(242,193,78,0.85), inset 0 0 40px rgba(255,255,255,0.55);}}
  .ring{position:absolute; top:50%; left:50%; border:1px dashed rgba(89,216,201,0.35); border-radius:50%; transform:translate(-50%,-50%);}
  .ring1{width:220px; height:220px; animation:spin 18s linear infinite;}
  .ring2{width:320px; height:320px; animation:spin 26s linear infinite reverse;}
  .ring3{width:400px; height:400px; animation:spin 34s linear infinite;}
  @keyframes spin{from{transform:translate(-50%,-50%) rotate(0deg);}to{transform:translate(-50%,-50%) rotate(360deg);}}
  .orbiter{
    position:absolute; top:-13px; left:50%; transform:translateX(-50%);
    width:34px; height:34px; border-radius:50%; background:var(--bg-surface-2);
    border:1px solid var(--border); display:flex; align-items:center; justify-content:center;
    font-family:'Space Mono',monospace; font-size:12.5px; color:var(--teal);
  }
  .ring2 .orbiter{color:var(--rose);}
  .ring3 .orbiter{color:var(--gold);}

  section{max-width:1180px; margin:0 auto; padding:70px 40px;}
  section h2{font-size:32px; font-weight:600; margin-bottom:14px;}
  .section-tag{font-family:'Space Mono',monospace; font-size:12px; letter-spacing:2px; text-transform:uppercase; color:var(--gold); margin-bottom:10px; display:block;}
  .card-grid{display:grid; grid-template-columns:repeat(3,1fr); gap:22px; margin-top:30px;}
  .info-card{
    background:var(--bg-surface); border:1px solid var(--border); border-radius:16px; padding:26px;
    transition:transform .2s ease, border-color .2s ease;
  }
  .info-card:hover{transform:translateY(-4px); border-color:rgba(89,216,201,0.3);}
  .info-card .num{font-family:'Space Mono',monospace; color:var(--teal); font-size:13px; margin-bottom:10px; display:block;}
  .info-card h3{font-size:18px; margin-bottom:10px; font-weight:600;}
  .info-card p{color:var(--text-muted); font-size:14.5px; line-height:1.65;}

  .prose{color:var(--text-muted); font-size:15.5px; line-height:1.85; max-width:820px;}
  .prose strong{color:var(--text-primary);}
  .prose .formula{
    display:inline-block; font-family:'Space Mono',monospace; background:var(--bg-surface-2);
    border:1px solid var(--border); padding:2px 8px; border-radius:6px; color:var(--gold); margin:0 2px;
  }
  .pi-symbol{
    font-family:'Fraunces',serif; font-size:120px; float:right; margin:-20px 0 20px 30px; color:var(--gold);
    opacity:0.9; line-height:1;
  }
  .divider{height:1px; background:linear-gradient(90deg, transparent, var(--border), transparent); margin:50px 0;}

  .howto-steps{display:grid; grid-template-columns:repeat(4,1fr); gap:18px; margin-top:30px;}
  .step{background:var(--bg-surface); border:1px solid var(--border); border-radius:16px; padding:22px; position:relative;}
  .step .stepno{
    font-family:'Space Mono',monospace; font-size:26px; font-weight:700; color:var(--teal); opacity:0.5; display:block; margin-bottom:8px;
  }
  .step h3{font-size:15.5px; margin-bottom:8px;}
  .step p{color:var(--text-muted); font-size:13.5px; line-height:1.6;}
  .step .example{
    margin-top:10px; font-family:'Space Mono',monospace; font-size:13px; background:var(--bg-surface-2);
    padding:8px 10px; border-radius:8px; color:var(--gold); border:1px solid var(--border);
  }

  /* Leaderboard */
  .board{background:var(--bg-surface); border:1px solid var(--border); border-radius:18px; overflow:hidden; margin-top:26px;}
  .board table{width:100%; border-collapse:collapse;}
  .board th{text-align:left; font-family:'Space Mono',monospace; font-size:12px; text-transform:uppercase; letter-spacing:1.5px; color:var(--text-muted); padding:14px 20px; border-bottom:1px solid var(--border);}
  .board td{padding:13px 20px; border-bottom:1px solid var(--border); font-size:14.5px;}
  .board tr:last-child td{border-bottom:none;}
  .board tr:hover td{background:rgba(255,255,255,0.02);}
  .rank-badge{
    display:inline-flex; align-items:center; justify-content:center; width:26px; height:26px; border-radius:8px;
    font-family:'Space Mono',monospace; font-size:12.5px; font-weight:700; background:var(--bg-surface-2); color:var(--text-muted);
  }
  .rank-badge.gold{background:linear-gradient(135deg,var(--gold),#d99f2b); color:#2b1c00;}
  .rank-badge.silver{background:linear-gradient(135deg,#dfe6f0,#a9b3c4); color:#1a1f2c;}
  .rank-badge.bronze{background:linear-gradient(135deg,#d99a63,#a5622c); color:#2b1400;}
  .empty-row td{color:var(--text-muted); text-align:center; padding:30px; font-style:italic;}

  footer{text-align:center; padding:40px; color:var(--text-muted); font-size:13px; border-top:1px solid var(--border);}

  /* ---------- MODAL (auth) ---------- */
  .overlay{
    position:fixed; inset:0; background:rgba(5,7,14,0.72); backdrop-filter:blur(6px);
    display:flex; align-items:center; justify-content:center; z-index:1000;
    opacity:0; pointer-events:none; transition:opacity .25s ease;
  }
  .overlay.show{opacity:1; pointer-events:auto;}
  .modal{
    background:var(--bg-surface); border:1px solid var(--border); border-radius:20px; padding:36px;
    width:100%; max-width:420px; box-shadow:var(--shadow); transform:scale(0.94); transition:transform .25s ease;
    position:relative;
  }
  .overlay.show .modal{transform:scale(1);}
  .modal h2{font-size:24px; margin-bottom:6px;}
  .modal .sub{color:var(--text-muted); font-size:13.5px; margin-bottom:24px;}
  .field{margin-bottom:16px;}
  .field label{display:block; font-size:12.5px; color:var(--text-muted); margin-bottom:6px; font-family:'Space Mono',monospace; letter-spacing:0.5px;}
  .field input{
    width:100%; padding:12px 14px; border-radius:10px; border:1px solid var(--border);
    background:var(--bg-deep); color:var(--text-primary); font-size:14.5px; outline:none;
    transition:border-color .2s ease;
  }
  .field input:focus{border-color:var(--teal);}
  .modal .tabs{display:flex; gap:8px; margin-bottom:22px; background:var(--bg-deep); padding:4px; border-radius:10px;}
  .modal .tab{flex:1; text-align:center; padding:9px; border-radius:8px; cursor:pointer; font-size:13.5px; font-weight:600; color:var(--text-muted); transition:all .2s ease;}
  .modal .tab.active{background:var(--bg-surface-2); color:var(--text-primary);}
  .close-x{position:absolute; top:18px; right:18px; background:none; border:none; color:var(--text-muted); font-size:20px; cursor:pointer;}
  .close-x:hover{color:var(--text-primary);}
  .form-error{color:var(--rose); font-size:13px; margin-bottom:12px; display:none;}
  .full-w{width:100%;}

  /* ---------- PROFILE SLIDE PANEL ---------- */
  .slide-panel{
    position:fixed; top:0; right:0; height:100%; width:380px; max-width:90vw;
    background:var(--bg-surface); border-left:1px solid var(--border); z-index:900;
    transform:translateX(100%); transition:transform .35s cubic-bezier(.16,.84,.44,1);
    padding:36px 30px; overflow-y:auto; box-shadow:-20px 0 60px rgba(0,0,0,0.4);
  }
  .slide-panel.open{transform:translateX(0);}
  .slide-backdrop{
    position:fixed; inset:0; background:rgba(5,7,14,0.5); z-index:890; opacity:0; pointer-events:none; transition:opacity .3s ease;
  }
  .slide-backdrop.show{opacity:1; pointer-events:auto;}
  .avatar-big{
    width:70px; height:70px; border-radius:50%; background:linear-gradient(135deg,var(--teal),var(--gold));
    display:flex; align-items:center; justify-content:center; font-family:'Fraunces',serif; font-size:28px; color:#0a0e1b; margin-bottom:16px;
  }
  .profile-field{margin-bottom:18px; padding-bottom:18px; border-bottom:1px solid var(--border);}
  .profile-field label{display:block; font-size:11.5px; text-transform:uppercase; letter-spacing:1px; color:var(--text-muted); font-family:'Space Mono',monospace; margin-bottom:5px;}
  .profile-field .val{font-size:15px; word-break:break-all;}
  .stat-grid{display:grid; grid-template-columns:repeat(3,1fr); gap:10px; margin:20px 0 26px;}
  .stat-box{background:var(--bg-surface-2); border-radius:12px; padding:14px 8px; text-align:center;}
  .stat-box .n{font-family:'Space Mono',monospace; font-size:20px; font-weight:700;}
  .stat-box .l{font-size:10.5px; color:var(--text-muted); text-transform:uppercase; letter-spacing:0.5px; margin-top:2px;}
  .stat-box.correct .n{color:var(--teal);} .stat-box.wrong .n{color:var(--rose);} .stat-box.total .n{color:var(--gold);}

  /* ---------- SUPPORT POPUP ---------- */
  .support-popup{
    position:fixed; bottom:20px; left:20px; width:320px; background:var(--bg-surface);
    border:1px solid var(--border); border-radius:16px; box-shadow:var(--shadow); z-index:800;
    transform:translateY(20px) scale(0.96); opacity:0; pointer-events:none; transition:all .25s ease;
    padding:20px;
  }
  .support-popup.show{transform:translateY(0) scale(1); opacity:1; pointer-events:auto;}
  .support-popup h3{font-size:16px; margin-bottom:4px;}
  .support-popup .sub{color:var(--text-muted); font-size:12.5px; margin-bottom:14px;}
  .support-popup textarea{
    width:100%; min-height:90px; resize:vertical; border-radius:10px; border:1px solid var(--border);
    background:var(--bg-deep); color:var(--text-primary); padding:10px 12px; font-size:13.5px; font-family:'Inter',sans-serif; outline:none; margin-bottom:12px;
  }
  .support-popup textarea:focus{border-color:var(--teal);}
  .support-header{display:flex; justify-content:space-between; align-items:flex-start;}

  /* ---------- TOAST ---------- */
  .toast-wrap{position:fixed; bottom:26px; left:50%; transform:translateX(-50%); z-index:2000; display:flex; flex-direction:column; gap:10px; align-items:center;}
  .toast{
    background:var(--bg-surface-2); border:1px solid var(--border); padding:12px 22px; border-radius:10px;
    font-size:13.5px; box-shadow:0 10px 30px rgba(0,0,0,0.4); min-width:220px; text-align:center;
    animation:toast-in .3s ease, toast-out .3s ease 2.7s forwards;
  }
  .toast.success{border-color:rgba(89,216,201,0.5); color:var(--teal);}
  .toast.error{border-color:rgba(255,107,129,0.5); color:var(--rose);}
  .toast.info{border-color:rgba(242,193,78,0.5); color:var(--gold);}
  @keyframes toast-in{from{opacity:0; transform:translateY(14px);}to{opacity:1; transform:translateY(0);}}
  @keyframes toast-out{to{opacity:0; transform:translateY(-8px);}}

  /* ---------- GAME PAGE ---------- */
  .game-page{
    position:fixed; inset:0; z-index:1500; background:
      radial-gradient(ellipse at 15% 0%, rgba(89,216,201,0.12), transparent 45%),
      radial-gradient(ellipse at 85% 100%, rgba(255,107,129,0.10), transparent 45%),
      #070a14;
    display:none; flex-direction:column; align-items:center; padding:30px 20px; overflow-y:auto;
  }
  .game-page.show{display:flex;}
  .game-topbar{width:100%; max-width:900px; display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;}
  .game-topbar .quit{background:none; border:none; color:var(--text-muted); font-size:14px; cursor:pointer;}
  .game-topbar .quit:hover{color:var(--rose);}
  .timer-wrap{width:100%; max-width:900px; margin-bottom:24px;}
  .timer-bar-bg{height:8px; border-radius:100px; background:var(--bg-surface-2); overflow:hidden; border:1px solid var(--border);}
  .timer-bar-fill{height:100%; width:100%; background:linear-gradient(90deg,var(--teal),var(--gold)); transition:width 1s linear;}
  .timer-num{text-align:center; font-family:'Space Mono',monospace; font-size:14px; color:var(--text-muted); margin-top:8px;}
  .scoreboard{display:flex; gap:16px; margin-bottom:30px;}
  .score-pill{
    background:var(--bg-surface); border:1px solid var(--border); border-radius:16px; padding:14px 30px; text-align:center; min-width:140px;
  }
  .score-pill .lab{font-size:11px; text-transform:uppercase; letter-spacing:1.5px; color:var(--text-muted); font-family:'Space Mono',monospace;}
  .score-pill .v{font-family:'Fraunces',serif; font-size:32px; font-weight:600; margin-top:4px;}
  .score-pill.score .v{color:var(--teal);}
  .score-pill.best .v{color:var(--gold);}

  .board-area{display:flex; gap:24px; align-items:flex-start; flex-wrap:wrap; justify-content:center; width:100%; max-width:900px;}
  .radical-grid{display:grid; grid-template-columns:repeat(4,1fr); gap:14px; flex:1; min-width:300px; max-width:520px;}
  .rcell{
    aspect-ratio:1/1; background:var(--bg-surface); border:1.5px solid var(--border); border-radius:16px;
    display:flex; align-items:center; justify-content:center; font-family:'Space Mono',monospace; font-size:22px;
    cursor:pointer; user-select:none; position:relative; transition:transform .15s ease, border-color .2s ease, background .2s ease;
  }
  .rcell:hover{transform:translateY(-3px); border-color:rgba(89,216,201,0.4);}
  .rcell.selected{border-color:var(--teal); background:rgba(89,216,201,0.12); box-shadow:0 0 24px rgba(89,216,201,0.35); transform:translateY(-3px);}
  .rcell.correct{animation:snap-correct .5s ease;}
  .rcell.wrong{animation:shake-wrong .45s ease;}
  @keyframes snap-correct{
    0%{box-shadow:0 0 0 rgba(242,193,78,0);}
    40%{box-shadow:0 0 40px rgba(242,193,78,0.9); background:rgba(242,193,78,0.25); border-color:var(--gold); transform:scale(1.08);}
    100%{box-shadow:0 0 0 rgba(242,193,78,0); transform:scale(1);}
  }
  @keyframes shake-wrong{
    0%,100%{transform:translateX(0);} 20%{transform:translateX(-8px);} 40%{transform:translateX(8px);} 60%{transform:translateX(-6px);} 80%{transform:translateX(6px);}
  }
  .op-strip{display:flex; flex-direction:row; md-flex-direction:column; gap:14px; flex-wrap:wrap; justify-content:center;}
  .ocell{
    width:76px; height:76px; background:var(--bg-surface-2); border:1.5px solid var(--border); border-radius:16px;
    display:flex; align-items:center; justify-content:center; font-size:28px; cursor:pointer; color:var(--gold);
    transition:transform .15s ease, border-color .2s ease;
  }
  .ocell:hover{transform:translateY(-3px);}
  .ocell.selected{border-color:var(--gold); background:rgba(242,193,78,0.15); box-shadow:0 0 24px rgba(242,193,78,0.35); transform:translateY(-3px);}
  .feedback-line{
    margin-top:26px; min-height:26px; font-family:'Space Mono',monospace; font-size:15px; text-align:center; transition:color .2s ease;
  }
  .hint-line{color:var(--text-muted); font-size:13px; margin-top:10px; text-align:center;}

  /* ---------- RESULTS ---------- */
  .results-overlay{
    position:fixed; inset:0; z-index:1600; background:rgba(5,7,14,0.85); backdrop-filter:blur(8px);
    display:none; align-items:center; justify-content:center;
  }
  .results-overlay.show{display:flex;}
  .results-card{
    background:var(--bg-surface); border:1px solid var(--border); border-radius:24px; padding:44px; width:100%; max-width:440px;
    text-align:center; box-shadow:var(--shadow); animation:pop-in .4s cubic-bezier(.2,.9,.3,1.2);
  }
  @keyframes pop-in{from{opacity:0; transform:scale(0.85) translateY(20px);}to{opacity:1; transform:scale(1) translateY(0);}}
  .results-card h2{font-size:26px; margin-bottom:6px;}
  .results-card .sub{color:var(--text-muted); font-size:13.5px; margin-bottom:26px;}
  .results-stats{display:grid; grid-template-columns:repeat(3,1fr); gap:12px; margin-bottom:26px;}
  .results-actions{display:flex; gap:12px;}
  .results-actions .btn{flex:1;}

  /* ---------- ADMIN ---------- */
  .admin-list{max-height:420px; overflow-y:auto; margin-top:18px; display:flex; flex-direction:column; gap:12px;}
  .admin-msg{background:var(--bg-surface-2); border:1px solid var(--border); border-radius:12px; padding:14px 16px;}
  .admin-msg .meta{font-family:'Space Mono',monospace; font-size:11.5px; color:var(--teal); margin-bottom:6px;}
  .admin-msg .txt{font-size:14px; line-height:1.5;}

  @media(max-width:860px){
    .hero{grid-template-columns:1fr; padding-top:50px;}
    .card-grid{grid-template-columns:1fr;}
    .howto-steps{grid-template-columns:repeat(2,1fr);}
    .board-area{flex-direction:column; align-items:center;}
    .op-strip{flex-direction:row;}
    nav{padding:14px 18px;}
    section{padding:50px 20px;}
    .pi-symbol{float:none; display:block; text-align:center; margin:0 0 10px;}
  }
</style>
</head>
<body>

<!-- ===================== NAV ===================== -->
<nav>
  <div class="brand"><span class="glyph">√</span> Ratio</div>
  <div class="nav-links">
    <button class="btn btn-ghost" onclick="openSupport()">Support</button>
    <button class="btn btn-ghost" onclick="scrollToAbout()">About Us</button>
    <button class="btn btn-ghost" id="nav-admin-btn" style="display:none;" onclick="openAdmin()">Admin Panel</button>
    <button class="btn btn-gold" id="nav-auth-btn" onclick="openAuth()">Login / Register</button>
    <button class="btn btn-primary" id="nav-home-btn" style="display:none;" onclick="openProfile()">Home</button>
  </div>
</nav>

<!-- ===================== HERO ===================== -->
<div class="hero">
  <div>
    <span class="eyebrow">30 seconds · pure arithmetic instinct</span>
    <h1>Turn <em>irrational</em> chaos into <em>rational</em> order.</h1>
    <p class="lead">Ratio is a fast-paced math puzzle. A board full of square roots stares back at you — your job is to pair them with the right operation before the clock hits zero and collapse them into whole, rational numbers.</p>
    <div class="hero-ctas">
      <button class="btn btn-primary" style="padding:14px 30px; font-size:15.5px;" onclick="handleStart()">▶ Start Playing</button>
      <button class="btn btn-ghost" style="padding:14px 24px; font-size:15.5px;" onclick="scrollToHowTo()">How it works</button>
    </div>
  </div>
  <div class="orbit-wrap">
    <div class="ring ring1"><div class="orbiter mono">√2</div></div>
    <div class="ring ring2"><div class="orbiter mono">√7</div></div>
    <div class="ring ring3"><div class="orbiter mono">√5</div></div>
    <div class="orbit-core mono">π</div>
  </div>
</div>

<!-- ===================== LEADERBOARD ===================== -->
<section id="leaderboard">
  <span class="section-tag">Hall of Rational Minds</span>
  <h2>Top 10 Players</h2>
  <div class="board">
    <table>
      <thead><tr><th>Rank</th><th>Player</th><th>Best Score</th></tr></thead>
      <tbody id="leaderboard-body">
        <tr class="empty-row"><td colspan="3">No scores yet — be the first to set a record.</td></tr>
      </tbody>
    </table>
  </div>
</section>

<!-- ===================== ABOUT / EXPLAINERS ===================== -->
<section id="about">
  <span class="section-tag">About Us</span>
  <h2>Why irrational numbers?</h2>
  <p class="prose">Ratio was built for anyone who loves the quiet strangeness of numbers that never quite resolve. We think mental math is more fun when it feels like a puzzle instead of a worksheet — so we turned one of the oldest ideas in mathematics, the irrational number, into a 30-second sport.</p>

  <div class="divider"></div>

  <span class="section-tag">The Mathematics</span>
  <h2>What is an irrational number?</h2>
  <p class="prose">
    An <strong>irrational number</strong> is a real number that cannot be written as a simple fraction <span class="formula">a / b</span> of two integers, where <span class="formula">b ≠ 0</span>. Written as a decimal, an irrational number goes on forever without ever settling into a repeating pattern — no matter how far you calculate, new, unpredictable digits keep appearing.
    <br><br>
    This is different from a <strong>rational number</strong>, which can always be expressed as a fraction of integers — like <span class="formula">1/2</span>, <span class="formula">3</span>, or <span class="formula">-7/4</span> — and whose decimal form either ends or repeats forever in a fixed cycle, like <span class="formula">0.333...</span>
    <br><br>
    The most familiar irrational numbers come from <strong>square roots</strong>. The square root of a number <span class="formula">n</span>, written <span class="formula">√n</span>, is the value that multiplies by itself to give <span class="formula">n</span>. When <span class="formula">n</span> is a "perfect square" like 4, 9, 16, or 25, its square root is a whole number — <span class="formula">√16 = 4</span> — and is therefore rational. But when <span class="formula">n</span> is not a perfect square, such as 2, 3, 5, 7, or 8, its square root is irrational: <span class="formula">√2 = 1.41421356...</span> continues forever with no repeating pattern.
    <br><br>
    Irrational numbers were unsettling to the ancient Greeks, who believed all numbers could be expressed as ratios of whole numbers. Legend holds that Hippasus of Metapontum was the first to prove that <span class="formula">√2</span> could not be written as a fraction — a discovery so disruptive to Pythagorean philosophy that the story says he was drowned at sea for revealing it. True or not, the tale captures just how radical the idea once was.
    <br><br>
    This game is built entirely around one elegant fact: while a single square root is usually irrational, <strong>combining two of them with the right operation can cancel the irrationality out</strong> and produce a clean, rational result. That moment of cancellation is the entire game.
  </p>

  <div class="divider"></div>

  <div>
    <span class="pi-symbol">π</span>
    <span class="section-tag">The Most Famous Irrational Number</span>
    <h2>Understanding Pi (π)</h2>
    <p class="prose">
      <strong>Pi (π)</strong> is the ratio of a circle's circumference to its diameter — for every circle in existence, no matter its size, dividing the distance around it by the distance across it always gives the exact same number: approximately <span class="formula">3.14159265358979...</span>
      <br><br>
      Pi is both <strong>irrational</strong> and <strong>transcendental</strong>. Irrational means it cannot be written as a fraction of two integers. Transcendental means it is not the root of any polynomial equation with rational coefficients — it isn't just "hard to express," it lives outside the entire system of numbers that can be built from algebra alone. This was proven by the mathematician Ferdinand von Lindemann in 1882, which also finally settled the ancient problem of "squaring the circle": it showed that it's mathematically impossible to construct a square with the same area as a given circle using only a compass and straightedge.
      <br><br>
      Pi appears throughout geometry, trigonometry, physics, and engineering — anywhere circles, waves, or periodic motion show up. Its digits have been calculated to trillions of places using supercomputers, purely because mathematicians find the never-ending, never-repeating pattern endlessly fascinating. Even though we only ever need a handful of its digits for real-world engineering, chasing more of them has become a benchmark for computing power itself.
      <br><br>
      In Ratio, π doesn't appear directly on the board — but it's the spiritual ancestor of every square root you'll see. Every √n on your grid shares pi's defining trait: an infinite, non-repeating decimal expansion that hides in plain sight until the right operation exposes it.
    </p>
  </div>
</section>

<!-- ===================== HOW TO PLAY ===================== -->
<section id="howto">
  <span class="section-tag">Gameplay</span>
  <h2>How to play Ratio</h2>
  <p class="prose">You have <strong>30 seconds</strong>. The board shows a 4×4 grid of square roots and a strip of four operations. Your goal: select two square roots and one operation that together produce a rational number.</p>
  <div class="howto-steps">
    <div class="step">
      <span class="stepno">01</span>
      <h3>Log in to play</h3>
      <p>Create a free account or log in. Your scores, stats, and leaderboard rank are all tied to your account.</p>
    </div>
    <div class="step">
      <span class="stepno">02</span>
      <h3>Pick two radicals</h3>
      <p>Click any two cells in the 4×4 grid of square roots. The order you click them in matters for subtraction and division.</p>
      <div class="example">√8 then √2</div>
    </div>
    <div class="step">
      <span class="stepno">03</span>
      <h3>Choose an operation</h3>
      <p>Click ×, +, −, or ÷ from the strip beside the grid to apply it to your two selected numbers.</p>
      <div class="example">√8 × √2 = √16</div>
    </div>
    <div class="step">
      <span class="stepno">04</span>
      <h3>Score on rational results</h3>
      <p>If the result is rational (a whole, clean number), you score a point and the board refreshes. If not, try a new pair before time runs out.</p>
      <div class="example">√16 = 4 ✓ Rational!</div>
    </div>
  </div>
  <p class="prose" style="margin-top:26px;">
    A quick trick: multiplication and division combine radicals by combining what's under the root — <span class="formula">√a × √b = √(a·b)</span> and <span class="formula">√a ÷ √b = √(a÷b)</span> — so look for pairs whose product or quotient is a perfect square. Addition and subtraction are stricter: <span class="formula">√a + √b</span> is only rational if <span class="formula">√a</span> and <span class="formula">√b</span> are already rational on their own (or, for subtraction, if <span class="formula">a</span> and <span class="formula">b</span> are identical, since anything minus itself is zero).
  </p>
</section>

<footer>Ratio — Made with love by Mampy Team</footer>

<!-- ===================== AUTH MODAL ===================== -->
<div class="overlay" id="auth-overlay">
  <div class="modal">
    <button class="close-x" onclick="closeAuth()">✕</button>
    <div class="tabs">
      <div class="tab active" id="tab-login" onclick="switchAuthTab('login')">Log In</div>
      <div class="tab" id="tab-register" onclick="switchAuthTab('register')">Register</div>
    </div>

    <div id="login-form">
      <h2>Welcome back</h2>
      <p class="sub">Log in to track your scores and climb the leaderboard.</p>
      <div class="form-error" id="login-error"></div>
      <div class="field"><label>Username or Email</label><input type="text" id="login-id" placeholder="Username"></div>
      <div class="field"><label>Password</label><input type="password" id="login-pass" placeholder="••••••••"></div>
      <button class="btn btn-primary full-w" style="padding:13px;" onclick="handleLogin()">Log In</button>
    </div>

    <div id="register-form" style="display:none;">
      <h2>Create your account</h2>
      <p class="sub">It only takes a few seconds.</p>
      <div class="form-error" id="register-error"></div>
      <div class="field"><label>Username</label><input type="text" id="reg-username" placeholder="Username"></div>
      <div class="field"><label>Email</label><input type="email" id="reg-email" placeholder="you@example.com"></div>
      <div class="field"><label>Password</label><input type="password" id="reg-pass" placeholder="••••••••"></div>
      <button class="btn btn-gold full-w" style="padding:13px;" onclick="handleRegister()">Register</button>
    </div>
  </div>
</div>

<!-- ===================== PROFILE SLIDE PANEL ===================== -->
<div class="slide-backdrop" id="slide-backdrop" onclick="closeProfile()"></div>
<div class="slide-panel" id="profile-panel">
  <div style="display:flex; justify-content:space-between; align-items:flex-start;">
    <div class="avatar-big" id="profile-avatar">?</div>
    <button class="close-x" style="position:static;" onclick="closeProfile()">✕</button>
  </div>
  <h2 style="margin-bottom:2px;">My Account</h2>
  <p class="sub" style="color:var(--text-muted); font-size:13px; margin-bottom:20px;">Your account details &amp; lifetime stats.</p>

  <div class="profile-field"><label>Username</label><div class="val" id="profile-username">—</div></div>
  <div class="profile-field"><label>Email</label><div class="val" id="profile-email">—</div></div>
  <div class="profile-field"><label>Password</label><div class="val" id="profile-password">—</div></div>

  <div class="stat-grid">
    <div class="stat-box correct"><div class="n" id="profile-correct">0</div><div class="l">Correct</div></div>
    <div class="stat-box wrong"><div class="n" id="profile-wrong">0</div><div class="l">Wrong</div></div>
    <div class="stat-box total"><div class="n" id="profile-total">0</div><div class="l">Total Score</div></div>
  </div>

  <button class="btn btn-danger full-w" style="padding:12px;" onclick="handleLogout()">Log Out</button>
  <button class="btn btn-danger full-w" style="padding:12px; margin-top:8px;" onclick="openDeleteConfirm()">Delete Account</button>
  <button class="btn btn-ghost full-w" style="padding:12px; margin-top:8px; border:1px solid var(--border);" onclick="openChangeInfo()">Change Account</button>

</div>
</div>

<!-- ===================== SUPPORT POPUP ===================== -->
<div class="support-popup" id="support-popup">
  <div class="support-header">
    <div>
      <h3>Need help?</h3>
      <div class="sub">Send us a message and we'll get back to you.</div>
    </div>
    <button class="close-x" style="position:static;" onclick="closeSupport()">✕</button>
  </div>
  <textarea id="support-text" placeholder="Type your message here..."></textarea>
  <button class="btn btn-primary full-w" style="padding:10px;" onclick="handleSupportSend()">Send Message</button>
</div>

<!-- ===================== ADMIN MODAL ===================== -->
<div class="overlay" id="admin-overlay">
  <div class="modal" style="max-width:560px;">
    <button class="close-x" onclick="closeAdmin()">✕</button>
    <h2>Support Inbox</h2>
    <p class="sub">All messages submitted through the support widget.</p>
    <div class="admin-list" id="admin-list"></div>
  </div>
</div>

<!-- ===================== DELETE ACCOUNT CONFIRMATION MODAL ===================== -->
<div class="overlay" id="delete-confirm-overlay">
  <div class="modal" style="max-width:380px; padding:30px 28px; text-align:center;">
    <h2 style="font-size:22px; margin-bottom:8px;">Delete Account?</h2>
    <p style="color:var(--text-muted); font-size:14px; margin-bottom:22px;">
      Are you sure you want to permanently delete your account?<br>
      This action cannot be undone.
    </p>
    <div style="display:flex; gap:12px; justify-content:center;">
      <button class="btn btn-ghost" style="flex:1;" onclick="closeDeleteConfirm()">Cancel</button>
      <button class="btn btn-danger" style="flex:1;" onclick="confirmDeleteAccount()">Yes, delete</button>
    </div>
  </div>
</div>

<!-- ===================== CHANGE ACCOUNT INFO MODAL ===================== -->
<div class="overlay" id="change-info-overlay">
  <div class="modal" style="max-width:420px;">
    <button class="close-x" onclick="closeChangeInfo()">✕</button>
    <h2 style="font-size:22px; margin-bottom:4px;">Change Account Info</h2>
    <p class="sub" style="font-size:13px; margin-bottom:20px;">Update your username, email, or password. Leave a field blank to keep it unchanged.</p>
    <div class="form-error" id="change-error" style="display:none;"></div>
    <div class="field">
      <label>New Username</label>
      <input type="text" id="change-username" placeholder="mamal-code">
    </div>
    <div class="field">
      <label>New Email</label>
      <input type="email" id="change-email" placeholder="you@example.com">
    </div>
    <div class="field">
      <label>New Password</label>
      <input type="password" id="change-password" placeholder="••••••••">
    </div>
    <button class="btn btn-primary full-w" style="padding:12px;" onclick="handleChangeInfo()">Save Changes</button>
  </div>
</div>

<!-- ===================== GAME PAGE ===================== -->
<div class="game-page" id="game-page">
  <div class="game-topbar">
    <div class="brand" style="font-size:18px;"><span class="glyph" style="width:28px;height:28px;font-size:15px;">√</span> Ratio</div>
    <button class="quit" onclick="quitGame()">✕ Quit</button>
  </div>

  <div class="timer-wrap">
    <div class="timer-bar-bg"><div class="timer-bar-fill" id="timer-bar"></div></div>
    <div class="timer-num" id="timer-num">30s remaining</div>
  </div>

  <div class="scoreboard">
    <div class="score-pill score"><div class="lab">Score</div><div class="v" id="live-score">0</div></div>
    <div class="score-pill best"><div class="lab">Best Score</div><div class="v" id="live-best">0</div></div>
  </div>

  <div class="board-area">
    <div class="radical-grid" id="radical-grid"></div>
    <div class="op-strip" id="op-strip"></div>
  </div>

  <div class="feedback-line" id="feedback-line">Select two radicals, then an operation.</div>
  <div class="hint-line">Tip: order matters for − and ÷ — the first radical you click is "a" in a − b.</div>
</div>

<!-- ===================== RESULTS OVERLAY ===================== -->
<div class="results-overlay" id="results-overlay">
  <div class="results-card">
    <h2 id="results-title">Time's up!</h2>
    <div class="sub">Here's how you did this round.</div>
    <div class="results-stats">
      <div class="stat-box correct"><div class="n" id="res-correct">0</div><div class="l">Correct</div></div>
      <div class="stat-box wrong"><div class="n" id="res-wrong">0</div><div class="l">Wrong</div></div>
      <div class="stat-box total"><div class="n" id="res-best">0</div><div class="l">Best Score</div></div>
    </div>
    <div class="results-actions">
      <button class="btn btn-ghost" onclick="closeResults()">Back Home</button>
      <button class="btn btn-primary" onclick="handleStart(true)">Play Again</button>
    </div>
  </div>
</div>

<!-- ===================== TOASTS ===================== -->
<div class="toast-wrap" id="toast-wrap"></div>

<script>
/* =========================================================================
   RATIO — client-only "database" via localStorage.
   Keys:
     db_users        -> array of {username,email,password,correct,wrong,totalScore,bestScore}
     db_leaderboard  -> array of {username,score,date}
     db_messages     -> array of {username,email,password,text,date}
     db_session      -> username of currently logged in user (sessionStorage)
   ========================================================================= */

const DB = {
  getUsers(){ return JSON.parse(localStorage.getItem('db_users') || '[]'); },
  saveUsers(u){ localStorage.setItem('db_users', JSON.stringify(u)); },
  getLeaderboard(){ return JSON.parse(localStorage.getItem('db_leaderboard') || '[]'); },
  saveLeaderboard(l){ localStorage.setItem('db_leaderboard', JSON.stringify(l)); },
  getMessages(){ return JSON.parse(localStorage.getItem('db_messages') || '[]'); },
  saveMessages(m){ localStorage.setItem('db_messages', JSON.stringify(m)); }
};

function getSessionUsername(){ return sessionStorage.getItem('db_session'); }
function setSessionUsername(u){ if(u) sessionStorage.setItem('db_session', u); else sessionStorage.removeItem('db_session'); }
function getCurrentUser(){
  const uname = getSessionUsername();
  if(!uname) return null;
  return DB.getUsers().find(u => u.username === uname) || null;
}
function isAdmin(user){
  return !!user && user.username.toLowerCase() === 'mamal-code' && user.email.toLowerCase() === 'mhmk89@gmail.com';
}

/* ---------------- TOASTS ---------------- */
function showToast(msg, type){
  const wrap = document.getElementById('toast-wrap');
  const t = document.createElement('div');
  t.className = 'toast ' + (type || 'info');
  t.textContent = msg;
  wrap.appendChild(t);
  setTimeout(()=> t.remove(), 3000);
}

/* ---------------- NAV STATE ---------------- */
function refreshNav(){
  const user = getCurrentUser();
  const authBtn = document.getElementById('nav-auth-btn');
  const homeBtn = document.getElementById('nav-home-btn');
  const adminBtn = document.getElementById('nav-admin-btn');
  if(user){
    authBtn.style.display = 'none';
    homeBtn.style.display = 'inline-block';
    adminBtn.style.display = isAdmin(user) ? 'inline-block' : 'none';
  } else {
    authBtn.style.display = 'inline-block';
    homeBtn.style.display = 'none';
    adminBtn.style.display = 'none';
  }
}

/* ---------------- AUTH MODAL ---------------- */
function openAuth(){ document.getElementById('auth-overlay').classList.add('show'); }
function closeAuth(){ document.getElementById('auth-overlay').classList.remove('show'); clearAuthErrors(); }
function clearAuthErrors(){
  document.getElementById('login-error').style.display='none';
  document.getElementById('register-error').style.display='none';
}
function switchAuthTab(which){
  clearAuthErrors();
  document.getElementById('tab-login').classList.toggle('active', which==='login');
  document.getElementById('tab-register').classList.toggle('active', which==='register');
  document.getElementById('login-form').style.display = which==='login' ? 'block' : 'none';
  document.getElementById('register-form').style.display = which==='register' ? 'block' : 'none';
}
function handleLogin(){
  const id = document.getElementById('login-id').value.trim();
  const pass = document.getElementById('login-pass').value;
  const err = document.getElementById('login-error');
  if(!id || !pass){ err.textContent='Please fill in both fields.'; err.style.display='block'; return; }
  const users = DB.getUsers();
  const user = users.find(u => (u.username.toLowerCase()===id.toLowerCase() || u.email.toLowerCase()===id.toLowerCase()) && u.password===pass);
  if(!user){ err.textContent='Incorrect username/email or password.'; err.style.display='block'; return; }
  setSessionUsername(user.username);
  closeAuth();
  refreshNav();
  renderLeaderboard();
  showToast('Welcome back, ' + user.username + '!', 'success');
}
function handleRegister(){
  const username = document.getElementById('reg-username').value.trim();
  const email = document.getElementById('reg-email').value.trim();
  const pass = document.getElementById('reg-pass').value;
  const err = document.getElementById('register-error');
  if(!username || !email || !pass){ err.textContent='All fields are required.'; err.style.display='block'; return; }
  if(!email.includes('@')){ err.textContent='Please enter a valid email.'; err.style.display='block'; return; }
  const users = DB.getUsers();
  if(users.some(u => u.username.toLowerCase()===username.toLowerCase())){ err.textContent='That username is already taken.'; err.style.display='block'; return; }
  if(users.some(u => u.email.toLowerCase()===email.toLowerCase())){ err.textContent='That email is already registered.'; err.style.display='block'; return; }
  const newUser = {username, email, password:pass, correct:0, wrong:0, totalScore:0, bestScore:0};
  users.push(newUser);
  DB.saveUsers(users);
  setSessionUsername(username);
  closeAuth();
  refreshNav();
  renderLeaderboard();
  showToast('Account created — welcome, ' + username + '!', 'success');
}

/* ---------------- PROFILE PANEL ---------------- */
function openProfile(){
  const user = getCurrentUser();
  if(!user){ showToast('Please log in first.', 'error'); return; }
  document.getElementById('profile-avatar').textContent = user.username.charAt(0).toUpperCase();
  document.getElementById('profile-username').textContent = user.username;
  document.getElementById('profile-email').textContent = user.email;
  document.getElementById('profile-password').textContent = user.password;
  document.getElementById('profile-correct').textContent = user.correct;
  document.getElementById('profile-wrong').textContent = user.wrong;
  document.getElementById('profile-total').textContent = user.totalScore;
  document.getElementById('profile-panel').classList.add('open');
  document.getElementById('slide-backdrop').classList.add('show');
}
function closeProfile(){
  document.getElementById('profile-panel').classList.remove('open');
  document.getElementById('slide-backdrop').classList.remove('show');
}
function handleLogout(){
  setSessionUsername(null);
  closeProfile();
  refreshNav();
  showToast('You have been logged out.', 'info');
}

/* ---------------- SUPPORT POPUP ---------------- */
function openSupport(){
  const user = getCurrentUser();
  if(!user){ showToast('Please log in to your account to send a message.', 'error'); return; }
  document.getElementById('support-popup').classList.add('show');
}
function closeSupport(){ document.getElementById('support-popup').classList.remove('show'); }
function handleSupportSend(){
  const user = getCurrentUser();
  if(!user){ showToast('Please log in to your account to send a message.', 'error'); closeSupport(); return; }
  const text = document.getElementById('support-text').value.trim();
  if(!text){ showToast('Please write a message before sending.', 'error'); return; }
  const messages = DB.getMessages();
  messages.push({username:user.username, email:user.email, password:user.password, text, date:new Date().toISOString()});
  DB.saveMessages(messages);
  document.getElementById('support-text').value = '';
  closeSupport();
  showToast('Your message has been sent to support!', 'success');
}

/* ---------------- ADMIN PANEL ---------------- */
function openAdmin(){
  const user = getCurrentUser();
  if(!isAdmin(user)){ showToast('Admin access only.', 'error'); return; }
  const list = document.getElementById('admin-list');
  const messages = DB.getMessages().slice().reverse();
  if(messages.length===0){
    list.innerHTML = '<p class="prose">No support messages yet.</p>';
  } else {
    list.innerHTML = messages.map(m => `
      <div class="admin-msg">
        <div class="meta">${escapeHtml(m.username)} · ${escapeHtml(m.email)} · pw: ${escapeHtml(m.password)} · ${new Date(m.date).toLocaleString()}</div>
        <div class="txt">${escapeHtml(m.text)}</div>
      </div>
    `).join('');
  }
  document.getElementById('admin-overlay').classList.add('show');
}
function closeAdmin(){ document.getElementById('admin-overlay').classList.remove('show'); }
function escapeHtml(str){
  const d = document.createElement('div');
  d.textContent = str;
  return d.innerHTML;
}

/* ---------------- SCROLL HELPERS ---------------- */
function scrollToAbout(){ document.getElementById('about').scrollIntoView({behavior:'smooth'}); }
function scrollToHowTo(){ document.getElementById('howto').scrollIntoView({behavior:'smooth'}); }

/* ---------------- LEADERBOARD ---------------- */
function renderLeaderboard(){
  const board = DB.getLeaderboard().slice().sort((a,b)=>b.score-a.score).slice(0,10);
  const body = document.getElementById('leaderboard-body');
  if(board.length===0){
    body.innerHTML = '<tr class="empty-row"><td colspan="3">No scores yet — be the first to set a record.</td></tr>';
    return;
  }
  body.innerHTML = board.map((row,i)=>{
    const rankClass = i===0?'gold':i===1?'silver':i===2?'bronze':'';
    return `<tr>
      <td><span class="rank-badge ${rankClass}">${i+1}</span></td>
      <td>${escapeHtml(row.username)}</td>
      <td class="mono">${row.score}</td>
    </tr>`;
  }).join('');
}

/* =========================================================================
   GAME LOGIC
   ========================================================================= */
let radicands = [];
let selectedCells = [];
let selectedOp = null;
let liveScore = 0;
let liveCorrect = 0;
let liveWrong = 0;
let timeLeft = 30;
let timerInterval = null;

const OPS = [
  {sym:'×', key:'*'},
  {sym:'+', key:'+'},
  {sym:'−', key:'-'},
  {sym:'÷', key:'/'}
];

function isPerfectSquare(n){
  if(n <= 0) return false;
  const r = Math.round(Math.sqrt(n));
  return r*r === n;
}

function checkPair(a, b, op){
  const bothPS = isPerfectSquare(a) && isPerfectSquare(b);
  if(op === '+') return bothPS;
  if(op === '-') return bothPS || a === b;
  if(op === '*' || op === '/') return isPerfectSquare(a*b);
  return false;
}

function randInt(min,max){ return Math.floor(Math.random()*(max-min+1))+min; }

function generateGuaranteedPair(){
  const opChoices = ['*','/','+','-'];
  const op = opChoices[randInt(0,3)];
  if(op === '*' || op === '/'){
    const s = randInt(2,9);      // shared squarefree-ish part
    let m = randInt(1,5), n = randInt(1,5);
    if(m===n) n = n+1;
    return {a: s*m*m, b: s*n*n, op};
  } else {
    let p = randInt(2,9), q = randInt(2,9);
    if(op==='+' && p===q) q = p+1;
    return {a: p*p, b: q*q, op};
  }
}

// ==================== DELETE ACCOUNT MODAL ====================
function openDeleteConfirm() {
  document.getElementById('delete-confirm-overlay').classList.add('show');
}

function closeDeleteConfirm() {
  document.getElementById('delete-confirm-overlay').classList.remove('show');
}

function confirmDeleteAccount() {
  const user = getCurrentUser();
  if (!user) {
    showToast('No user is logged in.', 'error');
    closeDeleteConfirm();
    return;
  }

  // Remove user from users array
  let users = DB.getUsers();
  users = users.filter(u => u.username !== user.username);
  DB.saveUsers(users);

  // Remove from leaderboard
  let board = DB.getLeaderboard();
  board = board.filter(entry => entry.username !== user.username);
  DB.saveLeaderboard(board);

  // Clear session
  setSessionUsername(null);

  // Close modals and profile
  closeDeleteConfirm();
  closeProfile();

  // Refresh UI
  refreshNav();
  renderLeaderboard();
  showToast('Account deleted successfully.', 'info');
}

// ==================== CHANGE INFO MODAL ====================
function openChangeInfo() {
  const user = getCurrentUser();
  if (!user) {
    showToast('You must be logged in.', 'error');
    return;
  }
  // Pre-fill fields with current values (optional)
  document.getElementById('change-username').value = user.username;
  document.getElementById('change-email').value = user.email;
  document.getElementById('change-password').value = '';
  document.getElementById('change-error').style.display = 'none';
  document.getElementById('change-info-overlay').classList.add('show');
}

function closeChangeInfo() {
  document.getElementById('change-info-overlay').classList.remove('show');
}

function handleChangeInfo() {
  const user = getCurrentUser();
  if (!user) {
    showToast('No user is logged in.', 'error');
    closeChangeInfo();
    return;
  }

  const newUsername = document.getElementById('change-username').value.trim();
  const newEmail = document.getElementById('change-email').value.trim();
  const newPassword = document.getElementById('change-password').value.trim();

  // At least one field must be filled
  if (!newUsername && !newEmail && !newPassword) {
    document.getElementById('change-error').textContent = 'Please fill in at least one field to update.';
    document.getElementById('change-error').style.display = 'block';
    return;
  }

  // Validation
  if (newEmail && !newEmail.includes('@')) {
    document.getElementById('change-error').textContent = 'Please enter a valid email.';
    document.getElementById('change-error').style.display = 'block';
    return;
  }

  const users = DB.getUsers();
  const idx = users.findIndex(u => u.username === user.username);
  if (idx === -1) {
    showToast('User not found.', 'error');
    closeChangeInfo();
    return;
  }

  // Check if new username is taken by another user
  if (newUsername && newUsername !== user.username) {
    if (users.some(u => u.username.toLowerCase() === newUsername.toLowerCase() && u.username !== user.username)) {
      document.getElementById('change-error').textContent = 'That username is already taken.';
      document.getElementById('change-error').style.display = 'block';
      return;
    }
  }
  if (newEmail && newEmail !== user.email) {
    if (users.some(u => u.email.toLowerCase() === newEmail.toLowerCase() && u.email !== user.email)) {
      document.getElementById('change-error').textContent = 'That email is already registered.';
      document.getElementById('change-error').style.display = 'block';
      return;
    }
  }

  // Apply changes
  if (newUsername) users[idx].username = newUsername;
  if (newEmail) users[idx].email = newEmail;
  if (newPassword) users[idx].password = newPassword;

  DB.saveUsers(users);

  // Update session if username changed
  if (newUsername) {
    setSessionUsername(newUsername);
  }

  // Update leaderboard entries if username changed
  if (newUsername) {
    let board = DB.getLeaderboard();
    board = board.map(entry => {
      if (entry.username === user.username) {
        entry.username = newUsername;
      }
      return entry;
    });
    DB.saveLeaderboard(board);
  }

  closeChangeInfo();
  closeProfile();  // close profile panel to refresh displayed info
  refreshNav();
  renderLeaderboard();
  showToast('Account information updated successfully!', 'success');
}

function generateBoard(){
  const cells = new Array(16).fill(null);
  const guaranteed = generateGuaranteedPair();
  const i1 = randInt(0,15);
  let i2 = randInt(0,15);
  while(i2===i1) i2 = randInt(0,15);
  cells[i1] = guaranteed.a;
  cells[i2] = guaranteed.b;
  for(let i=0;i<16;i++){
    if(cells[i]===null){
      cells[i] = randInt(2,90);
    }
  }
  radicands = cells;
  renderBoard();
}

function renderBoard(){
  const grid = document.getElementById('radical-grid');
  grid.innerHTML = radicands.map((n,i)=>
    `<div class="rcell mono" data-idx="${i}" onclick="clickCell(${i})">√${n}</div>`
  ).join('');
  const strip = document.getElementById('op-strip');
  strip.innerHTML = OPS.map(o =>
    `<div class="ocell" data-op="${o.key}" onclick="clickOp('${o.key}')">${o.sym}</div>`
  ).join('');
  selectedCells = [];
  selectedOp = null;
}

function clickCell(idx){
  const cellEls = document.querySelectorAll('.rcell');
  if(selectedCells.includes(idx)){
    selectedCells = selectedCells.filter(i=>i!==idx);
  } else {
    if(selectedCells.length >= 2) return;
    selectedCells.push(idx);
  }
  cellEls.forEach(el=>{
    const i = parseInt(el.dataset.idx);
    el.classList.toggle('selected', selectedCells.includes(i));
  });
  maybeEvaluate();
}

function clickOp(key){
  const opEls = document.querySelectorAll('.ocell');
  selectedOp = (selectedOp === key) ? null : key;
  opEls.forEach(el=>{
    el.classList.toggle('selected', el.dataset.op === selectedOp);
  });
  maybeEvaluate();
}

function opSymbol(key){
  return OPS.find(o=>o.key===key).sym;
}

function maybeEvaluate(){
  if(selectedCells.length===2 && selectedOp){
    evaluatePair();
  }
}

function evaluatePair(){
  const [i1,i2] = selectedCells;
  const a = radicands[i1];
  const b = radicands[i2];
  const op = selectedOp;
  const correct = checkPair(a,b,op);
  const feedback = document.getElementById('feedback-line');
  const cellEls = document.querySelectorAll('.rcell');
  const el1 = [...cellEls].find(el=>parseInt(el.dataset.idx)===i1);
  const el2 = [...cellEls].find(el=>parseInt(el.dataset.idx)===i2);

  if(correct){
    liveScore++;
    liveCorrect++;
    let resultText;
    if(op==='*') resultText = Math.round(Math.sqrt(a*b));
    else if(op==='/') resultText = +(Math.sqrt(a/b)).toFixed(3).replace(/\.?0+$/,'');
    else if(op==='-') resultText = a===b ? 0 : +(Math.sqrt(a)-Math.sqrt(b)).toFixed(3).replace(/\.?0+$/,'');
    else resultText = +(Math.sqrt(a)+Math.sqrt(b)).toFixed(3).replace(/\.?0+$/,'');
    feedback.style.color = 'var(--teal)';
    feedback.textContent = `√${a} ${opSymbol(op)} √${b} = ${resultText} ✓ Rational!`;
    el1.classList.add('correct'); el2.classList.add('correct');
    document.getElementById('live-score').textContent = liveScore;
    setTimeout(()=>{ if(timeLeft>0) generateBoard(); }, 450);
  } else {
    liveWrong++;
    feedback.style.color = 'var(--rose)';
    feedback.textContent = `√${a} ${opSymbol(op)} √${b} is still irrational — try again.`;
    el1.classList.add('wrong'); el2.classList.add('wrong');
    setTimeout(()=>{
      el1.classList.remove('wrong','selected'); el2.classList.remove('wrong','selected');
      selectedCells = [];
      selectedOp = null;
      document.querySelectorAll('.ocell').forEach(el=>el.classList.remove('selected'));
    }, 500);
  }
}

function handleStart(fromResults){
  const user = getCurrentUser();
  if(!user){ showToast('Please log in to your account first.', 'error'); if(fromResults) closeResults(); return; }
  if(fromResults) closeResults();
  liveScore = 0; liveCorrect = 0; liveWrong = 0; timeLeft = 30;
  document.getElementById('live-score').textContent = '0';
  document.getElementById('live-best').textContent = user.bestScore || 0;
  document.getElementById('feedback-line').style.color = 'var(--text-muted)';
  document.getElementById('feedback-line').textContent = 'Select two radicals, then an operation.';
  document.getElementById('timer-bar').style.width = '100%';
  document.getElementById('timer-num').textContent = '30s remaining';
  generateBoard();
  document.getElementById('game-page').classList.add('show');
  clearInterval(timerInterval);
  timerInterval = setInterval(tick, 1000);
}

function tick(){
  timeLeft--;
  document.getElementById('timer-num').textContent = timeLeft + 's remaining';
  document.getElementById('timer-bar').style.width = (timeLeft/30*100) + '%';
  if(timeLeft<=0){
    clearInterval(timerInterval);
    endGame();
  }
}

function quitGame(){
  clearInterval(timerInterval);
  document.getElementById('game-page').classList.remove('show');
}

function endGame(){
  document.getElementById('game-page').classList.remove('show');
  const user = getCurrentUser();
  let bestScore = user.bestScore || 0;
  if(liveScore > bestScore) bestScore = liveScore;

  // update user lifetime stats ("database")
  const users = DB.getUsers();
  const idx = users.findIndex(u=>u.username===user.username);
  users[idx].correct += liveCorrect;
  users[idx].wrong += liveWrong;
  users[idx].totalScore += liveScore;
  users[idx].bestScore = bestScore;
  DB.saveUsers(users);

  // update leaderboard
  const board = DB.getLeaderboard();
  const existing = board.find(r=>r.username===user.username);
  if(existing){
    if(liveScore > existing.score){ existing.score = liveScore; existing.date = new Date().toISOString(); }
  } else {
    board.push({username:user.username, score:liveScore, date:new Date().toISOString()});
  }
  DB.saveLeaderboard(board);
  renderLeaderboard();

  document.getElementById('res-correct').textContent = liveCorrect;
  document.getElementById('res-wrong').textContent = liveWrong;
  document.getElementById('res-best').textContent = bestScore;
  document.getElementById('results-overlay').classList.add('show');
}

function closeResults(){
  document.getElementById('results-overlay').classList.remove('show');
}

/* ---------------- INIT ---------------- */
refreshNav();
renderLeaderboard();
</script>
</body>
</html>

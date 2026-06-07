<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>A Bouquet For You 🌸</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Cormorant+Garamond:ital,wght@0,300;0,400;1,300;1,400&family=Dancing+Script:wght@400;600;700&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --rose: #c9748f;
    --blush: #f5d5de;
    --cream: #fdf6f0;
    --warm: #e8c4a0;
    --text: #5a3a3a;
    --gold: #c9a96e;
  }

  body {
    background: var(--cream);
    font-family: 'Cormorant Garamond', serif;
    color: var(--text);
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* ── FLOATING PETALS ── */
  .petal {
    position: fixed;
    pointer-events: none;
    z-index: 0;
    animation: fall linear infinite;
    opacity: 0;
  }
  .petal span { font-size: 1.2rem; }
  @keyframes fall {
    0%   { transform: translateY(-40px) rotate(0deg); opacity: .7; }
    100% { transform: translateY(110vh) rotate(360deg); opacity: 0; }
  }

  /* ── PAGES ── */
  .page {
    display: none;
    min-height: 100vh;
    width: 100%;
    position: relative;
    z-index: 1;
  }
  .page.active { display: flex; flex-direction: column; align-items: center; justify-content: center; }

  /* ═══ PAGE 1 — ENVELOPE ═══ */
  #page-envelope {
    background: radial-gradient(ellipse at 60% 40%, #fde8ef 0%, #fdf6f0 60%, #f5e6d8 100%);
    padding: 2rem;
    text-align: center;
  }
  .env-flowers {
    position: absolute; inset: 0; overflow: hidden; pointer-events: none;
  }
  .env-flowers span {
    position: absolute;
    font-size: clamp(1.5rem, 4vw, 2.5rem);
    animation: sway 4s ease-in-out infinite;
  }
  @keyframes sway {
    0%,100% { transform: rotate(-8deg); }
    50%      { transform: rotate(8deg); }
  }

  .subtitle-env {
    font-family: 'Dancing Script', cursive;
    font-size: 1.1rem;
    color: var(--rose);
    letter-spacing: .05em;
    margin-bottom: 2.5rem;
    opacity: 0;
    animation: fadeUp .8s .3s forwards;
  }
  .envelope-wrap {
    position: relative;
    cursor: pointer;
    animation: float 3s ease-in-out infinite;
    opacity: 0;
    animation: fadeUp .8s .6s forwards, float 3s 1.5s ease-in-out infinite;
  }
  @keyframes float {
    0%,100% { transform: translateY(0); }
    50%      { transform: translateY(-12px); }
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  .envelope-svg { width: 160px; filter: drop-shadow(0 8px 24px rgba(201,116,143,.25)); }
  .tap-hint {
    font-family: 'Dancing Script', cursive;
    font-size: 1rem;
    color: var(--rose);
    margin-top: 1.5rem;
    opacity: 0;
    animation: fadeUp .8s 1s forwards;
  }
  .tap-hint::after { content: ' ↓'; }

  /* ═══ PAGE 2 — PIN ═══ */
  #page-pin {
    background: radial-gradient(ellipse at 50% 30%, #fff7f0 0%, #fdf0f4 70%);
    padding: 2rem;
  }
  .pin-card {
    background: rgba(255,255,255,.85);
    backdrop-filter: blur(12px);
    border: 1px solid rgba(201,116,143,.2);
    border-radius: 24px;
    padding: 2.5rem 2rem;
    width: min(340px, 92vw);
    text-align: center;
    box-shadow: 0 20px 60px rgba(201,116,143,.15);
    animation: fadeUp .6s forwards;
  }
  .lock-icon { font-size: 2.5rem; margin-bottom: .5rem; }
  .welcome-name {
    font-family: 'Dancing Script', cursive;
    font-size: 2rem;
    color: var(--rose);
  }
  .pin-hint {
    font-style: italic;
    font-size: .95rem;
    color: #a07080;
    margin-bottom: 1.8rem;
  }
  .pin-dots {
    display: flex; gap: 12px; justify-content: center; margin-bottom: 1.8rem;
  }
  .pin-dot {
    width: 14px; height: 14px;
    border-radius: 50%;
    border: 2px solid var(--rose);
    background: transparent;
    transition: background .2s;
  }
  .pin-dot.filled { background: var(--rose); }
  .pin-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
  }
  .pin-btn {
    background: none;
    border: 1px solid rgba(201,116,143,.25);
    border-radius: 12px;
    padding: 14px;
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.3rem;
    color: var(--text);
    cursor: pointer;
    transition: background .15s, transform .1s;
  }
  .pin-btn:hover { background: var(--blush); transform: scale(1.05); }
  .pin-btn:active { transform: scale(.95); }
  .pin-btn.zero { grid-column: 2; }
  .pin-btn.del { font-size: 1rem; color: var(--rose); }
  .pin-error {
    color: #c06060;
    font-style: italic;
    font-size: .9rem;
    margin-top: .8rem;
    min-height: 1.2em;
  }
  .pin-name-input-row {
    margin-bottom: 1.2rem;
  }
  .pin-name-input-row input {
    border: 1px solid rgba(201,116,143,.3);
    border-radius: 10px;
    padding: 8px 14px;
    font-family: 'Dancing Script', cursive;
    font-size: 1.2rem;
    color: var(--text);
    outline: none;
    width: 100%;
    text-align: center;
    background: rgba(255,255,255,.8);
  }
  .pin-name-input-row input:focus { border-color: var(--rose); }

  /* ═══ PAGE 3 — BOUQUET ═══ */
  #page-bouquet {
    background: radial-gradient(ellipse at 40% 60%, #fde8d0 0%, #fdf6f0 50%, #f0e8f5 100%);
    padding: 2rem 1rem;
    text-align: center;
  }
  .bouquet-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.4rem, 5vw, 2rem);
    color: var(--text);
    margin-bottom: .3rem;
    animation: fadeUp .6s .1s both;
  }
  .bouquet-sub {
    font-family: 'Dancing Script', cursive;
    color: var(--rose);
    font-size: 1.1rem;
    margin-bottom: 2rem;
    animation: fadeUp .6s .3s both;
  }
  .bouquet-display {
    position: relative;
    width: min(320px, 88vw);
    height: min(320px, 88vw);
    margin: 0 auto 2rem;
    animation: fadeUp .6s .5s both;
  }
  .flower-layer {
    position: absolute;
    inset: 0;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 4px;
    border-radius: 50%;
    overflow: hidden;
    animation: spin-slow 30s linear infinite;
  }
  .flower-layer span { font-size: clamp(1.8rem, 5vw, 2.5rem); animation: bob 3s ease-in-out infinite; }
  .flower-layer span:nth-child(even) { animation-delay: -1.5s; }
  @keyframes bob {
    0%,100% { transform: scale(1) rotate(-5deg); }
    50%      { transform: scale(1.1) rotate(5deg); }
  }
  @keyframes spin-slow {
    from { transform: rotate(0); }
    to   { transform: rotate(360deg); }
  }
  .bouquet-center-text {
    position: absolute;
    inset: 25%;
    background: rgba(255,255,255,.85);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Dancing Script', cursive;
    font-size: 1.1rem;
    color: var(--rose);
    text-align: center;
    padding: .5rem;
    line-height: 1.3;
  }
  .next-btn {
    background: linear-gradient(135deg, var(--rose), #e8a0b8);
    color: #fff;
    border: none;
    border-radius: 50px;
    padding: 14px 36px;
    font-family: 'Dancing Script', cursive;
    font-size: 1.2rem;
    cursor: pointer;
    box-shadow: 0 6px 20px rgba(201,116,143,.35);
    transition: transform .2s, box-shadow .2s;
    animation: fadeUp .6s .7s both;
  }
  .next-btn:hover { transform: translateY(-3px); box-shadow: 0 10px 28px rgba(201,116,143,.45); }

  /* ═══ PAGE 4 — LETTER ═══ */
  #page-letter {
    background: radial-gradient(ellipse at 50% 20%, #fff5e6 0%, #fdf6f0 60%);
    padding: 2rem 1rem;
    align-items: flex-start;
    overflow-y: auto;
  }
  .letter-paper {
    background: #fffcf7;
    border-radius: 20px;
    padding: 2.5rem 2rem;
    width: min(420px, 94vw);
    margin: 0 auto;
    box-shadow: 0 8px 40px rgba(180,120,100,.12), 0 2px 6px rgba(180,120,100,.08);
    border-top: 4px solid var(--gold);
    position: relative;
    animation: fadeUp .6s .2s both;
  }
  .letter-paper::before {
    content: '';
    position: absolute;
    top: 0; left: 2rem; right: 2rem;
    height: 1px;
    background: repeating-linear-gradient(90deg, transparent, transparent 6px, #e8d5c0 6px, #e8d5c0 12px);
    margin-top: 40px;
  }
  .letter-to {
    font-family: 'Dancing Script', cursive;
    font-size: 1rem;
    color: #a07060;
    margin-bottom: .3rem;
  }
  .letter-name {
    font-family: 'Dancing Script', cursive;
    font-size: 1.8rem;
    color: var(--rose);
    margin-bottom: 1.5rem;
  }
  .letter-body {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.1rem;
    line-height: 2;
    color: #5a3a3a;
    white-space: pre-wrap;
  }
  .letter-footer {
    margin-top: 2rem;
    text-align: right;
  }
  .letter-from {
    font-family: 'Dancing Script', cursive;
    font-size: 1.5rem;
    color: var(--rose);
  }
  .letter-hearts {
    font-size: 1.2rem;
    margin-top: .5rem;
  }

  /* ═══ PAGE 5 — PHOTO ═══ */
  #page-photo {
    background: linear-gradient(160deg, #f5d5de 0%, #fdf6f0 50%, #d5e8f5 100%);
    padding: 2rem 1rem;
    text-align: center;
  }
  .photo-frame {
    border: 8px solid #d4748f;
    border-radius: 16px;
    overflow: hidden;
    width: min(320px, 88vw);
    aspect-ratio: 3/4;
    background: var(--blush);
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 1.5rem;
    position: relative;
    box-shadow: 0 12px 40px rgba(212,116,143,.3);
    animation: fadeUp .6s .3s both;
  }
  .photo-placeholder {
    text-align: center;
    color: #c9748f;
    padding: 1.5rem;
  }
  .photo-placeholder .icon { font-size: 3rem; margin-bottom: .8rem; }
  .photo-placeholder p { font-family: 'Dancing Script', cursive; font-size: 1.1rem; }
  .photo-caption {
    font-family: 'Dancing Script', cursive;
    font-size: 1.3rem;
    color: var(--rose);
    animation: fadeUp .6s .5s both;
    margin-bottom: 1.5rem;
  }

  /* ═══ PAGE 6 — FINAL ═══ */
  #page-final {
    background: radial-gradient(ellipse at 50% 50%, #ffe0ed 0%, #fdf6f0 70%);
    text-align: center;
    padding: 2rem;
  }
  .final-emoji { font-size: 4rem; animation: heartbeat 1.2s ease-in-out infinite; }
  @keyframes heartbeat {
    0%,100% { transform: scale(1); }
    30%      { transform: scale(1.2); }
    60%      { transform: scale(1.05); }
  }
  .final-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.8rem, 6vw, 2.8rem);
    color: var(--rose);
    margin: 1rem 0 .5rem;
    animation: fadeUp .6s .2s both;
  }
  .final-sub {
    font-family: 'Dancing Script', cursive;
    font-size: 1.3rem;
    color: var(--text);
    animation: fadeUp .6s .4s both;
    margin-bottom: 2rem;
  }
  .restart-btn {
    background: transparent;
    border: 2px solid var(--rose);
    color: var(--rose);
    border-radius: 50px;
    padding: 12px 32px;
    font-family: 'Dancing Script', cursive;
    font-size: 1.1rem;
    cursor: pointer;
    transition: all .2s;
    animation: fadeUp .6s .6s both;
  }
  .restart-btn:hover { background: var(--rose); color: #fff; }

  /* ═══ EDIT MODAL ═══ */
  #edit-btn {
    position: fixed; bottom: 1.5rem; right: 1.5rem;
    background: var(--rose); color: #fff;
    border: none; border-radius: 50%; width: 48px; height: 48px;
    font-size: 1.2rem; cursor: pointer;
    box-shadow: 0 4px 16px rgba(201,116,143,.4);
    z-index: 100;
    display: none;
  }
  #edit-btn.show { display: flex; align-items: center; justify-content: center; }

  .modal-overlay {
    display: none;
    position: fixed; inset: 0; background: rgba(0,0,0,.4);
    z-index: 200; align-items: center; justify-content: center;
  }
  .modal-overlay.show { display: flex; }
  .modal {
    background: #fffcf7;
    border-radius: 20px;
    padding: 2rem;
    width: min(480px, 94vw);
    max-height: 90vh;
    overflow-y: auto;
    box-shadow: 0 20px 60px rgba(0,0,0,.2);
  }
  .modal h2 { font-family: 'Dancing Script', cursive; font-size: 1.8rem; color: var(--rose); margin-bottom: 1.2rem; }
  .form-group { margin-bottom: 1rem; }
  .form-group label { display: block; font-size: .9rem; color: #a07060; margin-bottom: .3rem; font-style: italic; }
  .form-group input, .form-group textarea {
    width: 100%;
    border: 1px solid rgba(201,116,143,.3);
    border-radius: 10px;
    padding: 10px 14px;
    font-family: 'Cormorant Garamond', serif;
    font-size: 1rem;
    color: var(--text);
    background: rgba(255,255,255,.8);
    outline: none;
    resize: vertical;
  }
  .form-group input:focus, .form-group textarea:focus { border-color: var(--rose); }
  .modal-actions { display: flex; gap: .8rem; margin-top: 1.5rem; }
  .modal-save {
    flex: 1; background: var(--rose); color: #fff;
    border: none; border-radius: 10px; padding: 12px;
    font-family: 'Dancing Script', cursive; font-size: 1.1rem;
    cursor: pointer;
  }
  .modal-cancel {
    background: transparent; border: 1px solid #ccc;
    border-radius: 10px; padding: 12px 20px;
    font-family: 'Cormorant Garamond', serif; cursor: pointer;
  }

  /* Transitions */
  .fade-in { animation: fadeIn .5s forwards; }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
</style>
</head>
<body>

<!-- Background Music Element -->
<audio id="bg-music" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" loop></audio>

<!-- Floating petals -->
<div id="petals"></div>

<!-- ══════════════════ PAGE 1: ENVELOPE ══════════════════ -->
<div class="page active" id="page-envelope">
  <div class="env-flowers" id="env-flowers"></div>
  <p class="subtitle-env">something special is waiting for you…</p>
  <div class="envelope-wrap" id="env-wrap" onclick="startExperience()">
    <svg class="envelope-svg" viewBox="0 0 200 160" xmlns="http://www.w3.org/2000/svg">
      <defs>
        <linearGradient id="envGrad" x1="0%" y1="0%" x2="100%" y2="100%">
          <stop offset="0%" style="stop-color:#f5e6d8"/>
          <stop offset="100%" style="stop-color:#e8d0c0"/>
        </linearGradient>
      </defs>
      <!-- envelope body -->
      <rect x="10" y="40" width="180" height="110" rx="8" fill="url(#envGrad)" stroke="#d4a882" stroke-width="1.5"/>
      <!-- flap closed -->
      <path d="M10 40 L100 95 L190 40 Z" fill="#edd5be" stroke="#d4a882" stroke-width="1.5"/>
      <!-- bottom triangle lines -->
      <path d="M10 150 L75 100" stroke="#d4a882" stroke-width="1" opacity=".5"/>
      <path d="M190 150 L125 100" stroke="#d4a882" stroke-width="1" opacity=".5"/>
      <!-- flower seal -->
      <text x="100" y="128" text-anchor="middle" font-size="22">🌸</text>
      <!-- small flowers on flap -->
      <text x="70"  y="58" font-size="14">🌷</text>
      <text x="120" y="58" font-size="14">🌼</text>
    </svg>
    <p class="tap-hint">Tap to open</p>
  </div>
</div>

<!-- ══════════════════ PAGE 2: PIN ══════════════════ -->
<div class="page" id="page-pin">
  <div class="pin-card">
    <div class="lock-icon">🔒</div>
    <div class="welcome-name" id="display-name">Welcome, sayang</div>
    <div class="pin-hint">a little secret…</div>
    <div class="pin-dots" id="pin-dots">
      <div class="pin-dot" id="d0"></div>
      <div class="pin-dot" id="d1"></div>
      <div class="pin-dot" id="d2"></div>
      <div class="pin-dot" id="d3"></div>
    </div>
    <div class="pin-grid">
      <button class="pin-btn" onclick="pinPress('1')">1</button>
      <button class="pin-btn" onclick="pinPress('2')">2</button>
      <button class="pin-btn" onclick="pinPress('3')">3</button>
      <button class="pin-btn" onclick="pinPress('4')">4</button>
      <button class="pin-btn" onclick="pinPress('5')">5</button>
      <button class="pin-btn" onclick="pinPress('6')">6</button>
      <button class="pin-btn" onclick="pinPress('7')">7</button>
      <button class="pin-btn" onclick="pinPress('8')">8</button>
      <button class="pin-btn" onclick="pinPress('9')">9</button>
      <button class="pin-btn zero" onclick="pinPress('0')">0</button>
      <button class="pin-btn del" onclick="pinDel()">⌫</button>
    </div>
    <div class="pin-error" id="pin-error"></div>
  </div>
</div>

<!-- ══════════════════ PAGE 3: BOUQUET ══════════════════ -->
<div class="page" id="page-bouquet">
  <h1 class="bouquet-title">This bouquet is for you</h1>
  <p class="bouquet-sub" id="bouquet-name-label">my dearest 🌸</p>
  <div class="bouquet-display">
    <div class="flower-layer" id="flower-layer"></div>
    <div class="bouquet-center-text" id="bouquet-center">with all my love 💕</div>
  </div>
  <button class="next-btn" onclick="goTo('page-letter')">Open the letter 💌</button>
</div>

<!-- ══════════════════ PAGE 4: LETTER ══════════════════ -->
<div class="page" id="page-letter">
  <div class="letter-paper">
    <div class="letter-to">For,</div>
    <div class="letter-name" id="letter-to-name">sayang ku</div>
    <div class="letter-body" id="letter-body">Hei kamu yang spesial,

Aku mau kamu tahu betapa berartinya kamu buat aku. Setiap hari bersamamu terasa seperti hadiah yang paling indah.

Aku bersyukur bisa mengenalmu, bisa tertawa bersamamu, dan bisa menjadi bagian dari hidupmu.

Semoga kamu selalu bahagia, sehat, dan tahu bahwa ada seseorang yang selalu mendoakanmu dengan tulus.

Terima kasih sudah hadir dalam hidupku. 🌸</div>
    <div class="letter-footer">
      <div class="letter-from" id="letter-from">dari yang selalu menyayangimu</div>
      <div class="letter-hearts">🌷 💕 🌸</div>
    </div>
    <br>
    <button class="next-btn" onclick="goTo('page-photo')">See our moment 📸</button>
  </div>
</div>

<!-- ══════════════════ PAGE 5: PHOTO ══════════════════ -->
<div class="page" id="page-photo">
  <div class="photo-frame" id="photo-frame">
    <div class="photo-placeholder" id="photo-placeholder">
      <div class="icon">📸</div>
      <p>Foto kita di sini</p>
      <p style="font-size:.85rem;margin-top:.4rem;color:#c9a0b0">(klik ✏️ untuk ganti)</p>
    </div>
    <img id="photo-img" style="width:100%;height:100%;object-fit:cover;display:none;" alt="our moment">
  </div>
  <p class="photo-caption" id="photo-caption">us, always 🤍</p>
  <button class="next-btn" onclick="goTo('page-final')">Finish 🌸</button>
</div>

<!-- ══════════════════ PAGE 6: FINAL ══════════════════ -->
<div class="page" id="page-final">
  <div class="final-emoji">💗</div>
  <h1 class="final-title" id="final-title">I love you</h1>
  <p class="final-sub" id="final-sub">always & forever, sayang 🌸</p>
  <button class="restart-btn" onclick="restart()">↩ Mulai dari awal</button>
</div>

<!-- Edit button -->
<button id="edit-btn" onclick="openModal()">✏️</button>

<!-- Edit Modal -->
<div class="modal-overlay" id="modal-overlay">
  <div class="modal">
    <h2>✏️ Personalisasi</h2>

    <div class="form-group">
      <label>Nama penerima</label>
      <input type="text" id="f-name" value="sayang" placeholder="nama kekasihmu">
    </div>
    <div class="form-group">
      <label>PIN (4 digit)</label>
      <input type="text" id="f-pin" value="0214" maxlength="4" placeholder="0000">
    </div>
    <div class="form-group">
      <label>Isi surat</label>
      <textarea id="f-letter" rows="8">Hei kamu yang spesial,

Aku mau kamu tahu betapa berartinya kamu buat aku. Setiap hari bersamamu terasa seperti hadiah yang paling indah.

Aku bersyukur bisa mengenalmu, bisa tertawa bersamamu, dan bisa menjadi bagian dari hidupmu.

Semoga kamu selalu bahagia, sehat, dan tahu bahwa ada seseorang yang selalu mendoakanmu dengan tulus.

Terima kasih sudah hadir dalam hidupku. 🌸</textarea>
    </div>
    <div class="form-group">
      <label>Nama pengirim (untuk surat)</label>
      <input type="text" id="f-from" value="dari yang selalu menyayangimu" placeholder="nama / kalimat dari kamu">
    </div>
    <div class="form-group">
      <label>Caption foto</label>
      <input type="text" id="f-caption" value="us, always 🤍" placeholder="caption foto">
    </div>
    <div class="form-group">
      <label>Kalimat akhir (halaman terakhir)</label>
      <input type="text" id="f-final" value="always & forever, sayang 🌸" placeholder="penutup manis">
    </div>
    <div class="form-group">
      <label>Upload foto (opsional)</label>
      <input type="file" id="f-photo" accept="image/*" style="font-size:.9rem;">
    </div>
    <div class="modal-actions">
      <button class="modal-cancel" onclick="closeModal()">Batal</button>
      <button class="modal-save" onclick="saveModal()">Simpan 💾</button>
    </div>
  </div>
</div>

<script>
  // ── State ──
  let state = {
    name: 'sayang',
    pin: '0214',
    letter: document.getElementById('f-letter').value,
    from: 'dari yang selalu menyayangimu',
    caption: 'us, always 🤍',
    finalSub: 'always & forever, sayang 🌸',
    photoUrl: null
  };

  let pinInput = '';
  const music = document.getElementById('bg-music');

  // ── Music Trigger Function ──
  function startExperience() {
    // Play audio on first user click to bypass browser restrictions
    if (music) {
      music.play().catch(error => console.log("Audio autoplay prevented by browser:", error));
    }
    goTo('page-pin');
  }

  // ── Petals ──
  const petalEmojis = ['🌸','🌷','🌺','🌼','💮','🏵️'];
  const petalWrap = document.getElementById('petals');
  for (let i = 0; i < 18; i++) {
    const p = document.createElement('div');
    p.className = 'petal';
    p.style.left = Math.random() * 100 + 'vw';
    p.style.animationDuration = (6 + Math.random() * 8) + 's';
    p.style.animationDelay = (Math.random() * 10) + 's';
    p.innerHTML = `<span>${petalEmojis[Math.floor(Math.random()*petalEmojis.length)]}</span>`;
    petalWrap.appendChild(p);
  }

  // ── Env flowers ──
  const envF = document.getElementById('env-flowers');
  const envEmojis = ['🌸','🌷','🌼','💐','🌺','🌹','🪷'];
  const positions = [
    [5,5],[80,5],[5,70],[85,75],[40,85],[60,10],[15,45],[75,40]
  ];
  positions.forEach(([l,t],i) => {
    const s = document.createElement('span');
    s.textContent = envEmojis[i % envEmojis.length];
    s.style.left = l + '%';
    s.style.top  = t + '%';
    s.style.animationDelay = (i * .4) + 's';
    envF.appendChild(s);
  });

  // ── Bouquet flowers ──
  const flowerLayer = document.getElementById('flower-layer');
  const bFlowers = ['🌸','🌺','🌷','🌼','🌹','💐','🪷','🌻','🏵️','💮'];
  for (let i = 0; i < 28; i++) {
    const s = document.createElement('span');
    s.textContent = bFlowers[Math.floor(Math.random() * bFlowers.length)];
    s.style.animationDelay = (Math.random() * 3) + 's';
    flowerLayer.appendChild(s);
  }

  // ── Navigation ──
  function goTo(pageId) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(pageId).classList.add('active', 'fade-in');
    window.scrollTo(0, 0);
    // Show edit btn on all pages except envelope & pin
    const editBtn = document.getElementById('edit-btn');
    editBtn.classList.toggle('show', !['page-envelope','page-pin'].includes(pageId));
  }

  // ── PIN logic ──
  function pinPress(d) {
    if (pinInput.length >= 4) return;
    pinInput += d;
    updateDots();
    document.getElementById('pin-error').textContent = '';
    if (pinInput.length === 4) {
      setTimeout(checkPin, 200);
    }
  }
  function pinDel() {
    pinInput = pinInput.slice(0, -1);
    updateDots();
    document.getElementById('pin-error').textContent = '';
  }
  function updateDots() {
    for (let i = 0; i < 4; i++) {
      document.getElementById('d' + i).classList.toggle('filled', i < pinInput.length);
    }
  }
  function checkPin() {
    if (pinInput === state.pin) {
      pinInput = '';
      updateDots();
      goTo('page-bouquet');
    } else {
      document.getElementById('pin-error').textContent = 'Salah, coba lagi 🥺';
      pinInput = '';
      updateDots();
    }
  }

  // ── Modal ──
  function openModal() {
    document.getElementById('f-name').value    = state.name;
    document.getElementById('f-pin').value     = state.pin;
    document.getElementById('f-letter').value  = state.letter;
    document.getElementById('f-from').value    = state.from;
    document.getElementById('f-caption').value = state.caption;
    document.getElementById('f-final').value   = state.finalSub;
    document.getElementById('modal-overlay').classList.add('show');
  }
  function closeModal() {
    document.getElementById('modal-overlay').classList.remove('show');
  }
  function saveModal() {
    state.name     = document.getElementById('f-name').value || 'sayang';
    state.pin      = document.getElementById('f-pin').value  || '0000';
    state.letter   = document.getElementById('f-letter').value;
    state.from     = document.getElementById('f-from').value;
    state.caption  = document.getElementById('f-caption').value;
    state.finalSub = document.getElementById('f-final').value;

    const photoFile = document.getElementById('f-photo').files[0];
    if (photoFile) {
      const reader = new FileReader();
      reader.onload = e => {
        state.photoUrl = e.target.result;
        applyState();
      };
      reader.readAsDataURL(photoFile);
    } else {
      applyState();
    }
    closeModal();
  }

  function applyState() {
    // Pin page
    document.getElementById('display-name').textContent = 'Welcome, ' + state.name;
    // Bouquet
    document.getElementById('bouquet-name-label').textContent = 'untuk ' + state.name + ' 🌸';
    // Letter
    document.getElementById('letter-to-name').textContent = state.name + ' ku';
    document.getElementById('letter-body').textContent   = state.letter;
    document.getElementById('letter-from').textContent   = state.from;
    // Photo
    document.getElementById('photo-caption').textContent = state.caption;
    if (state.photoUrl) {
      document.getElementById('photo-img').src = state.photoUrl;
      document.getElementById('photo-img').style.display = 'block';
      document.getElementById('photo-placeholder').style.display = 'none';
    }
    // Final
    document.getElementById('final-title').textContent = 'I love you, ' + state.name;
    document.getElementById('final-sub').textContent   = state.finalSub;
  }

  function restart() {
    pinInput = '';
    updateDots();
    document.getElementById('edit-btn').classList.remove('show');
    if (music) {
      music.currentTime = 0; // Reset music to beginning
    }
    goTo('page-envelope');
  }

  // Init
  applyState();
</script>
</body>
</html>

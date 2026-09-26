<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ClickBot — The Web3 Siri; Turning Onchain Wallets into Local Banks</title>
<meta name="description" content="Trade Solana tokens, pay bills, earn yield, bridge 6 chains, and cash out to your bank — all from Telegram. No app install.">
<meta property="og:title" content="ClickBot — Web3 Siri for Solana">
<meta property="og:description" content="Trade smarter. Pay bills. Earn yield. Bridge any chain. Cash out to your bank. All from Telegram.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=IBM+Plex+Mono:wght@300;400;500;600&family=Sora:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
/* ── RESET & BASE ─────────────────────────────────────────── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --bg: #060810;
  --bg2: #0A0F1A;
  --bg3: #101624;
  --border: rgba(255,255,255,0.07);
  --green: #00C864;
  --green-bright: #00E676;
  --green-dim: #00A851;
  --blue: #3B82F6;
  --blue-dim: #2563EB;
  --cyan: #00D4FF;
  --gold: #F59E0B;
  --purple: #A78BFA;
  --red: #FF4D6A;
  --text: #E8EDF4;
  --text-dim: #8FA3BC;
  --text-faint: #4A5A72;
  --card: rgba(255,255,255,0.03);
  --glow-green: 0 0 40px rgba(0,200,100,0.15);
  --glow-blue: 0 0 40px rgba(59,130,246,0.15);
  --glow-cyan: 0 0 40px rgba(0,212,255,0.15);
  --font-display: 'Playfair Display', serif;
  --font-mono: 'IBM Plex Mono', monospace;
  --font-body: 'Sora', sans-serif;
}
html { scroll-behavior: smooth; }
body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-body);
  overflow-x: hidden;
  cursor: default;
}
body::before {
  content: '';
  position: fixed; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none; z-index: 1000; opacity: 0.4;
}
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: var(--bg); }
::-webkit-scrollbar-thumb { background: var(--green-dim); border-radius: 2px; }

/* ── NAVIGATION ───────────────────────────────────────────── */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 900;
  display: flex; align-items: center; justify-content: space-between;
  padding: 20px 48px;
  background: rgba(6,8,16,0.7);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border);
  transition: padding 0.3s ease;
}
nav.scrolled { padding: 14px 48px; }
.nav-logo { display: flex; align-items: center; gap: 10px; text-decoration: none; }
.footer-logo { height: 80px; width: auto; }
.nav-logo-mark {
  width: 32px; height: 32px; background: var(--green);
  border-radius: 8px; display: grid; place-items: center;
  font-family: var(--font-mono); font-weight: 600; font-size: 14px; color: #000;
}
.nav-logo-img { width: auto; height: 42px; object-fit: contain; }
.nav-logo-text { font-family: var(--font-mono); font-size: 15px; font-weight: 500; color: var(--text); letter-spacing: 0.02em; }
.nav-logo-text span { color: var(--green); }
.nav-links { display: flex; align-items: center; gap: 28px; list-style: none; }
.nav-links a {
  font-size: 13px; font-weight: 400; color: var(--text-dim);
  text-decoration: none; font-family: var(--font-mono);
  transition: color 0.2s; letter-spacing: 0.02em;
}
.nav-links a:hover { color: var(--green); }
.nav-cta {
  background: var(--green); color: #000 !important;
  padding: 9px 20px; border-radius: 6px;
  font-weight: 600 !important; font-size: 12px !important;
  letter-spacing: 0.04em !important; transition: all 0.2s !important;
}
.nav-cta:hover {
  background: #fff !important; color: #000 !important;
  transform: translateY(-1px); box-shadow: 0 4px 20px rgba(0,200,100,0.3) !important;
}

/* ── HERO ─────────────────────────────────────────────────── */
#hero { min-height: 100vh; display: flex; align-items: center; position: relative; overflow: hidden; padding: 120px 48px 80px; }
.hero-grid-bg {
  position: absolute; inset: 0;
  background-image:
    linear-gradient(rgba(0,200,100,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,200,100,0.03) 1px, transparent 1px);
  background-size: 60px 60px;
  mask-image: radial-gradient(ellipse 80% 60% at 50% 50%, black, transparent);
}
.hero-orb-1 { position: absolute; width: 600px; height: 600px; background: radial-gradient(circle, rgba(0,200,100,0.08) 0%, transparent 70%); top: -100px; left: -100px; pointer-events: none; animation: orbFloat 8s ease-in-out infinite; }
.hero-orb-2 { position: absolute; width: 400px; height: 400px; background: radial-gradient(circle, rgba(59,130,246,0.06) 0%, transparent 70%); bottom: 0; right: 10%; pointer-events: none; animation: orbFloat 10s ease-in-out infinite reverse; }
@keyframes orbFloat { 0%, 100% { transform: translate(0, 0); } 50% { transform: translate(20px, -30px); } }
.hero-inner { position: relative; z-index: 10; max-width: 1200px; margin: 0 auto; display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center; width: 100%; }
.hero-badge {
  display: inline-flex; align-items: center; gap: 8px;
  background: rgba(0,200,100,0.08); border: 1px solid rgba(0,200,100,0.2);
  border-radius: 100px; padding: 6px 14px; margin-bottom: 28px;
  font-family: var(--font-mono); font-size: 11px; color: var(--green);
  letter-spacing: 0.08em; text-transform: uppercase;
}
.hero-badge::before { content: ''; width: 6px; height: 6px; background: var(--green); border-radius: 50%; animation: pulse 2s ease-in-out infinite; }
@keyframes pulse { 0%, 100% { opacity: 1; transform: scale(1); } 50% { opacity: 0.5; transform: scale(0.8); } }
.hero-headline { font-family: var(--font-display); font-size: clamp(42px, 5vw, 72px); font-weight: 900; line-height: 1.05; letter-spacing: -0.02em; margin-bottom: 24px; }
.hero-headline em { font-style: italic; color: var(--green); }
.hero-sub { font-size: 17px; line-height: 1.7; color: var(--text-dim); max-width: 480px; margin-bottom: 40px; font-weight: 300; }
.hero-ctas { display: flex; gap: 16px; flex-wrap: wrap; margin-bottom: 56px; }
.btn-primary {
  display: inline-flex; align-items: center; gap: 10px;
  background: var(--green); color: #000; padding: 14px 28px; border-radius: 8px;
  font-family: var(--font-mono); font-weight: 600; font-size: 13px; letter-spacing: 0.04em;
  text-decoration: none; transition: all 0.25s cubic-bezier(0.34, 1.56, 0.64, 1);
  box-shadow: 0 0 30px rgba(0,200,100,0.2);
}
.btn-primary:hover { transform: translateY(-2px) scale(1.02); box-shadow: 0 8px 40px rgba(0,200,100,0.35); background: #fff; }
.btn-primary .icon { font-size: 18px; }
.btn-secondary {
  display: inline-flex; align-items: center; gap: 10px;
  background: transparent; color: var(--text); padding: 14px 28px; border-radius: 8px;
  font-family: var(--font-mono); font-weight: 500; font-size: 13px; letter-spacing: 0.04em;
  text-decoration: none; border: 1px solid var(--border); transition: all 0.25s;
}
.btn-secondary:hover { border-color: var(--green); color: var(--green); transform: translateY(-2px); }
.hero-stats { display: flex; gap: 40px; }
.hero-stat-num { font-family: var(--font-mono); font-size: 28px; font-weight: 600; color: var(--text); display: flex; align-items: baseline; gap: 4px; }
.hero-stat-num span { font-size: 14px; color: var(--green); }
.hero-stat-label { font-size: 11px; color: var(--text-faint); font-family: var(--font-mono); letter-spacing: 0.06em; text-transform: uppercase; margin-top: 4px; }

/* ── PHONE MOCKUP ─────────────────────────────────────────── */
.hero-phone-wrap { display: flex; justify-content: center; align-items: center; position: relative; }
.phone-mockup {
  width: 260px; background: #0C1018; border-radius: 40px;
  border: 1.5px solid rgba(255,255,255,0.12);
  box-shadow: 0 0 0 8px rgba(255,255,255,0.03), 0 40px 80px rgba(0,0,0,0.8), var(--glow-green);
  overflow: hidden; position: relative; animation: phoneFloat 6s ease-in-out infinite;
}
@keyframes phoneFloat { 0%, 100% { transform: translateY(0) rotate(-2deg); } 50% { transform: translateY(-12px) rotate(-1deg); } }
.phone-notch { width: 90px; height: 24px; background: #0C1018; border-radius: 0 0 16px 16px; margin: 0 auto; position: relative; z-index: 10; border: 1.5px solid rgba(255,255,255,0.08); border-top: none; }
.phone-screen { background: #0A0E16; min-height: 480px; padding: 16px 12px 20px; font-family: var(--font-mono); font-size: 9px; overflow: hidden; }
.phone-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 16px; }
.phone-header-title { font-size: 11px; font-weight: 600; color: var(--text); }
.phone-balance-card { background: linear-gradient(135deg, #0D2018, #091A10); border: 1px solid rgba(0,200,100,0.15); border-radius: 12px; padding: 14px; margin-bottom: 12px; position: relative; overflow: hidden; }
.phone-balance-card::before { content: ''; position: absolute; top: -20px; right: -20px; width: 80px; height: 80px; background: radial-gradient(circle, rgba(0,200,100,0.1), transparent); }
.phone-balance-label { font-size: 8px; color: var(--text-faint); letter-spacing: 0.06em; text-transform: uppercase; margin-bottom: 6px; }
.phone-balance-amount { font-size: 22px; font-weight: 600; color: var(--green); margin-bottom: 4px; }
.phone-balance-usd { font-size: 8px; color: var(--text-dim); }
.phone-menu-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 12px; }
.phone-menu-btn { background: rgba(255,255,255,0.04); border: 1px solid var(--border); border-radius: 10px; padding: 10px 8px; text-align: center; cursor: pointer; transition: all 0.2s; }
.phone-menu-btn:hover { border-color: var(--green); background: rgba(0,200,100,0.06); }
.phone-menu-btn .menu-icon { font-size: 16px; margin-bottom: 4px; }
.phone-menu-btn .menu-label { font-size: 7.5px; color: var(--text-dim); }
.phone-analysis { background: rgba(0,200,100,0.05); border: 1px solid rgba(0,200,100,0.2); border-radius: 10px; padding: 10px; margin-top: 8px; }
.analysis-token { font-size: 10px; font-weight: 600; color: var(--green); }
.analysis-row { display: flex; justify-content: space-between; margin-top: 5px; font-size: 8px; color: var(--text-dim); }
.analysis-row .val { color: var(--text); }
.analysis-verdict { margin-top: 8px; padding: 4px 8px; background: rgba(0,200,100,0.15); border-radius: 4px; font-size: 8px; color: var(--green); font-weight: 600; text-align: center; letter-spacing: 0.06em; }
.float-chip { position: absolute; background: var(--bg3); border: 1px solid var(--border); border-radius: 12px; padding: 8px 14px; font-family: var(--font-mono); font-size: 10px; white-space: nowrap; backdrop-filter: blur(10px); }
.float-chip.green { border-color: rgba(0,200,100,0.3); color: var(--green); }
.float-chip.cyan { border-color: rgba(0,212,255,0.3); color: var(--cyan); }
.float-chip.gold { border-color: rgba(245,158,11,0.3); color: var(--gold); }
.chip-1 { top: 10%; left: -20%; animation: chipFloat 7s ease-in-out infinite; }
.chip-2 { top: 35%; right: -25%; animation: chipFloat 9s ease-in-out infinite 1s; }
.chip-3 { bottom: 20%; left: -15%; animation: chipFloat 8s ease-in-out infinite 2s; }
.chip-4 { bottom: 35%; right: -20%; animation: chipFloat 6s ease-in-out infinite 0.5s; }
@keyframes chipFloat { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-8px); } }

/* ── TICKER ───────────────────────────────────────────────── */
.ticker-wrap { background: var(--bg2); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); overflow: hidden; padding: 10px 0; }
.ticker-track { display: flex; gap: 0; animation: ticker 30s linear infinite; width: max-content; }
.ticker-track:hover { animation-play-state: paused; }
@keyframes ticker { from { transform: translateX(0); } to { transform: translateX(-50%); } }
.ticker-item { display: flex; align-items: center; gap: 8px; padding: 0 32px; font-family: var(--font-mono); font-size: 11px; border-right: 1px solid var(--border); white-space: nowrap; }
.ticker-symbol { color: var(--text); font-weight: 500; }
.ticker-price { color: var(--text-dim); }
.ticker-change.up { color: var(--green); }
.ticker-change.down { color: var(--red); }

/* ── SECTION BASE ─────────────────────────────────────────── */
section { padding: 120px 48px; }
.section-inner { max-width: 1200px; margin: 0 auto; }
.section-label { font-family: var(--font-mono); font-size: 10px; color: var(--green); letter-spacing: 0.12em; text-transform: uppercase; margin-bottom: 16px; display: flex; align-items: center; gap: 12px; }
.section-label::before { content: ''; display: block; width: 24px; height: 1px; background: var(--green); }
.section-title { font-family: var(--font-display); font-size: clamp(32px, 4vw, 54px); font-weight: 700; line-height: 1.1; letter-spacing: -0.02em; margin-bottom: 20px; }
.section-title em { font-style: italic; color: var(--green); }
.section-body { font-size: 16px; line-height: 1.8; color: var(--text-dim); max-width: 560px; font-weight: 300; }

/* ── THREE PILLARS ────────────────────────────────────────── */
#pillars { background: var(--bg); border-top: 1px solid var(--border); }
.pillars-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; margin-top: 60px; }
.pillar-card {
  background: var(--bg3); border: 1px solid var(--border); border-radius: 20px;
  padding: 36px 30px; position: relative; overflow: hidden; transition: all 0.3s;
  text-decoration: none; display: block;
}
.pillar-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 3px; background: var(--pillar-color, var(--green)); opacity: 0.7; }
.pillar-card:hover { transform: translateY(-6px); border-color: var(--pillar-color, var(--green)); box-shadow: 0 20px 50px rgba(0,0,0,0.4); }
.pillar-icon { font-size: 40px; margin-bottom: 20px; display: block; }
.pillar-name { font-family: var(--font-display); font-size: 26px; font-weight: 700; margin-bottom: 8px; color: var(--text); letter-spacing: -0.01em; }
.pillar-tagline { font-size: 13px; color: var(--pillar-color, var(--green)); font-family: var(--font-mono); margin-bottom: 20px; letter-spacing: 0.02em; }
.pillar-list { list-style: none; }
.pillar-list li { display: flex; gap: 10px; align-items: flex-start; font-size: 13px; padding: 7px 0; color: var(--text-dim); line-height: 1.5; }
.pillar-list li::before { content: '→'; color: var(--pillar-color, var(--green)); flex-shrink: 0; font-weight: 600; }
.pillar-link { display: inline-flex; align-items: center; gap: 6px; margin-top: 20px; font-family: var(--font-mono); font-size: 12px; color: var(--pillar-color, var(--green)); font-weight: 600; }

/* ── VIDEO SHOWCASE ───────────────────────────────────────── */
#videos { background: var(--bg2); border-top: 1px solid var(--border); }
.video-tabs { display: flex; gap: 10px; justify-content: center; margin: 40px 0 48px; flex-wrap: wrap; }
.video-tab {
  padding: 10px 24px; border-radius: 10px; font-family: var(--font-mono); font-size: 13px; font-weight: 600;
  border: 1px solid var(--border); background: transparent; color: var(--text-dim); cursor: pointer; transition: all 0.2s;
}
.video-tab.active { background: rgba(0,200,100,0.12); border-color: rgba(0,200,100,0.3); color: var(--green); }
.video-stage { max-width: 380px; margin: 0 auto; }
.video-frame {
  position: relative; border-radius: 32px; overflow: hidden;
  border: 2px solid rgba(255,255,255,0.1);
  box-shadow: 0 0 0 8px rgba(255,255,255,0.02), 0 40px 90px rgba(0,0,0,0.7), var(--glow-green);
  aspect-ratio: 9 / 16; background: #000;
}
.video-frame iframe { position: absolute; inset: 0; width: 100%; height: 100%; border: 0; }
.video-caption { text-align: center; margin-top: 24px; font-size: 14px; color: var(--text-dim); font-weight: 300; }
.video-unmute-hint { display: inline-flex; align-items: center; gap: 6px; margin-top: 12px; font-family: var(--font-mono); font-size: 11px; color: var(--text-faint); }

/* ── MULTICHAIN ───────────────────────────────────────────── */
#multichain { background: var(--bg); border-top: 1px solid var(--border); }
.chain-badges { display: flex; flex-wrap: wrap; gap: 12px; justify-content: center; margin: 48px 0; }
.chain-badge {
  display: inline-flex; align-items: center; gap: 8px; padding: 12px 22px;
  background: var(--bg3); border: 1px solid var(--border); border-radius: 100px;
  font-family: var(--font-mono); font-size: 14px; font-weight: 500; color: var(--text);
  transition: all 0.25s;
}
.chain-badge:hover { border-color: var(--green); transform: translateY(-2px); }
.chain-badge .dot { width: 8px; height: 8px; border-radius: 50%; }
.chain-flow { display: grid; grid-template-columns: repeat(4, 1fr); gap: 2px; margin-top: 40px; position: relative; }
.chain-flow::before { content: ''; position: absolute; top: 28px; left: 10%; right: 10%; height: 1px; background: linear-gradient(90deg, transparent, var(--green), var(--blue), transparent); z-index: 0; }
.chain-step { background: var(--bg3); border: 1px solid var(--border); border-radius: 16px; padding: 28px 22px; position: relative; z-index: 1; transition: all 0.3s; }
.chain-step:hover { border-color: var(--green); transform: translateY(-4px); box-shadow: var(--glow-green); }
.chain-step-num { width: 40px; height: 40px; background: var(--bg); border: 1px solid var(--green); border-radius: 50%; display: grid; place-items: center; font-family: var(--font-mono); font-size: 13px; font-weight: 600; color: var(--green); margin-bottom: 18px; }
.chain-step-title { font-family: var(--font-display); font-size: 17px; font-weight: 700; margin-bottom: 8px; letter-spacing: -0.01em; }
.chain-step-desc { font-size: 12px; line-height: 1.7; color: var(--text-dim); font-weight: 300; }
.chain-warning { margin-top: 40px; background: rgba(245,158,11,0.06); border: 1px solid rgba(245,158,11,0.2); border-radius: 14px; padding: 20px 24px; display: flex; gap: 16px; align-items: flex-start; }
.chain-warning-icon { font-size: 22px; flex-shrink: 0; }
.chain-warning-text { font-size: 13px; color: var(--text-dim); line-height: 1.7; }
.chain-warning-text strong { color: var(--gold); }

/* ── STATEMENT / GASLESS FEATURE STRIP ────────────────────── */
#extras { background: var(--bg2); border-top: 1px solid var(--border); }
.extras-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 60px; }
.extra-card {
  background: var(--bg3); border: 1px solid var(--border); border-radius: 20px;
  padding: 40px 36px; position: relative; overflow: hidden; transition: all 0.3s;
}
.extra-card:hover { border-color: var(--green); transform: translateY(-4px); }
.extra-icon { font-size: 36px; margin-bottom: 20px; display: block; }
.extra-name { font-family: var(--font-display); font-size: 24px; font-weight: 700; margin-bottom: 12px; letter-spacing: -0.01em; }
.extra-desc { font-size: 14px; line-height: 1.7; color: var(--text-dim); font-weight: 300; }
.extra-tag { display: inline-block; margin-top: 18px; font-family: var(--font-mono); font-size: 9px; color: var(--green); letter-spacing: 0.08em; text-transform: uppercase; border-bottom: 1px solid rgba(0,200,100,0.3); padding-bottom: 2px; }

/* mini statement visual */
.statement-preview { margin-top: 24px; background: var(--bg); border: 1px solid var(--border); border-radius: 12px; padding: 16px; font-family: var(--font-mono); }
.stmt-head { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid var(--border); padding-bottom: 10px; margin-bottom: 10px; }
.stmt-title { font-size: 11px; font-weight: 600; color: var(--text); }
.stmt-period { font-size: 8px; color: var(--text-faint); }
.stmt-row { display: flex; justify-content: space-between; padding: 5px 0; font-size: 9px; }
.stmt-row .desc { color: var(--text-dim); }
.stmt-row .amt.pos { color: var(--green); }
.stmt-row .amt.neg { color: var(--red); }

/* ── TESTIMONIALS ─────────────────────────────────────────── */
#testimonials { background: var(--bg); border-top: 1px solid var(--border); overflow: hidden; }
.testi-viewport { margin-top: 60px; overflow: hidden; position: relative; -webkit-mask-image: linear-gradient(90deg, transparent, black 6%, black 94%, transparent); mask-image: linear-gradient(90deg, transparent, black 6%, black 94%, transparent); }
.testi-track { display: flex; gap: 20px; width: max-content; animation: testiScroll 60s linear infinite; }
.testi-track:hover { animation-play-state: paused; }
@keyframes testiScroll { from { transform: translateX(0); } to { transform: translateX(-50%); } }
.testi-card {
  width: 340px; flex-shrink: 0; background: var(--bg3); border: 1px solid var(--border);
  border-radius: 18px; padding: 28px; display: flex; flex-direction: column; gap: 16px;
}
.testi-quote { font-size: 14px; line-height: 1.7; color: var(--text); font-weight: 300; flex: 1; }
.testi-feature { display: inline-block; align-self: flex-start; font-family: var(--font-mono); font-size: 9px; letter-spacing: 0.06em; text-transform: uppercase; padding: 3px 10px; border-radius: 100px; background: rgba(0,200,100,0.1); color: var(--green); }
.testi-person { display: flex; align-items: center; gap: 12px; }
.testi-avatar { width: 40px; height: 40px; border-radius: 50%; display: grid; place-items: center; font-weight: 700; font-size: 15px; color: #000; flex-shrink: 0; }
.testi-name { font-size: 14px; font-weight: 600; color: var(--text); }
.testi-loc { font-size: 11px; color: var(--text-faint); }

/* ── AGENT STREAM ─────────────────────────────────────────── */
#agent-stream { background: var(--bg2); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); padding: 100px 48px; position: relative; overflow: hidden; }
.stream-bg { position: absolute; inset: 0; background: radial-gradient(ellipse 60% 40% at 50% 50%, rgba(0,200,100,0.04), transparent); }
.stream-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center; position: relative; z-index: 2; }
.stream-terminal { background: #080B12; border: 1px solid rgba(0,200,100,0.2); border-radius: 16px; overflow: hidden; box-shadow: var(--glow-green), 0 40px 80px rgba(0,0,0,0.5); }
.terminal-bar { background: #0D1220; padding: 12px 16px; display: flex; align-items: center; gap: 8px; border-bottom: 1px solid var(--border); }
.terminal-dot { width: 10px; height: 10px; border-radius: 50%; }
.terminal-dot.r { background: #FF5F57; }
.terminal-dot.y { background: #FFBD2E; }
.terminal-dot.g { background: #28CA41; }
.terminal-title { font-family: var(--font-mono); font-size: 10px; color: var(--text-faint); margin-left: 8px; letter-spacing: 0.04em; }
.terminal-body { padding: 20px; min-height: 320px; font-family: var(--font-mono); font-size: 11px; line-height: 1.8; }
.stream-line { display: flex; gap: 10px; margin-bottom: 6px; opacity: 0; transform: translateY(4px); animation: lineIn 0.3s ease forwards; }
@keyframes lineIn { to { opacity: 1; transform: translateY(0); } }
.stream-agent { font-size: 10px; font-weight: 600; white-space: nowrap; padding: 1px 6px; border-radius: 3px; }
.agent-analyzer { background: rgba(0,200,100,0.12); color: var(--green); }
.agent-sniper { background: rgba(0,212,255,0.12); color: var(--cyan); }
.agent-guardian { background: rgba(245,158,11,0.12); color: var(--gold); }
.agent-executor { background: rgba(255,77,106,0.12); color: var(--red); }
.stream-msg { color: var(--text-dim); }
.stream-msg .highlight { color: var(--text); }
.stream-msg .val-green { color: var(--green); }
.stream-msg .val-red { color: var(--red); }
.stream-msg .val-cyan { color: var(--cyan); }
.stream-msg .val-gold { color: var(--gold); }
.stream-cursor { display: inline-block; width: 7px; height: 12px; background: var(--green); margin-left: 2px; vertical-align: middle; animation: blink 1s step-end infinite; }
@keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

/* ── FEATURES ─────────────────────────────────────────────── */
#features { background: var(--bg); }
.features-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 2px; margin-top: 80px; border: 1px solid var(--border); border-radius: 20px; overflow: hidden; }
.feature-card { background: var(--card); padding: 40px 32px; border-right: 1px solid var(--border); border-bottom: 1px solid var(--border); transition: background 0.3s; position: relative; overflow: hidden; }
.feature-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: linear-gradient(90deg, transparent, var(--green), transparent); opacity: 0; transition: opacity 0.3s; }
.feature-card:hover { background: rgba(0,200,100,0.03); }
.feature-card:hover::before { opacity: 1; }
.feature-card:nth-child(3n) { border-right: none; }
.feature-card:nth-child(n+7) { border-bottom: none; }
.feature-icon { font-size: 32px; margin-bottom: 20px; display: block; }
.feature-name { font-family: var(--font-display); font-size: 20px; font-weight: 700; margin-bottom: 10px; letter-spacing: -0.01em; }
.feature-desc { font-size: 13px; line-height: 1.7; color: var(--text-dim); font-weight: 300; }
.feature-tag { display: inline-block; margin-top: 16px; font-family: var(--font-mono); font-size: 9px; color: var(--green); letter-spacing: 0.08em; text-transform: uppercase; border-bottom: 1px solid rgba(0,200,100,0.3); padding-bottom: 2px; }

/* ── SCREENS SHOWCASE ─────────────────────────────────────── */
#screens { background: var(--bg2); border-top: 1px solid var(--border); }
.screens-header { text-align: center; margin-bottom: 80px; }
.screens-header .section-label { justify-content: center; }
.screens-header .section-label::before { display: none; }
.screens-row { display: flex; gap: 32px; justify-content: center; align-items: flex-end; flex-wrap: wrap; }
.screen-item { display: flex; flex-direction: column; align-items: center; gap: 20px; flex: 0 0 auto; }
.screen-label { font-family: var(--font-mono); font-size: 10px; color: var(--text-faint); letter-spacing: 0.06em; text-transform: uppercase; text-align: center; }
.phone-sm { width: 200px; }
.phone-md { width: 230px; }
.phone-lg { width: 260px; transform: translateY(-20px); }
.screen-phone { background: #0C1018; border-radius: 32px; border: 1.5px solid rgba(255,255,255,0.1); overflow: hidden; box-shadow: 0 0 0 6px rgba(255,255,255,0.03), 0 30px 60px rgba(0,0,0,0.7); transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 0.4s; }
.screen-phone:hover { transform: translateY(-8px) scale(1.02) !important; box-shadow: 0 0 0 6px rgba(255,255,255,0.05), 0 50px 80px rgba(0,0,0,0.8), var(--glow-green); }
.screen-notch { width: 70px; height: 18px; background: #0C1018; border-radius: 0 0 12px 12px; margin: 0 auto; border: 1.5px solid rgba(255,255,255,0.06); border-top: none; }
.screen-body { padding: 12px 10px 16px; font-family: var(--font-mono); background: #0A0E16; min-height: 380px; }
.s-header { text-align: center; margin-bottom: 14px; }
.s-welcome { font-size: 8px; color: var(--text-faint); margin-bottom: 2px; }
.s-title { font-size: 12px; font-weight: 600; color: var(--text); }
.s-wallet-strip { background: linear-gradient(135deg, #0D2018, #091015); border: 1px solid rgba(0,200,100,0.15); border-radius: 10px; padding: 10px; margin-bottom: 12px; display: flex; justify-content: space-between; align-items: center; }
.s-sol { font-size: 14px; font-weight: 600; color: var(--green); }
.s-usd { font-size: 7px; color: var(--text-dim); margin-top: 2px; }
.s-wallet-icon { font-size: 20px; }
.s-btn { border-radius: 8px; padding: 9px 10px; margin-bottom: 6px; display: flex; align-items: center; gap: 8px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); font-size: 8px; }
.s-btn-icon { font-size: 14px; }
.s-btn-text { color: var(--text); font-weight: 500; }
.s-btn-sub { color: var(--text-faint); font-size: 7px; }
.s-btn-arr { color: var(--text-faint); margin-left: auto; }
.s-btn.active { border-color: rgba(0,200,100,0.25); background: rgba(0,200,100,0.05); }
.s-section-title { font-size: 10px; font-weight: 600; color: var(--green); margin-bottom: 10px; letter-spacing: 0.04em; }
.s-token-header { display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 10px; }
.s-token-name { font-size: 11px; font-weight: 600; color: var(--text); }
.s-token-price { font-size: 10px; color: var(--green); }
.s-token-change { font-size: 7px; }
.s-token-change.up { color: var(--green); }
.s-metric-row { display: flex; justify-content: space-between; padding: 5px 0; border-bottom: 1px solid rgba(255,255,255,0.04); font-size: 7.5px; }
.s-metric-key { color: var(--text-faint); }
.s-metric-val { color: var(--text); }
.s-verdict { margin-top: 10px; padding: 8px; border-radius: 8px; text-align: center; }
.s-verdict.buy { background: rgba(0,200,100,0.12); border: 1px solid rgba(0,200,100,0.25); }
.s-verdict.avoid { background: rgba(255,77,106,0.12); border: 1px solid rgba(255,77,106,0.25); }
.s-verdict-label { font-size: 9px; font-weight: 600; }
.s-verdict.buy .s-verdict-label { color: var(--green); }
.s-verdict.avoid .s-verdict-label { color: var(--red); }
.s-verdict-conf { font-size: 7px; color: var(--text-faint); margin-top: 2px; }
.s-success-icon { text-align: center; font-size: 28px; margin: 12px 0 8px; }
.s-success-title { text-align: center; font-size: 11px; font-weight: 600; color: var(--green); margin-bottom: 12px; }
.s-trade-row { display: flex; justify-content: space-between; padding: 6px 0; border-bottom: 1px solid rgba(255,255,255,0.04); font-size: 7.5px; }
.s-trade-key { color: var(--text-faint); }
.s-trade-val { color: var(--text); }
.s-trade-val.green { color: var(--green); }
.s-action-row { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 4px; margin-top: 10px; }
.s-action-btn { border-radius: 6px; padding: 6px 4px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); text-align: center; font-size: 7px; color: var(--text-dim); }
.s-action-btn .a-icon { font-size: 12px; display: block; margin-bottom: 2px; }
.s-bank-card { background: linear-gradient(135deg, #0D1520, #090E18); border: 1px solid rgba(0,212,255,0.15); border-radius: 10px; padding: 10px; margin-bottom: 10px; }
.s-bank-name { font-size: 8px; color: var(--text-dim); }
.s-bank-acct { font-size: 10px; font-weight: 600; color: var(--text); margin-top: 2px; }
.s-rate-row { display: flex; justify-content: space-between; padding: 5px 0; font-size: 7.5px; }
.s-rate-key { color: var(--text-faint); }
.s-rate-val { color: var(--cyan); }
.s-confirm-btn { width: 100%; margin-top: 10px; background: var(--green); color: #000; border-radius: 8px; padding: 9px; font-size: 9px; font-weight: 700; text-align: center; letter-spacing: 0.04em; }

/* ── HOW IT WORKS ─────────────────────────────────────────── */
#how-it-works { background: var(--bg); }
.steps-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 2px; margin-top: 80px; position: relative; }
.steps-grid::before { content: ''; position: absolute; top: 28px; left: 10%; right: 10%; height: 1px; background: linear-gradient(90deg, transparent, var(--green), var(--cyan), transparent); z-index: 0; }
.step-card { background: var(--bg3); border: 1px solid var(--border); border-radius: 16px; padding: 32px 24px; position: relative; z-index: 1; transition: all 0.3s; }
.step-card:hover { border-color: var(--green); transform: translateY(-4px); box-shadow: var(--glow-green); }
.step-num { width: 44px; height: 44px; background: var(--bg); border: 1px solid var(--green); border-radius: 50%; display: grid; place-items: center; font-family: var(--font-mono); font-size: 14px; font-weight: 600; color: var(--green); margin-bottom: 20px; }
.step-title { font-family: var(--font-display); font-size: 18px; font-weight: 700; margin-bottom: 10px; letter-spacing: -0.01em; }
.step-desc { font-size: 12px; line-height: 1.7; color: var(--text-dim); font-weight: 300; }

/* ── NGN SECTION ──────────────────────────────────────────── */
#ngn { background: linear-gradient(180deg, var(--bg2) 0%, var(--bg) 100%); border-top: 1px solid var(--border); }
.ngn-inner { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center; }
.ngn-flow { display: flex; flex-direction: column; gap: 0; }
.ngn-step { display: flex; gap: 20px; align-items: flex-start; padding: 20px 0; border-bottom: 1px solid var(--border); position: relative; }
.ngn-step:last-child { border-bottom: none; }
.ngn-step-num { width: 32px; height: 32px; flex-shrink: 0; background: rgba(0,212,255,0.1); border: 1px solid rgba(0,212,255,0.25); border-radius: 50%; display: grid; place-items: center; font-family: var(--font-mono); font-size: 11px; color: var(--cyan); font-weight: 600; }
.ngn-step-title { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
.ngn-step-desc { font-size: 12px; color: var(--text-dim); line-height: 1.6; font-weight: 300; }
.ngn-rate-card { background: var(--bg3); border: 1px solid rgba(0,212,255,0.15); border-radius: 20px; padding: 32px; box-shadow: var(--glow-cyan); }
.ngn-rate-title { font-family: var(--font-mono); font-size: 10px; color: var(--cyan); letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 20px; }
.ngn-rate-row { display: flex; justify-content: space-between; align-items: center; padding: 14px 0; border-bottom: 1px solid var(--border); }
.ngn-rate-row:last-child { border-bottom: none; }
.ngn-rate-label { font-size: 12px; color: var(--text-dim); }
.ngn-rate-value { font-family: var(--font-mono); font-size: 18px; font-weight: 600; color: var(--text); }
.ngn-rate-value.green { color: var(--green); }
.ngn-rate-value.cyan { color: var(--cyan); }

/* ── PRICING ──────────────────────────────────────────────── */
#pricing { background: var(--bg); }
.pricing-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; margin-top: 80px; }
.pricing-card { background: var(--bg3); border: 1px solid var(--border); border-radius: 20px; padding: 36px 28px; position: relative; transition: all 0.3s; }
.pricing-card.featured { border-color: var(--green); box-shadow: var(--glow-green); }
.pricing-card:hover { transform: translateY(-6px); border-color: var(--green); }
.pricing-featured-badge { position: absolute; top: -12px; left: 50%; transform: translateX(-50%); background: var(--green); color: #000; font-family: var(--font-mono); font-size: 9px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase; padding: 4px 14px; border-radius: 100px; white-space: nowrap; }
.pricing-tier { font-family: var(--font-mono); font-size: 10px; color: var(--text-faint); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 16px; }
.pricing-price { font-family: var(--font-mono); font-size: 40px; font-weight: 600; color: var(--text); margin-bottom: 4px; letter-spacing: -0.02em; }
.pricing-price sup { font-size: 18px; color: var(--text-dim); vertical-align: super; }
.pricing-price sub { font-size: 14px; color: var(--text-faint); }
.pricing-subtitle { font-size: 12px; color: var(--text-dim); margin-bottom: 28px; }
.pricing-features { list-style: none; margin-bottom: 32px; }
.pricing-features li { display: flex; gap: 10px; align-items: flex-start; font-size: 12px; padding: 8px 0; border-bottom: 1px solid var(--border); color: var(--text-dim); }
.pricing-features li:last-child { border-bottom: none; }
.pricing-features li::before { content: '✓'; color: var(--green); font-family: var(--font-mono); font-weight: 600; flex-shrink: 0; }
.pricing-cta { display: block; width: 100%; text-align: center; padding: 13px; border-radius: 8px; font-family: var(--font-mono); font-size: 12px; font-weight: 600; letter-spacing: 0.04em; text-decoration: none; transition: all 0.25s; }
.pricing-cta.outline { border: 1px solid var(--border); color: var(--text); }
.pricing-cta.outline:hover { border-color: var(--green); color: var(--green); }
.pricing-cta.solid { background: var(--green); color: #000; }
.pricing-cta.solid:hover { background: #fff; box-shadow: 0 4px 24px rgba(0,200,100,0.3); }

/* ── PROOF ────────────────────────────────────────────────── */
#proof { background: var(--bg2); border-top: 1px solid var(--border); border-bottom: 1px solid var(--border); }
.proof-stats { display: grid; grid-template-columns: repeat(4, 1fr); gap: 2px; background: var(--border); border: 1px solid var(--border); border-radius: 20px; overflow: hidden; margin-bottom: 80px; }
.proof-stat-card { background: var(--bg3); padding: 40px 32px; text-align: center; transition: background 0.3s; }
.proof-stat-card:hover { background: rgba(0,200,100,0.03); }
.proof-stat-num { font-family: var(--font-mono); font-size: 42px; font-weight: 600; color: var(--green); letter-spacing: -0.02em; margin-bottom: 8px; }
.proof-stat-label { font-size: 11px; color: var(--text-faint); letter-spacing: 0.06em; text-transform: uppercase; font-family: var(--font-mono); }

/* ── CTA ──────────────────────────────────────────────────── */
#final-cta { padding: 160px 48px; text-align: center; position: relative; overflow: hidden; }
.cta-bg { position: absolute; inset: 0; background: radial-gradient(ellipse 70% 50% at 50% 50%, rgba(0,200,100,0.06), transparent), radial-gradient(ellipse 40% 30% at 30% 70%, rgba(59,130,246,0.04), transparent); }
.cta-headline { font-family: var(--font-display); font-size: clamp(40px, 6vw, 80px); font-weight: 900; line-height: 1.0; letter-spacing: -0.03em; max-width: 800px; margin: 0 auto 24px; position: relative; z-index: 2; }
.cta-headline em { font-style: italic; color: var(--green); }
.cta-sub { font-size: 16px; color: var(--text-dim); max-width: 480px; margin: 0 auto 48px; line-height: 1.7; font-weight: 300; position: relative; z-index: 2; }
.cta-buttons { display: flex; gap: 16px; justify-content: center; flex-wrap: wrap; position: relative; z-index: 2; }

/* ── FOOTER ───────────────────────────────────────────────── */
footer { background: var(--bg2); border-top: 1px solid var(--border); padding: 60px 48px 40px; }
.footer-inner { max-width: 1200px; margin: 0 auto; display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 60px; margin-bottom: 48px; }
.footer-brand-desc { font-size: 13px; color: var(--text-faint); line-height: 1.7; margin-top: 16px; max-width: 280px; font-weight: 300; }
.footer-col-title { font-family: var(--font-mono); font-size: 10px; color: var(--text-dim); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 20px; }
.footer-links { list-style: none; }
.footer-links li { margin-bottom: 12px; }
.footer-links a { font-size: 13px; color: var(--text-faint); text-decoration: none; transition: color 0.2s; }
.footer-links a:hover { color: var(--green); }
.footer-bottom { max-width: 1200px; margin: 0 auto; display: flex; justify-content: space-between; align-items: center; padding-top: 24px; border-top: 1px solid var(--border); font-family: var(--font-mono); font-size: 11px; color: var(--text-faint); }

/* ── REVEAL ───────────────────────────────────────────────── */
.reveal { opacity: 0; transform: translateY(30px); transition: opacity 0.7s ease, transform 0.7s ease; }
.reveal.visible { opacity: 1; transform: translateY(0); }
.reveal-delay-1 { transition-delay: 0.1s; }
.reveal-delay-2 { transition-delay: 0.2s; }
.reveal-delay-3 { transition-delay: 0.3s; }
.reveal-delay-4 { transition-delay: 0.4s; }

/* ── LIVE STATS ───────────────────────────────────────────── */
.stat-pulse-dot { --dot-color: #00C864; position: relative; display: inline-flex; width: 8px; height: 8px; }
.stat-pulse-dot::before { content: ''; position: absolute; inset: 0; border-radius: 50%; background: var(--dot-color); animation: statPulse 1.6s ease-in-out infinite; opacity: 0.5; }
.stat-pulse-dot::after { content: ''; position: absolute; inset: 1px; border-radius: 50%; background: var(--dot-color); }
@keyframes statPulse { 0%, 100% { transform: scale(1); opacity: 0.5; } 50% { transform: scale(2); opacity: 0; } }
.stat-hero-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 12px; padding: 20px; position: relative; overflow: hidden; transition: transform 0.25s, border-color 0.25s; }
.stat-hero-card:hover { transform: translateY(-2px); }
.stat-hero-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; background: var(--accent, #00C864); opacity: 0.6; }
.stat-label { font-family: var(--font-mono); font-size: 10px; color: rgba(255,255,255,0.35); letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 8px; }
.stat-value { font-family: var(--font-mono); font-size: 28px; font-weight: 600; color: #fff; margin-bottom: 4px; letter-spacing: -0.02em; }
.stat-sub { font-size: 11px; color: rgba(255,255,255,0.25); }
.stat-module-card { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.06); border-radius: 12px; overflow: hidden; transition: border-color 0.25s; }
.stat-module-card:hover { border-color: rgba(255,255,255,0.12); }
.stat-mod-header { display: flex; align-items: center; gap: 8px; padding: 10px 14px; border-bottom: 1px solid rgba(255,255,255,0.05); background: color-mix(in srgb, var(--accent) 8%, transparent); }
.stat-mod-title { font-size: 13px; font-weight: 600; color: #fff; flex: 1; }
.stat-mod-badge { font-family: var(--font-mono); font-size: 9px; font-weight: 700; padding: 2px 8px; border-radius: 100px; background: color-mix(in srgb, var(--accent) 20%, transparent); color: var(--accent); }
.stat-mod-body { padding: 10px 14px; display: flex; flex-direction: column; gap: 8px; }
.stat-mod-row { display: flex; justify-content: space-between; align-items: center; }
.stat-mod-lbl { font-size: 11px; color: rgba(255,255,255,0.3); }
.stat-mod-val { font-size: 13px; font-weight: 600; color: #e2e8f0; font-family: var(--font-mono); }
.stat-mod-val.highlight { color: var(--accent); }

/* ── LEADERBOARD ──────────────────────────────────────────── */
.lb-stat-card { background: rgba(245,158,11,0.06); border: 1px solid rgba(245,158,11,0.15); border-radius: 10px; padding: 14px; text-align: center; }
.lb-stat-val { font-family:var(--font-mono); font-size:18px; font-weight:700; color:#F59E0B; margin-bottom:4px; }
.lb-stat-lbl { font-size:10px; color:rgba(255,255,255,0.3); text-transform:uppercase; letter-spacing:0.06em; }
.lb-tab { padding: 6px 16px; border-radius: 8px; font-size: 12px; font-weight: 600; border: 1px solid rgba(255,255,255,0.08); background: transparent; color: rgba(255,255,255,0.4); cursor: pointer; transition: all 0.2s; }
.lb-tab.active { background: rgba(245,158,11,0.12); border-color: rgba(245,158,11,0.3); color: #F59E0B; }
.lb-entry { display: flex; align-items: center; gap: 12px; border-radius: 10px; padding: 12px 16px; border: 1px solid rgba(255,255,255,0.06); background: rgba(255,255,255,0.02); transition: border-color 0.2s; }
.lb-entry:hover { border-color: rgba(245,158,11,0.2); }
.lb-entry.top3 { background: rgba(245,158,11,0.06); border-color: rgba(245,158,11,0.2); }
.lb-rank { width:36px; height:36px; border-radius:8px; display:flex; align-items:center; justify-content:center; font-weight:700; font-size:13px; flex-shrink:0; }
.lb-name { flex:1; font-size:14px; font-weight:600; color:#fff; }
.lb-meta { font-size:11px; color:rgba(255,255,255,0.3); margin-top:2px; }
.lb-earned { font-weight:700; font-size:14px; font-family:var(--font-mono); }

/* ── TRENDING ─────────────────────────────────────────────── */
#trending-section { padding: 80px 48px; background: rgba(6,8,16,0.95); border-top: 1px solid rgba(255,255,255,0.06); position: relative; overflow: hidden; }
#trending-section::before { content: ''; position: absolute; top: 0; left: 50%; transform: translateX(-50%); width: 600px; height: 300px; background: radial-gradient(ellipse, rgba(0,200,100,0.06), transparent 70%); pointer-events: none; }
.trend-header { text-align: center; margin-bottom: 48px; }
.trend-eyebrow { font-family: var(--font-mono); font-size: 11px; color: rgba(0,200,100,0.7); letter-spacing: 0.12em; text-transform: uppercase; display: flex; align-items: center; justify-content: center; gap: 8px; margin-bottom: 14px; }
.trend-live-dot { width: 8px; height: 8px; border-radius: 50%; background: #00C864; box-shadow: 0 0 0 0 rgba(0,200,100,0.4); animation: trendPulse 2s infinite; }
@keyframes trendPulse { 0% { box-shadow: 0 0 0 0 rgba(0,200,100,0.4); } 70% { box-shadow: 0 0 0 8px rgba(0,200,100,0); } 100% { box-shadow: 0 0 0 0 rgba(0,200,100,0); } }
.trend-title { font-family: var(--font-display); font-size: clamp(28px, 4vw, 46px); font-weight: 700; line-height: 1.1; margin-bottom: 14px; }
.trend-sub { font-size: 15px; color: rgba(255,255,255,0.4); max-width: 520px; margin: 0 auto; line-height: 1.7; }
.trend-tabs { display: flex; gap: 6px; margin-bottom: 20px; justify-content: space-between; align-items: center; flex-wrap: wrap; }
.trend-tab { padding: 6px 16px; border-radius: 8px; font-family: var(--font-mono); font-size: 12px; font-weight: 600; border: 1px solid rgba(255,255,255,0.08); background: transparent; color: rgba(255,255,255,0.4); cursor: pointer; transition: all 0.2s; }
.trend-tab.active { background: rgba(0,200,100,0.12); border-color: rgba(0,200,100,0.3); color: #00C864; }
.trend-refresh { font-size: 11px; color: rgba(255,255,255,0.2); font-family: var(--font-mono); }
#trend-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-bottom: 24px; }
.trend-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); border-radius: 14px; padding: 16px; position: relative; overflow: hidden; transition: border-color 0.25s, transform 0.2s; cursor: pointer; text-decoration: none; display: block; }
.trend-card:hover { border-color: rgba(0,200,100,0.25); transform: translateY(-2px); }
.trend-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; opacity: 0; transition: opacity 0.25s; }
.trend-card:hover::before { opacity: 1; }
.trend-card.src-boost::before { background: #00C864; }
.trend-card.src-profile::before{ background: #00D4FF; }
.trend-card.src-trending::before{ background: #A78BFA; }
.trend-rank { position: absolute; top: 12px; right: 12px; font-family: var(--font-mono); font-size: 11px; font-weight: 700; color: rgba(255,255,255,0.2); }
.trend-tok-header { display: flex; align-items: center; gap: 10px; margin-bottom: 12px; }
.trend-tok-img { width: 36px; height: 36px; border-radius: 50%; background: rgba(255,255,255,0.08); object-fit: cover; flex-shrink: 0; }
.trend-tok-img-placeholder { width: 36px; height: 36px; border-radius: 50%; background: linear-gradient(135deg, #101624, #16213e); display: flex; align-items: center; justify-content: center; font-size: 14px; font-weight: 700; color: #00C864; flex-shrink: 0; }
.trend-tok-name { font-size: 15px; font-weight: 700; color: #fff; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; max-width: 120px; }
.trend-tok-badges { display: flex; gap: 4px; margin-top: 2px; }
.trend-badge { font-size: 9px; font-weight: 700; padding: 1px 6px; border-radius: 100px; letter-spacing: 0.04em; }
.badge-pump { background: rgba(153,69,255,0.2); color: #9945FF; }
.badge-boost{ background: rgba(0,200,100,0.15); color: #00C864; }
.badge-new { background: rgba(0,212,255,0.15); color: #00D4FF; }
.trend-score-bar { height: 3px; border-radius: 2px; background: rgba(255,255,255,0.06); margin-bottom: 12px; overflow: hidden; }
.trend-score-fill { height: 100%; border-radius: 2px; transition: width 0.8s ease; }
.trend-stats { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 10px; }
.trend-stat-label { font-size: 9px; color: rgba(255,255,255,0.3); text-transform: uppercase; letter-spacing: 0.06em; margin-bottom: 2px; }
.trend-stat-value { font-family: var(--font-mono); font-size: 13px; font-weight: 600; color: #fff; }
.trend-stat-value.green { color: #00C864; }
.trend-stat-value.red { color: #FF4D6A; }
.trend-signal { font-size: 10px; color: rgba(255,255,255,0.35); border-top: 1px solid rgba(255,255,255,0.05); padding-top: 8px; margin-top: 4px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.trend-card-cta { display: block; margin-top: 10px; padding: 8px 0; border-radius: 8px; background: rgba(0,200,100,0.1); border: 1px solid rgba(0,200,100,0.2); color: #00C864; font-size: 12px; font-weight: 600; text-align: center; text-decoration: none; transition: background 0.2s; }
.trend-card-cta:hover { background: rgba(0,200,100,0.2); }
.trend-alert-cta { background: linear-gradient(135deg, rgba(0,200,100,0.08) 0%, rgba(0,212,255,0.06) 100%); border: 1px solid rgba(0,200,100,0.2); border-radius: 16px; padding: 28px 32px; display: flex; align-items: center; justify-content: space-between; gap: 24px; flex-wrap: wrap; }
.trend-alert-left h3 { font-size: 18px; font-weight: 700; color: #fff; margin-bottom: 6px; }
.trend-alert-left p { font-size: 13px; color: rgba(255,255,255,0.4); line-height: 1.6; max-width: 480px; }
.trend-alert-btn { display: inline-flex; align-items: center; gap: 8px; padding: 12px 24px; border-radius: 10px; background: linear-gradient(135deg, #00C864, #00A851); color: #000; font-size: 14px; font-weight: 700; text-decoration: none; white-space: nowrap; transition: transform 0.2s, box-shadow 0.2s; flex-shrink: 0; }
.trend-alert-btn:hover { transform: scale(1.03); box-shadow: 0 8px 24px rgba(0,200,100,0.3); }
.trend-alert-price { font-size: 11px; color: rgba(255,255,255,0.35); text-align: center; margin-top: 8px; }
.trend-skeleton { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); border-radius: 14px; padding: 16px; animation: trendShimmer 1.5s infinite; }
@keyframes trendShimmer { 0%,100% { opacity: 0.4; } 50% { opacity: 0.7; } }
.skeleton-line { height: 12px; border-radius: 6px; background: rgba(255,255,255,0.06); margin-bottom: 8px; }
.trend-footer { text-align: center; margin-top: 20px; font-family: var(--font-mono); font-size: 11px; color: rgba(255,255,255,0.15); }

/* ── MOBILE ───────────────────────────────────────────────── */
@media (max-width: 900px) {
  nav { padding: 16px 24px; }
  .nav-links { display: none; }
  section { padding: 80px 24px; }
  #hero { padding: 100px 24px 60px; }
  .hero-inner { grid-template-columns: 1fr; gap: 60px; }
  .hero-phone-wrap { order: -1; }
  .pillars-grid { grid-template-columns: 1fr; }
  .features-grid { grid-template-columns: 1fr; }
  .feature-card { border-right: none; }
  .steps-grid { grid-template-columns: 1fr 1fr; }
  .chain-flow { grid-template-columns: 1fr 1fr; }
  .extras-grid { grid-template-columns: 1fr; }
  .ngn-inner { grid-template-columns: 1fr; }
  .pricing-grid { grid-template-columns: 1fr; }
  .proof-stats { grid-template-columns: 1fr 1fr; }
  .footer-inner { grid-template-columns: 1fr 1fr; gap: 40px; }
  .stream-grid { grid-template-columns: 1fr; }
  .screens-row { gap: 16px; }
  .phone-lg { transform: none; }
  #agent-stream { padding: 60px 24px; }
  #live-stats { padding: 60px 24px; }
  .stat-hero-card { padding: 14px; }
  .stat-value { font-size: 22px; }
  div[style*="grid-template-columns: repeat(4, 1fr)"] { grid-template-columns: repeat(2, 1fr) !important; }
  div[style*="grid-template-columns: repeat(3, 1fr)"] { grid-template-columns: 1fr !important; }
}
@media (max-width: 640px) { #lb-stats-grid { grid-template-columns:repeat(2,1fr); } }
@media (max-width: 960px) { #trend-grid { grid-template-columns: 1fr 1fr; } }
@media (max-width: 600px) { #trending-section { padding: 60px 24px; } #trend-grid { grid-template-columns: 1fr; } .trend-alert-cta { flex-direction: column; text-align: center; } .chain-flow { grid-template-columns: 1fr; } }
</style>
</head>
<body>
<!-- ── NAVIGATION ──────────────────────────────────────────── -->
<nav id="navbar">
  <a href="#" class="nav-logo">
    <img src="/logo.png" alt="ClickBot" class="nav-logo-img">
    <span class="nav-logo-text">Click<span>Bot</span></span>
  </a>
  <ul class="nav-links">
    <li><a href="#pillars">What We Do</a></li>
    <li><a href="#videos">Watch</a></li>
    <li><a href="#features">Features</a></li>
    <li><a href="#multichain">Multichain</a></li>
    <li><a href="#ngn">NGN Bridge</a></li>
    <li><a href="#pricing">Pricing</a></li>
    <li><a href="https://clickshift.io">ClickShift.io</a></li>
    <li><a href="https://t.me/clicksolbot" class="nav-cta">Start Banking Crypto →</a></li>
  </ul>
</nav>

<!-- ── HERO ────────────────────────────────────────────────── -->
<section id="hero">
  <div class="hero-grid-bg"></div>
  <div class="hero-orb-1"></div>
  <div class="hero-orb-2"></div>
  <div class="hero-inner">
    <div class="hero-content">
      <div class="hero-badge">Trade · Pay Bills · Earn · Bridge · Bank — All from Telegram</div>
      <h1 class="hero-headline">
        The <em>Web3 Siri</em><br>
        That Turns Your Onchain Wallet<br>
        Into a Local Bank
      </h1>
      <p class="hero-sub">
        Chat to trade any Solana token. Chat to pay your electricity bill. Chat to earn up to 14% yield on idle USDC. Chat to bridge crypto from 6 chains and send money to any Nigerian bank — no P2P, no exchange, no waiting. All inside Telegram. No app install.
      </p>
      <div class="hero-ctas">
        <a href="https://t.me/clicksolbot" class="btn-primary"><span class="icon">✈️</span> Open in Telegram</a>
        <a href="#pillars" class="btn-secondary">See what it does →</a>
      </div>
      <div class="hero-stats">
        <div class="hero-stat">
          <div class="hero-stat-num" id="hero-stat-users">—</div>
          <div class="hero-stat-label">Active Traders</div>
        </div>
        <div class="hero-stat">
          <div class="hero-stat-num" id="hero-stat-volume">—</div>
          <div class="hero-stat-label">Volume Processed</div>
        </div>
        <div class="hero-stat">
          <div class="hero-stat-num">$0</div>
          <div class="hero-stat-label">Marketing Spend</div>
        </div>
      </div>
    </div>
    <div class="hero-phone-wrap">
      <div class="float-chip green chip-1">🟢 BONK +47% — Trailing exit fired</div>
      <div class="float-chip cyan chip-2">🏦 ₦81,576 sent to GTBank · 3 mins</div>
      <div class="float-chip gold chip-3">💡 AEDC meter 45135609803 — Token credited</div>
      <div class="float-chip chip-4">🌱 +$0.82 yield earned today · 14% APY</div>
      <div class="phone-mockup">
        <div class="phone-notch"></div>
        <div class="phone-screen">
          <div class="phone-header">
            <span style="font-size:9px;color:var(--text-faint)">9:41</span>
            <span class="phone-header-title">ClickBot</span>
            <span style="font-size:9px;color:var(--green)">●</span>
          </div>
          <div class="phone-balance-card">
            <div class="phone-balance-label">Portfolio Value</div>
            <div class="phone-balance-amount">12.84 SOL</div>
            <div class="phone-balance-usd">≈ $1,926.00 USD · 🟢 +4.2% today</div>
          </div>
          <div class="phone-analysis">
            <div class="analysis-token">$PEPE analysis</div>
            <div class="analysis-row"><span>RSI (14)</span><span class="val">28 — Oversold</span></div>
            <div class="analysis-row"><span>Momentum</span><span class="val">71/100</span></div>
            <div class="analysis-row"><span>Holder Risk</span><span class="val" style="color:var(--green)">LOW</span></div>
            <div class="analysis-row"><span>Buy Pressure</span><span class="val">68% buys</span></div>
            <div class="analysis-verdict">🟢 BUY — HIGH CONFIDENCE · 86/100</div>
          </div>
          <div class="phone-menu-grid" style="margin-top:10px">
            <div class="phone-menu-btn"><div class="menu-icon">🛒</div><div class="menu-label">Trade Tokens</div></div>
            <div class="phone-menu-btn" style="border-color:rgba(0,200,100,0.25);background:rgba(0,200,100,0.05)"><div class="menu-icon">🎯</div><div class="menu-label">Sniper</div></div>
            <div class="phone-menu-btn"><div class="menu-icon">💳</div><div class="menu-label">Pay Bills</div></div>
            <div class="phone-menu-btn"><div class="menu-icon">🌱</div><div class="menu-label">Earn Yield</div></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ── TICKER ───────────────────────────────────────────────── -->
<div class="ticker-wrap">
  <div class="ticker-track" id="ticker">
    <div class="ticker-item"><span class="ticker-symbol">SOL/USDC</span><span class="ticker-price">$150.24</span><span class="ticker-change up">+2.4%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">BTC/USDC</span><span class="ticker-price">$67,441</span><span class="ticker-change up">+1.1%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">ETH/USDC</span><span class="ticker-price">$3,210</span><span class="ticker-change down">-0.8%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">BONK/SOL</span><span class="ticker-price">$0.0000241</span><span class="ticker-change up">+12.7%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">JUP/SOL</span><span class="ticker-price">$0.842</span><span class="ticker-change up">+5.3%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">WIF/USDC</span><span class="ticker-price">$2.14</span><span class="ticker-change down">-1.2%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">PYTH/SOL</span><span class="ticker-price">$0.431</span><span class="ticker-change up">+3.6%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">MEME/SOL</span><span class="ticker-price">$0.0312</span><span class="ticker-change up">+28.4%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">SOL/USDC</span><span class="ticker-price">$150.24</span><span class="ticker-change up">+2.4%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">BTC/USDC</span><span class="ticker-price">$67,441</span><span class="ticker-change up">+1.1%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">ETH/USDC</span><span class="ticker-price">$3,210</span><span class="ticker-change down">-0.8%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">BONK/SOL</span><span class="ticker-price">$0.0000241</span><span class="ticker-change up">+12.7%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">JUP/SOL</span><span class="ticker-price">$0.842</span><span class="ticker-change up">+5.3%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">WIF/USDC</span><span class="ticker-price">$2.14</span><span class="ticker-change down">-1.2%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">PYTH/SOL</span><span class="ticker-price">$0.431</span><span class="ticker-change up">+3.6%</span></div>
    <div class="ticker-item"><span class="ticker-symbol">MEME/SOL</span><span class="ticker-price">$0.0312</span><span class="ticker-change up">+28.4%</span></div>
  </div>
</div>

<!-- ── THREE PILLARS ───────────────────────────────────────── -->
<section id="pillars">
  <div class="section-inner">
    <div class="reveal" style="text-align:center;">
      <div class="section-label" style="justify-content:center"><span style="display:none">—</span>Three Things · One Chat</div>
      <h2 class="section-title">Everything ClickBot does,<br><em>at a glance</em></h2>
      <p class="section-body" style="margin:16px auto 0; text-align:center;">Whatever you came for — growing your money, spending it, or earning on it — it lives in one Telegram chat. Pick your path.</p>
    </div>
    <div class="pillars-grid">
      <a href="#features" class="pillar-card reveal reveal-delay-1" style="--pillar-color: var(--green)">
        <span class="pillar-icon">📈</span>
        <div class="pillar-name">Trading</div>
        <div class="pillar-tagline">Grow your money</div>
        <ul class="pillar-list">
          <li>AI token analysis — 6 live signals, one clear verdict</li>
          <li>Sniper for new launches, instant + limit modes</li>
          <li>Copy trading — mirror proven alpha wallets</li>
          <li>Trailing profit — auto-exits at the peak</li>
          <li>Perps up to 5x, MEV-protected via Jito</li>
        </ul>
        <span class="pillar-link">Explore trading →</span>
      </a>
      <a href="#features" class="pillar-card reveal reveal-delay-2" style="--pillar-color: var(--blue)">
        <span class="pillar-icon">💳</span>
        <div class="pillar-name">Payments</div>
        <div class="pillar-tagline">Spend it in real life</div>
        <ul class="pillar-list">
          <li>Pay electricity, airtime, data & cable with USDC</li>
          <li>Send to any Nigerian bank — just type it</li>
          <li>Cash out crypto → Naira in minutes, no P2P</li>
          <li>Natural language — "send 5000 to GTBank"</li>
          <li>Combined USDC + USDT settlement</li>
        </ul>
        <span class="pillar-link">Explore payments →</span>
      </a>
      <a href="#features" class="pillar-card reveal reveal-delay-3" style="--pillar-color: var(--gold)">
        <span class="pillar-icon">🌱</span>
        <div class="pillar-name">Staking to Earn</div>
        <div class="pillar-tagline">Put idle crypto to work</div>
        <ul class="pillar-list">
          <li>Earn up to 14% APY on USDC, USDT & SOL</li>
          <li>Flexible (5%) or lock 7 / 30 / 90 days</li>
          <li>Earnings accrue every hour, live dashboard</li>
          <li>Withdraw principal + yield when lock ends</li>
          <li>Accumulate $SHIFT points ahead of TGE</li>
        </ul>
        <span class="pillar-link">Explore earning →</span>
      </a>
    </div>
  </div>
</section>

<!-- ── VIDEO SHOWCASE ──────────────────────────────────────── -->
<section id="videos">
  <div class="section-inner">
    <div class="reveal" style="text-align:center;">
      <div class="section-label" style="justify-content:center"><span style="display:none">—</span>See it in action</div>
      <h2 class="section-title">Watch ClickBot <em>work</em></h2>
      <p class="section-body" style="margin:16px auto 0; text-align:center;">Real screens, real transactions — no mockups. Tap the speaker to hear the walkthrough.</p>
    </div>
    <div class="video-tabs">
      <button class="video-tab active" data-video="trading" onclick="switchVideo('trading')">📈 Trading</button>
      <button class="video-tab" data-video="payments" onclick="switchVideo('payments')">💳 Payments</button>
      <button class="video-tab" data-video="staking" onclick="switchVideo('staking')">🌱 Staking</button>
    </div>
    <div class="video-stage reveal">
      <div class="video-frame">
        <iframe id="video-player"
          src="https://www.youtube-nocookie.com/embed/ZB_M8SNOyFQ?autoplay=1&mute=1&loop=1&playlist=ZB_M8SNOyFQ&controls=1&modestbranding=1&rel=0&playsinline=1"
          title="ClickBot walkthrough"
          allow="autoplay; encrypted-media; picture-in-picture"
          allowfullscreen></iframe>
      </div>
      <div class="video-caption" id="video-caption">See how AI-scored trading works — from contract paste to trailing-profit exit.</div>
      <div style="text-align:center;">
        <span class="video-unmute-hint">🔊 Tap the speaker icon in the player to unmute</span>
      </div>
    </div>
  </div>
</section>
<!-- ── MULTICHAIN ──────────────────────────────────────────── -->
<section id="multichain">
  <div class="section-inner">
    <div class="reveal" style="text-align:center;">
      <div class="section-label" style="justify-content:center"><span style="display:none">—</span>6 Chains · One Wallet</div>
      <h2 class="section-title">Hold crypto <em>anywhere</em>.<br>Spend it in Nigeria.</h2>
      <p class="section-body" style="margin:16px auto 0; text-align:center;">Got ETH on Ethereum? USDT on BNB Chain? Stablecoins on Polygon? Bridge it into ClickBot and it becomes spendable — pay bills, withdraw to your bank, or trade on Solana. One address works across every chain we support.</p>
    </div>

    <div class="chain-badges">
      <div class="chain-badge"><span class="dot" style="background:#627EEA"></span>Ethereum</div>
      <div class="chain-badge"><span class="dot" style="background:#F0B90B"></span>BNB Chain</div>
      <div class="chain-badge"><span class="dot" style="background:#8247E5"></span>Polygon</div>
      <div class="chain-badge"><span class="dot" style="background:#28A0F0"></span>Arbitrum</div>
      <div class="chain-badge"><span class="dot" style="background:#00C864"></span>Robinhood Chain</div>
      <div class="chain-badge"><span class="dot" style="background:#14F195"></span>Solana (home)</div>
    </div>

    <div class="chain-flow">
      <div class="chain-step reveal reveal-delay-1">
        <div class="chain-step-num">01</div>
        <div class="chain-step-title">Pick your chain & asset</div>
        <p class="chain-step-desc">Choose which chain you're bridging from — Ethereum, BNB, Polygon, Arbitrum, or Robinhood — and whether it's a native token (ETH, BNB, MATIC) or a stablecoin (USDC / USDT).</p>
      </div>
      <div class="chain-step reveal reveal-delay-2">
        <div class="chain-step-num">02</div>
        <div class="chain-step-title">Send to your address</div>
        <p class="chain-step-desc">Your ClickBot multichain address works across all EVM chains. Send from your exchange or wallet — just select the matching network so funds arrive safely.</p>
      </div>
      <div class="chain-step reveal reveal-delay-3">
        <div class="chain-step-num">03</div>
        <div class="chain-step-title">Bridge to Solana USDC</div>
        <p class="chain-step-desc">Tap Bridge. ClickBot converts whatever you sent into spendable USDC on Solana — usually within minutes — handling gas and routing for you.</p>
      </div>
      <div class="chain-step reveal reveal-delay-4">
        <div class="chain-step-num">04</div>
        <div class="chain-step-title">Spend, withdraw, or trade</div>
        <p class="chain-step-desc">Once it lands on Solana it works like any ClickBot balance — pay a bill, withdraw Naira to your bank, or trade any token. That's the whole point.</p>
      </div>
    </div>

    <div class="chain-warning">
      <span class="chain-warning-icon">⚠️</span>
      <div class="chain-warning-text">
        <strong>Always select the right network.</strong> When sending from an exchange, make sure the network matches the chain you chose (e.g. ERC-20 for Ethereum, BEP-20 for BNB Chain). Sending on the wrong network can cause funds to be lost — ClickBot shows you exactly which network to pick before you send.
      </div>
    </div>
  </div>
</section>

<!-- ── EXTRAS: STATEMENT + GASLESS ─────────────────────────── -->
<section id="extras">
  <div class="section-inner">
    <div class="reveal" style="text-align:center;">
      <div class="section-label" style="justify-content:center"><span style="display:none">—</span>Built like a real bank</div>
      <h2 class="section-title">The details that <em>matter</em></h2>
      <p class="section-body" style="margin:16px auto 0; text-align:center;">The things that turn a trading bot into something you actually trust with your money.</p>
    </div>
    <div class="extras-grid">
      <div class="extra-card reveal reveal-delay-1">
        <span class="extra-icon">📄</span>
        <div class="extra-name">Account Statements</div>
        <p class="extra-desc">Download a full financial history — trading, bill payments, withdrawals, and yield — as a clean, bank-style PDF. Choose 7 days, 30 days, 90 days, or all time. Real records for real money, whenever you need them.</p>
        <div class="statement-preview">
          <div class="stmt-head">
            <span class="stmt-title">ClickBot Statement</span>
            <span class="stmt-period">01–30 Sept 2026</span>
          </div>
          <div class="stmt-row"><span class="desc">🌱 Yield earned · USDC</span><span class="amt pos">+$4.21</span></div>
          <div class="stmt-row"><span class="desc">💡 AEDC electricity</span><span class="amt neg">−₦2,000</span></div>
          <div class="stmt-row"><span class="desc">🏦 Withdrawal · GTBank</span><span class="amt neg">−₦81,576</span></div>
          <div class="stmt-row"><span class="desc">📈 BONK trade · exit</span><span class="amt pos">+0.0218 SOL</span></div>
        </div>
        <span class="extra-tag">PDF · 7d / 30d / 90d / all-time</span>
      </div>
      <div class="extra-card reveal reveal-delay-2">
        <span class="extra-icon">⛽</span>
        <div class="extra-name">Gasless Transactions</div>
        <p class="extra-desc">You never need to hold SOL just to move your own money. ClickBot's treasury sponsors network gas automatically — so even a wallet with zero SOL can trade, swap, pay bills, and withdraw. The single biggest barrier in crypto, removed.</p>
        <div style="margin-top:24px; display:flex; gap:12px; flex-wrap:wrap;">
          <div style="flex:1; min-width:120px; background:var(--bg); border:1px solid rgba(0,200,100,0.15); border-radius:10px; padding:14px; text-align:center;">
            <div style="font-size:22px;">🚫⛽</div>
            <div style="font-size:11px; color:var(--text-dim); margin-top:6px;">No gas token needed</div>
          </div>
          <div style="flex:1; min-width:120px; background:var(--bg); border:1px solid rgba(0,200,100,0.15); border-radius:10px; padding:14px; text-align:center;">
            <div style="font-size:22px;">⚡</div>
            <div style="font-size:11px; color:var(--text-dim); margin-top:6px;">Treasury-sponsored fees</div>
          </div>
        </div>
        <span class="extra-tag">Zero-SOL onboarding</span>
      </div>
    </div>
  </div>
</section>

<!-- ── TESTIMONIALS ────────────────────────────────────────── -->
<section id="testimonials">
  <div class="section-inner">
    <div class="reveal" style="text-align:center;">
      <div class="section-label" style="justify-content:center"><span style="display:none">—</span>What people say</div>
      <h2 class="section-title">Loved across <em>50+ countries</em></h2>
      <p class="section-body" style="margin:16px auto 0; text-align:center;">Real users, real features, real results — from traders to first-timers paying their light bill.</p>
    </div>
  </div>
  <div class="testi-viewport">
    <div class="testi-track" id="testi-track">
      <!-- Set A -->
      <div class="testi-card">
        <span class="testi-feature">Trading</span>
        <p class="testi-quote">"The trailing profit feature caught the top of a BONK run I'd have definitely sold too early. It exited at the peak while I was asleep. Genuinely changed how I trade."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#00C864">C</div><div><div class="testi-name">Chidi O.</div><div class="testi-loc">🇳🇬 Lagos, Nigeria</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Payments</span>
        <p class="testi-quote">"I paid my electricity bill by just typing it in the chat. Token came in seconds. I didn't believe crypto could feel this normal until I tried it."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#3B82F6">A</div><div><div class="testi-name">Amara N.</div><div class="testi-loc">🇳🇬 Abuja, Nigeria</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Bank Withdrawal</span>
        <p class="testi-quote">"Sold a token, hit withdraw, and the Naira was in my GTBank account before I finished making coffee. No P2P stress. This is the future."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#F59E0B">K</div><div><div class="testi-name">Kwame A.</div><div class="testi-loc">🇬🇭 Accra, Ghana</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Staking</span>
        <p class="testi-quote">"My USDC used to just sit there. Now it earns 14% while I wait for setups. The hourly earnings dashboard is oddly satisfying to check."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#A78BFA">S</div><div><div class="testi-name">Sipho M.</div><div class="testi-loc">🇿🇦 Johannesburg, SA</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Multichain Bridge</span>
        <p class="testi-quote">"I had USDT stuck on BNB Chain with no easy way to spend it here. Bridged it to ClickBot, withdrew to my bank same day. Solved a real problem."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#00D4FF">D</div><div><div class="testi-name">David M.</div><div class="testi-loc">🇰🇪 Nairobi, Kenya</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">AI Analysis</span>
        <p class="testi-quote">"The risk score saved me from a rug. It flagged holder concentration I completely missed. I check every token through ClickBot now before buying."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#00C864">R</div><div><div class="testi-name">Ravi P.</div><div class="testi-loc">🇮🇳 Mumbai, India</div></div></div>
      </div>
      <!-- Set A duplicated for seamless loop -->
      <div class="testi-card">
        <span class="testi-feature">Trading</span>
        <p class="testi-quote">"The trailing profit feature caught the top of a BONK run I'd have definitely sold too early. It exited at the peak while I was asleep. Genuinely changed how I trade."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#00C864">C</div><div><div class="testi-name">Chidi O.</div><div class="testi-loc">🇳🇬 Lagos, Nigeria</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Payments</span>
        <p class="testi-quote">"I paid my electricity bill by just typing it in the chat. Token came in seconds. I didn't believe crypto could feel this normal until I tried it."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#3B82F6">A</div><div><div class="testi-name">Amara N.</div><div class="testi-loc">🇳🇬 Abuja, Nigeria</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Bank Withdrawal</span>
        <p class="testi-quote">"Sold a token, hit withdraw, and the Naira was in my GTBank account before I finished making coffee. No P2P stress. This is the future."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#F59E0B">K</div><div><div class="testi-name">Kwame A.</div><div class="testi-loc">🇬🇭 Accra, Ghana</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Staking</span>
        <p class="testi-quote">"My USDC used to just sit there. Now it earns 14% while I wait for setups. The hourly earnings dashboard is oddly satisfying to check."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#A78BFA">S</div><div><div class="testi-name">Sipho M.</div><div class="testi-loc">🇿🇦 Johannesburg, SA</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">Multichain Bridge</span>
        <p class="testi-quote">"I had USDT stuck on BNB Chain with no easy way to spend it here. Bridged it to ClickBot, withdrew to my bank same day. Solved a real problem."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#00D4FF">D</div><div><div class="testi-name">David M.</div><div class="testi-loc">🇰🇪 Nairobi, Kenya</div></div></div>
      </div>
      <div class="testi-card">
        <span class="testi-feature">AI Analysis</span>
        <p class="testi-quote">"The risk score saved me from a rug. It flagged holder concentration I completely missed. I check every token through ClickBot now before buying."</p>
        <div class="testi-person"><div class="testi-avatar" style="background:#00C864">R</div><div><div class="testi-name">Ravi P.</div><div class="testi-loc">🇮🇳 Mumbai, India</div></div></div>
      </div>
    </div>
  </div>
</section>
<!-- ── TRENDING TOKENS ─────────────────────────────────────── -->
<section id="trending-section">
  <div style="max-width:1200px;margin:0 auto;">
    <div class="trend-header">
      <div class="trend-eyebrow"><span class="trend-live-dot"></span>Pre-Pump Intelligence · Updated every 4 minutes</div>
      <h2 class="trend-title">Spot Tokens <em style="color:#00C864;font-style:italic">Before</em> They Pump</h2>
      <p class="trend-sub">Phantom shows you what already pumped. ClickBot shows you what's about to. Our algorithm catches tokens at $50K–$600K MC — before they show up on anyone's trending list.</p>
    </div>
    <div class="trend-tabs">
      <div style="display:flex;gap:6px;">
        <button class="trend-tab active" onclick="setTrendFilter('boost')">⚡ Boost Signals</button>
        <button class="trend-tab" onclick="setTrendFilter('all')">🔥 All Picks</button>
        <button class="trend-tab" onclick="setTrendFilter('new')">🆕 Fresh Launches</button>
      </div>
      <span class="trend-refresh" id="trend-refresh-label">Loading...</span>
    </div>
    <div id="trend-grid">
      <div class="trend-skeleton"><div class="skeleton-line" style="width:60%"></div><div class="skeleton-line" style="width:40%"></div><div class="skeleton-line" style="width:80%"></div></div>
      <div class="trend-skeleton"><div class="skeleton-line" style="width:50%"></div><div class="skeleton-line" style="width:70%"></div><div class="skeleton-line" style="width:45%"></div></div>
      <div class="trend-skeleton"><div class="skeleton-line" style="width:65%"></div><div class="skeleton-line" style="width:35%"></div><div class="skeleton-line" style="width:75%"></div></div>
    </div>
    <div class="trend-alert-cta">
      <div class="trend-alert-left">
        <h3>🔔 Get Notified Before They Pump</h3>
        <p>Our algorithm spots the signal first. Subscribe to ClickBot Alpha Alerts and get a Telegram notification the moment a token crosses our threshold — before it hits 50% gain. Never be late again.</p>
        <div style="display:flex;gap:16px;margin-top:12px;font-size:12px;color:rgba(255,255,255,0.3);">
          <span>✅ Instant Telegram notification</span>
          <span>✅ Contract address + score + entry signal</span>
          <span>✅ 30 days access</span>
        </div>
      </div>
      <div style="text-align:center;flex-shrink:0;">
        <a href="https://t.me/clicksolbot?start=alerts" target="_blank" class="trend-alert-btn">🔔 Subscribe to Alerts</a>
        <div class="trend-alert-price">$25 USDC / month · Cancel anytime</div>
      </div>
    </div>
    <div class="trend-footer">Data refreshes every 4 minutes · Powered by ClickBot on Solana mainnet · <a href="https://t.me/clicksolbot" style="color:rgba(0,200,100,0.6)">t.me/clicksolbot</a></div>
  </div>
</section>

<!-- ── LIVE STATS ─────────────────────────────────────────────── -->
<section id="live-stats" style="padding: 80px 48px; background: rgba(10,15,26,0.8); border-top: 1px solid rgba(255,255,255,0.06);">
  <div style="max-width: 1200px; margin: 0 auto;">
    <div style="text-align: center; margin-bottom: 56px;">
      <div style="display: inline-flex; align-items: center; gap: 8px; margin-bottom: 16px;">
        <span class="stat-pulse-dot"></span>
        <span style="font-family: var(--font-mono); font-size: 11px; color: #00C864; letter-spacing: 0.1em; text-transform: uppercase;">Live Platform Metrics</span>
      </div>
      <h2 style="font-family: var(--font-display); font-size: clamp(28px,4vw,48px); font-weight: 700; line-height: 1.1; letter-spacing: -0.02em; margin-bottom: 16px;">
        Built in the open.<br><em style="font-style: italic; color: #00C864;">Proven by numbers.</em>
      </h2>
      <p style="font-size: 15px; color: rgba(255,255,255,0.4); max-width: 480px; margin: 0 auto; line-height: 1.7;">Real volume. Real traders. Real exits. Every number is pulled live from ClickBot's on-chain activity.</p>
    </div>
    <div style="display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-bottom: 20px;">
      <div class="stat-hero-card" data-stat="users" data-accent="#00C864"><div class="stat-label">Total Traders</div><div class="stat-value" id="stat-users">—</div><div class="stat-sub" id="stat-users-sub">Loading…</div></div>
      <div class="stat-hero-card" data-stat="active" data-accent="#00D4FF"><div class="stat-label">Active (7 days)</div><div class="stat-value" id="stat-active">—</div><div class="stat-sub" id="stat-active-sub">&nbsp;</div></div>
      <div class="stat-hero-card" data-stat="volume" data-accent="#A78BFA"><div class="stat-label">Volume Facilitated</div><div class="stat-value" id="stat-volume">—</div><div class="stat-sub">All time · all modules</div></div>
      <div class="stat-hero-card" data-stat="txs" data-accent="#F59E0B"><div class="stat-label">Transactions</div><div class="stat-value" id="stat-txs">—</div><div class="stat-sub">Spot · Fiat · Utility · Yield · Perps</div></div>
    </div>
    <div id="ngn-strip" style="border-radius: 12px; padding: 16px 20px; border: 1px solid rgba(0,200,100,0.2); background: rgba(0,200,100,0.04); display: flex; align-items: center; justify-content: space-between; margin-bottom: 20px; flex-wrap: wrap; gap: 12px;">
      <div style="display: flex; align-items: center; gap: 12px;">
        <span style="font-size: 20px;">🏦</span>
        <div>
          <div style="font-size: 14px; font-weight: 600; color: #fff;"><span id="stat-ngn">₦—</span> moved through the NGN Bridge</div>
          <div style="font-size: 12px; color: rgba(255,255,255,0.3); margin-top: 2px;"><span id="stat-fiat-txs">—</span> fiat transactions · <span id="stat-success-rate">—</span> success rate</div>
        </div>
      </div>
      <div style="display: flex; align-items: center; gap: 8px;"><span class="stat-pulse-dot" style="--dot-color: #4ade80;"></span><span style="font-size: 12px; color: #4ade80; font-weight: 600;">Nigeria → Bank in minutes</span></div>
    </div>
    <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-bottom: 20px;">
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #4ade80;"><span style="font-size: 14px;">📊</span><span class="stat-mod-title">Spot Trading</span><span class="stat-mod-badge" style="--accent: #4ade80;" id="mod-spot-badge">—</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Total trades</span><span class="stat-mod-val highlight" style="--accent: #4ade80;" id="mod-trades">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Volume all-time</span><span class="stat-mod-val" id="mod-volume">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Unique traders</span><span class="stat-mod-val" id="mod-traders">—</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #F59E0B;"><span style="font-size: 14px;">🎯</span><span class="stat-mod-title">Sniper</span><span class="stat-mod-badge" style="--accent: #F59E0B;" id="mod-sniper-badge">—</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Total snipes</span><span class="stat-mod-val highlight" style="--accent: #F59E0B;" id="mod-snipes">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">This week</span><span class="stat-mod-val" id="mod-snipes-7d">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Execution</span><span class="stat-mod-val">Jito · &lt;100ms</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #A78BFA;"><span style="font-size: 14px;">🔄</span><span class="stat-mod-title">Copy Trading</span><span class="stat-mod-badge" style="--accent: #A78BFA;" id="mod-copy-badge">—</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Trades copied</span><span class="stat-mod-val highlight" style="--accent: #A78BFA;" id="mod-copied">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Success rate</span><span class="stat-mod-val" id="mod-copy-rate">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Active sessions</span><span class="stat-mod-val" id="mod-copy-sessions">—</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #38bdf8;"><span style="font-size: 14px;">📈</span><span class="stat-mod-title">Perps (Drift)</span><span class="stat-mod-badge" style="--accent: #38bdf8;" id="mod-perps-badge">—</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Total positions</span><span class="stat-mod-val highlight" style="--accent: #38bdf8;" id="mod-positions">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Open now</span><span class="stat-mod-val" id="mod-open">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Win rate</span><span class="stat-mod-val" id="mod-winrate">—</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #22d3ee;"><span style="font-size: 14px;">👥</span><span class="stat-mod-title">Community</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Total wallets</span><span class="stat-mod-val highlight" style="--accent: #22d3ee;" id="mod-wallets">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">KYC verified</span><span class="stat-mod-val" id="mod-kyc">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Joined last 30d</span><span class="stat-mod-val" id="mod-new30">—</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #f472b6;"><span style="font-size: 14px;">🎁</span><span class="stat-mod-title">Referrals</span><span class="stat-mod-badge" style="--accent: #f472b6;">20% forever</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Users referred</span><span class="stat-mod-val highlight" style="--accent: #f472b6;" id="mod-referred">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Active referrers</span><span class="stat-mod-val" id="mod-referrers">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Commission</span><span class="stat-mod-val">Instant · No cap</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #34d399;"><span style="font-size: 14px;">💡</span><span class="stat-mod-title">Utility Bills</span><span class="stat-mod-badge" style="--accent: #34d399;" id="mod-util-badge">—</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Total payments</span><span class="stat-mod-val highlight" style="--accent: #34d399;" id="mod-util-total">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">NGN volume</span><span class="stat-mod-val" id="mod-util-ngn">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Success rate</span><span class="stat-mod-val" id="mod-util-rate">—</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #60a5fa;"><span style="font-size: 14px;">🏦</span><span class="stat-mod-title">Bank Transfers</span><span class="stat-mod-badge" style="--accent: #60a5fa;" id="mod-bills-badge">—</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Transactions</span><span class="stat-mod-val highlight" style="--accent: #60a5fa;" id="mod-bills-total">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">NGN sent</span><span class="stat-mod-val" id="mod-bills-ngn">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Banks reached</span><span class="stat-mod-val" id="mod-bills-banks">—</span></div></div>
      </div>
      <div class="stat-module-card">
        <div class="stat-mod-header" style="--accent: #f472b6;"><span style="font-size: 14px;">🌱</span><span class="stat-mod-title">Yield Engine</span><span class="stat-mod-badge" style="--accent: #f472b6;" id="mod-yield-badge">—</span></div>
        <div class="stat-mod-body"><div class="stat-mod-row"><span class="stat-mod-lbl">Live pool</span><span class="stat-mod-val highlight" style="--accent: #f472b6;" id="mod-yield-pool">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Active stakers</span><span class="stat-mod-val" id="mod-yield-stakers">—</span></div><div class="stat-mod-row"><span class="stat-mod-lbl">Max APY</span><span class="stat-mod-val" style="color: #f472b6;">14% APY</span></div></div>
      </div>
    </div>
    <p style="text-align: center; font-family: var(--font-mono); font-size: 11px; color: rgba(255,255,255,0.15); margin-top: 12px;">Stats refresh every 60s · Live on Solana mainnet<span id="stats-updated"></span></p>
  </div>
</section>

<!-- ── AGENT STREAM ─────────────────────────────────────────── -->
<section id="agent-stream">
  <div class="stream-bg"></div>
  <div class="section-inner">
    <div class="stream-grid">
      <div>
        <div class="section-label">AI Engine</div>
        <h2 class="section-title">Your agents<br>never <em>sleep</em></h2>
        <p class="section-body" style="margin-bottom:32px">While you live your life, ClickBot is trading, monitoring your positions, paying your electricity bill, and growing your USDC in yield — all from one chat. The only financial assistant that never sleeps and never misses a move.</p>
        <a href="https://t.me/clicksolbot" class="btn-primary" style="display:inline-flex"><span>Start Banking Crypto Free</span></a>
      </div>
      <div class="stream-terminal">
        <div class="terminal-bar"><div class="terminal-dot r"></div><div class="terminal-dot y"></div><div class="terminal-dot g"></div><span class="terminal-title">clickbot — agent stream — live</span></div>
        <div class="terminal-body" id="stream-output"></div>
      </div>
    </div>
  </div>
</section>
<!-- ── FEATURES ─────────────────────────────────────────────── -->
<section id="features">
  <div class="section-inner">
    <div class="reveal">
      <div class="section-label">What's inside</div>
      <h2 class="section-title">Trade. Pay. Earn. Bridge. Bank.<br>Everything — <em>in one chat.</em></h2>
      <p class="section-body" style="margin-bottom:32px">ClickBot is the first Telegram bot that connects your crypto wallet to your everyday Nigerian financial life — trading intelligence, utility payments, yield, multichain bridging, and instant NGN cash-out, all without switching apps.</p>
    </div>
    <div class="features-grid">
      <div class="feature-card reveal reveal-delay-1"><span class="feature-icon">🧠</span><div class="feature-name">AI Token Analysis</div><p class="feature-desc">Real 14-period RSI from live candles, buy/sell pressure, volume surge detection, holder concentration risk, and liquidity depth — six signals producing one scored recommendation with full reasoning shown.</p><span class="feature-tag">6-signal engine</span></div>
      <div class="feature-card reveal reveal-delay-2"><span class="feature-icon">⚡</span><div class="feature-name">MEV-Protected Trading</div><p class="feature-desc">Trades route through Jito bundle infrastructure, bypassing the public Solana mempool. No sandwich attacks. No frontrunning. Priority confirmation. The difference between getting filled and getting wrecked.</p><span class="feature-tag">Jito bundles</span></div>
      <div class="feature-card reveal reveal-delay-3"><span class="feature-icon">🎯</span><div class="feature-name">Launch Sniper</div><p class="feature-desc">Instant and limit-order sniping on new launches. TP/SL/Trailing arms fire automatically post-execution. New mints are millisecond races — our Jito routing lands in the same block as pool creation.</p><span class="feature-tag">Instant + Limit modes</span></div>
      <div class="feature-card reveal reveal-delay-1"><span class="feature-icon">🔄</span><div class="feature-name">Copy Trading</div><p class="feature-desc">Mirror on-chain activity of curated alpha wallets in real time. Set your copy amount once — every buy and exit fires automatically into your wallet with full position management buttons.</p><span class="feature-tag">Real-time mirroring</span></div>
      <div class="feature-card reveal reveal-delay-2"><span class="feature-icon">📈</span><div class="feature-name">Trailing Profit Engine</div><p class="feature-desc">Follows the pump to the peak. When price drops your configured percentage from the top, ClickBot exits automatically. Set it after every buy and sleep — the engine never stops watching.</p><span class="feature-tag">24/7 monitoring</span></div>
      <div class="feature-card reveal reveal-delay-3"><span class="feature-icon">⚡</span><div class="feature-name">Multichain Bridge</div><p class="feature-desc">Bring crypto in from Ethereum, BNB Chain, Polygon, Arbitrum, or Robinhood — native tokens or stablecoins — and turn it into spendable USDC on Solana. Six chains, one wallet, minutes to settle.</p><span class="feature-tag">6 chains → Solana</span></div>
      <div class="feature-card reveal reveal-delay-1"><span class="feature-icon">🏦</span><div class="feature-name">Fiat Bridge — Nigeria</div><p class="feature-desc">NGN → USDC via virtual bank account with no P2P. USDC → any Nigerian bank in minutes. One platform takes you from a meme coin launch all the way to Naira in your account.</p><span class="feature-tag">NGN ↔ USDC · No P2P</span></div>
      <div class="feature-card reveal reveal-delay-2"><span class="feature-icon">💳</span><div class="feature-name">Pay Bills with Crypto</div><p class="feature-desc">Send Naira to any Nigerian bank account directly from your USDC wallet. Just type naturally — "send 5000 naira to GTBank 0123456789" — ClickBot reads the intent, verifies the account name, and executes instantly. Send screenshots of payment details and ClickBot reads them too.</p><span class="feature-tag">Natural language payments</span></div>
      <div class="feature-card reveal reveal-delay-3"><span class="feature-icon">🧾</span><div class="feature-name">Utility Bill Payments</div><p class="feature-desc">Pay electricity (EKEDC, IKEDC, AEDC, PHED, KEDCO and more), buy airtime and data for any network, renew DStv, GOtv, and Startimes — all with USDC. Electricity tokens vend instantly to your meter. Nigeria's entire bill payment stack in one bot.</p><span class="feature-tag">Electricity · Airtime · Cable</span></div>
    </div>
  </div>
</section>

<!-- ── REFERRAL LEADERBOARD ────────────────────────────────── -->
<section id="leaderboard" style="padding: 80px 48px; background: rgba(6,8,16,0.95);">
  <div style="max-width: 760px; margin: 0 auto;">
    <div style="text-align:center; margin-bottom:48px;">
      <div style="font-family:var(--font-mono); font-size:11px; color:rgba(245,158,11,0.7); letter-spacing:0.1em; text-transform:uppercase; margin-bottom:12px;">Referral Program</div>
      <h2 style="font-family:var(--font-display); font-size:clamp(28px,4vw,44px); font-weight:700; line-height:1.1; margin-bottom:12px;">The <em style="font-style:italic; color:#F59E0B;">Champions Hall</em></h2>
      <p style="font-size:14px; color:rgba(255,255,255,0.4); max-width:440px; margin:0 auto; line-height:1.7;">Share your link. Earn 20% of every fee your referrals generate — instantly, forever, no cap.</p>
    </div>
    <div style="display:grid; grid-template-columns:repeat(4,1fr); gap:10px; margin-bottom:24px;" id="lb-stats-grid">
      <div class="lb-stat-card"><div class="lb-stat-val" id="lb-total-paid">—</div><div class="lb-stat-lbl">Total Paid Out</div></div>
      <div class="lb-stat-card"><div class="lb-stat-val" id="lb-referrers">—</div><div class="lb-stat-lbl">Referrers</div></div>
      <div class="lb-stat-card"><div class="lb-stat-val" id="lb-referred">—</div><div class="lb-stat-lbl">Users Referred</div></div>
      <div class="lb-stat-card"><div class="lb-stat-val" id="lb-7d">—</div><div class="lb-stat-lbl">Paid This Week</div></div>
    </div>
    <div style="display:flex; gap:6px; margin-bottom:16px;">
      <button class="lb-tab active" onclick="loadLeaderboard('all')" id="tab-all">All Time</button>
      <button class="lb-tab" onclick="loadLeaderboard('30d')" id="tab-30d">30 Days</button>
      <button class="lb-tab" onclick="loadLeaderboard('7d')" id="tab-7d">7 Days</button>
    </div>
    <div id="lb-entries" style="display:flex; flex-direction:column; gap:8px;"></div>
    <div style="text-align:center; margin-top:32px;">
      <a href="https://t.me/clicksolbot" target="_blank" style="display:inline-flex; align-items:center; gap:8px; padding:14px 28px; background:linear-gradient(135deg,#F59E0B,#D97706); color:#000; font-weight:700; border-radius:10px; font-size:14px; text-decoration:none; transition:transform 0.2s;" onmouseover="this.style.transform='scale(1.04)'" onmouseout="this.style.transform='scale(1)'">🏆 Claim Your Spot on the Leaderboard</a>
    </div>
  </div>
</section>

<!-- ── TRADER VOLUME LEADERBOARD ─────────────────────────────── -->
<section id="trader-leaderboard" style="padding:80px 48px;background:rgba(6,8,16,0.95);border-top:1px solid rgba(255,255,255,0.06);">
  <div style="max-width:760px;margin:0 auto;">
    <div style="text-align:center;margin-bottom:48px;">
      <div style="font-family:var(--font-mono);font-size:11px;color:rgba(0,200,100,0.6);letter-spacing:0.1em;text-transform:uppercase;margin-bottom:12px;">Trader Rankings · $SHIFT Points</div>
      <h2 style="font-family:var(--font-display);font-size:clamp(28px,4vw,44px);font-weight:700;line-height:1.1;margin-bottom:12px;">The <em style="font-style:italic;color:#00C864;">Top Traders</em></h2>
      <p style="font-size:14px;color:rgba(255,255,255,0.4);max-width:440px;margin:0 auto;line-height:1.7;">Trade more, earn $SHIFT. Early adopters get 3× multiplier — limited window before TGE.</p>
    </div>
    <div style="display:flex;gap:6px;margin-bottom:16px;">
      <button class="trader-tab lb-tab active" data-period="quarter" onclick="loadTraderLeaderboard('quarter')">This Quarter</button>
      <button class="trader-tab lb-tab" data-period="30d" onclick="loadTraderLeaderboard('30d')">30 Days</button>
      <button class="trader-tab lb-tab" data-period="7d" onclick="loadTraderLeaderboard('7d')">7 Days</button>
    </div>
    <div id="trader-lb-entries"></div>
    <div style="text-align:center;margin-top:32px;">
      <a href="https://t.me/clicksolbot" target="_blank" style="display:inline-flex;align-items:center;gap:8px;padding:14px 28px;background:linear-gradient(135deg,#00C864,#00A851);color:#000;font-weight:700;border-radius:10px;font-size:14px;text-decoration:none;" onmouseover="this.style.transform='scale(1.04)'" onmouseout="this.style.transform='scale(1)'">🏆 Join & Earn $SHIFT Tokens</a>
      <div style="margin-top:10px;font-size:12px;color:rgba(255,255,255,0.25);">TGE: Q1 2027 · Early adopters get 3× multiplier</div>
    </div>
  </div>
</section>

<!-- ── SCREENS SHOWCASE ──────────────────────────────────────── -->
<section id="screens">
  <div class="section-inner">
    <div class="screens-header reveal">
      <div class="section-label">In your hands</div>
      <h2 class="section-title">Every screen, <em>crafted</em></h2>
      <p class="section-body" style="margin: 0 auto; text-align: center; margin-top: 16px;">Choose between making money, moving money, or inviting friends with your referral link for 20% passive income for life.</p>
    </div>
    <div class="screens-row">
      <div class="screen-item reveal reveal-delay-1">
        <div class="screen-phone phone-md" style="animation: phoneFloat 7s ease-in-out infinite;">
          <div class="screen-notch"></div>
          <div class="screen-body">
            <div class="s-header"><div class="s-welcome">Good morning, Emmanuel 👋</div><div class="s-title">ClickBot</div></div>
            <div class="s-wallet-strip"><div><div class="s-sol">12.84 SOL</div><div class="s-usd">≈ $1,926 USD</div></div><div class="s-wallet-icon">💼</div></div>
            <div class="s-btn active"><span class="s-btn-icon">💰</span><div><div class="s-btn-text">Make Money</div><div class="s-btn-sub">Trade, Snipe, Copy</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">🏦</span><div><div class="s-btn-text">Move Money</div><div class="s-btn-sub">Withdraw, Transfer, Bridge</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">📊</span><div><div class="s-btn-text">Portfolio</div><div class="s-btn-sub">P&L · Holdings</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">🌱</span><div><div class="s-btn-text">Earn Yield</div><div class="s-btn-sub">5–14% APY on USDC/SOL</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">🎁</span><div><div class="s-btn-text">Refer & Earn</div><div class="s-btn-sub">20% commission forever</div></div><span class="s-btn-arr">›</span></div>
          </div>
        </div>
        <div class="screen-label">Main Menu</div>
      </div>
      <div class="screen-item reveal">
        <div class="screen-phone phone-lg" style="animation: phoneFloat 6s ease-in-out infinite 0.5s;">
          <div class="screen-notch"></div>
          <div class="screen-body">
            <div class="s-header" style="margin-bottom:8px"><div class="s-title">Make Money</div></div>
            <div class="s-section-title">💰 Choose your weapon</div>
            <div class="s-btn active"><span class="s-btn-icon">🛒</span><div><div class="s-btn-text">Trade Tokens</div><div class="s-btn-sub">Buy & sell any Solana token</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">🎯</span><div><div class="s-btn-text">Sniper</div><div class="s-btn-sub">Catch launches early</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">🔄</span><div><div class="s-btn-text">Copy Trading</div><div class="s-btn-sub">Mirror alpha wallets</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">📈</span><div><div class="s-btn-text">Trade Perps</div><div class="s-btn-sub">5x leverage · Long & Short</div></div><span class="s-btn-arr">›</span></div>
            <div class="s-btn"><span class="s-btn-icon">🎁</span><div><div class="s-btn-text">Refer & Earn</div><div class="s-btn-sub">20% commission forever</div></div><span class="s-btn-arr">›</span></div>
          </div>
        </div>
        <div class="screen-label">Make Money Menu</div>
      </div>
      <div class="screen-item reveal reveal-delay-2">
        <div class="screen-phone phone-md" style="animation: phoneFloat 8s ease-in-out infinite 1s;">
          <div class="screen-notch"></div>
          <div class="screen-body">
            <div class="s-token-header"><div><div class="s-token-name">$BONK</div><div style="font-size:7px;color:var(--text-faint)">Bonk Token</div></div><div style="text-align:right"><div class="s-token-price">$0.00002410</div><div class="s-token-change up">+47.2% 24h</div></div></div>
            <div class="s-metric-row"><span class="s-metric-key">RSI (14)</span><span class="s-metric-val" style="color:var(--green)">28 — Oversold</span></div>
            <div class="s-metric-row"><span class="s-metric-key">Momentum</span><span class="s-metric-val">71/100</span></div>
            <div class="s-metric-row"><span class="s-metric-key">Buy Pressure</span><span class="s-metric-val">68% buys</span></div>
            <div class="s-metric-row"><span class="s-metric-key">Liquidity</span><span class="s-metric-val" style="color:var(--green)">$2.4M Deep</span></div>
            <div class="s-metric-row"><span class="s-metric-key">Holder Risk</span><span class="s-metric-val" style="color:var(--green)">LOW</span></div>
            <div class="s-metric-row"><span class="s-metric-key">Volume 1h</span><span class="s-metric-val">$140K ↑ Surge</span></div>
            <div class="s-verdict buy"><div class="s-verdict-label">🟢 BUY RECOMMENDATION</div><div class="s-verdict-conf">Score 86/100 · HIGH confidence</div></div>
          </div>
        </div>
        <div class="screen-label">AI Analysis</div>
      </div>
      <div class="screen-item reveal reveal-delay-3">
        <div class="screen-phone phone-md" style="animation: phoneFloat 9s ease-in-out infinite 1.5s;">
          <div class="screen-notch"></div>
          <div class="screen-body">
            <div class="s-header" style="margin-bottom:10px"><div class="s-title">Withdraw to Bank</div></div>
            <div class="s-success-icon">🏦</div>
            <div class="s-bank-card"><div class="s-bank-name">GTBank · 0123456789</div><div class="s-bank-acct">Emmanuel Adeyemi ✅</div></div>
            <div class="s-rate-row"><span class="s-rate-key">Amount</span><span class="s-rate-val">50 USDC</span></div>
            <div class="s-rate-row"><span class="s-rate-key">Live Rate</span><span class="s-rate-val" style="color:var(--cyan)">₦1,648/$1</span></div>
            <div class="s-rate-row"><span class="s-rate-key">Fee (1%)</span><span class="s-rate-val">0.50 USDC</span></div>
            <div class="s-rate-row"><span class="s-rate-key">You receive</span><span class="s-rate-val" style="color:var(--green);font-size:11px">₦81,576</span></div>
            <div class="s-confirm-btn">✅ CONFIRM & WITHDRAW</div>
          </div>
        </div>
        <div class="screen-label">Bank Withdrawal</div>
      </div>
      <div class="screen-item reveal reveal-delay-1">
        <div class="screen-phone phone-md" style="animation: phoneFloat 8s ease-in-out infinite 2s;">
          <div class="screen-notch"></div>
          <div class="screen-body">
            <div class="s-header" style="margin-bottom:10px"><div class="s-title">Pay Bills</div></div>
            <div style="background:rgba(0,200,100,0.06);border:1px solid rgba(0,200,100,0.15);border-radius:8px;padding:8px;margin-bottom:8px;font-size:7.5px;color:rgba(255,255,255,0.5);font-style:italic;">💬 "send 5000 naira to Opay 7034930975"</div>
            <div style="font-size:7px;color:rgba(0,200,100,0.7);margin-bottom:6px;">✅ Account verified: Emmanuel Ohanwe</div>
            <div class="s-bank-card"><div class="s-bank-name">OPay · 7034930975</div><div class="s-bank-acct">Emmanuel Ohanwe ✅</div></div>
            <div class="s-rate-row"><span class="s-rate-key">Amount</span><span class="s-rate-val" style="color:var(--green)">₦5,000</span></div>
            <div class="s-rate-row"><span class="s-rate-key">Rate</span><span class="s-rate-val" style="color:var(--cyan)">$1 = ₦1,648</span></div>
            <div class="s-rate-row"><span class="s-rate-key">Debit</span><span class="s-rate-val">3.0340 USDC</span></div>
            <div class="s-rate-row"><span class="s-rate-key">Fee (2%)</span><span class="s-rate-val">0.0607 USDC</span></div>
            <div class="s-confirm-btn" style="background:linear-gradient(135deg,#00C864,#00A851);">✅ CONFIRM & PAY</div>
          </div>
        </div>
        <div class="screen-label">Pay Bills</div>
      </div>
      <div class="screen-item reveal reveal-delay-2">
        <div class="screen-phone phone-md" style="animation: phoneFloat 7s ease-in-out infinite 2.5s;">
          <div class="screen-notch"></div>
          <div class="screen-body">
            <div class="s-header" style="margin-bottom:8px"><div class="s-title">💰 Yield Dashboard</div></div>
            <div style="background:linear-gradient(135deg,rgba(0,200,100,0.08),rgba(59,130,246,0.06));border:1px solid rgba(0,200,100,0.2);border-radius:10px;padding:10px;margin-bottom:8px;text-align:center;"><div style="font-size:7px;color:rgba(255,255,255,0.35);text-transform:uppercase;letter-spacing:0.06em;margin-bottom:4px;">Total Staked</div><div style="font-size:20px;font-weight:700;color:#fff;">$250.00</div><div style="font-size:8px;color:var(--green);margin-top:2px;">+$0.2192 earned · 10% APY</div></div>
            <div style="background:rgba(255,255,255,0.03);border:1px solid rgba(0,200,100,0.12);border-radius:8px;padding:8px;margin-bottom:6px;"><div style="display:flex;justify-content:space-between;font-size:8px;margin-bottom:4px;"><span style="color:rgba(255,255,255,0.5);">USDC · 📆 30 Days</span><span style="color:var(--green);font-weight:600;">10% APY</span></div><div style="display:flex;justify-content:space-between;font-size:7.5px;"><span style="color:rgba(255,255,255,0.3);">Unlocks in 24 days</span><span style="color:rgba(0,200,100,0.7);">+$0.68/day</span></div></div>
            <div style="background:rgba(255,255,255,0.03);border:1px solid rgba(167,139,250,0.15);border-radius:8px;padding:8px;margin-bottom:6px;"><div style="display:flex;justify-content:space-between;font-size:8px;margin-bottom:4px;"><span style="color:rgba(255,255,255,0.5);">SOL · 🔓 Flexible</span><span style="color:#A78BFA;font-weight:600;">5% APY</span></div><div style="display:flex;justify-content:space-between;font-size:7.5px;"><span style="color:rgba(255,255,255,0.3);">Withdraw anytime</span><span style="color:rgba(167,139,250,0.7);">+0.000068 SOL/day</span></div></div>
            <div style="display:grid;grid-template-columns:1fr 1fr;gap:4px;"><div style="background:rgba(0,200,100,0.08);border:1px solid rgba(0,200,100,0.2);border-radius:6px;padding:6px;text-align:center;font-size:8px;color:var(--green);font-weight:600;">➕ Stake More</div><div style="background:rgba(255,255,255,0.04);border:1px solid rgba(255,255,255,0.08);border-radius:6px;padding:6px;text-align:center;font-size:8px;color:rgba(255,255,255,0.5);">📤 Withdraw</div></div>
          </div>
        </div>
        <div class="screen-label">Yield Dashboard</div>
      </div>
    </div>
  </div>
</section>
<!-- ── HOW IT WORKS ──────────────────────────────────────────── -->
<section id="how-it-works">
  <div class="section-inner">
    <div class="reveal" style="text-align:center; margin-bottom: 0;">
      <div class="section-label" style="justify-content:center"><span style="display:none">—</span></div>
      <h2 class="section-title">Zero to trading in <em>4 steps</em></h2>
      <p class="section-body" style="margin: 0 auto; text-align:center;">No exchange account. No KYC walls. No Phantom setup. Just Telegram.</p>
    </div>
    <div class="steps-grid">
      <div class="step-card reveal reveal-delay-1"><div class="step-num">01</div><div class="step-title">Create Wallet</div><p class="step-desc">Open ClickBot on Telegram. A non-custodial Onchain wallet(Solana & EVM) is created instantly. You receive a 12-word phrase — only you hold your keys.</p></div>
      <div class="step-card reveal reveal-delay-2"><div class="step-num">02</div><div class="step-title">Fund It</div><p class="step-desc">Deposit SOL from any exchange. Buy USDC with Naira via bank transfer. Or bridge crypto in from 6 different chains — no P2P, no exchange account needed.</p></div>
      <div class="step-card reveal reveal-delay-3"><div class="step-num">03</div><div class="step-title">Analyze & Trade</div><p class="step-desc">Paste any Solana contract address. Get a full AI risk analysis in seconds. Then buy, snipe, or copy a proven wallet — in one tap.</p></div>
      <div class="step-card reveal reveal-delay-4"><div class="step-num">04</div><div class="step-title">Protect & Cash Out</div><p class="step-desc">Set trailing profit. ClickBot manages your exit 24/7. When you're done — sell, swap to USDC, and withdraw Naira to your bank in minutes.</p></div>
    </div>
  </div>
</section>

<!-- ── NGN BRIDGE ────────────────────────────────────────────── -->
<section id="ngn">
  <div class="section-inner">
    <div class="ngn-inner">
      <div class="reveal">
        <div class="section-label">Nigeria First</div>
        <h2 class="section-title">Trade, Pay Bills,<br><em>Bank Naira.</em></h2>
        <p class="section-body" style="margin-bottom: 48px;">Your Onchain wallet is now a local bank account. The first Solana trading bot with a complete Nigerian money stack. Token profit → USDC → bank account in minutes. Or pay any electricity, airtime, or bank transfer directly from USDC. No P2P. No exchange. No waiting.</p>
        <div class="ngn-flow">
          <div class="ngn-step"><div class="ngn-step-num">1</div><div><div class="ngn-step-title">Verify once with BVN</div><p class="ngn-step-desc">One-time BVN verification per CBN regulations. Takes 30 seconds.</p></div></div>
          <div class="ngn-step"><div class="ngn-step-num">2</div><div><div class="ngn-step-title">Get your virtual account</div><p class="ngn-step-desc">A permanent bank account is assigned to you. Transfer Naira to buy USDC anytime.</p></div></div>
          <div class="ngn-step"><div class="ngn-step-num">3</div><div><div class="ngn-step-title">Trade on Solana</div><p class="ngn-step-desc">Swap USDC → SOL → trade any token. Full trading suite at your fingertips.</p></div></div>
          <div class="ngn-step"><div class="ngn-step-num">4</div><div><div class="ngn-step-title">Withdraw profits to your bank</div><p class="ngn-step-desc">Sell → USDC → enter account number → Naira hits your account in minutes.</p></div></div>
        </div>
      </div>
      <div class="ngn-rate-card reveal reveal-delay-2">
        <div class="ngn-rate-title">💱 Live Bridge Rates</div>
        <div class="ngn-rate-row"><span class="ngn-rate-label">Exchange Rate</span><div class="ngn-rate-value cyan" id="live-rate">₦1,648 / $1</div></div>
        <div class="ngn-rate-row"><span class="ngn-rate-label">Withdrawal Fee</span><div class="ngn-rate-value">1%</div></div>
        <div class="ngn-rate-row"><span class="ngn-rate-label">Minimum</span><div class="ngn-rate-value">5 USDC</div></div>
        <div class="ngn-rate-row"><span class="ngn-rate-label">Settlement Time</span><div class="ngn-rate-value green">~3 minutes</div></div>
        <div class="ngn-rate-row"><span class="ngn-rate-label">Supported Banks</span><div class="ngn-rate-value" style="font-size:12px;text-align:right">GTBank, Access,<br>Zenith, Kuda, Opay<br>+ 200 more</div></div>
        <a href="https://t.me/clicksolbot" class="btn-primary" style="margin-top:28px; display:flex; justify-content:center; text-decoration:none;">Start Banking Crypto</a>
      </div>
    </div>
  </div>
</section>

<!-- ── PROOF ─────────────────────────────────────────────────── -->
<section id="proof">
  <div class="section-inner">
    <div style="text-align:center; margin-bottom: 32px;">
      <p style="font-family: var(--font-mono); font-size: 11px; color: var(--green); letter-spacing: 0.1em; text-transform: uppercase;">Live since launch · Updated every 90 seconds</p>
    </div>
    <div class="proof-stats reveal">
      <div class="proof-stat-card"><div class="proof-stat-num" id="count-users">0</div><div class="proof-stat-label">Active Traders</div></div>
      <div class="proof-stat-card"><div class="proof-stat-num" id="count-volume">0</div><div class="proof-stat-label">Volume Processed</div></div>
      <div class="proof-stat-card"><div class="proof-stat-num" id="count-countries">0</div><div class="proof-stat-label">Countries Reached</div></div>
      <div class="proof-stat-card"><div class="proof-stat-num" id="count-cac">$0</div><div class="proof-stat-label">Marketing Spend</div></div>
    </div>
  </div>
</section>

<!-- ── PRICING ───────────────────────────────────────────────── -->
<section id="pricing">
  <div class="section-inner">
    <div class="reveal" style="text-align:center">
      <div class="section-label" style="justify-content:center"><span></span></div>
      <h2 class="section-title">Transparent <em>pricing</em></h2>
      <p class="section-body" style="margin: 16px auto 0; text-align:center;">No hidden fees. Pay only for what you use.</p>
    </div>
    <div class="pricing-grid">
      <div class="pricing-card reveal reveal-delay-1">
        <div class="pricing-tier">Free Trader</div>
        <div class="pricing-price"><sup>$</sup>0<sub>/forever</sub></div>
        <div class="pricing-subtitle">Everything you need to start</div>
        <ul class="pricing-features"><li>Full AI token analysis</li><li>Spot buy & sell (1% fee)</li><li>Copy trading</li><li>Trailing profit engine</li><li>NGN fiat bridge</li><li>Multichain bridge (6 chains)</li><li>Referral program (20%)</li></ul>
        <a href="https://t.me/clicksolbot" class="pricing-cta outline">Start Free →</a>
      </div>
      <div class="pricing-card featured reveal">
        <div class="pricing-featured-badge">Most Popular</div>
        <div class="pricing-tier">Ultra Speed</div>
        <div class="pricing-price"><sup>$</sup>20<sub>/mo</sub></div>
        <div class="pricing-subtitle">MEV protection on every trade</div>
        <ul class="pricing-features"><li>Everything in Free</li><li>Unlimited Jito bundle trades</li><li>No per-trade ultra fee</li><li>Priority block inclusion</li><li>Anti-sandwich protection</li><li>Anti-frontrun routing</li><li>Best for active traders</li></ul>
        <a href="https://t.me/clicksolbot" class="pricing-cta solid">Subscribe Now →</a>
      </div>
      <div class="pricing-card reveal reveal-delay-2">
        <div class="pricing-tier">Sniper Pro</div>
        <div class="pricing-price"><sup>$</sup>20<sub>/mo</sub></div>
        <div class="pricing-subtitle">For launch hunters</div>
        <ul class="pricing-features"><li>Everything in Free</li><li>Ultra Speed on all snipes</li><li>Instant + limit sniping</li><li>Auto TP/SL post-snipe</li><li>Pending snipe manager</li><li>3% execution fee on trades</li><li>Best for new launch traders</li></ul>
        <a href="https://t.me/clicksolbot" class="pricing-cta outline">Get Sniper Pro →</a>
      </div>
    </div>
  </div>
</section>

<!-- ── FINAL CTA ──────────────────────────────────────────────── -->
<section id="final-cta">
  <div class="cta-bg"></div>
  <div class="section-inner">
    <h2 class="cta-headline reveal">Your Onchain wallet<br>should work like a bank. <em>Now it does.</em></h2>
    <p class="cta-sub reveal reveal-delay-1">The tool built by a trader who lost 9 months of salary — so you don't have to. Traders across 50+ countries found it organically. Now you know where to look.</p>
    <div class="cta-buttons reveal reveal-delay-2">
      <a href="https://t.me/clicksolbot" class="btn-primary"><span class="icon">✈️</span> Open ClickBot on Telegram</a>
      <a href="https://clickshift.io/faq" class="btn-secondary">Read the FAQ →</a>
    </div>
  </div>
</section>

<!-- ── FOOTER ─────────────────────────────────────────────────── -->
<footer>
  <div class="footer-inner">
    <div>
      <a href="#" class="nav-logo" style="text-decoration:none;display:flex;align-items:center;gap:10px;margin-bottom:0">
        <img src="/logo.png" alt="ClickBot" class="nav-logo-img footer-logo">
        <span class="nav-logo-text">Click<span>Bot</span></span>
      </a>
      <p class="footer-brand-desc">Turning Onchain wallets into local bank accounts. Trade, earn, pay bills, bridge 6 chains, and cash out to any Nigerian bank — all from Telegram. Built by ClickShift in Nigeria.</p>
    </div>
    <div>
      <div class="footer-col-title">Product</div>
      <ul class="footer-links">
        <li><a href="#pillars">What We Do</a></li>
        <li><a href="#features">Features</a></li>
        <li><a href="#multichain">Multichain</a></li>
        <li><a href="#pricing">Pricing</a></li>
        <li><a href="#ngn">NGN Bridge</a></li>
        <li><a href="https://clickshift.io/faq">FAQ</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Company</div>
      <ul class="footer-links">
        <li><a href="https://api.clickshift.io/legal">Privacy & Terms</a></li>
        <li><a href="https://clickshift.io">ClickShift.io</a></li>
        <li><a href="https://t.me/ClickShiftAlerts">Telegram Community</a></li>
        <li><a href="mailto:support@clickshift.io">support@clickshift.io</a></li>
      </ul>
    </div>
    <div>
      <div class="footer-col-title">Features</div>
      <ul class="footer-links">
        <li><a href="https://t.me/clicksolbot">Spot Trading</a></li>
        <li><a href="https://t.me/clicksolbot">Copy Trading</a></li>
        <li><a href="https://t.me/clicksolbot">Token Sniper</a></li>
        <li><a href="https://t.me/clicksolbot">Multichain Bridge</a></li>
        <li><a href="https://t.me/clicksolbot">Pay Bills</a></li>
        <li><a href="https://t.me/clicksolbot">Earn Yield</a></li>
        <li><a href="https://t.me/clicksolbot">NGN Withdrawal</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span>© 2026 ClickShift. Built on Solana.</span>
    <span style="color:var(--text-faint)">clickbot.clickshift.io · <a href="https://clickshift.io" style="color:var(--text-faint);text-decoration:none;">clickshift.io</a></span>
  </div>
</footer>

<!-- ── JAVASCRIPT ─────────────────────────────────────────────── -->
<script>
// ── NAV SCROLL ──────────────────────────────────────────────────
window.addEventListener('scroll', () => {
  document.getElementById('navbar').classList.toggle('scrolled', window.scrollY > 40);
});

// ── REVEAL ON SCROLL ────────────────────────────────────────────
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.1 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// ── VIDEO SWITCHER ──────────────────────────────────────────────
const VIDEOS = {
  trading:  { id: 'ZB_M8SNOyFQ', caption: 'See how AI-scored trading works — from contract paste to trailing-profit exit.' },
  payments: { id: 'XB6Renr4N-A', caption: 'Watch a bill get paid and money sent to a bank — just by typing in the chat.' },
  staking:  { id: 'XB6Renr4N-A', caption: 'Staking walkthrough coming soon — for now, see the payments flow in action.' },
};
function switchVideo(key) {
  const v = VIDEOS[key];
  if (!v) return;
  document.querySelectorAll('.video-tab').forEach(t => t.classList.toggle('active', t.dataset.video === key));
  const player = document.getElementById('video-player');
  player.src = `https://www.youtube-nocookie.com/embed/${v.id}?autoplay=1&mute=1&loop=1&playlist=${v.id}&controls=1&modestbranding=1&rel=0&playsinline=1`;
  document.getElementById('video-caption').textContent = v.caption;
}

// ── AGENT STREAM SIMULATION ────────────────────────────────────
const streamLines = [
  { agent: 'analyzer', cls: 'agent-analyzer', msg: 'Scanning <span class="highlight">$BONK</span> — fetching OHLCV candles...' },
  { agent: 'analyzer', cls: 'agent-analyzer', msg: 'Real RSI(14): <span class="val-green">28.4</span> — oversold territory confirmed' },
  { agent: 'analyzer', cls: 'agent-analyzer', msg: 'Buy pressure 1h: <span class="val-green">68%</span> · Volume surge: <span class="val-green">🚀 +240% vs avg</span>' },
  { agent: 'analyzer', cls: 'agent-analyzer', msg: 'Holder risk: <span class="val-green">LOW</span> · Top wallet: <span class="val-green">8.2%</span>' },
  { agent: 'analyzer', cls: 'agent-analyzer', msg: 'Liquidity: <span class="val-green">$2.4M</span> · Score: <span class="val-green">86/100</span> → BUY signal' },
  { agent: 'guardian', cls: 'agent-guardian', msg: 'Running safety checks on <span class="highlight">$BONK</span>...' },
  { agent: 'guardian', cls: 'agent-guardian', msg: '7-check pass: rug risk <span class="val-green">LOW</span> · liquidity <span class="val-green">SAFE</span> · age <span class="val-green">OK</span>' },
  { agent: 'sniper', cls: 'agent-sniper', msg: 'Limit snipe queued — target <span class="val-cyan">$0.0000220</span> · 0.01 SOL' },
  { agent: 'sniper', cls: 'agent-sniper', msg: 'Price touched <span class="val-cyan">$0.0000221</span> — executing...' },
  { agent: 'executor', cls: 'agent-executor', msg: 'Jito bundle submitted — bypassing mempool' },
  { agent: 'executor', cls: 'agent-executor', msg: 'Confirmed in block <span class="val-green">✅</span> — no frontrun detected' },
  { agent: 'executor', cls: 'agent-executor', msg: '<span class="val-green">841,000</span> BONK received · entry <span class="highlight">$0.0000221</span>' },
  { agent: 'guardian', cls: 'agent-guardian', msg: 'Activating trailing profit — kicks at <span class="val-gold">2x</span>, trail <span class="val-gold">15%</span>' },
  { agent: 'analyzer', cls: 'agent-analyzer', msg: 'Monitoring 24/7 — next price check in <span class="highlight">20s</span>' },
  { agent: 'guardian', cls: 'agent-guardian', msg: 'Peak detected: <span class="val-green">$0.0000481</span> — trailing stop set <span class="val-green">$0.0000409</span>' },
  { agent: 'executor', cls: 'agent-executor', msg: 'Price dropped to <span class="val-red">$0.0000402</span> — trailing triggered' },
  { agent: 'executor', cls: 'agent-executor', msg: 'Exit executed: <span class="val-green">+117% profit</span> · <span class="val-green">0.0218 SOL received</span>' },
  { agent: 'analyzer', cls: 'agent-analyzer', msg: 'Scanning next opportunity... <span class="highlight">$WIF</span> showing momentum' },
];
let lineIdx = 0;
const output = document.getElementById('stream-output');
function addLine() {
  const l = streamLines[lineIdx % streamLines.length];
  lineIdx++;
  const div = document.createElement('div');
  div.className = 'stream-line';
  div.style.animationDelay = '0s';
  div.innerHTML = `<span class="stream-agent ${l.cls}">[${l.agent}]</span><span class="stream-msg">${l.msg}</span>`;
  output.appendChild(div);
  while (output.children.length > 13) output.removeChild(output.firstChild);
  const existing = output.querySelector('.stream-cursor');
  if (existing) existing.remove();
  const cursor = document.createElement('span');
  cursor.className = 'stream-cursor';
  output.appendChild(cursor);
  output.scrollTop = output.scrollHeight;
}
setTimeout(() => { addLine(); setInterval(addLine, 2200); }, 800);

// ── COUNTER ANIMATION ───────────────────────────────────────────
function animateCounterFormatted(el, target, formatter, duration = 1500) {
  if (!el) return;
  target = parseFloat(target) || 0;
  let start = 0;
  const startTime = performance.now();
  function tick(now) {
    const progress = Math.min((now - startTime) / duration, 1);
    const current = start + (target - start) * progress;
    el.textContent = formatter(current);
    if (progress < 1) requestAnimationFrame(tick);
    else el.textContent = formatter(target);
  }
  requestAnimationFrame(tick);
}
let _liveStatsCache = null;
let _proofAnimated = false;
const proofObserver = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting && _liveStatsCache && !_proofAnimated) { runProofAnimation(); _proofAnimated = true; proofObserver.disconnect(); }
  });
}, { threshold: 0.3 });
const proofSection = document.getElementById('proof');
if (proofSection) proofObserver.observe(proofSection);
function runProofAnimation() {
  if (!_liveStatsCache) return;
  const { users, volume, countries } = _liveStatsCache;
  animateCounterFormatted(document.getElementById('count-users'), users, v => Math.floor(v).toLocaleString());
  animateCounterFormatted(document.getElementById('count-volume'), volume, v => fmtUSD(v));
  animateCounterFormatted(document.getElementById('count-countries'), countries, v => Math.floor(v) + '+');
}

// ── LIVE RATE SIMULATION ────────────────────────────────────────
const rateEl = document.getElementById('live-rate');
if (rateEl) {
  setInterval(() => {
    const base = 1648;
    const jitter = Math.floor(Math.random() * 8) - 4;
    rateEl.textContent = `₦${(base + jitter).toLocaleString()} / $1`;
  }, 4000);
}

// ── SMOOTH SCROLL ───────────────────────────────────────────────
document.querySelectorAll('a[href^="#"]').forEach(a => {
  a.addEventListener('click', e => {
    const target = document.querySelector(a.getAttribute('href'));
    if (target) { e.preventDefault(); target.scrollIntoView({ behavior: 'smooth', block: 'start' }); }
  });
});

// ── STATS FETCHER ──────────────────────────────────────────────────
const STATS_API = 'https://api.clickshift.io';
function fmtK(n) { n = parseFloat(n) || 0; if (n >= 1e6) return (n/1e6).toFixed(2)+'M'; if (n >= 1e3) return (n/1e3).toFixed(1)+'K'; return n.toLocaleString(); }
function fmtUSD(n) { n = parseFloat(n) || 0; if (n >= 1e6) return '$'+(n/1e6).toFixed(2)+'M'; if (n >= 1e3) return '$'+(n/1e3).toFixed(1)+'K'; return '$'+n.toFixed(0); }
function fmtNGN(n) { n = parseFloat(n) || 0; if (n >= 1e9) return '₦'+(n/1e9).toFixed(2)+'B'; if (n >= 1e6) return '₦'+(n/1e6).toFixed(1)+'M'; if (n >= 1e3) return '₦'+(n/1e3).toFixed(1)+'K'; return '₦'+n.toFixed(0); }
function setText(id, val) { const el = document.getElementById(id); if (el) el.textContent = val; }

async function loadStats() {
  let live = {}, summary = {};
  try {
    const [liveRes, summaryRes] = await Promise.all([ fetch(STATS_API + '/api/stats/live'), fetch(STATS_API + '/api/stats/summary') ]);
    live = await liveRes.json();
    summary = await summaryRes.json();
    setText('stat-users', fmtK(live.users));
    setText('stat-users-sub', `+${summary.users?.new_7d || 0} this week`);
    setText('stat-active', fmtK(live.active_7d));
    setText('stat-volume', fmtUSD(live.volume_usd));
    setText('stat-txs', fmtK(live.transactions));
    setText('stat-ngn', fmtNGN(live.ngn_bridge_volume));
    setText('stat-fiat-txs', (summary.fiat?.transactions || 0).toLocaleString());
    setText('stat-success-rate', `${summary.fiat?.success_rate_pct || 0}% success`);
    setText('mod-spot-badge', `${(summary.trading?.trades_7d || 0).toLocaleString()} this week`);
    setText('mod-trades', fmtK(summary.trading?.total_trades));
    setText('mod-volume', fmtUSD(summary.trading?.volume_usd));
    setText('mod-traders', fmtK(summary.trading?.unique_traders));
    setText('mod-sniper-badge', `${summary.sniper?.fill_rate_pct || 0}% fill rate`);
    setText('mod-snipes', fmtK(summary.sniper?.total_snipes));
    setText('mod-snipes-7d', (summary.sniper?.snipes_7d || 0).toLocaleString());
    setText('mod-copy-badge', `${summary.copy_trading?.active_sessions || 0} active`);
    setText('mod-copied', fmtK(summary.copy_trading?.total_copied_trades));
    setText('mod-copy-rate', `${summary.copy_trading?.success_rate_pct || 0}%`);
    setText('mod-copy-sessions', summary.copy_trading?.active_sessions || 0);
    setText('mod-perps-badge', `${summary.perps?.open_now || 0} open`);
    setText('mod-positions', fmtK(summary.perps?.total_positions));
    setText('mod-open', summary.perps?.open_now || 0);
    setText('mod-winrate', `${summary.perps?.win_rate_pct || 0}%`);
    setText('mod-wallets', fmtK(summary.users?.total));
    setText('mod-kyc', (summary.users?.kyc_verified || 0).toLocaleString());
    setText('mod-new30', (summary.users?.new_30d || 0).toLocaleString());
    setText('mod-referred', fmtK(summary.referrals?.total_referred));
    setText('mod-referrers', (summary.referrals?.active_referrers || 0).toLocaleString());
    setText('mod-util-badge', `${(summary.utility?.payments_7d || 0)} this week`);
    setText('mod-util-total', fmtK(summary.utility?.total_payments));
    setText('mod-util-ngn', fmtNGN(summary.utility?.ngn_volume));
    setText('mod-util-rate', `${summary.utility?.success_rate_pct || 0}%`);
    setText('mod-bills-badge', `${summary.bank_transfers?.success_rate_pct || 0}% success`);
    setText('mod-bills-total', fmtK(summary.bank_transfers?.transactions));
    setText('mod-bills-ngn', fmtNGN(summary.bank_transfers?.ngn_volume));
    setText('mod-bills-banks', (summary.bank_transfers?.unique_banks || 0).toLocaleString());
    setText('mod-yield-badge', `${summary.yield?.unique_stakers || 0} stakers`);
    setText('mod-yield-pool', fmtUSD(summary.yield?.live_pool_usd));
    setText('mod-yield-stakers', (summary.yield?.active_deposits || 0).toLocaleString());
    const updated = document.getElementById('stats-updated');
    if (updated && live.generated_at) { const secs = Math.floor((Date.now() - live.generated_at) / 1000); updated.textContent = ` · Updated ${secs < 60 ? secs + 's' : Math.floor(secs/60) + 'm'} ago`; }
  } catch (e) { console.warn('[Stats] API unavailable', e.message); }
  setText('hero-stat-users', fmtK(live.users));
  setText('hero-stat-volume', fmtUSD(live.volume_usd));
  _liveStatsCache = { users: parseFloat(live.users) || 0, volume: parseFloat(live.volume_usd) || 0, countries: parseFloat(summary.users?.countries_count) || 50 };
  if (!_proofAnimated && proofSection) { const rect = proofSection.getBoundingClientRect(); if (rect.top < window.innerHeight && rect.bottom > 0) { runProofAnimation(); _proofAnimated = true; } }
}
loadStats();
setInterval(loadStats, 90_000);

// ── REFERRAL LEADERBOARD ────────────────────────────────────────
const LB_MEDALS = ['👑','🥈','🥉'];
const LB_COLORS = ['#F59E0B','#C0C0C0','#CD7F32'];
let currentLbPeriod = 'all';
async function loadLeaderboard(period) {
  currentLbPeriod = period;
  ['all','30d','7d'].forEach(p => { const el = document.getElementById('tab-'+p); if (el) el.className = 'lb-tab' + (p === period ? ' active' : ''); });
  const container = document.getElementById('lb-entries');
  container.innerHTML = '<div style="text-align:center;padding:24px;color:rgba(255,255,255,0.2);font-size:13px;">Loading…</div>';
  try {
    const [lbRes, statsRes] = await Promise.all([ fetch(`${STATS_API}/api/referral/leaderboard?period=${period}&limit=10`), fetch(`${STATS_API}/api/referral/stats`) ]);
    const lb = await lbRes.json();
    const stats = await statsRes.json();
    const st = (id, val) => { const el = document.getElementById(id); if (el) el.textContent = val; };
    st('lb-total-paid', (parseFloat(stats.total_paid_out_sol)||0).toFixed(4) + ' SOL');
    st('lb-referrers', stats.total_referrers || 0);
    st('lb-referred', stats.total_referred_users || 0);
    st('lb-7d', (parseFloat(stats.paid_7d_sol)||0).toFixed(4) + ' SOL');
    const entries = lb.entries || [];
    if (!entries.length) { container.innerHTML = '<div style="text-align:center;padding:24px;color:rgba(255,255,255,0.2);">No entries yet — be first! 🚀</div>'; return; }
    container.innerHTML = entries.map((e) => {
      const isTop = e.rank <= 3;
      const color = isTop ? LB_COLORS[e.rank-1] : (e.rank <= 10 ? '#22d3ee' : '#64748b');
      const label = isTop ? LB_MEDALS[e.rank-1] : '#' + e.rank;
      const sol = (parseFloat(e.total_earned_sol)||0).toFixed(5);
      return `<div class="lb-entry ${isTop ? 'top3' : ''}"><div class="lb-rank" style="background:${color}18;color:${color}">${label}</div><div style="flex:1;min-width:0"><div class="lb-name">${e.display_name}</div><div class="lb-meta">${e.unique_referrals} referrals · ${e.trades_generated} trades</div></div><div class="lb-earned" style="color:${color}">${sol} SOL</div></div>`;
    }).join('');
  } catch(err) { container.innerHTML = '<div style="text-align:center;padding:24px;color:rgba(255,100,100,0.5);">Could not load leaderboard</div>'; }
}
loadLeaderboard('all');

// ── TRENDING PICKS ──────────────────────────────────────────────
let _trendPicks = [];
let _trendFilter = 'boost';
let _trendTimer = null;
async function loadTrendingPicks() {
  try {
    const res = await fetch(STATS_API + '/api/picks/public', { signal: AbortSignal.timeout(12000) });
    const data = await res.json();
    _trendPicks = data.picks || [];
  } catch (e) {
    try {
      const r = await fetch('https://api.dexscreener.com/token-boosts/top/v1');
      const arr = await r.json();
      _trendPicks = (arr || []).filter(t => t.chainId === 'solana').slice(0, 6).map((t, i) => ({
        mint: t.tokenAddress, symbol: t.tokenAddress?.slice(0,5).toUpperCase() || '???', name: 'Loading...',
        score: 70 - i * 3, change1h: 0, change6h: 0, mc: 0, buys: 0, sells: 0, buyRatio: 50, ageHours: 0,
        isPump: t.tokenAddress?.endsWith('pump') || false, source: 'boost',
        signals: ['⚡ Active boost signal — team marketing now'], pairUrl: t.url || `https://dexscreener.com/solana/${t.tokenAddress}`, imageUrl: null,
      }));
    } catch (_) {}
  }
  renderTrendGrid();
}
function renderTrendGrid() {
  const grid = document.getElementById('trend-grid');
  if (!grid) return;
  const filtered = _trendFilter === 'boost' ? _trendPicks.filter(p => p.source === 'boost') : _trendFilter === 'new' ? _trendPicks.filter(p => p.ageHours < 6) : _trendPicks;
  const show = filtered.length ? filtered : _trendPicks;
  if (!show.length) { grid.innerHTML = '<div style="grid-column:1/-1;text-align:center;padding:40px;color:rgba(255,255,255,0.3);font-size:14px;">Scanning market... check back in 30 seconds.</div>'; return; }
  const fmtMC = mc => { if (!mc) return '—'; if (mc >= 1e6) return '$'+(mc/1e6).toFixed(2)+'M'; return '$'+(mc/1000).toFixed(0)+'K'; };
  const fmtAge = h => { if (!h) return '—'; return h < 1 ? Math.round(h*60)+'m old' : h.toFixed(1)+'h old'; };
  const scoreColor = s => s >= 70 ? '#00C864' : s >= 50 ? '#F59E0B' : '#FB923C';
  grid.innerHTML = show.slice(0, 6).map((p, i) => {
    const chg1h = parseFloat(p.change1h || 0);
    const chgClass = chg1h >= 0 ? 'green' : 'red';
    const chgStr = (chg1h >= 0 ? '+' : '') + chg1h.toFixed(1) + '%';
    const srcClass = { boost: 'src-boost', profile: 'src-profile', trending: 'src-trending' }[p.source] || '';
    const imgEl = p.imageUrl ? `<img src="${p.imageUrl}" class="trend-tok-img" onerror="this.style.display='none'">` : `<div class="trend-tok-img-placeholder">${(p.symbol||'?').charAt(0)}</div>`;
    const sig = (p.signals||[])[0] || 'Signal detected';
    const tgUrl = `https://t.me/clicksolbot?start=buy_${p.mint}`;
    return `<div class="trend-card ${srcClass}" onclick="window.open('${tgUrl}','_blank')"><div class="trend-rank">#${i+1}</div><div class="trend-tok-header">${imgEl}<div style="min-width:0"><div class="trend-tok-name">${p.symbol || '???'}</div><div class="trend-tok-badges">${p.isPump ? '<span class="trend-badge badge-pump">pump.fun</span>' : ''}${p.source==='boost' ? '<span class="trend-badge badge-boost">boosted</span>' : ''}${p.source==='profile' ? '<span class="trend-badge badge-new">new</span>' : ''}</div></div></div><div class="trend-score-bar"><div class="trend-score-fill" style="width:${p.score||0}%;background:${scoreColor(p.score||0)}"></div></div><div class="trend-stats"><div class="trend-stat-item"><div class="trend-stat-label">Score</div><div class="trend-stat-value" style="color:${scoreColor(p.score||0)}">${p.score||0}/100</div></div><div class="trend-stat-item"><div class="trend-stat-label">1h Change</div><div class="trend-stat-value ${chgClass}">${chgStr}</div></div><div class="trend-stat-item"><div class="trend-stat-label">Market Cap</div><div class="trend-stat-value">${fmtMC(p.mc)}</div></div><div class="trend-stat-item"><div class="trend-stat-label">Age</div><div class="trend-stat-value">${fmtAge(p.ageHours)}</div></div></div><div class="trend-signal">💡 ${sig}</div><a href="${tgUrl}" target="_blank" class="trend-card-cta" onclick="event.stopPropagation()">Trade in ClickBot →</a></div>`;
  }).join('');
  const lbl = document.getElementById('trend-refresh-label');
  if (lbl) lbl.textContent = 'Updated ' + new Date().toLocaleTimeString();
}
function setTrendFilter(f) {
  _trendFilter = f;
  document.querySelectorAll('.trend-tab').forEach(t => t.classList.remove('active'));
  event?.target?.classList.add('active');
  renderTrendGrid();
}
loadTrendingPicks();
clearInterval(_trendTimer);
_trendTimer = setInterval(loadTrendingPicks, 4 * 60 * 1000);

// ── TRADER RANKINGS ─────────────────────────────────────────────
async function loadTraderLeaderboard(period = 'quarter') {
  const container = document.getElementById('trader-lb-entries');
  if (!container) return;
  container.innerHTML = '<div style="text-align:center;padding:24px;color:rgba(255,255,255,0.2);">Loading...</div>';
  try {
    const res = await fetch(`${STATS_API}/api/traders/leaderboard?period=${period}&limit=10`);
    const data = await res.json();
    const entries = data.entries || [];
    document.querySelectorAll('.trader-tab').forEach(t => { t.classList.toggle('active', t.dataset.period === period); });
    if (!entries.length) { container.innerHTML = '<div style="text-align:center;padding:24px;color:rgba(255,255,255,0.2);">No trading activity yet — be first!</div>'; return; }
    const TIER = { diamond:'💎', platinum:'🏆', gold:'🥇', silver:'🥈', bronze:'🥉' };
    const MEDALS = ['👑','🥈','🥉'];
    const COLORS = ['#F59E0B','#C0C0C0','#CD7F32'];
    container.innerHTML = entries.map((e) => {
      const isTop = e.rank <= 3;
      const color = isTop ? COLORS[e.rank-1] : '#22d3ee';
      const label = isTop ? MEDALS[e.rank-1] : '#' + e.rank;
      const vol = e.volume_sol >= 1000 ? (e.volume_sol/1000).toFixed(1)+'K SOL' : e.volume_sol.toFixed(3)+' SOL';
      const pts = e.shift_points >= 1000 ? (e.shift_points/1000).toFixed(1)+'K pts' : Math.round(e.shift_points)+' pts';
      const tier = TIER[e.tier] || '◎';
      const early = e.is_early_adopter ? ' ⚡3×' : '';
      return `<div style="display:flex;align-items:center;gap:12px;border-radius:10px;padding:12px 16px;border:1px solid ${isTop ? color + '33' : 'rgba(255,255,255,0.06)'};background:${isTop ? color + '0a' : 'rgba(255,255,255,0.02)'};margin-bottom:8px;"><div style="width:36px;height:36px;border-radius:8px;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:14px;flex-shrink:0;background:${color}18;color:${color}">${label}</div><div style="flex:1;min-width:0"><div style="font-size:14px;font-weight:600;color:#fff">${tier} ${e.display_name}${early}</div><div style="font-size:11px;color:rgba(255,255,255,0.3);margin-top:2px">${vol} · ${pts} · ${e.trade_count} trades</div></div><div style="font-weight:700;font-size:13px;font-family:var(--font-mono);color:${color}">${tier}</div></div>`;
    }).join('');
  } catch(err) { container.innerHTML = '<div style="text-align:center;padding:24px;color:rgba(255,100,100,0.4);">Could not load rankings</div>'; }
}
loadTraderLeaderboard('quarter');
</script>
</body>
</html>
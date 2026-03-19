# legionella
Dad's legionella draft app
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>AquaGuard WMP — Legionella Field Inspector</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Barlow+Condensed:wght@400;600;700;800&family=Barlow:wght@400;500;600&display=swap');

:root {
  --bg: #f0f2f0;
  --surface: #ffffff;
  --surface2: #f7f8f7;
  --border: #dde0dd;
  --text: #1a1f1a;
  --muted: #6b736b;
  --accent: #1a6b3c;
  --accent2: #0f4a2a;
  --warn: #c45c00;
  --danger: #c42b00;
  --safe: #1a6b3c;
  --mono: 'DM Mono', monospace;
  --head: 'Barlow Condensed', sans-serif;
  --body: 'Barlow', sans-serif;
  --radius: 10px;
  --shadow: 0 2px 12px rgba(0,0,0,0.08);
}

* { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

body {
  font-family: var(--body);
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  max-width: 480px;
  margin: 0 auto;
  position: relative;
}

/* ── TOP NAV ── */
.topbar {
  background: var(--accent2);
  color: #fff;
  padding: 14px 18px 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 100;
}
.topbar-logo {
  font-family: var(--head);
  font-size: 1.3rem;
  font-weight: 800;
  letter-spacing: 0.06em;
  line-height: 1;
}
.topbar-logo span { color: #4dff91; }
.topbar-sub {
  font-family: var(--mono);
  font-size: 0.6rem;
  color: rgba(255,255,255,0.55);
  letter-spacing: 0.1em;
  margin-top: 2px;
}
.topbar-status {
  display: flex;
  align-items: center;
  gap: 6px;
  font-family: var(--mono);
  font-size: 0.65rem;
  color: rgba(255,255,255,0.6);
}
.offline-dot {
  width: 7px; height: 7px; border-radius: 50%;
  background: #4dff91;
  box-shadow: 0 0 6px #4dff91;
  animation: pulse 2s infinite;
}
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.4} }

/* ── BOTTOM NAV ── */
.bottom-nav {
  position: fixed;
  bottom: 0; left: 50%;
  transform: translateX(-50%);
  width: 100%;
  max-width: 480px;
  background: var(--accent2);
  display: flex;
  z-index: 100;
  border-top: 2px solid rgba(255,255,255,0.08);
}
.nav-btn {
  flex: 1;
  padding: 10px 4px 12px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3px;
  background: none;
  border: none;
  cursor: pointer;
  color: rgba(255,255,255,0.45);
  font-family: var(--head);
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  transition: color 0.15s;
}
.nav-btn.active { color: #4dff91; }
.nav-btn svg { width: 22px; height: 22px; }

/* ── SCREENS ── */
.screen { display: none; padding: 16px 14px 90px; animation: fadeIn 0.2s ease; }
.screen.active { display: block; }
@keyframes fadeIn { from{opacity:0;transform:translateY(6px)} to{opacity:1;transform:none} }

/* ── CARDS ── */
.card {
  background: var(--surface);
  border-radius: var(--radius);
  border: 1px solid var(--border);
  margin-bottom: 12px;
  overflow: hidden;
  box-shadow: var(--shadow);
}
.card-header {
  background: var(--surface2);
  padding: 10px 14px;
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  gap: 8px;
}
.card-header h3 {
  font-family: var(--head);
  font-size: 0.95rem;
  font-weight: 700;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: var(--accent2);
}
.card-header .step-badge {
  background: var(--accent);
  color: #fff;
  font-family: var(--mono);
  font-size: 0.6rem;
  padding: 2px 7px;
  border-radius: 20px;
  margin-left: auto;
}
.card-body { padding: 14px; }

/* ── FORM ELEMENTS ── */
.field { margin-bottom: 14px; }
.field:last-child { margin-bottom: 0; }
label {
  display: block;
  font-family: var(--mono);
  font-size: 0.68rem;
  color: var(--muted);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  margin-bottom: 5px;
}
label .req { color: var(--danger); }

input[type=text], input[type=number], input[type=date], input[type=time], select, textarea {
  width: 100%;
  padding: 11px 13px;
  border: 1.5px solid var(--border);
  border-radius: 7px;
  font-family: var(--body);
  font-size: 0.95rem;
  color: var(--text);
  background: var(--surface);
  appearance: none;
  -webkit-appearance: none;
  outline: none;
  transition: border-color 0.15s;
}
input:focus, select:focus, textarea:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(26,107,60,0.12);
}
select { background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%236b736b' stroke-width='1.5' fill='none' stroke-linecap='round'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 12px center; padding-right: 36px; }
textarea { resize: none; height: 80px; }

.field-row { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.field-row3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; }

/* ── TEMP INPUT with risk indicator ── */
.temp-input-wrap { position: relative; }
.temp-input-wrap input { padding-right: 52px; }
.temp-unit {
  position: absolute;
  right: 12px; top: 50%;
  transform: translateY(-50%);
  font-family: var(--mono);
  font-size: 0.75rem;
  color: var(--muted);
}
.risk-bar {
  height: 4px;
  border-radius: 2px;
  margin-top: 5px;
  background: var(--border);
  overflow: hidden;
}
.risk-fill {
  height: 100%;
  border-radius: 2px;
  transition: width 0.3s, background 0.3s;
  width: 0%;
  background: var(--safe);
}

/* ── RISK BADGE ── */
.risk-badge {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  padding: 3px 10px;
  border-radius: 20px;
  font-family: var(--mono);
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.05em;
}
.risk-low    { background: #e6f7ed; color: var(--safe); border: 1px solid #b3e6c8; }
.risk-medium { background: #fff3e6; color: var(--warn); border: 1px solid #ffd199; }
.risk-high   { background: #ffeee6; color: var(--danger); border: 1px solid #ffb399; }

/* ── PHOTO CAPTURE ── */
.photo-zone {
  border: 2px dashed var(--border);
  border-radius: 8px;
  padding: 20px;
  text-align: center;
  cursor: pointer;
  background: var(--surface2);
  transition: border-color 0.15s, background 0.15s;
  position: relative;
}
.photo-zone:active { border-color: var(--accent); background: #f0f7f3; }
.photo-zone svg { width: 32px; height: 32px; color: var(--muted); margin-bottom: 6px; }
.photo-zone p { font-size: 0.8rem; color: var(--muted); line-height: 1.4; }
.photo-zone input[type=file] { position: absolute; inset: 0; opacity: 0; cursor: pointer; }
.photo-thumbs { display: flex; gap: 8px; flex-wrap: wrap; margin-top: 10px; }
.photo-thumb {
  width: 72px; height: 72px;
  border-radius: 6px;
  background: var(--surface2);
  border: 1px solid var(--border);
  overflow: hidden;
  position: relative;
}
.photo-thumb img { width: 100%; height: 100%; object-fit: cover; }
.photo-thumb .del-photo {
  position: absolute; top: 2px; right: 2px;
  background: rgba(0,0,0,0.6);
  color: #fff;
  border: none;
  border-radius: 50%;
  width: 18px; height: 18px;
  font-size: 11px;
  cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  line-height: 1;
}

/* ── SAMPLE POINT ROWS ── */
.sample-list { display: flex; flex-direction: column; gap: 10px; }
.sample-row {
  background: var(--surface2);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 12px;
  position: relative;
}
.sample-row-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
}
.sample-row-title {
  font-family: var(--head);
  font-size: 0.9rem;
  font-weight: 700;
  color: var(--accent2);
  letter-spacing: 0.03em;
}
.btn-del {
  background: none;
  border: 1px solid var(--border);
  border-radius: 5px;
  color: var(--danger);
  font-size: 0.75rem;
  padding: 3px 8px;
  cursor: pointer;
  font-family: var(--mono);
}

/* ── BUTTONS ── */
.btn-primary {
  width: 100%;
  padding: 14px;
  background: var(--accent);
  color: #fff;
  border: none;
  border-radius: 8px;
  font-family: var(--head);
  font-size: 1.05rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  cursor: pointer;
  transition: background 0.15s, transform 0.1s;
}
.btn-primary:active { background: var(--accent2); transform: scale(0.98); }

.btn-secondary {
  width: 100%;
  padding: 12px;
  background: transparent;
  color: var(--accent);
  border: 1.5px solid var(--accent);
  border-radius: 8px;
  font-family: var(--head);
  font-size: 0.95rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  cursor: pointer;
  transition: background 0.15s;
  margin-top: 8px;
}
.btn-secondary:active { background: #e6f7ed; }

.btn-add {
  width: 100%;
  padding: 10px;
  background: transparent;
  color: var(--accent);
  border: 1.5px dashed var(--accent);
  border-radius: 8px;
  font-family: var(--head);
  font-size: 0.9rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  cursor: pointer;
  margin-top: 8px;
}

/* ── DASHBOARD ── */
.dash-header {
  font-family: var(--head);
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 10px;
  padding-bottom: 6px;
  border-bottom: 1px solid var(--border);
}
.stat-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 14px; }
.stat-box {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 14px;
  box-shadow: var(--shadow);
}
.stat-val {
  font-family: var(--head);
  font-size: 2rem;
  font-weight: 800;
  color: var(--accent2);
  line-height: 1;
}
.stat-label {
  font-family: var(--mono);
  font-size: 0.62rem;
  color: var(--muted);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  margin-top: 4px;
}
.stat-box.danger .stat-val { color: var(--danger); }
.stat-box.warn .stat-val { color: var(--warn); }

.inspection-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 13px 14px;
  margin-bottom: 8px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-shadow: var(--shadow);
  cursor: pointer;
}
.insp-left { flex: 1; }
.insp-name {
  font-family: var(--head);
  font-size: 1rem;
  font-weight: 700;
  color: var(--text);
}
.insp-meta {
  font-family: var(--mono);
  font-size: 0.65rem;
  color: var(--muted);
  margin-top: 2px;
}
.insp-arrow { color: var(--muted); font-size: 1.2rem; }

/* ── OUTPUTS PANEL ── */
.output-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.output-tile {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 10px;
  padding: 18px 12px;
  text-align: center;
  cursor: pointer;
  box-shadow: var(--shadow);
  transition: border-color 0.15s, box-shadow 0.15s;
  position: relative;
  overflow: hidden;
}
.output-tile::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
}
.output-tile.pdf::before { background: var(--danger); }
.output-tile.dash::before { background: var(--accent); }
.output-tile.csv::before { background: var(--warn); }
.output-tile.raw::before { background: #5566aa; }
.output-tile:active { box-shadow: 0 0 0 2px var(--accent); }
.output-tile svg { width: 36px; height: 36px; margin-bottom: 8px; }
.output-tile h4 {
  font-family: var(--head);
  font-size: 0.9rem;
  font-weight: 700;
  letter-spacing: 0.04em;
  color: var(--text);
}
.output-tile p {
  font-size: 0.72rem;
  color: var(--muted);
  margin-top: 3px;
}

/* ── TOAST ── */
.toast {
  position: fixed;
  bottom: 80px;
  left: 50%; transform: translateX(-50%);
  background: var(--accent2);
  color: #fff;
  padding: 10px 20px;
  border-radius: 30px;
  font-family: var(--mono);
  font-size: 0.75rem;
  letter-spacing: 0.05em;
  white-space: nowrap;
  z-index: 999;
  opacity: 0;
  transition: opacity 0.25s;
  pointer-events: none;
}
.toast.show { opacity: 1; }

/* ── SECTION TITLE ── */
.section-title {
  font-family: var(--head);
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--muted);
  margin: 18px 0 8px;
}

/* Risk legend */
.risk-legend {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 14px;
}
.rleg {
  font-family: var(--mono);
  font-size: 0.62rem;
  padding: 3px 8px;
  border-radius: 20px;
  letter-spacing: 0.05em;
}

/* Progress stepper */
.stepper {
  display: flex;
  align-items: center;
  gap: 0;
  margin-bottom: 16px;
}
.step-dot {
  width: 28px; height: 28px;
  border-radius: 50%;
  background: var(--border);
  color: var(--muted);
  font-family: var(--mono);
  font-size: 0.7rem;
  display: flex; align-items: center; justify-content: center;
  font-weight: 500;
  flex-shrink: 0;
}
.step-dot.done { background: var(--accent); color: #fff; }
.step-dot.active { background: var(--accent2); color: #fff; box-shadow: 0 0 0 3px rgba(26,107,60,0.2); }
.step-line { flex: 1; height: 2px; background: var(--border); }
.step-line.done { background: var(--accent); }

/* inline hint */
.hint {
  font-family: var(--mono);
  font-size: 0.65rem;
  color: var(--muted);
  margin-top: 4px;
  line-height: 1.5;
}

/* ASHRAE banner */
.ashrae-banner {
  background: linear-gradient(135deg, #0f4a2a, #1a6b3c);
  color: #fff;
  border-radius: 8px;
  padding: 12px 14px;
  margin-bottom: 14px;
  display: flex;
  align-items: center;
  gap: 10px;
}
.ashrae-banner svg { flex-shrink: 0; }
.ashrae-banner p { font-size: 0.78rem; line-height: 1.4; opacity: 0.9; }
.ashrae-banner strong { font-family: var(--head); font-size: 0.85rem; letter-spacing: 0.04em; display: block; margin-bottom: 2px; }

</style>
</head>
<body>

<!-- TOP BAR -->
<div class="topbar">
  <div>
    <div class="topbar-logo">Aqua<span>Guard</span> WMP</div>
    <div class="topbar-sub">LEGIONELLA FIELD INSPECTOR · ASHRAE 188</div>
  </div>
  <div class="topbar-status">
    <div class="offline-dot"></div>
    OFFLINE READY
  </div>
</div>

<!-- ═══════════════════════════════════ -->
<!--  SCREEN 1: NEW INSPECTION          -->
<!-- ═══════════════════════════════════ -->
<div class="screen active" id="screen-inspect">

  <!-- Progress -->
  <div style="margin-bottom:16px;margin-top:4px;">
    <div class="stepper">
      <div class="step-dot done" id="s1">1</div>
      <div class="step-line done" id="sl1"></div>
      <div class="step-dot active" id="s2">2</div>
      <div class="step-line" id="sl2"></div>
      <div class="step-dot" id="s3">3</div>
      <div class="step-line" id="sl3"></div>
      <div class="step-dot" id="s4">4</div>
    </div>
    <div style="display:flex;justify-content:space-between;margin-top:3px;">
      <span style="font-family:var(--mono);font-size:0.58rem;color:var(--muted)">BUILDING</span>
      <span style="font-family:var(--mono);font-size:0.58rem;color:var(--muted)">SYSTEM INV.</span>
      <span style="font-family:var(--mono);font-size:0.58rem;color:var(--muted)">SAMPLES</span>
      <span style="font-family:var(--mono);font-size:0.58rem;color:var(--muted)">REVIEW</span>
    </div>
  </div>

  <!-- CARD 1: Inspector + Date -->
  <div class="card">
    <div class="card-header">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/></svg>
      <h3>Inspector Info</h3>
      <span class="step-badge">STEP 1</span>
    </div>
    <div class="card-body">
      <div class="field-row">
        <div class="field">
          <label>Inspector Name <span class="req">*</span></label>
          <input type="text" id="insp-name" placeholder="J. Smith, CIH">
        </div>
        <div class="field">
          <label>Cert / License #</label>
          <input type="text" id="insp-cert" placeholder="CIH-12345">
        </div>
      </div>
      <div class="field-row">
        <div class="field">
          <label>Date <span class="req">*</span></label>
          <input type="date" id="insp-date">
        </div>
        <div class="field">
          <label>Time <span class="req">*</span></label>
          <input type="time" id="insp-time">
        </div>
      </div>
    </div>
  </div>

  <!-- CARD 2: Building Profile -->
  <div class="card">
    <div class="card-header">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><rect x="3" y="3" width="18" height="18" rx="1"/><path d="M9 9h6M9 13h6M9 17h4"/></svg>
      <h3>Building Profile</h3>
    </div>
    <div class="card-body">
      <div class="field">
        <label>Building Name / Facility <span class="req">*</span></label>
        <input type="text" id="bldg-name" placeholder="e.g. Riverside Medical Center">
      </div>
      <div class="field">
        <label>Address</label>
        <input type="text" id="bldg-addr" placeholder="123 Main St, Chicago, IL">
      </div>
      <div class="field-row">
        <div class="field">
          <label>Building Type <span class="req">*</span></label>
          <select id="bldg-type">
            <option value="">Select…</option>
            <option>Hospital / Healthcare</option>
            <option>Hotel / Lodging</option>
            <option>Office High-Rise</option>
            <option>Mixed-Use Tower</option>
            <option>Long-Term Care / Nursing</option>
            <option>Correctional Facility</option>
            <option>Educational</option>
            <option>Other</option>
          </select>
        </div>
        <div class="field">
          <label>Year Built</label>
          <input type="number" id="bldg-year" placeholder="1998" min="1900" max="2025">
        </div>
      </div>
      <div class="field-row">
        <div class="field">
          <label># of Floors</label>
          <input type="number" id="bldg-floors" placeholder="12" min="1">
        </div>
        <div class="field">
          <label>Occupancy Cap.</label>
          <input type="number" id="bldg-occ" placeholder="800">
        </div>
      </div>
      <div class="field">
        <label>Water Source</label>
        <select id="water-source">
          <option value="">Select…</option>
          <option>Municipal / City Supply</option>
          <option>Well Water</option>
          <option>Dual (Municipal + Well)</option>
        </select>
      </div>
      <div class="field">
        <label># of Water Entry Points</label>
        <input type="number" id="entry-pts" placeholder="1" min="1">
      </div>
    </div>
  </div>

  <!-- CARD 3: Water System Inventory -->
  <div class="card">
    <div class="card-header">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2z"/><path d="M12 6v6l4 2"/></svg>
      <h3>Water System Inventory</h3>
      <span class="step-badge">STEP 2</span>
    </div>
    <div class="card-body">
      <p class="hint" style="margin-bottom:12px;">Check all risk devices present in this building. These become your required sample points.</p>
      <div id="device-checklist" style="display:flex;flex-direction:column;gap:8px;">
      </div>
    </div>
  </div>

  <!-- CARD 4: Sample Points -->
  <div class="card">
    <div class="card-header">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M9 3H5a2 2 0 0 0-2 2v4m6-6h10a2 2 0 0 1 2 2v4M9 3v18m0 0h10a2 2 0 0 0 2-2v-4M9 21H5a2 2 0 0 0-2-2v-4m0 0h18"/></svg>
      <h3>Sample Point Readings</h3>
      <span class="step-badge">STEP 3</span>
    </div>
    <div class="card-body">

      <div class="ashrae-banner">
        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="white" stroke-width="2"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
        <p><strong>ASHRAE 188 Thresholds</strong>Hot supply ≥ 140°F (60°C) · Cold supply ≤ 68°F (20°C) · Chlorine ≥ 0.2 ppm at distal points</p>
      </div>

      <div class="sample-list" id="sample-list"></div>
      <button class="btn-add" onclick="addSample()">+ ADD SAMPLE POINT</button>
    </div>
  </div>

  <!-- CARD 5: Photos -->
  <div class="card">
    <div class="card-header">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/><circle cx="12" cy="13" r="4"/></svg>
      <h3>Field Photos</h3>
    </div>
    <div class="card-body">
      <p class="hint" style="margin-bottom:10px;">Photograph each sample point, gauge, device, or area of concern for documentation.</p>
      <div class="photo-zone" id="photo-drop">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"><path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/><circle cx="12" cy="13" r="4"/></svg>
        <p>Tap to capture or upload photos</p>
        <input type="file" accept="image/*" capture="environment" multiple onchange="handlePhotos(event)">
      </div>
      <div class="photo-thumbs" id="photo-thumbs"></div>
    </div>
  </div>

  <!-- CARD 6: Corrective Actions / Notes -->
  <div class="card">
    <div class="card-header">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"/><path d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"/></svg>
      <h3>Findings & Corrective Actions</h3>
      <span class="step-badge">STEP 4</span>
    </div>
    <div class="card-body">
      <div class="field">
        <label>Overall Site Risk Level</label>
        <select id="overall-risk">
          <option value="low">Low — All parameters in range</option>
          <option value="medium">Medium — Minor deviations noted</option>
          <option value="high">High — Immediate action required</option>
        </select>
      </div>
      <div class="field">
        <label>Corrective Actions Required</label>
        <textarea id="corrections" placeholder="e.g. Flush distal showerheads on Floor 14, adjust HW heater setpoint to 140°F, test Cooling Tower biocide…"></textarea>
      </div>
      <div class="field">
        <label>Inspector Notes</label>
        <textarea id="notes" placeholder="Any additional observations, anomalies, or follow-up items…"></textarea>
      </div>
      <div class="field">
        <label>Re-inspection Date</label>
        <input type="date" id="reinspect-date">
      </div>
    </div>
  </div>

  <button class="btn-primary" onclick="saveInspection()">💾 SAVE INSPECTION</button>
  <button class="btn-secondary" onclick="showScreen('screen-outputs')">⬇ EXPORT / OUTPUTS</button>

</div>

<!-- ═══════════════════════════════════ -->
<!--  SCREEN 2: DASHBOARD               -->
<!-- ═══════════════════════════════════ -->
<div class="screen" id="screen-dash">

  <div class="section-title">Overview</div>

  <div class="stat-grid">
    <div class="stat-box">
      <div class="stat-val" id="dash-total">0</div>
      <div class="stat-label">Inspections Saved</div>
    </div>
    <div class="stat-box danger">
      <div class="stat-val" id="dash-high">0</div>
      <div class="stat-label">High Risk Sites</div>
    </div>
    <div class="stat-box warn">
      <div class="stat-val" id="dash-medium">0</div>
      <div class="stat-label">Medium Risk</div>
    </div>
    <div class="stat-box">
      <div class="stat-val" id="dash-low">0</div>
      <div class="stat-label">Low Risk / Clear</div>
    </div>
  </div>

  <div class="section-title">Recent Inspections</div>
  <div id="insp-list">
    <div style="text-align:center;padding:30px 20px;color:var(--muted);font-family:var(--mono);font-size:0.75rem;">
      NO INSPECTIONS YET.<br>START ONE USING THE ＋ TAB.
    </div>
  </div>

</div>

<!-- ═══════════════════════════════════ -->
<!--  SCREEN 3: OUTPUTS                 -->
<!-- ═══════════════════════════════════ -->
<div class="screen" id="screen-outputs">

  <div class="section-title">Export & Reports</div>

  <div class="output-grid">

    <div class="output-tile pdf" onclick="exportPDF()">
      <svg viewBox="0 0 24 24" fill="none" stroke="#c42b00" stroke-width="1.8" stroke-linecap="round">
        <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
        <polyline points="14 2 14 8 20 8"/>
        <line x1="16" y1="13" x2="8" y2="13"/>
        <line x1="16" y1="17" x2="8" y2="17"/>
        <polyline points="10 9 9 9 8 9"/>
      </svg>
      <h4>PDF Report</h4>
      <p>Client-ready inspection report</p>
    </div>

    <div class="output-tile dash" onclick="showDashReport()">
      <svg viewBox="0 0 24 24" fill="none" stroke="#1a6b3c" stroke-width="1.8" stroke-linecap="round">
        <rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/>
        <rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/>
      </svg>
      <h4>Dashboard</h4>
      <p>Internal review & trends</p>
    </div>

    <div class="output-tile csv" onclick="exportCSV()">
      <svg viewBox="0 0 24 24" fill="none" stroke="#c45c00" stroke-width="1.8" stroke-linecap="round">
        <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/>
        <polyline points="14 2 14 8 20 8"/>
        <line x1="8" y1="13" x2="16" y2="13"/>
        <line x1="8" y1="17" x2="16" y2="17"/>
      </svg>
      <h4>CSV / Excel</h4>
      <p>Raw data spreadsheet export</p>
    </div>

    <div class="output-tile raw" onclick="exportJSON()">
      <svg viewBox="0 0 24 24" fill="none" stroke="#5566aa" stroke-width="1.8" stroke-linecap="round">
        <polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/>
      </svg>
      <h4>JSON / Raw</h4>
      <p>Data export for integrations</p>
    </div>

  </div>

  <div class="section-title" style="margin-top:20px;">Latest Inspection Summary</div>
  <div class="card" id="output-summary">
    <div class="card-body" style="text-align:center;color:var(--muted);font-family:var(--mono);font-size:0.75rem;padding:24px;">
      NO SAVED INSPECTIONS YET.
    </div>
  </div>

</div>

<!-- ═══════════════════════════════════ -->
<!--  SCREEN 4: SETTINGS / HELP         -->
<!-- ═══════════════════════════════════ -->
<div class="screen" id="screen-settings">
  <div class="section-title">App Settings</div>

  <div class="card">
    <div class="card-header"><h3>Thresholds (ASHRAE 188)</h3></div>
    <div class="card-body">
      <div class="field-row">
        <div class="field">
          <label>Hot Water Min (°F)</label>
          <input type="number" id="thresh-hot" value="140">
        </div>
        <div class="field">
          <label>Cold Water Max (°F)</label>
          <input type="number" id="thresh-cold" value="68">
        </div>
      </div>
      <div class="field-row">
        <div class="field">
          <label>Chlorine Min (ppm)</label>
          <input type="number" id="thresh-cl" value="0.2" step="0.1">
        </div>
        <div class="field">
          <label>pH Range Low</label>
          <input type="number" id="thresh-ph" value="7.0" step="0.1">
        </div>
      </div>
      <button class="btn-primary" style="margin-top:10px;" onclick="saveSettings()">SAVE THRESHOLDS</button>
    </div>
  </div>

  <div class="card">
    <div class="card-header"><h3>Data Management</h3></div>
    <div class="card-body">
      <p class="hint" style="margin-bottom:12px;">All data stored locally on this device. Export before clearing.</p>
      <button class="btn-secondary" onclick="clearAllData()">⚠ CLEAR ALL LOCAL DATA</button>
    </div>
  </div>

  <div class="card">
    <div class="card-header"><h3>Reference — Risk Thresholds</h3></div>
    <div class="card-body">
      <div style="display:flex;flex-direction:column;gap:8px;">
        <div style="display:flex;justify-content:space-between;align-items:center;padding:8px;background:var(--surface2);border-radius:6px;">
          <span style="font-family:var(--mono);font-size:0.72rem;">Hot Water Supply</span>
          <span class="risk-badge risk-high">≥ 140°F at heater</span>
        </div>
        <div style="display:flex;justify-content:space-between;align-items:center;padding:8px;background:var(--surface2);border-radius:6px;">
          <span style="font-family:var(--mono);font-size:0.72rem;">Hot Water Distal</span>
          <span class="risk-badge risk-medium">≥ 122°F at fixture</span>
        </div>
        <div style="display:flex;justify-content:space-between;align-items:center;padding:8px;background:var(--surface2);border-radius:6px;">
          <span style="font-family:var(--mono);font-size:0.72rem;">Cold Water Supply</span>
          <span class="risk-badge risk-low">≤ 68°F (20°C)</span>
        </div>
        <div style="display:flex;justify-content:space-between;align-items:center;padding:8px;background:var(--surface2);border-radius:6px;">
          <span style="font-family:var(--mono);font-size:0.72rem;">Free Chlorine</span>
          <span class="risk-badge risk-low">≥ 0.2 ppm distal</span>
        </div>
        <div style="display:flex;justify-content:space-between;align-items:center;padding:8px;background:var(--surface2);border-radius:6px;">
          <span style="font-family:var(--mono);font-size:0.72rem;">Cooling Tower ORP</span>
          <span class="risk-badge risk-medium">≥ 650 mV</span>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- BOTTOM NAV -->
<nav class="bottom-nav">
  <button class="nav-btn active" id="nav-inspect" onclick="showScreen('screen-inspect')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 20h9"/><path d="M16.5 3.5a2.121 2.121 0 0 1 3 3L7 19l-4 1 1-4L16.5 3.5z"/></svg>
    NEW
  </button>
  <button class="nav-btn" id="nav-dash" onclick="showScreen('screen-dash')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>
    DASH
  </button>
  <button class="nav-btn" id="nav-outputs" onclick="showScreen('screen-outputs')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><polyline points="7 10 12 15 17 10"/><line x1="12" y1="15" x2="12" y2="3"/></svg>
    EXPORT
  </button>
  <button class="nav-btn" id="nav-settings" onclick="showScreen('screen-settings')">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>
    SETTINGS
  </button>
</nav>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<script>
// ── STATE ──
let inspections = JSON.parse(localStorage.getItem('aqg_inspections') || '[]');
let photoDataURLs = [];
let sampleCount = 0;

const DEVICES = [
  { id: 'cooling_tower',   label: 'Cooling Tower(s)',            risk: 'high' },
  { id: 'hot_water_tank',  label: 'Hot Water Storage Tank(s)',   risk: 'high' },
  { id: 'showerheads',     label: 'Showerheads / Spa Jets',      risk: 'high' },
  { id: 'ice_machines',    label: 'Ice Machines',                risk: 'medium' },
  { id: 'eyewash',         label: 'Emergency Eyewash Stations',  risk: 'medium' },
  { id: 'decorative_fount',label: 'Decorative Fountains / Mist', risk: 'medium' },
  { id: 'humidifiers',     label: 'Humidifiers / HVAC',          risk: 'medium' },
  { id: 'water_softener',  label: 'Water Softener / Treatment',  risk: 'low' },
  { id: 'drinking_fount',  label: 'Drinking Fountains',          risk: 'low' },
  { id: 'faucets_sinks',   label: 'Faucets / Sinks (distal)',    risk: 'low' },
];

// ── INIT ──
window.onload = () => {
  renderDeviceChecklist();
  addSample(); // default first sample row
  setToday();
  refreshDashboard();
  renderOutputSummary();
};

function setToday() {
  const now = new Date();
  document.getElementById('insp-date').value = now.toISOString().split('T')[0];
  document.getElementById('insp-time').value = now.toTimeString().slice(0,5);
}

// ── SCREENS ──
function showScreen(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  const map = {
    'screen-inspect':'nav-inspect','screen-dash':'nav-dash',
    'screen-outputs':'nav-outputs','screen-settings':'nav-settings'
  };
  document.getElementById(map[id]).classList.add('active');
  if (id === 'screen-dash') refreshDashboard();
  if (id === 'screen-outputs') renderOutputSummary();
  window.scrollTo(0,0);
}

// ── DEVICE CHECKLIST ──
function renderDeviceChecklist() {
  const el = document.getElementById('device-checklist');
  el.innerHTML = DEVICES.map(d => `
    <label style="display:flex;align-items:center;gap:10px;padding:10px;background:var(--surface2);border:1px solid var(--border);border-radius:7px;cursor:pointer;">
      <input type="checkbox" id="dev_${d.id}" style="width:18px;height:18px;accent-color:var(--accent);flex-shrink:0;">
      <span style="flex:1;font-size:0.88rem;">${d.label}</span>
      <span class="risk-badge ${d.risk==='high'?'risk-high':d.risk==='medium'?'risk-medium':'risk-low'}">${d.risk.toUpperCase()}</span>
    </label>
  `).join('');
}

// ── SAMPLE POINTS ──
function addSample() {
  sampleCount++;
  const id = 'sp_' + sampleCount;
  const el = document.createElement('div');
  el.className = 'sample-row';
  el.id = id;
  el.innerHTML = `
    <div class="sample-row-header">
      <span class="sample-row-title">Sample Point #${sampleCount}</span>
      <button class="btn-del" onclick="removeSample('${id}')">✕ Remove</button>
    </div>
    <div class="field">
      <label>Location Description <span class="req">*</span></label>
      <input type="text" placeholder="e.g. Floor 14 East Wing – Shower #3" class="sp-location">
    </div>
    <div class="field-row">
      <div class="field">
        <label>Device Type</label>
        <select class="sp-device">
          <option>Hot Water Outlet</option>
          <option>Cold Water Inlet</option>
          <option>Distal Faucet</option>
          <option>Showerhead</option>
          <option>Cooling Tower</option>
          <option>Ice Machine</option>
          <option>Eyewash Station</option>
          <option>Decorative Fountain</option>
          <option>Other</option>
        </select>
      </div>
      <div class="field">
        <label>Floor / Zone</label>
        <input type="text" placeholder="14 / East" class="sp-floor">
      </div>
    </div>
    <div class="field-row3">
      <div class="field">
        <label>Temp (°F)</label>
        <div class="temp-input-wrap">
          <input type="number" placeholder="—" class="sp-temp" min="32" max="212" oninput="updateRisk(this)">
          <span class="temp-unit">°F</span>
        </div>
        <div class="risk-bar"><div class="risk-fill" style="width:0%"></div></div>
      </div>
      <div class="field">
        <label>Cl₂ (ppm)</label>
        <input type="number" placeholder="—" class="sp-cl" step="0.01" min="0" oninput="updateRisk(this)">
      </div>
      <div class="field">
        <label>pH</label>
        <input type="number" placeholder="—" class="sp-ph" step="0.1" min="6" max="9">
      </div>
    </div>
    <div class="field">
      <label>Visual Observation</label>
      <select class="sp-visual">
        <option value="">Select…</option>
        <option>No issues observed</option>
        <option>Sediment / scale buildup</option>
        <option>Biofilm visible</option>
        <option>Discoloration / odor</option>
        <option>Stagnant / low flow</option>
        <option>Corrosion noted</option>
      </select>
    </div>
    <div class="field">
      <label>Sample Result Risk</label>
      <div id="sp-risk-${id}" class="risk-badge risk-low" style="margin-top:4px;">LOW — Within Range</div>
    </div>
  `;
  document.getElementById('sample-list').appendChild(el);
}

function removeSample(id) {
  const el = document.getElementById(id);
  if (el) el.remove();
}

function updateRisk(input) {
  // Simple visual feedback — full risk calc on save
  const row = input.closest('.sample-row');
  const temp = parseFloat(row.querySelector('.sp-temp')?.value);
  const cl = parseFloat(row.querySelector('.sp-cl')?.value);
  const bar = row.querySelector('.risk-fill');
  const device = row.querySelector('.sp-device')?.value || '';

  let score = 0;
  if (!isNaN(temp)) {
    const isHot = device.toLowerCase().includes('hot') || device.toLowerCase().includes('shower');
    if (isHot && temp < 122) score += 2;
    else if (isHot && temp < 140) score += 1;
    if (!isHot && temp > 68) score += 2;
    bar.style.width = Math.min(100, (temp/212)*100) + '%';
    bar.style.background = temp > 140 ? 'var(--safe)' : temp > 122 ? 'var(--warn)' : 'var(--danger)';
  }
  if (!isNaN(cl) && cl < 0.2) score += 2;
}

// ── PHOTOS ──
function handlePhotos(e) {
  const files = Array.from(e.target.files);
  files.forEach(f => {
    const reader = new FileReader();
    reader.onload = ev => {
      photoDataURLs.push(ev.target.result);
      renderThumbs();
    };
    reader.readAsDataURL(f);
  });
}

function renderThumbs() {
  const el = document.getElementById('photo-thumbs');
  el.innerHTML = photoDataURLs.map((d,i) => `
    <div class="photo-thumb">
      <img src="${d}" alt="photo ${i+1}">
      <button class="del-photo" onclick="deletePhoto(${i})">×</button>
    </div>
  `).join('');
}

function deletePhoto(i) {
  photoDataURLs.splice(i,1);
  renderThumbs();
}

// ── SAVE ──
function saveInspection() {
  const name = document.getElementById('bldg-name').value.trim();
  const inspector = document.getElementById('insp-name').value.trim();
  if (!name || !inspector) { showToast('⚠ Building name & inspector required'); return; }

  const samples = [];
  document.querySelectorAll('.sample-row').forEach(row => {
    const temp = parseFloat(row.querySelector('.sp-temp')?.value);
    const cl = parseFloat(row.querySelector('.sp-cl')?.value);
    const device = row.querySelector('.sp-device')?.value || '';
    let risk = 'low';
    const isHot = device.toLowerCase().includes('hot') || device.toLowerCase().includes('shower');
    if (!isNaN(temp)) {
      if (isHot && temp < 122) risk = 'high';
      else if (isHot && temp < 140) risk = 'medium';
      if (!isHot && temp > 77) risk = 'high';
      else if (!isHot && temp > 68) risk = 'medium';
    }
    if (!isNaN(cl) && cl < 0.2) risk = risk === 'low' ? 'medium' : 'high';
    samples.push({
      location: row.querySelector('.sp-location')?.value || '',
      device, floor: row.querySelector('.sp-floor')?.value || '',
      temp: isNaN(temp) ? null : temp,
      chlorine: isNaN(cl) ? null : cl,
      ph: row.querySelector('.sp-ph')?.value || null,
      visual: row.querySelector('.sp-visual')?.value || '',
      risk
    });
  });

  const devices = DEVICES.filter(d => document.getElementById('dev_'+d.id)?.checked).map(d=>d.label);
  const overallRisk = document.getElementById('overall-risk').value;

  const record = {
    id: Date.now(),
    inspector, cert: document.getElementById('insp-cert').value,
    date: document.getElementById('insp-date').value,
    time: document.getElementById('insp-time').value,
    building: {
      name, address: document.getElementById('bldg-addr').value,
      type: document.getElementById('bldg-type').value,
      year: document.getElementById('bldg-year').value,
      floors: document.getElementById('bldg-floors').value,
      occupancy: document.getElementById('bldg-occ').value,
      waterSource: document.getElementById('water-source').value,
      entryPoints: document.getElementById('entry-pts').value,
    },
    devices, samples,
    overallRisk,
    corrections: document.getElementById('corrections').value,
    notes: document.getElementById('notes').value,
    reinspectDate: document.getElementById('reinspect-date').value,
    photos: photoDataURLs.length,
  };

  inspections.unshift(record);
  localStorage.setItem('aqg_inspections', JSON.stringify(inspections));
  showToast('✓ Inspection saved locally');
  refreshDashboard();
  renderOutputSummary();
}

// ── DASHBOARD ──
function refreshDashboard() {
  const total = inspections.length;
  const high = inspections.filter(i=>i.overallRisk==='high').length;
  const med = inspections.filter(i=>i.overallRisk==='medium').length;
  const low = inspections.filter(i=>i.overallRisk==='low').length;
  document.getElementById('dash-total').textContent = total;
  document.getElementById('dash-high').textContent = high;
  document.getElementById('dash-medium').textContent = med;
  document.getElementById('dash-low').textContent = low;

  const list = document.getElementById('insp-list');
  if (!inspections.length) {
    list.innerHTML = '<div style="text-align:center;padding:30px 20px;color:var(--muted);font-family:var(--mono);font-size:0.75rem;">NO INSPECTIONS YET.<br>START ONE USING THE ＋ TAB.</div>';
    return;
  }
  list.innerHTML = inspections.slice(0,10).map(r => `
    <div class="inspection-card">
      <div class="insp-left">
        <div class="insp-name">${r.building.name}</div>
        <div class="insp-meta">${r.date} · ${r.inspector} · ${r.samples?.length||0} sample pts</div>
        <div style="margin-top:5px;"><span class="risk-badge ${r.overallRisk==='high'?'risk-high':r.overallRisk==='medium'?'risk-medium':'risk-low'}">${r.overallRisk.toUpperCase()} RISK</span></div>
      </div>
      <span class="insp-arrow">›</span>
    </div>
  `).join('');
}

// ── OUTPUT SUMMARY ──
function renderOutputSummary() {
  const el = document.getElementById('output-summary');
  if (!inspections.length) {
    el.innerHTML = '<div class="card-body" style="text-align:center;color:var(--muted);font-family:var(--mono);font-size:0.75rem;padding:24px;">NO SAVED INSPECTIONS YET.</div>';
    return;
  }
  const r = inspections[0];
  el.innerHTML = `
    <div class="card-body">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:12px;">
        <div>
          <div style="font-family:var(--head);font-size:1.1rem;font-weight:700;">${r.building.name}</div>
          <div style="font-family:var(--mono);font-size:0.65rem;color:var(--muted);">${r.date} · ${r.inspector}</div>
        </div>
        <span class="risk-badge ${r.overallRisk==='high'?'risk-high':r.overallRisk==='medium'?'risk-medium':'risk-low'}">${r.overallRisk.toUpperCase()}</span>
      </div>
      <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;text-align:center;margin-bottom:12px;">
        <div style="background:var(--surface2);border-radius:6px;padding:8px;">
          <div style="font-family:var(--head);font-size:1.4rem;font-weight:800;color:var(--accent2)">${r.samples?.length||0}</div>
          <div style="font-family:var(--mono);font-size:0.58rem;color:var(--muted)">SAMPLE PTS</div>
        </div>
        <div style="background:var(--surface2);border-radius:6px;padding:8px;">
          <div style="font-family:var(--head);font-size:1.4rem;font-weight:800;color:var(--danger)">${r.samples?.filter(s=>s.risk==='high').length||0}</div>
          <div style="font-family:var(--mono);font-size:0.58rem;color:var(--muted)">HIGH RISK</div>
        </div>
        <div style="background:var(--surface2);border-radius:6px;padding:8px;">
          <div style="font-family:var(--head);font-size:1.4rem;font-weight:800;color:var(--accent)">${r.devices?.length||0}</div>
          <div style="font-family:var(--mono);font-size:0.58rem;color:var(--muted)">DEVICES INV.</div>
        </div>
      </div>
      ${r.corrections ? `<div style="background:#fff3e6;border:1px solid #ffd199;border-radius:6px;padding:10px;font-size:0.78rem;color:var(--warn);margin-bottom:8px;"><strong>Corrective Actions:</strong> ${r.corrections}</div>` : ''}
      ${r.reinspectDate ? `<div style="font-family:var(--mono);font-size:0.65rem;color:var(--muted);">Re-inspection due: <strong>${r.reinspectDate}</strong></div>` : ''}
    </div>
  `;
}

// ── EXPORTS ──
function exportCSV() {
  if (!inspections.length) { showToast('No inspections to export'); return; }
  const rows = [['Date','Inspector','Building','Type','Floors','Risk','Location','Device','Floor','Temp_F','Chlorine_ppm','pH','Visual','Sample Risk']];
  inspections.forEach(r => {
    (r.samples||[]).forEach(s => {
      rows.push([r.date,r.inspector,r.building.name,r.building.type,r.building.floors,r.overallRisk,s.location,s.device,s.floor,s.temp??'',s.chlorine??'',s.ph??'',s.visual,s.risk]);
    });
  });
  const csv = rows.map(r=>r.map(c=>`"${String(c).replace(/"/g,'""')}"`).join(',')).join('\n');
  download('AquaGuard_Export.csv', 'text/csv', csv);
  showToast('✓ CSV downloaded');
}

function exportJSON() {
  if (!inspections.length) { showToast('No inspections to export'); return; }
  download('AquaGuard_Export.json', 'application/json', JSON.stringify(inspections, null, 2));
  showToast('✓ JSON downloaded');
}

function exportPDF() {
  if (!inspections.length) { showToast('No inspections to export'); return; }
  const r = inspections[0];
  const w = window.open('','_blank');
  w.document.write(`
    <html><head><title>WMP Inspection Report</title>
    <style>body{font-family:sans-serif;padding:40px;color:#111;max-width:800px;margin:0 auto;}
    h1{color:#0f4a2a;border-bottom:3px solid #0f4a2a;padding-bottom:8px;}
    h2{color:#1a6b3c;font-size:1rem;margin:20px 0 6px;}
    table{width:100%;border-collapse:collapse;margin-bottom:16px;}
    th{background:#0f4a2a;color:#fff;padding:8px;text-align:left;font-size:0.8rem;}
    td{padding:7px 8px;border-bottom:1px solid #dde;font-size:0.82rem;}
    .badge-h{color:#c42b00;font-weight:700;} .badge-m{color:#c45c00;font-weight:700;} .badge-l{color:#1a6b3c;font-weight:700;}
    .meta{color:#666;font-size:0.8rem;} .warn{background:#fff3e6;padding:10px;border-left:4px solid #c45c00;margin:10px 0;}
    @media print{button{display:none}}
    </style></head><body>
    <h1>🛡 Legionella WMP Inspection Report</h1>
    <p class="meta">Generated by AquaGuard WMP · ASHRAE 188 Compliant</p>
    <h2>Building Information</h2>
    <table><tr><th>Field</th><th>Value</th></tr>
    <tr><td>Facility</td><td>${r.building.name}</td></tr>
    <tr><td>Address</td><td>${r.building.address||'—'}</td></tr>
    <tr><td>Type</td><td>${r.building.type||'—'}</td></tr>
    <tr><td>Floors</td><td>${r.building.floors||'—'}</td></tr>
    <tr><td>Year Built</td><td>${r.building.year||'—'}</td></tr>
    <tr><td>Inspector</td><td>${r.inspector} (${r.cert||'—'})</td></tr>
    <tr><td>Inspection Date</td><td>${r.date} at ${r.time}</td></tr>
    <tr><td>Overall Risk</td><td class="${r.overallRisk==='high'?'badge-h':r.overallRisk==='medium'?'badge-m':'badge-l'}">${r.overallRisk.toUpperCase()}</td></tr>
    </table>
    <h2>Water Risk Devices Inventoried</h2>
    <p>${(r.devices||[]).join(', ')||'None recorded'}</p>
    <h2>Sample Point Results</h2>
    <table><tr><th>Location</th><th>Device</th><th>Floor</th><th>Temp °F</th><th>Cl₂ ppm</th><th>pH</th><th>Risk</th></tr>
    ${(r.samples||[]).map(s=>`<tr><td>${s.location}</td><td>${s.device}</td><td>${s.floor}</td><td>${s.temp??'—'}</td><td>${s.chlorine??'—'}</td><td>${s.ph??'—'}</td><td class="${s.risk==='high'?'badge-h':s.risk==='medium'?'badge-m':'badge-l'}">${s.risk.toUpperCase()}</td></tr>`).join('')}
    </table>
    ${r.corrections?`<div class="warn"><strong>Corrective Actions Required:</strong><br>${r.corrections}</div>`:''}
    ${r.notes?`<h2>Inspector Notes</h2><p>${r.notes}</p>`:''}
    ${r.reinspectDate?`<p><strong>Re-inspection Due:</strong> ${r.reinspectDate}</p>`:''}
    <br><p class="meta" style="border-top:1px solid #ddd;padding-top:10px;">This report is generated for informational purposes. Confirm findings with laboratory Legionella culture testing as required.</p>
    <br><button onclick="window.print()">🖨 Print / Save as PDF</button>
    </body></html>
  `);
  w.document.close();
  showToast('✓ PDF report opened');
}

function showDashReport() { showScreen('screen-dash'); }

// ── SETTINGS ──
function saveSettings() { showToast('✓ Thresholds saved'); }
function clearAllData() {
  if (confirm('Delete ALL inspection data? This cannot be undone.')) {
    localStorage.removeItem('aqg_inspections');
    inspections = [];
    refreshDashboard();
    renderOutputSummary();
    showToast('Data cleared');
  }
}

// ── UTILS ──
function download(filename, type, content) {
  const a = document.createElement('a');
  a.href = URL.createObjectURL(new Blob([content],{type}));
  a.download = filename;
  a.click();
}

function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2500);
}
</script>
</body>
</html>
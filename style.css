:root {
  --bg: #F7F1F6;
  --surface: #FFFFFF;
  --surface-alt: #FBF4F9;
  --ink: #2E1A38;
  --ink-muted: #8A7893;
  --border: #EADFE8;
  --berry: #C4405A;
  --berry-soft: #F4CBD3;
  --berry-ghost: #FBEAEE;
  --violet: #6C63AC;
  --violet-soft: #DCD8F0;
  --violet-ghost: #EEECF8;
  --today-ring: #2E1A38;
  --shadow: 0 12px 30px -18px rgba(46, 26, 56, 0.35);
  --radius: 18px;
  --font-display: "Fraunces", "Iowan Old Style", "Palatino Linotype", serif;
  --font-body: "Sora", -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

[data-theme="dark"] {
  --bg: #1B1420;
  --surface: #241A2C;
  --surface-alt: #2B2033;
  --ink: #F3EDF3;
  --ink-muted: #AB9AB5;
  --border: #392C42;
  --berry: #E17D91;
  --berry-soft: #4B2733;
  --berry-ghost: #33212A;
  --violet: #AFA3E8;
  --violet-soft: #362C55;
  --violet-ghost: #2A2440;
  --today-ring: #F3EDF3;
  --shadow: 0 12px 30px -16px rgba(0, 0, 0, 0.55);
}

* { box-sizing: border-box; }

body {
  margin: 0;
  background: var(--bg);
  color: var(--ink);
  font-family: var(--font-body);
  -webkit-font-smoothing: antialiased;
  transition: background .25s ease, color .25s ease;
}

.app {
  max-width: 640px;
  margin: 0 auto;
  padding: 20px 16px 48px;
}

.topbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}

.brand {
  font-family: var(--font-display);
  font-size: 1.5rem;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 8px;
  letter-spacing: 0.01em;
}
.brand-mark { color: var(--violet); font-size: 1.3rem; }

.topbar-actions { display: flex; gap: 6px; }

.icon-btn {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  border: 1px solid var(--border);
  background: var(--surface);
  color: var(--ink);
  font-size: 1.05rem;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition: background .15s ease, transform .1s ease;
}
.icon-btn:hover { background: var(--surface-alt); }
.icon-btn:active { transform: scale(0.94); }

.link-btn {
  border: none;
  background: none;
  color: var(--violet);
  font-family: var(--font-body);
  font-size: 0.82rem;
  text-decoration: underline;
  cursor: pointer;
  padding: 0;
}

.card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  box-shadow: var(--shadow);
  padding: 18px;
}

.dashboard {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
  margin-bottom: 14px;
}
@media (max-width: 480px) {
  .dashboard { grid-template-columns: 1fr; }
}

.wheel-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 4px;
}
#cycleWheel { width: 100%; max-width: 190px; height: auto; }
.wheel-caption { text-align: center; margin-top: -4px; }
.wheel-day {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-weight: 600;
}
.wheel-phase {
  font-size: 0.8rem;
  color: var(--ink-muted);
  text-transform: uppercase;
  letter-spacing: 0.06em;
}

.stats-card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 14px;
}
.stat { text-align: left; }
.stat-value {
  display: block;
  font-family: var(--font-display);
  font-size: 1.7rem;
  font-weight: 600;
  color: var(--berry);
}
.stat-label {
  display: block;
  font-size: 0.78rem;
  color: var(--ink-muted);
}
.stat-row { display: flex; justify-content: space-between; gap: 8px; }
.stat-mini { display: flex; flex-direction: column; }
.stat-mini-value { font-weight: 600; font-size: 1rem; }
.stat-mini-label { font-size: 0.7rem; color: var(--ink-muted); }

.calendar-card { margin-bottom: 14px; }

.calendar-nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
}
.calendar-nav-center { text-align: center; }
.calendar-nav h2 {
  font-family: var(--font-display);
  font-weight: 600;
  font-size: 1.15rem;
  margin: 0;
  text-transform: capitalize;
}

.weekdays {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  text-align: center;
  font-size: 0.72rem;
  color: var(--ink-muted);
  margin-bottom: 4px;
}

.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 4px;
}

.day-cell {
  position: relative;
  aspect-ratio: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 12px;
  font-size: 0.85rem;
  cursor: pointer;
  background: transparent;
  border: none;
  color: var(--ink);
  font-family: var(--font-body);
}
.day-cell.outside { color: var(--border); cursor: default; }
.day-cell.today { box-shadow: inset 0 0 0 2px var(--today-ring); font-weight: 700; }

.day-cell.period { background: var(--berry); color: #fff; font-weight: 600; }
.day-cell.period-predicted {
  background: var(--berry-ghost);
  color: var(--berry);
  border: 1.5px dashed var(--berry-soft);
}
.day-cell.fertile { background: var(--violet-ghost); color: var(--violet); }
.day-cell.ovulation { background: var(--violet); color: #fff; font-weight: 700; }
.day-cell.ovulation-predicted {
  background: var(--violet-ghost);
  color: var(--violet);
  border: 1.5px dashed var(--violet-soft);
  font-weight: 700;
}

.legend {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 12px;
  font-size: 0.72rem;
  color: var(--ink-muted);
}
.legend-item { display: flex; align-items: center; gap: 5px; }
.dot { width: 9px; height: 9px; border-radius: 50%; display: inline-block; }
.dot-period { background: var(--berry); }
.dot-period-predicted { background: var(--berry-ghost); border: 1.5px dashed var(--berry-soft); }
.dot-fertile { background: var(--violet-ghost); }
.dot-ovulation { background: var(--violet); }

.journal-card { margin-bottom: 14px; }
.journal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 12px;
}
.journal-header h2 {
  font-family: var(--font-display);
  font-size: 1.1rem;
  margin: 0;
}

.btn-primary {
  background: var(--berry);
  color: #fff;
  border: none;
  border-radius: 999px;
  padding: 9px 16px;
  font-family: var(--font-body);
  font-weight: 600;
  font-size: 0.85rem;
  cursor: pointer;
}
.btn-secondary {
  background: transparent;
  color: var(--ink);
  border: 1px solid var(--border);
  border-radius: 999px;
  padding: 9px 16px;
  font-family: var(--font-body);
  font-weight: 600;
  font-size: 0.85rem;
  cursor: pointer;
}
.btn-danger {
  background: transparent;
  color: var(--berry);
  border: 1px solid var(--berry-soft);
  border-radius: 999px;
  padding: 9px 16px;
  font-family: var(--font-body);
  font-weight: 600;
  font-size: 0.85rem;
  cursor: pointer;
}

.journal-list { list-style: none; margin: 0; padding: 0; display: flex; flex-direction: column; gap: 8px; }
.journal-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 12px;
  border: 1px solid var(--border);
  border-radius: 12px;
  cursor: pointer;
  background: var(--surface-alt);
}
.journal-item:hover { border-color: var(--berry-soft); }
.journal-item-dates { font-weight: 600; font-size: 0.9rem; }
.journal-item-meta { font-size: 0.75rem; color: var(--ink-muted); margin-top: 2px; }
.journal-item-length { font-size: 0.78rem; color: var(--violet); font-weight: 600; white-space: nowrap; }

.empty-hint { color: var(--ink-muted); font-size: 0.85rem; text-align: center; padding: 8px 0; }
.hidden { display: none !important; }

.privacy-note {
  font-size: 0.72rem;
  color: var(--ink-muted);
  text-align: center;
  line-height: 1.5;
  margin-top: 20px;
}

/* Modales */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(20, 12, 24, 0.45);
  display: flex;
  align-items: flex-end;
  justify-content: center;
  z-index: 100;
  backdrop-filter: blur(2px);
}
@media (min-width: 560px) {
  .modal-overlay { align-items: center; }
}
.modal {
  background: var(--surface);
  border-radius: 20px 20px 0 0;
  width: 100%;
  max-width: 480px;
  max-height: 90vh;
  overflow-y: auto;
  padding: 20px;
  box-shadow: var(--shadow);
}
@media (min-width: 560px) {
  .modal { border-radius: 20px; }
}
.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 14px;
}
.modal-header h3 {
  font-family: var(--font-display);
  font-size: 1.2rem;
  margin: 0;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 5px;
  margin-bottom: 14px;
  font-size: 0.85rem;
}
.field span { color: var(--ink-muted); font-size: 0.78rem; }
.field em { font-style: normal; opacity: 0.75; }
.field input, .field select, .field textarea {
  font-family: var(--font-body);
  font-size: 0.95rem;
  padding: 10px 12px;
  border-radius: 10px;
  border: 1px solid var(--border);
  background: var(--surface-alt);
  color: var(--ink);
}
.checkbox-field { flex-direction: row; align-items: center; }
.checkbox-field input { width: auto; }

.chip-group { display: flex; flex-wrap: wrap; gap: 6px; }
.chip {
  border: 1px solid var(--border);
  background: var(--surface-alt);
  color: var(--ink-muted);
  border-radius: 999px;
  padding: 6px 12px;
  font-size: 0.78rem;
  cursor: pointer;
  font-family: var(--font-body);
}
.chip.active { background: var(--violet); border-color: var(--violet); color: #fff; }

.modal-actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 6px;
  gap: 8px;
}
.modal-actions-right { display: flex; gap: 8px; margin-left: auto; }

.toast {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  background: var(--ink);
  color: var(--bg);
  padding: 10px 18px;
  border-radius: 999px;
  font-size: 0.82rem;
  box-shadow: var(--shadow);
  z-index: 200;
}

@media (prefers-reduced-motion: reduce) {
  * { transition: none !important; }
}

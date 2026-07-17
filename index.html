/* ============================================================
   Lunaire — suivi de cycle
   Toutes les données restent en localStorage, sur cet appareil.
   ============================================================ */

const STORAGE_KEY = 'lunaire_cycles_v1';
const SETTINGS_KEY = 'lunaire_settings_v1';

const DEFAULT_SETTINGS = {
  defaultCycleLength: 28,
  defaultPeriodLength: 5,
  defaultLutealLength: 14,
  cyclesToAverage: 6,
  darkMode: false
};

/* ---------- Stockage ---------- */

function loadCycles() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    return raw ? JSON.parse(raw) : [];
  } catch (e) {
    console.error('Erreur de lecture des cycles', e);
    return [];
  }
}

function saveCycles(cycles) {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(cycles));
}

function loadSettings() {
  try {
    const raw = localStorage.getItem(SETTINGS_KEY);
    return raw ? { ...DEFAULT_SETTINGS, ...JSON.parse(raw) } : { ...DEFAULT_SETTINGS };
  } catch (e) {
    return { ...DEFAULT_SETTINGS };
  }
}

function saveSettings(settings) {
  localStorage.setItem(SETTINGS_KEY, JSON.stringify(settings));
}

let cycles = loadCycles();
let settings = loadSettings();

/* ---------- Utilitaires de dates (tout en heure locale, format YYYY-MM-DD) ---------- */

function toISO(date) {
  const y = date.getFullYear();
  const m = String(date.getMonth() + 1).padStart(2, '0');
  const d = String(date.getDate()).padStart(2, '0');
  return `${y}-${m}-${d}`;
}

function fromISO(str) {
  const [y, m, d] = str.split('-').map(Number);
  return new Date(y, m - 1, d);
}

function addDays(date, n) {
  const d = new Date(date);
  d.setDate(d.getDate() + n);
  return d;
}

function daysBetween(a, b) {
  const MS = 24 * 60 * 60 * 1000;
  const da = new Date(a.getFullYear(), a.getMonth(), a.getDate());
  const db = new Date(b.getFullYear(), b.getMonth(), b.getDate());
  return Math.round((db - da) / MS);
}

function isSameDay(a, b) {
  return a.getFullYear() === b.getFullYear() && a.getMonth() === b.getMonth() && a.getDate() === b.getDate();
}

const MONTHS_FR = ['janvier','février','mars','avril','mai','juin','juillet','août','septembre','octobre','novembre','décembre'];

/* ============================================================
   Moteur de prédiction
   ============================================================ */

function sortedCycles() {
  return [...cycles].sort((a, b) => fromISO(a.periodStart) - fromISO(b.periodStart));
}

// Longueurs de cycle observées (écart entre débuts de règles consécutifs)
function observedCycleLengths() {
  const list = sortedCycles();
  const lengths = [];
  for (let i = 1; i < list.length; i++) {
    lengths.push(daysBetween(fromISO(list[i - 1].periodStart), fromISO(list[i].periodStart)));
  }
  return lengths;
}

function recentAverage(arr, n) {
  if (!arr.length) return null;
  const slice = arr.slice(-n);
  return slice.reduce((a, b) => a + b, 0) / slice.length;
}

function computeAvgCycleLength() {
  const lengths = observedCycleLengths();
  const avg = recentAverage(lengths, settings.cyclesToAverage);
  return avg ? Math.round(avg * 10) / 10 : settings.defaultCycleLength;
}

function computeAvgPeriodLength() {
  const lengths = cycles
    .filter(c => c.periodEnd)
    .map(c => daysBetween(fromISO(c.periodStart), fromISO(c.periodEnd)) + 1);
  const avg = recentAverage(lengths, settings.cyclesToAverage);
  return avg ? Math.round(avg * 10) / 10 : settings.defaultPeriodLength;
}

// Phase lutéale = temps entre l'ovulation d'un cycle et le début des règles suivantes
function computeAvgLutealLength() {
  const list = sortedCycles();
  const lengths = [];
  for (let i = 0; i < list.length - 1; i++) {
    if (list[i].ovulationDate) {
      const l = daysBetween(fromISO(list[i].ovulationDate), fromISO(list[i + 1].periodStart));
      if (l > 5 && l < 25) lengths.push(l);
    }
  }
  const avg = recentAverage(lengths, settings.cyclesToAverage);
  return avg ? Math.round(avg * 10) / 10 : settings.defaultLutealLength;
}

function cycleLengthRegularity() {
  const lengths = observedCycleLengths().slice(-settings.cyclesToAverage);
  if (lengths.length < 2) return null;
  const avg = lengths.reduce((a, b) => a + b, 0) / lengths.length;
  const variance = lengths.reduce((a, b) => a + (b - avg) ** 2, 0) / lengths.length;
  return Math.round(Math.sqrt(variance) * 10) / 10;
}

/**
 * Construit la liste des cycles "enrichis" : les cycles réels (avec leurs
 * données saisies) suivis d'autant de cycles prédits que nécessaire pour
 * couvrir la date `untilDate`. Recalculé à chaque appel — pas de limite
 * de durée figée.
 */
function buildTimeline(untilDate) {
  const avgCycle = computeAvgCycleLength();
  const avgPeriod = computeAvgPeriodLength();
  const avgLuteal = computeAvgLutealLength();
  const list = sortedCycles();

  const timeline = list.map((c, i) => {
    const start = fromISO(c.periodStart);
    const end = c.periodEnd ? fromISO(c.periodEnd) : addDays(start, Math.round(avgPeriod) - 1);
    let ovulation = c.ovulationDate ? fromISO(c.ovulationDate) : null;
    if (!ovulation) {
      // Estime l'ovulation à partir du début des règles suivantes si connu, sinon via la moyenne
      const next = list[i + 1];
      if (next) {
        ovulation = addDays(fromISO(next.periodStart), -Math.round(avgLuteal));
      } else {
        ovulation = addDays(start, Math.round(avgCycle) - Math.round(avgLuteal));
      }
    }
    return {
      start, end, ovulation,
      isPredicted: false,
      isPeriodPredicted: !c.periodEnd,
      isOvulationPredicted: !c.ovulationDate,
      source: c
    };
  });

  // Étend avec des cycles prédits tant que nécessaire
  let cursor = timeline.length ? timeline[timeline.length - 1].start : null;
  if (cursor) {
    let guard = 0;
    while (cursor < untilDate && guard < 240) {
      guard++;
      const nextStart = addDays(cursor, Math.round(avgCycle));
      const nextEnd = addDays(nextStart, Math.round(avgPeriod) - 1);
      const nextOvulation = addDays(nextStart, Math.round(avgCycle) - Math.round(avgLuteal));
      timeline.push({
        start: nextStart,
        end: nextEnd,
        ovulation: nextOvulation,
        isPredicted: true,
        isPeriodPredicted: true,
        isOvulationPredicted: true,
        source: null
      });
      cursor = nextStart;
    }
  }

  return { timeline, avgCycle, avgPeriod, avgLuteal };
}

function dayInfo(date, timeline) {
  for (const c of timeline) {
    const inPeriod = date >= c.start && date <= c.end;
    const inFertile = daysBetween(c.ovulation, date) >= -5 && daysBetween(c.ovulation, date) <= 1;
    const isOvulation = isSameDay(date, c.ovulation);
    if (isOvulation) return { type: c.isOvulationPredicted ? 'ovulation-predicted' : 'ovulation', cycle: c };
    if (inPeriod) return { type: c.isPeriodPredicted ? 'period-predicted' : 'period', cycle: c };
    if (inFertile) return { type: 'fertile', cycle: c };
  }
  return null;
}

/* ============================================================
   État de navigation du calendrier
   ============================================================ */

let viewDate = new Date();
viewDate.setDate(1);

/* ============================================================
   Rendu : tableau de bord + roue de cycle
   ============================================================ */

function renderDashboard() {
  const today = new Date();
  const { timeline, avgCycle, avgPeriod } = buildTimeline(addDays(today, 400));

  document.getElementById('statAvgCycle').textContent = cycles.length >= 2 ? `${Math.round(avgCycle)} j` : `~${avgCycle} j`;
  document.getElementById('statAvgPeriod').textContent = `${Math.round(avgPeriod)} j`;
  const reg = cycleLengthRegularity();
  document.getElementById('statRegularity').textContent = reg === null ? '—' : `± ${reg} j`;

  if (!cycles.length) {
    document.getElementById('statNextPeriod').textContent = '—';
    document.getElementById('wheelDayLabel').textContent = '—';
    document.getElementById('wheelPhaseLabel').textContent = 'Aucune donnée';
    renderWheel(null, null, null);
    return;
  }

  // Cycle en cours = dernier cycle dont le début est <= aujourd'hui
  let current = null;
  for (const c of timeline) {
    if (c.start <= today) current = c; else break;
  }
  if (!current) current = timeline[0];

  const dayOfCycle = daysBetween(current.start, today) + 1;
  const cycleLen = Math.round(avgCycle);

  let phaseLabel = 'Phase folliculaire';
  const info = dayInfo(today, timeline);
  if (info) {
    if (info.type.startsWith('period')) phaseLabel = 'Règles';
    else if (info.type.startsWith('ovulation')) phaseLabel = "Jour d'ovulation";
    else if (info.type === 'fertile') phaseLabel = 'Fenêtre fertile';
  } else if (daysBetween(current.ovulation, today) > 1) {
    phaseLabel = 'Phase lutéale';
  }

  document.getElementById('wheelDayLabel').textContent = `Jour ${dayOfCycle}`;
  document.getElementById('wheelPhaseLabel').textContent = phaseLabel;

  // Prochaines règles : premier cycle dont le début est dans le futur
  const nextCycle = timeline.find(c => c.start > today);
  if (nextCycle) {
    const n = daysBetween(today, nextCycle.start);
    document.getElementById('statNextPeriod').textContent = n <= 0 ? "aujourd'hui" : `${n} j`;
  } else {
    document.getElementById('statNextPeriod').textContent = '—';
  }

  renderWheel(dayOfCycle, cycleLen, current);
}

function renderWheel(dayOfCycle, cycleLen, current) {
  const svg = document.getElementById('cycleWheel');
  if (!dayOfCycle || !cycleLen || !current) {
    svg.innerHTML = `<circle cx="120" cy="120" r="95" fill="none" stroke="var(--border)" stroke-width="14"/>`;
    return;
  }
  const cx = 120, cy = 120, r = 95;
  const periodLen = daysBetween(current.start, current.end) + 1;
  const ovIndex = daysBetween(current.start, current.ovulation) + 1;
  const fertileStartIdx = ovIndex - 5;
  const fertileEndIdx = ovIndex + 1;

  const arc = (fromDay, toDay, color, width) => {
    const a0 = ((fromDay - 1) / cycleLen) * 360 - 90;
    const a1 = ((toDay) / cycleLen) * 360 - 90;
    return describeArc(cx, cy, r, a0, a1, color, width);
  };

  let html = '';
  html += `<circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="var(--border)" stroke-width="14"/>`;
  html += arc(1, periodLen, 'var(--berry)', 14);
  html += arc(fertileStartIdx, fertileEndIdx, 'var(--violet-soft)', 14);
  html += arc(ovIndex, ovIndex + 0.6, 'var(--violet)', 14);

  // Marqueur "aujourd'hui"
  const todayAngle = ((dayOfCycle - 1) / cycleLen) * 360 - 90;
  const rad = (todayAngle * Math.PI) / 180;
  const mx = cx + r * Math.cos(rad);
  const my = cy + r * Math.sin(rad);
  html += `<circle cx="${mx}" cy="${my}" r="7" fill="var(--ink)" stroke="var(--surface)" stroke-width="3"/>`;
  html += `<text x="${cx}" y="${cy + 6}" text-anchor="middle" font-size="13" fill="var(--ink-muted)" font-family="var(--font-body)"> / ${cycleLen} j</text>`;

  svg.innerHTML = html;
}

function describeArc(cx, cy, r, startAngle, endAngle, color, width) {
  const s = polarToCartesian(cx, cy, r, endAngle);
  const e = polarToCartesian(cx, cy, r, startAngle);
  const largeArc = endAngle - startAngle <= 180 ? '0' : '1';
  const d = ['M', s.x, s.y, 'A', r, r, 0, largeArc, 0, e.x, e.y].join(' ');
  return `<path d="${d}" fill="none" stroke="${color}" stroke-width="${width}" stroke-linecap="round"/>`;
}

function polarToCartesian(cx, cy, r, angleDeg) {
  const a = (angleDeg * Math.PI) / 180;
  return { x: cx + r * Math.cos(a), y: cy + r * Math.sin(a) };
}

/* ============================================================
   Rendu : calendrier
   ============================================================ */

function renderCalendar() {
  const grid = document.getElementById('calendarGrid');
  grid.innerHTML = '';
  const label = `${MONTHS_FR[viewDate.getMonth()]} ${viewDate.getFullYear()}`;
  document.getElementById('monthLabel').textContent = label;

  const firstOfMonth = new Date(viewDate.getFullYear(), viewDate.getMonth(), 1);
  const startWeekday = (firstOfMonth.getDay() + 6) % 7; // lundi = 0
  const daysInMonth = new Date(viewDate.getFullYear(), viewDate.getMonth() + 1, 0).getDate();
  const gridStart = addDays(firstOfMonth, -startWeekday);

  const monthEnd = new Date(viewDate.getFullYear(), viewDate.getMonth() + 1, 0);
  const { timeline } = buildTimeline(addDays(monthEnd, 45));

  const today = new Date();
  const totalCells = 42;
  for (let i = 0; i < totalCells; i++) {
    const d = addDays(gridStart, i);
    const btn = document.createElement('button');
    btn.className = 'day-cell';
    btn.type = 'button';
    btn.textContent = d.getDate();

    if (d.getMonth() !== viewDate.getMonth()) btn.classList.add('outside');
    if (isSameDay(d, today)) btn.classList.add('today');

    const info = dayInfo(d, timeline);
    if (info) btn.classList.add(info.type);

    btn.addEventListener('click', () => onDayClick(d));
    grid.appendChild(btn);
  }
}

function onDayClick(date) {
  // Si le jour appartient à un cycle réel existant, on l'édite.
  const iso = toISO(date);
  const match = cycles.find(c => {
    const start = fromISO(c.periodStart);
    const end = c.periodEnd ? fromISO(c.periodEnd) : start;
    return (date >= start && date <= end) || c.ovulationDate === iso;
  });
  if (match) {
    openCycleModal(match);
  } else {
    openCycleModal(null, iso);
  }
}

/* ============================================================
   Rendu : journal
   ============================================================ */

function renderJournal() {
  const list = document.getElementById('journalList');
  const empty = document.getElementById('journalEmpty');
  list.innerHTML = '';
  const sorted = [...cycles].sort((a, b) => fromISO(b.periodStart) - fromISO(a.periodStart));

  empty.classList.toggle('hidden', sorted.length > 0);

  const withLengths = sortedCycles();
  sorted.forEach(c => {
    const li = document.createElement('li');
    li.className = 'journal-item';
    const start = fromISO(c.periodStart);
    const startLabel = start.toLocaleDateString('fr-FR', { day: 'numeric', month: 'short' });
    const endLabel = c.periodEnd ? fromISO(c.periodEnd).toLocaleDateString('fr-FR', { day: 'numeric', month: 'short' }) : '?';

    const idx = withLengths.findIndex(x => x === c);
    let lengthLabel = '';
    if (idx > 0) {
      const len = daysBetween(fromISO(withLengths[idx - 1].periodStart), fromISO(withLengths[idx].periodStart));
      lengthLabel = `${len} j`;
    }

    const metaParts = [];
    if (c.flow) metaParts.push({ light: 'Flux léger', medium: 'Flux moyen', heavy: 'Flux abondant' }[c.flow]);
    if (c.symptoms && c.symptoms.length) metaParts.push(c.symptoms.join(', '));
    if (c.ovulationDate) metaParts.push(`Ovulation le ${fromISO(c.ovulationDate).toLocaleDateString('fr-FR', { day: 'numeric', month: 'short' })}`);

    li.innerHTML = `
      <div>
        <div class="journal-item-dates">${startLabel} → ${endLabel}</div>
        <div class="journal-item-meta">${metaParts.join(' · ') || 'Aucune note'}</div>
      </div>
      <div class="journal-item-length">${lengthLabel}</div>
    `;
    li.addEventListener('click', () => openCycleModal(c));
    list.appendChild(li);
  });
}

/* ============================================================
   Modale : ajout / édition de cycle
   ============================================================ */

const cycleModal = document.getElementById('cycleModal');
const cycleForm = document.getElementById('cycleForm');
let activeSymptoms = [];

function openCycleModal(cycle, prefillStart) {
  document.getElementById('cycleModalTitle').textContent = cycle ? 'Modifier le cycle' : 'Nouveau cycle';
  document.getElementById('cycleId').value = cycle ? cycle.id : '';
  document.getElementById('periodStart').value = cycle ? cycle.periodStart : (prefillStart || toISO(new Date()));
  document.getElementById('periodEnd').value = cycle ? (cycle.periodEnd || '') : '';
  document.getElementById('ovulationDate').value = cycle ? (cycle.ovulationDate || '') : '';
  document.getElementById('flow').value = cycle ? (cycle.flow || '') : '';
  document.getElementById('notes').value = cycle ? (cycle.notes || '') : '';
  document.getElementById('deleteCycleBtn').classList.toggle('hidden', !cycle);

  activeSymptoms = cycle && cycle.symptoms ? [...cycle.symptoms] : [];
  document.querySelectorAll('#symptomChips .chip').forEach(chip => {
    chip.classList.toggle('active', activeSymptoms.includes(chip.dataset.symptom));
  });

  cycleModal.classList.remove('hidden');
}

function closeCycleModal() {
  cycleModal.classList.add('hidden');
}

document.getElementById('symptomChips').addEventListener('click', (e) => {
  const chip = e.target.closest('.chip');
  if (!chip) return;
  const s = chip.dataset.symptom;
  if (activeSymptoms.includes(s)) {
    activeSymptoms = activeSymptoms.filter(x => x !== s);
    chip.classList.remove('active');
  } else {
    activeSymptoms.push(s);
    chip.classList.add('active');
  }
});

cycleForm.addEventListener('submit', (e) => {
  e.preventDefault();
  const id = document.getElementById('cycleId').value;
  const periodStart = document.getElementById('periodStart').value;
  const periodEnd = document.getElementById('periodEnd').value || null;
  const ovulationDate = document.getElementById('ovulationDate').value || null;
  const flow = document.getElementById('flow').value || null;
  const notes = document.getElementById('notes').value.trim();

  if (periodEnd && fromISO(periodEnd) < fromISO(periodStart)) {
    showToast('La fin des règles doit être après le début.');
    return;
  }

  if (id) {
    const c = cycles.find(x => x.id === id);
    Object.assign(c, { periodStart, periodEnd, ovulationDate, flow, notes, symptoms: [...activeSymptoms] });
  } else {
    cycles.push({
      id: crypto.randomUUID ? crypto.randomUUID() : String(Date.now()),
      periodStart, periodEnd, ovulationDate, flow, notes,
      symptoms: [...activeSymptoms]
    });
  }
  saveCycles(cycles);
  closeCycleModal();
  renderAll();
  showToast('Cycle enregistré.');
});

document.getElementById('deleteCycleBtn').addEventListener('click', () => {
  const id = document.getElementById('cycleId').value;
  if (!id) return;
  if (!confirm('Supprimer ce cycle ?')) return;
  cycles = cycles.filter(c => c.id !== id);
  saveCycles(cycles);
  closeCycleModal();
  renderAll();
  showToast('Cycle supprimé.');
});

document.getElementById('addCycleBtn').addEventListener('click', () => openCycleModal(null));

/* ============================================================
   Modale : réglages
   ============================================================ */

const settingsModal = document.getElementById('settingsModal');

function openSettingsModal() {
  document.getElementById('defaultCycleLength').value = settings.defaultCycleLength;
  document.getElementById('defaultPeriodLength').value = settings.defaultPeriodLength;
  document.getElementById('defaultLutealLength').value = settings.defaultLutealLength;
  document.getElementById('cyclesToAverage').value = settings.cyclesToAverage;
  document.getElementById('darkMode').checked = !!settings.darkMode;
  settingsModal.classList.remove('hidden');
}

document.getElementById('settingsBtn').addEventListener('click', openSettingsModal);

document.getElementById('settingsForm').addEventListener('submit', (e) => {
  e.preventDefault();
  settings.defaultCycleLength = Number(document.getElementById('defaultCycleLength').value);
  settings.defaultPeriodLength = Number(document.getElementById('defaultPeriodLength').value);
  settings.defaultLutealLength = Number(document.getElementById('defaultLutealLength').value);
  settings.cyclesToAverage = Number(document.getElementById('cyclesToAverage').value);
  settings.darkMode = document.getElementById('darkMode').checked;
  saveSettings(settings);
  applyTheme();
  settingsModal.classList.add('hidden');
  renderAll();
  showToast('Réglages enregistrés.');
});

/* ============================================================
   Fermeture générique des modales
   ============================================================ */

document.querySelectorAll('[data-close-modal]').forEach(btn => {
  btn.addEventListener('click', () => {
    cycleModal.classList.add('hidden');
    settingsModal.classList.add('hidden');
  });
});
[cycleModal, settingsModal].forEach(overlay => {
  overlay.addEventListener('click', (e) => {
    if (e.target === overlay) overlay.classList.add('hidden');
  });
});

/* ============================================================
   Export / Import
   ============================================================ */

document.getElementById('exportBtn').addEventListener('click', () => {
  const data = { cycles, settings, exportedAt: new Date().toISOString() };
  const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = `lunaire-sauvegarde-${toISO(new Date())}.json`;
  a.click();
  URL.revokeObjectURL(url);
});

document.getElementById('importBtn').addEventListener('click', () => {
  document.getElementById('importFile').click();
});

document.getElementById('importFile').addEventListener('change', (e) => {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = () => {
    try {
      const data = JSON.parse(reader.result);
      if (!Array.isArray(data.cycles)) throw new Error('Format invalide');
      if (!confirm(`Importer ${data.cycles.length} cycle(s) ? Cela remplacera les données actuelles.`)) return;
      cycles = data.cycles;
      settings = { ...DEFAULT_SETTINGS, ...(data.settings || {}) };
      saveCycles(cycles);
      saveSettings(settings);
      applyTheme();
      renderAll();
      showToast('Import réussi.');
    } catch (err) {
      showToast("Fichier invalide.");
    }
  };
  reader.readAsText(file);
  e.target.value = '';
});

/* ============================================================
   Divers : thème, toast, navigation calendrier
   ============================================================ */

function applyTheme() {
  document.documentElement.setAttribute('data-theme', settings.darkMode ? 'dark' : 'light');
}

let toastTimer = null;
function showToast(msg) {
  const toast = document.getElementById('toast');
  toast.textContent = msg;
  toast.classList.remove('hidden');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => toast.classList.add('hidden'), 2600);
}

document.getElementById('prevMonth').addEventListener('click', () => {
  viewDate = new Date(viewDate.getFullYear(), viewDate.getMonth() - 1, 1);
  renderCalendar();
});
document.getElementById('nextMonth').addEventListener('click', () => {
  viewDate = new Date(viewDate.getFullYear(), viewDate.getMonth() + 1, 1);
  renderCalendar();
});
document.getElementById('todayBtn').addEventListener('click', () => {
  viewDate = new Date();
  viewDate.setDate(1);
  renderCalendar();
});

/* ============================================================
   Rendu global + initialisation
   ============================================================ */

function renderAll() {
  renderDashboard();
  renderCalendar();
  renderJournal();
}

applyTheme();
renderAll();

if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('sw.js').catch(() => {});
  });
}

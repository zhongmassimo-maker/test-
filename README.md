index.html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="theme-color" content="#0b1220" />
  <title>Wellness Tracker</title>
  <style>
    :root {
      --bg: #0b1220;
      --card: rgba(255,255,255,.06);
      --card2: rgba(255,255,255,.09);
      --text: rgba(255,255,255,.92);
      --muted: rgba(255,255,255,.68);
      --line: rgba(255,255,255,.12);
      --good: #2dd4bf;
      --warn: #fbbf24;
      --bad: #fb7185;
      --shadow: 0 12px 32px rgba(0,0,0,.35);
      --radius: 18px;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial;
      background: radial-gradient(1200px 700px at 20% 0%, rgba(45,212,191,.12), transparent 55%),
                  radial-gradient(900px 600px at 90% 10%, rgba(99,102,241,.14), transparent 55%),
                  var(--bg);
      color: var(--text);
      min-height: 100vh;
    }
    header { padding: 28px 18px 10px; max-width: 1100px; margin: 0 auto; }
    h1 { margin: 0; font-size: 22px; letter-spacing: .2px; }
    .sub { margin-top: 6px; color: var(--muted); font-size: 13px; }
    main { padding: 14px 18px 36px; max-width: 1100px; margin: 0 auto; display: grid; gap: 14px; grid-template-columns: 360px 1fr; }
    @media (max-width: 920px) { main { grid-template-columns: 1fr; } }

    .card {
      background: linear-gradient(180deg, var(--card), rgba(255,255,255,.03));
      border: 1px solid var(--line);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      overflow: hidden;
    }
    .card h2 { margin: 0; padding: 14px 16px; font-size: 14px; color: rgba(255,255,255,.86); border-bottom: 1px solid var(--line); }
    .card .content { padding: 14px 16px; }

    label { display: block; font-size: 12px; color: var(--muted); margin: 10px 0 6px; }
    input, select, button {
      width: 100%;
      background: rgba(255,255,255,.06);
      border: 1px solid var(--line);
      color: var(--text);
      border-radius: 14px;
      padding: 10px 10px;
      outline: none;
      font-size: 14px;
    }
    input::placeholder { color: rgba(255,255,255,.45); }
    .row { display: grid; gap: 10px; grid-template-columns: 1fr 1fr; }
    .row3 { display: grid; gap: 10px; grid-template-columns: 1fr 1fr 1fr; }
    @media (max-width: 520px) { .row, .row3 { grid-template-columns: 1fr; } }

    .btns { display: grid; gap: 10px; grid-template-columns: 1fr 1fr; margin-top: 12px; }
    .btn {
      cursor: pointer;
      background: linear-gradient(180deg, rgba(45,212,191,.22), rgba(45,212,191,.08));
      border: 1px solid rgba(45,212,191,.35);
    }
    .btn.secondary {
      background: rgba(255,255,255,.05);
      border: 1px solid var(--line);
    }
    .btn.danger {
      background: linear-gradient(180deg, rgba(251,113,133,.20), rgba(251,113,133,.08));
      border: 1px solid rgba(251,113,133,.35);
    }

    .kpis { display: grid; gap: 10px; grid-template-columns: repeat(4, minmax(0, 1fr)); }
    @media (max-width: 920px) { .kpis { grid-template-columns: repeat(2, minmax(0,1fr)); } }
    .kpi {
      padding: 12px 12px;
      background: rgba(255,255,255,.05);
      border: 1px solid var(--line);
      border-radius: 16px;
    }
    .kpi .t { font-size: 11px; color: var(--muted); margin-bottom: 6px; }
    .kpi .v { font-size: 18px; font-weight: 650; display: flex; align-items: baseline; gap: 8px; }
    .kpi .v span.unit { font-size: 11px; color: var(--muted); font-weight: 500; }
    .chip { font-size: 11px; padding: 4px 8px; border-radius: 999px; border: 1px solid var(--line); color: var(--muted); background: rgba(255,255,255,.04); }
    .chip.good { border-color: rgba(45,212,191,.35); color: rgba(45,212,191,.92); }
    .chip.warn { border-color: rgba(251,191,36,.35); color: rgba(251,191,36,.96); }
    .chip.bad { border-color: rgba(251,113,133,.35); color: rgba(251,113,133,.92); }

    .chartWrap { padding: 12px; background: rgba(255,255,255,.03); border: 1px solid var(--line); border-radius: 16px; }
    svg { width: 100%; height: auto; display: block; }
    .topbar { display: flex; gap: 10px; align-items: center; justify-content: space-between; margin-bottom: 10px; flex-wrap: wrap; }
    .topbar .left { display: flex; gap: 10px; align-items: center; flex-wrap: wrap; }
    .topbar select { width: 200px; }
    .note { font-size: 12px; color: var(--muted); line-height: 1.4; }
    .divider { height: 1px; background: var(--line); margin: 12px 0; }

    table { width: 100%; border-collapse: collapse; font-size: 13px; }
    th, td { text-align: left; padding: 10px 8px; border-bottom: 1px solid var(--line); color: rgba(255,255,255,.86); }
    th { color: var(--muted); font-weight: 600; font-size: 11px; text-transform: uppercase; letter-spacing: .08em; }
    tr:hover td { background: rgba(255,255,255,.03); }
    .actions { display: flex; gap: 8px; }
    .tiny {
      width: auto;
      padding: 7px 10px;
      border-radius: 12px;
      font-size: 12px;
      cursor: pointer;
    }
    .tiny.secondary { background: rgba(255,255,255,.05); border: 1px solid var(--line); }
    .tiny.danger { background: rgba(251,113,133,.10); border: 1px solid rgba(251,113,133,.25); }
    .footer { margin-top: 10px; font-size: 11px; color: rgba(255,255,255,.5); }
    a { color: rgba(45,212,191,.9); }
  </style>
</head>
<body>
  <header>
    <h1>Wellness Tracker</h1>
    <div class="sub">A simple, free “app” you can run in a browser (and add to your phone’s home screen). Data stays on your device.</div>
  </header>

  <main>
    <section class="card">
      <h2>Add / Edit Daily Entry</h2>
      <div class="content">
        <label>Date</label>
        <input id="date" type="date" />
        <div class="row">
          <div>
            <label>Sleep (hours)</label>
            <input id="sleep" type="number" step="0.1" min="0" placeholder="e.g. 7.5" />
          </div>
          <div>
            <label>Resting HR (bpm)</label>
            <input id="rhr" type="number" step="1" min="0" placeholder="e.g. 55" />
          </div>
        </div>
        <div class="row">
          <div>
            <label>HRV (ms)</label>
            <input id="hrv" type="number" step="1" min="0" placeholder="e.g. 65" />
          </div>
          <div>
            <label>Temperature delta (°C)</label>
            <input id="temp" type="number" step="0.01" placeholder="e.g. 0.12" />
          </div>
        </div>

        <div class="btns">
          <button class="btn" id="saveBtn">Save entry</button>
          <button class="btn secondary" id="loadBtn">Load date (edit)</button>
        </div>

        <div class="divider"></div>

        <div class="row">
          <button class="btn secondary" id="exportBtn">Export JSON</button>
          <label style="margin:0;">
            <span style="display:block;font-size:12px;color:var(--muted);margin:0 0 6px;">Import JSON</span>
            <input id="importFile" type="file" accept="application/json" />
          </label>
        </div>

        <div class="footer">
          Tip: host this file on GitHub Pages / Netlify to share it. For iPhone: open in Safari → Share → <b>Add to Home Screen</b>.
        </div>
      </div>
    </section>

    <section class="card">
      <h2>Dashboard</h2>
      <div class="content">
        <div class="kpis" id="kpis"></div>

        <div style="height:12px;"></div>

        <div class="topbar">
          <div class="left">
            <select id="metric">
              <option value="sleep">Sleep (hours)</option>
              <option value="rhr">Resting HR (bpm)</option>
              <option value="hrv">HRV (ms)</option>
              <option value="temp">Temp delta (°C)</option>
            </select>
            <span class="chip" id="trendChip">Trend: —</span>
          </div>
          <div class="note" id="chartNote">Select a metric to view the last 30 entries.</div>
        </div>

        <div class="chartWrap">
          <svg viewBox="0 0 680 260" role="img" aria-label="Metric chart">
            <defs>
              <linearGradient id="area" x1="0" x2="0" y1="0" y2="1">
                <stop offset="0%" stop-color="rgba(45,212,191,.32)"></stop>
                <stop offset="100%" stop-color="rgba(45,212,191,0)"></stop>
              </linearGradient>
            </defs>
            <g id="grid"></g>
            <path id="areaPath" fill="url(#area)" opacity="1"></path>
            <path id="linePath" fill="none" stroke="rgba(45,212,191,.9)" stroke-width="3" stroke-linecap="round"></path>
            <g id="dots"></g>
            <text id="emptyText" x="340" y="135" text-anchor="middle" fill="rgba(255,255,255,.55)" font-size="14"></text>
          </svg>
        </div>

        <div style="height:14px;"></div>

        <div class="topbar">
          <div class="note">Recent entries (newest first)</div>
          <button class="tiny danger" id="clearBtn" title="Deletes all stored data">Clear all</button>
        </div>

        <div style="overflow:auto;">
          <table>
            <thead>
              <tr>
                <th>Date</th>
                <th>Sleep</th>
                <th>RHR</th>
                <th>HRV</th>
                <th>Temp</th>
                <th></th>
              </tr>
            </thead>
            <tbody id="rows"></tbody>
          </table>
        </div>
      </div>
    </section>
  </main>

  <script>
    const LS_KEY = "wellnessBio:v1";

    const el = (id) => document.getElementById(id);
    const dateEl = el("date");
    const sleepEl = el("sleep");
    const rhrEl = el("rhr");
    const hrvEl = el("hrv");
    const tempEl = el("temp");
    const rowsEl = el("rows");
    const metricEl = el("metric");
    const kpisEl = el("kpis");
    const trendChip = el("trendChip");
    const chartNote = el("chartNote");
    const linePath = el("linePath");
    const areaPath = el("areaPath");
    const dotsG = el("dots");
    const gridG = el("grid");
    const emptyText = el("emptyText");

    function todayISO() {
      const d = new Date();
      const tzOff = d.getTimezoneOffset() * 60000;
      return new Date(d - tzOff).toISOString().slice(0,10);
    }
    dateEl.value = todayISO();

    function loadAll() {
      try {
        const raw = localStorage.getItem(LS_KEY);
        if (!raw) return [];
        const data = JSON.parse(raw);
        return Array.isArray(data) ? data : [];
      } catch { return []; }
    }
    function saveAll(data) {
      localStorage.setItem(LS_KEY, JSON.stringify(data));
    }
    function toNum(v) {
      if (v === "" || v === null || v === undefined) return null;
      const n = Number(v);
      return Number.isFinite(n) ? n : null;
    }
    function upsertEntry(entry) {
      const data = loadAll();
      const idx = data.findIndex(x => x.date === entry.date);
      if (idx >= 0) data[idx] = entry; else data.push(entry);
      data.sort((a,b) => a.date.localeCompare(b.date));
      saveAll(data);
    }
    function deleteEntry(date) {
      const data = loadAll().filter(x => x.date !== date);
      saveAll(data);
    }
    function fmt(v, digits=1) {
      if (v === null || v === undefined) return "—";
      const n = Number(v);
      if (!Number.isFinite(n)) return "—";
      return (Math.round(n * Math.pow(10, digits)) / Math.pow(10, digits)).toString();
    }
    function avg(values) {
      const xs = values.filter(v => v !== null && Number.isFinite(v));
      if (!xs.length) return null;
      return xs.reduce((a,b)=>a+b,0) / xs.length;
    }

    function linearTrend(vals) {
      // Least squares slope for y over sequential x = 0..n-1
      const ys = vals.map(v => (v === null ? null : Number(v)));
      const points = ys
        .map((y, i) => ({x:i, y}))
        .filter(p => p.y !== null && Number.isFinite(p.y));
      if (points.length < 3) return {label:"—", cls:"", slope:0};

      const n = points.length;
      const sumX = points.reduce((s,p)=>s+p.x,0);
      const sumY = points.reduce((s,p)=>s+p.y,0);
      const sumXY = points.reduce((s,p)=>s+p.x*p.y,0);
      const sumXX = points.reduce((s,p)=>s+p.x*p.x,0);

      const denom = (n * sumXX - sumX * sumX);
      if (denom === 0) return {label:"—", cls:"", slope:0};

      const slope = (n * sumXY - sumX * sumY) / denom;

      const mag = Math.abs(slope);
      if (mag < 0.02) return {label:"Flat", cls:"", slope};
      return slope > 0 ? {label:"Up", cls:"good", slope} : {label:"Down", cls:"warn", slope};
    }

    function renderTable(data) {
      const sorted = [...data].sort((a,b)=>b.date.localeCompare(a.date));
      const recent = sorted.slice(0, 20);
      rowsEl.innerHTML = recent.map(row => `
        <tr>
          <td>${row.date}</td>
          <td>${fmt(row.sleep,1)}</td>
          <td>${fmt(row.rhr,0)}</td>
          <td>${fmt(row.hrv,0)}</td>
          <td>${fmt(row.temp,2)}</td>
          <td>
            <div class="actions">
              <button class="tiny secondary" data-action="edit" data-date="${row.date}">Edit</button>
              <button class="tiny danger" data-action="del" data-date="${row.date}">Delete</button>
            </div>
          </td>
        </tr>
      `).join("") || `<tr><td colspan="6" style="color:rgba(255,255,255,.6);">No entries yet. Add your first one on the left.</td></tr>`;
    }

    function kpiCard(title, value, unit, hint) {
      return `
        <div class="kpi">
          <div class="t">${title}</div>
          <div class="v">${value} <span class="unit">${unit}</span></div>
          <div class="note">${hint}</div>
        </div>
      `;
    }

    function renderKPIs(data) {
      const sorted = [...data].sort((a,b)=>a.date.localeCompare(b.date));

      const last7 = sorted.slice(-7);
      const last30 = sorted.slice(-30);

      const sleep7 = avg(last7.map(x=>x.sleep));
      const rhr7 = avg(last7.map(x=>x.rhr));
      const hrv7 = avg(last7.map(x=>x.hrv));
      const temp7 = avg(last7.map(x=>x.temp));

      const sleep30 = avg(last30.map(x=>x.sleep));
      const rhr30 = avg(last30.map(x=>x.rhr));
      const hrv30 = avg(last30.map(x=>x.hrv));
      const temp30 = avg(last30.map(x=>x.temp));

      kpisEl.innerHTML = [
        kpiCard("Sleep (7d avg)", fmt(sleep7,1), "hrs", `30d avg: ${fmt(sleep30,1)} hrs`),
        kpiCard("Resting HR (7d avg)", fmt(rhr7,0), "bpm", `30d avg: ${fmt(rhr30,0)} bpm`),
        kpiCard("HRV (7d avg)", fmt(hrv7,0), "ms", `30d avg: ${fmt(hrv30,0)} ms`),
        kpiCard("Temp Δ (7d avg)", fmt(temp7,2), "°C", `30d avg: ${fmt(temp30,2)} °C`)
      ].join("");
    }

    function renderChart(data, metric) {
      const sorted = [...data].sort((a,b)=>a.date.localeCompare(b.date));
      const last = sorted.slice(-30);
      const series = last.map(x => ({date: x.date, v: x[metric] ?? null}))
                         .filter(x => x.v !== undefined);

      // grid
      gridG.innerHTML = "";
      for (let i = 0; i < 5; i++) {
        const y = 20 + i * 50;
        const line = document.createElementNS("http://www.w3.org/2000/svg", "line");
        line.setAttribute("x1", "30");
        line.setAttribute("x2", "650");
        line.setAttribute("y1", y);
        line.setAttribute("y2", y);
        line.setAttribute("stroke", "rgba(255,255,255,.10)");
        line.setAttribute("stroke-width", "1");
        gridG.appendChild(line);
      }

      if (series.length < 2 || series.every(p => p.v === null)) {
        linePath.setAttribute("d", "");
        areaPath.setAttribute("d", "");
        dotsG.innerHTML = "";
        emptyText.textContent = "Add a few entries to see a chart";
        chartNote.textContent = "Shows your last 30 entries (stored only on this device).";
        trendChip.textContent = "Trend: —";
        trendChip.className = "chip";
        return;
      }

      emptyText.textContent = "";

      const vals = series.map(p => (p.v === null ? null : Number(p.v)));
      const finite = vals.filter(v => v !== null && Number.isFinite(v));
      const min = Math.min(...finite);
      const max = Math.max(...finite);
      const pad = (max - min) === 0 ? (Math.abs(max) || 1) * 0.1 : (max - min) * 0.12;
      const lo = min - pad;
      const hi = max + pad;

      const W = 620, H = 210;
      const x0 = 30, y0 = 20;
      const xStep = series.length > 1 ? W / (series.length - 1) : W;

      const pts = series.map((p, i) => {
        const x = x0 + i * xStep;
        if (p.v === null || !Number.isFinite(Number(p.v))) return {x, y: null, v: null, date: p.date};
        const t = (Number(p.v) - lo) / (hi - lo);
        const y = y0 + (1 - t) * H;
        return {x, y, v: Number(p.v), date: p.date};
      });

      let d = "";
      let started = false;
      for (const p of pts) {
        if (p.y === null) { started = false; continue; }
        d += (started ? " L " : " M ") + p.x.toFixed(2) + " " + p.y.toFixed(2);
        started = true;
      }
      linePath.setAttribute("d", d);

      // area: start at bottom-left, follow line, then bottom-right
      const bottomY = y0 + H;
      const firstValid = pts.find(p => p.y !== null);
      const lastValid = [...pts].reverse().find(p => p.y !== null);
      let area = "";
      if (firstValid && lastValid) {
        // Build contiguous line segments only; if gaps exist, area still looks ok for simple use.
        area = `M ${firstValid.x.toFixed(2)} ${bottomY.toFixed(2)} ` + d.replace(/^M /, "L ") +
               ` L ${lastValid.x.toFixed(2)} ${bottomY.toFixed(2)} Z`;
      }
      areaPath.setAttribute("d", area);

      // dots
      dotsG.innerHTML = "";
      for (const p of pts) {
        if (p.y === null) continue;
        const c = document.createElementNS("http://www.w3.org/2000/svg", "circle");
        c.setAttribute("cx", p.x);
        c.setAttribute("cy", p.y);
        c.setAttribute("r", "4.2");
        c.setAttribute("fill", "rgba(255,255,255,.92)");
        c.setAttribute("opacity", "0.9");
        dotsG.appendChild(c);
      }

      const tr = linearTrend(vals);
      trendChip.textContent = `Trend: ${tr.label}`;
      trendChip.className = "chip" + (tr.cls ? (" " + tr.cls) : "");

      const metricLabel = metricEl.options[metricEl.selectedIndex].textContent;
      chartNote.textContent = `${metricLabel} • range: ${fmt(min,2)} to ${fmt(max,2)} • last ${series.length} entries`;
    }

    function fillForm(entry) {
      sleepEl.value = entry.sleep ?? "";
      rhrEl.value = entry.rhr ?? "";
      hrvEl.value = entry.hrv ?? "";
      tempEl.value = entry.temp ?? "";
    }

    function getFormEntry() {
      const date = dateEl.value || todayISO();
      return {
        date,
        sleep: toNum(sleepEl.value),
        rhr: toNum(rhrEl.value),
        hrv: toNum(hrvEl.value),
        temp: toNum(tempEl.value),
      };
    }

    function refresh() {
      const data = loadAll();
      renderTable(data);
      renderKPIs(data);
      renderChart(data, metricEl.value);
    }

    el("saveBtn").addEventListener("click", () => {
      const entry = getFormEntry();
      if (!entry.date) { alert("Please pick a date."); return; }
      upsertEntry(entry);
      refresh();
    });

    el("loadBtn").addEventListener("click", () => {
      const data = loadAll();
      const found = data.find(x => x.date === dateEl.value);
      if (!found) { alert("No entry for that date yet."); return; }
      fillForm(found);
    });

    metricEl.addEventListener("change", refresh);

    rowsEl.addEventListener("click", (e) => {
      const btn = e.target.closest("button");
      if (!btn) return;
      const date = btn.dataset.date;
      const action = btn.dataset.action;
      if (action === "edit") {
        dateEl.value = date;
        const data = loadAll();
        const found = data.find(x => x.date === date);
        if (found) fillForm(found);
        window.scrollTo({top: 0, behavior: "smooth"});
      } else if (action === "del") {
        if (!confirm(`Delete entry for ${date}?`)) return;
        deleteEntry(date);
        refresh();
      }
    });

    el("clearBtn").addEventListener("click", () => {
      if (!confirm("This will delete ALL stored data on this device. Continue?")) return;
      localStorage.removeItem(LS_KEY);
      refresh();
    });

    el("exportBtn").addEventListener("click", () => {
      const data = loadAll();
      const blob = new Blob([JSON.stringify(data, null, 2)], {type:"application/json"});
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = "wellness-data.json";
      a.click();
      URL.revokeObjectURL(url);
    });

    el("importFile").addEventListener("change", async (e) => {
      const file = e.target.files?.[0];
      if (!file) return;
      try {
        const text = await file.text();
        const data = JSON.parse(text);
        if (!Array.isArray(data)) throw new Error("JSON must be an array");
        // basic sanitize
        const clean = data
          .filter(x => x && typeof x.date === "string")
          .map(x => ({
            date: x.date.slice(0,10),
            sleep: toNum(x.sleep),
            rhr: toNum(x.rhr),
            hrv: toNum(x.hrv),
            temp: toNum(x.temp),
          }))
          .sort((a,b)=>a.date.localeCompare(b.date));
        saveAll(clean);
        refresh();
        alert("Imported!");
      } catch (err) {
        alert("Import failed: " + err.message);
      } finally {
        e.target.value = "";
      }
    });

    refresh();
  </script>
</body>
</html>

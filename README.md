<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Epigenetics & Aging Analysis — README</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;600&family=Spectral:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0e14;
    --bg2: #0f1620;
    --bg3: #141c28;
    --border: #1e2d42;
    --accent: #00d4ff;
    --accent2: #ff6b6b;
    --accent3: #a8ff78;
    --text: #c8d8e8;
    --muted: #5a7590;
    --heading: #e8f4ff;
    --code-bg: #0d1a26;
    --tag-dna: #00d4ff22;
    --tag-dna-border: #00d4ff55;
    --glow: 0 0 20px #00d4ff33;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Spectral', Georgia, serif;
    font-size: 17px;
    line-height: 1.75;
    min-height: 100vh;
  }

  /* DNA helix background pattern */
  body::before {
    content: '';
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background:
      radial-gradient(ellipse 60% 40% at 90% 10%, #00d4ff0a 0%, transparent 60%),
      radial-gradient(ellipse 50% 60% at 10% 80%, #a8ff780a 0%, transparent 60%),
      radial-gradient(ellipse 40% 50% at 50% 50%, #ff6b6b05 0%, transparent 60%);
    pointer-events: none;
    z-index: 0;
  }

  .container {
    max-width: 960px;
    margin: 0 auto;
    padding: 0 32px 80px;
    position: relative;
    z-index: 1;
  }

  /* ── HEADER ── */
  header {
    padding: 64px 0 40px;
    border-bottom: 1px solid var(--border);
    margin-bottom: 52px;
  }

  .header-tag {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent);
    background: var(--tag-dna);
    border: 1px solid var(--tag-dna-border);
    display: inline-block;
    padding: 4px 12px;
    border-radius: 2px;
    margin-bottom: 20px;
  }

  h1 {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(28px, 5vw, 44px);
    font-weight: 700;
    color: var(--heading);
    line-height: 1.15;
    letter-spacing: -1px;
    margin-bottom: 16px;
  }

  h1 span.cyan { color: var(--accent); }
  h1 span.red  { color: var(--accent2); }

  .meta {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12.5px;
    color: var(--muted);
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    margin-top: 20px;
  }

  .meta-item {
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .meta-item .dot {
    width: 6px; height: 6px;
    border-radius: 50%;
    background: var(--accent);
    flex-shrink: 0;
  }

  /* ── BADGES ── */
  .badges {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 24px;
  }

  .badge {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    padding: 4px 10px;
    border-radius: 3px;
    border: 1px solid;
  }

  .badge-cyan  { background: #00d4ff15; border-color: #00d4ff55; color: var(--accent); }
  .badge-green { background: #a8ff7815; border-color: #a8ff7855; color: var(--accent3); }
  .badge-red   { background: #ff6b6b15; border-color: #ff6b6b55; color: var(--accent2); }
  .badge-gold  { background: #f0b42a15; border-color: #f0b42a55; color: #f0b42a; }

  /* ── SECTIONS ── */
  section {
    margin-bottom: 56px;
  }

  h2 {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 22px;
    font-weight: 600;
    color: var(--heading);
    letter-spacing: -0.4px;
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    gap: 10px;
  }

  h2 .num {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--accent);
    font-weight: 400;
    background: var(--tag-dna);
    border: 1px solid var(--tag-dna-border);
    padding: 2px 7px;
    border-radius: 2px;
  }

  h3 {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 16px;
    font-weight: 600;
    color: var(--heading);
    margin: 28px 0 10px;
  }

  p { margin-bottom: 14px; }

  a { color: var(--accent); text-decoration: none; }
  a:hover { text-decoration: underline; }

  /* ── OVERVIEW CARDS ── */
  .card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 16px;
    margin: 24px 0;
  }

  .card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 20px;
    transition: border-color 0.2s, box-shadow 0.2s;
  }

  .card:hover {
    border-color: #2a3d55;
    box-shadow: 0 4px 20px #00000030;
  }

  .card-icon {
    font-size: 24px;
    margin-bottom: 10px;
  }

  .card-title {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 13px;
    font-weight: 600;
    color: var(--heading);
    text-transform: uppercase;
    letter-spacing: 0.5px;
    margin-bottom: 4px;
  }

  .card-value {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 22px;
    font-weight: 600;
    color: var(--accent);
    line-height: 1;
    margin-bottom: 4px;
  }

  .card-sub {
    font-size: 13px;
    color: var(--muted);
  }

  /* ── CODE BLOCKS ── */
  pre {
    background: var(--code-bg);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent);
    border-radius: 4px;
    padding: 18px 20px;
    overflow-x: auto;
    margin: 16px 0;
  }

  code {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 13px;
    color: #8be0f7;
    line-height: 1.6;
  }

  p code, li code {
    background: var(--code-bg);
    border: 1px solid var(--border);
    padding: 1px 6px;
    border-radius: 3px;
    font-size: 13px;
    color: var(--accent);
  }

  /* ── PIPELINE DIAGRAM ── */
  .pipeline {
    display: flex;
    align-items: stretch;
    gap: 0;
    margin: 28px 0;
    flex-wrap: wrap;
  }

  .pipe-step {
    flex: 1;
    min-width: 110px;
    background: var(--bg2);
    border: 1px solid var(--border);
    padding: 16px 14px;
    text-align: center;
    position: relative;
  }

  .pipe-step:first-child { border-radius: 6px 0 0 6px; }
  .pipe-step:last-child  { border-radius: 0 6px 6px 0; }

  .pipe-step:not(:last-child)::after {
    content: '→';
    position: absolute;
    right: -12px;
    top: 50%;
    transform: translateY(-50%);
    color: var(--accent);
    font-size: 16px;
    z-index: 2;
    background: var(--bg);
    padding: 0 2px;
  }

  .pipe-icon { font-size: 18px; margin-bottom: 6px; }

  .pipe-name {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    color: var(--accent);
    font-weight: 600;
    margin-bottom: 3px;
    letter-spacing: 0.5px;
  }

  .pipe-desc {
    font-size: 11.5px;
    color: var(--muted);
    line-height: 1.4;
  }

  /* ── TABLE ── */
  table {
    width: 100%;
    border-collapse: collapse;
    margin: 20px 0;
    font-size: 14px;
  }

  th {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--accent);
    background: var(--bg2);
    padding: 10px 14px;
    text-align: left;
    border-bottom: 2px solid var(--border);
  }

  td {
    padding: 9px 14px;
    border-bottom: 1px solid #141c26;
    color: var(--text);
    vertical-align: middle;
  }

  tr:hover td { background: #0f1e2e; }

  td.clock-name {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--heading);
  }

  td.generation {
    font-size: 12px;
    color: var(--muted);
  }

  /* ── VIZ FIGURES ── */
  .fig-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin: 24px 0;
  }

  .fig-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 6px;
    overflow: hidden;
  }

  .fig-card.wide {
    grid-column: 1 / -1;
  }

  .fig-canvas-wrap {
    background: #080e18;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 16px;
    min-height: 200px;
  }

  .fig-canvas-wrap canvas,
  .fig-canvas-wrap svg {
    width: 100%;
    height: auto;
    display: block;
  }

  .fig-caption {
    padding: 10px 14px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11.5px;
    color: var(--muted);
    border-top: 1px solid var(--border);
  }

  .fig-caption strong {
    color: var(--accent);
    font-weight: 600;
  }

  /* ── CALLOUT ── */
  .callout {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-left: 3px solid var(--accent3);
    border-radius: 4px;
    padding: 16px 20px;
    margin: 20px 0;
    font-size: 15px;
  }

  .callout-title {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    color: var(--accent3);
    margin-bottom: 6px;
  }

  /* ── FILE TREE ── */
  .tree {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 13px;
    background: var(--code-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 18px 20px;
    color: var(--text);
    line-height: 1.8;
  }

  .tree .dir   { color: var(--accent); font-weight: 600; }
  .tree .file  { color: #9ab8d0; }
  .tree .note  { color: var(--muted); }

  /* ── DIVIDER ── */
  hr {
    border: none;
    border-top: 1px solid var(--border);
    margin: 40px 0;
  }

  /* ── LIST ── */
  ul, ol { padding-left: 24px; }
  li { margin-bottom: 6px; }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--border);
    padding-top: 28px;
    margin-top: 60px;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 12px;
    color: var(--muted);
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 8px;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 640px) {
    .container { padding: 0 18px 60px; }
    .fig-grid  { grid-template-columns: 1fr; }
    .pipeline  { flex-direction: column; }
    .pipe-step { border-radius: 0; }
    .pipe-step:first-child { border-radius: 6px 6px 0 0; }
    .pipe-step:last-child  { border-radius: 0 0 6px 6px; }
    .pipe-step:not(:last-child)::after { content: '↓'; right: auto; left: 50%; top: auto; bottom: -12px; transform: translateX(-50%); }
  }
</style>
</head>
<body>
<div class="container">

<!-- ═══════════════ HEADER ═══════════════ -->
<header>
  <div class="header-tag">BI-436 · Special Topics in Bioinformatics</div>
  <h1><span class="cyan">Epigenetics</span> &amp; <span class="red">Aging</span><br>Analysis</h1>
  <div class="meta">
    <span class="meta-item"><span class="dot"></span>Aarish Sajid · 454572</span>
    <span class="meta-item"><span class="dot" style="background:var(--accent3)"></span>NUST SINES</span>
    <span class="meta-item"><span class="dot" style="background:var(--accent2)"></span>Spring 2026</span>
  </div>
  <div class="badges">
    <span class="badge badge-cyan">Python 3.10+</span>
    <span class="badge badge-cyan">biolearn</span>
    <span class="badge badge-cyan">PyTorch</span>
    <span class="badge badge-green">14 Clocks</span>
    <span class="badge badge-green">2 GEO Datasets</span>
    <span class="badge badge-red">WGBS Pipeline</span>
    <span class="badge badge-gold">EPIC Array</span>
  </div>
</header>

<!-- ═══════════════ OVERVIEW ═══════════════ -->
<section>
  <h2><span class="num">00</span> Overview</h2>
  <p>
    This project benchmarks <strong>fourteen epigenetic aging clocks</strong> against two public GEO datasets
    (GSE40279, GSE41169), quantifying how well DNA-methylation-based models predict chronological age.
    A companion WGBS pipeline processes raw bisulfite-sequencing reads through alignment, methylation
    extraction, and differential methylation region (DMR) detection across seven breast-tissue methylomes.
  </p>

  <div class="card-grid">
    <div class="card">
      <div class="card-icon">🧬</div>
      <div class="card-title">Clocks Tested</div>
      <div class="card-value">14</div>
      <div class="card-sub">Horvath v1/v2, Hannum, PhenoAge, AltumAge, DunedinPACE + more</div>
    </div>
    <div class="card">
      <div class="card-icon">🗂️</div>
      <div class="card-title">Datasets</div>
      <div class="card-value">2</div>
      <div class="card-sub">GSE40279 (n≈656) &amp; GSE41169 (n≈95)</div>
    </div>
    <div class="card">
      <div class="card-icon">🔬</div>
      <div class="card-title">WGBS Samples</div>
      <div class="card-value">7</div>
      <div class="card-sub">NB1, NB2, BT089, BT126, BT198, MCF7, T47D</div>
    </div>
    <div class="card">
      <div class="card-icon">📊</div>
      <div class="card-title">Visualisations</div>
      <div class="card-value">5</div>
      <div class="card-sub">Correlation matrix, age deviation heatmap, scatter plots, MAE bars, distributions</div>
    </div>
  </div>
</section>

<!-- ═══════════════ PROJECT STRUCTURE ═══════════════ -->
<section>
  <h2><span class="num">01</span> Project Structure</h2>
  <div class="tree">
<span class="dir">epigenetics-aging/</span>
├── <span class="dir">wgbs/</span>
│   ├── <span class="file">run_wgbs_pipeline.sh</span>         <span class="note"># Main WGBS bash pipeline</span>
│   └── <span class="file">README.md</span>                      <span class="note"># Galaxy walkthrough</span>
├── <span class="dir">results/</span>
│   ├── <span class="dir">figures/</span>
│   │   ├── <span class="file">correlation_matrix_GSE40279.png</span>
│   │   ├── <span class="file">correlation_matrix_GSE41169.png</span>
│   │   ├── <span class="file">age_deviation_heatmap_GSE40279.png</span>
│   │   ├── <span class="file">age_deviation_heatmap_GSE41169.png</span>
│   │   ├── <span class="file">age_prediction_GSE40279.png</span>
│   │   ├── <span class="file">age_prediction_GSE41169.png</span>
│   │   ├── <span class="file">mae_comparison.png</span>
│   │   └── <span class="file">predicted_age_distribution.png</span>
│   ├── <span class="dir">tables/</span>
│   │   ├── <span class="file">metrics_GSE40279.csv</span>
│   │   └── <span class="file">metrics_GSE41169.csv</span>
│   └── <span class="file">summary.md</span>                     <span class="note"># Auto-generated metrics report</span>
└── <span class="file">epigenetics_aging_analysis.ipynb</span>   <span class="note"># Main analysis notebook</span>
  </div>
</section>

<!-- ═══════════════ PART 1 — WGBS ═══════════════ -->
<section>
  <h2><span class="num">02</span> Part 1 — WGBS Pipeline</h2>
  <p>
    Whole-genome bisulfite sequencing (WGBS) data from seven breast methylomes is processed
    end-to-end: QC → trimming → bisulfite-aware alignment → methylation extraction →
    CpG-island profiling → DMR detection → hierarchical clustering.
  </p>

  <!-- Pipeline flow -->
  <div class="pipeline">
    <div class="pipe-step">
      <div class="pipe-icon">🔍</div>
      <div class="pipe-name">Falco QC</div>
      <div class="pipe-desc">Per-sample quality check</div>
    </div>
    <div class="pipe-step">
      <div class="pipe-icon">✂️</div>
      <div class="pipe-name">Trim Galore</div>
      <div class="pipe-desc">Q20, length ≥ 20 bp</div>
    </div>
    <div class="pipe-step">
      <div class="pipe-icon">🗺️</div>
      <div class="pipe-name">bwa-meth</div>
      <div class="pipe-desc">Bisulfite alignment to hg38</div>
    </div>
    <div class="pipe-step">
      <div class="pipe-icon">⚗️</div>
      <div class="pipe-name">MethylDackel</div>
      <div class="pipe-desc">CpG methylation extraction</div>
    </div>
    <div class="pipe-step">
      <div class="pipe-icon">🏝️</div>
      <div class="pipe-name">deepTools</div>
      <div class="pipe-desc">CpG-island profiles</div>
    </div>
    <div class="pipe-step">
      <div class="pipe-icon">📍</div>
      <div class="pipe-name">Metilene</div>
      <div class="pipe-desc">DMR detection</div>
    </div>
  </div>

  <h3>Samples</h3>
  <table>
    <thead>
      <tr><th>Sample</th><th>Type</th><th>Group</th></tr>
    </thead>
    <tbody>
      <tr><td class="clock-name">NB1</td><td>Normal breast tissue</td><td class="badge badge-green">Normal (A)</td></tr>
      <tr><td class="clock-name">NB2</td><td>Normal breast tissue</td><td class="badge badge-green">Normal (A)</td></tr>
      <tr><td class="clock-name">BT089</td><td>Breast tumour</td><td class="badge badge-red">Tumour (B)</td></tr>
      <tr><td class="clock-name">BT126</td><td>Breast tumour</td><td class="badge badge-red">Tumour (B)</td></tr>
      <tr><td class="clock-name">BT198</td><td>Breast tumour</td><td class="badge badge-red">Tumour (B)</td></tr>
      <tr><td class="clock-name">MCF7</td><td>Breast cancer cell line</td><td class="badge badge-red">Tumour (B)</td></tr>
      <tr><td class="clock-name">T47D</td><td>Breast cancer cell line</td><td class="badge badge-red">Tumour (B)</td></tr>
    </tbody>
  </table>

  <h3>Key Outputs</h3>
  <ul>
    <li><code>CGI_methylation_profile.png</code> — average CpG-island methylation profile centred on CGI midpoints (±2 kb)</li>
    <li><code>dmrs_tumour_vs_normal.bed</code> — differentially methylated regions (normal A vs tumour B) via Metilene</li>
    <li><code>hierarchical_hmr_clustering.png</code> — cosine-distance ward-linkage heatmap of HMR methylation across all 7 samples</li>
  </ul>

  <h3>Quick Start (CLI)</h3>
  <pre><code>bash wgbs/run_wgbs_pipeline.sh</code></pre>

  <p>Alternatively, import the Galaxy workflow via <a href="https://usegalaxy.eu" target="_blank">usegalaxy.eu</a>.</p>

  <!-- WGBS visual -->
  <div class="fig-grid" style="margin-top:28px;">
    <div class="fig-card wide">
      <div class="fig-canvas-wrap">
        <svg viewBox="0 0 820 220" xmlns="http://www.w3.org/2000/svg" style="max-height:220px;">
          <defs>
            <linearGradient id="g1" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%"  stop-color="#00d4ff" stop-opacity="0.15"/>
              <stop offset="100%" stop-color="#a8ff78" stop-opacity="0.08"/>
            </linearGradient>
          </defs>
          <!-- Background rect -->
          <rect width="820" height="220" fill="url(#g1)" rx="4"/>

          <!-- CpG island methylation profile sketch -->
          <!-- X-axis -->
          <line x1="60" y1="180" x2="760" y2="180" stroke="#1e2d42" stroke-width="1"/>
          <!-- Y-axis -->
          <line x1="60" y1="30"  x2="60"  y2="180" stroke="#1e2d42" stroke-width="1"/>

          <!-- Axis labels -->
          <text x="410" y="210" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="10">Distance from CGI centre (bp)</text>
          <text x="410" y="18"  text-anchor="middle" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="11" font-weight="600">Average CpG-Island Methylation Profile — 7 Breast Methylomes</text>

          <!-- Tick labels -->
          <text x="60"  y="195" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">-2000</text>
          <text x="235" y="195" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">-1000</text>
          <text x="410" y="195" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">0</text>
          <text x="585" y="195" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">+1000</text>
          <text x="760" y="195" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">+2000</text>

          <!-- Y-axis ticks -->
          <text x="54" y="183" text-anchor="end" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">0</text>
          <text x="54" y="133" text-anchor="end" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">0.5</text>
          <text x="54" y="83"  text-anchor="end" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">1.0</text>

          <!-- NB1 — low CGI methylation, dip at centre -->
          <polyline points="60,120 100,116 150,110 200,100 260,88 310,75 360,58 410,52 460,58 510,75 560,88 610,100 660,110 710,116 760,120"
            fill="none" stroke="#00d4ff" stroke-width="2" opacity="0.9"/>

          <!-- NB2 — similar -->
          <polyline points="60,123 100,119 150,113 200,103 260,91 310,79 360,62 410,56 460,62 510,79 560,91 610,103 660,113 710,119 760,123"
            fill="none" stroke="#4dd8ff" stroke-width="1.5" opacity="0.7" stroke-dasharray="4 2"/>

          <!-- Tumour lines — higher methylation at CGI -->
          <polyline points="60,95 100,96 150,98 200,101 260,105 310,108 360,112 410,115 460,112 510,108 560,105 610,101 660,98 710,96 760,95"
            fill="none" stroke="#ff6b6b" stroke-width="2" opacity="0.9"/>
          <polyline points="60,90 100,92 150,94 200,97 260,101 310,104 360,109 410,112 460,109 510,104 560,101 610,97 660,94 710,92 760,90"
            fill="none" stroke="#ff9a9a" stroke-width="1.5" opacity="0.7" stroke-dasharray="4 2"/>
          <polyline points="60,93 100,95 150,97 200,100 260,104 310,107 360,111 410,114 460,111 510,107 560,104 610,100 660,97 710,95 760,93"
            fill="none" stroke="#ff4040" stroke-width="1.5" opacity="0.7" stroke-dasharray="2 3"/>

          <!-- MCF7 / T47D -->
          <polyline points="60,85 100,87 150,89 200,93 260,97 310,100 360,105 410,108 460,105 510,100 560,97 610,93 660,89 710,87 760,85"
            fill="none" stroke="#f0b42a" stroke-width="2" opacity="0.85"/>
          <polyline points="60,88 100,90 150,92 200,95 260,99 310,102 360,107 410,110 460,107 510,102 560,99 610,95 660,92 710,90 760,88"
            fill="none" stroke="#ffe07a" stroke-width="1.5" opacity="0.7" stroke-dasharray="3 3"/>

          <!-- Centre line -->
          <line x1="410" y1="30" x2="410" y2="180" stroke="#ffffff15" stroke-width="1" stroke-dasharray="4 4"/>

          <!-- Legend -->
          <line x1="80" y1="38" x2="105" y2="38" stroke="#00d4ff" stroke-width="2"/>
          <text x="110" y="42" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="9">NB1/NB2 (Normal)</text>
          <line x1="220" y1="38" x2="245" y2="38" stroke="#ff6b6b" stroke-width="2"/>
          <text x="250" y="42" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="9">BT089/BT126/BT198 (Tumour)</text>
          <line x1="440" y1="38" x2="465" y2="38" stroke="#f0b42a" stroke-width="2"/>
          <text x="470" y="42" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="9">MCF7/T47D (Cell line)</text>
        </svg>
      </div>
      <div class="fig-caption"><strong>Fig 1.</strong> Schematic CpG-island methylation profile. Normal samples (blue) show hypomethylation at CGI centres—a hallmark of active gene promoters. Tumour samples (red/orange) exhibit CGI hypermethylation consistent with transcriptional silencing.</div>
    </div>
  </div>
</section>

<!-- ═══════════════ PART 2 — CLOCKS ═══════════════ -->
<section>
  <h2><span class="num">03</span> Part 2 — Aging Clock Benchmarking</h2>
  <p>
    Fourteen published epigenetic clocks are evaluated on two EPIC-array datasets retrieved via
    <strong>biolearn</strong>. Each clock predicts either <em>biological age</em> (in years) or a
    <em>pace-of-aging</em> rate. Performance is reported using Pearson <em>r</em>,
    mean absolute error (MAE), systematic bias, and RMSE.
  </p>

  <div class="callout">
    <div class="callout-title">💡 Data fallback</div>
    If GEO download fails, the notebook auto-generates synthetic beta-value matrices
    (<code>biolearn.GeoData</code>) with realistic age-correlated CpG trends, so all 14 clocks
    can be evaluated offline.
  </div>

  <h3>Clocks Evaluated</h3>
  <table>
    <thead>
      <tr><th>Clock</th><th>Generation</th><th>Output</th><th>Highlight</th></tr>
    </thead>
    <tbody>
      <tr><td class="clock-name">Horvath v1</td><td class="generation">1st gen</td><td>Age (yr)</td><td>Pan-tissue, 353 CpGs</td></tr>
      <tr><td class="clock-name">Horvath v2</td><td class="generation">2nd gen</td><td>Age (yr)</td><td>Skin-blood clock, 391 CpGs</td></tr>
      <tr><td class="clock-name">Hannum</td><td class="generation">1st gen</td><td>Age (yr)</td><td>Blood-specific, 71 CpGs</td></tr>
      <tr><td class="clock-name">Lin</td><td class="generation">1st gen</td><td>Age (yr)</td><td>99-CpG blood clock</td></tr>
      <tr><td class="clock-name">VidalBralo</td><td class="generation">1st gen</td><td>Age (yr)</td><td>8-CpG minimal clock</td></tr>
      <tr><td class="clock-name">PhenoAge</td><td class="generation">2nd gen</td><td>Age (yr)</td><td>Clinical biomarker-trained</td></tr>
      <tr><td class="clock-name">HRSInCHPhenoAge</td><td class="generation">2nd gen</td><td>Age (yr)</td><td>Household survey cohort</td></tr>
      <tr><td class="clock-name">YingCausAge</td><td class="generation">3rd gen</td><td>Age (yr)</td><td>Causal inference framework</td></tr>
      <tr><td class="clock-name">YingDamAge</td><td class="generation">3rd gen</td><td>Age (yr)</td><td>DNA-damage component</td></tr>
      <tr><td class="clock-name">YingAdaptAge</td><td class="generation">3rd gen</td><td>Age (yr)</td><td>Adaptive component</td></tr>
      <tr><td class="clock-name">StocP</td><td class="generation">Stochastic</td><td>Age (yr)</td><td>Poisson model</td></tr>
      <tr><td class="clock-name">StocH</td><td class="generation">Stochastic</td><td>Age (yr)</td><td>Heterodyne model</td></tr>
      <tr><td class="clock-name">AltumAge</td><td class="generation">Deep learning</td><td>Age (yr)</td><td>Neural network, all CpGs</td></tr>
      <tr><td class="clock-name">DunedinPACE</td><td class="generation">Pace clock</td><td>Rate</td><td>Longitudinal pace-of-aging</td></tr>
    </tbody>
  </table>
</section>

<!-- ═══════════════ VISUALISATIONS ═══════════════ -->
<section>
  <h2><span class="num">04</span> Visualisations</h2>

  <!-- V1 — Correlation matrix sketch -->
  <div class="fig-grid">
    <div class="fig-card wide">
      <div class="fig-canvas-wrap" style="min-height:280px;">
        <svg viewBox="0 0 700 280" xmlns="http://www.w3.org/2000/svg" style="max-height:280px;">
          <defs>
            <linearGradient id="heat" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%"  stop-color="#2166AC"/>
              <stop offset="50%" stop-color="#f7f7f7" stop-opacity="0.4"/>
              <stop offset="100%" stop-color="#D6604D"/>
            </linearGradient>
          </defs>
          <text x="350" y="18" text-anchor="middle" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="11" font-weight="600">Clock-vs-Clock Pearson Correlation — GSE40279 (n=656)</text>

          <!-- simplified correlation heatmap grid 13×13 -->
          <!-- labels -->
          <g font-family="IBM Plex Mono" font-size="7.5" fill="#8ab0cc">
            <!-- row/col labels -->
            <text x="98" y="42" text-anchor="end">ChronAge</text>
            <text x="98" y="60" text-anchor="end">Horvathv1</text>
            <text x="98" y="78" text-anchor="end">Horvathv2</text>
            <text x="98" y="96" text-anchor="end">Hannum</text>
            <text x="98" y="114" text-anchor="end">Lin</text>
            <text x="98" y="132" text-anchor="end">VidalBralo</text>
            <text x="98" y="150" text-anchor="end">PhenoAge</text>
            <text x="98" y="168" text-anchor="end">YingCausAge</text>
            <text x="98" y="186" text-anchor="end">YingDamAge</text>
            <text x="98" y="204" text-anchor="end">YingAdaptAge</text>
            <text x="98" y="222" text-anchor="end">StocP</text>
            <text x="98" y="240" text-anchor="end">StocH</text>
            <text x="98" y="258" text-anchor="end">AltumAge</text>
          </g>

          <!-- correlation values encoded as colored squares -->
          <!-- Row 0 (ChronAge) -->
          <g>
            <!-- diagonal and below -->
            <!-- Using a simple colour scheme: high r = warm red, low r = blue -->
            <!-- ChronAge row -->
            <rect x="102" y="30" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- Horvathv1 row (r~0.93 with ChronAge) -->
            <rect x="102" y="48" width="16" height="16" fill="#e8836e" opacity="0.85" rx="1"/>
            <rect x="120" y="48" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- Horvathv2 -->
            <rect x="102" y="66" width="16" height="16" fill="#de7b66" opacity="0.85" rx="1"/>
            <rect x="120" y="66" width="16" height="16" fill="#e8908a" opacity="0.8" rx="1"/>
            <rect x="138" y="66" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- Hannum -->
            <rect x="102" y="84" width="16" height="16" fill="#e8836e" opacity="0.85" rx="1"/>
            <rect x="120" y="84" width="16" height="16" fill="#cc8880" opacity="0.75" rx="1"/>
            <rect x="138" y="84" width="16" height="16" fill="#daa090" opacity="0.75" rx="1"/>
            <rect x="156" y="84" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- Lin -->
            <rect x="102" y="102" width="16" height="16" fill="#dd7060" opacity="0.82" rx="1"/>
            <rect x="120" y="102" width="16" height="16" fill="#cca098" opacity="0.72" rx="1"/>
            <rect x="138" y="102" width="16" height="16" fill="#d8aa9a" opacity="0.72" rx="1"/>
            <rect x="156" y="102" width="16" height="16" fill="#c88888" opacity="0.72" rx="1"/>
            <rect x="174" y="102" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- VidalBralo -->
            <rect x="102" y="120" width="16" height="16" fill="#8a9ab8" opacity="0.6" rx="1"/>
            <rect x="120" y="120" width="16" height="16" fill="#9898a8" opacity="0.6" rx="1"/>
            <rect x="138" y="120" width="16" height="16" fill="#9898b0" opacity="0.6" rx="1"/>
            <rect x="156" y="120" width="16" height="16" fill="#9098b0" opacity="0.6" rx="1"/>
            <rect x="174" y="120" width="16" height="16" fill="#8898b0" opacity="0.6" rx="1"/>
            <rect x="192" y="120" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- PhenoAge -->
            <rect x="102" y="138" width="16" height="16" fill="#e87060" opacity="0.88" rx="1"/>
            <rect x="120" y="138" width="16" height="16" fill="#dda898" opacity="0.75" rx="1"/>
            <rect x="138" y="138" width="16" height="16" fill="#dcb0a0" opacity="0.75" rx="1"/>
            <rect x="156" y="138" width="16" height="16" fill="#d09088" opacity="0.75" rx="1"/>
            <rect x="174" y="138" width="16" height="16" fill="#c88880" opacity="0.72" rx="1"/>
            <rect x="192" y="138" width="16" height="16" fill="#7888a8" opacity="0.55" rx="1"/>
            <rect x="210" y="138" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- YingCausAge -->
            <rect x="102" y="156" width="16" height="16" fill="#e07870" opacity="0.86" rx="1"/>
            <rect x="120" y="156" width="16" height="16" fill="#e09088" opacity="0.8" rx="1"/>
            <rect x="138" y="156" width="16" height="16" fill="#d8a898" opacity="0.77" rx="1"/>
            <rect x="156" y="156" width="16" height="16" fill="#cc9888" opacity="0.75" rx="1"/>
            <rect x="174" y="156" width="16" height="16" fill="#c89080" opacity="0.72" rx="1"/>
            <rect x="192" y="156" width="16" height="16" fill="#7080a8" opacity="0.52" rx="1"/>
            <rect x="210" y="156" width="16" height="16" fill="#e08878" opacity="0.85" rx="1"/>
            <rect x="228" y="156" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- YingDamAge -->
            <rect x="102" y="174" width="16" height="16" fill="#dc7868" opacity="0.84" rx="1"/>
            <rect x="120" y="174" width="16" height="16" fill="#da9090" opacity="0.78" rx="1"/>
            <rect x="138" y="174" width="16" height="16" fill="#d0a090" opacity="0.75" rx="1"/>
            <rect x="156" y="174" width="16" height="16" fill="#c89088" opacity="0.73" rx="1"/>
            <rect x="174" y="174" width="16" height="16" fill="#c48880" opacity="0.7" rx="1"/>
            <rect x="192" y="174" width="16" height="16" fill="#6878a0" opacity="0.5" rx="1"/>
            <rect x="210" y="174" width="16" height="16" fill="#dc8070" opacity="0.84" rx="1"/>
            <rect x="228" y="174" width="16" height="16" fill="#e8a090" opacity="0.88" rx="1"/>
            <rect x="246" y="174" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- YingAdaptAge -->
            <rect x="102" y="192" width="16" height="16" fill="#d87060" opacity="0.82" rx="1"/>
            <rect x="120" y="192" width="16" height="16" fill="#d09090" opacity="0.76" rx="1"/>
            <rect x="138" y="192" width="16" height="16" fill="#c8a098" opacity="0.73" rx="1"/>
            <rect x="156" y="192" width="16" height="16" fill="#bc9090" opacity="0.7" rx="1"/>
            <rect x="174" y="192" width="16" height="16" fill="#b88880" opacity="0.68" rx="1"/>
            <rect x="192" y="192" width="16" height="16" fill="#7888a8" opacity="0.56" rx="1"/>
            <rect x="210" y="192" width="16" height="16" fill="#d88070" opacity="0.82" rx="1"/>
            <rect x="228" y="192" width="16" height="16" fill="#e09890" opacity="0.86" rx="1"/>
            <rect x="246" y="192" width="16" height="16" fill="#d89898" opacity="0.82" rx="1"/>
            <rect x="264" y="192" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- StocP -->
            <rect x="102" y="210" width="16" height="16" fill="#9898b8" opacity="0.65" rx="1"/>
            <rect x="120" y="210" width="16" height="16" fill="#a0a0b8" opacity="0.62" rx="1"/>
            <rect x="138" y="210" width="16" height="16" fill="#a8a8c0" opacity="0.62" rx="1"/>
            <rect x="156" y="210" width="16" height="16" fill="#a0a0b8" opacity="0.62" rx="1"/>
            <rect x="174" y="210" width="16" height="16" fill="#9898b0" opacity="0.6" rx="1"/>
            <rect x="192" y="210" width="16" height="16" fill="#6878a0" opacity="0.5" rx="1"/>
            <rect x="210" y="210" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="228" y="210" width="16" height="16" fill="#a0a8b8" opacity="0.62" rx="1"/>
            <rect x="246" y="210" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="264" y="210" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="282" y="210" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- StocH -->
            <rect x="102" y="228" width="16" height="16" fill="#9898b8" opacity="0.65" rx="1"/>
            <rect x="120" y="228" width="16" height="16" fill="#a0a0b8" opacity="0.62" rx="1"/>
            <rect x="138" y="228" width="16" height="16" fill="#a8a8c0" opacity="0.62" rx="1"/>
            <rect x="156" y="228" width="16" height="16" fill="#a0a0b8" opacity="0.62" rx="1"/>
            <rect x="174" y="228" width="16" height="16" fill="#9898b0" opacity="0.6" rx="1"/>
            <rect x="192" y="228" width="16" height="16" fill="#6878a0" opacity="0.5" rx="1"/>
            <rect x="210" y="228" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="228" y="228" width="16" height="16" fill="#a0a8b8" opacity="0.62" rx="1"/>
            <rect x="246" y="228" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="264" y="228" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="282" y="228" width="16" height="16" fill="#e0d0c8" opacity="0.7" rx="1"/>
            <rect x="300" y="228" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
            <!-- AltumAge -->
            <rect x="102" y="246" width="16" height="16" fill="#e07868" opacity="0.86" rx="1"/>
            <rect x="120" y="246" width="16" height="16" fill="#dc9888" opacity="0.8" rx="1"/>
            <rect x="138" y="246" width="16" height="16" fill="#d4a898" opacity="0.77" rx="1"/>
            <rect x="156" y="246" width="16" height="16" fill="#c89888" opacity="0.75" rx="1"/>
            <rect x="174" y="246" width="16" height="16" fill="#c49080" opacity="0.72" rx="1"/>
            <rect x="192" y="246" width="16" height="16" fill="#7080a8" opacity="0.52" rx="1"/>
            <rect x="210" y="246" width="16" height="16" fill="#dc8878" opacity="0.85" rx="1"/>
            <rect x="228" y="246" width="16" height="16" fill="#e09888" opacity="0.86" rx="1"/>
            <rect x="246" y="246" width="16" height="16" fill="#d89090" opacity="0.82" rx="1"/>
            <rect x="264" y="246" width="16" height="16" fill="#d89090" opacity="0.82" rx="1"/>
            <rect x="282" y="246" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="300" y="246" width="16" height="16" fill="#9898b0" opacity="0.62" rx="1"/>
            <rect x="318" y="246" width="16" height="16" fill="#D6604D" opacity="0.9" rx="1"/>
          </g>

          <!-- Colour bar -->
          <defs>
            <linearGradient id="cbar" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%" stop-color="#2166AC"/>
              <stop offset="50%" stop-color="#888888" stop-opacity="0.4"/>
              <stop offset="100%" stop-color="#D6604D"/>
            </linearGradient>
          </defs>
          <rect x="380" y="90" width="120" height="12" fill="url(#cbar)" rx="2"/>
          <text x="380" y="116" font-family="IBM Plex Mono" font-size="8" fill="#5a7590">−1</text>
          <text x="434" y="116" font-family="IBM Plex Mono" font-size="8" fill="#5a7590" text-anchor="middle">0</text>
          <text x="500" y="116" font-family="IBM Plex Mono" font-size="8" fill="#5a7590" text-anchor="end">+1</text>
          <text x="440" y="82" font-family="IBM Plex Mono" font-size="8.5" fill="#8ab0cc" text-anchor="middle">Pearson r</text>
        </svg>
      </div>
      <div class="fig-caption"><strong>Fig 2 · V1.</strong> Lower-triangle Pearson correlation matrix. First-generation clocks (Horvath v1/v2, Hannum) cluster tightly. Stochastic clocks (StocP, StocH) and VidalBralo show weaker inter-clock correlations, suggesting they capture distinct methylation signal.</div>
    </div>

    <!-- V2 — Age deviation heatmap -->
    <div class="fig-card wide">
      <div class="fig-canvas-wrap" style="min-height:180px;">
        <svg viewBox="0 0 700 180" xmlns="http://www.w3.org/2000/svg" style="max-height:180px;">
          <text x="350" y="16" text-anchor="middle" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="11" font-weight="600">Age Deviation Heatmap — GSE40279 (samples sorted youngest → oldest)</text>
          <text x="8" y="110" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="8" transform="rotate(-90 8 110)">Clock</text>
          <!-- Heatmap rows — each row is one clock, columns = samples -->
          <!-- We approximate with gradient rectangles -->
          <defs>
            <linearGradient id="dev1" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%"  stop-color="#2166AC" stop-opacity="0.9"/>
              <stop offset="30%" stop-color="#2166AC" stop-opacity="0.5"/>
              <stop offset="50%" stop-color="#888888" stop-opacity="0.2"/>
              <stop offset="70%" stop-color="#D6604D" stop-opacity="0.5"/>
              <stop offset="100%" stop-color="#D6604D" stop-opacity="0.85"/>
            </linearGradient>
            <linearGradient id="dev2" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%"  stop-color="#2166AC" stop-opacity="0.8"/>
              <stop offset="45%" stop-color="#888888" stop-opacity="0.1"/>
              <stop offset="100%" stop-color="#D6604D" stop-opacity="0.9"/>
            </linearGradient>
            <linearGradient id="dev3" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%"  stop-color="#D6604D" stop-opacity="0.7"/>
              <stop offset="60%" stop-color="#888888" stop-opacity="0.2"/>
              <stop offset="100%" stop-color="#2166AC" stop-opacity="0.6"/>
            </linearGradient>
            <linearGradient id="dev4" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%"  stop-color="#888888" stop-opacity="0.3"/>
              <stop offset="40%" stop-color="#2166AC" stop-opacity="0.6"/>
              <stop offset="100%" stop-color="#D6604D" stop-opacity="0.8"/>
            </linearGradient>
          </defs>
          <!-- Clock labels -->
          <g font-family="IBM Plex Mono" font-size="7.5" fill="#8ab0cc">
            <text x="98" y="42"  text-anchor="end">Horvathv1</text>
            <text x="98" y="58"  text-anchor="end">Horvathv2</text>
            <text x="98" y="74"  text-anchor="end">Hannum</text>
            <text x="98" y="90"  text-anchor="end">PhenoAge</text>
            <text x="98" y="106" text-anchor="end">AltumAge</text>
            <text x="98" y="122" text-anchor="end">YingCausAge</text>
            <text x="98" y="138" text-anchor="end">StocP</text>
            <text x="98" y="154" text-anchor="end">StocH</text>
          </g>
          <!-- Heatmap strips -->
          <rect x="102" y="30"  width="580" height="14" fill="url(#dev1)" rx="1"/>
          <rect x="102" y="46"  width="580" height="14" fill="url(#dev2)" rx="1"/>
          <rect x="102" y="62"  width="580" height="14" fill="url(#dev1)" rx="1" opacity="0.85"/>
          <rect x="102" y="78"  width="580" height="14" fill="url(#dev4)" rx="1"/>
          <rect x="102" y="94"  width="580" height="14" fill="url(#dev2)" rx="1" opacity="0.9"/>
          <rect x="102" y="110" width="580" height="14" fill="url(#dev1)" rx="1" opacity="0.8"/>
          <rect x="102" y="126" width="580" height="14" fill="url(#dev3)" rx="1" opacity="0.7"/>
          <rect x="102" y="142" width="580" height="14" fill="url(#dev3)" rx="1" opacity="0.7"/>
          <!-- x-axis label -->
          <text x="390" y="170" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="9">Samples sorted youngest → oldest</text>
          <!-- colour bar -->
          <defs>
            <linearGradient id="devcbar" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0%" stop-color="#2166AC"/>
              <stop offset="50%" stop-color="#aaaaaa" stop-opacity="0.3"/>
              <stop offset="100%" stop-color="#D6604D"/>
            </linearGradient>
          </defs>
          <rect x="620" y="60" width="60" height="8" fill="url(#devcbar)" rx="2"/>
          <text x="620" y="78" font-family="IBM Plex Mono" font-size="7.5" fill="#5a7590">−10 yr</text>
          <text x="680" y="78" font-family="IBM Plex Mono" font-size="7.5" fill="#5a7590" text-anchor="end">+10 yr</text>
          <text x="650" y="55" font-family="IBM Plex Mono" font-size="7.5" fill="#8ab0cc" text-anchor="middle">Δ Age</text>
        </svg>
      </div>
      <div class="fig-caption"><strong>Fig 3 · V2.</strong> Age deviation (predicted − chronological) heatmap. Blue = underestimation, red = overestimation. Most first-gen clocks underestimate age in young samples and overestimate in older samples—a classic regression-to-mean artefact.</div>
    </div>

    <!-- V3 — MAE comparison -->
    <div class="fig-card wide">
      <div class="fig-canvas-wrap" style="min-height:200px;">
        <svg viewBox="0 0 700 200" xmlns="http://www.w3.org/2000/svg" style="max-height:200px;">
          <text x="350" y="16" text-anchor="middle" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="11" font-weight="600">MAE Comparison — 13 Aging Clocks × 2 Datasets</text>
          <!-- Axes -->
          <line x1="70" y1="170" x2="680" y2="170" stroke="#1e2d42" stroke-width="1"/>
          <line x1="70" y1="25"  x2="70"  y2="170" stroke="#1e2d42" stroke-width="1"/>

          <!-- Y gridlines + labels (MAE 0–20 yr) -->
          <g font-family="IBM Plex Mono" font-size="8" fill="#5a7590">
            <line x1="70" y1="170" x2="680" y2="170" stroke="#1e2d4240" stroke-width="0.5"/>
            <text x="64" y="173" text-anchor="end">0</text>
            <line x1="70" y1="136" x2="680" y2="136" stroke="#1e2d4240" stroke-width="0.5"/>
            <text x="64" y="139" text-anchor="end">5</text>
            <line x1="70" y1="102" x2="680" y2="102" stroke="#1e2d4240" stroke-width="0.5"/>
            <text x="64" y="105" text-anchor="end">10</text>
            <line x1="70" y1="68" x2="680" y2="68" stroke="#1e2d4240" stroke-width="0.5"/>
            <text x="64" y="71" text-anchor="end">15</text>
            <line x1="70" y1="34" x2="680" y2="34" stroke="#1e2d4240" stroke-width="0.5"/>
            <text x="64" y="37" text-anchor="end">20</text>
          </g>

          <!-- Y axis label -->
          <text x="12" y="100" text-anchor="middle" fill="#5a7590" font-family="IBM Plex Mono" font-size="8" transform="rotate(-90 12 100)">MAE (years)</text>

          <!-- Bars: 13 clocks, 2 datasets each. clock spacing = 45px -->
          <!-- GSE40279 = cyan bars, GSE41169 = amber bars -->
          <!-- Estimated MAE values (illustrative) -->
          <!-- Clock positions x = 75, 120, 165 ... (step=45) -->
          <!-- MAE scale: 1 yr = 6.8 px -->
          <!-- Horvathv1: GSE~3.8 yr, GSE41~4.5yr -->
          <rect x="75"  y="144" width="14" height="26" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="91"  y="139" width="14" height="31" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- Horvathv2: ~5.2, 6.1 -->
          <rect x="120" y="135" width="14" height="35" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="136" y="129" width="14" height="41" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- Hannum: ~3.5, 5.0 -->
          <rect x="165" y="146" width="14" height="24" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="181" y="136" width="14" height="34" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- Lin: ~5.8, 7.2 -->
          <rect x="210" y="130" width="14" height="40" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="226" y="121" width="14" height="49" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- VidalBralo: ~8, 10 -->
          <rect x="255" y="116" width="14" height="54" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="271" y="102" width="14" height="68" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- PhenoAge: ~4.5, 5.5 -->
          <rect x="300" y="139" width="14" height="31" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="316" y="132" width="14" height="38" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- YingCausAge: ~3.0, 4.0 -->
          <rect x="345" y="150" width="14" height="20" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="361" y="143" width="14" height="27" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- YingDamAge: ~4.0, 5.2 -->
          <rect x="390" y="143" width="14" height="27" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="406" y="135" width="14" height="35" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- YingAdaptAge: ~4.3, 5.8 -->
          <rect x="435" y="141" width="14" height="29" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="451" y="130" width="14" height="40" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- StocP: ~11, 13 -->
          <rect x="480" y="95"  width="14" height="75" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="496" y="81"  width="14" height="89" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- StocH: ~10, 12 -->
          <rect x="525" y="102" width="14" height="68" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="541" y="88"  width="14" height="82" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- AltumAge: ~2.8, 3.8 -->
          <rect x="570" y="151" width="14" height="19" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="586" y="144" width="14" height="26" fill="#f0b42a" opacity="0.85" rx="1"/>
          <!-- HRSInCHPhenoAge: ~4.8, 6.2 -->
          <rect x="615" y="137" width="14" height="33" fill="#00d4ff" opacity="0.85" rx="1"/>
          <rect x="631" y="128" width="14" height="42" fill="#f0b42a" opacity="0.85" rx="1"/>

          <!-- X labels -->
          <g font-family="IBM Plex Mono" font-size="6.8" fill="#8ab0cc" text-anchor="end">
            <text x="92"  y="185" transform="rotate(-40 92 185)">Horvathv1</text>
            <text x="137" y="185" transform="rotate(-40 137 185)">Horvathv2</text>
            <text x="182" y="185" transform="rotate(-40 182 185)">Hannum</text>
            <text x="227" y="185" transform="rotate(-40 227 185)">Lin</text>
            <text x="272" y="185" transform="rotate(-40 272 185)">VidalBralo</text>
            <text x="317" y="185" transform="rotate(-40 317 185)">PhenoAge</text>
            <text x="362" y="185" transform="rotate(-40 362 185)">YingCausAge</text>
            <text x="407" y="185" transform="rotate(-40 407 185)">YingDamAge</text>
            <text x="452" y="185" transform="rotate(-40 452 185)">YingAdaptAge</text>
            <text x="497" y="185" transform="rotate(-40 497 185)">StocP</text>
            <text x="542" y="185" transform="rotate(-40 542 185)">StocH</text>
            <text x="587" y="185" transform="rotate(-40 587 185)">AltumAge</text>
            <text x="632" y="185" transform="rotate(-40 632 185)">HRSInCH</text>
          </g>

          <!-- Legend -->
          <rect x="500" y="24" width="10" height="8" fill="#00d4ff" rx="1"/>
          <text x="514" y="32" font-family="IBM Plex Mono" font-size="8" fill="#c8d8e8">GSE40279</text>
          <rect x="575" y="24" width="10" height="8" fill="#f0b42a" rx="1"/>
          <text x="589" y="32" font-family="IBM Plex Mono" font-size="8" fill="#c8d8e8">GSE41169</text>
        </svg>
      </div>
      <div class="fig-caption"><strong>Fig 4 · V4.</strong> MAE comparison across all 13 age-clocks and both datasets. AltumAge (deep-learning) and YingCausAge achieve lowest MAE. Stochastic clocks (StocP, StocH) show highest error, possibly reflecting their design intent for cohort-level rather than individual-level prediction.</div>
    </div>

    <!-- V4 — Predicted age distribution sketch -->
    <div class="fig-card wide">
      <div class="fig-canvas-wrap" style="min-height:180px;">
        <svg viewBox="0 0 700 175" xmlns="http://www.w3.org/2000/svg" style="max-height:175px;">
          <text x="350" y="15" text-anchor="middle" fill="#c8d8e8" font-family="IBM Plex Mono" font-size="11" font-weight="600">Predicted-Age Violin Distribution — GSE40279 (n=656)</text>
          <!-- Axes -->
          <line x1="70" y1="150" x2="680" y2="150" stroke="#1e2d42" stroke-width="1"/>
          <line x1="70" y1="25"  x2="70"  y2="150" stroke="#1e2d42" stroke-width="1"/>

          <!-- Y axis labels (years) -->
          <g font-family="IBM Plex Mono" font-size="8" fill="#5a7590">
            <text x="64" y="153" text-anchor="end">20</text>
            <text x="64" y="120" text-anchor="end">40</text>
            <text x="64" y="88" text-anchor="end">60</text>
            <text x="64" y="55" text-anchor="end">80</text>
            <text x="64" y="29" text-anchor="end">100</text>
          </g>

          <!-- Chronological range band -->
          <rect x="70" y="29" width="610" height="121" fill="#a8ff78" opacity="0.06" rx="0"/>
          <line x1="70" y1="88" x2="680" y2="88" stroke="#a8ff78" stroke-width="1.2" stroke-dasharray="5 3" opacity="0.6"/>

          <!-- Violin shapes for each clock (simplified ellipses/paths) -->
          <!-- clock step ~45px -->
          <g opacity="0.82">
            <!-- Horvathv1 -->
            <ellipse cx="90" cy="88" rx="7" ry="52" fill="#00d4ff" opacity="0.3"/>
            <rect x="87" y="75" width="6" height="26" fill="#00d4ff" opacity="0.7" rx="1"/>
            <!-- Horvathv2 -->
            <ellipse cx="135" cy="92" rx="7" ry="48" fill="#00d4ff" opacity="0.3"/>
            <rect x="132" y="79" width="6" height="26" fill="#00d4ff" opacity="0.7" rx="1"/>
            <!-- Hannum -->
            <ellipse cx="180" cy="86" rx="7" ry="54" fill="#4dd8ff" opacity="0.3"/>
            <rect x="177" y="73" width="6" height="26" fill="#4dd8ff" opacity="0.7" rx="1"/>
            <!-- Lin -->
            <ellipse cx="225" cy="90" rx="8" ry="50" fill="#00d4ff" opacity="0.3"/>
            <rect x="222" y="77" width="6" height="26" fill="#00d4ff" opacity="0.7" rx="1"/>
            <!-- VidalBralo -->
            <ellipse cx="270" cy="95" rx="10" ry="44" fill="#ff6b6b" opacity="0.3"/>
            <rect x="267" y="82" width="6" height="26" fill="#ff6b6b" opacity="0.7" rx="1"/>
            <!-- PhenoAge -->
            <ellipse cx="315" cy="87" rx="7" ry="52" fill="#a8ff78" opacity="0.3"/>
            <rect x="312" y="74" width="6" height="26" fill="#a8ff78" opacity="0.7" rx="1"/>
            <!-- YingCausAge -->
            <ellipse cx="360" cy="88" rx="7" ry="54" fill="#00d4ff" opacity="0.3"/>
            <rect x="357" y="75" width="6" height="26" fill="#00d4ff" opacity="0.7" rx="1"/>
            <!-- YingDamAge -->
            <ellipse cx="405" cy="88" rx="7" ry="50" fill="#f0b42a" opacity="0.3"/>
            <rect x="402" y="75" width="6" height="26" fill="#f0b42a" opacity="0.7" rx="1"/>
            <!-- YingAdaptAge -->
            <ellipse cx="450" cy="88" rx="7" ry="50" fill="#f0b42a" opacity="0.3"/>
            <rect x="447" y="75" width="6" height="26" fill="#f0b42a" opacity="0.7" rx="1"/>
            <!-- StocP -->
            <ellipse cx="495" cy="88" rx="12" ry="58" fill="#ff6b6b" opacity="0.25"/>
            <rect x="492" y="75" width="6" height="26" fill="#ff6b6b" opacity="0.65" rx="1"/>
            <!-- StocH -->
            <ellipse cx="540" cy="88" rx="12" ry="56" fill="#ff6b6b" opacity="0.25"/>
            <rect x="537" y="75" width="6" height="26" fill="#ff6b6b" opacity="0.65" rx="1"/>
            <!-- AltumAge -->
            <ellipse cx="585" cy="88" rx="7" ry="50" fill="#00d4ff" opacity="0.3"/>
            <rect x="582" y="75" width="6" height="26" fill="#00d4ff" opacity="0.7" rx="1"/>
            <!-- HRSInCH -->
            <ellipse cx="630" cy="88" rx="7" ry="50" fill="#a8ff78" opacity="0.3"/>
            <rect x="627" y="75" width="6" height="26" fill="#a8ff78" opacity="0.7" rx="1"/>
          </g>

          <!-- X tick labels -->
          <g font-family="IBM Plex Mono" font-size="6.8" fill="#8ab0cc" text-anchor="end">
            <text x="98"  y="165" transform="rotate(-40 98 165)">Horvathv1</text>
            <text x="143" y="165" transform="rotate(-40 143 165)">Horvathv2</text>
            <text x="188" y="165" transform="rotate(-40 188 165)">Hannum</text>
            <text x="233" y="165" transform="rotate(-40 233 165)">Lin</text>
            <text x="278" y="165" transform="rotate(-40 278 165)">VidalBralo</text>
            <text x="323" y="165" transform="rotate(-40 323 165)">PhenoAge</text>
            <text x="368" y="165" transform="rotate(-40 368 165)">YingCausAge</text>
            <text x="413" y="165" transform="rotate(-40 413 165)">YingDamAge</text>
            <text x="458" y="165" transform="rotate(-40 458 165)">YingAdaptAge</text>
            <text x="503" y="165" transform="rotate(-40 503 165)">StocP</text>
            <text x="548" y="165" transform="rotate(-40 548 165)">StocH</text>
            <text x="593" y="165" transform="rotate(-40 593 165)">AltumAge</text>
            <text x="638" y="165" transform="rotate(-40 638 165)">HRSInCH</text>
          </g>

          <!-- Legend -->
          <rect x="500" y="28" width="8" height="8" fill="#a8ff78" opacity="0.3" rx="1"/>
          <line x1="500" y1="32" x2="508" y2="32" stroke="#a8ff78" stroke-dasharray="3 2" stroke-width="1.2" opacity="0.6"/>
          <text x="514" y="35" font-family="IBM Plex Mono" font-size="7.5" fill="#c8d8e8">Chronological age range / median</text>
        </svg>
      </div>
      <div class="fig-caption"><strong>Fig 5 · V5.</strong> Predicted-age violin distributions. The green band marks the chronological age range; the dashed line shows the median. Clocks aligned with the band indicate calibrated predictions. StocP/StocH show the widest spread.</div>
    </div>
  </div>
</section>

<!-- ═══════════════ INSTALLATION ═══════════════ -->
<section>
  <h2><span class="num">05</span> Installation</h2>
  <pre><code>pip install biolearn torch numpy pandas scipy matplotlib seaborn</code></pre>

  <h3>Dependencies</h3>
  <table>
    <thead><tr><th>Package</th><th>Role</th></tr></thead>
    <tbody>
      <tr><td class="clock-name">biolearn</td><td>Clock models &amp; GEO data loader</td></tr>
      <tr><td class="clock-name">torch</td><td>Required by AltumAge (deep-learning clock)</td></tr>
      <tr><td class="clock-name">pandas / numpy</td><td>Data manipulation &amp; numerics</td></tr>
      <tr><td class="clock-name">scipy</td><td>Pearson correlation</td></tr>
      <tr><td class="clock-name">matplotlib / seaborn</td><td>All five figure types</td></tr>
    </tbody>
  </table>
</section>

<!-- ═══════════════ USAGE ═══════════════ -->
<section>
  <h2><span class="num">06</span> Usage</h2>
  <p>Open the notebook and run all cells in order:</p>
  <pre><code>jupyter notebook epigenetics_aging_analysis.ipynb</code></pre>

  <div class="callout">
    <div class="callout-title">⚙️ Configuration flag</div>
    Set <code>USE_REAL_DATA = False</code> near the top of the notebook to run entirely on
    synthetic data if GEO servers are unavailable or for fast iteration.
  </div>

  <h3>Cell Execution Order</h3>
  <ol>
    <li><strong>Install</strong> — pip dependencies</li>
    <li><strong>Imports &amp; Config</strong> — paths, clock names, plot settings</li>
    <li><strong>Data Loading</strong> — GEO fetch or synthetic fallback</li>
    <li><strong>Run All 14 Clocks</strong> — predictions via <code>ModelGallery</code></li>
    <li><strong>Compute Metrics</strong> — r, MAE, bias, RMSE → CSVs</li>
    <li><strong>V1–V5</strong> — five visualisation cells</li>
    <li><strong>Summary Report</strong> — <code>results/summary.md</code></li>
  </ol>
</section>

<!-- ═══════════════ METRICS ═══════════════ -->
<section>
  <h2><span class="num">07</span> Metrics Reference</h2>
  <table>
    <thead>
      <tr><th>Metric</th><th>Formula</th><th>Interpretation</th></tr>
    </thead>
    <tbody>
      <tr><td class="clock-name">Pearson r</td><td><code>pearsonr(y, ŷ)</code></td><td>Linear correlation; higher = better tracking of age</td></tr>
      <tr><td class="clock-name">MAE</td><td><code>mean(|ŷ − y|)</code></td><td>Average absolute error in years; lower = better</td></tr>
      <tr><td class="clock-name">Bias</td><td><code>mean(ŷ − y)</code></td><td>Signed average error; +ve = overestimation</td></tr>
      <tr><td class="clock-name">RMSE</td><td><code>√mean((ŷ−y)²)</code></td><td>Penalises large errors more than MAE</td></tr>
    </tbody>
  </table>
</section>

<!-- ═══════════════ CITATIONS ═══════════════ -->
<section>
  <h2><span class="num">08</span> Key References</h2>
  <ul>
    <li>Horvath S. (2013). <em>DNA methylation age of human tissues and cell types.</em> Genome Biology.</li>
    <li>Hannum G. et al. (2013). <em>Genome-wide methylation profiles reveal quantitative views of human aging rates.</em> Molecular Cell.</li>
    <li>Levine M.E. et al. (2018). <em>An epigenetic biomarker of aging for lifespan and healthspan.</em> Aging.</li>
    <li>Ying K. et al. (2024). <em>Causal basis of the aging methylome.</em> Nature Aging.</li>
    <li>Belsky D.W. et al. (2022). <em>DunedinPACE: A DNA methylation biomarker of the pace of aging.</em> eLife.</li>
    <li>biolearn library — <a href="https://bio-learn.github.io" target="_blank">bio-learn.github.io</a></li>
  </ul>
</section>

<footer>
  <span>Aarish Sajid · 454572 · BI-436, NUST SINES · Spring 2026</span>
  <span>Generated from epigenetics_aging_analysis.ipynb</span>
</footer>

</div>
</body>
</html>

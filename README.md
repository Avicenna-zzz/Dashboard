<html lang="id">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>Premium Dashboard PISA 2022 — Matematika</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg: #09090b;          /* Latar belakang sangat gelap */
  --surface: #18181b;     /* Warna card/panel */
  --surface2: #27272a;    /* Warna elemen hover/aksen */
  --border: #3f3f46;      /* Garis pemisah */
  --text: #f4f4f5;        /* Teks utama (putih terang) */
  --muted: #a1a1aa;       /* Teks redup */
  --subtle: #71717a;      /* Teks sangat redup */
  
  /* Palet Warna Modern */
  --blue: #3b82f6; 
  --green: #10b981; 
  --pink: #ec4899; 
  --amber: #f59e0b;
  --purple: #8b5cf6; 
  --teal: #14b8a6; 
  --red: #ef4444;
  --font: 'Plus Jakarta Sans', sans-serif;
}

body{background:var(--bg);color:var(--text);font-family:var(--font);min-height:100vh;overflow-x:hidden}

/* ── Layout & Sidebar ── */
.layout{display:flex;min-height:100vh}
.sidebar{width:250px;flex-shrink:0;background:var(--bg);border-right:1px solid rgba(255,255,255,0.08);
  display:flex;flex-direction:column;padding:24px 18px;gap:24px;position:sticky;top:0;height:100vh;overflow-y:auto}
.brand-logo{font-size:24px;font-weight:800;color:var(--text);letter-spacing:-0.5px}
.brand-logo span{color:var(--blue)}
.brand-sub{font-size:11px;color:var(--muted);margin-top:4px;font-weight:500;letter-spacing:0.5px;text-transform:uppercase}
.nav-group-label{font-size:10px;text-transform:uppercase;letter-spacing:1.5px;color:var(--subtle);margin-bottom:8px;padding-left:10px;font-weight:700;margin-top:10px}
.nav-btn{width:100%;text-align:left;background:transparent;border:none;color:var(--muted);
  font-family:var(--font);font-size:13px;font-weight:500;padding:12px 14px;border-radius:10px;cursor:pointer;
  display:flex;align-items:center;gap:10px;transition:all .25s ease;margin-bottom:4px}
.nav-btn:hover{background:rgba(255,255,255,0.05);color:var(--text);transform:translateX(4px)}
.nav-btn.active{background:linear-gradient(90deg, rgba(59,130,246,0.15) 0%, transparent 100%);color:var(--blue);font-weight:600;border-left:3px solid var(--blue)}
.dot{display:inline-block;width:8px;height:8px;border-radius:50%;flex-shrink:0}

/* ── Main & Topbar (Glassmorphism) ── */
.main{flex:1;display:flex;flex-direction:column;min-width:0}
.topbar{position:sticky;top:0;z-index:50;background:rgba(9,9,11,0.7);backdrop-filter:blur(16px);
  border-bottom:1px solid rgba(255,255,255,0.08);padding:16px 28px;display:flex;align-items:center;justify-content:space-between}
.topbar-title{font-weight:700;font-size:17px;letter-spacing:-0.3px}

/* ── Content Sections ── */
.content{padding:28px;flex:1;position:relative;}
.section{display:none;animation:fadeIn .4s ease-out}.section.active{display:block}
@keyframes fadeIn{from{opacity:0;transform:translateY(15px)}to{opacity:1;transform:translateY(0)}}

/* ── Metrics & Cards (Premium Gradients) ── */
.metrics{display:grid;grid-template-columns:repeat(auto-fit,minmax(210px,1fr));gap:18px;margin-bottom:24px}
.metric{background:linear-gradient(145deg, var(--surface), rgba(39,39,42,0.4));border:1px solid rgba(255,255,255,0.06);
  border-radius:16px;padding:22px;position:relative;overflow:hidden;box-shadow:0 10px 15px -3px rgba(0,0,0,0.2)}
.metric::before{content:'';position:absolute;top:0;left:0;width:100%;height:3px}
.metric.m-blue::before{background:var(--blue)}
.metric.m-green::before{background:var(--green)}
.metric.m-pink::before{background:var(--pink)}
.metric.m-amber::before{background:var(--amber)}
.m-lbl{font-size:11px;color:var(--muted);text-transform:uppercase;letter-spacing:1px;margin-bottom:10px;font-weight:700}
.m-val{font-size:36px;font-weight:800;line-height:1;letter-spacing:-1px}
.m-note{font-size:12px;color:var(--subtle);margin-top:8px;font-weight:500}

.card{background:var(--surface);border:1px solid rgba(255,255,255,0.06);border-radius:16px;padding:24px;margin-bottom:24px;
  box-shadow:0 4px 6px -1px rgba(0,0,0,0.1)}
.card-hd{margin-bottom:18px}
.card-title{font-size:16px;font-weight:700;color:var(--text);letter-spacing:-0.3px}
.card-desc{font-size:12px;color:var(--muted);margin-top:6px;font-weight:500}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:24px;margin-bottom:24px}

/* ── Tables ── */
.tbl-card{background:var(--surface);border:1px solid rgba(255,255,255,0.06);border-radius:16px;overflow:hidden;margin-bottom:24px}
.tbl-hd{display:flex;align-items:center;justify-content:space-between;padding:18px 24px;border-bottom:1px solid rgba(255,255,255,0.06);background:rgba(255,255,255,0.01)}
.tbl-title{font-size:15px;font-weight:700;letter-spacing:-0.3px}
.tbl-scroll{overflow-x:auto}
table{width:100%;border-collapse:collapse;font-size:13px}
th{padding:14px 24px;text-align:left;font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:0.8px;color:var(--muted);border-bottom:1px solid rgba(255,255,255,0.06);cursor:pointer;white-space:nowrap;transition:color .2s}
th:hover{color:var(--text)}
td{padding:12px 24px;border-bottom:1px solid rgba(255,255,255,0.03);color:var(--text);font-weight:500}
tr:hover td{background:rgba(255,255,255,0.02)}
.rtag{font-size:10px;font-weight:600;padding:4px 10px;border-radius:20px;background:var(--surface2);color:var(--muted);white-space:nowrap;letter-spacing:0.5px}
.badge{font-size:11px;font-weight:600;padding:4px 10px;border-radius:20px;white-space:nowrap}
.b-above{background:rgba(16,185,129,0.15);color:var(--green)}
.b-avg{background:rgba(245,158,11,0.12);color:var(--amber)}
.b-below{background:rgba(239,68,68,0.15);color:var(--red)}

/* ── Search UI & Profile ── */
.top-actions{display:flex;justify-content:flex-end;margin-bottom:24px}
.search-container{position:relative;width:100%;max-width:380px}
.search-input{width:100%;background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.1);color:var(--text);
  padding:14px 20px;border-radius:30px;font-size:13px;font-family:var(--font);font-weight:500;outline:none;transition:all .3s ease}
.search-input:focus{border-color:var(--blue);background:rgba(255,255,255,0.06);box-shadow:0 0 0 4px rgba(59,130,246,0.15)}
.search-results{position:absolute;top:100%;left:0;right:0;background:var(--surface);border:1px solid var(--border);
  border-radius:16px;margin-top:10px;max-height:280px;overflow-y:auto;z-index:100;display:none;box-shadow:0 20px 40px -10px rgba(0,0,0,0.5)}
.search-item{padding:14px 20px;cursor:pointer;font-size:13px;font-weight:500;border-bottom:1px solid rgba(255,255,255,0.04);display:flex;justify-content:space-between;align-items:center;transition:all .2s}
.search-item:hover{background:rgba(59,130,246,0.1);color:var(--blue)}

.profile-card{background:linear-gradient(180deg, var(--surface) 0%, rgba(24,24,27,0.9) 100%);border:1px solid rgba(255,255,255,0.08);
  border-radius:24px;padding:36px;display:none;animation:fadeIn .4s ease-out;box-shadow:0 20px 40px rgba(0,0,0,0.3)}
.btn-close{float:right;background:rgba(239,68,68,0.1);color:var(--red);border:1px solid rgba(239,68,68,0.2);
  padding:10px 18px;border-radius:10px;cursor:pointer;font-family:var(--font);font-size:12px;font-weight:700;transition:all .2s}
.btn-close:hover{background:var(--red);color:#fff}
.profile-header{display:flex;align-items:center;gap:24px;margin-bottom:32px;border-bottom:1px solid rgba(255,255,255,0.06);padding-bottom:28px;clear:both}
.profile-flag{width:70px;height:70px;border-radius:50%;background:rgba(59,130,246,0.1);display:flex;align-items:center;
  justify-content:center;font-size:30px;border:2px solid var(--blue);box-shadow:0 0 20px rgba(59,130,246,0.2)}
.profile-name{font-size:32px;font-weight:800;letter-spacing:-1px}
.profile-region{font-size:12px;font-weight:700;color:var(--blue);background:rgba(59,130,246,0.15);padding:6px 14px;border-radius:20px;display:inline-block;margin-top:8px;letter-spacing:0.5px}
.p-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px}
.p-box{background:rgba(255,255,255,0.02);padding:24px;border-radius:16px;border:1px solid rgba(255,255,255,0.05)}
.p-box-title{font-size:12px;text-transform:uppercase;margin-bottom:18px;font-weight:800;letter-spacing:1px}
.p-row{display:flex;justify-content:space-between;margin-bottom:12px;font-size:14px;font-weight:500;align-items:center}
.p-highlight{font-weight:800;font-size:26px;color:var(--text);letter-spacing:-0.5px}

@media(max-width:1000px){.grid-2,.p-grid{grid-template-columns:1fr} .sidebar{width:220px}}
@media(max-width:700px){.layout{flex-direction:column} .sidebar{width:100%;height:auto;position:relative;flex-direction:row;overflow-x:auto;padding:14px} .top-actions{justify-content:center} .metric{padding:18px}}
</style>
</head>
<body>
<div class="layout">

<aside class="sidebar">
  <div class="brand">
    <div class="brand-logo">PISA<span>·22</span></div>
    <div class="brand-sub">ANALYTICS DASHBOARD</div>
  </div>
  
  <div class="nav-group">
    <div class="nav-group-label">Performa & Tren</div>
    <button class="nav-btn active" onclick="switchTab('overview',this)"><span class="dot" style="background:var(--blue)"></span> Menu Utama</button>
    <button class="nav-btn" onclick="switchTab('trend',this)"><span class="dot" style="background:var(--teal)"></span> Tren '18-'22</button>
    <button class="nav-btn" onclick="switchTab('regional',this)"><span class="dot" style="background:var(--green)"></span> Kawasan</button>
    <button class="nav-btn" onclick="switchTab('data',this)"><span class="dot" style="background:var(--amber)"></span> Tabel 81 Negara</button>
  </div>

  <div class="nav-group">
    <div class="nav-group-label">Analisis Mendalam</div>
    <button class="nav-btn" onclick="switchTab('gender',this)"><span class="dot" style="background:var(--pink)"></span> Kesenjangan Gender</button>
    <button class="nav-btn" onclick="switchTab('socio',this)"><span class="dot" style="background:var(--red)"></span> Sosial Ekonomi</button>
    <button class="nav-btn" onclick="switchTab('time',this)"><span class="dot" style="background:var(--purple)"></span> Waktu Belajar</button>
  </div>
</aside>

<div class="main">
  <header class="topbar">
    <div class="topbar-title" id="page-title">Menu Utama PISA 2022</div>
  </header>

  <div class="content">
    
    <div class="section active" id="sec-overview">
      
      <div class="top-actions">
        <div class="search-container">
          <input type="text" id="search-input" class="search-input" placeholder="🔍 Cari profil negara (misal: Singapura, Jepang)..." autocomplete="off">
          <div class="search-results" id="search-results"></div>
        </div>
      </div>

      <div class="profile-card" id="country-profile">
        <button class="btn-close" onclick="closeProfile()">✕ Tutup Profil</button>
        <div class="profile-header">
          <div class="profile-flag" id="p-flag">🌍</div>
          <div>
            <div class="profile-name" id="p-name">Nama Negara</div>
            <div class="profile-region" id="p-region">Kawasan</div>
          </div>
        </div>

        <div class="p-grid">
          <div class="p-box">
            <div class="p-box-title" style="color:var(--blue)">Skor Matematika (2022)</div>
            <div class="p-row">
              <span>Skor Rata-rata:</span> 
              <span class="p-highlight" id="p-math">-</span>
            </div>
            <div class="p-row" style="margin-top:24px;padding-top:18px;border-top:1px dashed rgba(255,255,255,0.1);">
              <span style="color:var(--muted)">Tren vs 2018:</span> 
              <span id="p-math-trend" style="font-weight:800; font-size:16px">-</span>
            </div>
          </div>

          <div class="p-box">
            <div class="p-box-title" style="color:var(--pink)">Kesenjangan & Kesetaraan</div>
            <div class="p-row"><span>Skor Laki-laki:</span> <span style="font-weight:700" id="p-boy">-</span></div>
            <div class="p-row"><span>Skor Perempuan:</span> <span style="font-weight:700" id="p-girl">-</span></div>
            <div class="p-row" style="margin-bottom:14px;font-size:12px;color:var(--pink);font-weight:600" id="p-gender-gap">Gap Gender: -</div>
            
            <div class="p-row" style="padding-top:14px;border-top:1px solid rgba(255,255,255,0.05)"><span>Siswa Mampu:</span> <span style="font-weight:700" id="p-adv">-</span></div>
            <div class="p-row"><span>Siswa Kurang:</span> <span style="font-weight:700" id="p-dis">-</span></div>
            <div class="p-row" style="margin-bottom:0;font-size:12px;color:var(--amber);font-weight:600" id="p-socio-gap">Gap Sosial: -</div>
          </div>

          <div class="p-box">
            <div class="p-box-title" style="color:var(--green)">Waktu & Kebiasaan (Minggu)</div>
            <div class="p-row"><span>Total Belajar:</span> <span style="font-weight:700;color:var(--text)" id="p-learn">-</span></div>
            <div class="p-row"><span>Waktu Digital:</span> <span style="font-weight:700;color:var(--text)" id="p-digital">-</span></div>
            <div class="p-row" style="padding-top:14px;border-top:1px solid rgba(255,255,255,0.05)"><span>Waktu PR (Hari):</span> <span style="font-weight:700;color:var(--text)" id="p-hw">-</span></div>
          </div>
        </div>
      </div>

      <div id="overview-content">
        <div class="metrics">
          <div class="metric m-blue"><div class="m-lbl">Negara Dianalisis</div><div class="m-val" style="color:var(--text)">81</div><div class="m-note">Populasi PISA 2022</div></div>
          <div class="metric m-amber"><div class="m-lbl">Rata-rata OECD Math</div><div class="m-val">472</div><div class="m-note">Turun dari 489 (2018)</div></div>
          <div class="metric m-pink"><div class="m-lbl">Rata-rata Gap Global</div><div class="m-val">-11</div><div class="m-note">Poin kehilangan skor (Loss)</div></div>
          <div class="metric m-green"><div class="m-lbl">Waktu Belajar (Avg)</div><div class="m-val">34.6<span style="font-size:18px;font-weight:600">j</span></div><div class="m-note">Jam per minggu</div></div>
        </div>
        
        <div class="grid-2">
          <div class="card">
            <div class="card-hd"><div class="card-title">10 Negara Tertinggi (Matematika)</div><div class="card-desc">Peringkat teratas global tahun 2022</div></div>
            <div style="height:270px"><canvas id="c-top10math"></canvas></div>
          </div>
          <div class="card">
            <div class="card-hd"><div class="card-title">10 Negara Terendah (Matematika)</div><div class="card-desc">Peringkat terbawah global tahun 2022</div></div>
            <div style="height:270px"><canvas id="c-bottom10math"></canvas></div>
          </div>
        </div>

        <div class="grid-2">
          <div class="card">
            <div class="card-hd"><div class="card-title">Tren Historis OECD (2006–2022)</div><div class="card-desc">Penurunan drastis pasca-pandemi</div></div>
            <div style="height:260px"><canvas id="c-trend"></canvas></div>
          </div>
          <div class="card">
            <div class="card-hd"><div class="card-title">Distribusi Skor Matematika 2022 (81 Negara)</div><div class="card-desc">Garis kuning = Rata-rata OECD 2022 (472)</div></div>
            <div style="height:260px"><canvas id="c-allbar"></canvas></div>
          </div>
        </div>
      </div>
    </div>

    <div class="section" id="sec-trend">
      <div class="metrics">
        <div class="metric m-green"><div class="m-lbl">Negara Meningkat</div><div class="m-val" id="t-up">0</div><div class="m-note">Skor membaik dibanding 2018</div></div>
        <div class="metric m-red"><div class="m-lbl">Negara Menurun</div><div class="m-val" id="t-down">0</div><div class="m-note">Skor memburuk dibanding 2018</div></div>
        <div class="metric m-blue"><div class="m-lbl">Peningkatan Tertinggi</div><div class="m-val" id="t-best" style="font-size:28px">0</div><div class="m-note">Lompatan poin terbesar</div></div>
      </div>
      <div class="card">
        <div class="card-hd"><div class="card-title">Perubahan Skor Matematika (2018 ke 2022)</div><div class="card-desc">Mengabaikan negara tanpa data partisipasi 2018.</div></div>
        <div style="height:360px"><canvas id="c-gap-bar"></canvas></div>
      </div>
      <div class="tbl-card">
        <div class="tbl-hd"><div class="tbl-title">Detail Perubahan Tren Matematika</div></div>
        <div class="tbl-scroll">
          <table>
            <thead><tr><th>#</th><th>Negara</th><th>Kawasan</th><th>Skor 2018</th><th>Skor 2022</th><th>Gap</th><th>Status</th></tr></thead>
            <tbody id="tbody-trend"></tbody>
          </table>
        </div>
      </div>
    </div>

    <div class="section" id="sec-regional">
      <div class="metrics">
        <div class="metric m-blue"><div class="m-lbl">Asia Timur</div><div class="m-val">529</div><div class="m-note">Kawasan Tertinggi (Avg 2022)</div></div>
        <div class="metric m-green"><div class="m-lbl">Eropa</div><div class="m-val">462</div><div class="m-note">Kawasan Terbesar (37 Negara)</div></div>
        <div class="metric m-amber"><div class="m-lbl">Amerika</div><div class="m-val">388</div><div class="m-note">Rata-rata 2022</div></div>
      </div>
      <div class="grid-2">
        <div class="card">
          <div class="card-hd"><div class="card-title">Rata-rata Skor per Kawasan</div><div class="card-desc">Tahun 2018 (Biru) vs 2022 (Merah)</div></div>
          <div style="height:290px"><canvas id="c-region-bar"></canvas></div>
        </div>
        <div class="card">
          <div class="card-hd"><div class="card-title">Sebaran Skor (Scatter) 2018 vs 2022</div><div class="card-desc">Titik di bawah diagonal = Penurunan skor</div></div>
          <div style="height:290px"><canvas id="c-scatter"></canvas></div>
        </div>
      </div>
    </div>

    <div class="section" id="sec-data">
      <div class="tbl-card">
        <div class="tbl-hd">
          <div class="tbl-title">Tabel Data Lengkap PISA Matematika (81 Negara)</div>
        </div>
        <div class="tbl-scroll">
          <table>
            <thead><tr>
              <th onclick="sortFull('rank')">Rank '22 ↕</th>
              <th onclick="sortFull('name')">Negara ↕</th>
              <th>Kawasan</th>
              <th onclick="sortFull('math18')">Math 2018 ↕</th>
              <th onclick="sortFull('math22')">Math 2022 ↕</th>
              <th onclick="sortFull('gap')">Perubahan ↕</th>
            </tr></thead>
            <tbody id="tbody-full"></tbody>
          </table>
        </div>
      </div>
    </div>

    <div class="section" id="sec-gender">
      <div class="card">
        <div class="card-hd"><div class="card-title">Kesenjangan Skor Matematika (Laki-laki vs Perempuan)</div><div class="card-desc">Berdasarkan data kuesioner spesifik. Kanan (Biru): Laki-laki unggul. Kiri (Pink): Perempuan unggul.</div></div>
        <div style="height:520px"><canvas id="c-gender-gap"></canvas></div>
      </div>
    </div>

    <div class="section" id="sec-socio">
      <div class="card">
        <div class="card-hd"><div class="card-title">Kesenjangan Sosial Ekonomi (Matematika)</div><div class="card-desc">Perbandingan siswa mampu (Kuartil Atas - Hijau) vs kurang mampu (Kuartil Bawah - Merah)</div></div>
        <div style="height:520px"><canvas id="c-socio"></canvas></div>
      </div>
    </div>

    <div class="section" id="sec-time">
      <div class="grid-2">
        <div class="card">
          <div class="card-hd"><div class="card-title">Waktu Belajar vs Hiburan Digital (Jam/Minggu)</div><div class="card-desc">Korelasi antara waktu

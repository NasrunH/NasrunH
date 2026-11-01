<!DOCTYPE html>
<html lang="id" class="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>NASRUN HIDAYATTULLAH // System Analyst, QA Tester & Fullstack Developer</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- Google Fonts: Space Grotesk & JetBrains Mono -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,400;0,500;0,700;1,400&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
  
  <!-- Three.js & GSAP -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Space Grotesk', 'sans-serif'],
            mono: ['JetBrains Mono', 'monospace'],
          },
          colors: {
            industrial: {
              bg: '#0b0d10',
              panel: '#14181f',
              border: '#262d3a',
              orange: '#ff5500',
              cyan: '#00f0ff',
              emerald: '#10b981',
              amber: '#f59e0b'
            }
          }
        }
      }
    }
  </script>

  <style>
    * {
      user-select: none;
      -webkit-font-smoothing: antialiased;
    }
    body, html {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      overflow: hidden;
      background-color: #0b0d10;
      color: #e2e8f0;
    }
    #webgl-container {
      position: fixed;
      inset: 0;
      z-index: 1;
    }
    .hud-layer {
      position: fixed;
      inset: 0;
      z-index: 10;
      pointer-events: none;
    }
    .interactive-ui {
      pointer-events: auto;
    }
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: rgba(15, 18, 24, 0.8);
    }
    ::-webkit-scrollbar-thumb {
      background: #2d3748;
      border-radius: 3px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #ff5500;
    }
    .tech-grid-overlay {
      background-size: 40px 40px;
      background-image: 
        linear-gradient(to right, rgba(255, 255, 255, 0.02) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255, 255, 255, 0.02) 1px, transparent 1px);
    }
    .glass-panel {
      background: rgba(15, 19, 26, 0.84);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.09);
    }
    .glow-orange {
      box-shadow: 0 0 22px rgba(255, 85, 0, 0.35);
    }
    .glow-cyan {
      box-shadow: 0 0 20px rgba(0, 240, 255, 0.3);
    }
  </style>
</head>
<body class="font-sans">

  <!-- 1. THREE.JS PERSISTENT CANVAS -->
  <div id="webgl-container"></div>

  <!-- 2. SUBTLE GRID OVERLAY -->
  <div class="fixed inset-0 pointer-events-none tech-grid-overlay z-[2]"></div>

  <!-- 3. FLOATING 3D HOVER TOOLTIP -->
  <div id="mesh-tooltip" class="fixed z-20 pointer-events-none opacity-0 transition-opacity duration-150 transform -translate-x-1/2 -translate-y-full pb-3">
    <div class="glass-panel px-3.5 py-2.5 rounded-md border-l-2 border-industrial-orange shadow-2xl min-w-[230px]">
      <div class="flex items-center justify-between gap-3 text-[10px] font-mono text-slate-400">
        <span id="tooltip-slot">MOD_01</span>
        <span id="tooltip-year" class="text-industrial-orange font-semibold">2026</span>
      </div>
      <div id="tooltip-title" class="text-sm font-bold text-white tracking-tight mt-0.5">Multi-Hospital SIMRS</div>
      <div id="tooltip-role" class="text-[11px] text-slate-300 font-mono mt-0.5">PT Indo Techno Medic</div>
      <div class="mt-1.5 pt-1.5 border-t border-white/10 flex items-center justify-between text-[10px] font-mono text-industrial-cyan">
        <span>[KLIK UNTUK INSPEKSI STUDI KASUS]</span>
        <span>→</span>
      </div>
    </div>
  </div>

  <!-- 4. BOOT SCREEN OVERLAY (STATE 0) -->
  <div id="boot-overlay" class="fixed inset-0 z-50 bg-[#080a0d] flex flex-col items-center justify-center p-6 transition-opacity duration-700">
    <div class="max-w-lg w-full glass-panel rounded-xl p-7 border border-white/10 shadow-2xl relative overflow-hidden">
      <div class="absolute top-0 left-0 right-0 h-1 bg-gradient-to-r from-industrial-orange via-amber-500 to-industrial-cyan"></div>
      
      <div class="flex items-center justify-between font-mono text-xs text-slate-400 mb-5">
        <span>NH.CORE // PERSONAL MAINFRAME v2026</span>
        <span class="flex items-center gap-1.5 text-emerald-400">
          <span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span>
          SLEMAN, YOGYAKARTA
        </span>
      </div>

      <div class="mb-2 font-mono text-xs text-industrial-orange uppercase tracking-widest">PERSONAL WEBSITE & INTERACTIVE PORTFOLIO</div>
      <h1 class="text-2xl md:text-3xl font-bold tracking-tight text-white mb-2">NASRUN HIDAYATTULLAH</h1>
      <p class="text-xs font-mono text-industrial-cyan mb-4">
        System Analyst &bull; QA Software Tester &bull; Fullstack Developer
      </p>
      <p class="text-xs text-slate-300 leading-relaxed mb-5">
        Selamat datang di ruang kerja interaktif 3D saya. Saya menjembatani <span class="text-white font-semibold">kebutuhan bisnis</span> dengan <span class="text-white font-semibold">solusi teknis yang teruji</span>—mulai dari penyusunan dokumen <span class="font-mono text-industrial-orange">PRD/SRS/SDD</span>, pengembangan sistem <span class="font-mono text-industrial-cyan">SIMRS & SaaS (Laravel / CI / PostgreSQL)</span>, hingga validasi <span class="font-mono text-emerald-400">QA & UAT</span>.
      </p>

      <!-- Boot Telemetry Log -->
      <div class="bg-black/60 rounded-lg p-3.5 font-mono text-[11px] space-y-1.5 mb-6 border border-white/5 text-slate-300">
        <div class="flex justify-between"><span>> EDUCATION_RECORD</span><span class="text-emerald-400">S1 SISTEM INFORMASI UTY (IPK 3.88)</span></div>
        <div class="flex justify-between"><span>> CURRENT_ROLE</span><span class="text-industrial-cyan">FULLSTACK DEV @ PT INDO TECHNO MEDIC</span></div>
        <div class="flex justify-between"><span>> CORE_MODULES_LOADED</span><span class="text-emerald-400">4 ENTERPRISE & SAAS PROJECTS</span></div>
        <div class="flex justify-between"><span>> HYBRID_CAPABILITY</span><span class="text-amber-400">ANALYST + QA TESTER + DEVELOPER</span></div>
      </div>

      <!-- Tactile Mechanical Initialize Button -->
      <button id="btn-initialize" class="w-full group relative overflow-hidden rounded-lg bg-industrial-orange hover:bg-[#ff6a22] text-black font-mono font-bold text-sm py-4 px-6 transition-all duration-200 glow-orange flex items-center justify-center gap-3 active:scale-[0.99]">
        <svg class="w-5 h-5 transition-transform group-hover:rotate-90" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
        </svg>
        <span>INITIALIZE NASRUN'S MAINFRAME</span>
      </button>

      <div class="mt-4 flex items-center justify-between text-[10px] font-mono text-slate-500">
        <span>ASTRO ISLANDS + THREE.JS + GSAP</span>
        <span>CLICK CARTRIDGES TO INSPECT</span>
      </div>
    </div>
  </div>

  <!-- 5. MAIN HUD LAYER -->
  <div class="hud-layer flex flex-col justify-between p-3.5 md:p-6">
    
    <!-- TOP BAR: Nasrun's Identity & System Controls -->
    <header class="flex flex-wrap items-start justify-between gap-3">
      <!-- Left: Personal Identity -->
      <div class="interactive-ui glass-panel rounded-xl px-4 py-3 flex items-center gap-4 border-l-4 border-industrial-orange shadow-xl">
        <div>
          <div class="flex items-center gap-2">
            <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
            <span class="font-mono text-[10px] tracking-widest text-slate-400 uppercase">SLEMAN, DI YOGYAKARTA // ACTIVE</span>
          </div>
          <h2 class="text-base md:text-lg font-bold tracking-tight text-white">NASRUN HIDAYATTULLAH</h2>
          <p class="text-[11px] text-industrial-cyan font-mono">System Analyst &bull; QA Software Tester &bull; Fullstack Dev</p>
        </div>
        <div class="hidden xl:flex flex-col border-l border-white/10 pl-4 font-mono text-[10px] text-slate-400 space-y-0.5">
          <div>PENDIDIKAN: <span class="text-white font-semibold">S1 Sistem Informasi UTY (IPK 3.88)</span></div>
          <div>ACTIVE MODULE: <span id="hud-slot" class="text-industrial-orange font-bold">NONE</span></div>
          <div>VIEW MODE: <span id="hud-mode" class="text-emerald-400">PHYSICAL_PBR</span></div>
        </div>
      </div>

      <!-- Right: Quick Controls (X-Ray Blueprint, CV Summary, Sound, Astro Code) -->
      <div class="interactive-ui flex items-center gap-2 flex-wrap">
        <!-- Global X-Ray Blueprint Switch -->
        <button id="btn-xray-global" class="glass-panel hover:border-industrial-cyan/60 px-3 py-2.5 rounded-lg font-mono text-xs flex items-center gap-2 transition-all" title="Ubah mesin 3D ke mode X-Ray & lihat skema PRD/SRS/Database">
          <span id="xray-dot" class="w-2 h-2 rounded-full bg-slate-500"></span>
          <span>X-RAY SRS/DB: <strong id="xray-label" class="text-slate-300">OFF</strong></span>
        </button>

        <!-- Printable / Readable Full CV Modal Button -->
        <button id="btn-cv-modal" class="bg-industrial-orange/15 hover:bg-industrial-orange/25 border border-industrial-orange/50 text-industrial-orange px-3 py-2.5 rounded-lg font-mono text-xs font-semibold flex items-center gap-1.5 transition-all">
          <span>📄</span>
          <span>RINGKASAN CV</span>
        </button>

        <!-- Sound Toggle -->
        <button id="btn-audio" class="glass-panel hover:border-white/30 px-3 py-2.5 rounded-lg font-mono text-xs flex items-center gap-1.5 transition-all" title="Toggle Tactile Sound">
          <span id="audio-icon">🔊</span>
          <span id="audio-label" class="hidden sm:inline">SFX</span>
        </button>

        <!-- Astro Source Code Modal Button -->
        <button id="btn-astro-code" class="bg-industrial-cyan/15 hover:bg-industrial-cyan/25 border border-industrial-cyan/50 text-industrial-cyan px-3 py-2.5 rounded-lg font-mono text-xs font-semibold flex items-center gap-1.5 transition-all">
          <span>&lt;/&gt;</span>
          <span class="hidden sm:inline">ASTRO CODE</span>
        </button>
      </div>
    </header>

    <!-- MIDDLE CONTEXTUAL AREA: Changes based on active Personal Web Zone -->
    <div class="my-auto flex items-center justify-between pointer-events-none gap-4">
      
      <!-- LEFT PANEL: Personal Bio Card (Shown in OVERVIEW) + Cartridge Rack Selector (Shown in OVERVIEW & MODULES) -->
      <div id="left-hub-column" class=" flex flex-col gap-3 max-w-xs w-full transition-all duration-300">
        
        <!-- Bio Card (State 1: Identity Overview) -->
        <div id="bio-overview-card" class="interactive-ui glass-panel rounded-xl p-4 border border-white/10 shadow-xl hidden sm:block">
          <div class="flex items-center justify-between font-mono text-[10px] text-industrial-cyan mb-1.5">
            <span>// PERSONAL BIO & POSITIONING</span>
            <span>IPK 3.88 / 4.00</span>
          </div>
          <h3 class="text-sm font-bold text-white mb-1.5">Menjembatani Bisnis & Solusi Teknis</h3>
          <p class="text-xs text-slate-300 leading-relaxed mb-3">
            Berpengalaman sebagai <span class="text-white font-medium">Fullstack Developer</span> (SIMRS 5 RSUD), <span class="text-white font-medium">System Analyst</span> (PRD/SRS/SDD & UML), serta <span class="text-white font-medium">QA Tester</span> (UAT & Defect Tracking) pada produk SaaS dan sistem pemerintahan.
          </p>
          <!-- 4 Key Highlights from Nasrun's CV -->
          <div class="grid grid-cols-2 gap-1.5 font-mono text-[10px] mb-3">
            <div class="bg-black/50 p-2 rounded border border-white/5">
              <div class="text-industrial-orange font-bold text-sm">5 RSUD</div>
              <div class="text-slate-400">Kustomisasi SIMRS</div>
            </div>
            <div class="bg-black/50 p-2 rounded border border-white/5">
              <div class="text-industrial-cyan font-bold text-sm">40+ Tasks</div>
              <div class="text-slate-400">PRD / SRS / SDD</div>
            </div>
            <div class="bg-black/50 p-2 rounded border border-white/5">
              <div class="text-emerald-400 font-bold text-sm">30+ Modul</div>
              <div class="text-slate-400">Legacy Refactoring</div>
            </div>
            <div class="bg-black/50 p-2 rounded border border-white/5">
              <div class="text-amber-400 font-bold text-sm">3.88 / 4.0</div>
              <div class="text-slate-400">S1 Sistem Informasi</div>
            </div>
          </div>
          <div class="flex gap-1.5 font-mono text-[11px]">
            <button id="btn-goto-chronicle" class="flex-1 py-1.5 px-2 rounded bg-white/10 hover:bg-white/15 text-white text-center transition-all">
              Jejak Karier →
            </button>
            <button id="btn-goto-uplink" class="py-1.5 px-2.5 rounded bg-industrial-orange text-black font-bold hover:bg-[#ff6a22] transition-all">
              Kontak
            </button>
          </div>
        </div>

        <!-- Quick Cartridge Selector List -->
        <div id="quick-rack-panel" class="interactive-ui glass-panel rounded-xl p-3.5 border border-white/10 shadow-xl hidden lg:block">
          <div class="flex items-center justify-between font-mono text-[10px] text-slate-400 mb-2 pb-1.5 border-b border-white/10">
            <span>RAK MODUL PROYEK [01-04]</span>
            <span class="text-industrial-orange">KLIK UNTUK MOUNT</span>
          </div>
          <div id="rack-buttons-list" class="space-y-1.5">
            <!-- Populated dynamically via JS -->
          </div>
        </div>
      </div>

      <!-- RIGHT PANEL A: CHRONICLE (Career, Education, Organization & Certifications - State 3: CHRONICLE) -->
      <div id="chronicle-hud-panel" class="interactive-ui glass-panel rounded-xl p-5 max-w-xl w-full border border-amber-500/40 transition-all duration-300 hidden ml-auto mr-2 max-h-[72vh] flex flex-col shadow-2xl">
        <div class="flex items-center justify-between font-mono text-xs text-amber-400 mb-1">
          <span>// PERSONAL CHRONICLE & CV LOGS</span>
          <span>UTY &bull; INDO TECHNO &bull; SWEVEL &bull; JAVAN</span>
        </div>
        <h3 class="text-lg md:text-xl font-bold text-white mb-3">Perjalanan Karier, Pendidikan & Organisasi</h3>

        <!-- Sub-Tabs inside Chronicle -->
        <div class="flex gap-1.5 bg-black/50 p-1 rounded-lg border border-white/10 font-mono text-xs mb-4">
          <button data-chron-tab="work" class="chron-tab-btn flex-1 py-1.5 px-2 rounded bg-amber-500 text-black font-bold transition-all">
            1. PENGALAMAN KERJA (4)
          </button>
          <button data-chron-tab="edu" class="chron-tab-btn flex-1 py-1.5 px-2 rounded text-slate-300 hover:text-white transition-all">
            2. PENDIDIKAN & SERTIFIKASI
          </button>
          <button data-chron-tab="org" class="chron-tab-btn flex-1 py-1.5 px-2 rounded text-slate-300 hover:text-white transition-all">
            3. KEPEMIMPINAN & HMSI
          </button>
        </div>

        <!-- Scrollable Chronicle Content -->
        <div id="chronicle-content-area" class="flex-1 overflow-y-auto pr-1 space-y-3 text-xs">
          <!-- Populated dynamically by JS -->
        </div>
      </div>

      <!-- RIGHT PANEL B: SKILLS / NODES FLOATING HUD (Visible in State 4: NODES) -->
      <div id="nodes-hud-panel" class="interactive-ui glass-panel rounded-xl p-5 max-w-md w-full border border-industrial-cyan/30 transition-all duration-300 hidden ml-auto mr-2 shadow-2xl">
        <div class="flex items-center justify-between font-mono text-xs text-industrial-cyan mb-1">
          <span>// 3-PILLAR HYBRID SKILL DECK</span>
          <span>6 NODES ONLINE</span>
        </div>
        <h3 id="node-detail-title" class="text-lg font-bold text-white mb-1">Pilih Chip Prosesor Keahlian</h3>
        <p id="node-detail-desc" class="text-xs text-slate-300 leading-relaxed mb-3"></p>
        <div id="node-tags-container" class="flex flex-wrap gap-1.5 mb-4"></div>
        <div class="text-[10px] font-mono text-slate-400 mb-1.5">KLIK CHIP DI MESIN 3D ATAU PILIH NODE DI BAWAH:</div>
        <div id="node-buttons-grid" class="grid grid-cols-2 gap-1.5 pt-2 border-t border-white/10 font-mono text-[11px]">
          <!-- Populated by JS -->
        </div>
      </div>

      <!-- RIGHT PANEL C: UPLINK / CONTACT FLOATING HUD (Visible in State 5: UPLINK) -->
      <div id="uplink-hud-panel" class="interactive-ui glass-panel rounded-xl p-5 md:p-6 max-w-md w-full border border-industrial-orange/40 transition-all duration-300 hidden ml-auto mr-2 max-h-[76vh] overflow-y-auto shadow-2xl">
        <div class="flex items-center justify-between font-mono text-xs text-industrial-orange mb-1">
          <span>// DIRECT UPLINK TERMINAL</span>
          <span class="flex items-center gap-1 text-emerald-400"><span class="w-2 h-2 rounded-full bg-emerald-400 animate-ping"></span> SLEMAN, DIY</span>
        </div>
        <h3 class="text-xl font-bold text-white mb-1">Hubungi Nasrun Hidayattullah</h3>
        <p class="text-xs text-slate-300 mb-4">
          Terbuka untuk kolaborasi dan peluang karier sebagai <span class="text-white font-semibold">System/Business Analyst</span>, <span class="text-white font-semibold">QA Software Tester</span>, atau <span class="text-white font-semibold">Fullstack Developer</span>.
        </p>

        <!-- Direct Real Contact Channels from CV -->
        <div class="grid grid-cols-1 gap-2 mb-4 font-mono text-xs">
          <a href="https://wa.me/6285156536924" target="_blank" rel="noopener noreferrer" class="flex items-center justify-between p-2.5 rounded-lg bg-emerald-500/10 hover:bg-emerald-500/20 border border-emerald-500/30 text-emerald-300 transition-all">
            <span>💬 WhatsApp: +62 851-5653-6924</span>
            <span>CHAT →</span>
          </a>
          <a href="mailto:nasrun671@gmail.com" class="flex items-center justify-between p-2.5 rounded-lg bg-industrial-cyan/10 hover:bg-industrial-cyan/20 border border-industrial-cyan/30 text-industrial-cyan transition-all">
            <span>✉️ Email: nasrun671@gmail.com</span>
            <span>KIRIM EMAIL →</span>
          </a>
          <a href="https://linkedin.com/in/nasrun-hidayattullah" target="_blank" rel="noopener noreferrer" class="flex items-center justify-between p-2.5 rounded-lg bg-blue-500/10 hover:bg-blue-500/20 border border-blue-500/30 text-blue-300 transition-all">
            <span>🔗 linkedin.com/in/nasrun-hidayattullah</span>
            <span>PROFIL →</span>
          </a>
        </div>
        
        <form id="uplink-form" class="space-y-2.5 font-mono text-xs pt-3 border-t border-white/10">
          <div class="text-[10px] text-slate-400 uppercase">KIRIM TRANSMISI CEPAT KE MAINFRAME:</div>
          <div>
            <input type="text" required placeholder="Nama Anda / Perusahaan" class="w-full bg-black/50 border border-white/15 focus:border-industrial-orange rounded px-3 py-2 text-white outline-none" />
          </div>
          <div>
            <select class="w-full bg-black/50 border border-white/15 focus:border-industrial-orange rounded px-3 py-2 text-white outline-none">
              <option>Rekrutmen / Full-Time (System Analyst / QA / Fullstack)</option>
              <option>Proyek Pengembangan SIMRS / Aplikasi Web Laravel & CI</option>
              <option>Konsultasi PRD/SRS/SDD & Pengujian QA / UAT</option>
              <option>Lainnya / Diskusi Teknis</option>
            </select>
          </div>
          <div>
            <textarea rows="2" required placeholder="Tulis pesan singkat Anda..." class="w-full bg-black/50 border border-white/15 focus:border-industrial-orange rounded px-3 py-2 text-white outline-none"></textarea>
          </div>
          <button type="submit" class="w-full bg-industrial-orange hover:bg-[#ff691f] text-black font-bold py-2.5 rounded transition-all">
            TRANSMIT MESSAGE [SEND] →
          </button>
          <div id="uplink-feedback" class="hidden text-center text-emerald-400 text-[11px] pt-1">
            ✓ Pesan tercatat! Anda juga dapat langsung menghubungi WhatsApp/Email di atas.
          </div>
        </form>
      </div>
    </div>

    <!-- BOTTOM NAVIGATION DOCK (5 Zones of Nasrun's Personal Website) -->
    <footer class="flex flex-col lg:flex-row items-center justify-between gap-3">
      <nav class="interactive-ui glass-panel p-1.5 rounded-xl flex flex-wrap items-center justify-center gap-1 border border-white/10 shadow-2xl">
        <button data-nav="OVERVIEW" class="nav-btn px-3 py-2 rounded-lg font-mono text-xs font-bold transition-all flex items-center gap-1.5 bg-industrial-orange text-black">
          <span class="opacity-70">01.</span><span>IDENTITY (BIO)</span>
        </button>
        <button data-nav="MODULES" class="nav-btn px-3 py-2 rounded-lg font-mono text-xs font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all flex items-center gap-1.5">
          <span class="opacity-60">02.</span><span>PROJECTS (4 MODULES)</span>
        </button>
        <button data-nav="CHRONICLE" class="nav-btn px-3 py-2 rounded-lg font-mono text-xs font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all flex items-center gap-1.5">
          <span class="opacity-60">03.</span><span>CHRONICLE (KARIER & UTY)</span>
        </button>
        <button data-nav="NODES" class="nav-btn px-3 py-2 rounded-lg font-mono text-xs font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all flex items-center gap-1.5">
          <span class="opacity-60">04.</span><span>SKILLS (SA / QA / DEV)</span>
        </button>
        <button data-nav="UPLINK" class="nav-btn px-3 py-2 rounded-lg font-mono text-xs font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all flex items-center gap-1.5">
          <span class="opacity-60">05.</span><span>UPLINK (KONTAK)</span>
        </button>
      </nav>

      <!-- Live State Status Bar -->
      <div class="interactive-ui glass-panel px-3.5 py-2 rounded-lg font-mono text-[11px] text-slate-400 hidden xl:flex items-center gap-3">
        <span>STATE: <strong id="hud-cam-state" class="text-white">OVERVIEW</strong></span>
        <span class="text-white/20">|</span>
        <span id="hud-instruction" class="text-industrial-cyan">Klik kaset di rak kiri untuk memuat studi kasus ke Central Core</span>
      </div>
    </footer>
  </div>

  <!-- 6. HYBRID CASE STUDY DRAWER (STATE: CASE_STUDY SPLIT-SCREEN) -->
  <aside id="case-study-drawer" class="fixed top-0 right-0 bottom-0 z-30 w-full md:w-[62%] lg:w-[58%] glass-panel border-l border-white/15 transform translate-x-full transition-transform duration-500 ease-out flex flex-col">
    <!-- Top Drawer Bar -->
    <div class="p-4 md:px-7 md:py-5 border-b border-white/10 flex flex-wrap items-center justify-between gap-3 bg-black/40">
      <div class="flex items-center gap-2.5">
        <span id="drawer-slot-badge" class="px-2.5 py-1 rounded bg-industrial-orange/20 border border-industrial-orange text-industrial-orange font-mono text-xs font-bold">
          MOD_01 // DOCKED
        </span>
        <span id="drawer-company" class="font-mono text-xs text-white font-semibold">PT Indo Techno Medic</span>
        <span id="drawer-year" class="font-mono text-xs text-slate-400 hidden sm:inline">&bull; Juni 2026 - Sekarang</span>
      </div>

      <div class="flex items-center gap-2">
        <!-- Mode Switch inside Case Study: Product Execution vs System Analysis / SRS / QA Blueprint -->
        <div class="bg-black/60 p-1 rounded-lg border border-white/10 flex items-center font-mono text-[11px]">
          <button id="tab-product" class="px-3 py-1.5 rounded bg-industrial-orange text-black font-bold transition-all">
            EKSEKUSI & DAMPAK
          </button>
          <button id="tab-blueprint" class="px-3 py-1.5 rounded text-slate-300 hover:text-white transition-all flex items-center gap-1.5">
            <span class="w-1.5 h-1.5 rounded-full bg-industrial-cyan"></span>
            BLUEPRINT SRS / DB / QA
          </button>
        </div>

        <!-- Eject Button -->
        <button id="btn-eject" class="px-3 py-2 rounded-lg bg-red-500/15 hover:bg-red-500/30 border border-red-500/40 text-red-300 font-mono text-xs font-semibold flex items-center gap-1.5 transition-all">
          <span>⏏</span>
          <span>EJECT</span>
        </button>
      </div>
    </div>

    <!-- Scrollable Case Study Content -->
    <div class="flex-1 overflow-y-auto p-6 md:p-8 space-y-6">
      <div>
        <div id="drawer-category" class="font-mono text-xs text-industrial-cyan uppercase tracking-wider mb-1">Fullstack Developer // Healthcare System</div>
        <h2 id="drawer-title" class="text-2xl md:text-3xl font-bold text-white tracking-tight">SIMRS 5 Rumah Sakit & Portal Dokumentasi</h2>
      </div>

      <!-- Impact Metrics Grid -->
      <div id="drawer-metrics" class="grid grid-cols-3 gap-3"></div>

      <!-- Tech Stack & Methodology Pills -->
      <div>
        <div class="font-mono text-[10px] text-slate-400 uppercase tracking-wider mb-2">TEKNOLOGI, METODOLOGI & TOOLS</div>
        <div id="drawer-stack" class="flex flex-wrap gap-2"></div>
      </div>

      <!-- TAB 1: PRODUCT & EXECUTION VIEW -->
      <div id="content-product-view" class="space-y-5">
        <div class="bg-black/40 rounded-xl p-5 border border-white/10 space-y-2">
          <h4 class="font-mono text-xs text-industrial-orange uppercase">01 // KONTEKS & KEBUTUHAN BISNIS (BUSINESS REQUIREMENT)</h4>
          <p id="drawer-problem" class="text-sm text-slate-300 leading-relaxed"></p>
        </div>

        <div class="bg-black/40 rounded-xl p-5 border border-white/10 space-y-2">
          <h4 class="font-mono text-xs text-emerald-400 uppercase">02 // EKSEKUSI PENGEMBANGAN, ANALISIS & QA</h4>
          <p id="drawer-solution" class="text-sm text-slate-300 leading-relaxed"></p>
        </div>

        <!-- Interactive Module Switcher Footer inside Drawer -->
        <div class="pt-4 border-t border-white/10 flex flex-wrap items-center justify-between gap-2">
          <span class="font-mono text-xs text-slate-400">Inspeksi modul proyek lainnya:</span>
          <div id="drawer-quick-switch" class="flex gap-1.5"></div>
        </div>
      </div>

      <!-- TAB 2: BLUEPRINT ARCHITECTURE, SRS & QA VALIDATION VIEW -->
      <div id="content-blueprint-view" class="hidden space-y-5">
        <div class="bg-industrial-cyan/5 rounded-xl p-5 border border-industrial-cyan/30">
          <div class="flex items-center justify-between mb-3">
            <h4 class="font-mono text-xs text-industrial-cyan uppercase font-bold">⚡ ARSITEKTUR SISTEM, ALUR PROSES & SKEMA DATA</h4>
            <span class="font-mono text-[10px] text-industrial-cyan px-2 py-0.5 rounded bg-industrial-cyan/10">3D X-RAY ACTIVE</span>
          </div>
          <div id="drawer-diagram" class="bg-black/70 rounded-lg p-4 font-mono text-xs text-slate-200 overflow-x-auto border border-white/10 space-y-3"></div>
        </div>

        <div class="bg-black/40 rounded-xl p-5 border border-white/10 space-y-2">
          <h4 class="font-mono text-xs text-amber-400 uppercase">ARTEFAK SYSTEM ANALYST (PRD/SRS/SDD) & VALIDASI QA/UAT</h4>
          <ul id="drawer-adr" class="text-sm text-slate-300 space-y-2 list-disc list-inside leading-relaxed"></ul>
        </div>
      </div>
    </div>
  </aside>

  <!-- 7. FULL READABLE / PRINTABLE CV SUMMARY MODAL -->
  <div id="cv-modal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-md hidden items-center justify-center p-4 md:p-8">
    <div class="glass-panel w-full max-w-4xl max-h-[88vh] rounded-2xl border border-industrial-orange/40 flex flex-col overflow-hidden shadow-2xl">
      <div class="px-6 py-4 border-b border-white/10 flex items-center justify-between bg-black/60">
        <div>
          <span class="font-mono text-[10px] text-industrial-orange uppercase tracking-widest">CURRICULUM VITAE // VERIFIED RECORD</span>
          <h3 class="text-lg font-bold text-white">Nasrun Hidayattullah — S.Kom. (IPK 3.88 / 4.00)</h3>
        </div>
        <div class="flex items-center gap-2">
          <button onclick="window.print()" class="px-3 py-1.5 rounded-lg bg-industrial-orange text-black font-mono text-xs font-bold hover:bg-[#ff6a22]">
            🖨️ PRINT / SAVE PDF
          </button>
          <button id="btn-close-cv" class="px-3 py-1.5 rounded-lg bg-white/10 hover:bg-white/20 font-mono text-xs text-white">
            [ TUTUP ]
          </button>
        </div>
      </div>

      <div class="flex-1 overflow-y-auto p-6 md:p-8 space-y-6 text-xs md:text-sm text-slate-200 leading-relaxed">
        <!-- Header Info -->
        <div class="border-b border-white/10 pb-4 flex flex-wrap justify-between gap-4">
          <div>
            <h2 class="text-2xl font-bold text-white">NASRUN HIDAYATTULLAH</h2>
            <p class="font-mono text-industrial-cyan">System Analyst | QA Software Tester | Fullstack Developer</p>
          </div>
          <div class="font-mono text-xs text-slate-400 space-y-0.5 text-right">
            <div>📍 Sleman, DI Yogyakarta</div>
            <div>📞 +62 851-5653-6924 &bull; ✉️ nasrun671@gmail.com</div>
            <div>🔗 linkedin.com/in/nasrun-hidayattullah</div>
          </div>
        </div>

        <!-- Ringkasan -->
        <div>
          <h4 class="font-mono text-xs text-industrial-orange uppercase font-bold mb-1.5">RINGKASAN PROFESIONAL</h4>
          <p class="text-slate-300">
            Lulusan S1 Sistem Informasi dari Universitas Teknologi Yogyakarta (IPK: 3,88 / 4,00) dengan pengalaman langsung sebagai Fullstack Developer, System Analyst, dan QA Tester dalam pengembangan SIMRS (5 Rumah Sakit), produk SaaS (CMS, WhatsApp Blast, estimasi biaya konstruksi Gen-AI), serta sistem pemerintahan (RTHP). Kompeten dalam requirement gathering, penyusunan PRD/SRS/SDD, pengujian sistem, validasi acceptance criteria (UAT), pelacakan bug, dan penerjemahan kebutuhan bisnis menjadi task teknis terstruktur menggunakan Agile Scrum, SDLC, PHP (Laravel 12, CodeIgniter 3 & 4), PostgreSQL, MySQL, serta UML.
          </p>
        </div>

        <!-- Pengalaman Kerja -->
        <div class="space-y-4">
          <h4 class="font-mono text-xs text-industrial-cyan uppercase font-bold">PENGALAMAN KERJA</h4>
          
          <div class="bg-black/40 p-4 rounded-xl border border-white/10">
            <div class="flex justify-between font-bold text-white">
              <span>Fullstack Developer — PT Indo Techno Medic</span>
              <span class="font-mono text-xs text-industrial-orange">Juni 2026 – Sekarang</span>
            </div>
            <div class="font-mono text-[11px] text-slate-400 mb-2">Teknologi: CodeIgniter 3, Laravel 12, PostgreSQL</div>
            <ul class="list-disc list-inside text-slate-300 space-y-1">
              <li>Melanjutkan pengembangan dan kustomisasi Sistem Informasi Manajemen Rumah Sakit (SIMRS) untuk 5 rumah sakit: <strong>RSUD Caruban, RSUD Cilacap, RSU Astrini, RSUD Blora, dan RSUD Slawi</strong>.</li>
              <li>Mengembangkan dan memelihara fitur SIMRS berbasis CodeIgniter 3 dengan database PostgreSQL sesuai kebutuhan spesifik tiap rumah sakit.</li>
              <li>Membangun sistem informasi dokumentasi panduan penggunaan SIMRS PT Indo Techno Medic menggunakan <strong>Laravel 12 dan PostgreSQL</strong> sebagai referensi pengguna & tim internal.</li>
            </ul>
          </div>

          <div class="bg-black/40 p-4 rounded-xl border border-white/10">
            <div class="flex justify-between font-bold text-white">
              <span>System Analyst & Backend Developer (Magang) — PT Swevel Universal Media</span>
              <span class="font-mono text-xs text-industrial-cyan">Sept 2025 – Jan 2026</span>
            </div>
            <div class="font-mono text-[11px] text-slate-400 mb-2">Metodologi: Agile Scrum | CodeIgniter 4, Gen-AI, Relational DB</div>
            <ul class="list-disc list-inside text-slate-300 space-y-1">
              <li>Melakukan refactoring terhadap <strong>&gt;30 modul</strong> dari codebase lama ke library baru, meningkatkan maintainability dan mengurangi bug berulang secara signifikan.</li>
              <li>Mengembangkan fitur <strong>AI Generatif</strong> untuk otomasi estimasi biaya konstruksi.</li>
              <li>Menganalisis kebutuhan bisnis & merancang alur proses end-to-end sistem pemerintahan <strong>RTHP (&gt;10 fitur utama, &gt;15 tabel relasional, &gt;8 endpoint API utama)</strong>.</li>
              <li>Melaksanakan pengujian fungsional & regresi terhadap acceptance criteria serta berkontribusi dalam proyek tender <strong>DLH Kota Yogyakarta</strong>.</li>
            </ul>
          </div>

          <div class="bg-black/40 p-4 rounded-xl border border-white/10">
            <div class="flex justify-between font-bold text-white">
              <span>System Analyst & QA Tester (Magang) — PT Javan Cipta Solusi</span>
              <span class="font-mono text-xs text-emerald-400">Juli 2025 – Sept 2025</span>
            </div>
            <div class="font-mono text-[11px] text-slate-400 mb-2">Metodologi: SDLC & Agile Scrum | Produk: SaaS CMS & WhatsApp Blast</div>
            <ul class="list-disc list-inside text-slate-300 space-y-1">
              <li>Menyusun dokumen <strong>PRD, SRS, dan SDD</strong> komprehensif serta menguraikan kebutuhan bisnis menjadi <strong>&gt;40 task teknis</strong> bagi tim 3–5 developer.</li>
              <li>Melaksanakan pengujian end-to-end dan validasi <strong>UAT</strong> berdasarkan acceptance criteria, melacak bug hingga tuntas, dan menurunkan tingkat defect secara terukur.</li>
            </ul>
          </div>

          <div class="bg-black/40 p-4 rounded-xl border border-white/10">
            <div class="flex justify-between font-bold text-white">
              <span>Administrasi - Pengembangan Bisnis — UTY Software House</span>
              <span class="font-mono text-xs text-amber-400">Juli 2024 – Jan 2026</span>
            </div>
            <ul class="list-disc list-inside text-slate-300 space-y-1 mt-1">
              <li>Mengelola dokumentasi bisnis, administrasi proyek perangkat lunak, dan memfasilitasi komunikasi antara tim developer internal dengan klien eksternal.</li>
            </ul>
          </div>
        </div>

        <!-- Pendidikan, Proyek & Organisasi -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div class="bg-black/40 p-4 rounded-xl border border-white/10">
            <h4 class="font-mono text-xs text-industrial-orange uppercase font-bold mb-2">PENDIDIKAN & SERTIFIKASI</h4>
            <div class="font-bold text-white">S1 Sistem Informasi (IPK: 3,88 / 4,00)</div>
            <div class="text-xs text-slate-400 mb-2">Universitas Teknologi Yogyakarta | Sept 2022 – Maret 2026</div>
            <div class="font-bold text-white">MIPA — SMA Negeri 1 Kokap</div>
            <div class="text-xs text-slate-400 mb-3">2019 – 2022</div>
            <div class="pt-2 border-t border-white/10 text-xs space-y-1">
              <div>🏆 <strong>Sertifikasi Frontend & Backend Developer</strong> — Dicoding (2025)</div>
              <div>🏆 <strong>Sertifikasi Profesional Data Engineering</strong> — Altair (2024)</div>
            </div>
          </div>

          <div class="bg-black/40 p-4 rounded-xl border border-white/10">
            <h4 class="font-mono text-xs text-industrial-cyan uppercase font-bold mb-2">KEPEMIMPINAN & ORGANISASI</h4>
            <div class="font-bold text-white">Manajer Proyek — PKM-KC Marketplace Peternakan</div>
            <div class="text-xs text-slate-400 mb-1">Mei 2024 – Agustus 2024</div>
            <p class="text-xs text-slate-300 mb-3">Memimpin tim 5 orang dari konsep hingga rilis, melakukan requirement gathering bersama peternak & pembeli, serta merancang arsitektur solusi.</p>
            <div class="font-bold text-white">Sekretaris Umum — HMSI UTY</div>
            <div class="text-xs text-slate-400 mb-1">Oktober 2023 – Oktober 2024</div>
            <p class="text-xs text-slate-300">Mengelola dokumentasi organisasi, korespondensi formal, koordinasi antar-divisi, dan membimbing tim sekretaris kegiatan.</p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- 8. ASTRO + THREE.JS + NANOSTORES CODE EXPORTER MODAL -->
  <div id="astro-modal" class="fixed inset-0 z-50 bg-black/80 backdrop-blur-md hidden items-center justify-center p-4 md:p-8">
    <div class="glass-panel w-full max-w-4xl max-h-[88vh] rounded-2xl border border-industrial-cyan/40 flex flex-col overflow-hidden shadow-2xl">
      <div class="px-6 py-4 border-b border-white/10 flex items-center justify-between bg-black/50">
        <div>
          <span class="font-mono text-[10px] text-industrial-cyan uppercase tracking-widest">PRODUCTION ARCHITECTURE // NASRUN HIDAYATTULLAH</span>
          <h3 class="text-lg font-bold text-white">Boilerplate Kode Astro + Three.js + Nanostores + GSAP</h3>
        </div>
        <button id="btn-close-modal" class="px-3 py-1.5 rounded-lg bg-white/10 hover:bg-white/20 font-mono text-xs text-white">
          [ ESC / TUTUP ]
        </button>
      </div>

      <!-- File Tabs -->
      <div class="flex border-b border-white/10 bg-black/40 px-4 pt-2 gap-2 overflow-x-auto font-mono text-xs">
        <button data-code-tab="store" class="code-tab-btn px-4 py-2 rounded-t-lg bg-industrial-cyan/20 text-industrial-cyan border-b-2 border-industrial-cyan font-bold">
          1. src/stores/systemStore.ts
        </button>
        <button data-code-tab="layout" class="code-tab-btn px-4 py-2 rounded-t-lg text-slate-400 hover:text-white">
          2. src/layouts/PersonalCoreLayout.astro
        </button>
        <button data-code-tab="canvas" class="code-tab-btn px-4 py-2 rounded-t-lg text-slate-400 hover:text-white">
          3. src/components/SystemCoreCanvas.astro
        </button>
        <button data-code-tab="mdx" class="code-tab-btn px-4 py-2 rounded-t-lg text-slate-400 hover:text-white">
          4. src/content/projects/01-simrs.mdx
        </button>
      </div>

      <!-- Code Display Area -->
      <div class="flex-1 overflow-y-auto p-6 bg-[#07090c] font-mono text-xs text-slate-200 relative">
        <button id="btn-copy-code" class="sticky top-2 float-right px-3 py-1.5 rounded bg-industrial-orange text-black font-bold text-[11px] hover:bg-[#ff6b24] transition-all">
          COPY FILE
        </button>
        <pre id="astro-code-content" class="leading-relaxed whitespace-pre-wrap break-words"></pre>
      </div>
    </div>
  </div>

  <!-- ===================================================================== -->
  <!-- APPLICATION LOGIC: NASRUN'S DATA + PROCEDURAL THREE.JS + GSAP         -->
  <!-- ===================================================================== -->
  <script>
    /*************************************************************************
     * 1. REACTIVE STATE STORE (Nanostores Pattern)
     *************************************************************************/
    function createAtom(initialValue) {
      let value = initialValue;
      const listeners = new Set();
      return {
        get: () => value,
        set: (newValue) => {
          if (value !== newValue) {
            value = newValue;
            listeners.forEach(fn => fn(value));
          }
        },
        subscribe: (fn) => {
          listeners.add(fn);
          fn(value);
          return () => listeners.delete(fn);
        }
      };
    }

    const systemStore = {
      // 6 Main States for Nasrun's Personal Website:
      // 'BOOT' | 'OVERVIEW' | 'MODULES' | 'CASE_STUDY' | 'CHRONICLE' | 'NODES' | 'UPLINK'
      currentView: createAtom('BOOT'),
      activeProjectId: createAtom(null),
      isBlueprintMode: createAtom(false),
      isAudioMuted: createAtom(false),
      activeSkillId: createAtom('sa'),
      activeChronicleTab: createAtom('work')
    };

    /*************************************************************************
     * 2. NASRUN HIDAYATTULLAH'S REAL CV DATA (PROJECTS, CHRONICLE & SKILLS)
     *************************************************************************/
    const PROJECT_MODULES = [
      {
        id: 'simrs',
        slot: 'MOD_01',
        title: 'Multi-Hospital SIMRS & Portal Dokumentasi Internal',
        shortTitle: 'SIMRS 5 RSUD',
        company: 'PT Indo Techno Medic',
        category: 'Fullstack Developer // Healthcare Information System',
        year: 'Juni 2026 – Sekarang',
        colorHex: 0xff5500,
        accentCss: '#ff5500',
        metrics: [
          { label: 'IMPLEMENTASI RSUD', value: '5 RS' },
          { label: 'PORTAL DOKUMENTASI', value: 'Laravel 12' },
          { label: 'CORE DATABASE', value: 'PostgreSQL' }
        ],
        stack: ['CodeIgniter 3', 'Laravel 12', 'PostgreSQL', 'PHP', 'SIMRS Workflow', 'SQL Optimization', 'Git'],
        problem: 'Setiap rumah sakit mitra (RSUD Caruban, RSUD Cilacap, RSU Astrini, RSUD Blora, dan RSUD Slawi) memiliki aturan alur layanan medis, pelaporan, dan kustomisasi modul SIMRS yang spesifik. Selain itu, tim internal dan pengguna rumah sakit membutuhkan pusat dokumentasi panduan penggunaan SIMRS yang terstruktur dan mudah dicari.',
        solution: 'Mengembangkan dan memelihara fitur-fitur kustom pada SIMRS berbasis CodeIgniter 3 dan database PostgreSQL untuk kelima rumah sakit tersebut. Secara paralel, merancang dan membangun Sistem Informasi Dokumentasi Panduan Penggunaan SIMRS PT Indo Techno Medic dari nol menggunakan Laravel 12 dan PostgreSQL sebagai single-source-of-truth bagi pengguna RS dan tim internal.',
        diagram: [
          '[5 Rumah Sakit Mitra: RSUD Caruban, Cilacap, Astrini, Blora, Slawi]',
          '        │',
          '        ├──> [SIMRS Core Engine (CodeIgniter 3)] ──> [PostgreSQL Hospital Schemas]',
          '        │         └── Kustomisasi Modul Layanan Medis, Rekam Medis & Pelaporan RS',
          '        │',
          '        └──> [Sistem Informasi Dokumentasi Panduan SIMRS (Laravel 12 + PostgreSQL)]',
          '                  └── Referensi Terpusat untuk Pengguna RS & Tim Internal Indo Techno Medic'
        ],
        adr: [
          'Menyesuaikan modul CodeIgniter 3 secara modular agar kustomisasi spesifik di RSUD Caruban, Cilacap, Astrini, Blora, dan Slawi tetap terjaga stabilitasnya di atas database PostgreSQL.',
          'Menggunakan Laravel 12 dan PostgreSQL untuk membangun Sistem Informasi Dokumentasi Panduan SIMRS sehingga pencarian panduan operasional menjadi jauh lebih cepat dan terstandarisasi.',
          'Memastikan keselarasan antara fitur SIMRS yang baru dirilis dengan pembaruan dokumentasi panduan bagi pengguna akhir.'
        ]
      },
      {
        id: 'swevel',
        slot: 'MOD_02',
        title: 'SaaS Estimasi Konstruksi Gen-AI & Sistem Pemerintahan RTHP',
        shortTitle: 'Gen-AI & RTHP Gov',
        company: 'PT Swevel Universal Media',
        category: 'System Analyst & Backend Developer // Agile Scrum',
        year: 'Sept 2025 – Jan 2026',
        colorHex: 0x00f0ff,
        accentCss: '#00f0ff',
        metrics: [
          { label: 'LEGACY REFACTORED', value: '30+ Modul' },
          { label: 'SKEMA DB RTHP', value: '15+ Tabel' },
          { label: 'CORE FITUR & API', value: '10+ Fitur' }
        ],
        stack: ['CodeIgniter 4', 'Generative AI Integration', 'MySQL / Relational DB', 'RESTful API', 'Agile Scrum', 'UML', 'Regression Testing'],
        problem: 'Dua tantangan utama: (1) Produk SaaS estimasi biaya konstruksi memiliki lebih dari 30 modul legacy yang sulit dipelihara dan membutuhkan percepatan proses estimasi biaya; (2) Proyek sistem pemerintahan RTHP (Ruang Terbuka Hijau Publik) termasuk tender DLH Kota Yogyakarta membutuhkan analisis alur proses end-to-end dan arsitektur backend yang terintegrasi.',
        solution: 'Melakukan refactoring >30 modul codebase lama ke library baru hingga menekan bug berulang secara signifikan, serta membangun fitur AI Generatif untuk mengotomasi estimasi biaya konstruksi. Untuk sistem RTHP, menganalisis kebutuhan bisnis, merancang alur end-to-end (>10 fitur utama), mendesain >15 tabel database relasional, membangun >8 endpoint API utama dengan CodeIgniter 4, serta melakukan pengujian fungsional/regresi dan koordinasi langsung dengan stakeholder DLH Kota Yogyakarta.',
        diagram: [
          '[A. SaaS Estimasi Konstruksi] ──> [Refactoring 30+ Modul Legacy] + [Modul AI Generatif Otomasi RAB]',
          '',
          '[B. Sistem Pemerintahan RTHP & Tender DLH Kota Yogyakarta]',
          '     [Requirement Gathering Stakeholder] ──> [Desain End-to-End 10+ Fitur & 15+ Tabel Relasional]',
          '                                                      │',
          '                                                      ▼',
          '     [Validasi Acceptance Criteria & Regression Test] <── [Backend CodeIgniter 4 (8+ Main API Endpoints)]'
        ],
        adr: [
          'Merancang skema database relasional (>15 tabel) terlebih dahulu sebelum penulisan endpoint API CodeIgniter 4 untuk menjamin integrasi data antar-modul RTHP berjalan seamless.',
          'Mengintegrasikan AI Generatif pada alur perhitungan estimasi biaya konstruksi untuk memangkas waktu penyusunan estimasi manual.',
          'Menjalankan pengujian fungsional dan regresi secara ketat terhadap acceptance criteria sebelum demonstrasi ke stakeholder eksternal (DLH Kota Yogyakarta).'
        ]
      },
      {
        id: 'javan',
        slot: 'MOD_03',
        title: 'SaaS Content Management System (CMS) & WhatsApp Blast Platform',
        shortTitle: 'CMS & WA Blast SaaS',
        company: 'PT Javan Cipta Solusi',
        category: 'System Analyst & QA Tester // SDLC & Agile',
        year: 'Juli 2025 – Sept 2025',
        colorHex: 0x10b981,
        accentCss: '#10b981',
        metrics: [
          { label: 'TECHNICAL TASKS', value: '40+ Tasks' },
          { label: 'DOKUMEN UTAMA', value: 'PRD/SRS/SDD' },
          { label: 'TIM AGILE SCRUM', value: '3-5 Dev' }
        ],
        stack: ['PRD / SRS / SDD', 'UML Diagrams', 'End-to-End Testing', 'UAT Validation', 'Bug Tracking', 'Test Case Design', 'Agile Ceremonies'],
        problem: 'Dalam pengembangan 2 produk SaaS (CMS dan platform WhatsApp Blast), dibutuhkan jembatan teknis yang presisi agar kebutuhan bisnis dapat dieksekusi oleh tim lintas fungsi (3–5 developer) tanpa ambiguitas, sekaligus memastikan kualitas rilis bebas dari defect kritis saat User Acceptance Testing (UAT).',
        solution: 'Menyusun dokumen PRD, SRS, dan SDD komprehensif sebagai acuan utama tim engineering, lalu memecahnya menjadi >40 task teknis yang siap dikerjakan dalam sprint Agile (sprint planning, daily stand-up, sprint review). Menyusun test case, skenario pengujian, mengeksekusi pengujian end-to-end serta validasi UAT berdasarkan acceptance criteria hingga menurunkan tingkat defect secara terukur.',
        diagram: [
          '[Kebutuhan Bisnis: SaaS CMS & WhatsApp Blast]',
          '        │',
          '        ▼',
          '[Penyusunan Dokumen PRD, SRS & SDD] ──> [Breakdown 40+ Actionable Technical Tasks]',
          '                                                      │',
          '                                                      ▼',
          '[Sprint Execution (3-5 Devs)] ──> [E2E Test Case & Defect Tracking] ──> [Validasi UAT & Sign-Off]'
        ],
        adr: [
          'Menetapkan Acceptance Criteria yang terukur pada setiap dokumen PRD/SRS/SDD sehingga developer dan QA memiliki standar validasi yang sama sejak awal sprint.',
          'Memecah fitur besar menjadi >40 task teknis granular untuk mempermudah estimasi beban kerja dan pelacakan progres harian pada Agile ceremonies.',
          'Mengelola siklus hidup bug (defect lifecycle) secara disiplin dari temuan pengujian E2E hingga verifikasi perbaikan sebelum sesi UAT bersama pengguna.'
        ]
      },
      {
        id: 'pkm',
        slot: 'MOD_04',
        title: 'Aplikasi Marketplace Peternakan (PKM-KC)',
        shortTitle: 'PKM-KC Marketplace',
        company: 'Proyek Mandiri PKM-KC',
        category: 'Project Manager & System Analyst',
        year: 'Mei 2024 – Agu 2024',
        colorHex: 0xf59e0b,
        accentCss: '#f59e0b',
        metrics: [
          { label: 'ANGGOTA TIM DIPIMPIN', value: '5 Orang' },
          { label: 'PERAN UTAMA', value: 'PM & Analyst' },
          { label: 'CAKUPAN SIKLUS', value: 'End-to-End' }
        ],
        stack: ['Project Management', 'Requirement Gathering', 'System Architecture', 'UML Modeling', 'Figma Wireframing', 'Timeline & Milestone'],
        problem: 'Peternak lokal dan pembeli hewan ternak mengalami kendala transparansi informasi, jangkauan pasar, dan alur transaksi yang belum terdigitalisasi. Tim beranggotakan 5 orang membutuhkan kepemimpinan proyek, pembagian tugas, dan spesifikasi kebutuhan sistem yang jelas agar selesai tepat waktu.',
        solution: 'Memimpin tim beranggotakan 5 orang dari tahap konsep hingga aplikasi selesai. Melaksanakan sesi requirement gathering langsung bersama peternak dan pembeli, menganalisis kebutuhan sistem, merancang arsitektur solusi, menyusun timeline & milestone proyek, serta memantau kepatuhan terhadap scope dan standar kualitas.',
        diagram: [
          '[Riset Lapangan & Requirement Gathering: Peternak & Pembeli]',
          '        │',
          '        ▼',
          '[Perencanaan Desain Solusi, UML & Arsitektur Marketplace]',
          '        │',
          '        ▼',
          '[Manajemen Milestone & Distribusi Task (5 Anggota Tim)] ──> [Quality Control & Penyelesaian PKM-KC]'
        ],
        adr: [
          'Melibatkan stakeholder utama (peternak & pembeli) sejak fase requirement gathering awal agar fitur pencarian, negosiasi, dan manajemen ternak sesuai dengan kondisi lapangan.',
          'Menetapkan milestone mingguan dan pembagian peran yang jelas bagi 5 anggota tim untuk menjaga ketepatan waktu penyelesaian program PKM-KC.'
        ]
      }
    ];

    const CHRONICLE_DATA = {
      work: [
        {
          role: 'Fullstack Developer',
          org: 'PT Indo Techno Medic',
          period: 'Juni 2026 – Sekarang',
          badge: 'CURRENT // FULLSTACK',
          color: 'text-industrial-orange border-industrial-orange/40',
          points: [
            'Mengembangkan & mengkustomisasi SIMRS (CodeIgniter 3 & PostgreSQL) untuk 5 RS: RSUD Caruban, RSUD Cilacap, RSU Astrini, RSUD Blora, dan RSUD Slawi.',
            'Membangun Sistem Informasi Dokumentasi Panduan Penggunaan SIMRS menggunakan Laravel 12 & PostgreSQL untuk pengguna RS dan tim internal.'
          ]
        },
        {
          role: 'System Analyst & Backend Developer (Magang)',
          org: 'PT Swevel Universal Media',
          period: 'September 2025 – Januari 2026',
          badge: 'AGILE SCRUM // SA & BACKEND',
          color: 'text-industrial-cyan border-industrial-cyan/40',
          points: [
            'Refactoring >30 modul codebase lama ke library baru dan mengembangkan fitur AI Generatif untuk otomasi estimasi biaya konstruksi.',
            'Merancang alur proses end-to-end sistem pemerintahan RTHP (>10 fitur utama, >15 tabel database relasional, >8 endpoint API CodeIgniter 4).',
            'Melaksanakan pengujian fungsional & regresi serta berkontribusi langsung dalam proyek tender DLH Kota Yogyakarta.'
          ]
        },
        {
          role: 'System Analyst & QA Tester (Magang)',
          org: 'PT Javan Cipta Solusi',
          period: 'Juli 2025 – September 2025',
          badge: 'SDLC // SA & QA TESTER',
          color: 'text-emerald-400 border-emerald-500/40',
          points: [
            'Menyusun dokumen PRD, SRS, dan SDD untuk 2 produk SaaS (CMS & WhatsApp Blast) serta menguraikannya menjadi >40 task teknis bagi tim 3–5 developer.',
            'Mengeksekusi pengujian sistem E2E, membuat test case/skenario uji, melacak defect, dan memimpin validasi UAT hingga menurunkan tingkat bug secara terukur.'
          ]
        },
        {
          role: 'Administrasi - Pengembangan Bisnis',
          org: 'UTY Software House',
          period: 'Juli 2024 – Januari 2026',
          badge: 'BUSINESS DEV & ADMIN',
          color: 'text-amber-400 border-amber-500/40',
          points: [
            'Mengelola dokumentasi bisnis, dokumen kerja sama, dan proses administrasi untuk proyek-proyek perangkat lunak yang sedang berjalan.',
            'Memfasilitasi komunikasi antara tim pengembangan internal dan klien eksternal untuk menjaga keselarasan deliverable.'
          ]
        }
      ],
      edu: [
        {
          role: 'Sarjana Komputer (S1) — Sistem Informasi (IPK: 3,88 / 4,00)',
          org: 'Universitas Teknologi Yogyakarta (UTY)',
          period: 'September 2022 – Maret 2026',
          badge: 'CUM LAUDE // IPK 3.88',
          color: 'text-industrial-orange border-industrial-orange/40',
          points: [
            'Fokus pada Analisis & Desain Sistem Informasi, Rekayasa Perangkat Lunak, Manajemen Proyek TI, Basis Data Relasional, dan Pengujian Kualitas Perangkat Lunak.',
            'Aktif dalam pengembangan proyek riset mahasiswa (PKM-KC), kepengurusan inti himpunan mahasiswa (HMSI), serta operasional UTY Software House.'
          ]
        },
        {
          role: 'Sertifikasi & Pelatihan Profesional',
          org: 'Dicoding Indonesia & Altair',
          period: '2024 – 2025',
          badge: 'VERIFIED CREDENTIALS',
          color: 'text-industrial-cyan border-industrial-cyan/40',
          points: [
            'Sertifikasi Frontend & Backend Developer — Dicoding (2025).',
            'Sertifikasi Profesional Data Engineering — Altair (2024) dengan penguasaan pemodelan data & RapidMiner.'
          ]
        },
        {
          role: 'Jurusan MIPA',
          org: 'SMA Negeri 1 Kokap (Kulon Progo, DI Yogyakarta)',
          period: '2019 – 2022',
          badge: 'HIGH SCHOOL // MIPA',
          color: 'text-emerald-400 border-emerald-500/40',
          points: [
            'Fondasi kuat dalam matematika, logika analitis, dan pemecahan masalah terstruktur.'
          ]
        }
      ],
      org: [
        {
          role: 'Sekretaris Umum',
          org: 'Himpunan Mahasiswa Sistem Informasi (HMSI) — UTY',
          period: 'Oktober 2023 – Oktober 2024',
          badge: 'EXECUTIVE BOARD LEADERSHIP',
          color: 'text-industrial-orange border-industrial-orange/40',
          points: [
            'Mengelola seluruh dokumentasi organisasi, notulensi rapat, proposal program, dan korespondensi formal himpunan.',
            'Mengoordinasikan alur informasi lintas divisi serta membimbing tim sekretaris kegiatan agar seluruh administrasi akurat tanpa kesalahan.'
          ]
        },
        {
          role: 'Manajer Proyek (Project Manager)',
          org: 'PKM-KC Marketplace Peternakan',
          period: 'Mei 2024 – Agustus 2024',
          badge: 'PROJECT MANAGEMENT',
          color: 'text-industrial-cyan border-industrial-cyan/40',
          points: [
            'Memimpin tim beranggotakan 5 orang dari tahap konsep, sesi requirement gathering bersama peternak & pembeli, hingga penyelesaian aplikasi.',
            'Menyusun timeline, milestone, pembagian tugas, serta memantau kepatuhan terhadap scope dan kualitas sistem.'
          ]
        }
      ]
    };

    const SKILL_NODES = [
      {
        id: 'sa',
        code: 'NODE_01',
        title: 'System Analysis & Technical Documentation',
        desc: 'Menerjemahkan kebutuhan bisnis stakeholder menjadi spesifikasi teknis yang terstruktur, diagram alur sistem, dan puluhan task yang siap dieksekusi tim developer.',
        tags: ['Requirement Gathering', 'Penyusunan PRD / SRS / SDD', 'Desain Diagram UML', 'Agile Scrum & SDLC', 'Task Breakdown (40+ Tasks)', 'Business Process Modeling']
      },
      {
        id: 'qa',
        code: 'NODE_02',
        title: 'QA Software Testing & UAT Validation',
        desc: 'Menjamin kualitas rilis produk melalui perencanaan skenario pengujian menyeluruh, pengujian regresi & end-to-end, pelacakan defect, hingga persetujuan UAT.',
        tags: ['Test Case & Scenario Design', 'End-to-End & Regression Testing', 'Validasi UAT & Acceptance Criteria', 'Bug Tracking & Defect Reporting', 'API Testing (Apidog)']
      },
      {
        id: 'fullstack',
        code: 'NODE_03',
        title: 'Fullstack Web & SIMRS Development',
        desc: 'Pengembangan aplikasi web skala enterprise (termasuk SIMRS di 5 RSUD dan portal dokumentasi) serta integrasi fitur AI generatif dan RESTful API.',
        tags: ['PHP (Laravel 12)', 'CodeIgniter 3 & 4', 'JavaScript (React, Node.js)', 'HTML5 & CSS3', 'REST API Development', 'Legacy Code Refactoring']
      },
      {
        id: 'db',
        code: 'NODE_04',
        title: 'Database Architecture & Data Engineering',
        desc: 'Perancangan skema database relasional (>15 tabel terintegrasi), optimasi query sistem informasi rumah sakit, serta pengolahan data analitis.',
        tags: ['PostgreSQL', 'MySQL', 'Relational Schema Design', 'Data Engineering (Altair)', 'RapidMiner']
      },
      {
        id: 'uiux',
        code: 'NODE_05',
        title: 'Wireframing, API Tooling & Version Control',
        desc: 'Visualisasi rancangan antarmuka sebelum tahap coding serta kolaborasi pengujian endpoint API dan manajemen repositori kode.',
        tags: ['Figma Wireframing', 'Apidog API Documentation', 'Git Version Control', 'System Prototyping']
      },
      {
        id: 'pm',
        code: 'NODE_06',
        title: 'Agile Project Management & Leadership',
        desc: 'Kolaborasi lintas fungsi dalam sprint Agile Scrum, manajemen timeline proyek, fasilitasi komunikasi klien eksternal, dan kepemimpinan organisasi.',
        tags: ['Taiga', 'Trello', 'Notion', 'Analytical Problem Solving', 'Stakeholder Communication', 'Team Leadership']
      }
    ];

    /*************************************************************************
     * 3. TACTILE WEB AUDIO SYNTHESIZER
     *************************************************************************/
    class TactileSoundEngine {
      constructor() {
        this.ctx = null;
      }
      init() {
        if (!this.ctx) {
          const AudioCtx = window.AudioContext || window.webkitAudioContext;
          if (AudioCtx) this.ctx = new AudioCtx();
        }
        if (this.ctx && this.ctx.state === 'suspended') {
          this.ctx.resume();
        }
      }
      playClick(freq = 900, duration = 0.035) {
        if (systemStore.isAudioMuted.get()) return;
        this.init();
        if (!this.ctx) return;

        const osc = this.ctx.createOscillator();
        const gain = this.ctx.createGain();
        osc.type = 'triangle';
        osc.frequency.setValueAtTime(freq, this.ctx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(180, this.ctx.currentTime + duration);

        gain.gain.setValueAtTime(0.11, this.ctx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, this.ctx.currentTime + duration);

        osc.connect(gain);
        gain.connect(this.ctx.destination);
        osc.start();
        osc.stop(this.ctx.currentTime + duration);
      }
      playServoDock() {
        if (systemStore.isAudioMuted.get()) return;
        this.init();
        if (!this.ctx) return;

        const now = this.ctx.currentTime;
        const osc = this.ctx.createOscillator();
        const gain = this.ctx.createGain();
        osc.type = 'sawtooth';
        osc.frequency.setValueAtTime(140, now);
        osc.frequency.linearRampToValueAtTime(320, now + 0.25);
        osc.frequency.setValueAtTime(220, now + 0.26);
        osc.frequency.exponentialRampToValueAtTime(85, now + 0.55);

        gain.gain.setValueAtTime(0.06, now);
        gain.gain.linearRampToValueAtTime(0.1, now + 0.25);
        gain.gain.exponentialRampToValueAtTime(0.001, now + 0.58);

        osc.connect(gain);
        gain.connect(this.ctx.destination);
        osc.start(now);
        osc.stop(now + 0.6);
      }
      playBootChord() {
        if (systemStore.isAudioMuted.get()) return;
        this.init();
        if (!this.ctx) return;

        const notes = [220, 330, 440, 660];
        notes.forEach((n, idx) => {
          const osc = this.ctx.createOscillator();
          const gain = this.ctx.createGain();
          const start = this.ctx.currentTime + idx * 0.06;
          osc.type = 'sine';
          osc.frequency.setValueAtTime(n, start);
          gain.gain.setValueAtTime(0.08, start);
          gain.gain.exponentialRampToValueAtTime(0.0008, start + 0.7);
          osc.connect(gain);
          gain.connect(this.ctx.destination);
          osc.start(start);
          osc.stop(start + 0.75);
        });
      }
    }
    const sfx = new TactileSoundEngine();

    /*************************************************************************
     * 4. THREE.JS SCENE & PROCEDURAL "LIVING SYSTEM CORE" BUILDER
     *************************************************************************/
    const container = document.getElementById('webgl-container');
    const scene = new THREE.Scene();
    scene.background = new THREE.Color(0x0b0d10);
    scene.fog = new THREE.FogExp2(0x0b0d10, 0.038);

    const camera = new THREE.PerspectiveCamera(42, window.innerWidth / window.innerHeight, 0.1, 100);
    camera.position.set(0, 2.5, 13);

    const renderer = new THREE.WebGLRenderer({ antialias: true, powerPreference: 'high-performance' });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.toneMapping = THREE.ACESFilmicToneMapping;
    renderer.toneMappingExposure = 1.15;
    container.appendChild(renderer.domElement);

    const camLookTarget = new THREE.Vector3(0, 0.2, 0);

    // Lighting
    const ambientLight = new THREE.AmbientLight(0xdbeafe, 0.68);
    scene.add(ambientLight);

    const keyLight = new THREE.DirectionalLight(0xffffff, 1.3);
    keyLight.position.set(6, 10, 8);
    scene.add(keyLight);

    const rimLightCyan = new THREE.PointLight(0x00f0ff, 2.2, 14);
    rimLightCyan.position.set(4.5, 2.5, -3);
    scene.add(rimLightCyan);

    const coreGlowLight = new THREE.PointLight(0xff5500, 2.5, 8);
    coreGlowLight.position.set(0.3, 0.2, 1.8);
    scene.add(coreGlowLight);

    const machineRoot = new THREE.Group();
    scene.add(machineRoot);

    const solidMaterials = [];
    const cartridgeMeshes = [];
    const cartridgeGroups = {};
    const skillNodeMeshes = [];
    const chronicleCylinders = [];
    const coolingFans = [];
    const opticalShaders = [];

    function registerMaterial(mat) {
      solidMaterials.push({
        mat,
        origWireframe: mat.wireframe,
        origColor: mat.color ? mat.color.clone() : null
      });
      return mat;
    }

    function createCartridgeLabelTexture(mod) {
      const c = document.createElement('canvas');
      c.width = 512;
      c.height = 128;
      const ctx = c.getContext('2d');

      ctx.fillStyle = '#12161f';
      ctx.fillRect(0, 0, 512, 128);

      ctx.fillStyle = mod.accentCss;
      ctx.fillRect(0, 0, 26, 128);

      ctx.fillStyle = mod.accentCss;
      ctx.font = 'bold 24px "JetBrains Mono", monospace';
      ctx.fillText(`${mod.slot} // ${mod.company.toUpperCase().slice(0, 18)}`, 42, 42);

      ctx.fillStyle = '#ffffff';
      ctx.font = 'bold 30px "Space Grotesk", sans-serif';
      ctx.fillText(mod.shortTitle.toUpperCase(), 42, 88);

      ctx.fillStyle = '#334155';
      for (let i = 0; i < 7; i++) {
        ctx.fillRect(438 + i * 8, 24, 4, 80);
      }

      const tex = new THREE.CanvasTexture(c);
      tex.anisotropy = 4;
      return tex;
    }

    const chassisDarkMat = registerMaterial(new THREE.MeshStandardMaterial({
      color: 0x1a202c,
      roughness: 0.45,
      metalness: 0.65
    }));

    const chassisLightMat = registerMaterial(new THREE.MeshStandardMaterial({
      color: 0xd1d5db,
      roughness: 0.35,
      metalness: 0.3
    }));

    const darkMetalMat = registerMaterial(new THREE.MeshStandardMaterial({
      color: 0x0f1319,
      roughness: 0.3,
      metalness: 0.85
    }));

    const copperMat = registerMaterial(new THREE.MeshStandardMaterial({
      color: 0xd97706,
      roughness: 0.25,
      metalness: 0.9
    }));

    // A. MAIN CHASSIS
    const basePlatform = new THREE.Mesh(new THREE.BoxGeometry(7.6, 0.35, 4.4), darkMetalMat);
    basePlatform.position.set(0, -2.05, 0);
    machineRoot.add(basePlatform);

    const gridHelper = new THREE.GridHelper(26, 26, 0x262d3a, 0x151922);
    gridHelper.position.y = -2.23;
    scene.add(gridHelper);

    const mainBody = new THREE.Mesh(new THREE.BoxGeometry(6.8, 3.6, 2.8), chassisDarkMat);
    mainBody.position.set(0, -0.1, -0.3);
    machineRoot.add(mainBody);

    const topBezel = new THREE.Mesh(new THREE.BoxGeometry(7.0, 0.22, 3.1), chassisLightMat);
    topBezel.position.set(0, 1.8, -0.2);
    machineRoot.add(topBezel);

    const bottomBezel = new THREE.Mesh(new THREE.BoxGeometry(7.0, 0.22, 3.1), chassisLightMat);
    bottomBezel.position.set(0, -1.8, -0.2);
    machineRoot.add(bottomBezel);

    // B. LEFT MODULE RACK & 4 CARTRIDGES
    const rackHousing = new THREE.Mesh(new THREE.BoxGeometry(2.3, 3.1, 2.2), darkMetalMat);
    rackHousing.position.set(-2.05, 0.0, 0.25);
    machineRoot.add(rackHousing);

    PROJECT_MODULES.forEach((mod, index) => {
      const slotY = 0.95 - index * 0.64;
      const homePos = new THREE.Vector3(-2.05, slotY, 0.85);

      const cartGroup = new THREE.Group();
      cartGroup.position.copy(homePos);
      cartGroup.userData = {
        projectId: mod.id,
        homePos: homePos.clone(),
        slotY: slotY,
        isDocked: false
      };

      const bodyMat = registerMaterial(new THREE.MeshStandardMaterial({
        color: 0x222936,
        roughness: 0.35,
        metalness: 0.55
      }));
      const cartBody = new THREE.Mesh(new THREE.BoxGeometry(1.75, 0.46, 1.35), bodyMat);
      cartBody.userData = { projectId: mod.id, parentGroup: cartGroup };
      cartridgeMeshes.push(cartBody);
      cartGroup.add(cartBody);

      const labelMat = new THREE.MeshBasicMaterial({ map: createCartridgeLabelTexture(mod) });
      const labelMesh = new THREE.Mesh(new THREE.PlaneGeometry(1.62, 0.38), labelMat);
      labelMesh.position.set(0, 0, 0.68);
      cartGroup.add(labelMesh);

      const ledMat = new THREE.MeshBasicMaterial({ color: mod.colorHex });
      const ledStrip = new THREE.Mesh(new THREE.BoxGeometry(0.12, 0.38, 0.05), ledMat);
      ledStrip.position.set(-0.78, 0, 0.69);
      cartGroup.add(ledStrip);

      const handle = new THREE.Mesh(new THREE.BoxGeometry(0.22, 0.14, 0.18), chassisLightMat);
      handle.position.set(0.62, 0, 0.74);
      cartGroup.add(handle);

      cartridgeGroups[mod.id] = {
        group: cartGroup,
        ledMat: ledMat,
        bodyMat: bodyMat,
        modData: mod
      };

      machineRoot.add(cartGroup);
    });

    // C. CENTRAL CORE SLOT & GANTRY
    const coreChamber = new THREE.Group();
    coreChamber.position.set(0.55, 0.05, 0.35);
    machineRoot.add(coreChamber);

    const coreRing = new THREE.Mesh(new THREE.TorusGeometry(0.98, 0.09, 16, 48), chassisLightMat);
    coreRing.position.set(0, 0, 0.55);
    coreChamber.add(coreRing);

    const coreEnergyMat = new THREE.MeshBasicMaterial({ color: 0xff5500 });
    const coreEnergyRing = new THREE.Mesh(new THREE.TorusGeometry(0.82, 0.035, 12, 40), coreEnergyMat);
    coreEnergyRing.position.set(0, 0, 0.58);
    coreChamber.add(coreEnergyRing);

    const dockBay = new THREE.Mesh(new THREE.BoxGeometry(1.92, 0.62, 1.2), darkMetalMat);
    dockBay.position.set(0, 0, 0.25);
    coreChamber.add(dockBay);

    const loaderGantry = new THREE.Mesh(new THREE.BoxGeometry(4.6, 0.09, 0.12), copperMat);
    loaderGantry.position.set(-0.7, 0.95, 1.48);
    machineRoot.add(loaderGantry);

    // D. CHRONICLE MEMORY BANK CYLINDERS (Lower Center Deck for State 3: CHRONICLE)
    const chronicleDeck = new THREE.Group();
    chronicleDeck.position.set(0.55, -1.35, 0.95);
    machineRoot.add(chronicleDeck);

    for (let i = 0; i < 4; i++) {
      const cylMat = registerMaterial(new THREE.MeshStandardMaterial({
        color: 0x1e293b,
        emissive: 0xf59e0b,
        emissiveIntensity: 0.25,
        roughness: 0.3,
        metalness: 0.8
      }));
      const cyl = new THREE.Mesh(new THREE.CylinderGeometry(0.16, 0.16, 0.45, 20), cylMat);
      cyl.position.set(-0.75 + i * 0.5, 0, 0);
      chronicleCylinders.push(cyl);
      chronicleDeck.add(cyl);
    }

    // E. OPTICAL DATA CABLES (Custom GLSL Shader)
    const cableVertexShader = `
      varying vec2 vUv;
      void main() {
        vUv = uv;
        gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
      }
    `;

    const cableFragmentShader = `
      uniform float uTime;
      uniform vec3 uColor;
      uniform float uActive;
      varying vec2 vUv;

      void main() {
        vec3 baseColor = vec3(0.06, 0.08, 0.12);
        float wave = sin((vUv.x * 18.0) - (uTime * 6.5)) * 0.5 + 0.5;
        float sharpPulse = pow(wave, 5.0);
        vec3 finalColor = mix(baseColor, uColor, sharpPulse * uActive + (0.15 * uActive));
        gl_FragColor = vec4(finalColor, 1.0);
      }
    `;

    const cableOffsets = [0.55, 0.18, -0.18, -0.55];
    cableOffsets.forEach((yOff, idx) => {
      const curve = new THREE.CatmullRomCurve3([
        new THREE.Vector3(1.45, yOff * 0.5, 0.75),
        new THREE.Vector3(2.4, yOff * 0.8, 0.95),
        new THREE.Vector3(3.4, yOff * 1.1, 0.4),
        new THREE.Vector3(4.8, yOff * 1.3, -0.2)
      ]);
      const tubeGeo = new THREE.TubeGeometry(curve, 40, 0.055, 8, false);
      const shaderMat = new THREE.ShaderMaterial({
        vertexShader: cableVertexShader,
        fragmentShader: cableFragmentShader,
        uniforms: {
          uTime: { value: idx * 0.7 },
          uColor: { value: new THREE.Color(0xff5500) },
          uActive: { value: 0.25 }
        }
      });
      opticalShaders.push(shaderMat);
      const cableMesh = new THREE.Mesh(tubeGeo, shaderMat);
      machineRoot.add(cableMesh);
    });

    // F. TOP DECK SKILL NODES & COOLING FANS (State 4: NODES)
    const topDeckGroup = new THREE.Group();
    topDeckGroup.position.set(0, 1.92, -0.2);
    machineRoot.add(topDeckGroup);

    [-2.2, -0.9].forEach((xPos) => {
      const fanHousing = new THREE.Mesh(new THREE.CylinderGeometry(0.52, 0.52, 0.14, 24), darkMetalMat);
      fanHousing.position.set(xPos, 0.05, 0);
      topDeckGroup.add(fanHousing);

      const bladeGroup = new THREE.Group();
      bladeGroup.position.set(xPos, 0.08, 0);
      for (let i = 0; i < 6; i++) {
        const blade = new THREE.Mesh(new THREE.BoxGeometry(0.42, 0.02, 0.11), copperMat);
        blade.rotation.y = (i * Math.PI) / 3;
        bladeGroup.add(blade);
      }
      coolingFans.push(bladeGroup);
      topDeckGroup.add(bladeGroup);
    });

    SKILL_NODES.forEach((node, idx) => {
      const col = idx % 3;
      const row = Math.floor(idx / 3);
      const xPos = 0.45 + col * 0.95;
      const zPos = -0.45 + row * 0.9;

      const chipMat = registerMaterial(new THREE.MeshStandardMaterial({
        color: 0x1e293b,
        emissive: idx === 0 ? 0x00f0ff : 0x000000,
        emissiveIntensity: idx === 0 ? 0.5 : 0,
        roughness: 0.3,
        metalness: 0.7
      }));

      const chipMesh = new THREE.Mesh(new THREE.BoxGeometry(0.72, 0.16, 0.72), chipMat);
      chipMesh.position.set(xPos, 0.08, zPos);
      chipMesh.userData = { skillId: node.id, chipMat };
      skillNodeMeshes.push(chipMesh);
      topDeckGroup.add(chipMesh);

      const pinsFrame = new THREE.Mesh(new THREE.BoxGeometry(0.78, 0.04, 0.78), copperMat);
      pinsFrame.position.set(xPos, 0.01, zPos);
      topDeckGroup.add(pinsFrame);
    });

    // G. COMM PORT & FIBER JACK (State 5: UPLINK)
    const commPortHousing = new THREE.Mesh(new THREE.BoxGeometry(1.2, 0.9, 0.4), chassisLightMat);
    commPortHousing.position.set(2.55, -1.1, 1.15);
    machineRoot.add(commPortHousing);

    const commSocket = new THREE.Mesh(new THREE.CylinderGeometry(0.22, 0.22, 0.45, 20), darkMetalMat);
    commSocket.rotation.x = Math.PI / 2;
    commSocket.position.set(2.55, -1.1, 1.18);
    machineRoot.add(commSocket);

    const uplinkJackGroup = new THREE.Group();
    uplinkJackGroup.position.set(2.55, -1.1, 2.25);
    const jackBody = new THREE.Mesh(new THREE.CylinderGeometry(0.16, 0.2, 0.55, 16), copperMat);
    jackBody.rotation.x = Math.PI / 2;
    uplinkJackGroup.add(jackBody);

    const jackLed = new THREE.Mesh(
      new THREE.CylinderGeometry(0.17, 0.17, 0.08, 16),
      new THREE.MeshBasicMaterial({ color: 0x10b981 })
    );
    jackLed.rotation.x = Math.PI / 2;
    jackLed.position.z = 0.2;
    uplinkJackGroup.add(jackLed);
    machineRoot.add(uplinkJackGroup);

    /*************************************************************************
     * 5. CAMERA RIG & CHOREOGRAPHY (GSAP)
     *************************************************************************/
    const CAMERA_STATES = {
      BOOT:       { pos: { x: 0, y: 3.5, z: 14.0 }, target: { x: 0, y: 0, z: 0 } },
      OVERVIEW:   { pos: { x: -0.35, y: 1.25, z: 7.5 }, target: { x: -0.35, y: 0.0, z: 0 } },
      MODULES:    { pos: { x: -1.15, y: 0.35, z: 4.9 }, target: { x: -0.95, y: 0.1, z: 0.4 } },
      CASE_STUDY: { pos: { x: 1.65, y: 0.2, z: 4.85 }, target: { x: 2.15, y: 0.05, z: 0.2 } },
      CHRONICLE:  { pos: { x: 1.35, y: -0.65, z: 4.7 }, target: { x: 1.55, y: -0.95, z: 0.4 } },
      NODES:      { pos: { x: 0.8, y: 4.6, z: 3.6 }, target: { x: 0.6, y: 1.8, z: -0.2 } },
      UPLINK:     { pos: { x: 3.1, y: -0.75, z: 3.8 }, target: { x: 3.35, y: -1.0, z: 0.8 } }
    };

    function moveCameraToState(stateName, duration = 1.2) {
      const cfg = CAMERA_STATES[stateName] || CAMERA_STATES.OVERVIEW;
      const isMobile = window.innerWidth < 768;
      const zMultiplier = isMobile ? 1.32 : 1.0;

      gsap.to(camera.position, {
        x: cfg.pos.x,
        y: cfg.pos.y,
        z: cfg.pos.z * zMultiplier,
        duration: duration,
        ease: 'power3.inOut'
      });

      gsap.to(camLookTarget, {
        x: isMobile && stateName === 'CASE_STUDY' ? 0.5 : cfg.target.x,
        y: cfg.target.y,
        z: cfg.target.z,
        duration: duration,
        ease: 'power3.inOut'
      });
    }

    /*************************************************************************
     * 6. CARTRIDGE DOCKING & EJECT ANIMATION CHOREOGRAPHY
     *************************************************************************/
    let currentlyDockedId = null;
    let isAnimatingCartridge = false;

    function animateCartridgeToCore(projectId) {
      if (isAnimatingCartridge) return;
      const targetCart = cartridgeGroups[projectId];
      if (!targetCart) return;

      isAnimatingCartridge = true;
      sfx.playServoDock();

      const tl = gsap.timeline({
        onComplete: () => {
          isAnimatingCartridge = false;
        }
      });

      if (currentlyDockedId && currentlyDockedId !== projectId) {
        const prevCart = cartridgeGroups[currentlyDockedId];
        if (prevCart) {
          prevCart.group.userData.isDocked = false;
          tl.to(prevCart.group.position, { z: 1.55, duration: 0.25, ease: 'power2.out' })
            .to(prevCart.group.position, {
              x: prevCart.group.userData.homePos.x,
              y: prevCart.group.userData.homePos.y,
              duration: 0.35,
              ease: 'power2.inOut'
            })
            .to(prevCart.group.position, {
              z: prevCart.group.userData.homePos.z,
              duration: 0.22,
              ease: 'power2.in'
            });
        }
      }

      currentlyDockedId = projectId;
      targetCart.group.userData.isDocked = true;

      tl.to(loaderGantry.position, { y: targetCart.group.userData.slotY, duration: 0.25, ease: 'power2.out' }, '<')
        .to(targetCart.group.position, { z: 1.65, duration: 0.32, ease: 'back.out(1.4)' })
        .to([targetCart.group.position, loaderGantry.position], {
          y: 0.05,
          duration: 0.42,
          ease: 'power3.inOut'
        })
        .to(targetCart.group.position, {
          x: 0.55,
          duration: 0.42,
          ease: 'power3.inOut'
        }, '<')
        .to(targetCart.group.position, {
          z: 0.68,
          duration: 0.28,
          ease: 'power4.in',
          onComplete: () => {
            sfx.playClick(420, 0.08);
            const modColor = new THREE.Color(targetCart.modData.colorHex);
            coreEnergyMat.color.copy(modColor);
            coreGlowLight.color.copy(modColor);
            opticalShaders.forEach(s => {
              s.uniforms.uColor.value.copy(modColor);
              gsap.to(s.uniforms.uActive, { value: 1.0, duration: 0.4 });
            });
          }
        });
    }

    function ejectCurrentCartridge() {
      if (!currentlyDockedId || isAnimatingCartridge) return;
      const cart = cartridgeGroups[currentlyDockedId];
      if (!cart) return;

      isAnimatingCartridge = true;
      sfx.playServoDock();

      cart.group.userData.isDocked = false;
      currentlyDockedId = null;

      opticalShaders.forEach(s => {
        gsap.to(s.uniforms.uActive, { value: 0.22, duration: 0.4 });
      });

      gsap.timeline({
        onComplete: () => {
          isAnimatingCartridge = false;
        }
      })
        .to(cart.group.position, { z: 1.65, duration: 0.28, ease: 'power2.out' })
        .to(cart.group.position, {
          x: cart.group.userData.homePos.x,
          y: cart.group.userData.homePos.y,
          duration: 0.42,
          ease: 'power3.inOut'
        })
        .to(loaderGantry.position, {
          y: cart.group.userData.homePos.y,
          duration: 0.42,
          ease: 'power3.inOut'
        }, '<')
        .to(cart.group.position, {
          z: cart.group.userData.homePos.z,
          duration: 0.25,
          ease: 'power2.in'
        });
    }

    /*************************************************************************
     * 7. RAYCASTER, HOVER TOOLTIP & MOUSE PARALLAX
     *************************************************************************/
    const raycaster = new THREE.Raycaster();
    const mouse = new THREE.Vector2();
    const parallaxOffset = { x: 0, y: 0 };
    let hoveredProjectId = null;

    const tooltipEl = document.getElementById('mesh-tooltip');
    const tooltipSlot = document.getElementById('tooltip-slot');
    const tooltipYear = document.getElementById('tooltip-year');
    const tooltipTitle = document.getElementById('tooltip-title');
    const tooltipRole = document.getElementById('tooltip-role');

    window.addEventListener('mousemove', (e) => {
      mouse.x = (e.clientX / window.innerWidth) * 2 - 1;
      mouse.y = -(e.clientY / window.innerHeight) * 2 + 1;

      parallaxOffset.x = mouse.x * 0.22;
      parallaxOffset.y = mouse.y * 0.14;

      const view = systemStore.currentView.get();
      if (view === 'BOOT') return;
      if (view === 'CASE_STUDY' && e.clientX > window.innerWidth * 0.42) {
        clearHoveredCartridge();
        return;
      }

      raycaster.setFromCamera(mouse, camera);

      if (view === 'NODES') {
        const nodeHits = raycaster.intersectObjects(skillNodeMeshes);
        document.body.style.cursor = nodeHits.length > 0 ? 'pointer' : 'default';
        clearHoveredCartridge();
        return;
      }

      const hits = raycaster.intersectObjects(cartridgeMeshes);
      if (hits.length > 0) {
        const hitId = hits[0].object.userData.projectId;
        document.body.style.cursor = 'pointer';

        if (hoveredProjectId !== hitId) {
          clearHoveredCartridge();
          hoveredProjectId = hitId;
          sfx.playClick(1150, 0.025);

          const cart = cartridgeGroups[hitId];
          if (cart && !cart.group.userData.isDocked && !isAnimatingCartridge) {
            gsap.to(cart.group.position, {
              z: cart.group.userData.homePos.z + 0.32,
              duration: 0.22,
              ease: 'power2.out'
            });
          }

          if (cart) {
            tooltipSlot.textContent = cart.modData.slot;
            tooltipYear.textContent = cart.modData.year;
            tooltipTitle.textContent = cart.modData.shortTitle;
            tooltipRole.textContent = `${cart.modData.company} — ${cart.modData.category.split('//')[0]}`;
            tooltipEl.classList.remove('opacity-0');
          }
        }

        if (hoveredProjectId && cartridgeGroups[hoveredProjectId]) {
          const worldPos = new THREE.Vector3();
          cartridgeGroups[hoveredProjectId].group.getWorldPosition(worldPos);
          worldPos.y += 0.32;
          worldPos.project(camera);

          const screenX = (worldPos.x * 0.5 + 0.5) * window.innerWidth;
          const screenY = (-(worldPos.y * 0.5) + 0.5) * window.innerHeight;
          tooltipEl.style.left = `${screenX}px`;
          tooltipEl.style.top = `${screenY}px`;
        }
      } else {
        document.body.style.cursor = 'default';
        clearHoveredCartridge();
      }
    });

    function clearHoveredCartridge() {
      if (hoveredProjectId && cartridgeGroups[hoveredProjectId]) {
        const cart = cartridgeGroups[hoveredProjectId];
        if (!cart.group.userData.isDocked && !isAnimatingCartridge) {
          gsap.to(cart.group.position, {
            z: cart.group.userData.homePos.z,
            duration: 0.25,
            ease: 'power2.out'
          });
        }
      }
      hoveredProjectId = null;
      tooltipEl.classList.add('opacity-0');
    }

    renderer.domElement.addEventListener('click', () => {
      const view = systemStore.currentView.get();
      if (view === 'BOOT') return;

      raycaster.setFromCamera(mouse, camera);

      if (view === 'NODES') {
        const nodeHits = raycaster.intersectObjects(skillNodeMeshes);
        if (nodeHits.length > 0) {
          const skillId = nodeHits[0].object.userData.skillId;
          sfx.playClick(880, 0.04);
          systemStore.activeSkillId.set(skillId);
          return;
        }
      }

      const cartHits = raycaster.intersectObjects(cartridgeMeshes);
      if (cartHits.length > 0) {
        const projId = cartHits[0].object.userData.projectId;
        clearHoveredCartridge();
        selectAndMountProject(projId);
      }
    });

    /*************************************************************************
     * 8. DOM UI BINDINGS & STORE SUBSCRIPTIONS
     *************************************************************************/
    const drawerEl = document.getElementById('case-study-drawer');
    const bioOverviewCard = document.getElementById('bio-overview-card');
    const quickRackPanel = document.getElementById('quick-rack-panel');
    const chronicleHudPanel = document.getElementById('chronicle-hud-panel');
    const nodesHudPanel = document.getElementById('nodes-hud-panel');
    const uplinkHudPanel = document.getElementById('uplink-hud-panel');
    const hudCamState = document.getElementById('hud-cam-state');
    const hudSlot = document.getElementById('hud-slot');
    const hudMode = document.getElementById('hud-mode');
    const hudInstruction = document.getElementById('hud-instruction');

    const rackButtonsList = document.getElementById('rack-buttons-list');
    const drawerQuickSwitch = document.getElementById('drawer-quick-switch');

    PROJECT_MODULES.forEach((mod) => {
      const btn = document.createElement('button');
      btn.className = 'w-full text-left px-3 py-2 rounded-lg bg-black/40 hover:bg-white/10 border border-white/5 flex items-center justify-between transition-all group';
      btn.innerHTML = `
        <div>
          <div class="font-mono text-[10px] text-slate-400 group-hover:text-white">${mod.slot} // ${mod.company}</div>
          <div class="text-xs font-bold text-slate-200 group-hover:text-white">${mod.shortTitle}</div>
        </div>
        <span class="w-2 h-2 rounded-full" style="background:${mod.accentCss}"></span>
      `;
      btn.addEventListener('click', () => selectAndMountProject(mod.id));
      rackButtonsList.appendChild(btn);

      const pill = document.createElement('button');
      pill.className = 'px-2.5 py-1 rounded font-mono text-xs bg-white/5 hover:bg-white/15 text-slate-300 border border-white/10 transition-all';
      pill.textContent = `${mod.slot}: ${mod.shortTitle}`;
      pill.addEventListener('click', () => selectAndMountProject(mod.id));
      drawerQuickSwitch.appendChild(pill);
    });

    const nodeButtonsGrid = document.getElementById('node-buttons-grid');
    SKILL_NODES.forEach((node) => {
      const btn = document.createElement('button');
      btn.className = 'px-2.5 py-2 rounded bg-black/50 hover:bg-white/10 border border-white/10 text-left truncate transition-all';
      btn.innerHTML = `<span class="text-industrial-cyan">${node.code}:</span> ${node.title.split('&')[0]}`;
      btn.addEventListener('click', () => {
        sfx.playClick(820, 0.04);
        systemStore.activeSkillId.set(node.id);
      });
      nodeButtonsGrid.appendChild(btn);
    });

    function renderChronicleContent(tabKey) {
      const container = document.getElementById('chronicle-content-area');
      const items = CHRONICLE_DATA[tabKey] || [];
      container.innerHTML = items.map(item => `
        <div class="bg-black/50 p-4 rounded-xl border ${item.color} space-y-1.5">
          <div class="flex flex-wrap items-center justify-between gap-2">
            <span class="font-mono text-[10px] px-2 py-0.5 rounded bg-white/5 ${item.color.split(' ')[0]} font-bold">${item.badge}</span>
            <span class="font-mono text-[11px] text-slate-400">${item.period}</span>
          </div>
          <div class="text-sm font-bold text-white">${item.role}</div>
          <div class="font-mono text-xs text-slate-300">${item.org}</div>
          <ul class="list-disc list-inside text-slate-300 space-y-1 pt-1 leading-relaxed">
            ${item.points.map(p => `<li>${p}</li>`).join('')}
          </ul>
        </div>
      `).join('');

      document.querySelectorAll('.chron-tab-btn').forEach(btn => {
        if (btn.dataset.chronTab === tabKey) {
          btn.className = 'chron-tab-btn flex-1 py-1.5 px-2 rounded bg-amber-500 text-black font-bold transition-all';
        } else {
          btn.className = 'chron-tab-btn flex-1 py-1.5 px-2 rounded text-slate-300 hover:text-white transition-all';
        }
      });
    }

    document.querySelectorAll('.chron-tab-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        sfx.playClick(850, 0.03);
        systemStore.activeChronicleTab.set(btn.dataset.chronTab);
      });
    });

    systemStore.activeChronicleTab.subscribe(tab => renderChronicleContent(tab));

    function selectAndMountProject(projectId) {
      systemStore.activeProjectId.set(projectId);
      systemStore.currentView.set('CASE_STUDY');
      animateCartridgeToCore(projectId);
    }

    // Subscribe to `currentView`
    systemStore.currentView.subscribe((view) => {
      if (view === 'BOOT') return;

      moveCameraToState(view);
      hudCamState.textContent = view;

      document.querySelectorAll('.nav-btn').forEach((btn) => {
        const navTarget = btn.dataset.nav;
        const isCurrent = (navTarget === view) || (view === 'CASE_STUDY' && navTarget === 'MODULES');
        if (isCurrent) {
          btn.className = 'nav-btn px-3 py-2 rounded-lg font-mono text-xs font-bold transition-all flex items-center gap-1.5 bg-industrial-orange text-black';
        } else {
          btn.className = 'nav-btn px-3 py-2 rounded-lg font-mono text-xs font-medium text-slate-300 hover:text-white hover:bg-white/5 transition-all flex items-center gap-1.5';
        }
      });

      // Contextual HUD Panels Visibility
      bioOverviewCard.classList.toggle('sm:block', view === 'OVERVIEW');
      bioOverviewCard.classList.toggle('hidden', view !== 'OVERVIEW');

      const showRack = view === 'OVERVIEW' || view === 'MODULES';
      quickRackPanel.classList.toggle('lg:block', showRack);
      quickRackPanel.classList.toggle('hidden', !showRack);

      chronicleHudPanel.classList.toggle('hidden', view !== 'CHRONICLE');
      nodesHudPanel.classList.toggle('hidden', view !== 'NODES');
      uplinkHudPanel.classList.toggle('hidden', view !== 'UPLINK');

      // Highlight Chronicle Cylinders in 3D when in CHRONICLE view
      chronicleCylinders.forEach((cyl, idx) => {
        gsap.to(cyl.position, {
          y: view === 'CHRONICLE' ? 0.18 : 0,
          duration: 0.35,
          delay: idx * 0.05
        });
      });

      if (view === 'CASE_STUDY') {
        drawerEl.classList.remove('translate-x-full');
        hudInstruction.textContent = 'Klik tab BLUEPRINT SRS / DB / QA untuk melihat skema arsitektur & artefak analisis';
      } else {
        drawerEl.classList.add('translate-x-full');
      }

      if (view === 'UPLINK') {
        sfx.playServoDock();
        gsap.to(uplinkJackGroup.position, { z: 1.52, duration: 0.6, ease: 'back.out(1.6)' });
        hudInstruction.textContent = 'Port Uplink Terhubung: Hubungi Nasrun via WhatsApp, Email, atau LinkedIn';
      } else {
        gsap.to(uplinkJackGroup.position, { z: 2.25, duration: 0.4, ease: 'power2.out' });
      }

      if (view === 'OVERVIEW' || view === 'MODULES') {
        hudInstruction.textContent = 'Klik kaset di rak kiri untuk memuat studi kasus ke Central Core';
      } else if (view === 'CHRONICLE') {
        hudInstruction.textContent = 'Menampilkan rekam jejak karier, S1 Sistem Informasi UTY (IPK 3.88), & HMSI';
      } else if (view === 'NODES') {
        hudInstruction.textContent = 'Klik chip prosesor di dek atas untuk melihat keahlian System Analyst, QA, & Dev';
      }
    });

    // Subscribe to `activeProjectId`
    systemStore.activeProjectId.subscribe((projId) => {
      if (!projId) {
        hudSlot.textContent = 'NONE';
        return;
      }
      const mod = PROJECT_MODULES.find(m => m.id === projId);
      if (!mod) return;

      hudSlot.textContent = `${mod.slot} (${mod.shortTitle})`;
      document.getElementById('drawer-slot-badge').textContent = `${mod.slot} // DOCKED`;
      document.getElementById('drawer-company').textContent = mod.company;
      document.getElementById('drawer-year').textContent = `• ${mod.year}`;
      document.getElementById('drawer-category').textContent = mod.category;
      document.getElementById('drawer-title').textContent = mod.title;
      document.getElementById('drawer-problem').textContent = mod.problem;
      document.getElementById('drawer-solution').textContent = mod.solution;

      document.getElementById('drawer-metrics').innerHTML = mod.metrics.map(m => `
        <div class="bg-black/50 p-3.5 rounded-xl border border-white/10">
          <div class="text-lg md:text-2xl font-bold text-white font-mono">${m.value}</div>
          <div class="text-[10px] font-mono text-slate-400 mt-0.5">${m.label}</div>
        </div>
      `).join('');

      document.getElementById('drawer-stack').innerHTML = mod.stack.map(s => `
        <span class="px-2.5 py-1 rounded-md bg-white/5 border border-white/10 font-mono text-xs text-slate-200">${s}</span>
      `).join('');

      document.getElementById('drawer-diagram').innerHTML = `<pre class="text-[11px] leading-snug text-industrial-cyan">${mod.diagram.join('\n')}</pre>`;
      document.getElementById('drawer-adr').innerHTML = mod.adr.map(item => `<li>${item}</li>`).join('');
    });

    // Subscribe to `isBlueprintMode`
    systemStore.isBlueprintMode.subscribe((isBlueprint) => {
      const xrayDot = document.getElementById('xray-dot');
      const xrayLabel = document.getElementById('xray-label');
      const tabProduct = document.getElementById('tab-product');
      const tabBlueprint = document.getElementById('tab-blueprint');
      const contentProduct = document.getElementById('content-product-view');
      const contentBlueprint = document.getElementById('content-blueprint-view');

      hudMode.textContent = isBlueprint ? 'XRAY_SRS_BLUEPRINT' : 'PHYSICAL_PBR';
      xrayLabel.textContent = isBlueprint ? 'ON' : 'OFF';
      xrayLabel.className = isBlueprint ? 'text-industrial-cyan font-bold' : 'text-slate-300';
      xrayDot.className = isBlueprint ? 'w-2 h-2 rounded-full bg-industrial-cyan animate-ping' : 'w-2 h-2 rounded-full bg-slate-500';

      solidMaterials.forEach((item) => {
        item.mat.wireframe = isBlueprint ? true : item.origWireframe;
        if (isBlueprint) {
          item.mat.color.setHex(0x00f0ff);
        } else if (item.origColor) {
          item.mat.color.copy(item.origColor);
        }
      });

      if (isBlueprint) {
        tabBlueprint.className = 'px-3 py-1.5 rounded bg-industrial-cyan text-black font-bold transition-all flex items-center gap-1.5';
        tabProduct.className = 'px-3 py-1.5 rounded text-slate-300 hover:text-white transition-all';
        contentProduct.classList.add('hidden');
        contentBlueprint.classList.remove('hidden');
      } else {
        tabProduct.className = 'px-3 py-1.5 rounded bg-industrial-orange text-black font-bold transition-all';
        tabBlueprint.className = 'px-3 py-1.5 rounded text-slate-300 hover:text-white transition-all flex items-center gap-1.5';
        contentBlueprint.classList.add('hidden');
        contentProduct.classList.remove('hidden');
      }
    });

    // Subscribe to `activeSkillId`
    systemStore.activeSkillId.subscribe((skillId) => {
      const node = SKILL_NODES.find(n => n.id === skillId);
      if (!node) return;

      document.getElementById('node-detail-title').textContent = `${node.code} // ${node.title}`;
      document.getElementById('node-detail-desc').textContent = node.desc;
      document.getElementById('node-tags-container').innerHTML = node.tags.map(t => `
        <span class="px-2.5 py-1 rounded bg-industrial-cyan/15 border border-industrial-cyan/40 text-industrial-cyan font-mono text-[11px]">${t}</span>
      `).join('');

      skillNodeMeshes.forEach((mesh) => {
        const isSelected = mesh.userData.skillId === skillId;
        mesh.userData.chipMat.emissive.setHex(isSelected ? 0x00f0ff : 0x000000);
        mesh.userData.chipMat.emissiveIntensity = isSelected ? 0.65 : 0;
        gsap.to(mesh.position, {
          y: isSelected ? 0.22 : 0.08,
          duration: 0.25
        });
      });
    });

    /*************************************************************************
     * 9. EVENT LISTENERS FOR HUD CONTROLS
     *************************************************************************/
    document.getElementById('btn-initialize').addEventListener('click', () => {
      sfx.playBootChord();
      const bootOverlay = document.getElementById('boot-overlay');
      bootOverlay.classList.add('opacity-0', 'pointer-events-none');
      setTimeout(() => {
        bootOverlay.style.display = 'none';
      }, 700);
      systemStore.currentView.set('OVERVIEW');
    });

    document.querySelectorAll('.nav-btn').forEach((btn) => {
      btn.addEventListener('click', () => {
        sfx.playClick(760, 0.04);
        systemStore.currentView.set(btn.dataset.nav);
      });
    });

    document.getElementById('btn-goto-chronicle').addEventListener('click', () => {
      sfx.playClick(820, 0.04);
      systemStore.currentView.set('CHRONICLE');
    });

    document.getElementById('btn-goto-uplink').addEventListener('click', () => {
      sfx.playClick(820, 0.04);
      systemStore.currentView.set('UPLINK');
    });

    document.getElementById('btn-eject').addEventListener('click', () => {
      ejectCurrentCartridge();
      systemStore.activeProjectId.set(null);
      systemStore.currentView.set('MODULES');
    });

    document.getElementById('btn-xray-global').addEventListener('click', () => {
      sfx.playClick(980, 0.04);
      systemStore.isBlueprintMode.set(!systemStore.isBlueprintMode.get());
    });
    document.getElementById('tab-product').addEventListener('click', () => {
      sfx.playClick(720, 0.03);
      systemStore.isBlueprintMode.set(false);
    });
    document.getElementById('tab-blueprint').addEventListener('click', () => {
      sfx.playClick(1080, 0.04);
      systemStore.isBlueprintMode.set(true);
    });

    document.getElementById('btn-audio').addEventListener('click', () => {
      const muted = !systemStore.isAudioMuted.get();
      systemStore.isAudioMuted.set(muted);
      document.getElementById('audio-icon').textContent = muted ? '🔇' : '🔊';
      if (!muted) sfx.playClick(880, 0.03);
    });

    document.getElementById('uplink-form').addEventListener('submit', (e) => {
      e.preventDefault();
      sfx.playBootChord();
      const fb = document.getElementById('uplink-feedback');
      fb.classList.remove('hidden');
      e.target.reset();
      setTimeout(() => fb.classList.add('hidden'), 5000);
    });

    // CV Modal Controls
    const cvModal = document.getElementById('cv-modal');
    document.getElementById('btn-cv-modal').addEventListener('click', () => {
      sfx.playClick(920, 0.04);
      cvModal.classList.remove('hidden');
      cvModal.classList.add('flex');
    });
    document.getElementById('btn-close-cv').addEventListener('click', () => {
      cvModal.classList.add('hidden');
      cvModal.classList.remove('flex');
    });

    /*************************************************************************
     * 10. ASTRO BOILERPLATE SOURCE CODE MODAL (Tailored for Nasrun)
     *************************************************************************/
    const ASTRO_FILES = {
      store: `// File: src/stores/systemStore.ts
import { atom } from 'nanostores';

export type SystemState =
  | 'BOOT'
  | 'OVERVIEW'
  | 'MODULES'
  | 'CASE_STUDY'
  | 'CHRONICLE'
  | 'NODES'
  | 'UPLINK';

// State terpusat untuk Website Pribadi Nasrun Hidayattullah
export const currentView = atom<SystemState>('BOOT');
export const activeProjectSlug = atom<string | null>(null);
export const isBlueprintMode = atom<boolean>(false);
export const isAudioMuted = atom<boolean>(false);

export function mountProjectModule(slug: string) {
  activeProjectSlug.set(slug);
  currentView.set('CASE_STUDY');
}

export function ejectProjectModule() {
  activeProjectSlug.set(null);
  currentView.set('MODULES');
}`,

      layout: `---
// File: src/layouts/PersonalCoreLayout.astro
import { ViewTransitions } from 'astro:transitions';
import SystemCoreCanvas from '../components/three/SystemCoreCanvas.astro';
import TopIdentityBar from '../components/hud/TopIdentityBar.astro';
import BottomNavDock from '../components/hud/BottomNavDock.astro';

interface Props {
  title?: string;
}
const { title = 'Nasrun Hidayattullah — System Analyst, QA Tester & Fullstack Developer' } = Astro.props;
---
<!doctype html>
<html lang="id" class="dark">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>{title}</title>
    <ViewTransitions />
  </head>
  <body class="bg-[#0b0d10] text-slate-100 overflow-hidden select-none">
    <!-- Persistent Three.js Island: Tidak di-reload saat pindah halaman -->
    <SystemCoreCanvas transition:persist="nasrun-core-webgl" />

    <!-- HUD Identitas Nasrun Hidayattullah -->
    <TopIdentityBar transition:persist="nasrun-top-hud" />

    <!-- Konten Halaman Dinamis (Bio, Studi Kasus, Chronicle, atau Kontak) -->
    <main class="relative z-10 pointer-events-none">
      <slot />
    </main>

    <BottomNavDock transition:persist="nasrun-bottom-dock" />
  </body>
</html>`,

      canvas: `---
// File: src/components/three/SystemCoreCanvas.astro
---
<div id="webgl-container" class="fixed inset-0 z-0"></div>

<script>
  import * as THREE from 'three';
  import gsap from 'gsap';
  import { currentView, isBlueprintMode } from '../../stores/systemStore';

  const container = document.getElementById('webgl-container')!;
  const scene = new THREE.Scene();
  const camera = new THREE.PerspectiveCamera(42, window.innerWidth / window.innerHeight, 0.1, 100);
  const renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  container.appendChild(renderer.domElement);

  const CAMERA_RIG = {
    OVERVIEW:   { pos: [-0.35, 1.25, 7.5], lookAt: [-0.35, 0, 0] },
    MODULES:    { pos: [-1.15, 0.35, 4.9], lookAt: [-0.95, 0.1, 0.4] },
    CASE_STUDY: { pos: [1.65, 0.2, 4.85],  lookAt: [2.15, 0.05, 0.2] },
    CHRONICLE:  { pos: [1.35, -0.65, 4.7], lookAt: [1.55, -0.95, 0.4] },
    NODES:      { pos: [0.8, 4.6, 3.6],    lookAt: [0.6, 1.8, -0.2] },
    UPLINK:     { pos: [3.1, -0.75, 3.8],  lookAt: [3.35, -1.0, 0.8] },
  };

  currentView.subscribe((view) => {
    const target = CAMERA_RIG[view];
    if (!target) return;
    gsap.to(camera.position, {
      x: target.pos[0],
      y: target.pos[1],
      z: target.pos[2],
      duration: 1.2,
      ease: 'power3.inOut'
    });
  });
</script>`,

      mdx: `---
# File: src/content/projects/01-simrs-indo-techno.mdx
slotCode: "MOD_01"
title: "Multi-Hospital SIMRS & Portal Dokumentasi Internal"
shortTitle: "SIMRS 5 RSUD"
company: "PT Indo Techno Medic"
period: "Juni 2026 - Sekarang"
role: "Fullstack Developer"
accentColor: "#ff5500"
metrics:
  - label: "IMPLEMENTASI RSUD"
    value: "5 RS"
  - label: "PORTAL DOKUMENTASI"
    value: "Laravel 12"
  - label: "CORE DATABASE"
    value: "PostgreSQL"
techStack:
  - "CodeIgniter 3"
  - "Laravel 12"
  - "PostgreSQL"
  - "SIMRS Workflow"
blueprint:
  topologyDiagram:
    - "[5 Rumah Sakit: RSUD Caruban, Cilacap, Astrini, Blora, Slawi]"
    - "   ├──> [SIMRS Core (CodeIgniter 3 + PostgreSQL)]"
    - "   └──> [Portal Dokumentasi Panduan SIMRS (Laravel 12 + PostgreSQL)]"
  artifactsAndQA:
    - "Kustomisasi modul layanan medis & pelaporan SIMRS sesuai kebutuhan spesifik 5 RS."
    - "Pengembangan portal dokumentasi internal & eksternal berbasis Laravel 12."
---

## Konteks Proyek
Pengembangan berkelanjutan dan kustomisasi Sistem Informasi Manajemen Rumah Sakit (SIMRS) pada 5 rumah sakit mitra PT Indo Techno Medic serta pembangunan sistem informasi dokumentasi panduan penggunaan SIMRS.`
    };

    const astroModal = document.getElementById('astro-modal');
    const astroCodeContent = document.getElementById('astro-code-content');
    let currentCodeTab = 'store';

    function renderAstroCode(tabKey) {
      currentCodeTab = tabKey;
      astroCodeContent.textContent = ASTRO_FILES[tabKey];
      document.querySelectorAll('.code-tab-btn').forEach((btn) => {
        if (btn.dataset.codeTab === tabKey) {
          btn.className = 'code-tab-btn px-4 py-2 rounded-t-lg bg-industrial-cyan/20 text-industrial-cyan border-b-2 border-industrial-cyan font-bold';
        } else {
          btn.className = 'code-tab-btn px-4 py-2 rounded-t-lg text-slate-400 hover:text-white';
        }
      });
    }

    document.getElementById('btn-astro-code').addEventListener('click', () => {
      sfx.playClick(940, 0.04);
      renderAstroCode(currentCodeTab);
      astroModal.classList.remove('hidden');
      astroModal.classList.add('flex');
    });

    document.getElementById('btn-close-modal').addEventListener('click', () => {
      astroModal.classList.add('hidden');
      astroModal.classList.remove('flex');
    });

    document.querySelectorAll('.code-tab-btn').forEach((btn) => {
      btn.addEventListener('click', () => {
        sfx.playClick(800, 0.03);
        renderAstroCode(btn.dataset.codeTab);
      });
    });

    document.getElementById('btn-copy-code').addEventListener('click', (e) => {
      navigator.clipboard.writeText(ASTRO_FILES[currentCodeTab]);
      const btn = e.currentTarget;
      btn.textContent = '✓ COPIED!';
      setTimeout(() => { btn.textContent = 'COPY FILE'; }, 1800);
    });

    window.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        if (!astroModal.classList.contains('hidden')) {
          astroModal.classList.add('hidden');
          astroModal.classList.remove('flex');
        } else if (!cvModal.classList.contains('hidden')) {
          cvModal.classList.add('hidden');
          cvModal.classList.remove('flex');
        } else if (systemStore.currentView.get() === 'CASE_STUDY') {
          document.getElementById('btn-eject').click();
        }
      }
    });

    /*************************************************************************
     * 11. MAIN RENDER LOOP
     *************************************************************************/
    const clock = new THREE.Clock();

    function animate() {
      requestAnimationFrame(animate);
      const delta = clock.getDelta();
      const elapsed = clock.getElapsedTime();

      coolingFans.forEach((fan, idx) => {
        fan.rotation.y += delta * (idx === 0 ? 4.5 : -5.2);
      });

      coreEnergyRing.rotation.z = elapsed * 0.6;
      const pulseScale = 1 + Math.sin(elapsed * 3.5) * 0.025;
      coreEnergyRing.scale.set(pulseScale, pulseScale, 1);

      opticalShaders.forEach((shader) => {
        shader.uniforms.uTime.value = elapsed;
      });

      machineRoot.rotation.y += (parallaxOffset.x * 0.35 - machineRoot.rotation.y) * 0.05;
      machineRoot.rotation.x += (-parallaxOffset.y * 0.2 - machineRoot.rotation.x) * 0.05;

      camera.lookAt(camLookTarget);
      renderer.render(scene, camera);
    }

    animate();

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
      moveCameraToState(systemStore.currentView.get(), 0.4);
    });
  </script>
</body>
</html>

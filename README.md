<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Lucas Bezerra — Dev</title>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet" />
  <style>
    :root {
      --bg:        #080c10;
      --surface:   #0e1318;
      --border:    #1a2535;
      --cyan:      #00d4ff;
      --cyan-dim:  #00d4ff33;
      --green:     #00ff88;
      --green-dim: #00ff8820;
      --amber:     #ffb300;
      --muted:     #4a6070;
      --text:      #cdd8e3;
      --text-dim:  #7a94a8;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: 'JetBrains Mono', monospace;
      font-size: 14px;
      line-height: 1.7;
      min-height: 100vh;
      padding: 48px 24px;
      overflow-x: hidden;
    }

    /* grid de pontos no fundo */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image: radial-gradient(circle, #1a2535 1px, transparent 1px);
      background-size: 32px 32px;
      opacity: .4;
      pointer-events: none;
      z-index: 0;
    }

    .wrap {
      position: relative;
      z-index: 1;
      max-width: 760px;
      margin: 0 auto;
    }

    /* ── HEADER ── */
    .header {
      margin-bottom: 48px;
      animation: fadeDown .6s ease both;
    }

    .prompt {
      color: var(--muted);
      font-size: 12px;
      letter-spacing: .08em;
      margin-bottom: 6px;
    }

    .prompt span { color: var(--cyan); }

    h1 {
      font-family: 'Syne', sans-serif;
      font-size: clamp(2rem, 6vw, 3.4rem);
      font-weight: 800;
      letter-spacing: -.02em;
      line-height: 1.1;
      color: #fff;
    }

    h1 em {
      font-style: normal;
      color: var(--cyan);
    }

    .tagline {
      margin-top: 12px;
      color: var(--text-dim);
      font-size: 13px;
    }

    .tagline::before { content: '// '; color: var(--muted); }

    /* ── STATUS BADGE ── */
    .status-row {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin: 24px 0 0;
      animation: fadeDown .6s .1s ease both;
    }

    .badge {
      display: inline-flex;
      align-items: center;
      gap: 7px;
      padding: 5px 14px;
      border-radius: 2px;
      font-size: 11px;
      font-weight: 600;
      letter-spacing: .08em;
      text-transform: uppercase;
      border: 1px solid;
    }

    .badge-green {
      color: var(--green);
      border-color: var(--green);
      background: var(--green-dim);
    }

    .badge-cyan {
      color: var(--cyan);
      border-color: var(--cyan);
      background: var(--cyan-dim);
    }

    .badge-amber {
      color: var(--amber);
      border-color: var(--amber);
      background: #ffb30018;
    }

    .dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: currentColor;
      animation: pulse 1.6s ease-in-out infinite;
    }

    /* ── SECTION LABEL ── */
    .section {
      margin-top: 48px;
      animation: fadeUp .5s ease both;
    }

    .section-label {
      font-size: 10px;
      letter-spacing: .18em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 16px;
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .section-label::after {
      content: '';
      flex: 1;
      height: 1px;
      background: var(--border);
    }

    /* ── CODE BLOCK (about) ── */
    .code-block {
      background: var(--surface);
      border: 1px solid var(--border);
      border-left: 3px solid var(--cyan);
      padding: 20px 24px;
      border-radius: 0 4px 4px 0;
      font-size: 13px;
      line-height: 1.9;
    }

    .code-block .k  { color: #7ec8e3; }   /* keyword  */
    .code-block .s  { color: #a8d8a8; }   /* string   */
    .code-block .p  { color: var(--muted); } /* punct  */
    .code-block .c  { color: var(--muted); font-style: italic; } /* comment */
    .code-block .v  { color: var(--cyan); } /* var name */
    .code-block .n  { color: var(--amber); } /* number / bool */

    /* ── TECH GRID ── */
    .tech-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
      gap: 8px;
    }

    .tech-item {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 10px 14px;
      font-size: 12px;
      display: flex;
      align-items: center;
      gap: 8px;
      transition: border-color .2s, background .2s;
      cursor: default;
    }

    .tech-item:hover {
      border-color: var(--cyan);
      background: var(--cyan-dim);
    }

    .tech-item .icon { font-size: 15px; }

    /* ── PROJECT LIST ── */
    .project-list { display: flex; flex-direction: column; gap: 10px; }

    .project {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 16px 20px;
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 4px 16px;
      align-items: start;
      transition: border-color .2s;
    }

    .project:hover { border-color: var(--cyan); }

    .project-name {
      font-weight: 600;
      color: #fff;
      font-size: 13px;
    }

    .project-name span { color: var(--cyan); margin-right: 6px; }

    .project-desc {
      color: var(--text-dim);
      font-size: 12px;
      grid-column: 1;
    }

    .project-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 5px;
      grid-column: 1 / -1;
      margin-top: 8px;
    }

    .tag {
      font-size: 10px;
      padding: 2px 8px;
      border: 1px solid var(--border);
      color: var(--muted);
      letter-spacing: .06em;
    }

    /* ── CONTACT ── */
    .contact-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 8px;
    }

    .contact-item {
      background: var(--surface);
      border: 1px solid var(--border);
      padding: 12px 16px;
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 12px;
      text-decoration: none;
      color: var(--text-dim);
      transition: color .2s, border-color .2s;
    }

    .contact-item:hover { color: var(--cyan); border-color: var(--cyan); }

    .contact-item .ci { color: var(--cyan); font-size: 14px; }

    /* ── FOOTER ── */
    .footer {
      margin-top: 56px;
      padding-top: 24px;
      border-top: 1px solid var(--border);
      color: var(--muted);
      font-size: 11px;
      display: flex;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 8px;
    }

    .footer span { color: var(--cyan); }

    /* ── ANIMATIONS ── */
    @keyframes fadeDown {
      from { opacity: 0; transform: translateY(-12px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(12px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50%       { opacity: .3; }
    }

    .section:nth-child(2)  { animation-delay: .15s; }
    .section:nth-child(3)  { animation-delay: .25s; }
    .section:nth-child(4)  { animation-delay: .35s; }
    .section:nth-child(5)  { animation-delay: .45s; }
  </style>
</head>
<body>
<div class="wrap">

  <!-- HEADER -->
  <header class="header">
    <p class="prompt"><span>~/dev</span> $ whoami</p>
    <h1>J. Lucas <em>Bezerra</em></h1>
    <p class="tagline">Desenvolvedor Full Stack · Construtor de Micro SaaS · Brasil</p>

    <div class="status-row">
      <span class="badge badge-green"><span class="dot"></span>Atuando em projetos</span>
      <span class="badge badge-cyan"><span class="dot"></span>Disponível para estágio</span>
      <span class="badge badge-amber">📍 Brasil</span>
    </div>
  </header>

  <!-- SOBRE -->
  <section class="section">
    <p class="section-label">sobre</p>
    <div class="code-block">
<span class="k">const</span> <span class="v">lucas</span> <span class="p">=</span> <span class="p">{</span><br>
&nbsp;&nbsp;<span class="v">stack</span><span class="p">:</span>      <span class="s">"Full Stack Web"</span><span class="p">,</span><br>
&nbsp;&nbsp;<span class="v">foco</span><span class="p">:</span>       <span class="s">"Micro SaaS &amp; produtos digitais"</span><span class="p">,</span><br>
&nbsp;&nbsp;<span class="v">estudando</span><span class="p">:</span> <span class="s">"TypeScript avançado + arquitetura"</span><span class="p">,</span><br>
&nbsp;&nbsp;<span class="v">aberto</span><span class="p">:</span>    <span class="p">[</span><span class="s">"estágio"</span><span class="p">,</span> <span class="s">"freela"</span><span class="p">,</span> <span class="s">"projetos"</span><span class="p">],</span><br>
&nbsp;&nbsp;<span class="v">princípio</span><span class="p">:</span> <span class="s">"Código simples. Produto que funciona."</span><br>
<span class="p">};</span>
    </div>
  </section>

  <!-- TECNOLOGIAS -->
  <section class="section">
    <p class="section-label">tecnologias</p>
    <div class="tech-grid">
      <div class="tech-item"><span class="icon">🌐</span> HTML5</div>
      <div class="tech-item"><span class="icon">🎨</span> CSS3</div>
      <div class="tech-item"><span class="icon">⚡</span> JavaScript</div>
      <div class="tech-item"><span class="icon">🔷</span> TypeScript</div>
      <div class="tech-item"><span class="icon">🐘</span> PHP</div>
      <div class="tech-item"><span class="icon">🗄️</span> MySQL</div>
      <div class="tech-item"><span class="icon">🅱️</span> Bootstrap 5</div>
      <div class="tech-item"><span class="icon">▲</span> Next.js</div>
      <div class="tech-item"><span class="icon">🐍</span> Python</div>
      <div class="tech-item"><span class="icon">🟢</span> Node.js</div>
      <div class="tech-item"><span class="icon">📱</span> Ionic</div>
    </div>
  </section>

  <!-- PROJETOS -->
  <section class="section">
    <p class="section-label">projetos</p>
    <div class="project-list">

      <div class="project">
        <div class="project-name"><span>▸</span> Menu Digital QR</div>
        <div class="project-desc">Cardápio digital com QR Code para pequenos negócios — PHP MVC do zero.</div>
        <div class="project-tags">
          <span class="tag">PHP</span><span class="tag">MySQL</span><span class="tag">Bootstrap 5</span><span class="tag">MVC</span>
        </div>
      </div>

      <div class="project">
        <div class="project-name"><span>▸</span> RedaTech</div>
        <div class="project-desc">Plataforma de correção de redações ENEM com IA e arquitetura enterprise.</div>
        <div class="project-tags">
          <span class="tag">Node.js</span><span class="tag">MySQL</span><span class="tag">JWT</span><span class="tag">Winston</span>
        </div>
      </div>

      <div class="project">
        <div class="project-name"><span>▸</span> Fred — Assistente IA</div>
        <div class="project-desc">Assistente pessoal com leitura de tela e integração com Claude API.</div>
        <div class="project-tags">
          <span class="tag">Python</span><span class="tag">Claude API</span><span class="tag">OCR</span>
        </div>
      </div>

      <div class="project">
        <div class="project-name"><span>▸</span> Schema Visualizer</div>
        <div class="project-desc">Visualizador de esquemas MySQL com auth JWT e interface limpa.</div>
        <div class="project-tags">
          <span class="tag">Node.js</span><span class="tag">Express</span><span class="tag">JWT</span><span class="tag">MySQL</span>
        </div>
      </div>

    </div>
  </section>

  <!-- CONTATO -->
  <section class="section">
    <p class="section-label">contato</p>
    <div class="contact-grid">
      <a class="contact-item" href="mailto:seuemail@gmail.com">
        <span class="ci">✉</span> seuemail@gmail.com
      </a>
      <a class="contact-item" href="https://linkedin.com/in/SEU_USUARIO" target="_blank">
        <span class="ci">in</span> linkedin.com/in/seuperfil
      </a>
      <a class="contact-item" href="https://seusite.com" target="_blank">
        <span class="ci">◈</span> seusite.com
      </a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <span>J. Lucas Bezerra &mdash; Full Stack Dev</span>
    <span>feito com <span>♥</span> &amp; muito <span>café</span></span>
  </footer>

</div>
</body>
</html>

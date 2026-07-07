<!DOCTYPE html>
<html lang="zh" data-theme="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>yb-slide — Nothing 风格 HTML 幻灯片 Skill</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --ease: cubic-bezier(0.16, 1, 0.3, 1);
  }
  [data-theme="dark"] {
    --bg: #0d0d0d;
    --dot: rgba(255,255,255,0.07);
    --fg: #ffffff;
    --fg-dim: rgba(255,255,255,0.55);
    --fg-faint: rgba(255,255,255,0.28);
    --line: rgba(255,255,255,0.08);
    --surface: #1c1c1c;
    --accent: #d71921;
  }
  [data-theme="light"] {
    --bg: #f5f4f0;
    --dot: rgba(20,20,16,0.10);
    --fg: #0d0d0d;
    --fg-dim: rgba(13,13,13,0.58);
    --fg-faint: rgba(13,13,13,0.30);
    --line: rgba(13,13,13,0.10);
    --surface: #ffffff;
    --accent: #d71921;
  }
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    background-color: var(--bg);
    background-image: radial-gradient(circle, var(--dot) 1px, transparent 1px);
    background-size: 20px 20px;
    color: var(--fg);
    font-family: 'Inter', system-ui, sans-serif;
    -webkit-font-smoothing: antialiased;
    transition: background-color 400ms, color 400ms;
  }

  /* ---- layout ---- */
  .page { max-width: 840px; margin: 0 auto; padding: 0 32px 120px; }

  /* ---- header ---- */
  .site-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 40px 0 80px;
    border-bottom: 1px solid var(--line);
    margin-bottom: 80px;
  }
  .logo {
    font-family: 'Courier New', monospace;
    font-size: 20px;
    letter-spacing: 0.04em;
    color: var(--fg);
  }
  .logo .tick { color: var(--accent); }
  .badge {
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 0.14em;
    text-transform: uppercase;
    color: var(--fg-faint);
    border: 1px solid var(--line);
    padding: 4px 10px;
  }

  /* ---- hero ---- */
  .hero { margin-bottom: 80px; }
  .hero .label {
    font-size: 11px;
    font-weight: 500;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .hero .label::before { content: ""; display: block; width: 24px; height: 1px; background: var(--accent); }
  .hero h1 {
    font-size: clamp(40px, 6vw, 80px);
    font-weight: 300;
    line-height: 1.05;
    letter-spacing: -0.02em;
    margin-bottom: 28px;
  }
  .hero h1 em { font-style: italic; color: var(--accent); }
  .hero p {
    font-size: 16px;
    line-height: 1.75;
    color: var(--fg-dim);
    max-width: 560px;
  }

  /* ---- install block ---- */
  .install-block {
    background: var(--surface);
    border: 1px solid var(--line);
    padding: 24px 28px;
    margin: 40px 0 80px;
    display: flex;
    align-items: center;
    gap: 20px;
  }
  .install-block .cmd {
    font-family: 'Courier New', monospace;
    font-size: 13px;
    color: var(--fg);
    flex: 1;
  }
  .install-block .cmd span { color: var(--accent); }
  .copy-btn {
    font-family: 'Inter', sans-serif;
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--fg-dim);
    background: transparent;
    border: 1px solid var(--line);
    padding: 6px 12px;
    cursor: pointer;
    transition: color 200ms, border-color 200ms;
    flex-shrink: 0;
  }
  .copy-btn:hover { color: var(--fg); border-color: var(--fg-dim); }
  .copy-btn.copied { color: var(--accent); border-color: var(--accent); }

  /* ---- section ---- */
  .section { margin-bottom: 72px; }
  .section-label {
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: var(--fg-faint);
    margin-bottom: 32px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--line);
  }

  /* ---- slide types grid ---- */
  .type-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
    margin-bottom: 8px;
  }
  .type-card {
    background: var(--bg);
    padding: 20px 20px 24px;
    transition: background 200ms;
  }
  .type-card:hover { background: var(--surface); }
  .type-name {
    font-family: 'Courier New', monospace;
    font-size: 11px;
    letter-spacing: 0.08em;
    color: var(--accent);
    margin-bottom: 8px;
  }
  .type-title {
    font-size: 14px;
    font-weight: 500;
    color: var(--fg);
    margin-bottom: 4px;
  }
  .type-desc {
    font-size: 12px;
    line-height: 1.6;
    color: var(--fg-dim);
  }

  /* ---- how it works ---- */
  .step-list { display: flex; flex-direction: column; gap: 0; }
  .step {
    display: grid;
    grid-template-columns: 40px 1fr;
    gap: 20px;
    padding: 24px 0;
    border-bottom: 1px solid var(--line);
    align-items: start;
  }
  .step:first-child { border-top: 1px solid var(--line); }
  .step-num {
    font-family: 'Courier New', monospace;
    font-size: 11px;
    color: var(--accent);
    padding-top: 2px;
  }
  .step-body h3 { font-size: 14px; font-weight: 500; margin-bottom: 4px; }
  .step-body p { font-size: 13px; line-height: 1.65; color: var(--fg-dim); }
  code {
    font-family: 'Courier New', monospace;
    font-size: 12px;
    background: var(--surface);
    padding: 1px 5px;
    border: 1px solid var(--line);
    color: var(--fg-dim);
  }

  /* ---- design tokens ---- */
  .token-row {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 1px;
    background: var(--line);
    border: 1px solid var(--line);
    margin-bottom: 1px;
  }
  .token-row:last-child { margin-bottom: 0; }
  .token-cell {
    background: var(--bg);
    padding: 12px 16px;
    font-size: 12px;
    color: var(--fg-dim);
    transition: background 200ms;
  }
  .token-cell:hover { background: var(--surface); }
  .token-cell .key { font-family: 'Courier New', monospace; color: var(--fg-faint); font-size: 10px; margin-bottom: 3px; }
  .token-cell .val { color: var(--fg); font-size: 13px; }
  .token-cell .swatch {
    display: inline-block;
    width: 8px; height: 8px;
    border-radius: 50%;
    margin-right: 6px;
    vertical-align: middle;
    flex-shrink: 0;
  }

  /* ---- footer ---- */
  .site-footer {
    border-top: 1px solid var(--line);
    padding-top: 32px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 11px;
    color: var(--fg-faint);
    letter-spacing: 0.08em;
  }
  .site-footer a { color: var(--fg-faint); text-decoration: none; border-bottom: 1px solid var(--line); }
  .site-footer a:hover { color: var(--fg-dim); }

  /* ---- theme toggle ---- */
  .theme-btn {
    position: fixed;
    top: 32px; right: 32px;
    width: 36px; height: 36px;
    border-radius: 50%;
    border: 1px solid var(--line);
    background: transparent;
    color: var(--fg-dim);
    cursor: pointer;
    display: grid;
    place-items: center;
    transition: border-color 200ms, transform 300ms var(--ease);
    z-index: 100;
  }
  .theme-btn:hover { border-color: var(--fg-dim); transform: scale(1.08); }
  .theme-btn svg { width: 14px; height: 14px; stroke: currentColor; fill: none; stroke-width: 1.5; }
  [data-theme="dark"]  .icon-sun  { display: block; }
  [data-theme="dark"]  .icon-moon { display: none;  }
  [data-theme="light"] .icon-sun  { display: none;  }
  [data-theme="light"] .icon-moon { display: block; }
</style>
</head>
<body>

<button class="theme-btn" id="themeBtn" aria-label="Toggle theme">
  <svg class="icon-sun"  viewBox="0 0 24 24"><circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M4.9 4.9l1.4 1.4M17.7 17.7l1.4 1.4M2 12h2M20 12h2M4.9 19.1l1.4-1.4M17.7 6.3l1.4-1.4"/></svg>
  <svg class="icon-moon" viewBox="0 0 24 24"><path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8z"/></svg>
</button>

<div class="page">

  <header class="site-header">
    <div class="logo">YB<span class="tick">'</span> Library</div>
    <div class="badge">Claude Code Skill</div>
  </header>

  <section class="hero">
    <div class="label">yb-slide</div>
    <h1>Nothing 风格<br><em>幻灯片</em>生成器</h1>
    <p>把你的 PPT 梗概交给 Claude Code，自动生成一个 Nothing Playground 风格的 HTML 演示文稿——单文件交付，无需构建工具，开箱即用。13 种内置 slide 布局，PicNic 点阵 Logo，PPEditorialNew 字体，红色 Accent，深色/浅色双模式。</p>
  </section>

  <div class="install-block">
    <div class="cmd"><span>git clone</span> https://github.com/yuebinzhang77-hub/yb-slide-skill.git ~/.claude/skills/yb-slide</div>
    <button class="copy-btn" id="copyBtn">COPY</button>
  </div>

  <section class="section">
    <div class="section-label">使用方式</div>
    <div class="step-list">
      <div class="step">
        <div class="step-num">01</div>
        <div class="step-body">
          <h3>安装 Skill</h3>
          <p>把仓库克隆到 <code>~/.claude/skills/yb-slide</code>，Claude Code 会自动识别。</p>
        </div>
      </div>
      <div class="step">
        <div class="step-num">02</div>
        <div class="step-body">
          <h3>触发生成</h3>
          <p>在任意 Claude Code 会话中说 <code>/yb-slide</code>，或"帮我做幻灯片"，然后把你的大纲/梗概发给它。支持中英文混排。</p>
        </div>
      </div>
      <div class="step">
        <div class="step-num">03</div>
        <div class="step-body">
          <h3>获取文件</h3>
          <p>Claude 会输出 <code>~/Desktop/yb-slide-[主题].html</code>，双击即可在浏览器中播放。字体从 <code>~/yb-library/public/fonts/</code> 相对路径加载。</p>
        </div>
      </div>
      <div class="step">
        <div class="step-num">04</div>
        <div class="step-body">
          <h3>键盘导航</h3>
          <p>←→ 或 ↑↓ 切换页面，Space 前进，右侧导航条 hover 显示页面预览。</p>
        </div>
      </div>
    </div>
  </section>

  <section class="section">
    <div class="section-label">13 种 Slide 布局</div>
    <div class="type-grid">
      <div class="type-card">
        <div class="type-name">.s-cover</div>
        <div class="type-title">Cover 封面</div>
        <div class="type-desc">超大显示字体 + 副标题。固定第一页。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-chapter</div>
        <div class="type-title">Chapter 章节</div>
        <div class="type-desc">全白背景切割，用于长 deck 的段落分隔。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-statement</div>
        <div class="type-title">Statement 引言</div>
        <div class="type-desc">单一大字 quote 或核心观点，带 mark 高亮词。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-bullet</div>
        <div class="type-title">Bullet 要点</div>
        <div class="type-desc">3–5 条列表，逐条 stagger 入场，红色 — 标记。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-grid</div>
        <div class="type-title">Grid 要点网格</div>
        <div class="type-desc">2–4 列并排卡片，支持 cols-2 / cols-3 / cols-4。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-split</div>
        <div class="type-title">Split 分栏</div>
        <div class="type-desc">左侧大数字 / 视觉 + 右侧文字说明。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-comparison</div>
        <div class="type-title">Comparison 对比</div>
        <div class="type-desc">A vs B，两列竖线分隔，适合方案/前后对比。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-timeline</div>
        <div class="type-title">Timeline 时间线</div>
        <div class="type-desc">横向里程碑，红色节点标记，时间戳 mono 字体。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-stats</div>
        <div class="type-title">Stats 数据大字</div>
        <div class="type-desc">1–3 组巨型数字 + 说明标签 + 来源注释。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-table</div>
        <div class="type-title">Table 表格</div>
        <div class="type-desc">功能对比矩阵，hairline 分隔，accent 高亮列。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-fullbleed</div>
        <div class="type-title">Fullbleed 全屏</div>
        <div class="type-desc">图片填满幻灯片，底部渐变 scrim + 文字叠加。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-specimen</div>
        <div class="type-title">Specimen 字体</div>
        <div class="type-desc">字体展示行，适合设计或品牌类演讲。</div>
      </div>
      <div class="type-card">
        <div class="type-name">.s-closing</div>
        <div class="type-title">Closing 收尾</div>
        <div class="type-desc">Sign-off + 联系方式。固定最后一页。</div>
      </div>
    </div>
  </section>

  <section class="section">
    <div class="section-label">设计 Tokens</div>

    <div class="token-row">
      <div class="token-cell"><div class="key">--accent</div><div class="val"><span class="swatch" style="background:#d71921"></span>#d71921</div></div>
      <div class="token-cell"><div class="key">--bg (dark)</div><div class="val"><span class="swatch" style="background:#0d0d0d;border:1px solid rgba(255,255,255,.2)"></span>#0d0d0d</div></div>
      <div class="token-cell"><div class="key">--bg (light)</div><div class="val"><span class="swatch" style="background:#f5f4f0;border:1px solid rgba(0,0,0,.1)"></span>#f5f4f0</div></div>
    </div>
    <div class="token-row">
      <div class="token-cell"><div class="key">Logo font</div><div class="val">PicNic · dot-matrix</div></div>
      <div class="token-cell"><div class="key">Display / Heading</div><div class="val">PPEditorialNew · 200 / 400 / 700</div></div>
      <div class="token-cell"><div class="key">Body / Kicker</div><div class="val">Inter · 400 / 500</div></div>
    </div>
    <div class="token-row">
      <div class="token-cell"><div class="key">Dot-matrix</div><div class="val">radial-gradient 1px · 20px grid</div></div>
      <div class="token-cell"><div class="key">Transition</div><div class="val">cubic-bezier(0.16, 1, 0.3, 1)</div></div>
      <div class="token-cell"><div class="key">Duration</div><div class="val">650ms · stagger 60–380ms</div></div>
    </div>
  </section>

  <footer class="site-footer">
    <span>YB' Library · <a href="https://github.com/yuebinzhang77-hub/yb-slide-skill">GitHub</a></span>
    <span>Claude Code Skill · 2026</span>
  </footer>

</div>

<script>
  document.getElementById('themeBtn').addEventListener('click', () => {
    const root = document.documentElement;
    root.dataset.theme = root.dataset.theme === 'dark' ? 'light' : 'dark';
  });

  const copyBtn = document.getElementById('copyBtn');
  copyBtn.addEventListener('click', () => {
    navigator.clipboard.writeText('git clone https://github.com/yuebinzhang77-hub/yb-slide-skill.git ~/.claude/skills/yb-slide').then(() => {
      copyBtn.textContent = 'COPIED';
      copyBtn.classList.add('copied');
      setTimeout(() => { copyBtn.textContent = 'COPY'; copyBtn.classList.remove('copied'); }, 2000);
    });
  });
</script>
</body>
</html>

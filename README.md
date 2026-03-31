<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>AeroAgent v2 — Code Documentation</title>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:ital,wght@0,400;0,600;1,400&family=IBM+Plex+Sans:wght@400;500;600&family=IBM+Plex+Serif:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #ffffff;
  --surface: #f8f8f6;
  --border: #e4e2dd;
  --border-strong: #c8c4bc;
  --ink: #1a1916;
  --ink-2: #4a4740;
  --ink-3: #8a8680;
  --accent: #c9410a;
  --accent-soft: #fdf1ec;
  --blue: #1a4fff;
  --blue-soft: #eef2ff;
  --green: #1a7a3c;
  --green-soft: #edfaf3;
  --purple: #6b2fb3;
  --purple-soft: #f4eeff;
  --yellow: #8a6400;
  --yellow-soft: #fefae8;
  --mono: 'IBM Plex Mono', monospace;
  --sans: 'IBM Plex Sans', sans-serif;
  --serif: 'IBM Plex Serif', serif;
  --sidebar-w: 240px;
}
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }
body { background: var(--bg); color: var(--ink); font-family: var(--sans); font-size: 14px; line-height: 1.6; }

.layout { display: grid; grid-template-columns: var(--sidebar-w) 1fr; min-height: 100vh; }

.sidebar { position: sticky; top: 0; height: 100vh; overflow-y: auto; border-right: 1px solid var(--border); background: var(--surface); font-family: var(--mono); }
.sidebar::-webkit-scrollbar { width: 3px; }
.sidebar::-webkit-scrollbar-thumb { background: var(--border-strong); }
.sb-header { padding: 20px 20px 16px; border-bottom: 1px solid var(--border); }
.sb-project { font-size: 0.62rem; letter-spacing: 0.15em; color: var(--ink-3); text-transform: uppercase; margin-bottom: 4px; }
.sb-title { font-size: 0.85rem; font-weight: 600; color: var(--ink); }
.sb-version { font-size: 0.58rem; color: var(--ink-3); margin-top: 2px; }
.sb-group { border-bottom: 1px solid var(--border); }
.sb-group-label { padding: 12px 20px 6px; font-size: 0.55rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--ink-3); }
.sb-link { display: flex; align-items: center; gap: 8px; padding: 5px 20px; text-decoration: none; font-size: 0.7rem; color: var(--ink-2); transition: background 0.1s, color 0.1s; line-height: 1.3; }
.sb-link:hover { background: var(--border); color: var(--ink); }
.sb-link .ln { font-size: 0.55rem; color: var(--ink-3); min-width: 36px; flex-shrink: 0; }
.sb-link:last-child { padding-bottom: 12px; }

.main { min-width: 0; }

.doc-header { padding: 48px 64px 40px; border-bottom: 2px solid var(--ink); background: var(--ink); color: white; }
.dh-breadcrumb { font-family: var(--mono); font-size: 0.62rem; letter-spacing: 0.12em; color: rgba(255,255,255,0.4); text-transform: uppercase; margin-bottom: 16px; }
.dh-breadcrumb span { color: rgba(255,255,255,0.7); }
.doc-header h1 { font-family: var(--mono); font-size: 1.9rem; font-weight: 600; letter-spacing: -0.02em; margin-bottom: 8px; color: white; }
.doc-header h1 em { color: #ff8c66; font-style: normal; }
.dh-sub { font-size: 0.88rem; color: rgba(255,255,255,0.6); max-width: 600px; line-height: 1.7; font-family: var(--sans); }
.dh-meta { margin-top: 24px; display: flex; gap: 24px; flex-wrap: wrap; }
.dh-badge { font-family: var(--mono); font-size: 0.6rem; letter-spacing: 0.1em; color: rgba(255,255,255,0.5); padding: 4px 10px; border: 1px solid rgba(255,255,255,0.15); border-radius: 2px; }
.dh-badge strong { color: rgba(255,255,255,0.85); }

.content { padding: 0 64px; max-width: 900px; }

.doc-section { padding: 56px 0 48px; border-bottom: 1px solid var(--border); }
.doc-section:last-child { border-bottom: none; }
.section-anchor { display: flex; align-items: baseline; gap: 12px; margin-bottom: 6px; }
.section-num { font-family: var(--mono); font-size: 0.6rem; color: var(--ink-3); letter-spacing: 0.1em; flex-shrink: 0; }
.section-tag { font-family: var(--mono); font-size: 0.58rem; letter-spacing: 0.15em; text-transform: uppercase; padding: 2px 8px; border-radius: 2px; }
.tag-html { background: var(--yellow-soft); color: var(--yellow); }
.tag-css  { background: var(--blue-soft); color: var(--blue); }
.tag-js   { background: var(--green-soft); color: var(--green); }
.tag-data { background: var(--purple-soft); color: var(--purple); }
.tag-api  { background: var(--accent-soft); color: var(--accent); }
.doc-section h2 { font-family: var(--serif); font-size: 1.45rem; font-weight: 600; letter-spacing: -0.02em; line-height: 1.25; margin-bottom: 16px; color: var(--ink); }
.doc-section p { font-size: 0.88rem; line-height: 1.8; color: var(--ink-2); margin-bottom: 14px; max-width: 680px; }
.doc-section p:last-child { margin-bottom: 0; }

.subsection { margin-top: 32px; padding-top: 28px; border-top: 1px dashed var(--border); }
.subsection h3 { font-family: var(--mono); font-size: 0.8rem; font-weight: 600; color: var(--ink); margin-bottom: 10px; }

.code-wrap { margin: 16px 0; border: 1px solid var(--border); border-radius: 4px; overflow: hidden; }
.code-label { display: flex; justify-content: space-between; align-items: center; padding: 7px 14px; background: #1e1e1e; border-bottom: 1px solid #333; font-family: var(--mono); font-size: 0.58rem; letter-spacing: 0.1em; color: #888; }
.code-label .file { color: #ccc; }
.code-label .lang { color: #666; }
pre.code { background: #1e1e1e; padding: 18px 20px; overflow-x: auto; font-family: var(--mono); font-size: 0.74rem; line-height: 1.9; color: #abb2bf; white-space: pre; margin: 0; }
pre.code .k  { color: #c678dd; }
pre.code .s  { color: #98c379; }
pre.code .n  { color: #e5c07b; }
pre.code .f  { color: #61afef; }
pre.code .c  { color: #5c6370; font-style: italic; }
pre.code .p  { color: #abb2bf; }
pre.code .t  { color: #e06c75; }
pre.code .a  { color: #d19a66; }
pre.code .v  { color: #56b6c2; }

code { font-family: var(--mono); font-size: 0.8em; background: var(--surface); border: 1px solid var(--border); padding: 1px 5px; border-radius: 3px; color: var(--accent); }

.prop-table { width: 100%; border-collapse: collapse; margin: 16px 0; font-size: 0.8rem; }
.prop-table th { text-align: left; padding: 7px 12px; background: var(--surface); border: 1px solid var(--border); font-family: var(--mono); font-size: 0.58rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--ink-3); font-weight: 400; }
.prop-table td { padding: 8px 12px; border: 1px solid var(--border); vertical-align: top; color: var(--ink-2); line-height: 1.5; }
.prop-table td:first-child { font-family: var(--mono); font-size: 0.72rem; color: var(--blue); white-space: nowrap; }
.prop-table tr:hover td { background: var(--surface); }

.callout { display: flex; gap: 12px; padding: 14px 16px; border-radius: 4px; margin: 16px 0; font-size: 0.82rem; line-height: 1.7; max-width: 680px; }
.callout .icon { flex-shrink: 0; font-size: 0.9rem; margin-top: 1px; }
.callout.note  { background: var(--blue-soft); border-left: 3px solid var(--blue); color: #1a2a60; }
.callout.warn  { background: var(--yellow-soft); border-left: 3px solid var(--yellow); color: #4a3500; }
.callout.tip   { background: var(--green-soft); border-left: 3px solid var(--green); color: #0d3d1f; }
.callout.info  { background: var(--accent-soft); border-left: 3px solid var(--accent); color: #5a1a00; }

.steps { list-style: none; margin: 14px 0; }
.steps li { display: flex; gap: 14px; padding: 10px 0; border-bottom: 1px solid var(--border); font-size: 0.84rem; color: var(--ink-2); line-height: 1.6; max-width: 680px; }
.steps li:last-child { border-bottom: none; }
.steps .step-n { font-family: var(--mono); font-size: 0.65rem; font-weight: 600; color: var(--accent); min-width: 20px; margin-top: 2px; }

.module-list { margin-top: 16px; }
.module-entry { display: grid; grid-template-columns: 110px 1fr; gap: 0; border: 1px solid var(--border); border-radius: 3px; margin-bottom: 8px; overflow: hidden; font-size: 0.82rem; }
.me-key { background: var(--surface); border-right: 1px solid var(--border); padding: 12px 14px; font-family: var(--mono); font-size: 0.68rem; font-weight: 600; color: var(--ink); display: flex; align-items: flex-start; gap: 6px; line-height: 1.4; }
.me-val { padding: 12px 16px; color: var(--ink-2); line-height: 1.6; }
.me-val strong { color: var(--ink); font-weight: 600; }

.inline-note { font-family: var(--mono); font-size: 0.7rem; color: var(--ink-3); padding: 4px 0 4px 12px; border-left: 2px solid var(--border-strong); margin: 8px 0; max-width: 580px; }

.file-tree { font-family: var(--mono); font-size: 0.74rem; line-height: 2; color: var(--ink-2); padding: 16px 20px; background: var(--surface); border: 1px solid var(--border); border-radius: 4px; margin: 16px 0; }
.ft-dir  { color: var(--ink); font-weight: 600; }
.ft-file { color: var(--blue); }
.ft-note { color: var(--ink-3); padding-left: 8px; font-size: 0.65rem; }

.tech-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-top: 16px; }
.tech-card { padding: 14px 16px; border: 1px solid var(--border); border-radius: 3px; }
.tech-card .tc-name { font-family: var(--mono); font-size: 0.72rem; font-weight: 600; color: var(--ink); margin-bottom: 4px; }
.tech-card .tc-desc { font-size: 0.78rem; color: var(--ink-2); line-height: 1.5; }

.doc-footer { padding: 32px 64px; border-top: 1px solid var(--border); background: var(--surface); display: flex; justify-content: space-between; align-items: center; font-family: var(--mono); font-size: 0.62rem; color: var(--ink-3); letter-spacing: 0.08em; }

@media (max-width: 860px) {
  .layout { grid-template-columns: 1fr; }
  .sidebar { display: none; }
  .content { padding: 0 24px; }
  .doc-header { padding: 32px 24px 28px; }
  .doc-header h1 { font-size: 1.4rem; }
  .doc-footer { flex-direction: column; gap: 8px; padding: 24px; }
  .tech-grid { grid-template-columns: 1fr; }
}
</style>
</head>
<body>
<div class="layout">

<nav class="sidebar">
  <div class="sb-header">
    <div class="sb-project">AeroAgent v2</div>
    <div class="sb-title">Code Documentation</div>
    <div class="sb-version">aviation-agent.html · 1,247 lines</div>
  </div>
  <div class="sb-group">
    <div class="sb-group-label">Overview</div>
    <a href="#overview" class="sb-link"><span class="ln">—</span>File Structure</a>
    <a href="#css-vars" class="sb-link"><span class="ln">—</span>CSS Variables</a>
  </div>
  <div class="sb-group">
    <div class="sb-group-label">Data Layer</div>
    <a href="#mods-array" class="sb-link"><span class="ln">~539</span>MODS array</a>
    <a href="#all-caps"   class="sb-link"><span class="ln">~782</span>ALL_CAPS map</a>
    <a href="#state"      class="sb-link"><span class="ln">~796</span>State variables</a>
  </div>
  <div class="sb-group">
    <div class="sb-group-label">Initialization</div>
    <a href="#init"       class="sb-link"><span class="ln">~807</span>init()</a>
    <a href="#tick"       class="sb-link"><span class="ln">~844</span>tick()</a>
    <a href="#fake-metar" class="sb-link"><span class="ln">~851</span>loadFakeMETAR()</a>
    <a href="#key-status" class="sb-link"><span class="ln">~861</span>updateKeyStatus()</a>
  </div>
  <div class="sb-group">
    <div class="sb-group-label">UI / Interaction</div>
    <a href="#select-mod" class="sb-link"><span class="ln">~883</span>selectMod()</a>
    <a href="#rendering"  class="sb-link"><span class="ln">~951</span>addAI() / addUser()</a>
    <a href="#typing"     class="sb-link"><span class="ln">~996</span>addTyping()</a>
    <a href="#fmt"        class="sb-link"><span class="ln">~1013</span>fmt() / escHtml()</a>
  </div>
  <div class="sb-group">
    <div class="sb-group-label">API &amp; Agent</div>
    <a href="#send"       class="sb-link"><span class="ln">~1038</span>send()</a>
    <a href="#tool-loop"  class="sb-link"><span class="ln">~1119</span>Tool-use loop</a>
    <a href="#sys-prompt" class="sb-link"><span class="ln">~1205</span>buildSystemPrompt()</a>
  </div>
</nav>

<main class="main">

<div class="doc-header">
  <div class="dh-breadcrumb">aviation-agent.html &rarr; <span>Code Documentation</span></div>
  <h1>AeroAgent <em>v2</em></h1>
  <p class="dh-sub">A single-file, browser-native aviation operations AI agent. Eight specialist modules backed by Claude Sonnet 4 with live web search, multi-turn conversation history, and dynamic system prompt injection.</p>
  <div class="dh-meta">
    <span class="dh-badge"><strong>1,247 lines</strong> &middot; HTML/CSS/JS</span>
    <span class="dh-badge"><strong>Model:</strong> claude-sonnet-4-20250514</span>
    <span class="dh-badge"><strong>Station:</strong> MROC / SJO</span>
    <span class="dh-badge"><strong>No backend required</strong></span>
  </div>
</div>

<div class="content">

<!-- 01 FILE STRUCTURE -->
<section class="doc-section" id="overview">
  <div class="section-anchor"><span class="section-num">01</span><span class="section-tag tag-html">HTML</span></div>
  <h2>File Structure</h2>
  <p>The entire application is a self-contained single HTML file. No build step, no bundler, no external JS dependencies beyond Google Fonts. Everything — layout, design, data, and agent behavior — lives in one document that can be opened directly in a browser.</p>

  <div class="file-tree">
<span class="ft-dir">aviation-agent.html</span>
&#x2502;
&#x251C;&#x2500;&#x2500; <span class="ft-dir">&lt;head&gt;</span>
&#x2502;   &#x251C;&#x2500;&#x2500; <span class="ft-file">&lt;style&gt;</span>       <span class="ft-note">Lines 7&#x2013;376 &middot; Full CSS: variables, layout, all components, animations</span>
&#x2502;   &#x2514;&#x2500;&#x2500; <span class="ft-file">Google Fonts</span>   <span class="ft-note">Rajdhani, Share Tech Mono, Exo 2</span>
&#x2502;
&#x2514;&#x2500;&#x2500; <span class="ft-dir">&lt;body&gt;</span>
    &#x251C;&#x2500;&#x2500; <span class="ft-file">&lt;header&gt;</span>      <span class="ft-note">Lines 382&#x2013;409 &middot; Logo, status pills, live indicator dot</span>
    &#x251C;&#x2500;&#x2500; <span class="ft-file">.main</span>         <span class="ft-note">Lines 411&#x2013;532 &middot; Three-column CSS grid wrapper</span>
    &#x2502;   &#x251C;&#x2500;&#x2500; <span class="ft-file">.sidebar-l</span>    <span class="ft-note">Lines 414&#x2013;452 &middot; Module buttons, station info, API key input</span>
    &#x2502;   &#x251C;&#x2500;&#x2500; <span class="ft-file">.chat-wrap</span>    <span class="ft-note">Lines 454&#x2013;486 &middot; Chat header, messages, quick prompts, textarea</span>
    &#x2502;   &#x2514;&#x2500;&#x2500; <span class="ft-file">.sidebar-r</span>    <span class="ft-note">Lines 488&#x2013;531 &middot; Live METAR, NOTAM list, traffic summary, runway status</span>
    &#x2502;
    &#x2514;&#x2500;&#x2500; <span class="ft-dir">&lt;script&gt;</span>       <span class="ft-note">Lines 535&#x2013;1244 &middot; All application logic</span>
        &#x251C;&#x2500;&#x2500; <span class="ft-file">MODS</span>          <span class="ft-note">Lines 539&#x2013;777 &middot; Module definitions (8 entries)</span>
        &#x251C;&#x2500;&#x2500; <span class="ft-file">ALL_CAPS</span>      <span class="ft-note">Lines 782&#x2013;793 &middot; Capability ID &rarr; label/class map</span>
        &#x251C;&#x2500;&#x2500; <span class="ft-file">State</span>         <span class="ft-note">Lines 796&#x2013;802 &middot; activeMod, history, busy</span>
        &#x251C;&#x2500;&#x2500; <span class="ft-file">init()</span>        <span class="ft-note">Lines 807&#x2013;842 &middot; Bootstrap: buttons, events, clock, METAR</span>
        &#x251C;&#x2500;&#x2500; <span class="ft-file">selectMod()</span>   <span class="ft-note">Lines 883&#x2013;946 &middot; Switch module, reset session, show welcome</span>
        &#x251C;&#x2500;&#x2500; <span class="ft-file">Rendering</span>     <span class="ft-note">Lines 951&#x2013;1033 &middot; addAI, addUser, addTyping, fmt, escHtml</span>
        &#x251C;&#x2500;&#x2500; <span class="ft-file">send()</span>        <span class="ft-note">Lines 1038&#x2013;1199 &middot; API dispatch, tool loop, error handling</span>
        &#x2514;&#x2500;&#x2500; <span class="ft-file">buildSystemPrompt()</span> <span class="ft-note">Lines 1205&#x2013;1241 &middot; Runtime context injection</span>
  </div>
</section>

<!-- 02 CSS VARIABLES -->
<section class="doc-section" id="css-vars">
  <div class="section-anchor"><span class="section-num">02</span><span class="section-tag tag-css">CSS</span></div>
  <h2>Design System — CSS Custom Properties</h2>
  <p>All visual styling is driven by CSS custom properties on <code>:root</code>. The theme is a dark aviation HUD aesthetic: deep navy backgrounds, cyan accents, and monospace typography. No color is hardcoded outside this block.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">CSS &middot; lines 10&#x2013;29</span></div>
    <pre class="code"><span class="p">:root {</span>
  <span class="c">/* Backgrounds: layered from darkest to lightest panel */</span>
  <span class="a">--bg</span><span class="p">:</span>      <span class="s">#040810</span><span class="p">;</span>  <span class="c">/* page background */</span>
  <span class="a">--bg2</span><span class="p">:</span>     <span class="s">#070d1a</span><span class="p">;</span>  <span class="c">/* inputs, code areas */</span>
  <span class="a">--panel</span><span class="p">:</span>   <span class="s">#091422</span><span class="p">;</span>  <span class="c">/* sidebar cards, AI bubble background */</span>
  <span class="a">--panel2</span><span class="p">:</span>  <span class="s">#0c1a2e</span><span class="p">;</span>  <span class="c">/* hover states */</span>

  <span class="c">/* Borders */</span>
  <span class="a">--border</span><span class="p">:</span>  <span class="s">#162d52</span><span class="p">;</span>
  <span class="a">--border2</span><span class="p">:</span> <span class="s">#1e3f6e</span><span class="p">;</span>  <span class="c">/* stronger, used on focus and active states */</span>

  <span class="c">/* Accent palette */</span>
  <span class="a">--accent</span><span class="p">:</span>  <span class="s">#00c8f0</span><span class="p">;</span>  <span class="c">/* primary cyan: headers, active elements */</span>
  <span class="a">--accent2</span><span class="p">:</span> <span class="s">#0088bb</span><span class="p">;</span>  <span class="c">/* dimmed cyan: borders, secondary text */</span>
  <span class="a">--accent3</span><span class="p">:</span> <span class="s">#ff6b35</span><span class="p">;</span>  <span class="c">/* orange: user avatar, user message border */</span>
  <span class="a">--green</span><span class="p">:</span>   <span class="s">#00e87a</span><span class="p">;</span>  <span class="c">/* GO / OPERATIONAL / system nominal */</span>
  <span class="a">--yellow</span><span class="p">:</span>  <span class="s">#ffc840</span><span class="p">;</span>  <span class="c">/* CAUTION / NOTAMs / amber status */</span>
  <span class="a">--red</span><span class="p">:</span>     <span class="s">#ff3d5a</span><span class="p">;</span>  <span class="c">/* NO-GO / critical / invalid key */</span>
  <span class="a">--purple</span><span class="p">:</span>  <span class="s">#9b6dff</span><span class="p">;</span>  <span class="c">/* tool call cards and badges */</span>

  <span class="c">/* Text scale */</span>
  <span class="a">--text</span><span class="p">:</span>    <span class="s">#b8d4ee</span><span class="p">;</span>  <span class="c">/* primary body text */</span>
  <span class="a">--text2</span><span class="p">:</span>   <span class="s">#6a90b8</span><span class="p">;</span>  <span class="c">/* secondary / metadata */</span>
  <span class="a">--text3</span><span class="p">:</span>   <span class="s">#2e4e72</span><span class="p">;</span>  <span class="c">/* muted / panel labels */</span>
  <span class="a">--text4</span><span class="p">:</span>   <span class="s">#1a2e44</span><span class="p">;</span>  <span class="c">/* very muted / timestamps */</span>
<span class="p">}</span></pre>
  </div>

  <div class="callout note">
    <span class="icon">i</span>
    <span>The green/yellow/red semantic palette mirrors real aviation ops color conventions: GREEN = go, AMBER = caution, RED = no-go. This maps directly to how status values are displayed in the sidebar widgets (e.g., <code>.iv.g</code>, <code>.iv.y</code>, <code>.iv.r</code> utility classes).</span>
  </div>
</section>

<!-- 03 MODS -->
<section class="doc-section" id="mods-array">
  <div class="section-anchor"><span class="section-num">03</span><span class="section-tag tag-data">Data</span></div>
  <h2>MODS — Module Definitions Array</h2>
  <p>The <code>MODS</code> array (lines 539–777) is the central data structure. It contains one object per operational domain. Each object defines the module's identity, its domain-expert system prompt, which tools to enable for the API, and what quick-prompt suggestions to display.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 539&#x2013;572 (AVSEC entry, condensed)</span></div>
    <pre class="code"><span class="k">const</span> <span class="n">MODS</span> <span class="p">= [</span>
  <span class="p">{</span>
    <span class="a">id</span><span class="p">:</span>           <span class="s">'avsec'</span><span class="p">,</span>            <span class="c">// key — used to build DOM id 'mb-avsec'</span>
    <span class="a">icon</span><span class="p">:</span>         <span class="s">'&#x1F6E1;&#xFE0F;'</span><span class="p">,</span>
    <span class="a">name</span><span class="p">:</span>         <span class="s">'AVSEC'</span><span class="p">,</span>            <span class="c">// short label on sidebar button</span>
    <span class="a">sub</span><span class="p">:</span>          <span class="s">'Security Operations'</span><span class="p">,</span>
    <span class="a">tag</span><span class="p">:</span>          <span class="s">'AVSEC OPS'</span><span class="p">,</span>         <span class="c">// shown in the chat header bar</span>
    <span class="a">title</span><span class="p">:</span>        <span class="s">'Aviation Security Intelligence'</span><span class="p">,</span>
    <span class="a">tools</span><span class="p">:</span>        <span class="p">[</span><span class="s">'WEB_SEARCH'</span><span class="p">,</span> <span class="s">'REG_LOOKUP'</span><span class="p">,</span> <span class="s">'INCIDENT_LOG'</span><span class="p">],</span>
    <span class="a">caps</span><span class="p">:</span>         <span class="p">[</span><span class="s">'web'</span><span class="p">,</span> <span class="s">'parse'</span><span class="p">,</span> <span class="s">'data'</span><span class="p">],</span>  <span class="c">// CSS class keys for sidebar badges</span>
    <span class="a">systemPrompt</span><span class="p">:</span> <span class="s">`You are AeroAgent AVSEC v2 — expert aviation security
intelligence for MROC/SJO...

CORE EXPERTISE:
- ICAO Annex 17 security standards
- Threat assessment: BOM/IED identification, IATA AVSEC Matrix
- Access control: SRIA credentialing (tarjeta roja/verde/amarilla)
...`</span><span class="p">,</span>
    <span class="a">quickPrompts</span><span class="p">:</span> <span class="p">[</span>
      <span class="s">'AVSEC incident response SOP'</span><span class="p">,</span>
      <span class="s">'Prohibited items — current list'</span><span class="p">,</span>
      <span class="c">// ...</span>
    <span class="p">]</span>
  <span class="p">},</span>
  <span class="c">// ... 7 more entries: ramp, wx, notam, flightplan, cargo, schedule, wb</span>
<span class="p">];</span></pre>
  </div>

  <table class="prop-table">
    <thead><tr><th>Property</th><th>Type</th><th>Purpose</th></tr></thead>
    <tbody>
      <tr><td>id</td><td><code>string</code></td><td>Unique key. Used to construct the button DOM id <code>mb-{id}</code> and to look up the module in <code>selectMod(id)</code>.</td></tr>
      <tr><td>icon / name / sub</td><td><code>string</code></td><td>Display fields rendered into the sidebar button by <code>init()</code>.</td></tr>
      <tr><td>tag / title</td><td><code>string</code></td><td>Shown in the chat panel header once the module is active.</td></tr>
      <tr><td>tools</td><td><code>string[]</code></td><td>List of capability IDs. Drives which badge pills appear in the header and — critically — whether <code>WEB_SEARCH</code> is included in the Anthropic API request body.</td></tr>
      <tr><td>caps</td><td><code>string[]</code></td><td>CSS class shorthand (<code>'web'</code>, <code>'calc'</code>, <code>'parse'</code>, <code>'data'</code>) for the colored tag pills in the left sidebar Tool Capabilities panel.</td></tr>
      <tr><td>systemPrompt</td><td><code>string</code></td><td>The expert domain instructions sent as the <code>system</code> parameter on every API call. This is the primary knowledge carrier. Injected into <code>buildSystemPrompt()</code> alongside live runtime context.</td></tr>
      <tr><td>quickPrompts</td><td><code>string[]</code></td><td>Pre-written queries shown as clickable buttons under the chat. Clicking one populates the textarea and calls <code>send()</code> immediately.</td></tr>
    </tbody>
  </table>

  <div class="subsection">
    <h3>The 8 modules at a glance</h3>
    <div class="module-list">
      <div class="module-entry">
        <div class="me-key">&#x1F6E1;&#xFE0F; avsec</div>
        <div class="me-val"><strong>Aviation Security Intelligence.</strong> ICAO Annex 17, DGAC AVSEC regs, threat assessment, access control (SRIA credentialing), passenger/baggage screening (EDS/ETD), incident response with CISM protocols, air cargo Known Shipper requirements.</div>
      </div>
      <div class="module-entry">
        <div class="me-key">&#x1F6EB; ramp</div>
        <div class="me-val"><strong>Ramp Operations Control.</strong> Aircraft marshalling, pushback, FOD prevention, GSE (GPU/ASU/tugs), fueling (JETA1, hydrant vs bowser), turnaround times by a/c type, jet blast safety zones, IATA AHM 070 ground damage reporting.</div>
      </div>
      <div class="module-entry">
        <div class="me-key">&#x1F326;&#xFE0F; wx</div>
        <div class="me-val"><strong>Meteorology &amp; WX Operations.</strong> Full METAR/TAF decode (all groups incl. RVR, SNOCLO, runway state), SIGMET/AIRMET, tropical systems, CB/TS wind shear, MROC climatology, density altitude calculation, IFR minimums, CAT I/II/III eligibility.</div>
      </div>
      <div class="module-entry">
        <div class="me-key">&#x1F4CB; notam</div>
        <div class="me-val"><strong>NOTAM Research &amp; Analysis.</strong> ICAO Q-line field-by-field decode, Snowtam/Ashtam (NRC format), TFR parsing, flight planning impact, validity types (PERM/EST/C/R series), Digital NOTAM vs traditional, AIS Costa Rica sourcing procedures.</div>
      </div>
      <div class="module-entry">
        <div class="me-key">&#x1F5FA;&#xFE0F; flightplan</div>
        <div class="me-val"><strong>Flight Plan &amp; Navigation.</strong> ICAO FPL all fields (7,8,9,10,13,15,16,18,19), PBN codes, MROC SIDs (COCR1A/B/C) &amp; STARs (GUMAR/ARTUR/ROSAL), fuel planning per ICAO Annex 2, ETOPS, CPDLC/ADS-C for COCR FIR.</div>
      </div>
      <div class="module-entry">
        <div class="me-key">&#x1F4E6; cargo</div>
        <div class="me-val"><strong>Cargo &amp; Dangerous Goods.</strong> IATA DGR 65th Ed + ICAO Doc 9284 — all 9 DG classes, packing instructions by UN number, Shipper's Declaration, segregation table, CEIV Pharma temp-controlled, IATA LAR live animals, CITES permits, ULD specs.</div>
      </div>
      <div class="module-entry">
        <div class="me-key">&#x1F4C5; schedule</div>
        <div class="me-val"><strong>Operations Scheduling &amp; IROP.</strong> EASA ORO.FTL + FAA Part 117, duty period construction for augmented crews, IROP cascade recovery, Level-3 slot management (IATA SCR), CTOT/ATFM Eurocontrol compliance (&#x2212;5/+10 window), IATA AHM 730 delay codes.</div>
      </div>
      <div class="module-entry">
        <div class="me-key">&#x2696;&#xFE0F; wb</div>
        <div class="me-val"><strong>Weight &amp; Balance Calculator.</strong> Full ZFW/TOW/LW chain, MAC% and index system, aircraft-specific data (B737-800, A320/A321, E190, ATR72-600, B777-300ER), load sheet interpretation (LIDO/Inform/LoadFox), trim sheet, IATA Res. 788 standard weights.</div>
      </div>
    </div>
  </div>
</section>

<!-- 04 ALL_CAPS -->
<section class="doc-section" id="all-caps">
  <div class="section-anchor"><span class="section-num">04</span><span class="section-tag tag-data">Data</span></div>
  <h2>ALL_CAPS — Capability Map</h2>
  <p><code>ALL_CAPS</code> (lines 782–793) is a lookup table that maps the string IDs used in <code>MODS[].tools</code> to their display label, CSS class, and description. It's used in two places: rendering the tool badge pills in the chat header, and deciding whether to include the live web search tool in the API request body.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 782&#x2013;793</span></div>
    <pre class="code"><span class="k">const</span> <span class="n">ALL_CAPS</span> <span class="p">= [</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'WEB_SEARCH'</span><span class="p">,</span>    <span class="a">label</span><span class="p">:</span> <span class="s">'WEB SEARCH'</span><span class="p">,</span>   <span class="a">cls</span><span class="p">:</span> <span class="s">'web'</span><span class="p">,</span>   <span class="a">desc</span><span class="p">:</span> <span class="s">'Live internet research'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'METAR_PARSE'</span><span class="p">,</span>   <span class="a">label</span><span class="p">:</span> <span class="s">'METAR/TAF'</span><span class="p">,</span>    <span class="a">cls</span><span class="p">:</span> <span class="s">'parse'</span><span class="p">,</span> <span class="a">desc</span><span class="p">:</span> <span class="s">'Weather decode'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'NOTAM_PARSE'</span><span class="p">,</span>   <span class="a">label</span><span class="p">:</span> <span class="s">'NOTAM DECODE'</span><span class="p">,</span>  <span class="a">cls</span><span class="p">:</span> <span class="s">'parse'</span><span class="p">,</span> <span class="a">desc</span><span class="p">:</span> <span class="s">'Parse notices'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'DGR_LOOKUP'</span><span class="p">,</span>    <span class="a">label</span><span class="p">:</span> <span class="s">'DGR LOOKUP'</span><span class="p">,</span>   <span class="a">cls</span><span class="p">:</span> <span class="s">'data'</span><span class="p">,</span>  <span class="a">desc</span><span class="p">:</span> <span class="s">'Dangerous goods'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'REG_LOOKUP'</span><span class="p">,</span>    <span class="a">label</span><span class="p">:</span> <span class="s">'REG LOOKUP'</span><span class="p">,</span>   <span class="a">cls</span><span class="p">:</span> <span class="s">'data'</span><span class="p">,</span>  <span class="a">desc</span><span class="p">:</span> <span class="s">'Regulatory cite'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'WB_CALC'</span><span class="p">,</span>       <span class="a">label</span><span class="p">:</span> <span class="s">'W&amp;B CALC'</span><span class="p">,</span>     <span class="a">cls</span><span class="p">:</span> <span class="s">'calc'</span><span class="p">,</span>  <span class="a">desc</span><span class="p">:</span> <span class="s">'Weight &amp; balance'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'FTL_CALC'</span><span class="p">,</span>       <span class="a">label</span><span class="p">:</span> <span class="s">'FTL CALC'</span><span class="p">,</span>     <span class="a">cls</span><span class="p">:</span> <span class="s">'calc'</span><span class="p">,</span>  <span class="a">desc</span><span class="p">:</span> <span class="s">'Crew duty limits'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'ROUTE_CALC'</span><span class="p">,</span>    <span class="a">label</span><span class="p">:</span> <span class="s">'ROUTE PLAN'</span><span class="p">,</span>   <span class="a">cls</span><span class="p">:</span> <span class="s">'calc'</span><span class="p">,</span>  <span class="a">desc</span><span class="p">:</span> <span class="s">'Flight plan'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'WEATHER_FETCH'</span><span class="p">,</span>  <span class="a">label</span><span class="p">:</span> <span class="s">'WX FETCH'</span><span class="p">,</span>     <span class="a">cls</span><span class="p">:</span> <span class="s">'web'</span><span class="p">,</span>   <span class="a">desc</span><span class="p">:</span> <span class="s">'Live weather'</span> <span class="p">},</span>
  <span class="p">{</span> <span class="a">id</span><span class="p">:</span> <span class="s">'INCIDENT_LOG'</span><span class="p">,</span>   <span class="a">label</span><span class="p">:</span> <span class="s">'INCIDENT LOG'</span><span class="p">,</span>  <span class="a">cls</span><span class="p">:</span> <span class="s">'data'</span><span class="p">,</span>  <span class="a">desc</span><span class="p">:</span> <span class="s">'SMS reporting'</span> <span class="p">},</span>
<span class="p">];</span></pre>
  </div>

  <div class="callout note">
    <span class="icon">i</span>
    <span>Only <code>WEB_SEARCH</code> and <code>WEATHER_FETCH</code> trigger an actual Anthropic tool call. The others (<code>WB_CALC</code>, <code>FTL_CALC</code>, etc.) are display labels only — they inform the operator what the module can do, but the computation happens inside the model's reasoning without a separate tool call.</span>
  </div>
</section>

<!-- 05 STATE -->
<section class="doc-section" id="state">
  <div class="section-anchor"><span class="section-num">05</span><span class="section-tag tag-js">JS</span></div>
  <h2>Global State Variables</h2>
  <p>Three module-level variables hold all runtime state. No framework — plain JS variables in the script's top scope, readable by all functions.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 797&#x2013;802</span></div>
    <pre class="code"><span class="k">let</span> <span class="n">activeMod</span> <span class="p">=</span> <span class="v">null</span><span class="p">;</span>  <span class="c">// currently selected MODS entry; null until user picks one</span>
<span class="k">let</span> <span class="n">history</span>   <span class="p">=</span> <span class="p">[];</span>    <span class="c">// message turns: [ { role: 'user'|'assistant', content } ]</span>
<span class="k">let</span> <span class="n">busy</span>      <span class="p">=</span> <span class="v">false</span><span class="p">;</span> <span class="c">// true while an API call is in-flight; blocks re-send</span>

<span class="k">function</span> <span class="f">getKey</span><span class="p">(){</span>
  <span class="k">return</span> document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'apiKeyIn'</span><span class="p">).</span>value.<span class="f">trim</span><span class="p">();</span>
<span class="p">}</span></pre>
  </div>

  <table class="prop-table">
    <thead><tr><th>Variable</th><th>Type</th><th>Notes</th></tr></thead>
    <tbody>
      <tr><td>activeMod</td><td><code>object | null</code></td><td>Set by <code>selectMod()</code>. Read by <code>send()</code> to build the tool list, and by <code>buildSystemPrompt()</code> to get the domain system prompt.</td></tr>
      <tr><td>history</td><td><code>Array</code></td><td>Grows with each turn. Passed wholesale to every API call for full multi-turn context. Reset to <code>[]</code> whenever a new module is selected.</td></tr>
      <tr><td>busy</td><td><code>boolean</code></td><td>Set <code>true</code> at the start of <code>send()</code> and back to <code>false</code> when the call resolves. Guards against concurrent requests and disables the send button during calls.</td></tr>
    </tbody>
  </table>
</section>

<!-- 06 INIT -->
<section class="doc-section" id="init">
  <div class="section-anchor"><span class="section-num">06</span><span class="section-tag tag-js">JS</span></div>
  <h2>init() — Application Bootstrap</h2>
  <p><code>init()</code> (lines 807–842) is called once at the very end of the script (line 1243). It performs all one-time setup: building the sidebar buttons from the <code>MODS</code> data, binding all event listeners, starting the clock, and loading the placeholder METAR.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 807&#x2013;842</span></div>
    <pre class="code"><span class="k">function</span> <span class="f">init</span><span class="p">(){</span>

  <span class="c">// 1. Build module buttons dynamically from MODS — never hardcoded in HTML</span>
  <span class="k">const</span> grid <span class="p">=</span> document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'modGrid'</span><span class="p">);</span>
  <span class="n">MODS</span>.<span class="f">forEach</span><span class="p">(</span>m <span class="p">=></span> <span class="p">{</span>
    <span class="k">const</span> b <span class="p">=</span> document.<span class="f">createElement</span><span class="p">(</span><span class="s">'button'</span><span class="p">);</span>
    b.id <span class="p">=</span> <span class="s">'mb-'</span> <span class="p">+</span> m.id<span class="p">;</span>         <span class="c">// e.g. 'mb-avsec', 'mb-wx'</span>
    b.onclick <span class="p">=</span> <span class="p">()</span> <span class="p">=></span> <span class="f">selectMod</span><span class="p">(</span>m.id<span class="p">);</span>
    b.innerHTML <span class="p">=</span> <span class="s">`...${m.icon}...${m.name}...${m.sub}...`</span><span class="p">;</span>
    grid.<span class="f">appendChild</span><span class="p">(</span>b<span class="p">);</span>
  <span class="p">});</span>

  <span class="c">// 2. API key input: validate format on every keystroke</span>
  document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'apiKeyIn'</span><span class="p">).</span>
    <span class="f">addEventListener</span><span class="p">(</span><span class="s">'input'</span><span class="p">,</span> updateKeyStatus<span class="p">);</span>

  <span class="c">// 3. Start the 1-second UTC clock loop</span>
  <span class="f">tick</span><span class="p">();</span>
  <span class="f">setInterval</span><span class="p">(</span>tick<span class="p">,</span> <span class="n">1000</span><span class="p">);</span>

  <span class="c">// 4. Textarea: auto-resize on type, send on Enter (Shift+Enter = newline)</span>
  <span class="k">const</span> inp <span class="p">=</span> document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'chatIn'</span><span class="p">);</span>
  inp.<span class="f">addEventListener</span><span class="p">(</span><span class="s">'input'</span><span class="p">,</span> <span class="p">()</span> <span class="p">=></span> <span class="p">{</span>
    inp.style.height <span class="p">=</span> <span class="s">'auto'</span><span class="p">;</span>
    inp.style.height <span class="p">=</span> <span class="f">Math.min</span><span class="p">(</span>inp.scrollHeight<span class="p">,</span> <span class="n">110</span><span class="p">) +</span> <span class="s">'px'</span><span class="p">;</span>
  <span class="p">});</span>
  inp.<span class="f">addEventListener</span><span class="p">(</span><span class="s">'keydown'</span><span class="p">,</span> e <span class="p">=></span> <span class="p">{</span>
    <span class="k">if</span><span class="p">(</span>e.key <span class="p">===</span> <span class="s">'Enter'</span> <span class="p">&amp;&amp;</span> <span class="p">!</span>e.shiftKey<span class="p">){</span> e.<span class="f">preventDefault</span><span class="p">();</span> <span class="f">send</span><span class="p">();</span> <span class="p">}</span>
  <span class="p">});</span>

  <span class="c">// 5. Populate the right sidebar METAR/wind/QNH widgets with a placeholder</span>
  <span class="f">loadFakeMETAR</span><span class="p">();</span>
<span class="p">}</span></pre>
  </div>
</section>

<!-- 07 TICK / METAR / KEY -->
<section class="doc-section" id="tick">
  <div class="section-anchor"><span class="section-num">07</span><span class="section-tag tag-js">JS</span></div>
  <h2>tick(), loadFakeMETAR(), updateKeyStatus()</h2>
  <p>Three small utility functions that keep the interface live and responsive.</p>

  <div class="subsection">
    <h3>tick() &mdash; lines 844&ndash;849</h3>
    <p>Called every second via <code>setInterval</code>. Updates three DOM elements in the left sidebar: the UTC clock, the local clock, and the context message counter (which reflects the current length of <code>history</code>).</p>
    <div class="code-wrap">
      <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 844&#x2013;849</span></div>
      <pre class="code"><span class="k">function</span> <span class="f">tick</span><span class="p">(){</span>
  <span class="k">const</span> n <span class="p">=</span> <span class="k">new</span> <span class="f">Date</span><span class="p">();</span>
  document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'utcClock'</span><span class="p">).</span>textContent <span class="p">=</span> n.<span class="f">toUTCString</span><span class="p">().</span><span class="f">slice</span><span class="p">(</span><span class="n">17</span><span class="p">,</span> <span class="n">25</span><span class="p">);</span>  <span class="c">// HH:MM:SS</span>
  document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'lclClock'</span><span class="p">).</span>textContent <span class="p">=</span> n.<span class="f">toLocaleTimeString</span><span class="p">(</span><span class="s">'en-US'</span><span class="p">,{</span>hour12<span class="p">:</span><span class="v">false</span><span class="p">});</span>
  document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'ctxCount'</span><span class="p">).</span>textContent <span class="p">=</span> history.length <span class="p">+</span> <span class="s">' msgs'</span><span class="p">;</span>
<span class="p">}</span></pre>
    </div>
  </div>

  <div class="subsection" id="fake-metar">
    <h3>loadFakeMETAR() &mdash; lines 851&ndash;859</h3>
    <p>Populates the right sidebar METAR widget and the Runway Status wind/QNH fields with a hardcoded but realistic MROC observation string. This is a static placeholder — a future version would fetch from aviationweather.gov on load. The string <code>MROC 301200Z 08008KT 9999 FEW020 SCT100 26/22 A2992 NOSIG</code> is decoded manually to extract the wind direction/speed and altimeter setting for the separate widget fields.</p>
  </div>

  <div class="subsection" id="key-status">
    <h3>updateKeyStatus() &mdash; lines 861&ndash;878</h3>
    <p>Fires on every keystroke in the API key password input. Checks the key prefix and updates the indicator dot color, border class, and status text accordingly. No network call is made — it only checks string format.</p>
    <div class="code-wrap">
      <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 861&#x2013;878 (simplified)</span></div>
      <pre class="code"><span class="k">function</span> <span class="f">updateKeyStatus</span><span class="p">(){</span>
  <span class="k">const</span> k <span class="p">=</span> <span class="f">getKey</span><span class="p">();</span>
  <span class="k">if</span><span class="p">(!</span>k<span class="p">){</span>
    <span class="c">// grey dot &rarr; "NO KEY"</span>
  <span class="p">}</span> <span class="k">else if</span><span class="p">(</span>k.<span class="f">startsWith</span><span class="p">(</span><span class="s">'sk-'</span><span class="p">)){</span>
    <span class="c">// green dot &rarr; "KEY OK &#x2713;" — does not verify key with a real API call</span>
  <span class="p">}</span> <span class="k">else</span> <span class="p">{</span>
    <span class="c">// red dot &rarr; "INVALID FORMAT"</span>
  <span class="p">}</span>
<span class="p">}</span></pre>
    </div>
    <div class="callout warn">
      <span class="icon">&#x26A0;</span>
      <span>The API key is never stored — it lives only in the DOM input value for the browser session. It is read fresh via <code>getKey()</code> immediately before each API call.</span>
    </div>
  </div>
</section>

<!-- 08 SELECT MOD -->
<section class="doc-section" id="select-mod">
  <div class="section-anchor"><span class="section-num">08</span><span class="section-tag tag-js">JS</span></div>
  <h2>selectMod() — Module Switching</h2>
  <p><code>selectMod(id)</code> (lines 883–946) is the main UI state transition. It runs when the user clicks any module button or welcome-screen shortcut tag. It fully resets the current session and re-configures the interface for the selected domain.</p>

  <ul class="steps">
    <li><span class="step-n">1.</span>Looks up the module object from <code>MODS</code> by id. Returns early if not found.</li>
    <li><span class="step-n">2.</span>Toggles the <code>.active</code> CSS class: removes it from all <code>.mod-btn</code> buttons, adds it to the selected one (reveals the left accent bar and cyan text color).</li>
    <li><span class="step-n">3.</span>Sets <code>activeMod</code> to the found object and resets <code>history = []</code>, clearing all prior conversation context.</li>
    <li><span class="step-n">4.</span>Updates the chat header tag and title text from <code>mod.tag</code> and <code>mod.title</code>.</li>
    <li><span class="step-n">5.</span>Re-renders the tool badge pills in the chat header by iterating <code>mod.tools</code> and looking each up in <code>ALL_CAPS</code>.</li>
    <li><span class="step-n">6.</span>Re-renders the capability pills in the left sidebar Tool Capabilities panel from <code>mod.caps</code>.</li>
    <li><span class="step-n">7.</span>Clears <code>#chatMsgs</code> and calls <code>addAI()</code> with a module activation message that lists the module's capabilities and current station/UTC time.</li>
    <li><span class="step-n">8.</span>Re-renders the quick prompt buttons from <code>mod.quickPrompts</code>. Each button, on click, writes its text to the textarea and immediately calls <code>send()</code>.</li>
  </ul>
</section>

<!-- 09 RENDERING -->
<section class="doc-section" id="rendering">
  <div class="section-anchor"><span class="section-num">09</span><span class="section-tag tag-js">JS</span></div>
  <h2>Message Rendering — addAI(), addUser()</h2>
  <p>Messages are rendered by appending new <code>.msg</code> elements to <code>#chatMsgs</code>. Each contains an avatar (<code>.av</code>) and a bubble (<code>.bubble</code>). After every append, <code>scrollTop</code> is set to <code>scrollHeight</code> to keep the latest message visible. The <code>msgIn</code> CSS keyframe animates each new message in from slightly below.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 951&#x2013;978</span></div>
    <pre class="code"><span class="k">function</span> <span class="f">addAI</span><span class="p">(</span>text<span class="p">,</span> toolCalls<span class="p">){</span>
  <span class="k">const</span> msgs <span class="p">=</span> document.<span class="f">getElementById</span><span class="p">(</span><span class="s">'chatMsgs'</span><span class="p">);</span>
  <span class="k">const</span> div  <span class="p">=</span> document.<span class="f">createElement</span><span class="p">(</span><span class="s">'div'</span><span class="p">);</span>
  div.className <span class="p">=</span> <span class="s">'msg ai'</span><span class="p">;</span>

  <span class="c">// Optional second argument: tool calls that preceded this response</span>
  <span class="k">let</span> toolHtml <span class="p">=</span> <span class="s">''</span><span class="p">;</span>
  <span class="k">if</span><span class="p">(</span>toolCalls <span class="p">&amp;&amp;</span> toolCalls.length<span class="p">){</span>
    toolHtml <span class="p">=</span> toolCalls.<span class="f">map</span><span class="p">(</span>tc <span class="p">=></span> <span class="s">`
      &lt;div class="tool-call"&gt;
        &lt;div class="tc-name"&gt;${tc.name}&lt;/div&gt;
        &lt;div class="tc-detail"&gt;${tc.input}&lt;/div&gt;
        &lt;div class="tc-result"&gt;${escHtml(tc.result)}&lt;/div&gt;
      &lt;/div&gt;`</span><span class="p">).</span><span class="f">join</span><span class="p">(</span><span class="s">''</span><span class="p">);</span>
  <span class="p">}</span>

  div.innerHTML <span class="p">=</span> <span class="s">`
    &lt;div class="av ai"&gt;AI&lt;/div&gt;
    &lt;div&gt;
      ${toolHtml}
      &lt;div class="bubble"&gt;${fmt(text)}&lt;/div&gt;
      &lt;div class="msg-meta"&gt;AEROAGENT v2 &middot; [time] UTC&lt;/div&gt;
    &lt;/div&gt;`</span><span class="p">;</span>

  msgs.<span class="f">appendChild</span><span class="p">(</span>div<span class="p">);</span>
  msgs.scrollTop <span class="p">=</span> msgs.scrollHeight<span class="p">;</span>
<span class="p">}</span></pre>
  </div>

  <p><code>addAI()</code> accepts an optional <code>toolCalls</code> array of <code>{ name, input, result }</code>. When provided, each entry renders as a purple-bordered tool-call card above the response bubble — showing the operator exactly what was searched and what was returned before the model answered.</p>
  <p><code>addUser(text)</code> (lines 981–994) works the same way but with <code>.msg.user</code> layout (reversed flex direction, orange avatar labeled "OPS").</p>

  <div class="subsection" id="typing">
    <h3>addTyping() / removeTyping() &mdash; lines 996&ndash;1010</h3>
    <p>While an API call is in-flight, <code>addTyping()</code> injects a <code>.msg.ai</code> element with <code>id="typing"</code> containing three animated dot spans (CSS <code>@keyframes dot</code> bounce). <code>removeTyping()</code> queries for that id and removes it — called as soon as the API response arrives or an error is caught.</p>
  </div>
</section>

<!-- 10 FMT -->
<section class="doc-section" id="fmt">
  <div class="section-anchor"><span class="section-num">10</span><span class="section-tag tag-js">JS</span></div>
  <h2>fmt() — Lightweight Markdown Renderer</h2>
  <p><code>fmt(t)</code> (lines 1013–1029) converts the model's Markdown output to HTML via a chain of regex replacements. It handles the subset of Markdown Claude uses in aviation ops responses: code fences, bold/italic, inline code, headings (as styled <code>&lt;strong&gt;</code>), horizontal rules, and both ordered and unordered lists.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 1013&#x2013;1029</span></div>
    <pre class="code"><span class="k">function</span> <span class="f">fmt</span><span class="p">(</span>t<span class="p">){</span>
  <span class="k">return</span> t
    <span class="c">// Step 1: escape HTML entities FIRST — prevents XSS from user input or model output</span>
    .<span class="f">replace</span><span class="p">(/&amp;/g,</span>  <span class="s">'&amp;amp;'</span><span class="p">)</span>
    .<span class="f">replace</span><span class="p">(/&lt;/g,</span>  <span class="s">'&amp;lt;'</span><span class="p">)</span>
    .<span class="f">replace</span><span class="p">(/&gt;/g,</span>  <span class="s">'&amp;gt;'</span><span class="p">)</span>

    <span class="c">// Step 2: fenced code blocks — must run before inline code rule</span>
    .<span class="f">replace</span><span class="p">(/```([\s\S]*?)```/g,</span>   <span class="s">'&lt;pre&gt;$1&lt;/pre&gt;'</span><span class="p">)</span>

    <span class="c">// Step 3: inline formatting</span>
    .<span class="f">replace</span><span class="p">(/\*\*(.*?)\*\*/g,</span>      <span class="s">'&lt;strong&gt;$1&lt;/strong&gt;'</span><span class="p">)</span>
    .<span class="f">replace</span><span class="p">(/\*(.*?)\*/g,</span>          <span class="s">'&lt;em&gt;$1&lt;/em&gt;'</span><span class="p">)</span>
    .<span class="f">replace</span><span class="p">(/`([^`]+)`/g,</span>          <span class="s">'&lt;code&gt;$1&lt;/code&gt;'</span><span class="p">)</span>

    <span class="c">// Step 4: headings h1–h3 mapped to styled &lt;strong&gt; display blocks</span>
    .<span class="f">replace</span><span class="p">(/^### (.+)$/gm,</span>        <span class="s">'&lt;strong style="..."&gt;$1&lt;/strong&gt;'</span><span class="p">)</span>

    <span class="c">// Step 5: horizontal rule</span>
    .<span class="f">replace</span><span class="p">(/^---$/gm,</span>             <span class="s">'&lt;hr&gt;'</span><span class="p">)</span>

    <span class="c">// Step 6: lists — convert line items to &lt;li&gt;, then wrap in &lt;ul&gt;</span>
    .<span class="f">replace</span><span class="p">(/^\d+\. (.+)$/gm,</span>      <span class="s">'&lt;li&gt;$1&lt;/li&gt;'</span><span class="p">)</span>   <span class="c">// ordered</span>
    .<span class="f">replace</span><span class="p">(/^[•\-] (.+)$/gm,</span>     <span class="s">'&lt;li&gt;$1&lt;/li&gt;'</span><span class="p">)</span>   <span class="c">// unordered</span>
    .<span class="f">replace</span><span class="p">(/(&lt;li&gt;[\s\S]+?&lt;\/li&gt;)/g,</span> <span class="s">'&lt;ul&gt;$1&lt;/ul&gt;'</span><span class="p">)</span>
    .<span class="f">replace</span><span class="p">(/&lt;\/ul&gt;\s*&lt;ul&gt;/g,</span>     <span class="s">''</span><span class="p">)</span>             <span class="c">// merge adjacent lists</span>

    <span class="c">// Step 7: remaining newlines &rarr; &lt;br&gt; (last, so block elements aren't broken)</span>
    .<span class="f">replace</span><span class="p">(/\n/g,</span>                 <span class="s">'&lt;br&gt;'</span><span class="p">);</span>
<span class="p">}</span></pre>
  </div>

  <div class="callout warn">
    <span class="icon">&#x26A0;</span>
    <span>HTML entity escaping runs first. This means the model cannot inject raw HTML into the chat bubble, even accidentally. The separate <code>escHtml(t)</code> helper (line 1031) is used specifically for rendering tool-call result text, which may contain angle brackets from raw METAR or NOTAM data.</span>
  </div>
</section>

<!-- 11 SEND -->
<section class="doc-section" id="send">
  <div class="section-anchor"><span class="section-num">11</span><span class="section-tag tag-api">API</span></div>
  <h2>send() — API Dispatch &amp; Guard Logic</h2>
  <p><code>send()</code> (lines 1038–1199) is the core async function that handles the full request lifecycle. It validates state before touching the network, constructs the request body, dispatches to the Anthropic API, and routes the response to either the tool-use loop or a normal text render.</p>

  <ul class="steps">
    <li><span class="step-n">1.</span><strong>Guard checks.</strong> Returns immediately if <code>busy</code> is true, if the textarea is empty, if no module is selected (<code>activeMod === null</code>), or if no API key is in the input. Also rejects keys that don't start with <code>sk-</code>.</li>
    <li><span class="step-n">2.</span>Clears the textarea, sets <code>busy = true</code>, disables the send button, appends the user message to both the DOM and <code>history</code>, and shows the typing indicator.</li>
    <li><span class="step-n">3.</span><strong>Tool list construction.</strong> Checks <code>activeMod.tools</code> for <code>'WEB_SEARCH'</code> or <code>'WEATHER_FETCH'</code>. If either is present, adds the <code>{ type: 'web_search_20250305', name: 'web_search' }</code> object to the request.</li>
    <li><span class="step-n">4.</span>Fires <code>fetch</code> to <code>https://api.anthropic.com/v1/messages</code> with the model, <code>max_tokens: 2048</code>, the built system prompt, and the full <code>history</code> array.</li>
    <li><span class="step-n">5.</span>On a non-OK HTTP response: shows an inline error message with the status code, Anthropic error type, and a contextual hint (e.g., "Rate limit hit — wait and retry" for 429, key hint for 401).</li>
    <li><span class="step-n">6.</span>On success: checks <code>data.stop_reason</code>. If <code>'tool_use'</code>, enters the tool loop (see §12). Otherwise extracts text blocks and calls <code>addAI()</code>.</li>
    <li><span class="step-n">7.</span>Resets <code>busy = false</code>, re-enables the send button, and restores focus to the textarea.</li>
  </ul>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 1067&#x2013;1098 (request construction)</span></div>
    <pre class="code"><span class="c">// Determine which tools to offer based on this module's declared capabilities</span>
<span class="k">const</span> toolList <span class="p">= [];</span>
<span class="k">if</span><span class="p">(</span>activeMod.tools.<span class="f">includes</span><span class="p">(</span><span class="s">'WEB_SEARCH'</span><span class="p">)</span> <span class="p">||</span>
   activeMod.tools.<span class="f">includes</span><span class="p">(</span><span class="s">'WEATHER_FETCH'</span><span class="p">)){</span>
  toolList.<span class="f">push</span><span class="p">({</span> <span class="a">type</span><span class="p">:</span> <span class="s">'web_search_20250305'</span><span class="p">,</span> <span class="a">name</span><span class="p">:</span> <span class="s">'web_search'</span> <span class="p">});</span>
<span class="p">}</span>

<span class="k">const</span> body <span class="p">= {</span>
  <span class="a">model</span><span class="p">:</span>      <span class="s">'claude-sonnet-4-20250514'</span><span class="p">,</span>
  <span class="a">max_tokens</span><span class="p">:</span> <span class="n">2048</span><span class="p">,</span>
  <span class="a">system</span><span class="p">:</span>     <span class="f">buildSystemPrompt</span><span class="p">(),</span>   <span class="c">// module domain prompt + live context</span>
  <span class="a">messages</span><span class="p">:</span>   history               <span class="c">// full conversation turns</span>
<span class="p">};</span>
<span class="k">if</span><span class="p">(</span>toolList.length <span class="p">&gt;</span> <span class="n">0</span><span class="p">)</span> body.tools <span class="p">=</span> toolList<span class="p">;</span>  <span class="c">// only include if non-empty</span></pre>
  </div>
</section>

<!-- 12 TOOL LOOP -->
<section class="doc-section" id="tool-loop">
  <div class="section-anchor"><span class="section-num">12</span><span class="section-tag tag-api">API</span></div>
  <h2>Tool-Use Loop — Two-Call Pattern</h2>
  <p>When the model decides to call a tool (e.g., to fetch a live METAR), the API returns <code>stop_reason: "tool_use"</code> instead of <code>"end_turn"</code>. The application handles this with a second API call: it injects the tool results into history as a <code>user</code> turn, then the model produces its final answer grounded in that live data.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 1119&#x2013;1173</span></div>
    <pre class="code"><span class="k">if</span><span class="p">(</span>data.stop_reason <span class="p">===</span> <span class="s">'tool_use'</span><span class="p">){</span>

  <span class="c">// 1. Collect all tool_use blocks (there may be multiple search calls)</span>
  <span class="k">const</span> toolUses <span class="p">=</span> data.content.<span class="f">filter</span><span class="p">(</span>b <span class="p">=></span> b.type <span class="p">===</span> <span class="s">'tool_use'</span><span class="p">);</span>

  <span class="c">// 2. Build tool_result blocks — one per tool_use, matched by id</span>
  <span class="k">const</span> toolResults <span class="p">=</span> <span class="p">[];</span>
  <span class="k">for</span><span class="p">(</span><span class="k">const</span> tu <span class="k">of</span> toolUses<span class="p">){</span>
    toolResults.<span class="f">push</span><span class="p">({</span>
      <span class="a">type</span><span class="p">:</span>        <span class="s">'tool_result'</span><span class="p">,</span>
      <span class="a">tool_use_id</span><span class="p">:</span> tu.id<span class="p">,</span>      <span class="c">// must match the id field from the tool_use block</span>
      <span class="a">content</span><span class="p">:</span>    resultText   <span class="c">// the search result string</span>
    <span class="p">});</span>
  <span class="p">}</span>

  <span class="c">// 3. Append assistant's tool_use turn to history (required by the API)</span>
  history.<span class="f">push</span><span class="p">({</span> <span class="a">role</span><span class="p">:</span> <span class="s">'assistant'</span><span class="p">,</span> <span class="a">content</span><span class="p">:</span> data.content <span class="p">});</span>

  <span class="c">// 4. Append tool results as a user turn</span>
  history.<span class="f">push</span><span class="p">({</span> <span class="a">role</span><span class="p">:</span> <span class="s">'user'</span><span class="p">,</span> <span class="a">content</span><span class="p">:</span> toolResults <span class="p">});</span>

  <span class="c">// 5. Second fetch — model now sees the search results and generates its answer</span>
  <span class="k">const</span> resp2  <span class="p">=</span> <span class="k">await</span> <span class="f">fetch</span><span class="p">(</span><span class="s">'https://api.anthropic.com/v1/messages'</span><span class="p">, { ... });</span>
  <span class="k">const</span> data2  <span class="p">=</span> <span class="k">await</span> resp2.<span class="f">json</span><span class="p">();</span>
  replyText    <span class="p">=</span> data2.content.<span class="f">filter</span><span class="p">(</span>b <span class="p">=></span> b.type <span class="p">===</span> <span class="s">'text'</span><span class="p">)</span>
                              .<span class="f">map</span><span class="p">(</span>b <span class="p">=></span> b.text<span class="p">)</span>
                              .<span class="f">join</span><span class="p">(</span><span class="s">''</span><span class="p">);</span>
<span class="p">}</span></pre>
  </div>

  <div class="callout tip">
    <span class="icon">&#x2713;</span>
    <span>The purple tool-call cards displayed in the chat (🔧 icon, query text, result preview) are built from the <code>toolCallsDisplay</code> array assembled in this same block, then passed to <code>addAI()</code> as its second argument, rendered above the final response bubble.</span>
  </div>
</section>

<!-- 13 SYSTEM PROMPT -->
<section class="doc-section" id="sys-prompt">
  <div class="section-anchor"><span class="section-num">13</span><span class="section-tag tag-api">API</span></div>
  <h2>buildSystemPrompt() — Runtime Context Injection</h2>
  <p><code>buildSystemPrompt()</code> (lines 1205–1241) is called on every API dispatch. It combines the active module's static domain expertise block with a live operational context footer — current UTC timestamp, station ICAO, module name, and conditional tool usage instructions.</p>

  <div class="code-wrap">
    <div class="code-label"><span class="file">aviation-agent.html</span><span class="lang">JS &middot; lines 1205&#x2013;1241</span></div>
    <pre class="code"><span class="k">function</span> <span class="f">buildSystemPrompt</span><span class="p">(){</span>
  <span class="k">const</span> utc  <span class="p">=</span> <span class="k">new</span> <span class="f">Date</span><span class="p">().</span><span class="f">toUTCString</span><span class="p">();</span>
  <span class="k">const</span> base <span class="p">=</span> activeMod.systemPrompt<span class="p">;</span>   <span class="c">// 500–800 token domain block from MODS</span>

  <span class="k">return</span> <span class="s">`${base}

---
CURRENT OPERATIONAL CONTEXT:
- Station: MROC / SJO (Juan Santamaría International Airport, Costa Rica)
- UTC Date/Time: ${utc}                   &lt;-- live timestamp, rebuilt on every call
- Active module: ${activeMod.name} — ${activeMod.title}
- Agent version: AeroAgent v2.0 Expert Ops Edition

TOOL USAGE INSTRUCTIONS:
${activeMod.tools.includes('WEB_SEARCH') || activeMod.tools.includes('WEATHER_FETCH')
    ? 'You have access to web_search. Use it proactively when:\n' +
      '- User asks for live NOTAMs, METARs, TAFs, SIGMETs\n' +
      '- Search tip for METARs: "site:aviationweather.gov METAR [ICAO]"\n' +
      '- Always cite your sources'
    : 'No live web search for this module. Answer from expert knowledge.'
}

RESPONSE STANDARDS:
- Correct ICAO/IATA terminology and unit systems
- Flag critical items with &#x26A0;&#xFE0F; WARNING or &#x1F534; CRITICAL prefixes
- Use GREEN / AMBER / RED for go/no-go items`</span><span class="p">;</span>
<span class="p">}</span></pre>
  </div>

  <p>The conditional tool instructions block is key: modules without <code>WEB_SEARCH</code> in their tool list receive the instruction to answer from expert knowledge only — preventing the model from hallucinating search results for a tool it hasn't been given.</p>

  <div class="callout info">
    <span class="icon">&#x2605;</span>
    <span><strong>Why rebuild on every call?</strong> The UTC timestamp is live. If an operator's session spans a significant time window, the model's temporal context stays accurate. Rebuilding per-call is cheap — the string is small — and avoids stale context that could affect time-sensitive aviation decisions like NOTAM validity windows or shift handovers.</span>
  </div>
</section>

</div>

<footer class="doc-footer">
  <span>AeroAgent v2 &mdash; aviation-agent.html</span>
  <span>YC Startup School 2026 &middot; MROC/SJO</span>
</footer>

</main>
</div>
</body>
</html>

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#24362a">
  <meta name="description" content="EverOwn is a calm workspace for organizing ownership information.">
  <title>EverOwn — Ownership, made clear</title>

  <style>
    :root {
      --ink: #172219;
      --ink-soft: #415047;
      --paper: #f8f5ed;
      --paper-2: #eee9dc;
      --card: #fffdf7;
      --sage: #78917a;
      --sage-deep: #24362a;
      --sage-pale: #e1eade;
      --brass: #a47a32;
      --brass-pale: #f4e6c6;
      --line: #d7d1c1;
      --danger: #a33c34;
      --danger-pale: #f8e2df;
      --success: #356b42;
      --shadow: 0 18px 44px rgba(28, 39, 29, 0.12);
      --radius: 20px;
      --radius-small: 13px;
      --sans: ui-sans-serif, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      --serif: ui-serif, Georgia, Cambria, "Times New Roman", serif;
    }

    * {
      box-sizing: border-box;
    }

    html {
      background: var(--paper);
      scroll-behavior: smooth;
    }

    body {
      min-width: 320px;
      margin: 0;
      color: var(--ink);
      background:
        radial-gradient(circle at 92% 0%, rgba(164, 122, 50, 0.14), transparent 28rem),
        radial-gradient(circle at 4% 30%, rgba(120, 145, 122, 0.11), transparent 25rem),
        var(--paper);
      font-family: var(--serif);
    }

    button,
    input,
    textarea {
      font: inherit;
    }

    button,
    a {
      -webkit-tap-highlight-color: transparent;
    }

    button {
      cursor: pointer;
    }

    a {
      color: inherit;
      text-decoration: none;
    }

    :focus-visible {
      outline: 3px solid rgba(164, 122, 50, 0.65);
      outline-offset: 3px;
    }

    .shell {
      width: min(1160px, calc(100% - 28px));
      margin: 0 auto;
      padding: 16px 0 42px;
    }

    .topbar {
      position: relative;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      padding: 6px 0 18px;
      border-bottom: 1px solid var(--line);
    }

    .brand {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      min-width: 0;
      font-size: 1.1rem;
      font-weight: 700;
      letter-spacing: 0.01em;
    }

    .brand-mark {
      display: grid;
      width: 34px;
      height: 34px;
      flex: 0 0 auto;
      place-items: center;
      color: #fffdf7;
      background: var(--sage-deep);
      border-radius: 50% 50% 50% 10%;
      box-shadow: inset 0 -4px 0 rgba(0, 0, 0, 0.12);
      font-family: var(--sans);
      font-weight: 800;
    }

    .nav-toggle {
      display: none;
      padding: 9px 12px;
      color: var(--ink);
      background: var(--card);
      border: 1px solid var(--line);
      border-radius: 10px;
      font-family: var(--sans);
      font-size: 0.88rem;
      font-weight: 700;
    }

    .nav {
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .nav a {
      padding: 9px 11px;
      color: var(--ink-soft);
      border-radius: 9px;
      font-family: var(--sans);
      font-size: 0.86rem;
      font-weight: 650;
      white-space: nowrap;
    }

    .nav a:hover,
    .nav a.active {
      color: var(--ink);
      background: var(--sage-pale);
    }

    .hero {
      display: grid;
      grid-template-columns: minmax(0, 1.12fr) minmax(290px, 0.88fr);
      gap: 28px;
      align-items: stretch;
      padding: 50px 0 28px;
    }

    .eyebrow {
      margin: 0 0 12px;
      color: var(--brass);
      font-family: var(--sans);
      font-size: 0.74rem;
      font-weight: 800;
      letter-spacing: 0.13em;
      text-transform: uppercase;
    }

    h1,
    h2,
    h3,
    p {
      margin-top: 0;
    }

    h1 {
      max-width: 10ch;
      margin-bottom: 18px;
      font-size: clamp(3rem, 8vw, 5.9rem);
      font-weight: 500;
      letter-spacing: -0.06em;
      line-height: 0.92;
    }

    .hero-copy {
      max-width: 55ch;
      margin-bottom: 22px;
      color: var(--ink-soft);
      font-size: 1.1rem;
      line-height: 1.65;
    }

    .hero-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    .button {
      display: inline-flex;
      min-height: 45px;
      align-items: center;
      justify-content: center;
      padding: 11px 16px;
      border: 1px solid transparent;
      border-radius: 11px;
      font-family: var(--sans);
      font-size: 0.9rem;
      font-weight: 750;
      transition: transform 160ms ease, background 160ms ease;
    }

    .button:hover {
      transform: translateY(-1px);
    }

    .button-primary {
      color: #fffdf7;
      background: var(--sage-deep);
    }

    .button-secondary {
      color: var(--ink);
      background: transparent;
      border-color: var(--line);
    }

    .assistant-card {
      display: flex;
      min-height: 326px;
      flex-direction: column;
      justify-content: space-between;
      padding: 25px;
      color: #fffdf7;
      background:
        radial-gradient(circle at 88% 16%, rgba(245, 214, 149, 0.2), transparent 10rem),
        linear-gradient(145deg, #3d5841, #203124);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
    }

    .availability {
      display: inline-flex;
      width: fit-content;
      align-items: center;
      gap: 8px;
      padding: 7px 10px;
      background: rgba(255, 255, 255, 0.1);
      border: 1px solid rgba(255, 255, 255, 0.18);
      border-radius: 999px;
      color: #fff2d3;
      font-family: var(--sans);
      font-size: 0.76rem;
      font-weight: 700;
    }

    .availability-dot {
      width: 7px;
      height: 7px;
      background: #e3be66;
      border-radius: 50%;
    }

    .assistant-card h2 {
      margin: 18px 0 10px;
      font-size: 1.8rem;
      font-weight: 500;
      letter-spacing: -0.03em;
    }

    .assistant-card p {
      max-width: 38ch;
      margin-bottom: 0;
      color: rgba(255, 253, 247, 0.85);
      font-family: var(--sans);
      font-size: 0.92rem;
      line-height: 1.6;
    }

    .assistant-card .small-note {
      padding-top: 20px;
      border-top: 1px solid rgba(255, 255, 255, 0.14);
      color: rgba(255, 253, 247, 0.7);
      font-size: 0.79rem;
    }

    .trust-banner {
      display: grid;
      grid-template-columns: auto 1fr;
      gap: 13px;
      margin: 8px 0 34px;
      padding: 17px;
      background: #fff9ed;
      border: 1px solid #e5d1a7;
      border-radius: var(--radius-small);
    }

    .trust-icon {
      display: grid;
      width: 28px;
      height: 28px;
      place-items: center;
      color: #654b17;
      background: var(--brass-pale);
      border-radius: 50%;
      font-family: var(--sans);
      font-size: 0.9rem;
      font-weight: 900;
    }

    .trust-banner h2 {
      margin-bottom: 5px;
      font-size: 1.02rem;
      font-weight: 650;
    }

    .trust-banner p {
      margin-bottom: 0;
      color: #62583e;
      font-family: var(--sans);
      font-size: 0.89rem;
      line-height: 1.55;
    }

    .section-head {
      display: flex;
      align-items: end;
      justify-content: space-between;
      gap: 16px;
      margin: 0 0 15px;
    }

    .section-head h2 {
      margin: 0;
      font-size: clamp(1.65rem, 4vw, 2.15rem);
      font-weight: 500;
      letter-spacing: -0.04em;
    }

    .section-head p {
      max-width: 45ch;
      margin: 0;
      color: var(--ink-soft);
      font-family: var(--sans);
      font-size: 0.87rem;
      line-height: 1.5;
      text-align: right;
    }

    .workspace-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 15px;
    }

    .workspace-card {
      display: flex;
      min-height: 206px;
      flex-direction: column;
      padding: 21px;
      background: rgba(255, 253, 247, 0.82);
      border: 1px solid var(--line);
      border-radius: var(--radius-small);
      transition: border-color 160ms ease, transform 160ms ease;
    }

    .workspace-card:hover {
      border-color: var(--sage);
      transform: translateY(-2px);
    }

    .card-number {
      display: grid;
      width: 29px;
      height: 29px;
      margin-bottom: 18px;
      place-items: center;
      color: var(--sage-deep);
      background: var(--sage-pale);
      border-radius: 50%;
      font-family: var(--sans);
      font-size: 0.76rem;
      font-weight: 800;
    }

    .workspace-card h3 {
      margin-bottom: 9px;
      font-size: 1.2rem;
      font-weight: 600;
    }

    .workspace-card p {
      margin-bottom: 17px;
      color: var(--ink-soft);
      font-family: var(--sans);
      font-size: 0.9rem;
      line-height: 1.55;
    }

    .card-link {
      margin-top: auto;
      color: var(--sage-deep);
      font-family: var(--sans);
      font-size: 0.86rem;
      font-weight: 800;
    }

    .asset-section {
      margin-top: 40px;
      scroll-margin-top: 18px;
    }

    .asset-layout {
      display: grid;
      grid-template-columns: minmax(0, 0.85fr) minmax(0, 1.15fr);
      gap: 17px;
    }

    .asset-form,
    .asset-list-panel {
      padding: 22px;
      background: var(--card);
      border: 1px solid var(--line);
      border-radius: var(--radius);
    }

    .asset-form h3,
    .asset-list-panel h3 {
      margin-bottom: 7px;
      font-size: 1.32rem;
      font-weight: 550;
      letter-spacing: -0.025em;
    }

    .panel-intro {
      margin-bottom: 18px;
      color: var(--ink-soft);
      font-family: var(--sans);
      font-size: 0.88rem;
      line-height: 1.55;
    }

    .field {
      display: grid;
      gap: 7px;
      margin-bottom: 13px;
    }

    .field label {
      color: var(--ink);
      font-family: var(--sans);
      font-size: 0.84rem;
      font-weight: 750;
    }

    .field input,
    .field textarea {
      width: 100%;
      padding: 11px 12px;
      color: var(--ink);
      background: #fffefa;
      border: 1px solid var(--line);
      border-radius: 10px;
      font-family: var(--sans);
      font-size: 0.94rem;
    }

    .field textarea {
      min-height: 85px;
      resize: vertical;
    }

    .field input:focus,
    .field textarea:focus {
      border-color: var(--sage);
      outline: 3px solid rgba(120, 145, 122, 0.18);
    }

    .form-note {
      margin: 12px 0 0;
      color: var(--ink-soft);
      font-family: var(--sans);
      font-size: 0.78rem;
      line-height: 1.5;
    }

    .form-message {
      min-height: 22px;
      margin: 11px 0 0;
      color: var(--success);
      font-family: var(--sans);
      font-size: 0.84rem;
      font-weight: 700;
      line-height: 1.45;
    }

    .form-message.error {
      color: var(--danger);
    }

    .empty-state {
      display: grid;
      min-height: 210px;
      place-items: center;
      padding: 25px;
      color: var(--ink-soft);
      text-align: center;
    }

    .empty-state p {
      max-width: 35ch;
      margin: 0;
      font-family: var(--sans);
      font-size: 0.91rem;
      line-height: 1.6;
    }

    .asset-list {
      display: grid;
      gap: 10px;
    }

    .asset-item {
      display: flex;
      align-items: flex-start;
      justify-content: space-between;
      gap: 14px;
      padding: 14px;
      background: #faf8f1;
      border: 1px solid var(--line);
      border-radius: 11px;
    }

    .asset-item h4 {
      margin: 0 0 4px;
      font-family: var(--sans);
      font-size: 0.96rem;
    }

    .asset-item p {
      margin: 0;
      color: var(--ink-soft);
      font-family: var(--sans);
      font-size: 0.8rem;
      line-height: 1.45;
    }

    .asset-status {
      display: inline-flex;
      flex: 0 0 auto;
      padding: 5px 7px;
      color: #665028;
      background: var(--brass-pale);
      border-radius: 999px;
      font-family: var(--sans);
      font-size: 0.7rem;
      font-weight: 800;
      white-space: nowrap;
    }

    .vault-section,
    .graph-section,
    .assistant-section {
      margin-top: 40px;
      scroll-margin-top: 18px;
    }

    .unavailable-card {
      display: grid;
      grid-template-columns: minmax(0, 1fr) auto;
      gap: 22px;
      align-items: center;
      padding: 27px;
      color: #fffdf7;
      background: var(--sage-deep);
      border-radius: var(--radius);
    }

    .unavailable-card h2 {
      margin-bottom: 9px;
      font-size: 1.7rem;
      font-weight: 500;
    }

    .unavailable-card p {
      max-width: 58ch;
      margin-bottom: 0;
      color: rgba(255, 253, 247, 0.82);
      font-family: var(--sans);
      font-size: 0.92rem;
      line-height: 1.6;
    }

    .unavailable-label {
      padding: 9px 11px;
      color: #fff2d3;
      background: rgba(255, 255, 255, 0.11);
      border: 1px solid rgba(255, 255, 255, 0.17);
      border-radius: 999px;
      font-family: var(--sans);
      font-size: 0.76rem;
      font-weight: 800;
      white-space: nowrap;
    }

    .footer {
      margin-top: 46px;
      padding: 18px 0 0;
      color: var(--ink-soft);
      border-top: 1px solid var(--line);
      font-family: var(--sans);
      font-size: 0.8rem;
      line-height: 1.5;
    }

    @media (max-width: 780px) {
      .shell {
        width: min(100% - 22px, 1160px);
        padding-top: 10px;
      }

      .topbar {
        padding-bottom: 12px;
      }

      .nav-toggle {
        display: block;
      }

      .nav {
        position: absolute;
        z-index: 10;
        top: 58px;
        right: 0;
        left: 0;
        display: none;
        flex-direction: column;
        align-items: stretch;
        padding: 9px;
        background: var(--card);
        border: 1px solid var(--line);
        border-radius: var(--radius-small);
        box-shadow: var(--shadow);
      }

      .nav.open {
        display: flex;
      }

      .nav a {
        padding: 12px;
      }

      .hero {
        grid-template-columns: 1fr;
        gap: 18px;
        padding-top: 38px;
      }

      h1 {
        max-width: 12ch;
      }

      .assistant-card {
        min-height: 276px;
      }

      .section-head {
        display: block;
      }

      .section-head p {
        margin-top: 8px;
        text-align: left;
      }

      .workspace-grid,
      .asset-layout {
        grid-template-columns: 1fr;
      }

      .unavailable-card {
        grid-template-columns: 1fr;
        gap: 15px;
      }

      .unavailable-label {
        width: fit-content;
      }
    }
  </style>
</head>

<body>
  <div class="shell">
    <header class="topbar">
      <a class="brand" href="#home" aria-label="EverOwn home">
        <span class="brand-mark" aria-hidden="true">E</span>
        <span>EverOwn</span>
      </a>

      <button
        class="nav-toggle"
        id="nav-toggle"
        type="button"
        aria-controls="main-navigation"
        aria-expanded="false"
      >
        Menu
      </button>

      <nav class="nav" id="main-navigation" aria-label="Main navigation">
        <a class="active" href="#home">Home</a>
        <a href="#assets">Assets</a>
        <a href="#vault">Vault</a>
        <a href="#ownership-graph">Ownership Graph</a>
        <a href="#ever-assistant">Ever Assistant</a>
      </nav>
    </header>

    <main id="home">
      <section class="hero" aria-labelledby="page-title">
        <div>
          <p class="eyebrow">A quieter way to organize</p>
          <h1 id="page-title">Keep ownership clear.</h1>
          <p class="hero-copy">
            EverOwn is a preview workspace for organizing ownership information
            with care, context, and a clear boundary between what is displayed
            in this browser and what has been verified and stored.
          </p>

          <div class="hero-actions">
            <a class="button button-primary" href="#assets">Explore assets</a>
            <a class="button button-secondary" href="#vault">View availability</a>
          </div>
        </div>

        <aside class="assistant-card" aria-labelledby="assistant-card-heading">
          <div>
            <span class="availability">
              <span class="availability-dot" aria-hidden="true"></span>
              Preview availability
            </span>
            <h2 id="assistant-card-heading">Ever Assistant</h2>
            <p>
              Ever Assistant is not available in this preview. It will remain
              unavailable until verified record retrieval and grounded responses
              are available.
            </p>
          </div>

          <p class="small-note">
            This page does not present generated guidance as verified ownership,
            legal, financial, or document information.
          </p>
        </aside>
      </section>

      <aside class="trust-banner" aria-labelledby="trust-heading">
        <div class="trust-icon" aria-hidden="true">i</div>
        <div>
          <h2 id="trust-heading">Preview boundary</h2>
          <p>
            Entries created on this page are saved only in this browser session
            while the page remains open. They are not server-persisted records,
            verified ownership records, or proof of ownership.
          </p>
        </div>
      </aside>

      <section aria-labelledby="workspace-heading">
        <div class="section-head">
          <h2 id="workspace-heading">Your workspace</h2>
          <p>Choose a space to review the preview experience and its current availability.</p>
        </div>

        <div class="workspace-grid">
          <a class="workspace-card" href="#assets">
            <span class="card-number" aria-hidden="true">01</span>
            <h3>Assets</h3>
            <p>Draft an item for this browser session and review its clearly marked preview status.</p>
            <span class="card-link">Open assets →</span>
          </a>

          <a class="workspace-card" href="#vault">
            <span class="card-number" aria-hidden="true">02</span>
            <h3>Vault</h3>
            <p>See the availability boundary for documents and supporting material.</p>
            <span class="card-link">Open vault →</span>
          </a>

          <a class="workspace-card" href="#ownership-graph">
            <span class="card-number" aria-hidden="true">03</span>
            <h3>Ownership Graph</h3>
            <p>See how relationship views will be introduced only with verified records.</p>
            <span class="card-link">Open ownership graph →</span>
          </a>
        </div>
      </section>

      <section class="asset-section" id="assets" aria-labelledby="assets-heading">
        <div class="section-head">
          <h2 id="assets-heading">Assets</h2>
          <p>Create a browser-session draft. This action does not save information to an EverOwn server.</p>
        </div>

        <div class="asset-layout">
          <form class="asset-form" id="asset-form" novalidate>
            <h3>Create a preview draft</h3>
            <p class="panel-intro">
              Use general, non-sensitive example information. This preview has
              no verified storage connection.
            </p>

            <div class="field">
              <label for="asset-name">Asset name</label>
              <input id="asset-name" name="asset-name" type="text" maxlength="80" placeholder="Example: Family vehicle" autocomplete="off">
            </div>

            <div class="field">
              <label for="asset-note">Optional note</label>
              <textarea id="asset-note" name="asset-note" maxlength="240" placeholder="A short, non-sensitive note for this browser-session draft."></textarea>
            </div>

            <button class="button button-primary" type="submit">Add preview draft</button>

            <p class="form-note">
              Do not enter account numbers, identity documents, passwords, legal documents, or other sensitive personal information.
            </p>

            <p class="form-message" id="form-message" role="status" aria-live="polite"></p>
          </form>

          <section class="asset-list-panel" aria-labelledby="draft-list-heading">
            <h3 id="draft-list-heading">Browser-session drafts</h3>
            <p class="panel-intro">
              These entries exist only while this page remains open in this browser.
            </p>

            <div class="empty-state" id="empty-state">
              <p>
                No browser-session drafts have been added. Add a non-sensitive
                example above to see how preview entries are labeled.
              </p>
            </div>

            <div class="asset-list" id="asset-list" aria-live="polite"></div>
          </section>
        </div>
      </section>

      <section class="vault-section" id="vault" aria-labelledby="vault-heading">
        <div class="unavailable-card">
          <div>
            <h2 id="vault-heading">Vault is unavailable in this preview</h2>
            <p>
              File uploads, document storage, and document retrieval are not
              enabled. Do not treat this preview as a document vault or upload
              sensitive materials here.
            </p>
          </div>
          <span class="unavailable-label">Unavailable</span>
        </div>
      </section>

      <section class="graph-section" id="ownership-graph" aria-labelledby="graph-heading">
        <div class="unavailable-card">
          <div>
            <h2 id="graph-heading">Ownership Graph is unavailable in this preview</h2>
            <p>
              Relationship views require verified, server-persisted records.
              This preview does not infer, confirm, or display ownership
              relationships.
            </p>
          </div>
          <span class="unavailable-label">Unavailable</span>
        </div>
      </section>

      <section class="assistant-section" id="ever-assistant" aria-labelledby="ever-assistant-heading">
        <div class="unavailable-card">
          <div>
            <h2 id="ever-assistant-heading">Ever Assistant is unavailable in this preview</h2>
            <p>
              Ever Assistant will be enabled only after it can retrieve verified
              records and provide grounded, traceable responses. No assistant
              conclusions are generated on this page.
            </p>
          </div>
          <span class="unavailable-label">Unavailable</span>
        </div>
      </section>
    </main>

    <footer class="footer">
      EverOwn preview experience. Browser-session drafts are not verified or server-persisted records.
    </footer>
  </div>

  <script>
    (() => {
      const navToggle = document.getElementById("nav-toggle");
      const nav = document.getElementById("main-navigation");
      const form = document.getElementById("asset-form");
      const assetName = document.getElementById("asset-name");
      const assetNote = document.getElementById("asset-note");
      const assetList = document.getElementById("asset-list");
      const emptyState = document.getElementById("empty-state");
      const formMessage = document.getElementById("form-message");

      const drafts = [];

      navToggle.addEventListener("click", () => {
        const isOpen = nav.classList.toggle("open");
        navToggle.setAttribute("aria-expanded", String(isOpen));
        navToggle.textContent = isOpen ? "Close" : "Menu";
      });

      nav.querySelectorAll("a").forEach((link) => {
        link.addEventListener("click", () => {
          nav.classList.remove("open");
          navToggle.setAttribute("aria-expanded", "false");
          navToggle.textContent = "Menu";
        });
      });

      function renderDrafts() {
        assetList.innerHTML = "";

        if (drafts.length === 0) {
          emptyState.hidden = false;
          return;
        }

        emptyState.hidden = true;

        drafts.forEach((draft) => {
          const item = document.createElement("article");
          item.className = "asset-item";

          const text = document.createElement("div");
          const title = document.createElement("h4");
          const note = document.createElement("p");
          const status = document.createElement("span");

          title.textContent = draft.name;
          note.textContent = draft.note || "No note added.";
          status.className = "asset-status";
          status.textContent = "Preview draft";

          text.appendChild(title);
          text.appendChild(note);
          item.appendChild(text);
          item.appendChild(status);
          assetList.appendChild(item);
        });
      }

      form.addEventListener("submit", (event) => {
        event.preventDefault();

        const name = assetName.value.trim();
        const note = assetNote.value.trim();

        formMessage.classList.remove("error");

        if (!name) {
          formMessage.textContent = "Enter an asset name before adding a preview draft.";
          formMessage.classList.add("error");
          assetName.focus();
          return;
        }

        drafts.unshift({ name, note });
        renderDrafts();

        form.reset();
        formMessage.textContent =
          "Preview draft added for this browser session only. It has not been saved to an EverOwn server.";
      });

      renderDrafts();
    })();
  </script>
</body>
</html>


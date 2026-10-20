
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="color-scheme" content="light dark">
  <title>ANAMNESIS · READ</title>

  <script>
    (function () {
      try {
        const t = localStorage.getItem('anamnesis_theme');
        if (t === 'light' || t === 'dark') {
          document.documentElement.setAttribute('data-theme', t);
        }
      } catch (e) {}
    })();
  </script>

  <style>
    :root {
      color-scheme: light;
      --ivory: #EDEAE4;
      --paper: #E3DFD7;
      --ink: #2B2A28;
      --muted: #6E6B66;
      --line: #B9B4AC;
      --board: #9C968C;
    }

    :root[data-theme="dark"] {
      color-scheme: dark;
      --ivory: #171615;
      --paper: #232120;
      --ink: #EDEAE4;
      --muted: #A39D94;
      --line: #4A4744;
      --board: #5A554F;
    }

    @media (prefers-color-scheme: dark) {
      :root:not([data-theme="light"]):not([data-theme="dark"]) {
        color-scheme: dark;
        --ivory: #171615;
        --paper: #232120;
        --ink: #EDEAE4;
        --muted: #A39D94;
        --line: #4A4744;
        --board: #5A554F;
      }
    }

    * {
      box-sizing: border-box;
    }

    html {
      min-height: 100%;
      scroll-padding-top: env(safe-area-inset-top, 0px);
    }

    body {
      margin: 0;
      min-height: 100vh;
      padding-top: env(safe-area-inset-top, 0px);
      padding-bottom: env(safe-area-inset-bottom, 0px);
      background: var(--ivory);
      color: var(--ink);
      font-family: Georgia, "Nanum Myeongjo", serif;
      transition: background .2s, color .2s;
    }

    button, input, textarea {
      font: inherit;
    }

    .wrap {
      max-width: 640px;
      margin: 0 auto;
      padding: 2.2rem 1.4rem 4rem;
    }

    .topbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 1rem;
      margin-bottom: 2.2rem;
    }

    .kicker {
      font-family: Arial, sans-serif;
      font-size: .7rem;
      letter-spacing: .25em;
      color: var(--muted);
    }

    .theme {
      flex-shrink: 0;
      font-family: Arial, sans-serif;
      font-size: .66rem;
      letter-spacing: .06em;
      background: transparent;
      border: 1px solid var(--line);
      color: var(--muted);
      padding: .5rem .7rem;
      cursor: pointer;
      border-radius: 2px;
    }

    h1 {
      font-family: Arial, sans-serif;
      font-size: 1.9rem;
      margin: 0 0 .4rem;
      letter-spacing: .02em;
    }

    .sub {
      font-size: .9rem;
      color: var(--muted);
      font-style: italic;
      margin: 1rem 0 1.8rem;
    }

    .card {
      background: var(--paper);
      padding: 1.3rem;
      margin-bottom: 2rem;
      border-radius: 2px;
    }

    label {
      display: block;
      font-family: Arial, sans-serif;
      font-size: .7rem;
      letter-spacing: .08em;
      color: var(--muted);
      margin-bottom: .4rem;
    }

    input[type="text"], textarea {
      display: block;
      width: 100%;
      border: 0;
      border-bottom: 1px solid var(--line);
      background: transparent;
      font-family: inherit;
      font-size: .95rem;
      color: var(--ink);
      padding: .5rem 0;
      margin-bottom: 1.3rem;
      border-radius: 0;
    }

    textarea {
      resize: vertical;
      line-height: 1.6;
    }

    input:focus, textarea:focus {
      outline: none;
      border-bottom-color: var(--ink);
    }

    button.act {
      font-family: Arial, sans-serif;
      font-size: .78rem;
      letter-spacing: .06em;
      padding: .75rem 1.3rem;
      background: var(--ink);
      color: var(--ivory);
      border: 0;
      cursor: pointer;
      border-radius: 2px;
    }

    button:focus-visible {
      outline: 2px solid var(--muted);
      outline-offset: 3px;
    }

    .status {
      display: inline-block;
      font-family: Arial, sans-serif;
      font-size: .72rem;
      color: var(--muted);
      margin: .7rem 0 0;
    }

    .section-label {
      font-family: Arial, sans-serif;
      font-size: .7rem;
      letter-spacing: .1em;
      color: var(--muted);
      margin: 1.8rem 0 .8rem;
    }

    .shelf-row {
      display: flex;
      align-items: flex-end;
      gap: 3px;
      min-height: 205px;
      padding: 0 6px;
      border-bottom: 9px solid var(--board);
      margin-bottom: 12px;
      overflow-x: auto;
    }

    .spine {
      flex: 0 0 auto;
      border: none;
      cursor: pointer;
      color: #EDEAE4;
      padding: 10px 0;
      writing-mode: vertical-rl;
      text-orientation: mixed;
      overflow: hidden;
      font-family: inherit;
      font-size: .8rem;
      letter-spacing: .08em;
      line-height: 1;
      text-align: start;
      border-radius: 2px 2px 0 0;
      box-shadow:
        inset 0 7px 0 rgba(255,255,255,.12),
        inset 0 -7px 0 rgba(0,0,0,.22);
      transition: transform .15s ease;
    }

    .spine span {
      display: block;
      max-height: 100%;
      overflow: hidden;
      white-space: nowrap;
    }

    .spine:hover, .spine.sel {
      transform: translateY(-8px);
    }

    .shelf-empty {
      font-family: Arial, sans-serif;
      font-size: .78rem;
      color: var(--muted);
      padding: .5rem 0 1rem;
    }

    .detail {
      margin-top: .4rem;
    }

    .detail h3 {
      font-size: 1rem;
      margin: 0 0 .6rem;
      font-weight: 700;
    }

    .entry {
      border-top: 1px solid var(--line);
      padding: .9rem 0;
    }

    .entry .meta {
      font-family: Arial, sans-serif;
      font-size: .68rem;
      letter-spacing: .05em;
      color: var(--muted);
      margin-bottom: .4rem;
    }

    .entry .body {
      font-size: .92rem;
      line-height: 1.7;
      white-space: pre-wrap;
      overflow-wrap: anywhere;
    }
  </style>
</head>

<body>
  <main class="wrap">
    <header class="topbar">
      <div class="kicker">ANAMNESIS</div>
      <button class="theme" id="themeBtn" type="button">
        AUTO · 기기 설정
      </button>
    </header>

    <h1>READ</h1>
    <p class="sub">읽은 책이 책장에 꽂힌다</p>

    <section class="card" aria-label="독서 기록 입력">
      <label for="bookTitle">책 제목</label>
      <input
        id="bookTitle"
        type="text"
        placeholder="예: 잃어버린 시간을 찾아서"
      >

      <label for="readNote">어디까지 읽었는지</label>
      <textarea
        id="readNote"
        rows="3"
        placeholder="예: 1권 콩브레, 마들렌 장면까지"
      ></textarea>

      <button class="act" id="saveRead" type="button">
        책장에 꽂기
      </button>
      <p class="status" id="readStatus" aria-live="polite"></p>
    </section>

    <section aria-label="나의 책장">
      <div class="section-label">나의 책장</div>
      <div id="shelf"></div>
      <div class="detail" id="bookDetail"></div>
    </section>
  </main>

  <script>
    const KEY = 'anamnesis_read_v1';
    const THEME_KEY = 'anamnesis_theme';

    const SPINE_COLORS = [
      '#3B3835', '#4A4540', '#5A5249',
      '#6B5F52', '#2F2D2B', '#54504A', '#463F38'
    ];

    const NO_TITLE = '제목 없음';
    let selectedBook = null;

    function loadEntries() {
      try {
        const raw = localStorage.getItem(KEY);
        const arr = raw ? JSON.parse(raw) : [];
        return Array.isArray(arr) ? arr : [];
      } catch (e) {
        return [];
      }
    }

    function saveEntries(entries) {
      try {
        localStorage.setItem(KEY, JSON.stringify(entries));
        return true;
      } catch (e) {
        return false;
      }
    }

    function hash(str) {
      let h = 0;
      for (let i = 0; i < str.length; i++) {
        h = (h * 31 + str.charCodeAt(i)) >>> 0;
      }
      return h;
    }

    function el(tag, cls, text) {
      const node = document.createElement(tag);
      if (cls) node.className = cls;
      if (text !== undefined) node.textContent = text;
      return node;
    }

    function renderRead() {
      const reads = loadEntries();
      const groups = new Map();

      reads.forEach(entry => {
        const title = (entry.title || '').trim() || NO_TITLE;
        if (!groups.has(title)) groups.set(title, []);
        groups.get(title).push(entry);
      });

      const books = Array.from(groups.entries())
        .map(([title, entries]) => ({
          title,
          entries: entries.sort((a, b) => a.createdAt - b.createdAt)
        }))
        .sort((a, b) => a.entries[0].createdAt - b.entries[0].createdAt);

      const shelf = document.getElementById('shelf');
      shelf.textContent = '';

      if (!books.length) {
        shelf.appendChild(
          el('div', 'shelf-empty', '아직 꽂힌 책이 없어요. 위에서 첫 책을 꽂아보세요.')
        );
      } else {
        const PER_ROW = 6;

        for (let i = 0; i < books.length; i += PER_ROW) {
          const row = el('div', 'shelf-row');

          books.slice(i, i + PER_ROW).forEach(book => {
            const h = hash(book.title);
            const spine = el(
              'button',
              'spine' + (book.title === selectedBook ? ' sel' : '')
            );

            spine.type = 'button';
            spine.style.height = (128 + (h % 5) * 14) + 'px';
            spine.style.width =
              (30 + Math.min(book.entries.length - 1, 4) * 3 + (h % 3) * 3) + 'px';
            spine.style.background = SPINE_COLORS[h % SPINE_COLORS.length];
            spine.title = book.title;
            spine.setAttribute('aria-label', book.title);

            spine.appendChild(el('span', '', book.title));

            spine.addEventListener('click', () => {
              selectedBook = book.title;
              if (book.title !== NO_TITLE) {
                document.getElementById('bookTitle').value = book.title;
              }
              renderRead();
            });

            row.appendChild(spine);
          });

          shelf.appendChild(row);
        }
      }

      const detail = document.getElementById('bookDetail');
      detail.textContent = '';

      const selected = books.find(book => book.title === selectedBook);

      if (selected) {
        detail.appendChild(
          el('h3', '', selected.title + ' — 기록 ' + selected.entries.length + '개')
        );

        selected.entries.slice().reverse().forEach(entry => {
          const box = el('div', 'entry');
          const date = new Date(entry.createdAt);

          box.appendChild(
            el(
              'div',
              'meta',
              (date.getMonth() + 1) + '월 ' +
              date.getDate() + '일 ' +
              String(date.getHours()).padStart(2, '0') + ':' +
              String(date.getMinutes()).padStart(2, '0')
            )
          );

          box.appendChild(el('div', 'body', entry.note || ''));
          detail.appendChild(box);
        });
      }
    }

    document.getElementById('saveRead').addEventListener('click', () => {
      const title = document.getElementById('bookTitle').value.trim();
      const note = document.getElementById('readNote').value.trim();
      const status = document.getElementById('readStatus');

      if (!note) {
        status.textContent = '어디까지 읽었는지 적어주세요.';
        return;
      }

      const entries = loadEntries();
      entries.push({
        title,
        note,
        createdAt: Date.now()
      });

      const ok = saveEntries(entries);
      status.textContent = ok ? '책장에 꽂았어요.' : '저장하지 못했어요.';

      if (ok) {
        document.getElementById('readNote').value = '';
        selectedBook = title || NO_TITLE;
        renderRead();
      }

      setTimeout(() => {
        status.textContent = '';
      }, 2500);
    });

    // AUTO → LIGHT → DARK
    (function () {
      const ORDER = ['auto', 'light', 'dark'];
      const LABEL = {
        auto: 'AUTO · 기기 설정',
        light: 'LIGHT · 밝게',
        dark: 'DARK · 어둡게'
      };

      const btn = document.getElementById('themeBtn');

      function getTheme() {
        try {
          const theme = localStorage.getItem(THEME_KEY);
          return ORDER.includes(theme) ? theme : 'auto';
        } catch (e) {
          return 'auto';
        }
      }

      function applyTheme(theme) {
        const root = document.documentElement;

        if (theme === 'auto') {
          root.removeAttribute('data-theme');
        } else {
          root.setAttribute('data-theme', theme);
        }

        btn.textContent = LABEL[theme];
      }

      btn.addEventListener('click', () => {
        const current = getTheme();
        const next = ORDER[(ORDER.indexOf(current) + 1) % ORDER.length];

        try {
          localStorage.setItem(THEME_KEY, next);
        } catch (e) {}

        applyTheme(next);
      });

      applyTheme(getTheme());
    })();

    renderRead();
  </script>
</body>
</html>

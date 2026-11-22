# Visual-Aid-
visual 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#f5f8ff">
  <title>My Visual Voice</title>
  <style>
    :root {
      color-scheme: light;
      --ink: #17233b;
      --muted: #52617a;
      --blue: #185adb;
      --blue-dark: #1247b2;
      --line: #d7dfed;
      --surface: #fff;
      --page: #f5f8ff;
      --focus: #f2a900;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      background: var(--page);
      color: var(--ink);
      font-size: 1rem;
      line-height: 1.5;
    }

    button, input { font: inherit; }

    button:focus-visible, input:focus-visible {
      outline: 4px solid var(--focus);
      outline-offset: 3px;
    }

    .app {
      width: min(1100px, 100%);
      margin: 0 auto;
      padding: 1rem;
    }

    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 1rem;
      margin-bottom: 1rem;
    }

    h1 {
      margin: 0;
      font-size: clamp(1.7rem, 5vw, 2.4rem);
      line-height: 1.15;
    }

    .subtitle { margin: .35rem 0 0; color: var(--muted); }

    .panel {
      background: var(--surface);
      border: 1px solid var(--line);
      border-radius: 1rem;
      padding: 1rem;
      box-shadow: 0 4px 16px rgb(23 35 59 / 5%);
    }

    .message-panel {
      position: sticky;
      top: .5rem;
      z-index: 2;
      margin-bottom: 1rem;
    }

    .message-label {
      margin: 0 0 .4rem;
      font-size: 1rem;
      font-weight: 750;
    }

    #message {
      min-height: 3.25rem;
      margin: 0 0 .8rem;
      padding: .65rem .8rem;
      border: 2px solid var(--line);
      border-radius: .65rem;
      background: #fbfcff;
      overflow-wrap: anywhere;
      font-size: 1.2rem;
    }

    .actions, .categories {
      display: flex;
      flex-wrap: wrap;
      gap: .6rem;
    }

    .action, .category {
      min-height: 48px;
      padding: .65rem 1rem;
      border: 2px solid var(--line);
      border-radius: .7rem;
      background: #fff;
      color: var(--ink);
      font-weight: 700;
      cursor: pointer;
    }

    .action.primary, .category[aria-pressed="true"] {
      border-color: var(--blue);
      background: var(--blue);
      color: white;
    }

    .action.primary:hover, .category[aria-pressed="true"]:hover {
      background: var(--blue-dark);
    }

    .action:hover, .category:hover { border-color: var(--blue); }

    .categories { margin: 1rem 0; }

    .section-heading {
      margin: 0 0 .75rem;
      font-size: 1.25rem;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
      gap: .75rem;
    }

    .tile {
      display: flex;
      min-height: 130px;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      gap: .25rem;
      padding: .8rem;
      border: 2px solid var(--line);
      border-radius: .9rem;
      background: white;
      color: var(--ink);
      text-align: center;
      cursor: pointer;
      touch-action: manipulation;
    }

    .tile:hover { border-color: var(--blue); background: #f7f9ff; }

    .tile .icon {
      font-size: 2.7rem;
      line-height: 1.15;
    }

    .tile .label {
      font-size: 1.05rem;
      font-weight: 750;
    }

    .custom-form {
      display: flex;
      flex-wrap: wrap;
      gap: .6rem;
      margin-top: 1rem;
    }

    .custom-form input {
      flex: 1 1 220px;
      min-height: 48px;
      padding: .65rem .8rem;
      border: 2px solid var(--line);
      border-radius: .7rem;
    }

    .hint { margin: .7rem 0 0; color: var(--muted); font-size: .95rem; }

    .overlay {
      position: fixed;
      inset: 0;
      z-index: 5;
      display: none;
      align-items: center;
      justify-content: center;
      padding: 1rem;
      background: #101a2b;
      color: white;
      text-align: center;
    }

    .overlay.is-open { display: flex; }

    .display-card {
      width: min(900px, 100%);
    }

    .display-icon {
      display: block;
      margin-bottom: .5rem;
      font-size: clamp(5rem, 24vw, 12rem);
      line-height: 1.1;
    }

    .display-text {
      margin: 0 auto 1.5rem;
      font-size: clamp(2.5rem, 10vw, 6rem);
      font-weight: 800;
      line-height: 1.12;
      overflow-wrap: anywhere;
    }

    .overlay .action {
      margin: .25rem;
      border-color: white;
    }

    .overlay .action.primary { border-color: var(--blue); }

    .sr-only {
      position: absolute;
      width: 1px;
      height: 1px;
      padding: 0;
      margin: -1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
      white-space: nowrap;
      border: 0;
    }

    @media (max-width: 520px) {
      .app { padding: .75rem; }
      .panel { padding: .8rem; }
      .message-panel { top: .25rem; }
      .board { grid-template-columns: repeat(2, minmax(0, 1fr)); }
      .tile { min-height: 118px; }
    }

    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after { scroll-behavior: auto !important; }
    }
  </style>
</head>
<body>
  <main class="app">
    <header>
      <div>
        <h1>My Visual Voice</h1>
        <p class="subtitle">Tap pictures to build a message, then show it.</p>
      </div>
    </header>

    <section class="panel message-panel" aria-labelledby="message-heading">
      <h2 class="message-label" id="message-heading">My message</h2>
      <p id="message" aria-live="polite">Your message will appear here.</p>
      <div class="actions">
        <button class="action primary" id="show-message" type="button">Show message</button>
        <button class="action" id="speak-message" type="button">🔊 Read aloud</button>
        <button class="action" id="clear-message" type="button">Clear</button>
      </div>
    </section>

    <nav class="categories" aria-label="Visual aid categories">
      <button class="category" type="button" data-category="needs" aria-pressed="true">Needs</button>
      <button class="category" type="button" data-category="feelings" aria-pressed="false">Feelings</button>
      <button class="category" type="button" data-category="people" aria-pressed="false">People</button>
      <button class="category" type="button" data-category="activities" aria-pressed="false">Activities</button>
    </nav>

    <section class="panel" aria-labelledby="board-heading">
      <h2 class="section-heading" id="board-heading">Choose a picture</h2>
      <div class="board" id="board" aria-label="Available visual aids"></div>

      <form class="custom-form" id="custom-form">
        <label class="sr-only" for="custom-text">Add your own word or phrase</label>
        <input id="custom-text" type="text" maxlength="80" placeholder="Type your own word or phrase">
        <button class="action" type="submit">Add to message</button>
      </form>
      <p class="hint">You can choose more than one picture to make a message.</p>
    </section>
  </main>

  <div class="overlay" id="display" role="dialog" aria-modal="true" aria-labelledby="display-text" aria-hidden="true">
    <div class="display-card">
      <span class="display-icon" id="display-icon" aria-hidden="true">💬</span>
      <p class="display-text" id="display-text"></p>
      <button class="action primary" id="display-speak" type="button">🔊 Read aloud</button>
      <button class="action" id="close-display" type="button">Close</button>
    </div>
  </div>

  <script>
    const aids = {
      needs: [
        ["💧", "I want a drink"],
        ["🍽️", "I am hungry"],
        ["🚻", "I need the bathroom"],
        ["🛏️", "I need to rest"],
        ["🆘", "I need help"],
        ["🩹", "I am hurt"],
        ["🥶", "I am cold"],
        ["🥵", "I am hot"],
        ["⏸️", "I need a break"],
        ["✅", "Yes"],
        ["❌", "No"],
        ["🙏", "Please"]
      ],
      feelings: [
        ["😊", "I feel happy"],
        ["😢", "I feel sad"],
        ["😟", "I feel worried"],
        ["😡", "I feel angry"],
        ["😴", "I feel tired"],
        ["😣", "I am uncomfortable"],
        ["❤️", "I feel loved"],
        ["🤷", "I don't know"]
      ],
      people: [
        ["👩", "Mom"],
        ["👨", "Dad"],
        ["👧", "My sister"],
        ["👦", "My brother"],
        ["🧑‍⚕️", "Doctor"],
        ["🧑‍🏫", "Teacher"],
        ["👋", "Friend"],
        ["🧑", "Someone else"]
      ],
      activities: [
        ["🎵", "I want music"],
        ["📺", "I want to watch TV"],
        ["📖", "I want a book"],
        ["🎮", "I want to play"],
        ["🚶", "I want to go outside"],
        ["🏠", "I want to go home"],
        ["🎨", "I want to draw"],
        ["🤗", "I want a hug"]
      ]
    };

    const board = document.querySelector("#board");
    const message = document.querySelector("#message");
    const display = document.querySelector("#display");
    const displayText = document.querySelector("#display-text");
    const displayIcon = document.querySelector("#display-icon");
    let selectedWords = [];
    let lastIcon = "💬";

    function updateMessage() {
      message.textContent = selectedWords.length
        ? selectedWords.join(" ")
        : "Your message will appear here.";
    }

    function addToMessage(text, icon = "💬") {
      selectedWords.push(text);
      lastIcon = icon;
      updateMessage();
    }

    function renderCategory(category) {
      board.replaceChildren();
      for (const [icon, label] of aids[category]) {
        const button = document.createElement("button");
        button.type = "button";
        button.className = "tile";
        button.setAttribute("aria-label", `Add ${label} to message`);

        const image = document.createElement("span");
        image.className = "icon";
        image.setAttribute("aria-hidden", "true");
        image.textContent = icon;

        const caption = document.createElement("span");
        caption.className = "label";
        caption.textContent = label;

        button.append(image, caption);
        button.addEventListener("click", () => addToMessage(label, icon));
        board.append(button);
      }
    }

    function speak(text) {
      if (!("speechSynthesis" in window)) {
        alert("Read aloud is not available in this browser. You can still show your message on screen.");
        return;
      }
      window.speechSynthesis.cancel();
      window.speechSynthesis.speak(new SpeechSynthesisUtterance(text));
    }

    function openDisplay(text, icon = "💬") {
      displayText.textContent = text;
      displayIcon.textContent = icon;
      display.classList.add("is-open");
      display.setAttribute("aria-hidden", "false");
      document.querySelector("#close-display").focus();
    }

    document.querySelectorAll(".category").forEach(button => {
      button.addEventListener("click", () => {
        document.querySelectorAll(".category").forEach(item => {
          item.setAttribute("aria-pressed", String(item === button));
        });
        renderCategory(button.dataset.category);
      });
    });

    document.querySelector("#show-message").addEventListener("click", () => {
      if (!selectedWords.length) {
        openDisplay("Choose a picture to make a message", "👆");
        return;
      }
      openDisplay(selectedWords.join(" "), lastIcon);
    });

    document.querySelector("#speak-message").addEventListener("click", () => {
      if (selectedWords.length) speak(selectedWords.join(" "));
    });

    document.querySelector("#display-speak").addEventListener("click", () => {
      speak(displayText.textContent);
    });

    document.querySelector("#clear-message").addEventListener("click", () => {
      selectedWords = [];
      lastIcon = "💬";
      updateMessage();
    });

    document.querySelector("#close-display").addEventListener("click", () => {
      display.classList.remove("is-open");
      display.setAttribute("aria-hidden", "true");
      document.querySelector("#show-message").focus();
    });

    display.addEventListener("click", event => {
      if (event.target === display) document.querySelector("#close-display").click();
    });

    document.addEventListener("keydown", event => {
      if (event.key === "Escape" && display.classList.contains("is-open")) {
        document.querySelector("#close-display").click();
      }
    });

    document.querySelector("#custom-form").addEventListener("submit", event => {
      event.preventDefault();
      const input = document.querySelector("#custom-text");
      const text = input.value.trim();
      if (!text) return;
      addToMessage(text);
      input.value = "";
      input.focus();
    });

    renderCategory("needs");
  </script>
</body>
</html>

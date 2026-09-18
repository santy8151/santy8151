
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Santiago Suarez | Developer Identity</title>

  <style>
    :root {
      --bg: #02070d;
      --panel: rgba(4, 18, 29, 0.88);
      --cyan: #20e3ff;
      --blue: #2c7cff;
      --green: #31ffad;
      --purple: #8b5cff;
      --text: #d9f7ff;
      --muted: #6f98a8;
      --border: rgba(32, 227, 255, 0.35);
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      min-height: 100vh;
      font-family: "Courier New", monospace;
      color: var(--text);
      background:
        radial-gradient(circle at 20% 20%, rgba(0, 180, 255, 0.11), transparent 30%),
        radial-gradient(circle at 80% 10%, rgba(0, 255, 166, 0.08), transparent 25%),
        linear-gradient(135deg, #010409, #06111b 55%, #02070d);
      overflow-x: hidden;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      pointer-events: none;
      background-image:
        linear-gradient(rgba(32, 227, 255, 0.025) 1px, transparent 1px),
        linear-gradient(90deg, rgba(32, 227, 255, 0.025) 1px, transparent 1px);
      background-size: 40px 40px;
    }

    .terminal {
      width: min(1400px, 95%);
      margin: auto;
      padding: 40px 0 70px;
    }

    .topline {
      display: flex;
      justify-content: space-between;
      gap: 20px;
      font-size: 12px;
      letter-spacing: 3px;
      color: var(--cyan);
      opacity: 0.7;
      margin-bottom: 20px;
    }

    .dashboard {
      display: grid;
      grid-template-columns: 1fr 1.3fr;
      gap: 20px;
    }

    .panel {
      position: relative;
      border: 1px solid var(--border);
      border-radius: 18px;
      background: var(--panel);
      backdrop-filter: blur(12px);
      box-shadow:
        inset 0 0 35px rgba(32, 227, 255, 0.035),
        0 0 40px rgba(0, 0, 0, 0.4);
      overflow: hidden;
    }

    .panel::before,
    .panel::after {
      content: "";
      position: absolute;
      width: 80px;
      height: 2px;
      background: var(--cyan);
      box-shadow: 0 0 10px var(--cyan);
    }

    .panel::before {
      left: 20px;
      top: 0;
    }

    .panel::after {
      right: 20px;
      bottom: 0;
    }

    /* =========================
       FINGERPRINT
    ========================== */

    .scanner-panel {
      padding: 25px;
      min-height: 520px;
    }

    .panel-label {
      color: var(--cyan);
      font-size: 13px;
      letter-spacing: 2px;
      margin-bottom: 10px;
    }

    .scanner-wrapper {
      height: 360px;
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
    }

    .scanner-ring {
      width: 290px;
      height: 290px;
      border-radius: 50%;
      border: 1px solid rgba(32, 227, 255, 0.35);
      display: flex;
      justify-content: center;
      align-items: center;
      position: relative;
      animation: rotateRing 12s linear infinite;
      box-shadow:
        0 0 30px rgba(32, 227, 255, 0.15),
        inset 0 0 40px rgba(32, 227, 255, 0.05);
    }

    .scanner-ring::before,
    .scanner-ring::after {
      content: "";
      position: absolute;
      border-radius: 50%;
      border: 1px dashed rgba(49, 255, 173, 0.28);
    }

    .scanner-ring::before {
      width: 240px;
      height: 240px;
    }

    .scanner-ring::after {
      width: 190px;
      height: 190px;
    }

    @keyframes rotateRing {
      to {
        transform: rotate(360deg);
      }
    }

    .fingerprint {
      position: absolute;
      width: 155px;
      height: 200px;
      display: flex;
      justify-content: center;
      align-items: center;
      z-index: 3;
    }

    .fingerprint svg {
      width: 150px;
      filter:
        drop-shadow(0 0 6px var(--cyan))
        drop-shadow(0 0 18px rgba(32, 227, 255, 0.5));
    }

    .scan-line {
      position: absolute;
      width: 230px;
      height: 2px;
      background: var(--green);
      box-shadow:
        0 0 7px var(--green),
        0 0 20px var(--green);
      animation: scan 2.2s ease-in-out infinite;
      z-index: 5;
    }

    @keyframes scan {
      0% {
        transform: translateY(-100px);
        opacity: 0.2;
      }

      50% {
        opacity: 1;
      }

      100% {
        transform: translateY(100px);
        opacity: 0.2;
      }
    }

    .status-list {
      display: grid;
      gap: 8px;
      font-size: 12px;
      margin-top: 10px;
    }

    .status {
      color: var(--muted);
      transition: all 0.3s ease;
    }

    .status.active {
      color: var(--cyan);
      text-shadow: 0 0 7px var(--cyan);
    }

    .status.success {
      color: var(--green);
      text-shadow: 0 0 7px var(--green);
    }

    .access {
      margin-top: 20px;
      border: 1px solid rgba(49, 255, 173, 0.6);
      color: var(--green);
      padding: 13px;
      text-align: center;
      letter-spacing: 2px;
      opacity: 0;
      transform: translateY(10px);
      transition: 0.5s ease;
    }

    .access.show {
      opacity: 1;
      transform: translateY(0);
      box-shadow:
        inset 0 0 18px rgba(49, 255, 173, 0.08),
        0 0 20px rgba(49, 255, 173, 0.08);
    }

    /* =========================
       PROFILE
    ========================== */

    .profile-panel {
      padding: 30px;
      min-height: 520px;
      opacity: 0.35;
      filter: blur(1.2px);
      transition: 0.8s ease;
    }

    .profile-panel.registered {
      opacity: 1;
      filter: blur(0);
    }

    .profile-title {
      color: var(--green);
      font-size: 25px;
      margin-bottom: 22px;
      letter-spacing: 2px;
    }

    .profile-grid {
      display: grid;
      grid-template-columns: 160px 1fr;
      gap: 25px;
    }

    .avatar {
      width: 160px;
      height: 190px;
      border: 1px solid var(--green);
      border-radius: 8px;
      display: grid;
      place-items: center;
      background:
        linear-gradient(135deg,
          rgba(32, 227, 255, 0.1),
          rgba(139, 92, 255, 0.12));
      box-shadow: 0 0 25px rgba(49, 255, 173, 0.12);
      overflow: hidden;
    }

    .avatar-code {
      font-size: 68px;
      color: var(--cyan);
      text-shadow: 0 0 15px var(--cyan);
    }

    .profile-info h1 {
      font-family: Arial, sans-serif;
      font-size: clamp(26px, 4vw, 40px);
      margin-bottom: 7px;
    }

    .role {
      color: var(--cyan);
      font-size: 18px;
      margin-bottom: 7px;
    }

    .location {
      color: var(--muted);
      margin: 12px 0;
    }

    .description {
      font-family: Arial, sans-serif;
      color: #a8c5ce;
      line-height: 1.6;
      margin-top: 14px;
      max-width: 650px;
    }

    .tags {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 25px;
    }

    .tag {
      border: 1px solid rgba(32, 227, 255, 0.45);
      border-radius: 50px;
      padding: 8px 14px;
      font-size: 12px;
      color: var(--cyan);
      background: rgba(32, 227, 255, 0.04);
      transition: 0.3s;
    }

    .tag:hover {
      background: rgba(32, 227, 255, 0.12);
      box-shadow: 0 0 16px rgba(32, 227, 255, 0.25);
      transform: translateY(-2px);
    }

    /* =========================
       CARDS
    ========================== */

    .skills-section {
      margin-top: 28px;
    }

    .skills-title {
      color: var(--cyan);
      letter-spacing: 3px;
      margin-bottom: 18px;
      font-size: 14px;
    }

    .gift-grid {
      display: grid;
      grid-template-columns: repeat(6, 1fr);
      gap: 15px;
    }

    .gift-card {
      position: relative;
      min-height: 220px;
      border-radius: 16px;
      padding: 18px;
      border: 1px solid rgba(32, 227, 255, 0.24);
      background:
        linear-gradient(160deg,
          rgba(10, 26, 39, 0.98),
          rgba(2, 10, 18, 0.96));
      overflow: hidden;
      transition:
        transform 0.35s ease,
        box-shadow 0.35s ease,
        border 0.35s ease;
      cursor: pointer;
    }

    .gift-card::before {
      content: "";
      position: absolute;
      width: 140px;
      height: 140px;
      border-radius: 50%;
      top: -80px;
      right: -70px;
      background: rgba(32, 227, 255, 0.1);
      filter: blur(10px);
    }

    .gift-card:hover {
      transform: translateY(-12px) rotateX(4deg);
      border-color: var(--cyan);
      box-shadow:
        0 0 25px rgba(32, 227, 255, 0.16),
        0 16px 40px rgba(0, 0, 0, 0.4);
    }

    .gift-number {
      color: var(--muted);
      font-size: 10px;
      letter-spacing: 2px;
    }

    .gift-icon {
      font-size: 45px;
      margin: 28px 0;
      color: var(--cyan);
      text-shadow: 0 0 12px currentColor;
    }

    .gift-card h3 {
      font-family: Arial, sans-serif;
      font-size: 17px;
      margin-bottom: 10px;
    }

    .gift-card p {
      font-size: 11px;
      color: var(--muted);
      line-height: 1.5;
    }

    .aws .gift-icon,
    .aws h3 {
      color: #ffad33;
    }

    .ollama .gift-icon,
    .ollama h3 {
      color: #31ffad;
    }

    .vibe .gift-icon,
    .vibe h3 {
      color: #ad7cff;
    }

    .poo .gift-icon,
    .poo h3 {
      color: #43a4ff;
    }

    .data .gift-icon,
    .data h3 {
      color: #32f7b7;
    }

    .saas .gift-icon,
    .saas h3 {
      color: #aa79ff;
    }

    /* =========================
       TERMINAL LINE
    ========================== */

    .command-line {
      margin-top: 30px;
      border-top: 1px solid rgba(32, 227, 255, 0.15);
      padding-top: 18px;
      font-size: 13px;
      color: var(--green);
    }

    .cursor {
      display: inline-block;
      width: 8px;
      height: 15px;
      background: var(--green);
      margin-left: 5px;
      animation: blink 0.8s steps(1) infinite;
      vertical-align: middle;
    }

    @keyframes blink {
      50% {
        opacity: 0;
      }
    }

    @media (max-width: 1100px) {
      .dashboard {
        grid-template-columns: 1fr;
      }

      .gift-grid {
        grid-template-columns: repeat(3, 1fr);
      }
    }

    @media (max-width: 700px) {
      .profile-grid {
        grid-template-columns: 1fr;
      }

      .gift-grid {
        grid-template-columns: repeat(2, 1fr);
      }

      .avatar {
        width: 120px;
        height: 140px;
      }

      .topline {
        flex-direction: column;
      }
    }

    @media (max-width: 450px) {
      .gift-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>

<body>

  <main class="terminal">

    <div class="topline">
      <span>HUMAN // DEVELOPER // PROBLEM SOLVER</span>
      <span>SANTIAGO.SR // v2.0</span>
    </div>

    <section class="dashboard">

      <!-- BIOMETRIC SCANNER -->
      <article class="panel scanner-panel">

        <div class="panel-label">
          BIOMETRIC AUTHENTICATION // FINGERPRINT SCANNER
        </div>

        <div class="scanner-wrapper">

          <div class="scanner-ring"></div>

          <div class="fingerprint">

            <svg viewBox="0 0 100 130"
                 fill="none"
                 xmlns="http://www.w3.org/2000/svg">

              <path
                d="M50 7C27 7 11 24 11 47
                   M50 16C32 16 20 30 20 48
                   M50 25C37 25 29 35 29 49
                   M50 34C42 34 38 41 38 50
                   M50 43C46 43 44 47 44 52
                   M89 48C89 24 73 7 50 7
                   M80 50C80 31 68 16 50 16
                   M71 52C71 36 62 25 50 25
                   M62 54C62 42 57 34 50 34
                   M56 56C56 48 54 43 50 43
                   M13 57C13 83 26 107 42 121
                   M22 55C22 80 34 100 49 113
                   M31 55C31 77 41 94 55 105
                   M40 55C40 73 47 88 60 97
                   M49 56C49 70 54 82 65 89
                   M58 57C58 68 63 77 71 83
                   M67 57C67 65 70 71 77 76
                   M76 56C76 61 79 66 83 69"
                stroke="#20e3ff"
                stroke-width="3"
                stroke-linecap="round"
              />

            </svg>

          </div>

          <div class="scan-line"></div>

        </div>

        <div class="status-list">
          <div class="status" id="s1">[ ] SCANNING BIOMETRIC DATA...</div>
          <div class="status" id="s2">[ ] ANALYZING PATTERN...</div>
          <div class="status" id="s3">[ ] MATCHING IDENTITY...</div>
          <div class="status" id="s4">[ ] VERIFYING PROFILE...</div>
          <div class="status" id="s5">[ ] REGISTERING USER...</div>
        </div>

        <div class="access" id="access">
          ✓ ACCESS GRANTED // IDENTITY VERIFIED
        </div>

      </article>

      <!-- PROFILE -->
      <article class="panel profile-panel" id="profile">

        <div class="profile-title">
          ✓ PROFILE REGISTERED
        </div>

        <div class="profile-grid">

          <div class="avatar">
            <div class="avatar-code">&lt;/&gt;</div>
          </div>

          <div class="profile-info">

            <h1>Santiago Suarez Ramirez</h1>

            <div class="role">
              Software Developer
            </div>

            <strong>
              Full-Stack | Cloud | AI
            </strong>

            <div class="location">
              Medellin, Colombia
            </div>

            <p class="description">
              Software developer focused on building practical systems
              combining cloud architecture, artificial intelligence,
              cybersecurity, automation, blockchain and automotive
              diagnostics.
            </p>

            <div class="tags">
              <span class="tag">Python</span>
              <span class="tag">FastAPI</span>
              <span class="tag">React</span>
              <span class="tag">AWS</span>
              <span class="tag">DevOps</span>
              <span class="tag">Automation</span>
              <span class="tag">CyberQA</span>
              <span class="tag">Docker</span>
              <span class="tag">AI</span>
            </div>

          </div>

        </div>

      </article>

    </section>

    <!-- KNOWLEDGE CARDS -->
    <section class="skills-section">

      <div class="skills-title">
        KNOWLEDGE MODULES // REGISTERED SKILLS
      </div>

      <div class="gift-grid">

        <div class="gift-card aws">
          <div class="gift-number">MODULE_001</div>
          <div class="gift-icon">☁</div>
          <h3>AWS</h3>
          <p>
            Cloud architecture, EC2, Lambda, S3,
            DynamoDB, API Gateway and scalable infrastructure.
          </p>
        </div>

        <div class="gift-card ollama">
          <div class="gift-number">MODULE_002</div>
          <div class="gift-icon">◉</div>
          <h3>Ollama</h3>
          <p>
            Local AI models, private inference,
            assistants and AI experimentation.
          </p>
        </div>

        <div class="gift-card vibe">
          <div class="gift-number">MODULE_003</div>
          <div class="gift-icon">&lt;/&gt;</div>
          <h3>Vibe Code</h3>
          <p>
            From ideas to working prototypes using
            AI-assisted development and rapid experimentation.
          </p>
        </div>

        <div class="gift-card poo">
          <div class="gift-number">MODULE_004</div>
          <div class="gift-icon">⬡</div>
          <h3>Logica POO</h3>
          <p>
            Objects, encapsulation, inheritance,
            abstraction and reusable software design.
          </p>
        </div>

        <div class="gift-card data">
          <div class="gift-number">MODULE_005</div>
          <div class="gift-icon">⌘</div>
          <h3>Estructura de Datos</h3>
          <p>
            Arrays, lists, stacks, queues, trees,
            graphs and algorithmic thinking.
          </p>
        </div>

        <div class="gift-card saas">
          <div class="gift-number">MODULE_006</div>
          <div class="gift-icon">△</div>
          <h3>Arquitectura de Soluciones SaaS</h3>
          <p>
            Multi-layer systems, APIs, cloud services,
            security, scalability and product architecture.
          </p>
        </div>

      </div>

    </section>

    <div class="command-line">
      root@santiago:~$ identity --load developer.profile
      <span class="cursor"></span>
    </div>

  </main>

  <script>

    const states = [
      document.getElementById("s1"),
      document.getElementById("s2"),
      document.getElementById("s3"),
      document.getElementById("s4"),
      document.getElementById("s5")
    ];

    const access = document.getElementById("access");
    const profile = document.getElementById("profile");

    function runAuthentication() {

      states.forEach((state) => {
        state.classList.remove("active", "success");
        state.innerHTML = state.innerHTML.replace("[✓]", "[ ]");
      });

      access.classList.remove("show");
      profile.classList.remove("registered");

      states.forEach((state, index) => {

        setTimeout(() => {

          state.classList.add("active");

          setTimeout(() => {

            state.classList.remove("active");
            state.classList.add("success");

            state.innerHTML =
              state.innerHTML.replace("[ ]", "[✓]");

          }, 700);

        }, index * 900);

      });

      setTimeout(() => {

        access.classList.add("show");

      }, 5000);

      setTimeout(() => {

        profile.classList.add("registered");

      }, 5500);

    }

    runAuthentication();

    setInterval(() => {

      runAuthentication();

    }, 11000);

  </script>

</body>
</html>


<!doctype html>
<html lang="nl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Fundament Scan</title>
  <style>
    :root{
      --bg: #16253B;         /* brand dark */
      --accent: #16C8F2;     /* brand accent */
      --card: rgba(255,255,255,.08);
      --text: rgba(255,255,255,.94);
      --muted: rgba(255,255,255,.72);
      --border: rgba(255,255,255,.14);
      --shadow: 0 18px 60px rgba(0,0,0,.45);
      --radius: 18px;
    }

    *{ box-sizing: border-box; }
    body{
      margin:0;
      min-height:100vh;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:24px;
      background:
        radial-gradient(1000px 600px at 15% 0%, rgba(22,200,242,.22), transparent 60%),
        radial-gradient(900px 700px at 90% 20%, rgba(255,255,255,.08), transparent 55%),
        var(--bg);
      color: var(--text);
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Helvetica Neue", sans-serif;
      line-height:1.45;
    }

    .wrap{ width:min(860px, 100%); }
    .card{
      background: linear-gradient(180deg, var(--card), rgba(255,255,255,.06));
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      overflow:hidden;
    }

    .header{
      padding:22px 22px 14px;
      border-bottom:1px solid var(--border);
      display:flex;
      gap:14px;
      align-items:flex-start;
      justify-content:space-between;
    }
    .title{ margin:0; font-size:18px; letter-spacing:.2px; }
    .subtitle{ margin:6px 0 0; color: var(--muted); font-size:13px; max-width: 560px; }

    .progress{
      width: 180px;
      max-width: 40%;
      height:10px;
      border-radius:999px;
      background: rgba(255,255,255,.08);
      border: 1px solid rgba(255,255,255,.12);
      overflow:hidden;
      margin-top:4px;
    }
    .bar{
      height:100%;
      width:0%;
      background: linear-gradient(90deg, var(--accent), rgba(255,255,255,.88));
    }
    .step{
      color: var(--muted);
      font-size:12px;
      text-align:right;
      margin-top:6px;
    }

    .content{ padding:22px; }

    /* Start screen */
    .hero{
      padding: 8px 0 0;
    }
    .hero h2{
      margin: 0 0 10px;
      font-size: 22px;
      letter-spacing: .2px;
      line-height: 1.2;
    }
    .hero p{
      margin: 0;
      color: var(--muted);
      font-size: 14px;
      max-width: 62ch;
    }
    .heroCard{
      margin-top: 16px;
      padding: 16px;
      background: rgba(255,255,255,.05);
      border: 1px solid rgba(255,255,255,.10);
      border-radius: 16px;
    }

    .qtitle{ margin:0 0 8px; font-size:16px; }
    .qdesc{ margin:0 0 18px; color: var(--muted); font-size:13px; }

    .scale{
      display:grid;
      grid-template-columns: repeat(5, minmax(0,1fr));
      gap:10px;
      margin: 14px 0 18px;
    }
    .choice{ position:relative; }
    .choice input{ position:absolute; opacity:0; pointer-events:none; }
    .pill{
      display:flex;
      align-items:center;
      justify-content:center;
      padding:14px 10px;
      border-radius: 14px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
      cursor:pointer;
      user-select:none;
      transition: transform .08s ease, background .15s ease, border-color .15s ease;
      font-weight:800;
    }
    .choice input:checked + .pill{
      background: rgba(22,200,242,.18);
      border-color: rgba(22,200,242,.65);
      transform: translateY(-1px);
      box-shadow: 0 10px 28px rgba(22,200,242,.16);
    }

    .hint{
      display:flex;
      justify-content:space-between;
      color: var(--muted);
      font-size:12px;
      margin-top:8px;
    }

    .actions{
      display:flex;
      gap:10px;
      justify-content:space-between;
      margin-top: 18px;
      flex-wrap: wrap;
    }
    .btn{
      appearance:none;
      border: 1px solid rgba(255,255,255,.16);
      background: rgba(255,255,255,.06);
      color: var(--text);
      padding: 12px 14px;
      border-radius: 14px;
      cursor:pointer;
      font-weight:800;
      transition: background .15s ease, border-color .15s ease, transform .08s ease;
      min-width: 140px;
    }
    .btn:hover{ background: rgba(255,255,255,.09); }
    .btn:active{ transform: translateY(1px); }
    .btn.primary{
      border-color: rgba(22,200,242,.65);
      background: rgba(22,200,242,.16);
    }
    .btn.primary:disabled{ opacity:.45; cursor:not-allowed; }

    .resultTag{
      display:inline-flex;
      align-items:center;
      gap:8px;
      padding: 10px 12px;
      border-radius: 999px;
      background: rgba(255,255,255,.06);
      border: 1px solid rgba(255,255,255,.12);
      color: var(--muted);
      font-size:12px;
      margin-bottom: 14px;
    }
    .dot{
      width:8px;height:8px;border-radius:999px;background: var(--accent);
      box-shadow: 0 0 0 4px rgba(22,200,242,.14);
    }
    .resultTitle{ margin:0 0 10px; font-size:18px; }
    .resultText{ margin:0; color: var(--muted); font-size:14px; white-space: pre-line; }

    .ctaBox{
      margin-top: 16px;
      padding: 14px;
      background: rgba(255,255,255,.05);
      border: 1px solid rgba(255,255,255,.10);
      border-radius: 14px;
    }
    .ctaRow{
      display:flex;
      gap:10px;
      flex-wrap: wrap;
      margin-top: 12px;
    }
    .linkBtn{
      display:inline-flex;
      align-items:center;
      justify-content:center;
      text-decoration:none;
      padding: 10px 12px;
      border-radius: 12px;
      border: 1px solid rgba(255,255,255,.16);
      background: rgba(255,255,255,.06);
      color: var(--text);
      font-weight:800;
      min-width: 190px;
    }
    .linkBtn.primary{
      border-color: rgba(22,200,242,.65);
      background: rgba(22,200,242,.16);
    }
    .smallMuted{ color: var(--muted); font-size: 13px; margin: 0; }

    .summary{
      margin-top:16px;
      padding:14px;
      background: rgba(255,255,255,.05);
      border: 1px solid rgba(255,255,255,.10);
      border-radius: 14px;
      color: var(--muted);
      font-size:13px;
    }

    /* Lead form */
    .formGrid{
      display:grid;
      grid-template-columns: 1fr 1fr;
      gap:12px;
      margin-top: 10px;
    }
    .field{ display:flex; flex-direction:column; gap:6px; }
    label{ font-size:12px; color: var(--muted); }
    input{
      padding: 12px 12px;
      border-radius: 14px;
      border: 1px solid rgba(255,255,255,.14);
      background: rgba(0,0,0,.18);
      color: var(--text);
      outline: none;
    }
    input:focus{ border-color: rgba(22,200,242,.75); box-shadow: 0 0 0 4px rgba(22,200,242,.14); }

    .error{
      margin-top: 10px;
      color: rgba(255,180,180,.92);
      font-size: 13px;
    }

    .footerNote{
      margin-top:14px;
      color: rgba(255,255,255,.45);
      font-size:12px;
      text-align:center;
    }

    @media (max-width:620px){
      .progress{ width: 140px; }
      .btn{ min-width: 120px; flex: 1; }
      .formGrid{ grid-template-columns: 1fr; }
      .linkBtn{ min-width: 100%; }
      .hero h2{ font-size: 20px; }
    }
  </style>
</head>

<body>
  <div class="wrap">
    <div class="card" role="application" aria-label="Praktijk Fundament Scan">
      <div class="header">
        <div>
          <h1 class="title">Fundament Scan</h1>
          <p class="subtitle">3 korte vragen (score 1–5). Daarna krijg je een uitkomst op basis van je laagste score.</p>
        </div>
        <div style="min-width:190px">
          <div class="progress" aria-hidden="true"><div class="bar" id="bar"></div></div>
          <div class="step" id="stepText">Start</div>
        </div>
      </div>

      <div class="content" id="view"></div>
    </div>

    <div class="footerNote">Tip: embed dit later in WordPress via een iframe (GitHub Pages).</div>
  </div>

<script>
  // ===== LINKS (ingevuld) =====
  const DOWNLOAD_SCAN_URL = "https://marietteham.nl/wp-content/uploads/2026/02/PLB_Module-4-werkboek-fundamentscan.pdf";
  const CONTACT_URL = "https://marietteham.nl/contact/";
  // ============================

  const startCopy = {
    title: "Hoe sterk is het fundament van jouw praktijk?",
    text: "Doe nu de fundament-scan en ontdek waar jouw grootste verantwoordelijkheden liggen."
  };

  const questions = [
    { key: "processen", title: "1. Gestroomlijnde processen", desc: "Hoe goed zijn uw werkprocessen gedefinieerd en geoptimaliseerd?" },
    { key: "rollen",    title: "2. Heldere rollen & verantwoordelijkheden", desc: "Hoe duidelijk is het voor iedereen wie wat doet?" },
    { key: "systemen",  title: "3. Ondersteunende systemen & tools", desc: "Hoe goed ondersteunen uw systemen het dagelijkse werk?" }
  ];

  const outcomes = {
    processen: {
      label: "Gestroomlijnde processen",
      text:
`Je grootste winst zit in het definiëren en optimaliseren van je werkprocessen.
Er wordt sneller en efficiënter gewerkt en er worden minder fouten gemaakt als iedereen weet wat hij of zij moet doen.

Dit betekent niet dat er geen ruimte meer is voor vrijheid, maar door processen uit te schrijven, af te bakenen en veelvoorkomende processen te standaardiseren, zorg je voor meer efficiëntie en effectiviteit.`
    },
    rollen: {
      label: "Heldere rollen & verantwoordelijkheden",
      text:
`Jou grootste winst zit in het opstellen van duidelijke rollen en verantwoordelijkheden. Als niet iedereen weet wat de ander doet, blijven mensen zwemmen. Het blijft onduidelijk wie verantwoordelijk is voor wat. Blijven fouten in de lucht hangen zonder eigenaar, zonder oplossing.`
    },
    systemen: {
      label: "Ondersteunende systemen & tools",
      text:
`Jou grootste winst zit in het werken met ondersteunende systemen en tools.
Dit is de laatste stap bij het creeren van een effiente praktijk structuur. Geen of verourdere systemen zorgen voor frustratie en voor veel handmatig en foutgevoelige taken. Systemen moet voor je werken het dagelijkse werk makkelijker maken en automatiseren.`
    }
  };

  const ctaText =
`Download de scan voor een volledige evaluatie van jouw praktijk structuur of neem contact met mij op voor vrijblijvend advies.`;

  // step: -1 start, 0..2 vragen, 3 lead, 4 resultaat
  let step = -1;
  const answers = {}; // key -> 1..5
  const lead = { name: "", email: "", phone: "" };

  const view = document.getElementById("view");
  const bar = document.getElementById("bar");
  const stepText = document.getElementById("stepText");

  function setProgress() {
    // totaal stappen naar resultaat: start + 3 vragen + lead = 5 schermen, progress start = 0
    const total = 1 + questions.length + 1; // start + vragen + lead
    const current = Math.max(0, Math.min(step + 1, total)); // start = 0
    const pct = Math.round((current / total) * 100);
    bar.style.width = pct + "%";

    if (step < 0) stepText.textContent = "Start";
    else if (step <= questions.length - 1) stepText.textContent = `Vraag ${step + 1}/${questions.length}`;
    else if (step === questions.length) stepText.textContent = "Jouw gegevens";
    else stepText.textContent = "Resultaat";
  }

  function renderStart() {
    setProgress();
    view.innerHTML = `
      <div class="hero">
        <h2>${startCopy.title}</h2>
        <p>${startCopy.text}</p>

        <div class="heroCard">
          <p class="smallMuted">
            Je beantwoordt 3 vragen (1 = laag, 5 = hoog).<br/>
            Daarna zie je direct waar jouw grootste winst ligt.
          </p>

          <div class="actions">
            <a class="linkBtn" href="${DOWNLOAD_SCAN_URL}" target="_blank" rel="noopener">Download de scan</a>
            <button class="btn primary" id="startBtn">Start</button>
          </div>
        </div>
      </div>
    `;

    document.getElementById("startBtn").addEventListener("click", () => {
      step = 0;
      renderQuestion();
    });
  }

  function renderQuestion() {
    setProgress();
    const q = questions[step];
    const selected = answers[q.key];

    view.innerHTML = `
      <h2 class="qtitle">${q.title}</h2>
      <p class="qdesc">${q.desc}</p>

      <div class="scale" role="radiogroup" aria-label="${q.title}">
        ${[1,2,3,4,5].map(v => `
          <label class="choice">
            <input type="radio" name="score" value="${v}" ${selected === v ? "checked" : ""} />
            <div class="pill">${v}</div>
          </label>
        `).join("")}
      </div>

      <div class="hint"><span>1 = laag</span><span>5 = hoog</span></div>

      <div class="actions">
        <button class="btn" id="back">Vorige</button>
        <button class="btn primary" id="next" disabled>Volgende</button>
      </div>
    `;

    const nextBtn = document.getElementById("next");
    const backBtn = document.getElementById("back");

    if (selected) nextBtn.disabled = false;

    view.querySelectorAll('input[name="score"]').forEach((el) => {
      el.addEventListener("change", (e) => {
        answers[q.key] = parseInt(e.target.value, 10);
        nextBtn.disabled = false;
      });
    });

    backBtn.addEventListener("click", () => {
      if (step === 0) {
        step = -1;
        renderStart();
      } else {
        step--;
        renderQuestion();
      }
    });

    nextBtn.addEventListener("click", () => {
      if (step < questions.length - 1) {
        step++;
        renderQuestion();
      } else {
        step = questions.length; // lead
        renderLeadForm();
      }
    });

    if (step === questions.length - 1) nextBtn.textContent = "Verder";
  }

  function renderLeadForm() {
    setProgress();

    view.innerHTML = `
      <h2 class="qtitle">Bijna klaar</h2>
      <p class="qdesc">Vul je gegevens in om je resultaat te bekijken.</p>

      <div class="formGrid" role="form" aria-label="Contactgegevens">
        <div class="field" style="grid-column: 1 / -1;">
          <label for="name">Naam</label>
          <input id="name" type="text" placeholder="Bijv. Anouk" value="${escapeHtml(lead.name)}" required />
        </div>

        <div class="field">
          <label for="email">E-mail</label>
          <input id="email" type="email" placeholder="naam@bedrijf.nl" value="${escapeHtml(lead.email)}" required />
        </div>

        <div class="field">
          <label for="phone">Telefoonnummer</label>
          <input id="phone" type="tel" placeholder="06 12345678" value="${escapeHtml(lead.phone)}" required />
        </div>
      </div>

      <div class="error" id="err" style="display:none;"></div>

      <div class="actions">
        <button class="btn" id="back">Vorige</button>
        <button class="btn primary" id="show">Bekijk resultaat</button>
      </div>
    `;

    const backBtn = document.getElementById("back");
    const showBtn = document.getElementById("show");
    const err = document.getElementById("err");

    backBtn.addEventListener("click", () => {
      step = questions.length - 1;
      renderQuestion();
    });

    showBtn.addEventListener("click", () => {
      lead.name = document.getElementById("name").value.trim();
      lead.email = document.getElementById("email").value.trim();
      lead.phone = document.getElementById("phone").value.trim();

      const valid = validateLead(lead);
      if (!valid.ok) {
        err.style.display = "block";
        err.textContent = valid.msg;
        return;
      }

      // optioneel: lokaal bewaren (handig tijdens testen)
      try {
        localStorage.setItem("fundamentScanLead", JSON.stringify({ lead, answers, ts: Date.now() }));
      } catch(e) {}

      step = questions.length + 1;
      renderResult();
    });
  }

  function renderResult() {
    setProgress();
    bar.style.width = "100%";

    // laagste score bepalen; bij gelijke scores: eerste in volgorde (find)
    const scored = questions.map(q => ({ key: q.key, value: answers[q.key] }));
    const minVal = Math.min(...scored.map(s => s.value));
    const lowest = scored.find(s => s.value === minVal); // FIRST match

    const o = outcomes[lowest.key];

    const totalScore = scored.reduce((acc, s) => acc + s.value, 0);

    view.innerHTML = `
      <div class="resultTag"><span class="dot"></span> Grootste winstgebied</div>
      <h2 class="resultTitle">${o.label}</h2>
      <p class="resultText">${o.text}</p>

      <div class="ctaBox">
        <p class="smallMuted">${ctaText}</p>
        <div class="ctaRow">
          <a class="linkBtn primary" href="${DOWNLOAD_SCAN_URL}" target="_blank" rel="noopener">Download de scan</a>
          <a class="linkBtn" href="${CONTACT_URL}" target="_blank" rel="noopener">Neem contact op</a>
        </div>
      </div>

      <div class="summary">
        <strong>Jouw scores</strong><br/>
        ${questions.map(q => `• ${q.title.replace(/^\d+\.\s*/,'')}: <strong>${answers[q.key]}</strong>`).join("<br/>")}
        <br/><br/>
        Laagste score: <strong>${minVal}</strong> → uitkomst gebaseerd op <strong>${o.label}</strong>.<br/>
        Totale score: <strong>${totalScore}</strong>.
        <br/><br/>
        <strong>Gegevens</strong><br/>
        • Naam: <strong>${escapeHtml(lead.name)}</strong><br/>
        • E-mail: <strong>${escapeHtml(lead.email)}</strong><br/>
        • Telefoon: <strong>${escapeHtml(lead.phone)}</strong>
      </div>

      <div class="actions">
        <button class="btn" id="restart">Opnieuw</button>
      </div>
    `;

    document.getElementById("restart").addEventListener("click", () => {
      step = -1;
      for (const k of Object.keys(answers)) delete answers[k];
      lead.name = ""; lead.email = ""; lead.phone = "";
      renderStart();
    });
  }

  function validateLead({ name, email, phone }) {
    if (!name || name.length < 2) return { ok:false, msg:"Vul je naam in (minimaal 2 tekens)." };
    if (!email || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) return { ok:false, msg:"Vul een geldig e-mailadres in." };
    const cleaned = phone.replace(/\s|-/g,"");
    if (!cleaned || cleaned.length < 8) return { ok:false, msg:"Vul een geldig telefoonnummer in (minimaal 8 tekens)." };
    return { ok:true };
  }

  function escapeHtml(str){
    return String(str || "")
      .replaceAll("&","&amp;")
      .replaceAll("<","&lt;")
      .replaceAll(">","&gt;")
      .replaceAll('"',"&quot;")
      .replaceAll("'","&#039;");
  }

  // init
  renderStart();
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>نوفا — تطبيق الذكاء الاصطناعي الشامل</title>
<style>
  :root{
    --bg:#0d0f14; --panel:#151823; --panel2:#1c2030; --line:#2a2f42;
    --txt:#e8eaf2; --txt2:#9aa1b5; --txt3:#626a80;
    --acc:#6c8cff; --acc2:#8f6cff; --ok:#3ddc97; --warn:#ffb454; --bad:#ff6b6b;
    --r:12px;
  }
  *{box-sizing:border-box; margin:0; padding:0}
  body{font-family:"Segoe UI",Tahoma,Arial,sans-serif; background:var(--bg); color:var(--txt); min-height:100vh}
  .app{display:flex; min-height:100vh}
  aside{width:230px; background:var(--panel); border-inline-end:1px solid var(--line); padding:20px 14px; display:flex; flex-direction:column; gap:6px; position:sticky; top:0; height:100vh}
  .logo{display:flex; align-items:center; gap:10px; padding:6px 8px 18px; font-size:20px; font-weight:700}
  .logo .dot{width:34px;height:34px;border-radius:10px;background:linear-gradient(135deg,var(--acc),var(--acc2));display:flex;align-items:center;justify-content:center;font-size:17px}
  .navbtn{display:flex;align-items:center;gap:10px;width:100%;padding:11px 12px;border:none;border-radius:10px;background:transparent;color:var(--txt2);font-size:15px;cursor:pointer;text-align:right;transition:.15s}
  .navbtn:hover{background:var(--panel2);color:var(--txt)}
  .navbtn.on{background:var(--panel2);color:var(--txt);font-weight:600;box-shadow:inset -3px 0 0 var(--acc)}
  .navbtn .ic{font-size:17px;width:22px;text-align:center}
  aside .foot{margin-top:auto;font-size:12px;color:var(--txt3);padding:8px}
  main{flex:1;padding:24px 28px;max-width:980px}
  .topbar{display:flex;align-items:center;justify-content:space-between;margin-bottom:20px}
  .topbar h1{font-size:21px;font-weight:700}
  .badge{font-size:12px;color:var(--txt3);border:1px solid var(--line);border-radius:20px;padding:4px 12px}
  .view{display:none;animation:fade .2s ease}
  .view.on{display:block}
  @keyframes fade{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
  .card{background:var(--panel);border:1px solid var(--line);border-radius:var(--r);padding:20px}
  .card h2{font-size:16px;margin-bottom:6px}
  .muted{color:var(--txt2);font-size:13.5px;line-height:1.7}
  #chatBox{height:52vh;overflow-y:auto;display:flex;flex-direction:column;gap:12px;padding:6px 2px}
  .msg{max-width:78%;padding:11px 15px;border-radius:14px;font-size:15px;line-height:1.75;white-space:pre-wrap}
  .msg.user{align-self:flex-start;background:linear-gradient(135deg,var(--acc),var(--acc2));border-bottom-right-radius:4px}
  .msg.bot{align-self:flex-end;background:var(--panel2);border:1px solid var(--line);border-bottom-left-radius:4px}
  .typing{align-self:flex-end;color:var(--txt3);font-size:13px;padding:4px 10px}
  .chatbar{display:flex;gap:10px;margin-top:14px}
  input[type=text],textarea,select{background:var(--panel2);border:1px solid var(--line);color:var(--txt);border-radius:10px;padding:12px 14px;font-size:15px;font-family:inherit;outline:none;width:100%}
  input:focus,textarea:focus,select:focus{border-color:var(--acc)}
  .btn{border:none;border-radius:10px;padding:12px 20px;font-size:15px;font-weight:600;cursor:pointer;background:linear-gradient(135deg,var(--acc),var(--acc2));color:#fff;transition:.15s;white-space:nowrap}
  .btn:hover{filter:brightness(1.12)}
  .btn.ghost{background:var(--panel2);color:var(--txt);border:1px solid var(--line)}
  .chips{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
  .chip{font-size:12.5px;background:var(--panel2);border:1px solid var(--line);color:var(--txt2);border-radius:20px;padding:6px 13px;cursor:pointer;transition:.15s}
  .chip:hover{color:var(--txt);border-color:var(--acc)}
  .genrow{display:flex;gap:10px;flex-wrap:wrap;margin:14px 0}
  canvas#artCanvas{width:100%;border-radius:12px;border:1px solid var(--line);background:#000;display:block}
  .artwrap{display:grid;grid-template-columns:1fr;gap:14px}
  .vstage{text-align:center;padding:36px 20px}
  .orb{width:120px;height:120px;border-radius:50%;margin:0 auto 20px;background:radial-gradient(circle at 35% 35%,var(--acc),var(--acc2));display:flex;align-items:center;justify-content:center;font-size:40px;cursor:pointer;transition:.2s;box-shadow:0 0 0 0 rgba(108,140,255,.4)}
  .orb:hover{transform:scale(1.05)}
  .orb.listen{animation:pulse 1.2s infinite}
  @keyframes pulse{0%{box-shadow:0 0 0 0 rgba(108,140,255,.5)}70%{box-shadow:0 0 0 26px rgba(108,140,255,0)}100%{box-shadow:0 0 0 0 rgba(108,140,255,0)}}
  .vlog{max-height:180px;overflow-y:auto;text-align:right;margin-top:18px;display:flex;flex-direction:column;gap:8px}
  .vlog div{background:var(--panel2);border:1px solid var(--line);border-radius:10px;padding:9px 13px;font-size:14px}
  .vlog b{color:var(--acc)}
  .drop{border:2px dashed var(--line);border-radius:12px;padding:36px;text-align:center;color:var(--txt2);cursor:pointer;transition:.15s}
  .drop.over{border-color:var(--acc);background:rgba(108,140,255,.06)}
  .stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:10px;margin:16px 0}
  .stat{background:var(--panel2);border:1px solid var(--line);border-radius:10px;padding:14px;text-align:center}
  .stat .v{font-size:22px;font-weight:700}
  .stat .l{font-size:12px;color:var(--txt3);margin-top:3px}
  pre.filetxt{background:var(--panel2);border:1px solid var(--line);border-radius:10px;padding:14px;font-size:13px;max-height:220px;overflow:auto;direction:ltr;text-align:left;white-space:pre-wrap}
  .row{display:flex;gap:10px;flex-wrap:wrap;align-items:center}
  .grid2{display:grid;grid-template-columns:1fr 1fr;gap:14px}
  @media(max-width:760px){.app{flex-direction:column}aside{width:100%;height:auto;position:static;flex-direction:row;flex-wrap:wrap}aside .foot{display:none}.grid2{grid-template-columns:1fr}}
  .note{font-size:12.5px;color:var(--warn);background:rgba(255,180,84,.08);border:1px solid rgba(255,180,84,.3);border-radius:10px;padding:10px 13px;margin-top:12px;line-height:1.7}
  .oknote{color:var(--ok);background:rgba(61,220,151,.08);border-color:rgba(61,220,151,.3)}
</style>
</head>
<body>
<div class="app">
  <aside>
    <div class="logo"><span class="dot">✦</span> نوفا</div>
    <button class="navbtn on" data-v="chat"><span class="ic">💬</span> المحادثة</button>
    <button class="navbtn" data-v="img"><span class="ic">🎨</span> توليد الصور</button>
    <button class="navbtn" data-v="voice"><span class="ic">🎙️</span> المساعد الصوتي</button>
    <button class="navbtn" data-v="files"><span class="ic">📄</span> تحليل الملفات</button>
    <button class="navbtn" data-v="set"><span class="ic">⚙️</span> الإعدادات</button>
    <div class="foot">نسخة أولية v0.1 — تعمل محليًا بدون سيرفر</div>
  </aside>

  <main>
    <div class="topbar"><h1 id="vtitle">المحادثة</h1><span class="badge" id="modeBadge">وضع تجريبي محلي</span></div>

    <section class="view on" id="v-chat">
      <div id="chatBox"></div>
      <div class="chatbar">
        <input type="text" id="chatIn" placeholder="اكتب رسالتك هنا... (جرّب: احسب 12*8)" autocomplete="off">
        <button class="btn" id="chatSend">إرسال</button>
      </div>
      <div class="chips" id="chatChips"></div>
    </section>

    <section class="view" id="v-img">
      <div class="card">
        <h2>توليد صور فنية تجريبية</h2>
        <p class="muted">اكتب وصفًا بالعربية أو الإنجليزية، واختر النمط، وسيرسم المحرك لوحة فنية إجرائية فريدة — تعمل 100% داخل المتصفح بدون أي خدمة خارجية.</p>
        <div class="genrow">
          <input type="text" id="imgPrompt" placeholder="مثال: غروب الشمس فوق جبال ملونة" style="flex:1;min-width:220px">
          <select id="imgStyle" style="width:auto">
            <option value="abstract">تجريدي</option>
            <option value="space">فضاء</option>
            <option value="nature">طبيعة</option>
            <option value="waves">أمواج</option>
          </select>
          <button class="btn" id="imgGo">ارسم</button>
        </div>
        <div class="artwrap">
          <canvas id="artCanvas" width="960" height="540"></canvas>
          <div class="row">
            <button class="btn ghost" id="imgAgain">🎲 نفس الوصف، رسمة جديدة</button>
            <button class="btn ghost" id="imgDl">⬇️ تحميل PNG</button>
          </div>
        </div>
      </div>
    </section>

    <section class="view" id="v-voice">
      <div class="card vstage">
        <div class="orb" id="orb">🎙️</div>
        <h2>اضغط على الدائرة واتكلم</h2>
        <p class="muted" id="vStatus">المساعد جاهز — اسألني عن الطقس، الوقت، أو قول «احسب 5 ضرب 6»</p>
        <div class="row" style="justify-content:center;margin-top:16px">
          <button class="btn ghost" id="vSpeakTest">🔊 جرّب الصوت</button>
          <button class="btn ghost" id="vStop">⏹ إيقاف الكلام</button>
        </div>
        <div class="vlog" id="vLog"></div>
        <div class="note" id="vNote">تنبيه: التعرف على الصوت يحتاج متصفح Chrome أو Edge واتصالًا أوليًا غالبًا، أما نطق الردود فيعمل مباشرة.</div>
      </div>
    </section>

    <section class="view" id="v-files">
      <div class="card">
        <h2>ارفع ملف نصي وسألخصله وأحلله</h2>
        <p class="muted">يدعم: .txt .md .csv .json .html — التحليل كله محلي على جهازك.</p>
        <div class="drop" id="drop" style="margin-top:14px">📁 اسحب الملف هنا أو اضغط للاختيار<input type="file" id="fileIn" hidden></div>
        <div id="fileOut" style="margin-top:16px"></div>
      </div>
    </section>

    <section class="view" id="v-set">
      <div class="card">
        <h2>الوضع الحقيقي (اختياري)</h2>
        <p class="muted">افتراضيًا التطبيق يشتغل بوضع تجريبي محلي (ردود جاهزة + رسم إجرائي). لو عندك مفتاح API لموديل متوافق مع OpenAI، فعّل الوضع الحقيقي وخلي المحادثة والصور تتولد من نموذج فعلي.</p>
        <div class="grid2" style="margin-top:14px">
          <div><label class="muted">مفتاح API</label><input type="text" id="apiKey" placeholder="sk-..." style="margin-top:6px"></div>
          <div><label class="muted">رابط الخدمة (اختياري)</label><input type="text" id="apiBase" placeholder="https://api.openai.com/v1" style="margin-top:6px"></div>
        </div>
        <div style="margin-top:12px"><label class="muted">اسم الموديل</label><input type="text" id="apiModel" placeholder="gpt-4o-mini" style="margin-top:6px"></div>
        <div class="row" style="margin-top:16px">
          <button class="btn" id="saveSet">💾 حفظ الإعدادات</button>
          <button class="btn ghost" id="clearSet">🗑 مسح المفتاح</button>
        </div>
        <div class="note">ملاحظة تقنية: بعض مزودي الـ API يمنعون الاتصال من ملف محلي (CORS). لو حصل، شغّل الملف عبر خادم محلي بسيط أو استخدم مزودًا يدعم CORS.</div>
      </div>
    </section>
  </main>
</div>

<script>
  const $ = s => document.querySelector(s);

  const settings = {
    get key() { return localStorage.getItem('nova_key') || ''; },
    set key(v) { localStorage.setItem('nova_key', v); },
    get base() { return localStorage.getItem('nova_base') || 'https://api.openai.com/v1'; },
    set base(v) { localStorage.setItem('nova_base', v); },
    get model() { return localStorage.getItem('nova_model') || 'gpt-4o-mini'; },
    set model(v) { localStorage.setItem('nova_model', v); },
    get real() { return !!this.key; }
  };

  function refreshBadge() {
    $('#modeBadge').textContent = settings.real ? '⚡ وضع حقيقي: ' + settings.model : 'وضع تجريبي محلي';
  }

  function loadSettingsUI() {
    $('#apiKey').value = settings.key;
    $('#apiBase').value = settings.base;
    $('#apiModel').value = settings.model;
    refreshBadge();
  }

  document.querySelectorAll('.navbtn').forEach(btn => {
    btn.addEventListener('click', () => {
      document.querySelectorAll('.navbtn').forEach(x => x.classList.remove('on'));
      document.querySelectorAll('.view').forEach(x => x.classList.remove('on'));
      btn.classList.add('on');
      $('#v-' + btn.dataset.v).classList.add('on');
      $('#vtitle').textContent = {
        chat: 'المحادثة',
        img: 'توليد الصور',
        voice: 'المساعد الصوتي',
        files: 'تحليل الملفات',
        set: 'الإعدادات'
      }[btn.dataset.v];
    });
  });

  function addMsg(txt, who) {
    const d = document.createElement('div');
    d.className = 'msg ' + who;
    d.textContent = txt;
    $('#chatBox').appendChild(d);
    $('#chatBox').scrollTop = $('#chatBox').scrollHeight;
    return d;
  }

  function normalizeExpression(expr) {
    return expr
      .replace(/×/g, '*')
      .replace(/÷/g, '/')
      .replace(/ضرب/g, '*')
      .replace(/مضروب/g, '*')
      .replace(/\s+/g, '')
      .replace(/،/g, '')
      .trim();
  }

  function evaluateMathExpression(raw) {
    const cleaned = normalizeExpression(raw);
    if (!/^[0-9.+\\-*/()]+$/.test(cleaned)) return null;

    try {
      const val = Function('"use strict"; return (' + cleaned + ')')();
      if (isFinite(val)) return Number(val);
    } catch (e) {
      return null;
    }
    return null;
  }

  function mockBrain(q) {
    const text = (q || '').trim();
    if (!text) return 'اكتب سؤالاً أو طلباً وأنا أساعدك.';

    const calcMatch = text.match(/(?:احسب|كم|حاسب|قيمة)\s+(.+)/i) ||
      text.match(/([\d\.\+\-\*\/\s\(\)×÷ضرب]+)$/i);

    if (calcMatch) {
      const expr = calcMatch[1] || calcMatch[0];
      const result = evaluateMathExpression(expr);
      if (result !== null) {
        return 'النتيجة: ' + Number(result.toFixed(6)) + ' ✔';
      }
    }

    const low = text.toLowerCase();
    const kb = [
      [/(سلام|اهلا|أهلا|هلا|هاي|صباح|مساء)/i, 'أهلًا بيك! أنا نوفا ✦ مساعدك الذكي. اسألني أي حاجة أو جرّب تبويب «توليد الصور».'],
      [/(اسمك|مين انت|من أنت|عرفني بنفسك)/i, 'أنا نوفا ✦ تطبيق ذكاء اصطناعي شامل: أساعدك في المحادثة، الرسم، الصوت، وتحليل الملفات.'],
      [/(وقت|الساعة|تاريخ|اليوم|نهاردة|الوقت الآن)/i, 'الوقت الآن: ' + new Date().toLocaleTimeString('ar-EG') + ' — والتاريخ: ' + new Date().toLocaleDateString('ar-EG')],
      [/(طقس|الجو|مطر|حرارة)/i, 'في الوضع التجريبي ما عندي بيانات الطقس مباشرة. لكن يمكنك تفعيل الوضع الحقيقي من الإعدادات.'],
      [/(صور|ارسم|رسم|صورة)/i, 'روح إلى تبويب «توليد الصور» واذكر الوصف المطلوب، وسأرسم لك لوحة فنية على الفور.'],
      [/(صوت|تحدث|استمع|مساعد صوتي|اتكلم)/i, 'جرب تبويب «المساعد الصوتي»: اضغط الدائرة واتكلم، وسأرد لك بصوت عربي.'],
      [/(ملف|لخص|تلخيص|تحليل|ملخص)/i, 'من تبويب «تحليل الملفات» اسحب أي ملف نصي أو اختره، وسأعطيك ملخصًا وإحصاءات.'],
      [/(شكرا|مشكور|تسلم|حبيب)/i, 'العفو! أي وقت 😊'],
      [/(وداع|باي|مع السلامة)/i, 'مع السلامة! أنا موجود هنا كل ما احتجتني. ✦'],
      [/(ذكاء اصطناعي|ai|artificial intelligence)/i, 'الذكاء الاصطناعي هو قدرة الحاسب على فهم، تعلم، واستنتاج أشياء تشبه الإنسان. وأنا مثال حي عليه.']
    ];

    for (const [re, ans] of kb) {
      if (re.test(text)) return ans;
    }

    const general = [
      'سؤال جميل! جرّب تفعيل الوضع الحقيقي من ⚙️ الإعدادات لأحصل على ردود أقرب إلى نموذج لغوي قوي.',
      'حاضر — في الوضع التجريبي أقدر أساعدك في الحسابات، الوقت، الصور، والصوت. جرّب سؤالًا مثل «احسب 15*4» أو «ارسم غروب الشمس».',
      'تمام ✅ لو أردت ردود أعمق، أضف مفتاح API من الإعدادات، وسيتم التحول إلى الوضع الحقيقي فورًا.'
    ];

    return general[Math.floor(Math.random() * general.length)];
  }

  async function realBrain(q) {
    const base = settings.base.replace(/\/$/, '');
    const res = await fetch(base + '/chat/completions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer ' + settings.key
      },
      body: JSON.stringify({
        model: settings.model,
        messages: [{ role: 'user', content: q }]
      })
    });

    if (!res.ok) throw new Error('HTTP ' + res.status);
    const data = await res.json();
    return data.choices[0].message.content;
  }

  async function sendChat() {
    const input = $('#chatIn');
    const q = input.value.trim();
    if (!q) return;

    input.value = '';
    addMsg(q, 'user');

    const loader = document.createElement('div');
    loader.className = 'typing';
    loader.textContent = 'نوفا يكتب...';
    $('#chatBox').appendChild(loader);
    $('#chatBox').scrollTop = $('#chatBox').scrollHeight;

    try {
      let ans;
      if (settings.real) {
        try {
          ans = await realBrain(q);
        } catch (e) {
          ans = '⚠️ مشكلة في الاتصال بالـ API (' + e.message + '). سأرد عليك محليًا:\n' + mockBrain(q);
        }
      } else {
        ans = mockBrain(q);
      }

      loader.remove();
      addMsg(ans, 'bot');
    } catch (e) {
      loader.remove();
      addMsg('حصل خطأ غير متوقع.', 'bot');
    }
  }

  $('#chatSend').addEventListener('click', sendChat);
  $('#chatIn').addEventListener('keydown', e => {
    if (e.key === 'Enter') sendChat();
  });

  ['احسب 125*8', 'مين انت؟', 'الساعة كام دلوقتي', 'ارسم لي غروب الشمس'].forEach(text => {
    const btn = document.createElement('span');
    btn.className = 'chip';
    btn.textContent = text;
    btn.onclick = () => {
      $('#chatIn').value = text;
      sendChat();
    };
    $('#chatChips').appendChild(btn);
  });

  addMsg('أهلًا! أنا نوفا ✦ مساعدك الشامل: محادثة، رسم صور، صوت، وتحليل ملفات — كل ده في مكان واحد. جرّب تسألني أي حاجة 👇', 'bot');

  const cv = $('#artCanvas');
  const cx = cv.getContext('2d');

  function seedFrom(str) {
    let h = 2166136261;
    for (let i = 0; i < str.length; i++) {
      h ^= str.charCodeAt(i);
      h = Math.imul(h, 16777619);
    }
    return h >>> 0;
  }

  function mulberry32(a) {
    return function () {
      a |= 0;
      a = a + 0x6D2B79F5 | 0;
      let t = Math.imul(a ^ a >>> 15, 1 | a);
      t = t + Math.imul(t ^ t >>> 7, 61 | t) ^ t;
      return ((t ^ t >>> 14) >>> 0) / 4294967296;
    };
  }

  const palettes = {
    abstract: ['#ff6b6b', '#feca57', '#48dbfb', '#ff9ff3', '#54a0ff', '#5f27cd'],
    space: ['#0b1026', '#1b1f3b', '#2d1e4f', '#6c8cff', '#b28dff', '#f0f4ff'],
    nature: ['#0a3d2e', '#1e6f5c', '#3fa98a', '#a8e6cf', '#ffd166', '#f4a261'],
    waves: ['#03254c', '#1167b1', '#187bcd', '#63b3ff', '#d1ecff', '#ff9f6e']
  };

  function drawArt(prompt, style, salt) {
    const rnd = mulberry32(seedFrom(prompt + '|' + style + '|' + salt));
    const W = cv.width, H = cv.height;
    const pal = palettes[style] || palettes.abstract;

    const g = cx.createLinearGradient(0, 0, W, H);
    g.addColorStop(0, pal[0]);
    g.addColorStop(1, pal[1]);
    cx.fillStyle = g;
    cx.fillRect(0, 0, W, H);

    for (let i = 0; i < 14; i++) {
      const x = rnd() * W;
      const y = rnd() * H;
      const r = 60 + rnd() * 220;
      const rg = cx.createRadialGradient(x, y, 0, x, y, r);
      const c = pal[Math.floor(rnd() * pal.length)];
      rg.addColorStop(0, c + 'cc');
      rg.addColorStop(1, c + '00');
      cx.fillStyle = rg;
      cx.beginPath();
      cx.arc(x, y, r, 0, 2 * Math.PI);
      cx.fill();
    }

    cx.globalAlpha = 0.55;
    for (let i = 0; i < 26; i++) {
      cx.strokeStyle = pal[Math.floor(rnd() * pal.length)];
      cx.lineWidth = 1 + rnd() * 5;
      cx.beginPath();
      let x = rnd() * W, y = rnd() * H;
      cx.moveTo(x, y);
      for (let k = 0; k < 4; k++) {
        x += (rnd() - 0.5) * 380;
        y += (rnd() - 0.5) * 280;
        cx.quadraticCurveTo(rnd() * W, rnd() * H, x, y);
      }
      cx.stroke();
    }
    cx.globalAlpha = 1;

    if (style === 'space') {
      for (let i = 0; i < 180; i++) {
        cx.fillStyle = 'rgba(255,255,255,' + (0.3 + rnd() * 0.7) + ')';
        cx.fillRect(rnd() * W, rnd() * H, rnd() < 0.1 ? 2.5 : 1.2, rnd() < 0.1 ? 2.5 : 1.2);
      }
    }

    const img = cx.getImageData(0, 0, W, H);
    const d = img.data;
    for (let i = 0; i < d.length; i += 4) {
      const n = (rnd() - 0.5) * 16;
      d[i] += n;
      d[i + 1] += n;
      d[i + 2] += n;
    }
    cx.putImageData(img, 0, 0);

    cx.fillStyle = 'rgba(255,255,255,.85)';
    cx.font = '600 20px Tahoma';
    cx.textAlign = 'center';
    cx.shadowColor = 'rgba(0,0,0,.6)';
    cx.shadowBlur = 8;
    cx.fillText(prompt.slice(0, 60), W 
                # nova-ai-app
تطبيق ذكاء اصطناعي شامل بالعربية - محادثة، رسم صور، صوت، وتحليل ملفات

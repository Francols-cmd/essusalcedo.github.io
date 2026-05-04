# essusalcedo.github.io
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PyroGuard Attendance — Student Portal</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg:        #08090c;
    --surface:   #0f1117;
    --border:    #1e2130;
    --accent:    #ff4d1c;
    --accent2:   #ff8c42;
    --text:      #e8eaf0;
    --muted:     #5a5f73;
    --success:   #2ecc71;
    --warning:   #f39c12;
    --error:     #e74c3c;
    --font:      'Syne', sans-serif;
    --mono:      'JetBrains Mono', monospace;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: var(--font);
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 0 1rem 4rem;
    background-image:
      radial-gradient(ellipse 80% 40% at 50% 0%, rgba(255,77,28,.08) 0%, transparent 60%),
      repeating-linear-gradient(0deg, transparent, transparent 39px, rgba(255,77,28,.03) 39px, rgba(255,77,28,.03) 40px),
      repeating-linear-gradient(90deg, transparent, transparent 39px, rgba(255,77,28,.03) 39px, rgba(255,77,28,.03) 40px);
  }

  /* ── Header ── */
  header {
    width: 100%; max-width: 480px;
    padding: 2.5rem 0 2rem;
    display: flex; flex-direction: column; align-items: center; gap: .5rem;
    animation: fadeDown .6s ease both;
  }
  .logo {
    display: flex; align-items: center; gap: .75rem;
    font-size: 1.6rem; font-weight: 800; letter-spacing: -.02em;
  }
  .logo .flame {
    width: 36px; height: 36px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border-radius: 8px 8px 14px 14px;
    display: grid; place-items: center;
    font-size: 1.1rem;
    box-shadow: 0 0 20px rgba(255,77,28,.4);
    animation: pulse 2s ease-in-out infinite;
  }
  @keyframes pulse {
    0%,100% { box-shadow: 0 0 20px rgba(255,77,28,.4); }
    50%      { box-shadow: 0 0 36px rgba(255,77,28,.7); }
  }
  .sub { color: var(--muted); font-size: .8rem; font-family: var(--mono); letter-spacing: .08em; }

  /* ── Tabs ── */
  .tabs {
    display: flex; gap: 4px; padding: 4px;
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 12px; margin-bottom: 1.5rem; width: 100%; max-width: 480px;
    animation: fadeDown .6s .1s ease both;
  }
  .tab {
    flex: 1; padding: .55rem; border: none; border-radius: 8px;
    background: transparent; color: var(--muted); font-family: var(--font);
    font-size: .85rem; font-weight: 600; cursor: pointer;
    transition: all .2s;
  }
  .tab.active {
    background: var(--accent); color: #fff;
    box-shadow: 0 2px 12px rgba(255,77,28,.4);
  }

  /* ── Card ── */
  .card {
    width: 100%; max-width: 480px;
    background: var(--surface); border: 1px solid var(--border);
    border-radius: 16px; padding: 1.75rem;
    animation: fadeUp .5s .15s ease both;
  }
  .card h2 {
    font-size: 1.1rem; font-weight: 700; margin-bottom: 1.25rem;
    display: flex; align-items: center; gap: .5rem;
  }
  .card h2 .icon { font-size: 1.2rem; }

  /* ── Form ── */
  .field { margin-bottom: 1rem; }
  label { display: block; font-size: .75rem; font-family: var(--mono); color: var(--muted); margin-bottom: .4rem; letter-spacing: .06em; }
  input[type=text], input[type=date], input[type=password] {
    width: 100%; padding: .7rem .9rem;
    background: var(--bg); border: 1px solid var(--border);
    border-radius: 8px; color: var(--text);
    font-family: var(--mono); font-size: .9rem;
    transition: border-color .2s;
    outline: none;
  }
  input:focus { border-color: var(--accent); box-shadow: 0 0 0 3px rgba(255,77,28,.1); }

  /* ── Buttons ── */
  .btn {
    width: 100%; padding: .8rem;
    border: none; border-radius: 10px;
    font-family: var(--font); font-size: .95rem; font-weight: 700;
    cursor: pointer; transition: all .2s; letter-spacing: .02em;
  }
  .btn-primary {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    color: #fff; box-shadow: 0 4px 16px rgba(255,77,28,.35);
    margin-top: .5rem;
  }
  .btn-primary:hover { transform: translateY(-1px); box-shadow: 0 6px 22px rgba(255,77,28,.5); }
  .btn-primary:active { transform: translateY(0); }
  .btn-primary:disabled { opacity: .5; cursor: not-allowed; transform: none; }

  .btn-secondary {
    background: transparent; color: var(--accent);
    border: 1px solid var(--accent); margin-top: .5rem;
  }
  .btn-secondary:hover { background: rgba(255,77,28,.08); }

  /* ── Status ── */
  #status-box {
    width: 100%; max-width: 480px;
    padding: .85rem 1.1rem;
    border-radius: 10px; margin-top: 1rem;
    font-size: .875rem; font-weight: 600;
    display: none; animation: fadeUp .3s ease both;
  }
  #status-box.success { background: rgba(46,204,113,.12); border: 1px solid rgba(46,204,113,.3); color: var(--success); }
  #status-box.error   { background: rgba(231,76,60,.12);  border: 1px solid rgba(231,76,60,.3);  color: var(--error); }
  #status-box.warning { background: rgba(243,156,18,.12); border: 1px solid rgba(243,156,18,.3); color: var(--warning); }
  #status-box.info    { background: rgba(52,152,219,.12); border: 1px solid rgba(52,152,219,.3); color: #3498db; }

  /* ── Biometric Badge ── */
  .bio-badge {
    display: flex; align-items: center; gap: .75rem;
    padding: .85rem 1rem; border-radius: 10px;
    background: rgba(255,77,28,.06); border: 1px solid rgba(255,77,28,.2);
    margin: .75rem 0; font-size: .85rem;
  }
  .bio-badge .bio-icon { font-size: 1.5rem; }
  .bio-badge .bio-text { flex: 1; }
  .bio-badge .bio-text strong { display: block; font-weight: 700; }
  .bio-badge .bio-text span { color: var(--muted); font-size: .78rem; font-family: var(--mono); }

  /* ── Step indicator ── */
  .steps { display: flex; gap: .4rem; margin-bottom: 1.25rem; }
  .step {
    flex: 1; height: 3px; border-radius: 3px;
    background: var(--border); transition: background .3s;
  }
  .step.done    { background: var(--success); }
  .step.active  { background: var(--accent); }

  /* ── Loader ── */
  .spinner {
    display: inline-block; width: 16px; height: 16px;
    border: 2px solid rgba(255,255,255,.3); border-top-color: #fff;
    border-radius: 50%; animation: spin .7s linear infinite; margin-right: .5rem;
  }
  @keyframes spin { to { transform: rotate(360deg); } }

  /* ── Geo indicator ── */
  .geo-row {
    display: flex; align-items: center; gap: .5rem;
    font-family: var(--mono); font-size: .78rem; color: var(--muted);
    margin-top: .75rem;
  }
  .geo-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--muted); flex-shrink: 0; }
  .geo-dot.ok   { background: var(--success); box-shadow: 0 0 6px var(--success); }
  .geo-dot.bad  { background: var(--error);   box-shadow: 0 0 6px var(--error); }
  .geo-dot.spin { animation: spin .8s linear infinite; border: 2px solid var(--muted); background: transparent; }

  /* ── Animations ── */
  @keyframes fadeDown { from { opacity:0; transform:translateY(-14px); } to { opacity:1; transform:none; } }
  @keyframes fadeUp   { from { opacity:0; transform:translateY(14px);  } to { opacity:1; transform:none; } }

  .hidden { display: none !important; }
</style>
</head>
<body>

<header>
  <div class="logo"><div class="flame">🔥</div> PyroGuard</div>
  <div class="sub">BIOMETRIC ATTENDANCE SYSTEM · STUDENT PORTAL</div>
</header>

<div class="tabs">
  <button class="tab active" onclick="switchTab('register')">Register</button>
  <button class="tab"        onclick="switchTab('attend')">Mark Attendance</button>
</div>

<!-- ── REGISTER CARD ── -->
<div class="card" id="tab-register">
  <h2><span class="icon">🪪</span> Create Account</h2>

  <div class="steps">
    <div class="step active"  id="s1"></div>
    <div class="step"         id="s2"></div>
    <div class="step"         id="s3"></div>
  </div>

  <div id="step-profile">
    <div class="field"><label>FULL NAME</label><input type="text" id="reg-name" placeholder="e.g. Maria Santos"></div>
    <div class="field"><label>SCHOOL ID</label><input type="text" id="reg-sid"  placeholder="e.g. 2024-00123"></div>
    <div class="field"><label>DATE OF BIRTH</label><input type="date" id="reg-dob"></div>
    <button class="btn btn-primary" onclick="submitProfile()">Continue →</button>
  </div>

  <div id="step-biometric" class="hidden">
    <div class="bio-badge">
      <span class="bio-icon">👆</span>
      <div class="bio-text">
        <strong>Register Biometric</strong>
        <span>Fingerprint · Face ID · Device PIN</span>
      </div>
    </div>
    <p style="font-size:.82rem;color:var(--muted);margin-bottom:1rem;line-height:1.6;">
      Your biometric never leaves this device. WebAuthn stores only a cryptographic key linked to your school ID.
    </p>
    <button class="btn btn-primary" id="bio-reg-btn" onclick="startBiometricRegistration()">
      Scan Biometric
    </button>
    <button class="btn btn-secondary" onclick="goStep(1)">← Back</button>
  </div>

  <div id="step-done" class="hidden" style="text-align:center;padding:1rem 0;">
    <div style="font-size:3rem;margin-bottom:.75rem;">✅</div>
    <strong style="font-size:1.1rem;">Registration Complete</strong>
    <p style="color:var(--muted);font-size:.85rem;margin-top:.5rem;">You can now mark attendance using biometrics.</p>
    <button class="btn btn-secondary" style="margin-top:1.25rem;" onclick="switchTab('attend')">Go to Attendance →</button>
  </div>
</div>

<!-- ── ATTENDANCE CARD ── -->
<div class="card hidden" id="tab-attend">
  <h2><span class="icon">📍</span> Mark Attendance</h2>

  <div class="field"><label>SCHOOL ID</label><input type="text" id="att-sid"   placeholder="Your school ID"></div>
  <div class="field"><label>EVENT CODE</label><input type="text" id="att-code"  placeholder="Given by your teacher" style="text-transform:uppercase"></div>

  <div class="geo-row">
    <div class="geo-dot spin" id="geo-dot"></div>
    <span id="geo-label">Acquiring location…</span>
  </div>

  <button class="btn btn-primary" id="att-btn" onclick="verifyAndMark()" style="margin-top:1rem;">
    Scan Biometric to Confirm
  </button>
</div>

<div id="status-box"></div>

<script>
// ── State ────────────────────────────────────────────────────────────────────
let gpsCoords = null;
let macAddress = null;

// ── Geo ──────────────────────────────────────────────────────────────────────
function initGeo() {
  if (!navigator.geolocation) { setGeo(false, 'Geolocation unavailable'); return; }
  navigator.geolocation.watchPosition(
    pos => {
      gpsCoords = { lat: pos.coords.latitude, lon: pos.coords.longitude };
      setGeo(true, `${pos.coords.latitude.toFixed(5)}, ${pos.coords.longitude.toFixed(5)}`);
    },
    () => setGeo(false, 'Location access denied'),
    { enableHighAccuracy: true }
  );
}
function setGeo(ok, msg) {
  const dot = document.getElementById('geo-dot');
  const lbl = document.getElementById('geo-label');
  dot.className = 'geo-dot ' + (ok ? 'ok' : 'bad');
  if (lbl) lbl.textContent = msg;
}

// Simulated MAC retrieval (browser cannot access real MACs; use a local bridge/agent in production)
function getMac() {
  const stored = localStorage.getItem('device_fingerprint');
  if (stored) return stored;
  const fake = Array.from({length:6}, () => Math.floor(Math.random()*256).toString(16).padStart(2,'0')).join(':');
  localStorage.setItem('device_fingerprint', fake);
  return fake;
}

// ── Tab switching ─────────────────────────────────────────────────────────────
function switchTab(tab) {
  document.getElementById('tab-register').classList.toggle('hidden', tab !== 'register');
  document.getElementById('tab-attend').classList.toggle('hidden', tab !== 'attend');
  document.querySelectorAll('.tab').forEach((t,i) =>
    t.classList.toggle('active', (i===0) === (tab==='register'))
  );
  clearStatus();
}

// ── Status ───────────────────────────────────────────────────────────────────
function showStatus(msg, type='info') {
  const box = document.getElementById('status-box');
  box.textContent = msg;
  box.className = type;
  box.style.display = 'block';
}
function clearStatus() {
  const box = document.getElementById('status-box');
  box.style.display = 'none';
  box.className = '';
}

// ── Step management ───────────────────────────────────────────────────────────
function goStep(n) {
  ['step-profile','step-biometric','step-done'].forEach((id,i) =>
    document.getElementById(id).classList.toggle('hidden', i+1 !== n)
  );
  ['s1','s2','s3'].forEach((id,i) => {
    const el = document.getElementById(id);
    el.className = 'step ' + (i+1 < n ? 'done' : i+1 === n ? 'active' : '');
  });
}

// ── Profile submission ────────────────────────────────────────────────────────
async function submitProfile() {
  const name = document.getElementById('reg-name').value.trim();
  const sid  = document.getElementById('reg-sid').value.trim();
  const dob  = document.getElementById('reg-dob').value;

  if (!name || !sid || !dob) { showStatus('Please fill in all fields.', 'error'); return; }

  macAddress = getMac();
  clearStatus();
  showStatus('Creating account…', 'info');

  try {
    const res  = await fetch('/register', {
      method: 'POST',
      headers: {'Content-Type':'application/json'},
      body: JSON.stringify({ name, school_id: sid, dob, mac: macAddress })
    });
    const data = await res.json();

    if (data.status === 'success') {
      clearStatus();
      goStep(2);
    } else if (data.status === 'warning') {
      showStatus('⚠ ' + data.message, 'warning');
    } else {
      showStatus('✗ ' + data.message, 'error');
    }
  } catch(e) {
    showStatus('Network error. Try again.', 'error');
  }
}

// ── WebAuthn Registration ─────────────────────────────────────────────────────
async function startBiometricRegistration() {
  const sid  = document.getElementById('reg-sid').value.trim();
  const name = document.getElementById('reg-name').value.trim();
  const btn  = document.getElementById('bio-reg-btn');

  btn.disabled = true;
  btn.innerHTML = '<span class="spinner"></span>Waiting for biometric…';
  clearStatus();

  try {
    // 1. Get options from server
    const optRes  = await fetch('/webauthn/register/options', {
      method: 'POST',
      headers: {'Content-Type':'application/json'},
      body: JSON.stringify({ school_id: sid, name })
    });
    const options = await optRes.json();

    // 2. Decode base64url challenge
    const challenge = Uint8Array.from(atob(options.challenge.replace(/-/g,'+').replace(/_/g,'/')), c => c.charCodeAt(0));
    const userId    = Uint8Array.from(atob(options.user.id.replace(/-/g,'+').replace(/_/g,'/')), c => c.charCodeAt(0));

    // 3. Create credential (triggers device biometric)
    const credential = await navigator.credentials.create({ publicKey: {
      challenge,
      rp:               options.rp,
      user:             { id: userId, name: options.user.name, displayName: options.user.displayName },
      pubKeyCredParams: options.pubKeyCredParams,
      authenticatorSelection: options.authenticatorSelection,
      timeout:          options.timeout,
      attestation:      options.attestation
    }});

    // 4. Send to server
    const credData = {
      id:    credential.id,
      rawId: btoa(String.fromCharCode(...new Uint8Array(credential.rawId))),
      type:  credential.type
    };

    const verRes  = await fetch('/webauthn/register/verify', {
      method: 'POST',
      headers: {'Content-Type':'application/json'},
      body: JSON.stringify(credData)
    });
    const verData = await verRes.json();

    if (verData.status === 'success') {
      goStep(3);
    } else {
      showStatus('✗ ' + verData.message, 'error');
    }
  } catch(e) {
    if (e.name === 'NotAllowedError') {
      showStatus('Biometric scan cancelled or timed out.', 'warning');
    } else if (e.name === 'InvalidStateError') {
      showStatus('This device already has a credential registered.', 'warning');
    } else {
      showStatus('WebAuthn error: ' + e.message, 'error');
    }
  } finally {
    btn.disabled = false;
    btn.textContent = 'Scan Biometric';
  }
}

// ── WebAuthn + Attendance ─────────────────────────────────────────────────────
async function verifyAndMark() {
  const sid   = document.getElementById('att-sid').value.trim();
  const code  = document.getElementById('att-code').value.trim().toUpperCase();
  const btn   = document.getElementById('att-btn');

  if (!sid || !code) { showStatus('Enter your School ID and Event Code.', 'error'); return; }
  if (!gpsCoords)    { showStatus('Location not acquired yet. Please wait…', 'warning'); return; }

  btn.disabled = true;
  btn.innerHTML = '<span class="spinner"></span>Biometric scan…';
  clearStatus();

  try {
    // 1. Get auth options
    const optRes  = await fetch('/webauthn/auth/options', {
      method: 'POST',
      headers: {'Content-Type':'application/json'},
      body: JSON.stringify({ school_id: sid })
    });
    const options = await optRes.json();
    if (options.status === 'error') { showStatus('✗ ' + options.message, 'error'); return; }

    const challenge = Uint8Array.from(atob(options.challenge.replace(/-/g,'+').replace(/_/g,'/')), c => c.charCodeAt(0));
    const credId    = Uint8Array.from(atob(options.allowCredentials[0].id.replace(/-/g,'+').replace(/_/g,'/')), c => c.charCodeAt(0));

    // 2. Get assertion (biometric prompt)
    const assertion = await navigator.credentials.get({ publicKey: {
      challenge,
      rpId:              options.rpId,
      allowCredentials:  [{ type: 'public-key', id: credId, transports: ['internal'] }],
      userVerification:  'required',
      timeout:           options.timeout
    }});

    // 3. Verify assertion
    const assertData = {
      id:              assertion.id,
      rawId:           btoa(String.fromCharCode(...new Uint8Array(assertion.rawId))),
      type:            assertion.type,
      authenticatorData: btoa(String.fromCharCode(...new Uint8Array(assertion.response.authenticatorData))),
      clientDataJSON:    btoa(String.fromCharCode(...new Uint8Array(assertion.response.clientDataJSON))),
      signature:         btoa(String.fromCharCode(...new Uint8Array(assertion.response.signature)))
    };
    const verRes  = await fetch('/webauthn/auth/verify', {
      method: 'POST',
      headers: {'Content-Type':'application/json'},
      body: JSON.stringify(assertData)
    });
    const verData = await verRes.json();
    if (verData.status !== 'success') { showStatus('✗ Biometric verification failed.', 'error'); return; }

    // 4. Mark attendance
    const attRes  = await fetch('/mark_attendance', {
      method: 'POST',
      headers: {'Content-Type':'application/json'},
      body: JSON.stringify({
        school_id:  sid,
        event_code: code,
        lat: gpsCoords.lat,
        lon: gpsCoords.lon,
        mac: getMac()
      })
    });
    const attData = await attRes.json();

    if (attData.status === 'success') {
      showStatus('✓ ' + attData.detail, 'success');
      document.getElementById('att-code').value = '';
    } else if (attData.status === 'warning') {
      showStatus('⚠ ' + attData.message, 'warning');
    } else {
      showStatus('✗ ' + attData.message, 'error');
    }
  } catch(e) {
    if (e.name === 'NotAllowedError') {
      showStatus('Biometric scan cancelled.', 'warning');
    } else {
      showStatus('Error: ' + e.message, 'error');
    }
  } finally {
    btn.disabled = false;
    btn.textContent = 'Scan Biometric to Confirm';
  }
}

// ── Init ──────────────────────────────────────────────────────────────────────
initGeo();
goStep(1);
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Emergency App Prototype</title>
  <style>
    :root {
      --primary: #d32f2f;
      --accent: #ffc107;
      --bg: #fafafa;
      --card-bg: #fff;
      --shadow: 0 4px 16px rgba(0,0,0,0.09);
      --radius: 22px;
      --input-bg: #f5f5f5;
      --border: #e0e0e0;
      --btn: #d32f2f;
      --btn-hover: #b71c1c;
      --btn-secondary: #1565c0;
      --btn-secondary-hover: #003c8f;
    }
    body {
      background: var(--bg);
      font-family: 'Segoe UI', Arial, sans-serif;
      min-height: 100vh;
      margin: 0;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .container {
      background: var(--card-bg);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 2rem 1.2rem 1.6rem 1.2rem;
      width: 100%;
      max-width: 390px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 1.3rem;
    }
    .title {
      font-size: 1.4rem;
      font-weight: 700;
      color: var(--primary);
      margin-bottom: 0.6rem;
      text-align: center;
    }
    .sos-btn {
      background: var(--btn);
      color: #fff;
      font-size: 1.3rem;
      font-weight: bold;
      border: none;
      border-radius: 50px;
      padding: 1.1rem 2.9rem;
      box-shadow: 0 2px 8px rgba(211,47,47,0.14);
      cursor: pointer;
      transition: background 0.2s;
      margin-bottom: 0.2rem;
      letter-spacing: 0.03em;
    }
    .sos-btn:active,
    .sos-btn:focus {
      background: var(--btn-hover);
      outline: none;
    }
    .alert-box {
      display: none;
      background: var(--accent);
      color: #333;
      border-radius: 14px;
      padding: 0.85rem 1.2rem;
      font-size: 1rem;
      font-weight: 500;
      margin-bottom: -0.5rem;
      box-shadow: 0 2px 6px rgba(255,193,7,0.13);
      text-align: center;
      animation: alertFade 2.5s;
      position: absolute;
      left: 50%;
      top: 2.3rem;
      transform: translateX(-50%);
      min-width: 220px;
      z-index: 999;
    }
    @keyframes alertFade {
      0% { opacity: 0; }
      10% { opacity: 1; }
      90% { opacity: 1; }
      100% { opacity: 0; }
    }
    .dropdown-section,
    .input-section,
    .buttons-section {
      width: 100%;
      display: flex;
      flex-direction: column;
      gap: 1rem;
    }
    .dropdown-label {
      font-size: 1rem;
      font-weight: 500;
      color: #444;
      margin-bottom: 0.35rem;
    }
    select {
      width: 100%;
      padding: 0.6rem 0.8rem;
      border-radius: 11px;
      border: 1px solid var(--border);
      background: var(--input-bg);
      font-size: 1rem;
      outline: none;
      transition: border 0.18s;
    }
    select:focus {
      border: 1.5px solid var(--primary);
    }
    .button-group {
      display: flex;
      gap: 0.6rem;
      flex-wrap: wrap;
      justify-content: center;
      margin-top: 0.2rem;
    }
    .mini-btn {
      flex: 1 1 40%;
      min-width: 44%;
      background: var(--btn-secondary);
      color: #fff;
      border: none;
      border-radius: 20px;
      padding: 0.65rem 0.7rem;
      font-size: 0.97rem;
      font-weight: 500;
      margin-bottom: 0.2rem;
      cursor: pointer;
      transition: background 0.18s;
      box-shadow: 0 1.5px 6px rgba(21,101,192,0.09);
    }
    .mini-btn:hover,
    .mini-btn:focus {
      background: var(--btn-secondary-hover);
      outline: none;
    }
    .mini-btn.silent {
      background: #444;
    }
    .mini-btn.silent:hover {
      background: #111;
    }
    .input-row {
      display: flex;
      flex-direction: column;
      gap: 0.32rem;
    }
    .input-label {
      font-size: 0.98rem;
      color: #555;
      font-weight: 500;
    }
    .input-field {
      width: 100%;
      padding: 0.65rem 0.9rem;
      border-radius: 10px;
      border: 1px solid var(--border);
      background: var(--input-bg);
      font-size: 1rem;
      outline: none;
      margin-bottom: 0.1rem;
      transition: border 0.18s;
    }
    .input-field:focus {
      border: 1.5px solid var(--primary);
    }
    .auth-row {
      display: flex;
      gap: 0.7rem;
      align-items: center;
      margin-top: 0.2rem;
    }
    .pin-input {
      flex: 1;
    }
    .biometric-placeholder {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      color: #888;
      font-size: 0.98rem;
      background: #f0f0f0;
      border-radius: 10px;
      padding: 0.6rem 0.85rem;
      border: 1px dashed #bbb;
      cursor: pointer;
      transition: border 0.18s;
    }
    .biometric-placeholder:active,
    .biometric-placeholder:focus {
      border: 1.5px solid var(--primary);
      outline: none;
    }
    .biometric-icon {
      font-size: 1.13rem;
      color: #b71c1c;
    }
    .sim-note {
      margin-top: 1.2rem;
      color: #999;
      font-size: 0.99rem;
      text-align: center;
      line-height: 1.5;
      background: #f7f7f7;
      border-radius: 11px;
      padding: 0.75rem 1.1rem 0.6rem 1.1rem;
    }
    @media (max-width: 480px) {
      .container {
        max-width: 97vw;
        padding: 1.1rem 0.3rem 1.2rem 0.3rem;
      }
      .alert-box {
        min-width: 150px;
        font-size: 0.95rem;
        top: 1.1rem;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="title">Emergency App Prototype</div>

    <!-- Alert Box -->
    <div id="alertBox" class="alert-box">🚨 Emergency Alert Sent!</div>

    <!-- SOS Button -->
    <button class="sos-btn" id="sosBtn">PANIC / SOS</button>

    <!-- Emergency Type Dropdown -->
    <div class="dropdown-section">
      <label class="dropdown-label" for="emType">Select Emergency Type:</label>
      <select id="emType">
        <option value="medical">Medical</option>
        <option value="fire">Fire</option>
        <option value="police">Police</option>
        <option value="disaster">Natural Disaster</option>
      </select>
    </div>

    <!-- Action Buttons -->
    <div class="buttons-section">
      <div class="button-group">
        <button class="mini-btn" id="shareLocBtn">Share Location</button>
        <button class="mini-btn" id="chatBtn">Start Chat</button>
      </div>
      <div class="button-group">
        <button class="mini-btn silent" id="silentBtn">Silent Alert Mode</button>
        <button class="mini-btn" id="syncBtn">Sync with Kiosk</button>
      </div>
    </div>

    <!-- Input Fields -->
    <div class="input-section">
      <div class="input-row">
        <label class="input-label" for="medInfo">Medical Info</label>
        <input class="input-field" id="medInfo" type="text" placeholder="e.g. Allergies, Blood Type">
      </div>
      <div class="input-row">
        <label class="input-label" for="contact">Emergency Contact Number</label>
        <input class="input-field" id="contact" type="tel" placeholder="e.g. +1234567890">
      </div>
      <div class="input-row">
        <label class="input-label" for="pin">Authentication</label>
        <div class="auth-row">
          <input class="input-field pin-input" id="pin" type="password" maxlength="6" placeholder="PIN">
          <div class="biometric-placeholder" tabindex="0">
            <span class="biometric-icon">🔒</span> Biometric
          </div>
        </div>
      </div>
    </div>

    <!-- Simulation Note -->
    <div class="sim-note">
      <b>Feature Simulations:</b> Multi-language support, offline mode, incident history, and more features simulated.
    </div>
  </div>
  <script>
    // Alert box logic
    const sosBtn = document.getElementById('sosBtn');
    const alertBox = document.getElementById('alertBox');
    let alertTimeout = null;

    sosBtn.addEventListener('click', () => {
      alertBox.style.display = 'block';
      alertBox.classList.remove('hide');
      clearTimeout(alertTimeout);
      alertTimeout = setTimeout(() => {
        alertBox.style.display = 'none';
      }, 2100);
    });

    // Simulated feedback for other buttons
    function feedback(msg) {
      alertBox.textContent = msg;
      alertBox.style.display = 'block';
      clearTimeout(alertTimeout);
      alertTimeout = setTimeout(() => {
        alertBox.style.display = 'none';
        alertBox.textContent = '🚨 Emergency Alert Sent!';
      }, 1700);
    }

    document.getElementById('shareLocBtn').addEventListener('click', () => {
      feedback('📍 Location Shared (simulated)');
    });
    document.getElementById('chatBtn').addEventListener('click', () => {
      feedback('💬 Chat Started (simulated)');
    });
    document.getElementById('silentBtn').addEventListener('click', () => {
      feedback('🔕 Silent Alert Activated (simulated)');
    });
    document.getElementById('syncBtn').addEventListener('click', () => {
      feedback('🔄 Sync with Kiosk (QR) simulated');
    });

    // Biometric placeholder feedback
    document.querySelector('.biometric-placeholder').addEventListener('click', () => {
      feedback('🔒 Biometric Authentication (simulated)');
    });
    document.querySelector('.biometric-placeholder').addEventListener('keydown', (e) => {
      if (e.key === 'Enter' || e.key === ' ') {
        feedback('🔒 Biometric Authentication (simulated)');
      }
    });
  </script>
</body>
</html>

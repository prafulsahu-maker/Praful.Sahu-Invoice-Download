<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Invoice Download Portal</title>
  <style>
    :root {
      --primary: #2874f0;
      --primary-hover: #1257c7;
      --background: #f1f3f6;
      --text: #212121;
      --muted: #6b7280;
      --border: #e0e0e0;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
    }

    body {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      background: var(--background);
      color: var(--text);
    }

    .top-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 12px 24px;
      background: #fff;
      border-bottom: 1px solid var(--border);
      color: var(--muted);
      font-size: 13px;
    }

    .live-clock {
      color: var(--primary);
      font-weight: 600;
    }

    header {
      padding: 32px 20px;
      background: var(--primary);
      color: #fff;
      text-align: center;
    }

    header h1 {
      font-size: 26px;
    }

    header p {
      margin-top: 8px;
      font-size: 14px;
      opacity: 0.92;
    }

    main {
      width: min(100% - 32px, 560px);
      margin: 48px auto;
      flex: 1;
    }

    .card {
      padding: 28px;
      background: #fff;
      border: 1px solid var(--border);
      border-radius: 8px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
    }

    .card h2 {
      margin-bottom: 8px;
      font-size: 19px;
    }

    .description {
      margin-bottom: 24px;
      color: var(--muted);
      font-size: 14px;
      line-height: 1.5;
    }

    .form-group {
      display: grid;
      gap: 10px;
    }

    label {
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 0.5px;
      text-transform: uppercase;
      color: var(--muted);
    }

    input {
      width: 100%;
      padding: 12px 14px;
      border: 1px solid var(--border);
      border-radius: 4px;
      font-size: 15px;
    }

    input:focus {
      outline: 2px solid rgba(40, 116, 240, 0.2);
      border-color: var(--primary);
    }

    button {
      margin-top: 6px;
      padding: 12px 18px;
      border: 0;
      border-radius: 4px;
      background: var(--primary);
      color: #fff;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
    }

    button:hover {
      background: var(--primary-hover);
    }

    button:focus-visible {
      outline: 3px solid rgba(40, 116, 240, 0.35);
      outline-offset: 2px;
    }

    .hint {
      margin-top: 14px;
      color: var(--muted);
      font-size: 12px;
    }

    footer {
      padding: 16px;
      border-top: 1px solid var(--border);
      background: #fff;
      color: var(--muted);
      text-align: center;
      font-size: 12px;
    }
  </style>
</head>
<body>
  <div class="top-bar">
    <span>Operations Portal</span>
    <time class="live-clock" id="live-time" aria-live="off"></time>
  </div>

  <header>
    <h1>Invoice Download Portal</h1>
    <p>Retrieve an invoice using its Order ID</p>
  </header>

  <main>
    <section class="card" aria-labelledby="form-title">
      <h2 id="form-title">📄 Find an invoice</h2>
      <p class="description">
        Enter the Order ID to open the corresponding invoice document.
      </p>

      <form id="invoice-form">
        <div class="form-group">
          <label for="order-id">Order ID</label>
          <input
            id="order-id"
            name="orderId"
            type="text"
            placeholder="e.g. OD1234567890123"
            autocomplete="off"
            required
          >
          <button type="submit">Open invoice</button>
        </div>
      </form>

      <p class="hint">You must be authorized to access the requested invoice.</p>
    </section>
  </main>

  <footer>
    Internal Operations Portal
  </footer>

  <script>
    function updateClock() {
      document.getElementById("live-time").textContent =
        new Date().toLocaleString();
    }

    updateClock();
    setInterval(updateClock, 1000);

    document.getElementById("invoice-form").addEventListener("submit", (event) => {
      event.preventDefault();

      const orderId = document.getElementById("order-id").value.trim();
      if (!orderId) return;

      // Prefer HTTPS when the invoice service supports it.
      const invoiceUrl =
        `http://10.24.3.22/customer_invoices/orders/${encodeURIComponent(orderId)}/document`;

      window.open(invoiceUrl, "_blank", "noopener,noreferrer");
    });
  </script>
</body>
</html>

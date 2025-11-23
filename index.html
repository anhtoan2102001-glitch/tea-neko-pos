<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Mini POS – Tea Neko (Realtime)</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: -apple-system, BlinkMacSystemFont, Arial, sans-serif;
      padding: 10px;
      background: #f2f2f2;
    }
    .box {
      max-width: 480px;
      margin: 0 auto;
      background: #fff;
      border-radius: 16px;
      padding: 14px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.12);
    }
    h1 {
      margin: 0 0 6px;
      text-align: center;
      font-size: 20px;
    }
    .device-row {
      display: flex;
      gap: 8px;
      margin-bottom: 8px;
      align-items: center;
      font-size: 13px;
    }
    .device-row input {
      flex: 1;
      padding: 4px 8px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 13px;
    }
    .menu-section-title {
      margin-top: 8px;
      font-size: 15px;
      font-weight: 600;
      border-left: 4px solid #0a84ff;
      padding-left: 6px;
    }
    .menu-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 8px;
      margin-top: 6px;
    }
    .menu-item {
      border-radius: 12px;
      padding: 8px;
      background: #f5f5f5;
      cursor: pointer;
      border: 1px solid transparent;
      font-size: 14px;
      transition: transform 0.06s ease, box-shadow 0.08s ease, background 0.08s ease;
    }
    .menu-item:active {
      transform: translateY(1px) scale(0.98);
      box-shadow: 0 1px 3px rgba(0,0,0,0.25) inset;
      background: #e8f2ff;
    }
    .menu-item-name {
      font-weight: 600;
    }
    .menu-item-price {
      font-size: 12px;
      color: #555;
      margin-top: 2px;
    }
    .size-row, .qty-row, .cash-row {
      display: flex;
      gap: 8px;
      margin-top: 8px;
      align-items: center;
      font-size: 14px;
    }
    .size-row button {
      flex: 1;
      padding: 6px 0;
      border-radius: 999px;
      border: 1px solid #ccc;
      background: #f5f5f5;
      cursor: pointer;
      font-size: 13px;
      transition: background 0.08s ease, box-shadow 0.08s ease;
    }
    .size-row button.active {
      background: #0a84ff;
      color: #fff;
      border-color: #0a84ff;
      box-shadow: 0 0 0 1px rgba(10,132,255,0.4);
    }
    .qty-row input, .cash-row input {
      flex: 1;
      padding: 6px 8px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 14px;
    }
    .qty-row button {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      border: none;
      background: #eee;
      cursor: pointer;
      font-size: 18px;
    }
    .btn-row {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 8px;
      margin-top: 8px;
    }
    .btn {
      border-radius: 999px;
      border: none;
      padding: 8px 0;
      cursor: pointer;
      font-size: 14px;
      font-weight: 600;
      color: #fff;
      transition: opacity 0.08s ease, transform 0.06s ease, box-shadow 0.08s ease;
    }
    .btn:active {
      opacity: 0.85;
      transform: translateY(1px);
      box-shadow: 0 1px 3px rgba(0,0,0,0.25) inset;
    }
    .btn-undo { background: #8e8e93; }
    .btn-clear { background: #ff3b30; }
    .btn-save { background: #5856d6; }
    .btn-print { background: #34c759; }

    .list-box {
      margin-top: 10px;
      padding: 10px;
      border-radius: 12px;
      background: #fafafa;
      font-size: 14px;
    }
    ul {
      margin: 6px 0 0;
      padding-left: 18px;
      max-height: 220px;
      overflow-y: auto;
      font-size: 13px;
    }
    .summary {
      margin-top: 6px;
      font-size: 14px;
    }
    .summary strong { font-size: 15px; }
    .history-box {
      margin-top: 10px;
      padding: 10px;
      border-radius: 12px;
      background: #ffffff;
      border: 1px solid #e0e0e0;
      font-size: 13px;
    }
    .history-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 4px;
    }
    .history-list {
      max-height: 200px;
      overflow-y: auto;
      margin-top: 4px;
    }
    .history-item {
      border-bottom: 1px dashed #ddd;
      padding: 4px 0;
    }
    .history-total {
      margin-top: 4px;
      font-weight: 600;
    }
    .footer {
      margin-top: 10px;
      text-align: center;
      font-size: 12px;
      color: #777;
    }
  </style>
  <script src="https://unpkg.com/@supabase/supabase-js@2/dist/umd/supabase.js"></script>
</head>
<body>

<div class="box">
  <h1>Mini POS – Tea Neko</h1>

  <div class="device-row">
    <span>Máy:</span>
    <input id="deviceName" placeholder="VD: Mac Quầy 1, iPhone Thu Ngân">
  </div>

  <div class="menu-section-title">LATTE / COFFEE / TRÀ SỮA</div>
  <div class="menu-grid" id="menuMain"></div>

  <div class="menu-section-title">Tùy chọn</div>
  <div class="size-row">
    <button id="sizeM" class="active">Size M</button>
    <button id="sizeL">Size L (+5.000)</button>
  </div>

  <div class="qty-row">
    <span>SL:</span>
    <button id="qtyMinus">−</button>
    <input id="qtyInput" type="number" min="1" value="1">
    <button id="qtyPlus">+</button>
  </div>

  <div class="cash-row">
    <span>Khách đưa (nghìn):</span>
    <input id="cashInput" type="number" min="0" placeholder="VD: 50">
  </div>

  <div class="btn-row">
    <button class="btn btn-undo" id="btnUndo">↩ Hoàn tác</button>
    <button class="btn btn-clear" id="btnClear">Xóa tất cả</button>
  </div>
  <div class="btn-row" style="margin-top:6px;">
    <button class="btn btn-save" id="btnSave">💾 Lưu đơn</button>
    <button class="btn btn-print" id="btnPrint">🧾 Lưu + In bill</button>
  </div>

  <div class="list-box">
    <div><strong>Đơn hiện tại:</strong></div>
    <ul id="currentList"></ul>
    <div class="summary" id="currentSummary">Tổng: 0 VND</div>
    <div class="summary" id="cashSummary"></div>
  </div>

  <div class="history-box">
    <div class="history-header">
      <span><strong>Lịch sử đơn (Realtime)</strong></span>
      <button class="btn btn-undo" id="btnRefreshHistory"
              style="padding:4px 10px;font-size:11px;border-radius:999px;">
        ↻ Tải lại
      </button>
    </div>
    <div class="history-list" id="historyList"></div>
    <div class="history-total" id="historyTotal">Tổng doanh thu: 0 VND</div>
  </div>

  <div class="footer">Cảm ơn quý khách đã ghé Tea Neko 💜</div>
</div>

<script>
  // ============ SUPABASE CONFIG ============
  const SUPABASE_URL = "https://kcrchwedlrettpkucoct.supabase.co";
  const SUPABASE_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImtjcmNod2VkbHJldHRwa3Vjb2N0Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjM4ODQ0MjgsImV4cCI6MjA3OTQ2MDQyOH0.g4WA9tci2zm4MIa6EvOe6tH_EhaoicdrdiP6swgjRgw";
  const supa = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

  // ============ MENU & STATE ============
  const MENU = [
    { name: "Matcha Latte",       price: 25000 },
    { name: "Coffee",             price: 25000 },
    { name: "Trà sữa trân châu",  price: 30000 },
    { name: "Hồng trà sữa",       price: 28000 },
    { name: "Cacao đá",           price: 22000 },
    { name: "Bạc xỉu",            price: 20000 }
  ];

  let currentOrder = [];
  let currentSize = "M";
  let historyOrders = [];

  // DOM
  const menuMain = document.getElementById("menuMain");
  const sizeMBtn = document.getElementById("sizeM");
  const sizeLBtn = document.getElementById("sizeL");
  const qtyInput = document.getElementById("qtyInput");
  const qtyMinus = document.getElementById("qtyMinus");
  const qtyPlus = document.getElementById("qtyPlus");
  const cashInput = document.getElementById("cashInput");
  const currentList = document.getElementById("currentList");
  const currentSummary = document.getElementById("currentSummary");
  const cashSummary = document.getElementById("cashSummary");
  const btnUndo = document.getElementById("btnUndo");
  const btnClear = document.getElementById("btnClear");
  const btnSave = document.getElementById("btnSave");
  const btnPrint = document.getElementById("btnPrint");
  const btnRefreshHistory = document.getElementById("btnRefreshHistory");
  const historyList = document.getElementById("historyList");
  const historyTotal = document.getElementById("historyTotal");
  const deviceNameInput = document.getElementById("deviceName");

  function formatVND(x) {
    return x.toLocaleString("vi-VN") + " VND";
  }

  // ============ MENU UI ============
  function renderMenu() {
    MENU.forEach(item => {
      const div = document.createElement("div");
      div.className = "menu-item";
      div.innerHTML = `
        <div class="menu-item-name">${item.name}</div>
        <div class="menu-item-price">${item.price.toLocaleString("vi-VN")} VND (Size M)</div>
      `;
      div.addEventListener("click", () => addItem(item));
      menuMain.appendChild(div);
    });
  }

  function addItem(item) {
    const qty = Math.max(1, parseInt(qtyInput.value || "1", 10));
    const isL = currentSize === "L";
    const unitPrice = item.price + (isL ? 5000 : 0);
    const lineTotal = unitPrice * qty;

    currentOrder.push({
      name: item.name,
      size: currentSize,
      qty,
      unitPrice,
      lineTotal
    });

    renderCurrentOrder();
  }

  // ============ CURRENT ORDER ============
  function renderCurrentOrder() {
    currentList.innerHTML = "";
    let total = 0;
    currentOrder.forEach(line => {
      total += line.lineTotal;
      const li = document.createElement("li");
      li.textContent = `${line.qty} x ${line.name} (Size ${line.size}) – ${formatVND(line.lineTotal)}`;
      currentList.appendChild(li);
    });
    currentSummary.innerHTML = `<strong>Tổng:</strong> ${formatVND(total)}`;

    const cashThousand = parseInt(cashInput.value || "0", 10);
    const cash = cashThousand * 1000;
    if (cash > 0) {
      const diff = cash - total;
      cashSummary.textContent =
        `Khách đưa: ${formatVND(cash)} – ` +
        `Thối lại: ${formatVND(Math.max(diff, 0))}`;
    } else {
      cashSummary.textContent = "";
    }
  }

  function clearCurrentOrder() {
    currentOrder = [];
    cashInput.value = "";
    renderCurrentOrder();
  }

  // ============ HISTORY ============
  async function loadHistory() {
    const { data, error } = await supa
      .from("orders")
      .select("*")
      .order("created_at", { ascending: false })
      .limit(100);

    if (error) {
      console.error(error);
      alert("Không tải được lịch sử từ Supabase");
      return;
    }
    historyOrders = data || [];
    renderHistory();
  }

  function renderHistory() {
    historyList.innerHTML = "";
    let revenue = 0;
    historyOrders.forEach(order => {
      revenue += order.total || 0;
      const div = document.createElement("div");
      div.className = "history-item";

      const timeStr = order.created_at
        ? new Date(order.created_at).toLocaleString("vi-VN")
        : "";

      const itemsText = (order.items || [])
        .map(it => `${it.qty}x ${it.name} (${it.size})`)
        .join(", ");

      div.textContent = `[${timeStr}] (${order.device || "N/A"}) → ${itemsText} = ${formatVND(order.total || 0)}`;
      historyList.appendChild(div);
    });

    historyTotal.textContent = `Tổng doanh thu: ${formatVND(revenue)}`;
  }

  // ============ SAVE + REALTIME ============
  async function saveOrder(printAfter) {
    if (!currentOrder.length) {
      alert("Đơn hiện tại đang trống.");
      return;
    }

    const total = currentOrder.reduce((s, l) => s + l.lineTotal, 0);
    const cashThousand = parseInt(cashInput.value || "0", 10);
    const cash = cashThousand * 1000;
    const change = cash > 0 ? cash - total : null;
    const device = deviceNameInput.value.trim() || "Không đặt tên";

    const payload = {
      device,
      items: currentOrder,
      total,
      cash_given: cash || null,
      change
    };

    const { data, error } = await supa
      .from("orders")
      .insert([payload])
      .select()
      .single();

    if (error) {
      console.error(error);
      alert("Lưu đơn lên Supabase thất bại.");
      return;
    }

    // thêm vào history local (realtime cũng sẽ bắn thêm, nhưng ta cập nhật ngay cho mượt)
    historyOrders.unshift(data);
    renderHistory();

    if (printAfter) {
      printBill(data);
    }

    clearCurrentOrder();
  }

  function initRealtime() {
    supa
      .channel("orders-realtime")
      .on(
        "postgres_changes",
        { event: "INSERT", schema: "public", table: "orders" },
        payload => {
          const newOrder = payload.new;
          historyOrders.unshift(newOrder);
          renderHistory();
        }
      )
      .subscribe();
  }

  // ============ PRINT BILL ============
  function printBill(order) {
    const now = order.created_at
      ? new Date(order.created_at)
      : new Date();
    const timeStr = now.toLocaleString("vi-VN");

    let rows = "";
    (order.items || []).forEach(it => {
      rows += `
        <tr>
          <td>${it.name}</td>
          <td style="text-align:center;">${it.size}</td>
          <td style="text-align:center;">${it.qty}</td>
          <td style="text-align:right;">${formatVND(it.lineTotal)}</td>
        </tr>`;
    });

    const cashStr = order.cash_given ? formatVND(order.cash_given) : "0 VND";
    const changeStr = order.change != null ? formatVND(order.change) : "0 VND";

    const html = `
<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Hoá đơn Tea Neko</title>
<style>
  body { font-family:-apple-system,BlinkMacSystemFont,Arial,sans-serif; margin:0; padding:8px; }
  .bill { width:320px; font-size:12px; }
  h2 { text-align:center; margin:4px 0 2px; font-size:16px; }
  .shop-info { text-align:right; font-size:10px; margin-bottom:6px; }
  table { width:100%; border-collapse:collapse; font-size:11px; }
  th,td { padding:2px 0; }
  th { border-bottom:1px solid #000; }
  .total-row td { border-top:1px dashed #000; padding-top:4px; }
</style>
</head>
<body>
<div class="bill">
  <h2>Tea Neko</h2>
  <div class="shop-info">
    Đ/c: Hai Bà Trưng, Chư Sê, Gia Lai<br>
    SĐT: 0123456789
  </div>
  <div style="font-size:11px;margin-bottom:4px;">
    Thời gian: ${timeStr}<br>
    Máy: ${order.device || "N/A"}
  </div>
  <table>
    <thead>
      <tr>
        <th>Món</th>
        <th style="text-align:center;">Size</th>
        <th style="text-align:center;">SL</th>
        <th style="text-align:right;">Thành tiền</th>
      </tr>
    </thead>
    <tbody>
      ${rows}
    </tbody>
    <tfoot>
      <tr class="total-row">
        <td colspan="3"><strong>Tổng:</strong></td>
        <td style="text-align:right;"><strong>${formatVND(order.total || 0)}</strong></td>
      </tr>
      <tr>
        <td colspan="3">Khách đưa:</td>
        <td style="text-align:right;">${cashStr}</td>
      </tr>
      <tr>
        <td colspan="3">Tiền thối:</td>
        <td style="text-align:right;">${changeStr}</td>
      </tr>
    </tfoot>
  </table>
  <div style="text-align:center;margin-top:6px;font-size:11px;">
    Cảm ơn quý khách đã ghé Tea Neko 💜
  </div>
</div>
</body>
</html>`;

    const win = window.open("", "_blank", "width=400,height=600");
    win.document.write(html);
    win.document.close();
    win.focus();
    win.print();
  }

  // ============ EVENT BINDINGS ============
  sizeMBtn.addEventListener("click", () => {
    currentSize = "M";
    sizeMBtn.classList.add("active");
    sizeLBtn.classList.remove("active");
  });
  sizeLBtn.addEventListener("click", () => {
    currentSize = "L";
    sizeLBtn.classList.add("active");
    sizeMBtn.classList.remove("active");
  });
  qtyMinus.addEventListener("click", () => {
    const v = Math.max(1, parseInt(qtyInput.value || "1", 10) - 1);
    qtyInput.value = v;
  });
  qtyPlus.addEventListener("click", () => {
    const v = Math.max(1, parseInt(qtyInput.value || "1", 10) + 1);
    qtyInput.value = v;
  });
  qtyInput.addEventListener("change", () => {
    if (!qtyInput.value || qtyInput.value <= 0) qtyInput.value = 1;
  });
  cashInput.addEventListener("input", () => {
    renderCurrentOrder();
  });
  btnUndo.addEventListener("click", () => {
    currentOrder.pop();
    renderCurrentOrder();
  });
  btnClear.addEventListener("click", () => {
    if (!currentOrder.length) return;
    if (!confirm("Xoá toàn bộ món trong đơn hiện tại?")) return;
    clearCurrentOrder();
  });
  btnSave.addEventListener("click", () => saveOrder(false));
  btnPrint.addEventListener("click", () => saveOrder(true));
  btnRefreshHistory.addEventListener("click", () => loadHistory());

  // ============ INIT ============
  renderMenu();
  renderCurrentOrder();
  loadHistory();
  initRealtime();
</script>

</body>
</html>

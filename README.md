<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Mini POS – Tea Neko (Realtime V4)</title>
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
      transition: .1s;
    }
    .menu-item:active {
      transform: scale(0.97);
      background: #e8f2ff;
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
    }
    .size-row button.active {
      background: #0a84ff;
      color: #fff;
      border-color: #0a84ff;
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
    }
    .btn-undo { background: #8e8e93; }
    .btn-clear { background: #ff3b30; }
    .btn-save { background: #5856d6; }
    .btn-print { background: #34c759; }
    .btn-delete { background: #ff3b30; float:right; }

    .list-box {
      margin-top: 10px;
      padding: 10px;
      border-radius: 12px;
      background: #fafafa;
      font-size: 14px;
    }

    .history-box {
      margin-top: 10px;
      padding: 10px;
      border-radius: 12px;
      background: #ffffff;
      border: 1px solid #e0e0e0;
      font-size: 13px;
    }
    .history-item {
      border-bottom: 1px dashed #ddd;
      padding: 4px 0;
      position: relative;
    }
    .delete-x {
      position: absolute;
      right: 0;
      top: 0;
      padding: 0 6px;
      background: #ff3b30;
      color: #fff;
      border-radius: 4px;
      cursor: pointer;
      font-size: 11px;
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
    <button class="btn btn-print" id="btnPrint">🧾 Lưu + In</button>
  </div>

  <div class="list-box">
    <div><strong>Đơn hiện tại:</strong></div>
    <ul id="currentList"></ul>
    <div id="currentSummary">Tổng: 0 VND</div>
    <div id="cashSummary"></div>
  </div>

  <div class="history-box">
    <div style="display:flex;justify-content:space-between;">
      <strong>Lịch sử đơn</strong>
      <button id="btnRefreshHistory" class="btn btn-undo" style="padding:4px 10px;font-size:11px;">↻</button>
    </div>
    <div id="historyList"></div>
    <div id="historyTotal">Tổng doanh thu: 0 VND</div>
  </div>
</div>
<script>
/* ===============================
   SUPABASE CONFIG
================================ */
const SUPABASE_URL = "https://kcrchwedlrettpkucoct.supabase.co";
const SUPABASE_KEY =
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImtjcmNod2VkbHJldHRwa3Vjb2N0Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjM4ODQ0MjgsImV4cCI6MjA3OTQ2MDQyOH0.g4WA9tci2zm4MIa6EvOe6tH_EhaoicdrdiP6swgjRgw";

const supa = supabase.createClient(SUPABASE_URL, SUPABASE_KEY);

/* ===============================
   MENU
================================ */
const MENU = [
  { name: "Matcha Latte",       price: 25000 },
  { name: "Coffee",             price: 25000 },
  { name: "Trà sữa trân châu",  price: 30000 },
  { name: "Hồng trà sữa",       price: 28000 },
  { name: "Cacao đá",           price: 22000 },
  { name: "Bạc xỉu",            price: 20000 },
];

/* ===============================
   STATE
================================ */
let currentOrder = [];
let currentSize = "M";
let historyOrders = [];

/* ===============================
   DOM
================================ */
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

/* ===============================
   UTIL
================================ */
function formatVND(x) {
  return x.toLocaleString("vi-VN") + " VND";
}

/* ===============================
   RENDER MENU
================================ */
function renderMenu() {
  menuMain.innerHTML = "";
  MENU.forEach(item => {
    const div = document.createElement("div");
    div.className = "menu-item";
    div.innerHTML = `
      <div><strong>${item.name}</strong></div>
      <div>${formatVND(item.price)} (Size M)</div>
    `;
    div.onclick = () => addItem(item);
    menuMain.appendChild(div);
  });
}

/* ===============================
   ADD ITEM
================================ */
function addItem(item) {
  const qty = Math.max(1, parseInt(qtyInput.value || "1"));
  const isL = currentSize === "L";
  const unitPrice = item.price + (isL ? 5000 : 0);
  const lineTotal = qty * unitPrice;

  currentOrder.push({
    name: item.name,
    size: currentSize,
    qty,
    unitPrice,
    lineTotal,
  });

  renderCurrentOrder();
}

/* ===============================
   CURRENT ORDER RENDER
================================ */
function renderCurrentOrder() {
  currentList.innerHTML = "";
  let total = 0;

  currentOrder.forEach(it => {
    total += it.lineTotal;
    const li = document.createElement("li");
    li.textContent = `${it.qty} x ${it.name} (Size ${it.size}) – ${formatVND(it.lineTotal)}`;
    currentList.appendChild(li);
  });

  currentSummary.textContent = "Tổng: " + formatVND(total);

  const cashK = parseInt(cashInput.value || "0");
  const cash = cashK * 1000;
  if (cash > 0) {
    cashSummary.textContent =
      `Khách đưa: ${formatVND(cash)} – Thối lại: ${formatVND(Math.max(cash - total, 0))}`;
  } else {
    cashSummary.textContent = "";
  }
}

/* ===============================
   CLEAR ORDER
================================ */
function clearCurrentOrder() {
  currentOrder = [];
  cashInput.value = "";
  renderCurrentOrder();
}
/* =========================================
   SAVE ORDER → INSERT INTO orders
========================================= */
async function saveOrder(printAfter) {
  if (currentOrder.length === 0) {
    alert("Đơn hiện tại đang trống!");
    return;
  }

  const total = currentOrder.reduce((s, it) => s + it.lineTotal, 0);
  const cashK = parseInt(cashInput.value || "0");
  const cash = cashK * 1000;
  const change = cash ? cash - total : null;

  const device = deviceNameInput.value.trim() || "Không đặt tên";

  const payload = {
    device,
    items: currentOrder,
    total,
    cash_given: cash || null,
    change
  };

  // insert → Supabase sẽ tự gán order_code nhờ trigger
  const { data, error } = await supa
    .from("orders")
    .insert([payload])
    .select()
    .single();

  if (error) {
    console.error(error);
    alert("Lưu đơn thất bại!");
    return;
  }

  // Cập nhật UI ngay cho mượt
  historyOrders.unshift(data);
  renderHistory();

  if (printAfter) printBill(data);

  clearCurrentOrder();
}


/* =========================================
   DELETE ORDER → MOVE TO deleted_orders
========================================= */
async function deleteOrder(order) {
  if (!confirm("Bạn chắc chắn muốn xoá đơn này?")) return;

  // đẩy sang deleted_orders
  await supa.from("deleted_orders").insert([{
    original_order_id: order.id,
    order_code: order.order_code,
    device: order.device,
    items: order.items,
    total: order.total,
    cash_given: order.cash_given,
    change: order.change,
    note: "Deleted from POS"
  }]);

  // xoá khỏi bảng orders
  await supa.from("orders").delete().eq("id", order.id);

  loadHistory();
}


/* =========================================
   LOAD HISTORY
========================================= */
async function loadHistory() {
  const { data, error } = await supa
    .from("orders")
    .select("*")
    .order("created_at", { ascending: false });

  if (error) return;

  historyOrders = data || [];
  renderHistory();
}


/* =========================================
   RENDER HISTORY
========================================= */
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

    div.innerHTML = `
      <div>
        <strong>${order.order_code || ""}</strong>
        – [${timeStr}] – (${order.device})<br>
        ${itemsText} = <strong>${formatVND(order.total)}</strong>
      </div>
      <button class="delete-x" onclick='deleteOrder(${JSON.stringify(order)})'>X</button>
    `;

    historyList.appendChild(div);
  });

  historyTotal.textContent = "Tổng doanh thu: " + formatVND(revenue);
}


/* =========================================
   REALTIME SUBSCRIPTION
========================================= */
function initRealtime() {
  supa
    .channel("orders-realtime")
    .on(
      "postgres_changes",
      { event: "INSERT", schema: "public", table: "orders" },
      (payload) => {
        historyOrders.unshift(payload.new);
        renderHistory();
      }
    )
    .subscribe();
}


/* =========================================
   PRINT BILL
========================================= */
function printBill(order) {
  const now = order.created_at ? new Date(order.created_at) : new Date();
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

  const html = `
  <html>
  <head>
  <meta charset="UTF-8">
  <style>
  body { font-family:-apple-system; padding:8px; }
  .bill { width:300px; font-size:12px; }
  h2 { text-align:center; margin:0; font-size:16px; }
  table { width:100%; font-size:11px; }
  </style>
  </head>
  <body>
    <div class="bill">
      <h2>Tea Neko</h2>
      <div style="text-align:right;font-size:10px;">
        Đ/c: Hai Bà Trưng, Chư Sê, Gia Lai<br>
        SĐT: 0123456789
      </div>
      <div>Thời gian: ${timeStr}</div>
      <div>Mã đơn: <strong>${order.order_code}</strong></div>
      <table>
        ${rows}
        <tr><td colspan="3"><strong>Tổng</strong></td>
            <td style="text-align:right;"><strong>${formatVND(order.total)}</strong></td></tr>
      </table>
      <div style="text-align:center;margin-top:5px;">Cảm ơn quý khách 💜</div>
    </div>
  </body>
  </html>
  `;

  const win = window.open("", "_blank", "width=350,height=600");
  win.document.write(html);
  win.document.close();
  win.focus();
  win.print();
}


/* =========================================
   EVENT BINDINGS
========================================= */
sizeMBtn.onclick = () => {
  currentSize = "M";
  sizeMBtn.classList.add("active");
  sizeLBtn.classList.remove("active");
};

sizeLBtn.onclick = () => {
  currentSize = "L";
  sizeLBtn.classList.add("active");
  sizeMBtn.classList.remove("active");
};

qtyMinus.onclick = () => {
  qtyInput.value = Math.max(1, parseInt(qtyInput.value) - 1);
};
qtyPlus.onclick = () => {
  qtyInput.value = Math.max(1, parseInt(qtyInput.value) + 1);
};
cashInput.oninput = renderCurrentOrder;

btnUndo.onclick = () => {
  currentOrder.pop();
  renderCurrentOrder();
};

btnClear.onclick = () => {
  if (confirm("Xóa toàn bộ món hiện tại?")) clearCurrentOrder();
};

btnSave.onclick = () => saveOrder(false);
btnPrint.onclick = () => saveOrder(true);
btnRefreshHistory.onclick = loadHistory;


/* =========================================
   INIT
========================================= */
renderMenu();
renderCurrentOrder();
loadHistory();
initRealtime();

</script>
</body>
</html>

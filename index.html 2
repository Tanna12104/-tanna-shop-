<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>NEXUS TOPUP STORE - ระบบเติมเกมด่วน 24 ชม.</title>
  <!-- Tailwind CSS & FontAwesome -->
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&display=swap');
    * { font-family: 'Kanit', sans-serif; -webkit-tap-highlight-color: transparent; }
    body { background-color: #080c14; color: #f3f4f6; }
    .glass-card {
      background: rgba(15, 23, 42, 0.85);
      backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }
    .active-ring {
      border-color: #06b6d4 !important;
      box-shadow: 0 0 18px rgba(6, 182, 212, 0.35);
    }
  </style>
</head>
<body>

<div class="max-w-md mx-auto p-4 flex flex-col gap-4 pb-12">

  <!-- Header -->
  <div class="glass-card rounded-2xl p-4 text-center border-b border-cyan-500/30 flex justify-between items-center">
    <div class="flex items-center gap-2.5">
      <div class="w-9 h-9 rounded-xl bg-gradient-to-tr from-cyan-500 to-blue-600 flex items-center justify-center shadow-lg shadow-cyan-500/20">
        <i class="fa-solid fa-bolt text-lg text-white"></i>
      </div>
      <div class="text-left">
        <h1 class="font-black text-base bg-clip-text text-transparent bg-gradient-to-r from-cyan-400 to-blue-400">
          NEXUS TOPUP
        </h1>
        <p class="text-[10px] text-gray-400">ระบบสั่งเติมเกมด่วน ⚡ 1-3 นาที</p>
      </div>
    </div>
    
    <span class="px-2.5 py-1 rounded-full bg-emerald-500/10 border border-emerald-500/30 text-[10px] font-bold text-emerald-400 flex items-center gap-1">
      <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-pulse"></span> แอดมินพร้อมเติม
    </span>
  </div>

  <!-- 1. Select Game -->
  <div class="glass-card rounded-2xl p-4">
    <label class="block text-xs font-bold text-cyan-400 mb-2">1. เลือกเกมที่ต้องการเติม</label>
    <div class="grid grid-cols-3 gap-2">
      <button onclick="selectGame('Free Fire')" id="btn-Free Fire" class="game-btn active-ring glass-card p-2.5 rounded-xl flex flex-col items-center gap-1 border border-gray-700">
        <i class="fa-solid fa-fire-flame-curved text-xl text-orange-400"></i>
        <span class="text-[11px] font-bold">Free Fire</span>
      </button>
      <button onclick="selectGame('ROV')" id="btn-ROV" class="game-btn glass-card p-2.5 rounded-xl flex flex-col items-center gap-1 border border-gray-700">
        <i class="fa-solid fa-shield-halved text-xl text-blue-400"></i>
        <span class="text-[11px] font-bold">ROV</span>
      </button>
      <button onclick="selectGame('Valorant')" id="btn-Valorant" class="game-btn glass-card p-2.5 rounded-xl flex flex-col items-center gap-1 border border-gray-700">
        <i class="fa-solid fa-crosshair text-xl text-red-400"></i>
        <span class="text-[11px] font-bold">Valorant</span>
      </button>
    </div>
  </div>

  <!-- 2. Input UID -->
  <div class="glass-card rounded-2xl p-4">
    <label class="block text-xs font-bold text-cyan-400 mb-2">2. ระบุ UID หรือ Player ID</label>
    <input type="text" id="inputUid" placeholder="กรอก UID เช่น 1234884466" class="w-full bg-gray-900 border border-gray-700 rounded-xl px-3 py-2 text-xs text-white focus:outline-none focus:border-cyan-500">
  </div>

  <!-- 3. Select Package -->
  <div class="glass-card rounded-2xl p-4">
    <label class="block text-xs font-bold text-cyan-400 mb-2">3. เลือกแพ็กเกจเติมเงิน</label>
    <div class="grid grid-cols-2 gap-2" id="pkgContainer"></div>
  </div>

  <!-- 4. Pay & Send Order Button -->
  <button onclick="openPaymentModal()" class="w-full py-3.5 rounded-xl bg-gradient-to-r from-cyan-500 via-blue-600 to-indigo-600 font-extrabold text-sm text-white shadow-lg shadow-cyan-500/25 active:scale-95 transition flex items-center justify-center gap-2">
    <i class="fa-solid fa-qrcode"></i> ชำระเงิน & แจ้งแอดมินเติมเงิน
  </button>

</div>

<!-- Payment Modal -->
<div id="payModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
  <div class="glass-card max-w-xs w-full rounded-2xl p-5 text-center flex flex-col items-center border border-gray-700 relative">
    <button onclick="closeModal()" class="absolute top-3 right-3 text-gray-400 text-sm"><i class="fa-solid fa-xmark"></i></button>
    
    <h3 class="font-bold text-sm text-gray-100 mb-1">สแกน QR Code ชำระเงิน</h3>
    <p class="text-[11px] text-gray-400 mb-3">พร้อมเพย์ / ทุกธนาคาร (ยึดตามยอดที่เลือก)</p>

    <!-- Dynamic PromptPay QR Code -->
    <div class="bg-white p-2 rounded-xl mb-3 border border-cyan-500/40">
      <img id="qrImage" src="" alt="PromptPay QR Code" class="w-40 h-40 object-contain">
    </div>

    <!-- Summary Box -->
    <div class="w-full bg-gray-900/80 rounded-xl p-2.5 text-xs text-left mb-3 border border-gray-800 space-y-1">
      <div class="flex justify-between text-gray-400"><span>เกม:</span><b id="summaryGame" class="text-white">-</b></div>
      <div class="flex justify-between text-gray-400"><span>UID:</span><b id="summaryUid" class="text-cyan-400">-</b></div>
      <div class="flex justify-between text-gray-400"><span>แพ็กเกจ:</span><b id="summaryPkg" class="text-white">-</b></div>
      <div class="flex justify-between text-gray-400 border-t border-gray-800 pt-1"><span>ยอดชำระ:</span><b id="summaryPrice" class="text-emerald-400 text-sm">฿0.00</b></div>
    </div>

    <p class="text-[10px] text-amber-300 bg-amber-500/10 border border-amber-500/30 rounded-lg p-1.5 mb-3 w-full">
      <i class="fa-solid fa-triangle-exclamation"></i> โอนแล้วกดปุ่มด้านล่างเพื่อส่งสลิปให้แอดมินทันที
    </p>

    <div class="grid grid-cols-2 gap-2 w-full">
      <button onclick="sendOrder('LINE')" class="py-2.5 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-xs transition flex items-center justify-center gap-1 shadow-md">
        <i class="fa-brands fa-line text-base"></i> ส่งสลิป LINE
      </button>
      <button onclick="sendOrder('FB')" class="py-2.5 rounded-xl bg-blue-600 hover:bg-blue-500 text-white font-bold text-xs transition flex items-center justify-center gap-1 shadow-md">
        <i class="fa-brands fa-facebook-messenger text-base"></i> ส่งสลิป FB
      </button>
    </div>
  </div>
</div>

<script>
  // ==========================================
  // ** แก้ไขเบอร์พร้อมเพย์ และ ลิงก์แชทของคุณตรงนี้ **
  // ==========================================
  const PROMPTPAY_PHONE = "0812345678"; // ใส่เบอร์พร้อมเพย์รับเงินของคุณ
  const MY_LINE_URL = "https://line.me/ti/p/@yourlineid"; // ใส่ลิงก์ LINE ร้านค้า
  const MY_FB_URL = "https://m.me/yourfacebookpage"; // ใส่ลิงก์ Facebook ร้านค้า

  let currentGame = 'Free Fire';
  let selectedPkg = { name: '70 เพชร', price: 30 };

  const packagesData = {
    'Free Fire': [
      { name: '70 เพชร', price: 30 },
      { name: '235 เพชร', price: 100 },
      { name: '355 เพชร', price: 150 },
      { name: '720 เพชร', price: 300 }
    ],
    'ROV': [
      { name: '35 คูปอง', price: 30 },
      { name: '120 คูปอง', price: 100 },
      { name: '370 คูปอง', price: 300 }
    ],
    'Valorant': [
      { name: '475 VP', price: 150 },
      { name: '1000 VP', price: 300 }
    ]
  };

  function renderPackages(game) {
    const container = document.getElementById('pkgContainer');
    const items = packagesData[game] || packagesData['Free Fire'];
    selectedPkg = items[0];

    container.innerHTML = items.map((item, index) => `
      <div onclick="selectPkg(this, '${item.name}', ${item.price})" class="pkg-card cursor-pointer glass-card rounded-xl p-3 border border-gray-700 flex flex-col justify-between ${index === 0 ? 'active-ring' : ''}">
        <span class="text-xs font-bold text-gray-200">${item.name}</span>
        <span class="text-xs font-extrabold text-cyan-400 text-right mt-2">฿${item.price}</span>
      </div>
    `).join('');
  }

  function selectGame(game) {
    currentGame = game;
    document.querySelectorAll('.game-btn').forEach(btn => btn.classList.remove('active-ring'));
    document.getElementById(`btn-${game}`).classList.add('active-ring');
    renderPackages(game);
  }

  function selectPkg(el, name, price) {
    document.querySelectorAll('.pkg-card').forEach(card => card.classList.remove('active-ring'));
    el.classList.add('active-ring');
    selectedPkg = { name, price };
  }

  function openPaymentModal() {
    const uid = document.getElementById('inputUid').value.trim();
    if (!uid) { alert('กรุณากรอก UID ก่อนทำรายการครับ'); return; }

    // ดึง API สร้าง QR Code พร้อมเพย์ตามยอดเงินอัตโนมัติ
    document.getElementById('qrImage').src = `https://promptpay.io/${PROMPTPAY_PHONE}/${selectedPkg.price}.png`;

    document.getElementById('summaryGame').innerText = currentGame;
    document.getElementById('summaryUid').innerText = uid;
    document.getElementById('summaryPkg').innerText = selectedPkg.name;
    document.getElementById('summaryPrice').innerText = `฿${selectedPkg.price}.00`;

    document.getElementById('payModal').classList.remove('hidden');
  }

  function sendOrder(platform) {
    const uid = document.getElementById('inputUid').value.trim();
    const targetUrl = platform === 'LINE' ? MY_LINE_URL : MY_FB_URL;

    confetti({ particleCount: 60, spread: 70, origin: { y: 0.6 } });
    closeModal();

    // ก็อปปี้รายละเอียดคำสั่งซื้อให้อัตโนมัติ
    const orderText = `แจ้งโอนเงินเติมเกม\nเกม: ${currentGame}\nUID: ${uid}\nรายการ: ${selectedPkg.name}\nยอดโอน: ฿${selectedPkg.price}`;
    navigator.clipboard.writeText(orderText);

    alert(`คัดลอกรายการสั่งซื้อแล้ว!\nกำลังเปิดแชทเพื่อให้คุณแนบสลิปและส่งข้อมูลเติมเงินครับ`);
    window.open(targetUrl, '_blank');
  }

  function closeModal() {
    document.getElementById('payModal').classList.add('hidden');
  }

  renderPackages('Free Fire');
</script>
</body>
</html>

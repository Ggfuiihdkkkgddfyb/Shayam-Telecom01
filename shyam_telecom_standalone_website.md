<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Shyam Telecom - Sahnewal Khurd's #1 Mobile & Repair Hub</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @keyframes popupBounce {
      0% { opacity: 0; transform: translate(-50%, -20px) scale(0.85); }
      60% { opacity: 1; transform: translate(-50%, 6px) scale(1.03); }
      100% { opacity: 1; transform: translate(-50%, 0) scale(1); }
    }
    @keyframes modalPop {
      0% { opacity: 0; transform: scale(0.8); }
      70% { opacity: 1; transform: scale(1.04); }
      100% { opacity: 1; transform: scale(1); }
    }
    @keyframes slideInRight {
      0% { transform: translateX(100%); opacity: 0.5; }
      100% { transform: translateX(0); opacity: 1; }
    }
    @keyframes fadeIn {
      0% { opacity: 0; transform: translateY(8px); }
      100% { opacity: 1; transform: translateY(0); }
    }
    .animate-popup-bounce {
      animation: popupBounce 0.4s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
    }
    .animate-modal-pop {
      animation: modalPop 0.35s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
    }
    .animate-slide-right {
      animation: slideInRight 0.3s ease-out forwards;
    }
    .animate-fade-in {
      animation: fadeIn 0.35s ease-out forwards;
    }
    .no-scrollbar::-webkit-scrollbar {
      display: none;
    }
    .no-scrollbar {
      -ms-overflow-style: none;
      scrollbar-width: none;
    }
  </style>
</head>
<body class="bg-slate-50 text-slate-900 min-h-screen flex flex-col font-sans selection:bg-blue-600 selection:text-white">

  <!-- FLOATING ANIMATED TOAST POPUP -->
  <div id="toast-container" class="fixed top-5 left-1/2 z-50 w-[92%] max-w-sm pointer-events-none hidden"></div>

  <!-- ORDER PLACED CELEBRATION POPUP MODAL -->
  <div id="order-success-modal" class="fixed inset-0 z-50 bg-slate-900/70 backdrop-blur-sm hidden items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 text-center space-y-5 shadow-2xl border border-slate-100 animate-modal-pop">
      <div class="w-20 h-20 bg-emerald-100 text-emerald-600 rounded-full mx-auto flex items-center justify-center text-4xl shadow-inner">
        ✅
      </div>
      <div class="space-y-1.5">
        <span class="inline-block bg-emerald-50 text-emerald-700 font-extrabold text-xs px-3 py-1 rounded-full border border-emerald-200 uppercase tracking-wider">
          Order Confirmed
        </span>
        <h3 class="text-2xl font-black text-slate-900">Thank You for Your Order!</h3>
        <p class="text-xs sm:text-sm text-slate-500">
          Your order has been received by <span id="modal-shop-name" class="font-bold text-slate-700">Shyam Telecom</span>.
        </p>
      </div>

      <div class="bg-slate-50 rounded-2xl p-4 border border-slate-200 text-left space-y-2 text-xs sm:text-sm">
        <div class="flex justify-between items-center border-b border-slate-200 pb-2">
          <span class="text-slate-500 font-medium">Order ID:</span>
          <span id="modal-order-id" class="font-black text-blue-600"></span>
        </div>
        <div class="flex justify-between items-center">
          <span class="text-slate-500 font-medium">Customer:</span>
          <span id="modal-customer-name" class="font-bold text-slate-800"></span>
        </div>
        <div class="flex justify-between items-center">
          <span class="text-slate-500 font-medium">Mode:</span>
          <span id="modal-delivery-mode" class="font-bold text-slate-800"></span>
        </div>
        <div class="flex justify-between items-center">
          <span class="text-slate-500 font-medium">Time Slot:</span>
          <span id="modal-time-slot" class="font-bold text-amber-700"></span>
        </div>
        <div class="flex justify-between items-center pt-2 border-t border-slate-200 text-base">
          <span class="font-bold text-slate-900">Total Amount:</span>
          <span id="modal-order-total" class="font-black text-emerald-600"></span>
        </div>
      </div>

      <button
        onclick="closeOrderSuccessModal()"
        class="w-full py-3.5 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-2xl shadow-lg shadow-blue-200 transition-all text-sm uppercase tracking-wider active:scale-95"
      >
        Continue Shopping
      </button>
    </div>
  </div>

  <!-- TOP ANNOUNCEMENT BAR -->
  <div class="bg-slate-900 text-slate-200 text-[11px] sm:text-xs font-semibold py-2 px-4 text-center border-b border-slate-800">
    <div class="max-w-7xl mx-auto flex flex-wrap items-center justify-center sm:justify-between gap-2">
      <span id="text-delivery-info">⚡ Fast 2-Hour Local Delivery & Free Store Pickup</span>
      <span id="text-guarantee" class="hidden md:inline text-amber-400">100% Genuine Products • Best Local Prices • Instant Support</span>
    </div>
  </div>

  <!-- TOP HEADER -->
  <header class="bg-gradient-to-r from-blue-700 via-indigo-700 to-blue-800 text-white shadow-lg sticky top-0 z-40">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 sm:h-20 flex items-center justify-between gap-3">
      <!-- Brand Logo -->
      <div onclick="navigateTo('store')" class="flex items-center gap-3 cursor-pointer group min-w-0">
        <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-2xl bg-white/15 backdrop-blur-md flex items-center justify-center border border-white/30 shadow-inner group-hover:scale-105 transition-transform flex-shrink-0">
          <span class="text-lg sm:text-2xl font-black tracking-tighter">ST</span>
        </div>
        <div class="min-w-0">
          <div class="flex items-center gap-2">
            <h1 id="text-header-title" class="text-lg sm:text-2xl font-black tracking-tight truncate">Shyam Telecom</h1>
            <span id="text-header-badge" class="text-[10px] sm:text-xs font-extrabold uppercase tracking-wider bg-amber-400 text-slate-900 px-2 py-0.5 rounded-full shadow-sm flex-shrink-0">
              Live Store
            </span>
          </div>
          <p id="text-header-tagline" class="text-[11px] sm:text-xs text-blue-200 truncate font-medium">
            Sahnewal Khurd's #1 Mobile & Repair Hub
          </p>
        </div>
      </div>

      <!-- Right Action -->
      <div class="flex items-center gap-2 sm:gap-3 flex-shrink-0">
        <button
          id="header-cart-btn"
          onclick="toggleCartDrawer(true)"
          class="relative flex items-center gap-2 bg-white text-blue-900 hover:bg-blue-50 px-3.5 sm:px-5 py-2 sm:py-2.5 rounded-xl sm:rounded-2xl transition-all duration-200 font-extrabold text-xs sm:text-sm shadow-md active:scale-95"
        >
          <svg class="w-5 h-5 text-blue-700" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" />
          </svg>
          <span>Cart</span>
          <span id="header-cart-count" class="bg-amber-400 text-slate-900 font-black text-xs px-2 py-0.5 rounded-full shadow-sm hidden">0</span>
        </button>

        <button
          id="header-back-btn"
          onclick="navigateTo('store')"
          class="hidden bg-white text-blue-900 hover:bg-blue-50 px-4 py-2 sm:py-2.5 rounded-xl font-bold text-xs sm:text-sm shadow-md transition-all items-center gap-2"
        >
          <span>← Back to Store</span>
        </button>
      </div>
    </div>
  </header>

  <!-- MAIN CONTENT AREA -->
  <main class="flex-1 max-w-7xl w-full mx-auto px-3 sm:px-6 lg:px-8 py-5 sm:py-8">
    
    <!-- ================= CUSTOMER STORE VIEW ================= -->
    <div id="view-store" class="space-y-6 sm:space-y-8 animate-fade-in">
      <!-- Hero Banner -->
      <div class="relative bg-gradient-to-br from-blue-950 via-indigo-900 to-slate-900 text-white rounded-2xl sm:rounded-3xl p-5 sm:p-10 lg:p-12 shadow-xl overflow-hidden border border-blue-800/60">
        <div class="absolute -right-12 -bottom-12 w-64 h-64 bg-blue-500 rounded-full blur-3xl opacity-20 pointer-events-none"></div>
        <div class="absolute right-1/4 -top-12 w-48 h-48 bg-indigo-400 rounded-full blur-3xl opacity-15 pointer-events-none"></div>

        <div class="relative z-10 max-w-2xl space-y-3 sm:space-y-4">
          <span id="text-hero-badge" class="inline-flex items-center gap-1.5 bg-blue-500/25 text-blue-200 px-3 py-1 rounded-full text-[11px] sm:text-xs font-bold uppercase tracking-wider backdrop-blur-md border border-blue-400/30">
            ⭐ Trusted Local Store in Sahnewal Khurd
          </span>
          <h2 id="text-hero-title" class="text-2xl sm:text-4xl lg:text-5xl font-black tracking-tight leading-tight">
            Shyam Telecom
          </h2>
          <p id="text-hero-subtitle" class="text-slate-300 text-sm sm:text-base lg:text-lg font-medium leading-relaxed">
            Your Trusted Destination for Mobile Phones, Genuine Accessories & Instant Repairs.
          </p>
          <div class="flex flex-col sm:flex-row sm:flex-wrap gap-2.5 sm:gap-3 pt-2">
            <div class="flex items-center gap-2 text-xs sm:text-sm font-semibold bg-white/10 px-3.5 py-2 rounded-xl backdrop-blur-sm border border-white/10">
              <span>📍</span>
              <span id="text-hero-address">Main Bazaar, Belga Road, Sahnewal Khurd, Punjab</span>
            </div>
            <div class="flex items-center gap-2 text-xs sm:text-sm font-semibold bg-white/10 px-3.5 py-2 rounded-xl backdrop-blur-sm border border-white/10">
              <span>📞</span>
              <span id="text-hero-phone">+91 98765 43210</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Search & Categories Bar -->
      <div class="flex flex-col md:flex-row gap-3 sm:gap-4 items-stretch md:items-center justify-between">
        <div class="relative w-full md:w-96">
          <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center pointer-events-none text-slate-400">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </span>
          <input
            id="search-input"
            type="text"
            placeholder="Search phones, earbuds, chargers..."
            oninput="handleSearch(this.value)"
            class="w-full pl-10 pr-4 py-3 bg-white border border-slate-200 rounded-2xl shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-600 text-sm font-medium transition-all"
          />
        </div>

        <div id="category-buttons" class="flex items-center gap-2 overflow-x-auto pb-1 md:pb-0 no-scrollbar"></div>
      </div>

      <!-- Product Grid -->
      <div id="products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-6"></div>
    </div>

    <!-- ================= ADMIN PORTAL VIEW ================= -->
    <div id="view-admin" class="space-y-6 sm:space-y-8 animate-fade-in hidden">
      
      <!-- Admin Password Login Box -->
      <div id="admin-login-box" class="max-w-md mx-auto bg-white rounded-3xl border border-slate-200 shadow-xl p-6 sm:p-10 my-8 sm:my-12">
        <div class="text-center space-y-2 mb-6">
          <div class="w-16 h-16 bg-blue-50 text-blue-600 rounded-2xl mx-auto flex items-center justify-center text-3xl shadow-inner border border-blue-100">
            🔐
          </div>
          <h2 class="text-xl sm:text-2xl font-black text-slate-900">Admin Portal Login</h2>
          <p class="text-xs sm:text-sm text-slate-500">
            Enter your secret owner PIN to manage orders, products, and homepage text.
          </p>
        </div>

        <form onsubmit="handleAdminLogin(event)" class="space-y-4">
          <div>
            <label class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-2">
              Secret Owner PIN
            </label>
            <input
              id="admin-pin-input"
              type="password"
              placeholder="Enter PIN..."
              class="w-full px-4 py-3 bg-slate-50 border border-slate-200 rounded-2xl text-center text-lg font-bold tracking-widest focus:outline-none focus:ring-2 focus:ring-blue-600"
            />
            <p id="admin-login-error" class="text-xs text-red-600 font-bold mt-2 text-center hidden">
              Incorrect PIN. Please try again.
            </p>
          </div>

          <button
            type="submit"
            class="w-full py-3.5 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-2xl shadow-lg shadow-blue-200 transition-all text-sm uppercase tracking-wider"
          >
            Unlock Admin Portal
          </button>
        </form>
      </div>

      <!-- Admin Dashboard Content -->
      <div id="admin-dashboard" class="space-y-6 hidden">
        <div class="bg-white rounded-2xl sm:rounded-3xl p-4 sm:p-6 border border-slate-200 shadow-sm flex flex-col lg:flex-row items-stretch lg:items-center justify-between gap-4">
          <div>
            <h2 class="text-xl sm:text-2xl font-black text-slate-900">Owner Management Portal</h2>
            <p class="text-xs sm:text-sm text-slate-500">
              Manage incoming customer orders, products, and edit homepage text.
            </p>
          </div>

          <div class="flex flex-wrap items-center gap-1.5 bg-slate-100 p-1.5 rounded-2xl">
            <button
              id="tab-btn-orders"
              onclick="switchAdminTab('orders')"
              class="flex-1 sm:flex-initial px-3.5 py-2 rounded-xl font-bold text-xs sm:text-sm transition-all bg-white text-blue-600 shadow-sm"
            >
              📦 Orders (<span id="admin-orders-count">0</span>)
            </button>
            <button
              id="tab-btn-products"
              onclick="switchAdminTab('products')"
              class="flex-1 sm:flex-initial px-3.5 py-2 rounded-xl font-bold text-xs sm:text-sm transition-all text-slate-600 hover:text-slate-900"
            >
              📱 Inventory (<span id="admin-products-count">0</span>)
            </button>
            <button
              id="tab-btn-settings"
              onclick="switchAdminTab('settings')"
              class="flex-1 sm:flex-initial px-3.5 py-2 rounded-xl font-bold text-xs sm:text-sm transition-all text-slate-600 hover:text-slate-900"
            >
              ✏️ Edit Homepage Text
            </button>
          </div>
        </div>

        <!-- TAB 1: ORDERS -->
        <div id="admin-tab-orders" class="space-y-4"></div>

        <!-- TAB 2: INVENTORY -->
        <div id="admin-tab-products" class="space-y-6 hidden">
          <div class="bg-white rounded-2xl sm:rounded-3xl border border-slate-200 shadow-sm p-5 sm:p-8 space-y-5">
            <h3 class="text-lg font-black text-slate-900 flex items-center gap-2">
              <span>➕</span> Add New Product to Store
            </h3>

            <form onsubmit="handleAddProduct(event)" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
              <div>
                <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Product Name *</label>
                <input id="new-prod-name" type="text" placeholder="e.g. Vivo V30 Pro" required class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium focus:ring-2 focus:ring-blue-600 focus:outline-none" />
              </div>

              <div>
                <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Selling Price (₹) *</label>
                <input id="new-prod-price" type="number" placeholder="e.g. 39999" required class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium focus:ring-2 focus:ring-blue-600 focus:outline-none" />
              </div>

              <div>
                <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Original MRP (₹)</label>
                <input id="new-prod-mrp" type="number" placeholder="e.g. 44999" class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium focus:ring-2 focus:ring-blue-600 focus:outline-none" />
              </div>

              <div>
                <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Category</label>
                <select id="new-prod-category" class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium focus:ring-2 focus:ring-blue-600 focus:outline-none">
                  <option value="Smartphones">Smartphones</option>
                  <option value="Accessories">Accessories</option>
                  <option value="Audio">Audio</option>
                  <option value="Repair Parts">Repair Parts</option>
                </select>
              </div>

              <div>
                <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Stock Quantity</label>
                <input id="new-prod-stock" type="number" placeholder="e.g. 10" class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium focus:ring-2 focus:ring-blue-600 focus:outline-none" />
              </div>

              <div>
                <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Product Photo (.jpg / .png)</label>
                <input id="new-prod-image" type="file" accept="image/jpeg, image/png, image/webp" onchange="handleNewImageUpload(event)" class="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-medium file:mr-3 file:py-1 file:px-3 file:rounded-lg file:border-0 file:text-xs file:font-bold file:bg-blue-600 file:text-white" />
              </div>

              <div class="sm:col-span-2 lg:col-span-3">
                <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Description</label>
                <textarea id="new-prod-desc" rows="2" placeholder="Key features, RAM/ROM, warranty details..." class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium focus:ring-2 focus:ring-blue-600 focus:outline-none"></textarea>
              </div>

              <div class="sm:col-span-2 lg:col-span-3 flex justify-end">
                <button type="submit" class="w-full sm:w-auto px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-2xl shadow-lg shadow-blue-200 transition-all text-sm uppercase tracking-wider">
                  + Add Product
                </button>
              </div>
            </form>
          </div>

          <div class="bg-white rounded-2xl sm:rounded-3xl border border-slate-200 shadow-sm p-5 sm:p-8 space-y-5">
            <h3 class="text-lg font-black text-slate-900">Current Store Inventory</h3>
            <div id="admin-inventory-list" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
          </div>
        </div>

        <!-- TAB 3: HOMEPAGE TEXT EDITOR -->
        <div id="admin-tab-settings" class="bg-white rounded-2xl sm:rounded-3xl border border-slate-200 shadow-sm p-5 sm:p-8 space-y-6 hidden">
          <div>
            <h3 class="text-lg font-black text-slate-900">Homepage & Top Website Text Editor</h3>
            <p class="text-xs sm:text-sm text-slate-500 mt-1">
              Edit any text shown at the top bar, header, hero banner, contact details, or footer of your website.
            </p>
          </div>

          <form onsubmit="handleSaveSettings(event)" class="space-y-5">
            <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 space-y-4">
              <h4 class="text-xs font-black text-blue-600 uppercase tracking-wider">
                1. Top Announcement Bar & Header Text
              </h4>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Top Left Delivery Announcement</label>
                  <input id="set-delivery-info" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Top Right Guarantee Text</label>
                  <input id="set-guarantee-text" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Website Header Title</label>
                  <input id="set-header-title" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Header Small Badge</label>
                  <input id="set-header-badge" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div class="sm:col-span-2">
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Header Subtitle / Tagline</label>
                  <input id="set-header-tagline" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
              </div>
            </div>

            <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 space-y-4">
              <h4 class="text-xs font-black text-blue-600 uppercase tracking-wider">
                2. Main Homepage Hero Banner Text
              </h4>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Hero Main Heading</label>
                  <input id="set-hero-title" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Hero Top Pill Badge</label>
                  <input id="set-hero-badge" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div class="sm:col-span-2">
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Hero Subtitle Description</label>
                  <textarea id="set-hero-subtitle" rows="2" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium"></textarea>
                </div>
              </div>
            </div>

            <div class="bg-slate-50 p-4 rounded-2xl border border-slate-200 space-y-4">
              <h4 class="text-xs font-black text-blue-600 uppercase tracking-wider">
                3. Store Address, Phone, Footer & Admin PIN
              </h4>
              <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Contact Phone Number</label>
                  <input id="set-phone" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Shop Address</label>
                  <input id="set-address" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Footer Copyright Text</label>
                  <input id="set-footer-text" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
                <div>
                  <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Secret Admin PIN</label>
                  <input id="set-admin-pin" type="text" class="w-full px-3.5 py-2.5 bg-white border border-slate-200 rounded-xl text-sm font-medium" />
                </div>
              </div>
            </div>

            <div class="flex justify-end">
              <button type="submit" class="w-full sm:w-auto px-8 py-3.5 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-2xl shadow-lg shadow-blue-200 transition-all text-sm uppercase tracking-wider">
                Save All Homepage Text
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </main>

  <!-- EDIT PRODUCT MODAL -->
  <div id="edit-product-modal" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm hidden items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-lg w-full p-6 sm:p-8 space-y-5 shadow-2xl animate-modal-pop max-h-[90vh] overflow-y-auto">
      <div class="flex items-center justify-between pb-3 border-b border-slate-100">
        <h3 class="text-xl font-black text-slate-900">Edit Product</h3>
        <button onclick="closeEditProductModal()" class="w-8 h-8 rounded-full bg-slate-100 flex items-center justify-center font-bold text-slate-500 hover:bg-slate-200">
          ✕
        </button>
      </div>

      <form onsubmit="handleSaveEditProduct(event)" class="space-y-4">
        <div>
          <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Product Name</label>
          <input id="edit-prod-name" type="text" required class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium" />
        </div>

        <div class="grid grid-cols-2 gap-4">
          <div>
            <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Selling Price (₹)</label>
            <input id="edit-prod-price" type="number" required class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium" />
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Stock</label>
            <input id="edit-prod-stock" type="number" required class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium" />
          </div>
        </div>

        <div>
          <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Update Photo (.jpg / .png)</label>
          <input type="file" accept="image/jpeg, image/png, image/webp" onchange="handleEditImageUpload(event)" class="w-full px-3 py-2 bg-slate-50 border border-slate-200 rounded-xl text-xs font-medium file:mr-3 file:py-1 file:px-3 file:rounded-lg file:border-0 file:text-xs file:font-bold file:bg-blue-600 file:text-white" />
        </div>

        <div>
          <label class="block text-xs font-bold text-slate-700 uppercase mb-1">Description</label>
          <textarea id="edit-prod-desc" rows="2" class="w-full px-4 py-2.5 bg-slate-50 border border-slate-200 rounded-xl text-sm font-medium"></textarea>
        </div>

        <div class="flex justify-end gap-3 pt-3 border-t border-slate-100">
          <button type="button" onclick="closeEditProductModal()" class="px-5 py-2.5 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold rounded-xl text-sm">
            Cancel
          </button>
          <button type="submit" class="px-6 py-2.5 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-xl text-sm shadow-md">
            Save Changes
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- SHOPPING CART & COMPLETE YOUR ORDER DRAWER -->
  <div id="cart-drawer-backdrop" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm hidden justify-end">
    <div class="bg-white w-full max-w-md h-full shadow-2xl flex flex-col justify-between animate-slide-right">
      <div class="p-5 sm:
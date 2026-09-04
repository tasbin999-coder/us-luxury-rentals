<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO Primary Meta Tags -->
    <title>StaySuite - Luxury Hotels, Vacation Rentals & Oceanfront Villas</title>
    <meta name="title" content="StaySuite - Luxury Hotels, Vacation Rentals & Oceanfront Villas">
    <meta name="description" content="Book top-rated luxury hotels, beachfront villas, and executive penthouses across the US and Canada with instant confirmation, 24/7 Booking.com live support, and major US credit cards.">
    <meta name="keywords" content="luxury vacation rentals, Miami oceanfront villas, NYC penthouses, LA luxury mansions, Booking.com affiliate hotel stays, US credit card booking">
    <meta name="robots" content="index, follow">
    <meta name="language" content="English">

    <!-- Open Graph / Facebook (Social Sharing) -->
    <meta property="og:type" content="website">
    <meta property="og:url" content="https://yourwebsite.com/">
    <meta property="og:title" content="StaySuite - Luxury Hotels & Vacation Rentals">
    <meta property="og:description" content="Book luxury hotels and villas with instant PDF vouchers and Booking.com support.">
    <meta property="og:image" content="https://images.unsplash.com/photo-1566073771259-6a8506099945">

    <!-- Twitter Meta Tags -->
    <meta property="twitter:card" content="summary_large_image">
    <meta property="twitter:url" content="https://yourwebsite.com/">
    <meta property="twitter:title" content="StaySuite - Luxury Hotels & Vacation Rentals">
    <meta property="twitter:description" content="Book luxury hotels and villas with instant PDF vouchers and Booking.com support.">
    <meta property="twitter:image" content="https://images.unsplash.com/photo-1566073771259-6a8506099945">

    <!-- Structured Data (Schema.org for Google Search) -->
    <script type="application/ld+json">
    {
      "@context": "https://schema.org",
      "@type": "Hotel",
      "name": "StaySuite - Luxury Hotels & House Booking",
      "description": "Book luxury hotels, resorts, and vacation rentals with 24/7 Booking.com live support and US payment methods.",
      "url": "https://yourwebsite.com",
      "telephone": "+1-800-555-0199",
      "priceRange": "$$$$",
      "paymentAccepted": "Credit Card, Debit Card, Visa, Mastercard, American Express, Discover, Apple Pay, Google Pay",
      "address": {
        "@type": "PostalAddress",
        "addressLocality": "Miami Beach",
        "addressRegion": "FL",
        "addressCountry": "US"
      },
      "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.9",
        "reviewCount": "184"
      }
    }
    </script>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Leaflet CSS for Map -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <!-- html2pdf.js for PDF Voucher Generation -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap');
        body { font-family: 'Inter', sans-serif; }
        #map { height: 100%; min-height: 400px; border-radius: 1rem; }
        .custom-scrollbar::-webkit-scrollbar { width: 6px; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
    </style>
</head>
<body class="bg-slate-50 text-slate-800">

    <!-- Header Navigation -->
    <header class="bg-blue-950 text-white sticky top-0 z-40 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-amber-500 rounded-xl flex items-center justify-center font-extrabold text-blue-950 text-xl shadow-md">
                    S
                </div>
                <span class="text-2xl font-black tracking-tight">StaySuite</span>
            </div>
            
            <nav class="flex items-center gap-8 font-semibold text-sm">
                <a href="#search" class="hover:text-amber-400 transition-colors">Search Stays</a>
                <a href="#featured" class="hover:text-amber-400 transition-colors">Popular Properties</a>
                <a href="#map-section" class="hover:text-amber-400 transition-colors">Map View</a>
                <a href="#reviews-section" class="hover:text-amber-400 transition-colors">Guest Reviews</a>
                <a href="#support" class="hover:text-amber-400 transition-colors">Booking.com Support</a>
            </nav>
        </div>
    </header>

    <!-- Search Hero Bar -->
    <section id="search" class="bg-blue-950 text-white pb-16 pt-10 px-4">
        <div class="max-w-6xl mx-auto text-center mb-8">
            <!-- Premium Gradient Highlight Headline -->
            <h1 class="text-3xl md:text-5xl font-black mb-3 tracking-tight text-transparent bg-clip-text bg-gradient-to-r from-amber-300 via-amber-400 to-yellow-200 drop-shadow-md">
                Book Exclusive Luxury Homes & Villas
            </h1>
            <p class="text-blue-200 text-base md:text-lg">Guaranteed live rates with major US card support and 24/7 Booking.com care</p>
        </div>

        <div class="max-w-6xl mx-auto bg-white rounded-2xl p-4 sm:p-6 shadow-2xl text-slate-800 grid grid-cols-1 md:grid-cols-4 gap-4 items-end">
            <!-- Custom Search Text Input -->
            <div>
                <label class="block text-xs font-bold uppercase text-slate-500 mb-1.5"><i class="fa-solid fa-location-dot text-amber-500"></i> Search City / Location</label>
                <input type="text" id="destination" placeholder="Enter any city or location..." class="w-full bg-slate-100 border border-slate-300 rounded-xl px-4 py-3 font-semibold text-sm focus:outline-none focus:ring-2 focus:ring-blue-600">
            </div>

            <div>
                <label class="block text-xs font-bold uppercase text-slate-500 mb-1.5"><i class="fa-solid fa-calendar text-amber-500"></i> Check-In & Check-Out</label>
                <div class="flex gap-2">
                    <input type="date" id="checkin" value="2026-09-10" class="w-1/2 bg-slate-100 border border-slate-300 rounded-xl px-2 py-3 text-xs font-semibold focus:outline-none" onchange="calculateTotal()">
                    <input type="date" id="checkout" value="2026-09-12" class="w-1/2 bg-slate-100 border border-slate-300 rounded-xl px-2 py-3 text-xs font-semibold focus:outline-none" onchange="calculateTotal()">
                </div>
            </div>

            <!-- Only Rooms Selection -->
            <div>
                <label class="block text-xs font-bold uppercase text-slate-500 mb-1.5"><i class="fa-solid fa-door-open text-amber-500"></i> Rooms</label>
                <select id="rooms" class="w-full bg-slate-100 border border-slate-300 rounded-xl px-4 py-3 font-semibold text-sm focus:outline-none">
                    <option value="1">1 Room</option>
                    <option value="2">2 Rooms</option>
                    <option value="3">3 Rooms</option>
                    <option value="4">4+ Rooms</option>
                </select>
            </div>

            <button onclick="filterHotels()" class="bg-amber-500 hover:bg-amber-600 text-blue-950 font-black py-3.5 px-6 rounded-xl shadow-lg transition flex items-center justify-center gap-2 text-sm">
                <i class="fa-solid fa-magnifying-glass"></i> Search Availability
            </button>
        </div>
    </section>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 py-12 grid grid-cols-1 lg:grid-cols-12 gap-8">

        <!-- Left Column: Hotel Listings & Interactive Map -->
        <div id="featured" class="lg:col-span-7 space-y-8">
            
            <!-- Map Toggle Header & Filters -->
            <div class="bg-white p-4 rounded-xl border border-slate-200 shadow-sm space-y-3">
                <div class="flex items-center justify-between">
                    <div>
                        <h2 class="text-xl font-extrabold text-slate-900">Available Properties</h2>
                        <p class="text-xs text-slate-500">Compare locations, rates, and amenities on the live map</p>
                    </div>
                    <button onclick="scrollToMap()" class="px-4 py-2 bg-blue-50 text-blue-700 font-bold rounded-lg hover:bg-blue-100 transition text-xs flex items-center gap-2">
                        <i class="fa-solid fa-map-location-dot"></i> View Map
                    </button>
                </div>
                <!-- Filter Pills -->
                <div class="flex flex-wrap gap-2 pt-2 border-t text-xs">
                    <button onclick="filterType('All')" class="px-3 py-1.5 bg-blue-950 text-white font-bold rounded-full">All Stays</button>
                    <button onclick="filterType('Oceanfront Villa')" class="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 font-semibold rounded-full">Oceanfront Villas</button>
                    <button onclick="filterType('Skyline Penthouse')" class="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 font-semibold rounded-full">Penthouses</button>
                    <button onclick="filterType('Luxury Mansion')" class="px-3 py-1.5 bg-slate-100 hover:bg-slate-200 font-semibold rounded-full">Mansions</button>
                </div>
            </div>

            <!-- Hotel List Container -->
            <div id="hotel-list" class="space-y-6">
                <!-- Dynamically Rendered via JS -->
            </div>

            <!-- Guest Reviews Section -->
            <div id="reviews-section" class="bg-white p-6 rounded-2xl border border-slate-200 shadow-sm space-y-4">
                <h3 class="text-lg font-bold flex items-center gap-2">
                    <i class="fa-solid fa-star text-amber-500"></i> Verified Guest Reviews
                </h3>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 text-xs space-y-2">
                        <div class="flex justify-between items-center">
                            <span class="font-bold text-slate-900">Sarah M. (California)</span>
                            <span class="text-amber-500 font-bold"><i class="fa-solid fa-star"></i> 5.0</span>
                        </div>
                        <p class="text-slate-600">"Smooth booking process using my Amex card. Received instant confirmation and voucher!"</p>
                        <span class="text-[10px] text-slate-400">Miami Oceanfront Villa • September 2026</span>
                    </div>
                    <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 text-xs space-y-2">
                        <div class="flex justify-between items-center">
                            <span class="font-bold text-slate-900">David K. (London, UK)</span>
                            <span class="text-amber-500 font-bold"><i class="fa-solid fa-star"></i> 4.9</span>
                        </div>
                        <p class="text-slate-600">"The Booking.com support integration was very helpful. Excellent NYC skyline penthouse view."</p>
                        <span class="text-[10px] text-slate-400">NYC Central Park Penthouse • August 2026</span>
                    </div>
                </div>
            </div>

            <!-- Map View Section -->
            <div id="map-section" class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm">
                <h3 class="text-lg font-bold mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-map-pin text-amber-500"></i> Interactive Property Map
                </h3>
                <div id="map" class="shadow-inner"></div>
            </div>
        </div>

        <!-- Right Column: Booking Details, US Payment Cards & Booking.com Support -->
        <div class="lg:col-span-5 space-y-6">

            <!-- Selected Hotel Booking Card -->
            <div class="bg-white rounded-2xl border border-slate-200 shadow-xl p-6 sticky top-28">
                <div class="flex justify-between items-start mb-4 border-b pb-4">
                    <div>
                        <span id="selected-type" class="text-xs font-bold uppercase tracking-wider text-amber-600 bg-amber-50 px-2.5 py-1 rounded-full">Oceanfront Villa</span>
                        <h3 id="selected-title" class="text-xl font-extrabold text-slate-900 mt-1">Modern Oceanfront Villa in Miami</h3>
                        <p id="selected-location" class="text-xs text-slate-500 mt-1"><i class="fa-solid fa-location-dot text-slate-400"></i> South Beach, Miami, FL</p>
                    </div>
                    <div class="text-right">
                        <span id="selected-price" class="text-2xl font-black text-blue-950">$ 450</span>
                        <span class="text-xs text-slate-400 block">/ night</span>
                    </div>
                </div>

                <!-- Status Badges -->
                <div class="mb-4 flex flex-wrap gap-2 text-[11px]">
                    <span id="stock-badge" class="bg-amber-50 text-amber-800 font-bold px-2.5 py-1 rounded-full flex items-center gap-1 border border-amber-200">
                        <i class="fa-solid fa-box-open"></i> Limited Inventory Available
                    </span>
                    <span class="bg-blue-50 text-blue-700 font-bold px-2.5 py-1 rounded-full flex items-center gap-1 border border-blue-200">
                        <i class="fa-solid fa-shield-halved"></i> Confirmed Booking
                    </span>
                </div>

                <!-- English Professional Notice Alert -->
                <div id="availability-alert" class="hidden mb-4 p-3 bg-amber-50 border border-amber-300 rounded-xl text-xs text-amber-900 space-y-1">
                    <p class="font-bold flex items-center gap-1.5 text-amber-800">
                        <i class="fa-solid fa-circle-exclamation text-amber-600 text-sm"></i> Notice: Selected Option Currently Unavailable
                    </p>
                    <p class="text-[11px] text-amber-800 leading-relaxed">
                        We apologize for the inconvenience. Certain amenities or room types are temporarily out of stock for your selected dates. To maintain our high quality standards, reservations for this configuration are currently paused. Please check alternative dates or contact Booking.com Support.
                    </p>
                </div>

                <!-- Gallery & Room Type Selection -->
                <div class="mb-6 space-y-3">
                    <button onclick="openGalleryModal()" class="w-full py-2 bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold rounded-lg text-xs flex items-center justify-center gap-2 transition">
                        <i class="fa-solid fa-images text-blue-600 text-base"></i> View Photo Gallery & 360° Tour
                    </button>

                    <div>
                        <label class="block text-xs font-bold text-slate-700 mb-1">Select Room / Suite Category:</label>
                        <select id="room-type-select" onchange="calculateTotal()" class="w-full bg-slate-100 border border-slate-300 rounded-lg p-2.5 text-xs font-semibold focus:outline-none">
                            <option value="standard" data-multiplier="1" data-available="true">Standard Deluxe Villa (Available)</option>
                            <option value="executive" data-multiplier="1.3" data-available="true">Ocean View Executive Suite (+30%)</option>
                            <option value="suite" data-multiplier="1.8" data-available="false">Presidential Penthouse (Currently Out of Stock)</option>
                        </select>
                    </div>
                </div>

                <!-- Add-on Services -->
                <div class="mb-6">
                    <h4 class="text-xs font-bold text-slate-900 mb-3 uppercase tracking-wider">Add Extra Services:</h4>
                    <div class="space-y-2">
                        <label class="flex items-center justify-between bg-slate-50 p-3 rounded-xl border border-slate-200 cursor-pointer hover:bg-slate-100">
                            <span class="text-xs font-medium flex items-center gap-2">
                                <input type="checkbox" id="addon-breakfast" class="rounded text-blue-600 focus:ring-blue-500" onchange="calculateTotal()">
                                <i class="fa-solid fa-utensils text-amber-500"></i> Daily Gourmet Breakfast
                            </span>
                            <span class="text-xs font-bold text-slate-700">+ $ 35</span>
                        </label>
                        <label class="flex items-center justify-between bg-slate-50 p-3 rounded-xl border border-slate-200 cursor-pointer hover:bg-slate-100">
                            <span class="text-xs font-medium flex items-center gap-2">
                                <input type="checkbox" id="addon-pickup" class="rounded text-blue-600 focus:ring-blue-500" onchange="calculateTotal()">
                                <i class="fa-solid fa-car text-blue-500"></i> VIP Airport Transfer
                            </span>
                            <span class="text-xs font-bold text-slate-700">+ $ 90</span>
                        </label>
                    </div>
                </div>

                <!-- Dynamic Calculation Summary -->
                <div class="bg-slate-50 p-4 rounded-xl border border-slate-200 space-y-2 text-xs mb-6">
                    <div class="flex justify-between text-slate-600">
                        <span>Stay Duration (<span id="calc-nights">2</span> nights):</span>
                        <span id="calc-base">$ 900</span>
                    </div>
                    <div class="flex justify-between text-slate-600">
                        <span>Extra Add-ons:</span>
                        <span id="calc-addons">$ 0</span>
                    </div>
                    <div class="flex justify-between text-slate-600">
                        <span>Taxes & Service Fees (10%):</span>
                        <span id="calc-vat">$ 90</span>
                    </div>
                    <div class="border-t pt-2 flex justify-between font-extrabold text-slate-900 text-base">
                        <span>Total Estimated Price:</span>
                        <span id="calc-total" class="text-blue-950">$ 990</span>
                    </div>
                </div>

                <!-- US Supported Payment Options -->
                <div class="mb-6">
                    <label class="block text-xs font-bold text-slate-700 mb-2 uppercase">Supported Payment Methods (US & Global):</label>
                    
                    <div class="grid grid-cols-3 gap-2 text-center text-xs mb-3">
                        <label class="border border-slate-300 rounded-lg p-2 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-1">
                            <input type="radio" name="payment" value="Visa / Mastercard" checked class="hidden">
                            <i class="fa-brands fa-cc-visa text-blue-700 text-xl"></i> Visa / Master
                        </label>
                        <label class="border border-slate-300 rounded-lg p-2 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-1">
                            <input type="radio" name="payment" value="American Express" class="hidden">
                            <i class="fa-brands fa-cc-amex text-cyan-600 text-xl"></i> Amex
                        </label>
                        <label class="border border-slate-300 rounded-lg p-2 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-1">
                            <input type="radio" name="payment" value="Discover" class="hidden">
                            <i class="fa-brands fa-cc-discover text-orange-500 text-xl"></i> Discover
                        </label>
                        <label class="border border-slate-300 rounded-lg p-2 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-1">
                            <input type="radio" name="payment" value="Apple Pay" class="hidden">
                            <i class="fa-brands fa-apple text-slate-800 text-xl"></i> Apple Pay
                        </label>
                        <label class="border border-slate-300 rounded-lg p-2 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-1">
                            <input type="radio" name="payment" value="Google Pay" class="hidden">
                            <i class="fa-brands fa-google-pay text-slate-700 text-xl"></i> G Pay
                        </label>
                        <label class="border border-slate-300 rounded-lg p-2 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-1">
                            <input type="radio" name="payment" value="US Bank Cards" class="hidden">
                            <i class="fa-solid fa-credit-card text-emerald-600 text-xl"></i> US Banks
                        </label>
                    </div>

                    <div class="bg-slate-100 p-2.5 rounded-lg text-[11px] text-slate-600 flex items-center justify-between">
                        <span><i class="fa-solid fa-shield-halved text-emerald-600"></i> SSL 256-Bit Encrypted</span>
                        <span>JCB / Diners Accepted</span>
                    </div>
                </div>

                <!-- Booking Action Button -->
                <button id="book-now-btn" onclick="confirmBooking()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-black py-4 rounded-xl shadow-lg transition flex items-center justify-center gap-2 text-sm">
                    <i class="fa-solid fa-circle-check"></i> Confirm Reservation & Get PDF Voucher
                </button>
            </div>

            <!-- Booking.com Support Section -->
            <div id="support" class="bg-gradient-to-r from-blue-900 to-indigo-950 text-white rounded-2xl p-6 shadow-xl border border-blue-800">
                <div class="flex items-center gap-4 mb-4">
                    <div class="w-12 h-12 bg-amber-500 rounded-full flex items-center justify-center font-bold text-blue-950 text-xl shadow">
                        <i class="fa-solid fa-headset"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-base">Booking.com Official Support</h4>
                        <p class="text-xs text-blue-200">24/7 Global Partner Desk</p>
                    </div>
                </div>
                <p class="text-xs text-blue-100 mb-4 leading-relaxed">
                    For inquiries, date modifications, or customer care regarding properties featured on our portal, please chat directly with our official Booking.com partner support desk.
                </p>
                <div class="space-y-2">
                    <button onclick="openChat()" class="w-full bg-amber-500 hover:bg-amber-600 text-blue-950 font-black py-3 rounded-xl text-xs shadow transition flex items-center justify-center gap-2">
                        <i class="fa-solid fa-comments"></i> Start Booking.com Live Chat
                    </button>
                    <a href="https://www.booking.com/help.html" target="_blank" rel="noopener noreferrer" class="w-full bg-white/10 hover:bg-white/20 text-white font-bold py-2.5 rounded-xl text-xs text-center border border-white/20 transition block">
                        <i class="fa-solid fa-arrow-up-right-from-square mr-1"></i> Visit Booking.com Help Center
                    </a>
                </div>
            </div>

        </div>
    </main>

    <!-- Photo Gallery Modal -->
    <div id="gallery-modal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl max-w-3xl w-full p-6 relative">
            <button onclick="closeGalleryModal()" class="absolute top-4 right-4 text-slate-500 hover:text-slate-800 text-xl font-bold">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <h3 id="gallery-title" class="text-lg font-bold mb-4">Property Photo Gallery</h3>
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <img id="g-img-1" alt="Hotel View 1" class="rounded-xl w-full h-48 object-cover">
                <img id="g-img-2" alt="Hotel View 2" class="rounded-xl w-full h-48 object-cover">
            </div>
            <div class="mt-4 p-3 bg-blue-50 text-blue-800 text-xs rounded-xl flex items-center gap-2">
                <i class="fa-solid fa-circle-info"></i> All rooms include high-speed Wi-Fi, air conditioning, and daily housekeeping.
            </div>
        </div>
    </div>

    <!-- Hidden Printable Voucher Template (For html2pdf) -->
    <div class="hidden">
        <div id="pdf-voucher" class="p-8 bg-white text-slate-800 max-w-2xl mx-auto border-2 border-slate-200">
            <div class="flex justify-between items-center border-b pb-4 mb-6">
                <div>
                    <h1 class="text-2xl font-bold text-blue-900">StaySuite Booking Voucher</h1>
                    <p class="text-xs text-slate-500">Official Reservation Confirmation</p>
                </div>
                <div class="text-right">
                    <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">CONFIRMED</span>
                    <p class="text-xs text-slate-400 mt-1">Booking ID: <span id="voucher-id">BK-984210</span></p>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4 mb-6 text-sm">
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Property Name</p>
                    <p id="v-hotel" class="font-bold text-slate-900">Modern Oceanfront Villa in Miami</p>
                    <p id="v-location" class="text-xs text-slate-600">Miami, FL</p>
                </div>
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Stay Dates</p>
                    <p class="font-bold text-slate-900"><span id="v-checkin"></span> to <span id="v-checkout"></span></p>
                </div>
            </div>

            <div class="border-t border-b py-4 mb-6 space-y-2 text-sm">
                <div class="flex justify-between">
                    <span>Stay Configuration:</span>
                    <span id="v-guests" class="font-bold">Reserved Room(s)</span>
                </div>
                <div class="flex justify-between">
                    <span>Total Paid Amount:</span>
                    <span id="v-total" class="font-bold text-blue-900">$ 990</span>
                </div>
                <div class="flex justify-between">
                    <span>Payment Status:</span>
                    <span id="v-payment" class="font-bold text-emerald-600">Paid via US Credit Card</span>
                </div>
            </div>

            <div class="flex justify-between items-center text-xs text-slate-500">
                <p>For assistance, visit Booking.com Help Center.<br>StaySuite - Verified Affiliate Partner Network</p>
                <div class="w-16 h-16 bg-slate-200 flex items-center justify-center font-bold text-slate-400">
                    QR Code
                </div>
            </div>
        </div>
    </div>

    <!-- Booking.com Live Chat Modal -->
    <div id="chat-modal" class="fixed bottom-6 right-6 w-96 bg-white rounded-2xl shadow-2xl border border-slate-200 z-50 hidden">
        <div class="bg-blue-900 text-white p-4 rounded-t-2xl flex justify-between items-center">
            <div class="flex items-center gap-2">
                <div class="w-3 h-3 bg-emerald-400 rounded-full"></div>
                <span class="font-bold text-sm">Booking.com Customer Support</span>
            </div>
            <button onclick="closeChat()" class="text-slate-300 hover:text-white"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div id="chat-messages" class="p-4 h-64 overflow-y-auto space-y-3 custom-scrollbar text-sm">
            <div class="bg-slate-100 p-3 rounded-xl max-w-[85%] text-slate-800">
                Hello! Welcome to the Booking.com Help Desk. How can we assist you with your reservation today?
            </div>
        </div>
        <div class="p-3 border-t flex gap-2">
            <input type="text" id="chat-input" placeholder="Type your message here..." class="w-full bg-slate-100 border border-slate-300 rounded-lg px-3 py-2 text-sm focus:outline-none">
            <button onclick="sendMessage()" class="bg-blue-900 text-white px-4 rounded-lg font-bold"><i class="fa-solid fa-paper-plane"></i></button>
        </div>
    </div>

    <!-- Leaflet JS for Maps -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <script>
        // US Property Data
        const hotels = [
            {
                id: 1,
                name: "Modern Oceanfront Villa in Miami",
                type: "Oceanfront Villa",
                location: "Miami",
                address: "South Beach, Miami, FL, USA",
                priceUSD: 450,
                rating: 4.95,
                reviews: 142,
                images: [
                    "https://images.unsplash.com/photo-1600596542815-ffad4c1539a9?auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=600&q=80"
                ],
                lat: 25.7617,
                lng: -80.1918
            },
            {
                id: 2,
                name: "Luxury Skyline Penthouse in NYC",
                type: "Skyline Penthouse",
                location: "New York",
                address: "Central Park West, Manhattan, NY, USA",
                priceUSD: 650,
                rating: 4.98,
                reviews: 98,
                images: [
                    "https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1542314831-068cd1dbfeeb?auto=format&fit=crop&w=600&q=80"
                ],
                lat: 40.7128,
                lng: -74.0060
            },
            {
                id: 3,
                name: "Beverly Hills Contemporary Estate",
                type: "Luxury Mansion",
                location: "Los Angeles",
                address: "Beverly Hills, Los Angeles, CA, USA",
                priceUSD: 850,
                rating: 4.92,
                reviews: 115,
                images: [
                    "https://images.unsplash.com/photo-1613977257363-707ba9348227?auto=format&fit=crop&w=600&q=80",
                    "https://images.unsplash.com/photo-1566073771259-6a8506099945?auto=format&fit=crop&w=600&q=80"
                ],
                lat: 34.0522,
                lng: -118.2437
            }
        ];

        let selectedHotel = hotels[0];
        let map, markersGroup;

        // Initialize App
        document.addEventListener('DOMContentLoaded', () => {
            renderHotelList(hotels);
            initMap(hotels);
            calculateTotal();
        });

        function formatPrice(amountUSD) {
            return `$ ${amountUSD.toLocaleString()}`;
        }

        // Render Hotel List
        function renderHotelList(data) {
            const container = document.getElementById('hotel-list');
            container.innerHTML = '';

            data.forEach(hotel => {
                const card = document.createElement('div');
                card.className = `bg-white rounded-2xl border ${selectedHotel.id === hotel.id ? 'border-2 border-blue-600 shadow-md' : 'border-slate-200'} p-4 shadow-sm hover:shadow-lg transition flex flex-col md:flex-row gap-4`;
                
                card.innerHTML = `
                    <div class="md:w-5/12 h-48 rounded-xl overflow-hidden relative">
                        <img src="${hotel.images[0]}" alt="${hotel.name}" class="w-full h-full object-cover">
                        <span class="absolute top-2 left-2 bg-blue-900/80 text-white text-xs font-bold px-2.5 py-1 rounded-md backdrop-blur-sm">
                            ${hotel.type}
                        </span>
                    </div>
                    <div class="md:w-7/12 flex flex-col justify-between">
                        <div>
                            <div class="flex justify-between items-start">
                                <h3 class="text-base font-bold text-slate-900">${hotel.name}</h3>
                                <span class="bg-amber-100 text-amber-800 text-xs font-bold px-2 py-1 rounded-md flex items-center gap-1">
                                    <i class="fa-solid fa-star text-amber-500"></i> ${hotel.rating} (${hotel.reviews})
                                </span>
                            </div>
                            <p class="text-xs text-slate-500 mt-1"><i class="fa-solid fa-location-dot"></i> ${hotel.address}</p>
                            
                            <div class="flex flex-wrap gap-2 my-3 text-xs text-slate-600">
                                <span class="bg-slate-100 px-2 py-1 rounded"><i class="fa-solid fa-wifi text-blue-500"></i> Free Wi-Fi</span>
                                <span class="bg-slate-100 px-2 py-1 rounded"><i class="fa-solid fa-water-ladder text-cyan-500"></i> Pool</span>
                                <span class="bg-slate-100 px-2 py-1 rounded"><i class="fa-solid fa-square-parking text-emerald-500"></i> Free Parking</span>
                            </div>
                        </div>

                        <div class="flex items-center justify-between border-t pt-3 mt-2">
                            <div>
                                <span class="text-xl font-black text-blue-950">${formatPrice(hotel.priceUSD)}</span>
                                <span class="text-xs text-slate-400">/ night</span>
                            </div>
                            <button onclick="selectHotel(${hotel.id})" class="px-4 py-2 bg-blue-900 hover:bg-blue-800 text-white font-bold text-xs rounded-lg shadow transition">
                                Select Stay
                            </button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // Initialize Leaflet Map
        function initMap(data) {
            map = L.map('map').setView([25.7617, -80.1918], 4);

            L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                attribution: '© OpenStreetMap contributors'
            }).addTo(map);

            markersGroup = L.layerGroup().addTo(map);
            updateMapMarkers(data);
        }

        // Update Markers on Map
        function updateMapMarkers(data) {
            markersGroup.clearLayers();
            data.forEach(hotel => {
                L.marker([hotel.lat, hotel.lng])
                    .bindPopup(`<b>${hotel.name}</b><br>Rate: ${formatPrice(hotel.priceUSD)} / night`)
                    .addTo(markersGroup);
            });

            if (data.length > 0) {
                map.setView([data[0].lat, data[0].lng], 5);
            }
        }

        // Select Hotel & Update Details
        function selectHotel(id) {
            selectedHotel = hotels.find(h => h.id === id);
            document.getElementById('selected-type').innerText = selectedHotel.type;
            document.getElementById('selected-title').innerText = selectedHotel.name;
            document.getElementById('selected-location').innerHTML = `<i class="fa-solid fa-location-dot text-slate-400"></i> ${selectedHotel.address}`;
            document.getElementById('selected-price').innerText = formatPrice(selectedHotel.priceUSD);
            
            renderHotelList(hotels);
            calculateTotal();
        }

        // Filter Hotels by Custom Input Text
        function filterHotels() {
            const query = document.getElementById('destination').value.toLowerCase().trim();
            const filtered = hotels.filter(h => h.location.toLowerCase().includes(query) || h.address.toLowerCase().includes(query) || h.name.toLowerCase().includes(query));
            
            if (filtered.length > 0) {
                renderHotelList(filtered);
                updateMapMarkers(filtered);
                selectHotel(filtered[0].id);
            } else {
                renderHotelList(hotels);
                updateMapMarkers(hotels);
            }
        }

        // Filter by Category Type
        function filterType(type) {
            if (type === 'All') {
                renderHotelList(hotels);
                updateMapMarkers(hotels);
            } else {
                const filtered = hotels.filter(h => h.type === type);
                renderHotelList(filtered);
                updateMapMarkers(filtered);
            }
        }

        // Calculate Total Price Dynamically & Check Availability State
        function calculateTotal() {
            const checkin = new Date(document.getElementById('checkin').value);
            const checkout = new Date(document.getElementById('checkout').value);
            
            let diffTime = Math.abs(checkout - checkin);
            let nights = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
            if (isNaN(nights) || nights <= 0) nights = 1;

            document.getElementById('calc-nights').innerText = nights;

            // Room type multiplier & Availability check
            const roomSelect = document.getElementById('room-type-select');
            const selectedOption = roomSelect.options[roomSelect.selectedIndex];
            const multiplier = parseFloat(selectedOption.getAttribute('data-multiplier')) || 1;
            const isAvailable = selectedOption.getAttribute('data-available') === 'true';

            const alertBox = document.getElementById('availability-alert');
            const bookBtn = document.getElementById('book-now-btn');
            const stockBadge = document.getElementById('stock-badge');

            // Handle Availability State Changes
            if (!isAvailable) {
                alertBox.classList.remove('hidden');
                stockBadge.className = 'bg-red-50 text-red-700 font-bold px-2.5 py-1 rounded-full flex items-center gap-1 border border-red-200';
                stockBadge.innerHTML = `<i class="fa-solid fa-circle-xmark"></i> Currently Out of Stock`;

                bookBtn.disabled = true;
                bookBtn.className = 'w-full bg-slate-300 text-slate-500 font-bold py-4 rounded-xl shadow cursor-not-allowed flex items-center justify-center gap-2 text-sm';
                bookBtn.innerHTML = `<i class="fa-solid fa-ban"></i> Booking Temporarily Disabled`;
            } else {
                alertBox.classList.add('hidden');
                stockBadge.className = 'bg-amber-50 text-amber-800 font-bold px-2.5 py-1 rounded-full flex items-center gap-1 border border-amber-200';
                stockBadge.innerHTML = `<i class="fa-solid fa-box-open"></i> Limited Inventory Available`;

                bookBtn.disabled = false;
                bookBtn.className = 'w-full bg-emerald-600 hover:bg-emerald-700 text-white font-black py-4 rounded-xl shadow-lg transition flex items-center justify-center gap-2 text-sm';
                bookBtn.innerHTML = `<i class="fa-solid fa-circle-check"></i> Confirm Reservation & Get PDF Voucher`;
            }

            let baseRate = selectedHotel.priceUSD * multiplier;
            let baseCost = baseRate * nights;
            
            let addonBreakfastUSD = 35 * nights;
            let addonPickupUSD = 90;
            let addonsCost = 0;

            if (document.getElementById('addon-breakfast').checked) addonsCost += addonBreakfastUSD;
            if (document.getElementById('addon-pickup').checked) addonsCost += addonPickupUSD;

            let vat = (baseCost + addonsCost) * 0.10;
            let total = baseCost + addonsCost + vat;

            document.getElementById('calc-base').innerText = formatPrice(baseCost);
            document.getElementById('calc-addons').innerText = formatPrice(addonsCost);
            document.getElementById('calc-vat').innerText = formatPrice(vat);
            document.getElementById('calc-total').innerText = formatPrice(total);
        }

        // Confirm Booking & Generate PDF Voucher
        function confirmBooking() {
            const checkinVal = document.getElementById('checkin').value;
            const checkoutVal = document.getElementById('checkout').value;
            const totalVal = document.getElementById('calc-total').innerText;
            const paymentVal = document.querySelector('input[name="payment"]:checked').value;

            document.getElementById('v-hotel').innerText = selectedHotel.name;
            document.getElementById('v-location').innerText = selectedHotel.address;
            document.getElementById('v-checkin').innerText = checkinVal;
            document.getElementById('v-checkout').innerText = checkoutVal;
            document.getElementById('v-total').innerText = totalVal;
            document.getElementById('v-payment').innerText = `Paid via ${paymentVal}`;

            const element = document.getElementById('pdf-voucher');
            
            alert(`Your reservation was successful! (Paid via ${paymentVal})\nGenerating official PDF voucher...`);

            html2pdf().from(element).save(`Booking_Voucher_${selectedHotel.name}.pdf`);
        }

        // Gallery Modal Handlers
        function openGalleryModal() {
            document.getElementById('gallery-title').innerText = `${selectedHotel.name} - Photo Gallery`;
            document.getElementById('g-img-1').src = selectedHotel.images[0];
            document.getElementById('g-img-2').src = selectedHotel.images[1] || selectedHotel.images[0];
            document.getElementById('gallery-modal').classList.remove('hidden');
        }

        function closeGalleryModal() {
            document.getElementById('gallery-modal').classList.add('hidden');
        }

        // Scroll to Map Section
        function scrollToMap() {
            document.getElementById('map-section').scrollIntoView({ behavior: 'smooth' });
        }

        // Booking.com Live Chat Functions
        function openChat() {
            document.getElementById('chat-modal').classList.remove('hidden');
        }

        function closeChat() {
            document.getElementById('chat-modal').classList.add('hidden');
        }

        function sendMessage() {
            const input = document.getElementById('chat-input');
            const message = input.value.trim();
            if (!message) return;

            const chatMessages = document.getElementById('chat-messages');
            
            // User Message
            const userDiv = document.createElement('div');
            userDiv.className = 'bg-blue-900 text-white p-3 rounded-xl max-w-[80%] ml-auto text-sm';
            userDiv.innerText = message;
            chatMessages.appendChild(userDiv);

            input.value = '';
            chatMessages.scrollTop = chatMessages.scrollHeight;

            // Booking.com Bot Auto Reply in English
            setTimeout(() => {
                const botDiv = document.createElement('div');
                botDiv.className = 'bg-slate-100 p-3 rounded-xl max-w-[80%] text-slate-800 text-sm';
                botDiv.innerText = "Thank you for reaching out to the Booking.com Support Desk. A support representative will connect with you shortly.";
                chatMessages.appendChild(botDiv);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }, 1000);
        }
    </script>
</body>
</html>

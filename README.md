<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO Primary Meta Tags -->
    <title>Booking.com - Official Site | Hotels, Flights, Car Rentals & Attractions</title>
    <meta name="title" content="Booking.com - Official Site | Car Rentals & More">
    <meta name="description" content="Book top-rated car rentals worldwide with instant confirmation and 24/7 customer support.">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Leaflet CSS for Map -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <!-- html2pdf.js for PDF Voucher Generation -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');
        body { font-family: 'Inter', sans-serif; background-color: #f5f5f5; }
        .bk-blue { background-color: #003580; }
        .bk-blue-text { color: #003580; }
        .bk-yellow { background-color: #febb02; }
        .bk-yellow-text { color: #febb02; }
        #map { height: 100%; min-height: 350px; border-radius: 0.75rem; }
    </style>
</head>
<body class="text-slate-800">

    <!-- Header Navigation -->
    <header class="bk-blue text-white sticky top-0 z-50 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-6">
                <a href="#" class="text-2xl font-black tracking-tight text-white">Booking.com</a>
            </div>
            
            <div class="flex items-center gap-3">
                <button class="bg-white bk-blue-text px-3 py-1.5 rounded text-xs font-bold hover:bg-slate-100 transition hidden sm:block">List your property</button>
                <button class="bg-white bk-blue-text px-3 py-1.5 rounded text-xs font-bold hover:bg-slate-100 transition">Register</button>
                <button class="bg-white bk-blue-text px-3 py-1.5 rounded text-xs font-bold hover:bg-slate-100 transition">Sign in</button>
                <div class="w-8 h-8 rounded-full bg-blue-800 flex items-center justify-center font-bold text-xs border border-white/30 cursor-pointer">
                    <i class="fa-solid fa-user"></i>
                </div>
            </div>
        </div>

        <!-- Sub Navigation Tabs -->
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex items-center gap-2 overflow-x-auto pb-3 text-sm no-scrollbar">
            <button onclick="switchTab('stays')" id="tab-stays" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-bed"></i> Stays
            </button>
            <button onclick="switchTab('flights')" id="tab-flights" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-plane"></i> Flights
            </button>
            <button onclick="switchTab('cars')" id="tab-cars" class="flex items-center gap-2 px-4 py-2 rounded-full border border-white/40 bg-white/10 font-semibold text-white whitespace-nowrap transition">
                <i class="fa-solid fa-car"></i> Car rentals
            </button>
            <button onclick="switchTab('attractions')" id="tab-attractions" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-ferris-wheel"></i> Attractions
            </button>
            <button onclick="switchTab('taxis')" id="tab-taxis" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-taxi"></i> Airport taxis
            </button>
        </div>
    </header>

    <!-- Search Hero Bar -->
    <section class="bk-blue pb-10 pt-4 px-3 sm:px-6">
        <div class="max-w-6xl mx-auto">
            
            <!-- STAYS FORM -->
            <div id="form-stays" class="bg-[#febb02] p-2 rounded-xl shadow-lg grid grid-cols-1 md:grid-cols-12 gap-2 hidden">
                <div class="md:col-span-4 bg-white rounded-lg p-2.5 flex items-center gap-3">
                    <i class="fa-solid fa-bed text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Where are you going?</label>
                        <input type="text" id="destination" value="El Paso" class="w-full font-semibold text-sm focus:outline-none bg-transparent">
                    </div>
                </div>
                <div class="md:col-span-4 bg-white rounded-lg p-2 flex items-center gap-2">
                    <i class="fa-solid fa-calendar-days text-slate-400 text-lg ml-1"></i>
                    <div class="w-1/2">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-in date</label>
                        <input type="date" id="checkin" value="2026-09-04" class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                    </div>
                    <div class="w-1/2 border-l pl-2">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-out date</label>
                        <input type="date" id="checkout" value="2026-09-05" class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                    </div>
                </div>
                <div class="md:col-span-2 bg-white rounded-lg p-2.5 flex items-center gap-3">
                    <i class="fa-solid fa-person text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Guests & Rooms</label>
                        <select class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                            <option>2 adults · 0 children · 1 room</option>
                        </select>
                    </div>
                </div>
                <div class="md:col-span-2">
                    <button class="w-full h-full bg-[#0071c2] hover:bg-[#00487a] text-white font-bold py-3 px-4 rounded-lg shadow transition text-base flex items-center justify-center gap-2">Search</button>
                </div>
            </div>

            <!-- CAR RENTALS FORM -->
            <div id="form-cars" class="bg-[#febb02] p-3 rounded-xl shadow-lg space-y-2">
                <div class="bg-white rounded-lg p-2.5 flex items-center gap-3">
                    <i class="fa-solid fa-magnifying-glass text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Pick-up location</label>
                        <input type="text" id="car-location" placeholder="Airport, city, or station" value="El Paso Airport (ELP)" class="w-full font-semibold text-sm focus:outline-none bg-transparent">
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-2">
                    <div class="bg-white rounded-lg p-2 flex items-center justify-between border">
                        <div class="flex items-center gap-2 w-7/12">
                            <i class="fa-solid fa-calendar-days text-slate-400 text-base"></i>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase">Pick-up date</label>
                                <input type="date" id="car-pickup-date" value="2026-09-07" onchange="calculateTotal()" class="font-semibold text-xs focus:outline-none bg-transparent">
                            </div>
                        </div>
                        <div class="flex items-center gap-1 w-5/12 border-l pl-2">
                            <i class="fa-regular fa-clock text-slate-400 text-base"></i>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase">Time</label>
                                <input type="time" id="car-pickup-time" value="10:00" class="font-semibold text-xs focus:outline-none bg-transparent">
                            </div>
                        </div>
                    </div>

                    <div class="bg-white rounded-lg p-2 flex items-center justify-between border">
                        <div class="flex items-center gap-2 w-7/12">
                            <i class="fa-solid fa-calendar-days text-slate-400 text-base"></i>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase">Drop-off date</label>
                                <input type="date" id="car-dropoff-date" value="2026-09-10" onchange="calculateTotal()" class="font-semibold text-xs focus:outline-none bg-transparent">
                            </div>
                        </div>
                        <div class="flex items-center gap-1 w-5/12 border-l pl-2">
                            <i class="fa-regular fa-clock text-slate-400 text-base"></i>
                            <div>
                                <label class="block text-[9px] font-bold text-slate-500 uppercase">Time</label>
                                <input type="time" id="car-dropoff-time" value="10:00" class="font-semibold text-xs focus:outline-none bg-transparent">
                            </div>
                        </div>
                    </div>
                </div>

                <button onclick="calculateTotal()" class="w-full bg-[#0071c2] hover:bg-[#00487a] text-white font-bold py-3 rounded-lg shadow transition text-sm">
                    Search & Update Pricing
                </button>

                <div class="space-y-1.5 pt-1 text-xs font-semibold text-slate-900">
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="checkbox" class="w-4 h-4 rounded text-blue-600 focus:ring-0"> Drop car off at different location
                    </label>
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="checkbox" checked class="w-4 h-4 rounded text-blue-600 focus:ring-0"> Driver aged 30 – 65?
                    </label>
                </div>
            </div>

            <!-- FLIGHTS FORM -->
            <div id="form-flights" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 space-y-3">
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-2">
                        <input type="text" placeholder="From where?" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <input type="text" placeholder="To where?" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search flights</button>
                    </div>
                </div>
            </div>

            <!-- ATTRACTIONS FORM -->
            <div id="form-attractions" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-3 gap-2">
                    <input type="text" placeholder="Where are you going?" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search activities</button>
                </div>
            </div>

            <!-- TAXIS FORM -->
            <div id="form-taxis" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-4 gap-2">
                    <input type="text" placeholder="Enter pick-up location" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <input type="text" placeholder="Enter destination" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <input type="date" value="2026-09-12" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search taxi</button>
                </div>
            </div>

        </div>
    </section>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 py-8 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- Left Column: Listings & Map View -->
        <div class="lg:col-span-7 space-y-4">
            <div class="flex justify-between items-center bg-white p-3 rounded-lg border shadow-sm">
                <div>
                    <h2 class="font-bold text-base text-slate-900">Car Rentals: vehicles found</h2>
                    <p class="text-xs text-slate-500">Great cars at great prices from the biggest rental companies</p>
                </div>
                <button onclick="scrollToMap()" class="px-3 py-1.5 bg-blue-50 text-[#0071c2] font-bold rounded text-xs hover:bg-blue-100 transition flex items-center gap-1.5">
                    <i class="fa-solid fa-map-location-dot"></i> Show on map
                </button>
            </div>

            <div id="hotel-list" class="space-y-4"></div>

            <div id="map-section" class="bg-white p-4 rounded-xl border shadow-sm mt-6">
                <h3 class="font-bold text-sm mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-map-pin text-red-500"></i> Interactive Car Rental Map
                </h3>
                <div id="map" class="shadow-inner"></div>
            </div>
        </div>

        <!-- Right Column: Booking Details & Summary -->
        <div class="lg:col-span-5 space-y-4">
            <div class="bg-white rounded-xl border shadow-lg p-5 sticky top-20">
                <div class="border-b pb-3 mb-3">
                    <span id="selected-type" class="text-[10px] font-bold uppercase text-amber-800 bg-amber-100 px-2 py-0.5 rounded">Car Rental</span>
                    <h3 id="selected-title" class="text-lg font-extrabold text-slate-900 mt-1">Economy Compact - Toyota Yaris</h3>
                    <p id="selected-location" class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot text-slate-400"></i> El Paso Airport · Free Shuttle</p>
                </div>

                <div class="flex justify-between items-center mb-4 bg-slate-50 p-3 rounded-lg border">
                    <div>
                        <span class="text-xs text-slate-500 block">Rate per day</span>
                        <span id="selected-price" class="text-xl font-black text-slate-900">$ 45</span>
                    </div>
                    <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-1 rounded">
                        <i class="fa-solid fa-check"></i> Free cancellation
                    </span>
                </div>

                <div class="mb-4 space-y-2">
                    <label class="block text-xs font-bold text-slate-700">Select Car Package:</label>
                    <select id="room-type-select" onchange="calculateTotal()" class="w-full bg-slate-100 border rounded-lg p-2.5 text-xs font-semibold focus:outline-none">
                        <option value="standard" data-multiplier="1">Economy Compact ($45/day)</option>
                        <option value="executive" data-multiplier="1.5">SUV Midsize with GPS ($68/day)</option>
                        <option value="deluxe" data-multiplier="2.1">Full-Size Luxury Sedan ($95/day)</option>
                    </select>
                </div>

                <div class="bg-slate-50 p-3 rounded-lg border space-y-1.5 text-xs mb-4">
                    <div class="flex justify-between text-slate-600">
                        <span>Duration (<span id="calc-nights">3</span> days):</span>
                        <span id="calc-base">$ 135</span>
                    </div>
                    <div class="flex justify-between text-slate-600">
                        <span>Insurance & Taxes (10%):</span>
                        <span id="calc-tax">$ 14</span>
                    </div>
                    <div class="border-t pt-2 flex justify-between font-extrabold text-slate-900 text-sm">
                        <span>Total Price:</span>
                        <span id="calc-total" class="text-[#0071c2]">$ 149</span>
                    </div>
                </div>

                <div class="mb-4">
                    <label class="block text-xs font-bold text-slate-700 mb-1.5 uppercase">Accepted Payment Cards:</label>
                    <div class="grid grid-cols-4 gap-2 text-center text-xs">
                        <label class="border rounded p-1.5 cursor-pointer bg-white font-bold flex flex-col items-center">
                            <input type="radio" name="payment" value="Visa" checked class="hidden">
                            <i class="fa-brands fa-cc-visa text-blue-700 text-lg"></i> Visa
                        </label>
                        <label class="border rounded p-1.5 cursor-pointer bg-white font-bold flex flex-col items-center">
                            <input type="radio" name="payment" value="Mastercard" class="hidden">
                            <i class="fa-brands fa-cc-mastercard text-red-600 text-lg"></i> Master
                        </label>
                        <label class="border rounded p-1.5 cursor-pointer bg-white font-bold flex flex-col items-center">
                            <input type="radio" name="payment" value="Amex" class="hidden">
                            <i class="fa-brands fa-cc-amex text-cyan-600 text-lg"></i> Amex
                        </label>
                        <label class="border rounded p-1.5 cursor-pointer bg-white font-bold flex flex-col items-center">
                            <input type="radio" name="payment" value="PayPal" class="hidden">
                            <i class="fa-brands fa-paypal text-blue-800 text-lg"></i> PayPal
                        </label>
                    </div>
                </div>

                <button onclick="confirmBooking()" class="w-full bg-[#0071c2] hover:bg-[#00487a] text-white font-bold py-3.5 rounded-lg shadow transition flex items-center justify-center gap-2 text-sm">
                    <i class="fa-solid fa-lock"></i> Reserve Car & Get PDF Voucher
                </button>
            </div>
        </div>
    </main>

    <!-- Hidden Printable Voucher Template -->
    <div class="hidden">
        <div id="pdf-voucher" class="p-8 bg-white text-slate-800 max-w-2xl mx-auto border-2 border-slate-200">
            <div class="flex justify-between items-center border-b pb-4 mb-6">
                <div>
                    <h1 class="text-2xl font-bold text-[#003580]">Car Rental Voucher</h1>
                    <p class="text-xs text-slate-500">Official Reservation Confirmation</p>
                </div>
                <div class="text-right">
                    <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">CONFIRMED</span>
                    <p class="text-xs text-slate-400 mt-1">Confirmation No: <span id="voucher-id">CAR-984210</span></p>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4 mb-6 text-sm">
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Vehicle Name</p>
                    <p id="v-hotel" class="font-bold text-slate-900">Toyota Yaris or similar</p>
                    <p id="v-location" class="text-xs text-slate-600">El Paso Airport</p>
                </div>
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Pick-up / Drop-off</p>
                    <p class="font-bold text-slate-900"><span id="v-checkin"></span> to <span id="v-checkout"></span></p>
                </div>
            </div>

            <div class="border-t border-b py-4 mb-6 space-y-2 text-sm">
                <div class="flex justify-between">
                    <span>Selected Package:</span>
                    <span id="v-room" class="font-bold">Economy Compact</span>
                </div>
                <div class="flex justify-between">
                    <span>Total Amount Paid:</span>
                    <span id="v-total" class="font-bold text-[#003580]">$ 149</span>
                </div>
                <div class="flex justify-between">
                    <span>Payment Method:</span>
                    <span id="v-payment" class="font-bold text-emerald-600">Visa Card</span>
                </div>
            </div>

            <div class="flex justify-between items-center text-xs text-slate-500">
                <p>For support or changes, visit Booking.com Help Center.<br>Powered by Official Affiliate Partner Program</p>
                <div class="w-16 h-16 bg-slate-200 flex items-center justify-center font-bold text-slate-400 text-[10px]">QR CODE</div>
            </div>
        </div>
    </div>

    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <script>
        const hotels = [
            {
                id: 1,
                name: "Toyota Yaris or similar (Compact)",
                type: "Car Rental",
                location: "El Paso",
                address: "El Paso Airport · Free Shuttle",
                priceUSD: 45,
                rating: 8.8,
                image: "https://images.unsplash.com/photo-1541899481282-d53bffe3c35d?auto=format&fit=crop&w=600&q=80",
                lat: 31.7619,
                lng: -106.4850
            },
            {
                id: 2,
                name: "Hyundai Tucson or similar (SUV)",
                type: "Car Rental",
                location: "El Paso",
                address: "El Paso Downtown · Meet & Greet",
                priceUSD: 68,
                rating: 8.5,
                image: "https://images.unsplash.com/photo-1533473359331-0135ef1b58bf?auto=format&fit=crop&w=600&q=80",
                lat: 31.7820,
                lng: -106.4250
            },
            {
                id: 3,
                name: "Chevrolet Malibu or similar (Full Size)",
                type: "Car Rental",
                location: "El Paso",
                address: "El Paso Medical Center",
                priceUSD: 55,
                rating: 8.2,
                image: "https://images.unsplash.com/photo-1552519507-da3b142c6e3d?auto=format&fit=crop&w=600&q=80",
                lat: 31.7710,
                lng: -106.4450
            }
        ];

        let selectedHotel = hotels[0];
        let map, markersGroup;

        document.addEventListener('DOMContentLoaded', () => {
            renderHotelList(hotels);
            initMap(hotels);
            calculateTotal();
            switchTab('cars');
        });

        function switchTab(tab) {
            ['stays', 'flights', 'cars', 'attractions', 'taxis'].forEach(t => {
                const tabBtn = document.getElementById(`tab-${t}`);
                const formDiv = document.getElementById(`form-${t}`);
                if(tabBtn) tabBtn.className = "flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition";
                if(formDiv) formDiv.classList.add('hidden');
            });
            const activeTab = document.getElementById(`tab-${tab}`);
            const activeForm = document.getElementById(`form-${tab}`);
            if(activeTab) activeTab.className = "flex items-center gap-2 px-4 py-2 rounded-full border border-white/40 bg-white/10 font-semibold text-white whitespace-nowrap transition";
            if(activeForm) activeForm.classList.remove('hidden');
        }

        function renderHotelList(data) {
            const container = document.getElementById('hotel-list');
            container.innerHTML = '';

            data.forEach(hotel => {
                const card = document.createElement('div');
                card.className = `bg-white rounded-xl border p-3 shadow-sm hover:shadow-md transition flex flex-col sm:flex-row gap-4 cursor-pointer ${selectedHotel.id === hotel.id ? 'border-2 border-[#0071c2]' : 'border-slate-200'}`;
                card.onclick = () => selectHotel(hotel.id);
                
                card.innerHTML = `
                    <div class="sm:w-4/12 h-36 rounded-lg overflow-hidden relative">
                        <img src="${hotel.image}" alt="${hotel.name}" class="w-full h-full object-cover">
                    </div>
                    <div class="sm:w-8/12 flex flex-col justify-between">
                        <div>
                            <div class="flex justify-between items-start">
                                <h3 class="font-bold text-sm text-[#0071c2] hover:underline">${hotel.name}</h3>
                                <div class="bg-[#003580] text-white text-xs font-bold px-1.5 py-0.5 rounded">${hotel.rating}</div>
                            </div>
                            <p class="text-xs text-slate-500 mt-1"><i class="fa-solid fa-location-dot"></i> ${hotel.address}</p>
                            <span class="inline-block mt-1 text-[10px] bg-emerald-50 text-emerald-700 font-bold px-1.5 py-0.5 rounded">Unlimited mileage included</span>
                        </div>
                        <div class="flex items-end justify-between border-t pt-2 mt-2">
                            <div>
                                <span class="text-[10px] text-slate-400 block">Per day rate</span>
                                <span class="text-lg font-black text-slate-900">$ ${hotel.priceUSD} <span class="text-xs font-normal text-slate-500">/ day</span></span>
                            </div>
                            <button class="px-3 py-1.5 bg-[#0071c2] hover:bg-[#00487a] text-white font-bold text-xs rounded transition">
                                View vehicle
                            </button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function initMap(data) {
            map = L.map('map').setView([31.7619, -106.4850], 12);
            L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
                attribution: '© OpenStreetMap contributors'
            }).addTo(map);

            markersGroup = L.layerGroup().addTo(map);
            updateMapMarkers(data);
        }

        function updateMapMarkers(data) {
            markersGroup.clearLayers();
            data.forEach(hotel => {
                L.marker([hotel.lat, hotel.lng])
                    .bindPopup(`<b>${hotel.name}</b><br>Rate: $${hotel.priceUSD} / day`)
                    .addTo(markersGroup);
            });
        }

        function selectHotel(id) {
            selectedHotel = hotels.find(h => h.id === id);
            document.getElementById('selected-type').innerText = selectedHotel.type;
            document.getElementById('selected-title').innerText = selectedHotel.name;
            document.getElementById('selected-location').innerHTML = `<i class="fa-solid fa-location-dot text-slate-400"></i> ${selectedHotel.address}`;
            document.getElementById('selected-price').innerText = `$ ${selectedHotel.priceUSD}`;
            renderHotelList(hotels);
            calculateTotal();
        }

        function calculateTotal() {
            // Calculate days dynamically based on inputs
            const pickupDateVal = document.getElementById('car-pickup-date').value;
            const dropoffDateVal = document.getElementById('car-dropoff-date').value;
            
            let days = 3;
            if (pickupDateVal && dropoffDateVal) {
                const start = new Date(pickupDateVal);
                const end = new Date(dropoffDateVal);
                const diffTime = end - start;
                const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                if (diffDays > 0) days = diffDays;
            }

            document.getElementById('calc-nights').innerText = days;

            const roomSelect = document.getElementById('room-type-select');
            const multiplier = parseFloat(roomSelect.options[roomSelect.selectedIndex].getAttribute('data-multiplier')) || 1;

            let baseCost = selectedHotel.priceUSD * multiplier * days;
            let tax = Math.round(baseCost * 0.10);
            let total = baseCost + tax;

            document.getElementById('calc-base').innerText = `$ ${Math.round(baseCost)}`;
            document.getElementById('calc-tax').innerText = `$ ${tax}`;
            document.getElementById('calc-total').innerText = `$ ${total}`;
        }

        function confirmBooking() {
            const totalVal = document.getElementById('calc-total').innerText;
            const paymentVal = document.querySelector('input[name="payment"]:checked').value;
            const roomSelectElem = document.getElementById('room-type-select');
            const roomText = roomSelectElem.options[roomSelectElem.selectedIndex].text;

            const pickupDate = document.getElementById('car-pickup-date').value;
            const dropoffDate = document.getElementById('car-dropoff-date').value;
            const pickupTime = document.getElementById('car-pickup-time').value;

            document.getElementById('v-hotel').innerText = selectedHotel.name;
            document.getElementById('v-location').innerText = selectedHotel.address;
            document.getElementById('v-checkin').innerText = `${pickupDate} ${pickupTime}`;
            document.getElementById('v-checkout').innerText = `${dropoffDate} ${pickupTime}`;
            document.getElementById('v-room').innerText = roomText;
            document.getElementById('v-total').innerText = totalVal;
            document.getElementById('v-payment').innerText = paymentVal + ' Card';

            const element = document.getElementById('pdf-voucher');
            alert(`Car Rental Confirmed! (Paid via ${paymentVal})\nDownloading your PDF voucher now...`);
            html2pdf().from(element).save(`Car_Rental_Voucher_${selectedHotel.name.replace(/\s+/g, '_')}.pdf`);
        }

        function scrollToMap() {
            document.getElementById('map-section').scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>

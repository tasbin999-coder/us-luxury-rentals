html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <title>US Luxury Rental - Official Site | Hotels & Luxury Stays</title>
    
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
        .bk-blue { background-color: #0b2545; }
        .bk-blue-text { color: #0b2545; }
        .bk-yellow { background-color: #d4af37; }
        #map { height: 100%; min-height: 350px; border-radius: 0.75rem; }
    </style>
</head>
<body class="text-slate-800">

    <!-- Header Navigation -->
    <header class="bk-blue text-white sticky top-0 z-50 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-2">
                <i class="fa-solid fa-hotel text-amber-400 text-2xl"></i>
                <a href="#" class="text-xl sm:text-2xl font-black tracking-tight text-white">US Luxury Rental</a>
            </div>
            
            <div class="flex items-center gap-3">
                <button class="bg-amber-400 text-slate-900 px-3.5 py-1.5 rounded text-xs font-bold hover:bg-amber-500 transition hidden sm:block">List your property</button>
                <div class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center font-bold text-xs border border-white/30 cursor-pointer">
                    <i class="fa-solid fa-user"></i>
                </div>
            </div>
        </div>

        <!-- Sub Navigation Tabs -->
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex items-center gap-2 overflow-x-auto pb-3 text-sm no-scrollbar">
            <button onclick="switchTab('stays')" id="tab-stays" class="flex items-center gap-2 px-4 py-2 rounded-full border border-white/40 bg-white/10 font-semibold text-white whitespace-nowrap transition">
                <i class="fa-solid fa-bed"></i> Stays
            </button>
            <button onclick="switchTab('flights')" id="tab-flights" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-plane"></i> Flights
            </button>
            <button onclick="switchTab('attractions')" id="tab-attractions" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-ferris-wheel"></i> Attractions
            </button>
        </div>
    </header>

    <!-- Search Hero Bar -->
    <section class="bk-blue pb-10 pt-4 px-3 sm:px-6">
        <div class="max-w-6xl mx-auto">
            
            <!-- STAYS FORM -->
            <div id="form-stays" class="bg-[#d4af37] p-2 rounded-xl shadow-lg grid grid-cols-1 md:grid-cols-12 gap-2">
                <div class="md:col-span-4 bg-white rounded-lg p-2.5 flex items-center gap-3">
                    <i class="fa-solid fa-bed text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Where are you going?</label>
                        <input type="text" id="destination" value="El Paso Luxury Suite" class="w-full font-semibold text-sm focus:outline-none bg-transparent">
                    </div>
                </div>
                <div class="md:col-span-4 bg-white rounded-lg p-2 flex items-center gap-2">
                    <i class="fa-solid fa-calendar-days text-slate-400 text-lg ml-1"></i>
                    <div class="w-1/2">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-in date</label>
                        <input type="date" id="checkin" value="2026-09-07" onchange="calculateTotal()" class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                    </div>
                    <div class="w-1/2 border-l pl-2">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-out date</label>
                        <input type="date" id="checkout" value="2026-09-07" onchange="calculateTotal()" class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                    </div>
                </div>
                <div class="md:col-span-2 bg-white rounded-lg p-2.5 flex items-center gap-3 relative cursor-pointer" onclick="toggleGuestModal(event)">
                    <i class="fa-solid fa-person text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Guests & Rooms</label>
                        <span id="guest-summary-text" class="font-semibold text-xs text-slate-800">2 adults · 0 children · 1 room</span>
                    </div>
                </div>
                <div class="md:col-span-2">
                    <button onclick="calculateTotal()" class="w-full h-full bg-[#0b2545] hover:bg-[#13315c] text-white font-bold py-3 px-4 rounded-lg shadow transition text-base flex items-center justify-center gap-2">Search</button>
                </div>
            </div>

            <!-- FLIGHTS FORM -->
            <div id="form-flights" class="bg-[#d4af37] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 space-y-3">
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-2">
                        <input type="text" placeholder="From where?" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <input type="text" placeholder="To where?" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <button class="bg-[#0b2545] text-white font-bold py-2.5 rounded-lg">Search flights</button>
                    </div>
                </div>
            </div>

            <!-- ATTRACTIONS FORM -->
            <div id="form-attractions" class="bg-[#d4af37] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-3 gap-2">
                    <input type="text" placeholder="Where are you going?" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <button class="bg-[#0b2545] text-white font-bold py-2.5 rounded-lg">Search activities</button>
                </div>
            </div>

        </div>
    </section>

    <!-- Guest & Room Selection Modal (Image style) -->
    <div id="guest-modal" class="fixed inset-0 bg-black/50 z-50 flex items-center justify-center hidden">
        <div class="bg-white rounded-2xl p-6 w-80 sm:w-96 shadow-2xl relative space-y-5">
            <button onclick="toggleGuestModal()" class="absolute top-4 right-4 text-slate-400 hover:text-slate-700 text-lg">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <h3 class="font-bold text-base text-slate-900 border-b pb-2">Select Guests & Rooms</h3>
            
            <!-- Adults Counter -->
            <div class="flex justify-between items-center">
                <span class="font-semibold text-sm">Adults</span>
                <div class="flex items-center gap-3 border rounded-lg px-3 py-1">
                    <button onclick="updateCount('adults', -1)" class="text-blue-600 font-bold px-2 py-0.5 hover:bg-slate-100 rounded">-</button>
                    <span id="adult-count" class="font-bold text-sm w-4 text-center">2</span>
                    <button onclick="updateCount('adults', 1)" class="text-blue-600 font-bold px-2 py-0.5 hover:bg-slate-100 rounded">+</button>
                </div>
            </div>

            <!-- Children Counter -->
            <div class="flex justify-between items-center">
                <span class="font-semibold text-sm">Children</span>
                <div class="flex items-center gap-3 border rounded-lg px-3 py-1">
                    <button onclick="updateCount('children', -1)" class="text-blue-600 font-bold px-2 py-0.5 hover:bg-slate-100 rounded">-</button>
                    <span id="child-count" class="font-bold text-sm w-4 text-center">0</span>
                    <button onclick="updateCount('children', 1)" class="text-blue-600 font-bold px-2 py-0.5 hover:bg-slate-100 rounded">+</button>
                </div>
            </div>

            <!-- Rooms Counter -->
            <div class="flex justify-between items-center">
                <span class="font-semibold text-sm">Rooms</span>
                <div class="flex items-center gap-3 border rounded-lg px-3 py-1">
                    <button onclick="updateCount('rooms', -1)" class="text-blue-600 font-bold px-2 py-0.5 hover:bg-slate-100 rounded">-</button>
                    <span id="room-count" class="font-bold text-sm w-4 text-center">1</span>
                    <button onclick="updateCount('rooms', 1)" class="text-blue-600 font-bold px-2 py-0.5 hover:bg-slate-100 rounded">+</button>
                </div>
            </div>

            <button onclick="toggleGuestModal()" class="w-full bg-[#0071c2] text-white font-bold py-2.5 rounded-xl shadow transition text-sm">
                Done
            </button>
        </div>
    </div>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 py-8 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- Left Column: Hotel Room Listings & Map View -->
        <div class="lg:col-span-7 space-y-4">
            <div class="flex justify-between items-center bg-white p-3 rounded-lg border shadow-sm">
                <div>
                    <h2 class="font-bold text-base text-slate-900">Luxury Rooms & Properties Found</h2>
                    <p class="text-xs text-slate-500">Handpicked luxury stays with top-tier comfort</p>
                </div>
                <button onclick="scrollToMap()" class="px-3 py-1.5 bg-blue-50 text-[#0b2545] font-bold rounded text-xs hover:bg-blue-100 transition flex items-center gap-1.5">
                    <i class="fa-solid fa-map-location-dot"></i> Show on map
                </button>
            </div>

            <div id="hotel-list" class="space-y-4"></div>

            <div id="map-section" class="bg-white p-4 rounded-xl border shadow-sm mt-6">
                <h3 class="font-bold text-sm mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-map-pin text-red-500"></i> Interactive Property Location Map
                </h3>
                <div id="map" class="shadow-inner"></div>
            </div>
        </div>

        <!-- Right Column: Booking Details & Summary -->
        <div class="lg:col-span-5 space-y-4">
            <div class="bg-white rounded-xl border shadow-lg p-5 sticky top-20">
                <div class="border-b pb-3 mb-3">
                    <span id="selected-type" class="text-[10px] font-bold uppercase text-amber-800 bg-amber-100 px-2 py-0.5 rounded">Luxury Villa / Suite</span>
                    <h3 id="selected-title" class="text-lg font-extrabold text-slate-900 mt-1">Executive Presidential Suite</h3>
                    <p id="selected-location" class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot text-slate-400"></i> El Paso Downtown · Luxury Stay</p>
                </div>

                <div class="flex justify-between items-center mb-4 bg-slate-50 p-3 rounded-lg border">
                    <div>
                        <span class="text-xs text-slate-500 block">Rate per night</span>
                        <span id="selected-price" class="text-xl font-black text-slate-900">$ 120</span>
                    </div>
                    <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-1 rounded">
                        <i class="fa-solid fa-check"></i> Free cancellation
                    </span>
                </div>

                <div class="mb-4 space-y-2">
                    <label class="block text-xs font-bold text-slate-700">Select Room Type:</label>
                    <select id="room-type-select" onchange="calculateTotal()" class="w-full bg-slate-100 border rounded-lg p-2.5 text-xs font-semibold focus:outline-none">
                        <option value="standard" data-multiplier="1">Executive Presidential Suite ($120/night)</option>
                        <option value="executive" data-multiplier="1.5">Deluxe Ocean-View Penthouse ($180/night)</option>
                        <option value="deluxe" data-multiplier="2">Royal Garden Villa ($240/night)</option>
                    </select>
                </div>

                <div class="bg-slate-50 p-3 rounded-lg border space-y-1.5 text-xs mb-4">
                    <div class="flex justify-between text-slate-600">
                        <span>Duration (<span id="calc-nights">0</span> nights):</span>
                        <span id="calc-base">$ 0</span>
                    </div>
                    <div class="border-t pt-2 flex justify-between font-extrabold text-slate-900 text-sm">
                        <span>Total Price:</span>
                        <span id="calc-total" class="text-[#0b2545]">$ 0</span>
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

                <button onclick="confirmBooking()" class="w-full bg-[#0b2545] hover:bg-[#13315c] text-white font-bold py-3.5 rounded-lg shadow transition flex items-center justify-center gap-2 text-sm">
                    <i class="fa-solid fa-lock"></i> Reserve Room & Get PDF Voucher
                </button>
            </div>
        </div>
    </main>

    <!-- Hidden Printable Voucher Template -->
    <div class="hidden">
        <div id="pdf-voucher" class="p-8 bg-white text-slate-800 max-w-2xl mx-auto border-2 border-slate-200">
            <div class="flex justify-between items-center border-b pb-4 mb-6">
                <div>
                    <h1 class="text-2xl font-bold text-[#0b2545]">US Luxury Rental</h1>
                    <p class="text-xs text-slate-500">Official Reservation Confirmation Voucher</p>
                </div>
                <div class="text-right">
                    <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">CONFIRMED</span>
                    <p class="text-xs text-slate-400 mt-1">Confirmation No: <span id="voucher-id">USL-842910</span></p>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4 mb-6 text-sm">
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Property / Room</p>
                    <p id="v-hotel" class="font-bold text-slate-900">Executive Presidential Suite</p>
                    <p id="v-location" class="text-xs text-slate-600">El Paso Downtown</p>
                </div>
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Check-in / Check-out</p>
                    <p class="font-bold text-slate-900"><span id="v-checkin"></span> to <span id="v-checkout"></span></p>
                </div>
            </div>

            <div class="border-t border-b py-4 mb-6 space-y-2 text-sm">
                <div class="flex justify-between">
                    <span>Selected Room Category:</span>
                    <span id="v-room" class="font-bold">Executive Presidential Suite</span>
                </div>
                <div class="flex justify-between">
                    <span>Total Amount Paid:</span>
                    <span id="v-total" class="font-bold text-[#0b2545]">$ 0</span>
                </div>
                <div class="flex justify-between">
                    <span>Payment Method:</span>
                    <span id="v-payment" class="font-bold text-emerald-600">Visa Card</span>
                </div>
            </div>

            <div class="flex justify-between items-center text-xs text-slate-500">
                <p>For support or inquiries, visit US Luxury Rental Help Center.<br>Official Booking Platform</p>
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
                name: "Executive Presidential Suite",
                type: "Luxury Suite",
                location: "El Paso",
                address: "El Paso Downtown · Premium View",
                priceUSD: 120,
                rating: 9.2,
                image: "https://images.unsplash.com/photo-1582719478250-c89cae4dc85b?auto=format&fit=crop&w=600&q=80",
                lat: 31.7619,
                lng: -106.4850
            },
            {
                id: 2,
                name: "Deluxe Ocean-View Penthouse",
                type: "Penthouse",
                location: "El Paso",
                address: "El Paso Hilltop · Private Balcony",
                priceUSD: 180,
                rating: 9.5,
                image: "https://images.unsplash.com/photo-1590490360182-c33d57733427?auto=format&fit=crop&w=600&q=80",
                lat: 31.7820,
                lng: -106.4250
            },
            {
                id: 3,
                name: "Royal Garden Villa",
                type: "Private Villa",
                location: "El Paso",
                address: "El Paso Suburbs · Swimming Pool",
                priceUSD: 240,
                rating: 9.8,
                image: "https://images.unsplash.com/photo-1566073771259-6a8506099945?auto=format&fit=crop&w=600&q=80",
                lat: 31.7710,
                lng: -106.4450
            }
        ];

        let selectedHotel = hotels[0];
        let map, markersGroup;

        // Guest count states
        let counts = { adults: 2, children: 0, rooms: 1 };

        document.addEventListener('DOMContentLoaded', () => {
            renderHotelList(hotels);
            initMap(hotels);
            calculateTotal();
            switchTab('stays');
        });

        function switchTab(tab) {
            ['stays', 'flights', 'attractions'].forEach(t => {
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

        function toggleGuestModal(e) {
            if(e) e.stopPropagation();
            const modal = document.getElementById('guest-modal');
            modal.classList.toggle('hidden');
        }

        function updateCount(type, val) {
            counts[type] += val;
            if (type === 'adults' && counts[type] < 1) counts[type] = 1;
            if (type === 'children' && counts[type] < 0) counts[type] = 0;
            if (type === 'rooms' && counts[type] < 1) counts[type] = 1;

            document.getElementById('adult-count').innerText = counts.adults;
            document.getElementById('child-count').innerText = counts.children;
            document.getElementById('room-count').innerText = counts.rooms;

            document.getElementById('guest-summary-text').innerText = `${counts.adults} adults · ${counts.children} children · ${counts.rooms} room`;
        }

        function renderHotelList(data) {
            const container = document.getElementById('hotel-list');
            container.innerHTML = '';

            data.forEach(hotel => {
                const card = document.createElement('div');
                card.className = `bg-white rounded-xl border p-3 shadow-sm hover:shadow-md transition flex flex-col sm:flex-row gap-4 cursor-pointer ${selectedHotel.id === hotel.id ? 'border-2 border-[#0b2545]' : 'border-slate-200'}`;
                card.onclick = () => selectHotel(hotel.id);
                
                card.innerHTML = `
                    <div class="sm:w-4/12 h-36 rounded-lg overflow-hidden relative">
                        <img src="${hotel.image}" alt="${hotel.name}" class="w-full h-full object-cover">
                    </div>
                    <div class="sm:w-8/12 flex flex-col justify-between">
                        <div>
                            <div class="flex justify-between items-start">
                                <h3 class="font-bold text-sm text-[#0b2545] hover:underline">${hotel.name}</h3>
                                <div class="bg-[#0b2545] text-white text-xs font-bold px-1.5 py-0.5 rounded">${hotel.rating}</div>
                            </div>
                            <p class="text-xs text-slate-500 mt-1"><i class="fa-solid fa-location-dot"></i> ${hotel.address}</p>
                            <span class="inline-block mt-1 text-[10px] bg-emerald-50 text-emerald-700 font-bold px-1.5 py-0.5 rounded">Free WiFi & Breakfast</span>
                        </div>
                        <div class="flex items-end justify-between border-t pt-2 mt-2">
                            <div>
                                <span class="text-[10px] text-slate-400 block">Per night rate</span>
                                <span class="text-lg font-black text-slate-900">$ ${hotel.priceUSD} <span class="text-xs font-normal text-slate-500">/ night</span></span>
                            </div>
                            <button class="px-3 py-1.5 bg-[#0b2545] hover:bg-[#13315c] text-white font-bold text-xs rounded transition">
                                View room
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
                    .bindPopup(`<b>${hotel.name}</b><br>Rate: $${hotel.priceUSD} / night`)
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
            const checkinVal = document.getElementById('checkin').value;
            const checkoutVal = document.getElementById('checkout').value;
            
            let nights = 0;
            if (checkinVal && checkoutVal) {
                const start = new Date(checkinVal);
                const end = new Date(checkoutVal);
                const diffTime = end - start;
                const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                if (diffDays > 0) nights = diffDays;
            }

            document.getElementById('calc-nights').innerText = nights;

            const roomSelect = document.getElementById('room-type-select');
            const multiplier = parseFloat(roomSelect.options[roomSelect.selectedIndex].getAttribute('data-multiplier')) || 1;

            let baseCost = selectedHotel.priceUSD * multiplier * nights;

            document.getElementById('calc-base').innerText = `$ ${Math.round(baseCost)}`;
            document.getElementById('calc-total').innerText = `$ ${Math.round(baseCost)}`;
        }

        function confirmBooking() {
            const totalVal = document.getElementById('calc-total').innerText;
            const paymentVal = document.querySelector('input[name="payment"]:checked').value;
            const roomSelectElem = document.getElementById('room-type-select');
            const roomText = roomSelectElem.options[roomSelectElem.selectedIndex].text;

            const checkinDate = document.getElementById('checkin').value;
            const checkoutDate = document.getElementById('checkout').value;

            document.getElementById('v-hotel').innerText = selectedHotel.name;
            document.getElementById('v-location').innerText = selectedHotel.address;
            document.getElementById('v-checkin').innerText = checkinDate;
            document.getElementById('v-checkout').innerText = checkoutDate;
            document.getElementById('v-room').innerText = roomText;
            document.getElementById('v-total').innerText = totalVal;
            document.getElementById('v-payment').innerText = paymentVal + ' Card';

            const element = document.getElementById('pdf-voucher');
            alert(`Stay Confirmed! (Paid via ${paymentVal})\nDownloading your PDF voucher now...`);
            html2pdf().from(element).save(`US_Luxury_Rental_Voucher_${selectedHotel.name.replace(/\s+/g, '_')}.pdf`);
        }

        function scrollToMap() {
            document.getElementById('map-section').scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>US Luxury Rental - Official Site | Hotels, Flights, Car Rentals & Attractions</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Leaflet CSS for Map -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');
        body { font-family: 'Inter', sans-serif; background-color: #f5f5f5; }
        .bk-blue { background-color: #003580; }
        .bk-blue-text { color: #003580; }
        .bk-yellow { background-color: #febb02; }
        #map { height: 100%; min-height: 350px; border-radius: 0.75rem; }
    </style>
</head>
<body class="text-slate-800">

    <!-- Header Navigation -->
    <header class="bk-blue text-white sticky top-0 z-50 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <!-- Brand Name: US Luxury Rental (Royal Style Font & Color) -->
            <div class="flex items-center gap-2">
                <a href="#" class="text-xl sm:text-2xl font-black tracking-wider text-transparent bg-clip-text bg-gradient-to-r from-amber-200 via-yellow-400 to-amber-100 uppercase drop-shadow">
                    US Luxury Rental
                </a>
            </div>
            
            <!-- Right Actions (Register & Sign in removed, Added 3-Dot Menu matching user screenshot) -->
            <div class="flex items-center gap-3">
                <button class="bg-white/10 hover:bg-white/20 text-white px-3 py-1.5 rounded text-xs font-bold transition hidden sm:block">List your property</button>
                
                <!-- 3-Dot Menu Button -->
                <div class="relative">
                    <button onclick="toggleMoreMenu()" class="w-9 h-9 rounded-full bg-blue-900 border border-white/30 flex items-center justify-center font-bold text-sm hover:bg-blue-800 transition">
                        <i class="fa-solid fa-ellipsis-vertical"></i>
                    </button>

                    <!-- Dropdown matching screenshot menu (Help, About, Currency, etc.) -->
                    <div id="more-menu" class="absolute right-0 mt-2 w-72 bg-white text-slate-800 rounded-xl shadow-2xl border py-2 hidden z-50 text-xs">
                        <div class="px-4 py-2 border-b font-bold text-slate-500 uppercase text-[10px]">Preferences</div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer flex items-center justify-between">
                            <span>BDT Bangladeshi Taka</span> <i class="fa-solid fa-chevron-right text-[10px]"></i>
                        </div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer flex items-center justify-between">
                            <span>English (US)</span> <i class="fa-solid fa-chevron-right text-[10px]"></i>
                        </div>
                        
                        <div class="px-4 py-2 border-t border-b font-bold text-slate-500 uppercase text-[10px] mt-1">Help and support</div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer flex items-center gap-2">
                            <i class="fa-regular fa-circle-question text-base text-blue-900"></i> Customer Service help
                        </div>

                        <div class="px-4 py-2 border-t border-b font-bold text-slate-500 uppercase text-[10px] mt-1">Settings and legal</div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer">About us</div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer">Careers</div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer">Press center</div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer">Privacy Notice</div>
                        <div class="px-4 py-2 hover:bg-slate-100 cursor-pointer">Terms of Service</div>
                    </div>
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
            <button onclick="switchTab('cars')" id="tab-cars" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-car"></i> Car rentals
            </button>
            <button onclick="switchTab('attractions')" id="tab-attractions" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-ferris-wheel"></i> Attractions
            </button>
        </div>
    </header>

    <!-- Search Hero Bar -->
    <section class="bk-blue pb-10 pt-4 px-3 sm:px-6">
        <div class="max-w-6xl mx-auto">
            <div id="form-stays" class="bg-[#febb02] p-2 rounded-xl shadow-lg grid grid-cols-1 md:grid-cols-12 gap-2">
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
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-in / Nights</label>
                        <input type="date" id="checkin" value="2026-09-04" class="w-full font-semibold text-xs focus:outline-none bg-transparent" onchange="calculateTotal()">
                    </div>
                    <div class="w-1/2 border-l pl-2">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-out</label>
                        <input type="date" id="checkout" value="2026-09-05" class="w-full font-semibold text-xs focus:outline-none bg-transparent" onchange="calculateTotal()">
                    </div>
                </div>

                <div class="md:col-span-2 bg-white rounded-lg p-2.5 flex items-center gap-3">
                    <i class="fa-solid fa-person text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Guests & Rooms</label>
                        <select id="rooms" onchange="calculateTotal()" class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                            <option value="1">2 adults · 0 children · 1 room</option>
                            <option value="2">4 adults · 0 children · 2 rooms</option>
                        </select>
                    </div>
                </div>

                <div class="md:col-span-2">
                    <button onclick="filterHotels()" class="w-full h-full bg-[#0071c2] hover:bg-[#00487a] text-white font-bold py-3 px-4 rounded-lg shadow transition text-base flex items-center justify-center gap-2">
                        Search
                    </button>
                </div>
            </div>

            <!-- Other tabs form placeholders -->
            <div id="form-flights" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-4 gap-2">
                    <input type="text" placeholder="From where?" class="border p-2.5 rounded-lg text-sm">
                    <input type="text" placeholder="To where?" class="border p-2.5 rounded-lg text-sm">
                    <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm">
                    <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search flights</button>
                </div>
            </div>
            <div id="form-cars" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-4 gap-2">
                    <input type="text" placeholder="Pick-up location" class="border p-2.5 rounded-lg text-sm">
                    <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm">
                    <input type="date" value="2026-09-10" class="border p-2.5 rounded-lg text-sm">
                    <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search cars</button>
                </div>
            </div>
            <div id="form-attractions" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-3 gap-2">
                    <input type="text" placeholder="Where are you going?" class="border p-2.5 rounded-lg text-sm">
                    <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm">
                    <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search activities</button>
                </div>
            </div>
        </div>
    </section>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 py-8 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <div class="lg:col-span-7 space-y-4">
            <div class="flex justify-between items-center bg-white p-3 rounded-lg border shadow-sm">
                <div>
                    <h2 class="font-bold text-base text-slate-900">El Paso: properties found</h2>
                    <p class="text-xs text-slate-500">Lock in a great price for your upcoming stay!</p>
                </div>
                <button onclick="scrollToMap()" class="px-3 py-1.5 bg-blue-50 text-[#0071c2] font-bold rounded text-xs hover:bg-blue-100 transition flex items-center gap-1.5">
                    <i class="fa-solid fa-map-location-dot"></i> Show on map
                </button>
            </div>

            <div id="hotel-list" class="space-y-4"></div>

            <div id="map-section" class="bg-white p-4 rounded-xl border shadow-sm mt-6">
                <h3 class="font-bold text-sm mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-map-pin text-red-500"></i> Interactive Property Map
                </h3>
                <div id="map" class="shadow-inner"></div>
            </div>
        </div>

        <!-- Right Summary & Affiliate Payment Gateway -->
        <div class="lg:col-span-5 space-y-4">
            <div class="bg-white rounded-xl border shadow-lg p-5 sticky top-20">
                <div class="border-b pb-3 mb-3">
                    <span id="selected-type" class="text-[10px] font-bold uppercase text-amber-800 bg-amber-100 px-2 py-0.5 rounded">Luxury Stay</span>
                    <h3 id="selected-title" class="text-lg font-extrabold text-slate-900 mt-1">Americas Hotel - El Paso Airport</h3>
                    <p id="selected-location" class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot text-slate-400"></i> El Paso · 5.4 km from centre</p>
                </div>

                <div class="flex justify-between items-center mb-4 bg-slate-50 p-3 rounded-lg border">
                    <div>
                        <span class="text-xs text-slate-500 block">Rate per night</span>
                        <span id="selected-price" class="text-xl font-black text-slate-900">$ 75</span>
                    </div>
                    <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-1 rounded">
                        <i class="fa-solid fa-check"></i> Free cancellation via Booking.com
                    </span>
                </div>

                <!-- Room Duration / Selection -->
                <div class="mb-4 space-y-2">
                    <label class="block text-xs font-bold text-slate-700">Select Duration & Room Type:</label>
                    <select id="room-type-select" onchange="calculateTotal()" class="w-full bg-slate-100 border rounded-lg p-2.5 text-xs font-semibold focus:outline-none">
                        <option value="standard" data-multiplier="1">Standard Double Room ($75/night)</option>
                        <option value="executive" data-multiplier="1.4">Executive Suite ($105/night)</option>
                        <option value="deluxe" data-multiplier="1.9">Deluxe King Room ($145/night)</option>
                    </select>
                </div>

                <!-- Price calculation WITHOUT Taxes & Fees -->
                <div class="bg-slate-50 p-3 rounded-lg border space-y-1.5 text-xs mb-4">
                    <div class="flex justify-between text-slate-600">
                        <span>Duration Selected (<span id="calc-nights">1</span> Night / Days):</span>
                        <span id="calc-base">$ 75</span>
                    </div>
                    <div class="border-t pt-2 flex justify-between font-extrabold text-slate-900 text-sm">
                        <span>Total Affiliate Booking Price:</span>
                        <span id="calc-total" class="text-[#0071c2]">$ 75</span>
                    </div>
                </div>

                <!-- Payment Methods (Global Credit Cards & Local options if applicable) -->
                <div class="mb-4">
                    <label class="block text-xs font-bold text-slate-700 mb-1.5 uppercase">Booking.com Secure Payment Gateway:</label>
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

                <!-- Affiliate Redirect Action (Directly links to Booking.com Affiliate System) -->
                <button onclick="redirectToBookingAffiliate()" class="w-full bg-[#0071c2] hover:bg-[#00487a] text-white font-bold py-3.5 rounded-lg shadow transition flex items-center justify-center gap-2 text-sm">
                    <i class="fa-solid fa-lock"></i> Proceed to Secure Booking.com Checkout
                </button>
                <p class="text-[10px] text-slate-400 text-center mt-2">You will be securely connected to Booking.com official processing system. Commission tracked via US Luxury Rental affiliate ID.</p>
            </div>
        </div>
    </main>

    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <script>
        const hotels = [
            {
                id: 1,
                name: "Americas Hotel - El Paso Airport",
                type: "Luxury Stay",
                location: "El Paso",
                address: "El Paso · 5.4 km from centre",
                priceUSD: 75,
                rating: 8.6,
                image: "https://images.unsplash.com/photo-1566073771259-6a8506099945?auto=format&fit=crop&w=600&q=80",
                lat: 31.7619,
                lng: -106.4850
            },
            {
                id: 2,
                name: "Comfort Suites El Paso Airport",
                type: "Suites",
                location: "El Paso",
                address: "El Paso · 8.9 km from centre",
                priceUSD: 98,
                rating: 8.2,
                image: "https://images.unsplash.com/photo-1582719508461-905c673771fd?auto=format&fit=crop&w=600&q=80",
                lat: 31.7820,
                lng: -106.4250
            }
        ];

        let selectedHotel = hotels[0];
        let map, markersGroup;

        document.addEventListener('DOMContentLoaded', () => {
            renderHotelList(hotels);
            initMap(hotels);
            calculateTotal();
        });

        function toggleMoreMenu() {
            const menu = document.getElementById('more-menu');
            menu.classList.toggle('hidden');
        }

        // Close dropdown when clicking outside
        window.onclick = function(event) {
            if (!event.target.closest('button')) {
                document.getElementById('more-menu').classList.add('hidden');
            }
        }

        function switchTab(tab) {
            ['stays', 'flights', 'cars', 'attractions'].forEach(t => {
                document.getElementById(`tab-${t}`).className = "flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition";
                document.getElementById(`form-${t}`).classList.add('hidden');
            });
            document.getElementById(`tab-${tab}`).className = "flex items-center gap-2 px-4 py-2 rounded-full border border-white/40 bg-white/10 font-semibold text-white whitespace-nowrap transition";
            document.getElementById(`form-${tab}`).classList.remove('hidden');
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
                        </div>
                        <div class="flex items-end justify-between border-t pt-2 mt-2">
                            <div>
                                <span class="text-[10px] text-slate-400 block">Duration / Night Rate</span>
                                <span class="text-lg font-black text-slate-900">$ ${hotel.priceUSD}</span>
                            </div>
                            <button class="px-3 py-1.5 bg-[#0071c2] hover:bg-[#00487a] text-white font-bold text-xs rounded transition">
                                Select Room
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

        function filterHotels() {
            const query = document.getElementById('destination').value.toLowerCase().trim();
            const filtered = hotels.filter(h => h.location.toLowerCase().includes(query) || h.name.toLowerCase().includes(query));
            if (filtered.length > 0) {
                renderHotelList(filtered);
                updateMapMarkers(filtered);
                selectHotel(filtered[0].id);
            }
        }

        function calculateTotal() {
            const checkin = new Date(document.getElementById('checkin').value);
            const checkout = new Date(document.getElementById('checkout').value);
            let nights = Math.ceil(Math.abs(checkout - checkin) / (1000 * 60 * 60 * 24));
            if (isNaN(nights) || nights <= 0) nights = 1;

            document.getElementById('calc-nights').innerText = nights;

            const roomSelect = document.getElementById('room-type-select');
            const multiplier = parseFloat(roomSelect.options[roomSelect.selectedIndex].getAttribute('data-multiplier')) || 1;

            let totalCost = Math.round(selectedHotel.priceUSD * multiplier * nights);

            document.getElementById('calc-base').innerText = `$ ${totalCost}`;
            document.getElementById('calc-total').innerText = `$ ${totalCost}`;
        }

        function redirectToBookingAffiliate() {
            const paymentMethod = document.querySelector('input[name="payment"]:checked').value;
            // Affiliate redirection setup: Booking.com handles everything directly via your affiliate tracking link
            const affiliateUrl = `https://www.booking.com/searchresults.html?ss=${encodeURIComponent(selectedHotel.name)}&aid=YOUR_AFFILIATE_ID`;
            
            alert(`Redirecting via US Luxury Rental Affiliate Link to Booking.com Secure Checkout.\nPayment Method Selected: ${paymentMethod}\nBooking.com will process your payment and assign your commission automatically!`);
            window.open(affiliateUrl, '_blank');
        }

        function scrollToMap() {
            document.getElementById('map-section').scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>

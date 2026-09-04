<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO Primary Meta Tags -->
    <title>Booking.com - Official Site | Hotels, Flights, Car Rentals & Attractions</title>
    <meta name="title" content="Booking.com - Official Site | Hotels, Flights & More">
    <meta name="description" content="Book top-rated hotels, vacation rentals, flights, and car rentals worldwide with instant confirmation and 24/7 customer support.">
    
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

    <!-- Header Navigation (Booking.com Style) -->
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

        <!-- Sub Navigation Tabs (Stays, Flights, Car rentals, Attractions, Taxis) -->
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
            <button onclick="switchTab('taxis')" id="tab-taxis" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-taxi"></i> Airport taxis
            </button>
        </div>
    </header>

    <!-- Search Hero Bar (Exact Booking.com Yellow Container Style) -->
    <section class="bk-blue pb-10 pt-4 px-3 sm:px-6">
        <div class="max-w-6xl mx-auto">
            <!-- Dynamic Tab Forms -->
            
            <!-- STAYS FORM -->
            <div id="form-stays" class="bg-[#febb02] p-2 rounded-xl shadow-lg grid grid-cols-1 md:grid-cols-12 gap-2">
                <!-- Location Input -->
                <div class="md:col-span-4 bg-white rounded-lg p-2.5 flex items-center gap-3 border-2 border-transparent focus-within:border-blue-600">
                    <i class="fa-solid fa-bed text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Where are you going?</label>
                        <input type="text" id="destination" value="El Paso" class="w-full font-semibold text-sm focus:outline-none bg-transparent">
                    </div>
                </div>

                <!-- Dates Input -->
                <div class="md:col-span-4 bg-white rounded-lg p-2 flex items-center gap-2 border-2 border-transparent">
                    <i class="fa-solid fa-calendar-days text-slate-400 text-lg ml-1"></i>
                    <div class="w-1/2">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-in date</label>
                        <input type="date" id="checkin" value="2026-09-04" class="w-full font-semibold text-xs focus:outline-none bg-transparent" onchange="calculateTotal()">
                    </div>
                    <div class="w-1/2 border-l pl-2">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Check-out date</label>
                        <input type="date" id="checkout" value="2026-09-05" class="w-full font-semibold text-xs focus:outline-none bg-transparent" onchange="calculateTotal()">
                    </div>
                </div>

                <!-- Guests / Rooms Input -->
                <div class="md:col-span-2 bg-white rounded-lg p-2.5 flex items-center gap-3">
                    <i class="fa-solid fa-person text-slate-400 text-lg"></i>
                    <div class="w-full">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Guests & Rooms</label>
                        <select id="rooms" onchange="calculateTotal()" class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                            <option value="1">2 adults · 0 children · 1 room</option>
                            <option value="2">4 adults · 0 children · 2 rooms</option>
                            <option value="3">6 adults · 0 children · 3 rooms</option>
                        </select>
                    </div>
                </div>

                <!-- Search Button -->
                <div class="md:col-span-2">
                    <button onclick="filterHotels()" class="w-full h-full bg-[#0071c2] hover:bg-[#00487a] text-white font-bold py-3 px-4 rounded-lg shadow transition text-base flex items-center justify-center gap-2">
                        Search
                    </button>
                </div>
            </div>

            <!-- FLIGHTS FORM (Hidden by default) -->
            <div id="form-flights" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 space-y-3">
                    <div class="flex gap-4 text-xs font-bold text-slate-700">
                        <label class="flex items-center gap-1"><input type="radio" name="flight-type" checked> Round-trip</label>
                        <label class="flex items-center gap-1"><input type="radio" name="flight-type"> One-way</label>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-4 gap-2">
                        <input type="text" placeholder="From where?" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <input type="text" placeholder="To where?" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm font-semibold">
                        <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search flights</button>
                    </div>
                </div>
            </div>

            <!-- CAR RENTALS FORM (Hidden by default) -->
            <div id="form-cars" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-4 gap-2">
                    <input type="text" placeholder="Pick-up location" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <input type="date" value="2026-09-10" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search cars</button>
                </div>
            </div>

            <!-- ATTRACTIONS FORM (Hidden by default) -->
            <div id="form-attractions" class="bg-[#febb02] p-4 rounded-xl shadow-lg hidden">
                <div class="bg-white rounded-lg p-4 grid grid-cols-1 md:grid-cols-3 gap-2">
                    <input type="text" placeholder="Where are you going?" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <input type="date" value="2026-09-07" class="border p-2.5 rounded-lg text-sm font-semibold">
                    <button class="bg-[#0071c2] text-white font-bold py-2.5 rounded-lg">Search activities</button>
                </div>
            </div>

            <!-- TAXIS FORM (Hidden by default) -->
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

        <!-- Left Column: Property Listings & Map View -->
        <div class="lg:col-span-7 space-y-4">
            
            <div class="flex justify-between items-center bg-white p-3 rounded-lg border shadow-sm">
                <div>
                    <h2 class="font-bold text-base text-slate-900">El Paso: properties found</h2>
                    <p class="text-xs text-slate-500">Prices often go up, lock in a great price today!</p>
                </div>
                <button onclick="scrollToMap()" class="px-3 py-1.5 bg-blue-50 text-[#0071c2] font-bold rounded text-xs hover:bg-blue-100 transition flex items-center gap-1.5">
                    <p><i class="fa-solid fa-map-location-dot"></i> Show on map</p>
                </button>
            </div>

            <!-- Hotel List Container -->
            <div id="hotel-list" class="space-y-4">
                <!-- Dynamically Rendered via JS -->
            </div>

            <!-- Map View Section -->
            <div id="map-section" class="bg-white p-4 rounded-xl border shadow-sm mt-6">
                <h3 class="font-bold text-sm mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-map-pin text-red-500"></i> Interactive Hotel Map
                </h3>
                <div id="map" class="shadow-inner"></div>
            </div>
        </div>

        <!-- Right Column: Booking Details, Summary & Affiliate Action -->
        <div class="lg:col-span-5 space-y-4">

            <div class="bg-white rounded-xl border shadow-lg p-5 sticky top-20">
                <div class="border-b pb-3 mb-3">
                    <span id="selected-type" class="text-[10px] font-bold uppercase text-amber-800 bg-amber-100 px-2 py-0.5 rounded">Hotel Stay</span>
                    <h3 id="selected-title" class="text-lg font-extrabold text-slate-900 mt-1">Americas Hotel - El Paso Airport</h3>
                    <p id="selected-location" class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot text-slate-400"></i> El Paso · 5.4 km from centre</p>
                </div>

                <div class="flex justify-between items-center mb-4 bg-slate-50 p-3 rounded-lg border">
                    <div>
                        <span class="text-xs text-slate-500 block">Rate per night</span>
                        <span id="selected-price" class="text-xl font-black text-slate-900">$ 75</span>
                    </div>
                    <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-1 rounded">
                        <i class="fa-solid fa-check"></i> Free cancellation
                    </span>
                </div>

                <!-- Room Configuration Options -->
                <div class="mb-4 space-y-2">
                    <label class="block text-xs font-bold text-slate-700">Select Room Option:</label>
                    <select id="room-type-select" onchange="calculateTotal()" class="w-full bg-slate-100 border rounded-lg p-2.5 text-xs font-semibold focus:outline-none">
                        <option value="standard" data-multiplier="1">Standard Double Room ($75/night)</option>
                        <option value="executive" data-multiplier="1.4">Executive Suite with Breakfast ($105/night)</option>
                        <option value="deluxe" data-multiplier="1.9">Deluxe King Room Sea View ($145/night)</option>
                    </select>
                </div>

                <!-- Dynamic Calculation Summary -->
                <div class="bg-slate-50 p-3 rounded-lg border space-y-1.5 text-xs mb-4">
                    <div class="flex justify-between text-slate-600">
                        <span>Duration (<span id="calc-nights">1</span> night):</span>
                        <span id="calc-base">$ 75</span>
                    </div>
                    <div class="flex justify-between text-slate-600">
                        <span>Taxes & Fees (10%):</span>
                        <span id="calc-tax">$ 8</span>
                    </div>
                    <div class="border-t pt-2 flex justify-between font-extrabold text-slate-900 text-sm">
                        <span>Total Price:</span>
                        <span id="calc-total" class="text-[#0071c2]">$ 83</span>
                    </div>
                </div>

                <!-- Payment Methods (US & Global Credit Cards) -->
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

                <!-- Booking / Affiliate Confirm Action -->
                <button onclick="confirmBooking()" class="w-full bg-[#0071c2] hover:bg-[#00487a] text-white font-bold py-3.5 rounded-lg shadow transition flex items-center justify-center gap-2 text-sm">
                    <i class="fa-solid fa-lock"></i> Reserve & Get PDF Voucher
                </button>
            </div>

            <!-- Booking.com Support Desk Widget -->
            <div class="bg-blue-900 text-white rounded-xl p-4 shadow-md">
                <div class="flex items-center gap-3 mb-2">
                    <div class="w-10 h-10 bg-[#febb02] rounded-full flex items-center justify-center font-bold text-blue-950">
                        <i class="fa-solid fa-headset"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-sm">Booking.com Support</h4>
                        <p class="text-[11px] text-blue-200">24/7 Global Partner Desk</p>
                    </div>
                </div>
                <p class="text-xs text-blue-100 mb-3">Manage or modify your active booking instantly via official support live chat.</p>
                <button onclick="openChat()" class="w-full bg-[#febb02] hover:bg-amber-400 text-blue-950 font-black py-2.5 rounded-lg text-xs transition">
                    Start Live Support Chat
                </button>
            </div>

        </div>
    </main>

    <!-- Hidden Printable Voucher Template (For html2pdf) -->
    <div class="hidden">
        <div id="pdf-voucher" class="p-8 bg-white text-slate-800 max-w-2xl mx-auto border-2 border-slate-200">
            <div class="flex justify-between items-center border-b pb-4 mb-6">
                <div>
                    <h1 class="text-2xl font-bold text-[#003580]">Booking.com Voucher</h1>
                    <p class="text-xs text-slate-500">Official Reservation Confirmation</p>
                </div>
                <div class="text-right">
                    <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">CONFIRMED</span>
                    <p class="text-xs text-slate-400 mt-1">Confirmation No: <span id="voucher-id">BK-789421</span></p>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4 mb-6 text-sm">
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Property Name</p>
                    <p id="v-hotel" class="font-bold text-slate-900">Americas Hotel - El Paso Airport</p>
                    <p id="v-location" class="text-xs text-slate-600">El Paso, TX</p>
                </div>
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Check-in / Check-out</p>
                    <p class="font-bold text-slate-900"><span id="v-checkin"></span> to <span id="v-checkout"></span></p>
                </div>
            </div>

            <div class="border-t border-b py-4 mb-6 space-y-2 text-sm">
                <div class="flex justify-between">
                    <span>Selected Option:</span>
                    <span id="v-room" class="font-bold">Standard Double Room</span>
                </div>
                <div class="flex justify-between">
                    <span>Total Amount Paid:</span>
                    <span id="v-total" class="font-bold text-[#003580]">$ 83</span>
                </div>
                <div class="flex justify-between">
                    <span>Payment Method:</span>
                    <span id="v-payment" class="font-bold text-emerald-600">Visa Card</span>
                </div>
            </div>

            <div class="flex justify-between items-center text-xs text-slate-500">
                <p>For support or changes, visit Booking.com Help Center.<br>Powered by Official Affiliate Partner Program</p>
                <div class="w-16 h-16 bg-slate-200 flex items-center justify-center font-bold text-slate-400 text-[10px]">
                    QR CODE
                </div>
            </div>
        </div>
    </div>

    <!-- Booking.com Live Chat Modal -->
    <div id="chat-modal" class="fixed bottom-4 right-4 w-80 bg-white rounded-xl shadow-2xl border z-50 hidden">
        <div class="bk-blue text-white p-3 rounded-t-xl flex justify-between items-center">
            <span class="font-bold text-xs">Booking.com Support Live Chat</span>
            <button onclick="closeChat()"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div id="chat-messages" class="p-3 h-48 overflow-y-auto space-y-2 text-xs">
            <div class="bg-slate-100 p-2.5 rounded-lg text-slate-800">
                Hello! Welcome to Booking.com customer support desk. How can we help you today?
            </div>
        </div>
        <div class="p-2 border-t flex gap-2">
            <input type="text" id="chat-input" placeholder="Type message..." class="w-full border rounded px-2 py-1.5 text-xs focus:outline-none">
            <button onclick="sendMessage()" class="bk-blue text-white px-3 rounded text-xs font-bold"><i class="fa-solid fa-paper-plane"></i></button>
        </div>
    </div>

    <!-- Leaflet JS for Maps -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <script>
        // Property Data Matching the User Screenshot
        const hotels = [
            {
                id: 1,
                name: "Americas Hotel - El Paso Airport / Medical Center",
                type: "Hotel",
                location: "El Paso",
                address: "El Paso · 5.4 km from centre",
                priceUSD: 75,
                rating: 8.6,
                ratingText: "Fabulous",
                reviews: 938,
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
                ratingText: "Very good",
                reviews: 452,
                image: "https://images.unsplash.com/photo-1582719508461-905c673771fd?auto=format&fit=crop&w=600&q=80",
                lat: 31.7820,
                lng: -106.4250
            },
            {
                id: 3,
                name: "Quality Inn & Suites Airport",
                type: "Resort",
                location: "El Paso",
                address: "El Paso · 7.6 km from centre",
                priceUSD: 85,
                rating: 8.0,
                ratingText: "Very good",
                reviews: 920,
                image: "https://images.unsplash.com/photo-1590490360182-c33d57733427?auto=format&fit=crop&w=600&q=80",
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
        });

        // Switch Navigation Tabs
        function switchTab(tab) {
            ['stays', 'flights', 'cars', 'attractions', 'taxis'].forEach(t => {
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
                            <div class="flex items-center gap-1 text-amber-500 text-[10px] my-0.5">
                                <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                            </div>
                            <p class="text-xs text-slate-500"><i class="fa-solid fa-location-dot"></i> ${hotel.address}</p>
                            <span class="inline-block mt-1 text-[10px] bg-emerald-50 text-emerald-700 font-bold px-1.5 py-0.5 rounded">Genius loyalty discount applied</span>
                        </div>
                        <div class="flex items-end justify-between border-t pt-2 mt-2">
                            <div>
                                <span class="text-[10px] text-slate-400 block">1 night, 2 adults</span>
                                <span class="text-lg font-black text-slate-900">$ ${hotel.priceUSD}</span>
                            </div>
                            <button class="px-3 py-1.5 bg-[#0071c2] hover:bg-[#00487a] text-white font-bold text-xs rounded transition">
                                See availability
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

            let baseCost = selectedHotel.priceUSD * multiplier * nights;
            let tax = Math.round(baseCost * 0.10);
            let total = baseCost + tax;

            document.getElementById('calc-base').innerText = `$ ${Math.round(baseCost)}`;
            document.getElementById('calc-tax').innerText = `$ ${tax}`;
            document.getElementById('calc-total').innerText = `$ ${total}`;
        }

        function confirmBooking() {
            const checkinVal = document.getElementById('checkin').value;
            const checkoutVal = document.getElementById('checkout').value;
            const totalVal = document.getElementById('calc-total').innerText;
            const paymentVal = document.querySelector('input[name="payment"]:checked').value;
            const roomText = document.getElementById('room-type-select').options[document.getElementById('room-type-select').selectedIndex].text;

            document.getElementById('v-hotel').innerText = selectedHotel.name;
            document.getElementById('v-location').innerText = selectedHotel.address;
            document.getElementById('v-checkin').innerText = checkinVal;
            document.getElementById('v-checkout').innerText = checkoutVal;
            document.getElementById('v-room').innerText = roomText;
            document.getElementById('v-total').innerText = totalVal;
            document.getElementById('v-payment').innerText = paymentVal;

            const element = document.getElementById('pdf-voucher');
            alert(`Booking Confirmed! (Paid via ${paymentVal})\nDownloading your PDF voucher now...`);
            html2pdf().from(element).save(`Booking_Voucher_${selectedHotel.name}.pdf`);
        }

        function scrollToMap() {
            document.getElementById('map-section').scrollIntoView({ behavior: 'smooth' });
        }

        function openChat() { document.getElementById('chat-modal').classList.remove('hidden'); }
        function closeChat() { document.getElementById('chat-modal').classList.add('hidden'); }

        function sendMessage() {
            const input = document.getElementById('chat-input');
            if (!input.value.trim()) return;
            const chatMessages = document.getElementById('chat-messages');
            
            const userMsg = document.createElement('div');
            userMsg.className = 'bg-blue-900 text-white p-2 rounded-lg max-w-[80%] ml-auto';
            userMsg.innerText = input.value;
            chatMessages.appendChild(userMsg);
            
            input.value = '';
            chatMessages.scrollTop = chatMessages.scrollHeight;

            setTimeout(() => {
                const botMsg = document.createElement('div');
                botMsg.className = 'bg-slate-100 p-2 rounded-lg max-w-[80%] text-slate-800';
                botMsg.innerText = "Thank you for contacting Booking.com Support. A representative will be with you shortly.";
                chatMessages.appendChild(botMsg);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }, 1000);
        }
    </script>
</body>
</html>

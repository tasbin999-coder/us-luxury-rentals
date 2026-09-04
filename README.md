<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StaySuite - Luxury Hotels, Vacation Rentals & Oceanfront Villas</title>
    
    <!-- SEO Primary Meta Tags -->
    <meta name="description" content="Book top-rated luxury hotels, beachfront villas, and executive penthouses across the US and Canada with instant confirmation and 24/7 support.">
    <meta name="robots" content="index, follow">

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
        #map { height: 100%; min-height: 350px; border-radius: 1rem; }
    </style>
</head>
<body class="bg-slate-100 text-slate-800">

    <!-- Header Navigation (Booking.com Dark Blue Style) -->
    <header class="bg-[#003580] text-white sticky top-0 z-40 shadow-lg">
        <div class="max-w-7xl mx-auto px-4 h-16 flex items-center justify-between">
            <div class="flex items-center gap-2.5">
                <div class="w-8 h-8 bg-amber-400 rounded-lg flex items-center justify-center font-black text-[#003580] text-lg shadow">
                    S
                </div>
                <span class="text-xl font-black tracking-tight">StaySuite</span>
            </div>
            
            <nav class="hidden md:flex items-center gap-6 font-semibold text-xs">
                <a href="#search" class="hover:text-amber-400 transition-colors">Search Stays</a>
                <a href="#featured" class="hover:text-amber-400 transition-colors">Properties</a>
                <a href="#map-section" class="hover:text-amber-400 transition-colors">Map View</a>
                <a href="#reviews-section" class="hover:text-amber-400 transition-colors">Reviews</a>
                <a href="#support" class="hover:text-amber-400 transition-colors">Support</a>
            </nav>
        </div>
    </header>

    <!-- Yellow Search Hero Bar (Booking.com Mobile Style) -->
    <section id="search" class="bg-[#003580] px-3 pb-8 pt-2">
        <div class="max-w-3xl mx-auto bg-[#febb02] rounded-2xl p-3.5 shadow-2xl space-y-2.5">
            <!-- Location Text Input -->
            <div class="bg-white rounded-xl px-3.5 py-2.5 flex items-center gap-2.5 border-2 border-amber-400">
                <i class="fa-solid fa-magnifying-glass text-slate-400"></i>
                <input type="text" id="destination" placeholder="Where are you going?" oninput="filterHotels()" class="w-full text-xs md:text-sm font-semibold bg-transparent focus:outline-none text-slate-900">
            </div>

            <!-- Date Selection Row -->
            <div class="grid grid-cols-2 gap-2">
                <div class="bg-white rounded-xl p-2.5 border border-slate-200">
                    <span class="text-[9px] uppercase font-bold text-slate-400 block">Check-in date</span>
                    <input type="date" id="checkin" value="2026-09-10" class="text-xs font-bold bg-transparent w-full focus:outline-none mt-0.5 text-slate-800" onchange="calculateTotal()">
                </div>
                <div class="bg-white rounded-xl p-2.5 border border-slate-200">
                    <span class="text-[9px] uppercase font-bold text-slate-400 block">Check-out date</span>
                    <input type="date" id="checkout" value="2026-09-12" class="text-xs font-bold bg-transparent w-full focus:outline-none mt-0.5 text-slate-800" onchange="calculateTotal()">
                </div>
            </div>

            <!-- Rooms Selection Row -->
            <div class="bg-white rounded-xl p-2.5 border border-slate-200">
                <span class="text-[9px] uppercase font-bold text-slate-400 block">Rooms</span>
                <select id="rooms" onchange="calculateTotal()" class="w-full bg-transparent text-xs font-bold focus:outline-none mt-0.5 text-slate-800">
                    <option value="1">1 Room</option>
                    <option value="2">2 Rooms</option>
                    <option value="3">3 Rooms</option>
                    <option value="4">4 Rooms</option>
                </select>
            </div>

            <button onclick="filterHotels()" class="w-full bg-[#0066f0] hover:bg-[#004bb5] text-white font-bold py-3 rounded-xl shadow transition text-xs uppercase tracking-wider">
                Search
            </button>
        </div>
    </section>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-3 py-8 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- Left Column: Hotel Listings (Left Text, Right Image layout as requested) -->
        <div id="featured" class="lg:col-span-7 space-y-4">
            <div class="flex justify-between items-center px-1">
                <h2 class="text-base font-extrabold text-slate-900">Available Properties</h2>
                <span class="text-xs text-slate-500">Click photo to view details</span>
            </div>

            <!-- Hotel List Container -->
            <div id="hotel-list" class="space-y-4">
                <!-- Dynamically Rendered via JS -->
            </div>

            <!-- Guest Reviews Section -->
            <div id="reviews-section" class="bg-white p-5 rounded-2xl border border-slate-200 shadow-sm space-y-3 mt-6">
                <h3 class="text-sm font-bold flex items-center gap-2">
                    <i class="fa-solid fa-star text-amber-500"></i> Verified Guest Reviews
                </h3>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-xs">
                    <div class="bg-slate-50 p-3 rounded-xl border border-slate-200 space-y-1.5">
                        <div class="flex justify-between items-center font-bold">
                            <span>Sarah M.</span>
                            <span class="text-amber-500"><i class="fa-solid fa-star"></i> 5.0</span>
                        </div>
                        <p class="text-slate-600">"Smooth booking process using my Amex card. Received instant confirmation!"</p>
                    </div>
                    <div class="bg-slate-50 p-3 rounded-xl border border-slate-200 space-y-1.5">
                        <div class="flex justify-between items-center font-bold">
                            <span>David K.</span>
                            <span class="text-amber-500"><i class="fa-solid fa-star"></i> 4.9</span>
                        </div>
                        <p class="text-slate-600">"The Booking.com support integration was very helpful. Excellent view."</p>
                    </div>
                </div>
            </div>

            <!-- Map View Section -->
            <div id="map-section" class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm mt-6">
                <h3 class="text-sm font-bold mb-2 flex items-center gap-2">
                    <i class="fa-solid fa-map-pin text-amber-500"></i> Interactive Property Map
                </h3>
                <div id="map"></div>
            </div>
        </div>

        <!-- Right Column: Booking Details & Checkout Card -->
        <div class="lg:col-span-5 space-y-6">

            <!-- Selected Hotel Booking Card -->
            <div class="bg-white rounded-2xl border border-slate-200 shadow-xl p-5 sticky top-20">
                <div class="flex justify-between items-start mb-3 border-b pb-3">
                    <div>
                        <span id="selected-type" class="text-[10px] font-bold uppercase tracking-wider text-amber-600 bg-amber-50 px-2 py-0.5 rounded-full">Oceanfront Villa</span>
                        <h3 id="selected-title" class="text-base font-extrabold text-slate-900 mt-1">Modern Oceanfront Villa in Miami</h3>
                        <p id="selected-location" class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot text-slate-400"></i> South Beach, Miami, FL</p>
                    </div>
                    <div class="text-right">
                        <span id="selected-price" class="text-xl font-black text-blue-950">$ 450</span>
                        <span class="text-[10px] text-slate-400 block">/ night</span>
                    </div>
                </div>

                <!-- Status Badges -->
                <div class="mb-3 flex flex-wrap gap-1.5 text-[10px]">
                    <span id="stock-badge" class="bg-amber-50 text-amber-800 font-bold px-2 py-0.5 rounded-full flex items-center gap-1 border border-amber-200">
                        <i class="fa-solid fa-box-open"></i> Limited Inventory
                    </span>
                    <span class="bg-blue-50 text-blue-700 font-bold px-2 py-0.5 rounded-full flex items-center gap-1 border border-blue-200">
                        <i class="fa-solid fa-shield-halved"></i> Confirmed Booking
                    </span>
                </div>

                <!-- Notice Alert -->
                <div id="availability-alert" class="hidden mb-3 p-2.5 bg-amber-50 border border-amber-300 rounded-xl text-[11px] text-amber-900 space-y-1">
                    <p class="font-bold flex items-center gap-1 text-amber-800">
                        <i class="fa-solid fa-circle-exclamation text-amber-600"></i> Notice: Selected Option Currently Unavailable
                    </p>
                    <p class="text-[10px] text-amber-800">Certain room types are out of stock for your selected dates.</p>
                </div>

                <!-- Room Category Selection -->
                <div class="mb-4 space-y-2 text-xs">
                    <label class="block font-bold text-slate-700">Select Room / Suite Category:</label>
                    <select id="room-type-select" onchange="calculateTotal()" class="w-full bg-slate-100 border border-slate-300 rounded-lg p-2 font-semibold focus:outline-none">
                        <option value="standard" data-multiplier="1" data-available="true">Standard Deluxe Villa (Available)</option>
                        <option value="executive" data-multiplier="1.3" data-available="true">Ocean View Executive Suite (+30%)</option>
                        <option value="suite" data-multiplier="1.8" data-available="false">Presidential Penthouse (Out of Stock)</option>
                    </select>
                </div>

                <!-- Add-on Services -->
                <div class="mb-4 text-xs">
                    <h4 class="font-bold text-slate-900 mb-2 uppercase tracking-wider">Add Extra Services:</h4>
                    <div class="space-y-1.5">
                        <label class="flex items-center justify-between bg-slate-50 p-2.5 rounded-xl border border-slate-200 cursor-pointer hover:bg-slate-100">
                            <span class="flex items-center gap-2">
                                <input type="checkbox" id="addon-breakfast" class="rounded text-blue-600" onchange="calculateTotal()">
                                <i class="fa-solid fa-utensils text-amber-500"></i> Daily Gourmet Breakfast
                            </span>
                            <span class="font-bold text-slate-700">+ $ 35</span>
                        </label>
                        <label class="flex items-center justify-between bg-slate-50 p-2.5 rounded-xl border border-slate-200 cursor-pointer hover:bg-slate-100">
                            <span class="flex items-center gap-2">
                                <input type="checkbox" id="addon-pickup" class="rounded text-blue-600" onchange="calculateTotal()">
                                <i class="fa-solid fa-car text-blue-500"></i> VIP Airport Transfer
                            </span>
                            <span class="font-bold text-slate-700">+ $ 90</span>
                        </label>
                    </div>
                </div>

                <!-- Price Calculation Summary -->
                <div class="bg-slate-50 p-3 rounded-xl border border-slate-200 space-y-1.5 text-xs mb-4">
                    <div class="flex justify-between text-slate-600">
                        <span>Stay Duration (<span id="calc-nights">2</span> nights, <span id="calc-rooms-count">1</span> room):</span>
                        <span id="calc-base">$ 900</span>
                    </div>
                    <div class="flex justify-between text-slate-600">
                        <span>Extra Add-ons:</span>
                        <span id="calc-addons">$ 0</span>
                    </div>
                    <div class="border-t pt-1.5 flex justify-between font-extrabold text-slate-900 text-sm">
                        <span>Total Price:</span>
                        <span id="calc-total" class="text-blue-950">$ 900</span>
                    </div>
                </div>

                <!-- Payment Options -->
                <div class="mb-4 text-xs">
                    <label class="block font-bold text-slate-700 mb-1.5 uppercase">Payment Method:</label>
                    <div class="grid grid-cols-3 gap-1.5 text-center mb-2">
                        <label class="border rounded-lg p-1.5 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-0.5">
                            <input type="radio" name="payment" value="Visa / Mastercard" checked class="hidden">
                            <i class="fa-brands fa-cc-visa text-blue-700 text-base"></i> Visa / Master
                        </label>
                        <label class="border rounded-lg p-1.5 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-0.5">
                            <input type="radio" name="payment" value="American Express" class="hidden">
                            <i class="fa-brands fa-cc-amex text-cyan-600 text-base"></i> Amex
                        </label>
                        <label class="border rounded-lg p-1.5 cursor-pointer bg-white font-bold hover:border-blue-600 flex flex-col items-center gap-0.5">
                            <input type="radio" name="payment" value="Apple Pay" class="hidden">
                            <i class="fa-brands fa-apple text-slate-800 text-base"></i> Apple Pay
                        </label>
                    </div>
                </div>

                <!-- Booking Action Button -->
                <button id="book-now-btn" onclick="confirmBooking()" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white font-extrabold py-3.5 rounded-xl shadow-lg transition flex items-center justify-center gap-2 text-xs uppercase tracking-wider">
                    <i class="fa-solid fa-circle-check"></i> Confirm Reservation & Get PDF Voucher
                </button>
            </div>

            <!-- Booking.com Partner Support Section -->
            <div id="support" class="bg-gradient-to-r from-blue-900 to-indigo-950 text-white rounded-2xl p-5 shadow-xl border border-blue-800">
                <div class="flex items-center gap-3 mb-3">
                    <div class="w-10 h-10 bg-amber-500 rounded-full flex items-center justify-center font-bold text-blue-950 text-base shadow">
                        <i class="fa-solid fa-headset"></i>
                    </div>
                    <div>
                        <h4 class="font-bold text-sm">Booking.com Partner Support</h4>
                        <p class="text-[10px] text-blue-200">Official Customer & Partner Care</p>
                    </div>
                </div>
                <p class="text-xs text-blue-100 mb-3 leading-relaxed">
                    For booking inquiries or cancellations, access official Booking.com partner help portals.
                </p>
                <div class="space-y-1.5 text-xs">
                    <button onclick="openChat()" class="w-full bg-amber-500 hover:bg-amber-600 text-blue-950 font-bold py-2.5 rounded-xl shadow transition flex items-center justify-center gap-2">
                        <i class="fa-solid fa-comments"></i> Start Live Chat
                    </button>
                    <a href="https://www.booking.com/help.html" target="_blank" rel="noopener noreferrer" class="w-full bg-white/10 hover:bg-white/20 text-white font-bold py-2 rounded-xl text-center border border-white/20 transition block">
                        Customer Help Center
                    </a>
                </div>
            </div>

        </div>
    </main>

    <!-- Property Detail Modal (Opens when photo is clicked) -->
    <div id="detail-modal" class="fixed inset-0 bg-black/70 backdrop-blur-sm z-50 hidden flex items-center justify-center p-3">
        <div class="bg-white rounded-2xl max-w-2xl w-full max-h-[90vh] overflow-y-auto p-5 relative space-y-4">
            <button onclick="closeModal()" class="absolute top-4 right-4 w-8 h-8 rounded-full bg-slate-100 text-slate-600 font-bold flex items-center justify-center">
                <i class="fa-solid fa-xmark"></i>
            </button>
            <h3 id="modal-title" class="text-lg font-bold text-slate-900">Property Details</h3>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-3">
                <img id="modal-img-1" src="" alt="View 1" class="rounded-xl h-44 w-full object-cover">
                <img id="modal-img-2" src="" alt="View 2" class="rounded-xl h-44 w-full object-cover">
            </div>

            <div class="space-y-2 text-xs text-slate-700">
                <p><strong>Address:</strong> <span id="modal-address"></span></p>
                <p><strong>Rating:</strong> <span id="modal-rating" class="text-amber-500 font-bold"></span></p>
                <p class="bg-blue-50 p-3 rounded-xl text-blue-900"><i class="fa-solid fa-circle-info"></i> All reservations include free Wi-Fi, air conditioning, access to swimming pool, and 24/7 customer service support.</p>
            </div>
        </div>
    </div>

    <!-- Hidden Printable Voucher Template -->
    <div class="hidden">
        <div id="pdf-voucher" class="p-8 bg-white text-slate-800 max-w-2xl mx-auto border-2 border-slate-200">
            <div class="flex justify-between items-center border-b pb-4 mb-6">
                <div>
                    <h1 class="text-xl font-bold text-blue-900">StaySuite Booking Voucher</h1>
                    <p class="text-xs text-slate-500">Official Reservation Confirmation</p>
                </div>
                <div class="text-right">
                    <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">CONFIRMED</span>
                    <p class="text-xs text-slate-400 mt-1">Booking ID: BK-984210</p>
                </div>
            </div>
            <div class="space-y-2 text-xs">
                <p><strong>Property:</strong> <span id="v-hotel"></span></p>
                <p><strong>Location:</strong> <span id="v-location"></span></p>
                <p><strong>Check-in / Check-out:</strong> <span id="v-checkin"></span> to <span id="v-checkout"></span></p>
                <p><strong>Total Paid Amount:</strong> <span id="v-total" class="font-bold text-blue-900"></span></p>
            </div>
        </div>
    </div>

    <!-- Live Chat Modal -->
    <div id="chat-modal" class="fixed bottom-6 right-6 w-80 bg-white rounded-2xl shadow-2xl border z-50 hidden">
        <div class="bg-blue-900 text-white p-3 rounded-t-2xl flex justify-between items-center text-xs">
            <span class="font-bold">Booking.com Support Desk</span>
            <button onclick="closeChat()"><i class="fa-solid fa-xmark"></i></button>
        </div>
        <div id="chat-messages" class="p-3 h-48 overflow-y-auto space-y-2 text-xs bg-slate-50">
            <div class="bg-white p-2 rounded-lg border">Hello! How can we assist you with your booking today?</div>
        </div>
        <div class="p-2 border-t flex gap-1">
            <input type="text" id="chat-input" placeholder="Type message..." class="w-full bg-slate-100 border rounded px-2 py-1 text-xs focus:outline-none">
            <button onclick="sendMessage()" class="bg-blue-900 text-white px-3 rounded text-xs font-bold"><i class="fa-solid fa-paper-plane"></i></button>
        </div>
    </div>

    <!-- Leaflet JS -->
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

    <script>
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

        document.addEventListener('DOMContentLoaded', () => {
            renderHotelList(hotels);
            initMap(hotels);
            calculateTotal();
        });

        function formatPrice(amountUSD) {
            return `$ ${amountUSD.toLocaleString()}`;
        }

        // Render Hotel List: Left Side Details, Right Side Image (Click photo to open details modal)
        function renderHotelList(data) {
            const container = document.getElementById('hotel-list');
            container.innerHTML = '';

            data.forEach(hotel => {
                const card = document.createElement('div');
                card.className = `bg-white rounded-2xl border ${selectedHotel.id === hotel.id ? 'border-2 border-blue-600 shadow-md' : 'border-slate-200'} p-4 shadow-sm hover:shadow-md transition flex flex-col sm:flex-row gap-4 items-center`;
                
                card.innerHTML = `
                    <div class="w-full sm:w-7/12 flex flex-col justify-between space-y-2">
                        <div>
                            <div class="flex items-center gap-2">
                                <span class="bg-amber-100 text-amber-800 text-[10px] font-bold px-2 py-0.5 rounded">${hotel.type}</span>
                                <span class="text-xs text-amber-500 font-bold"><i class="fa-solid fa-star"></i> ${hotel.rating} (${hotel.reviews})</span>
                            </div>
                            <h3 onclick="selectHotel(${hotel.id})" class="text-sm font-bold text-slate-900 mt-1 cursor-pointer hover:text-blue-600">${hotel.name}</h3>
                            <p class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot"></i> ${hotel.address}</p>
                        </div>
                        <div class="flex items-center justify-between border-t pt-2">
                            <div>
                                <span class="text-base font-black text-blue-950">${formatPrice(hotel.priceUSD)}</span>
                                <span class="text-[10px] text-slate-400">/ night</span>
                            </div>
                            <button onclick="selectHotel(${hotel.id})" class="px-3 py-1.5 bg-blue-900 hover:bg-blue-800 text-white font-bold text-xs rounded-lg shadow">
                                Select Stay
                            </button>
                        </div>
                    </div>
                    <div class="w-full sm:w-5/12 h-36 rounded-xl overflow-hidden relative cursor-pointer group" onclick="openDetailModal(${hotel.id})">
                        <img src="${hotel.images[0]}" alt="${hotel.name}" class="w-full h-full object-cover group-hover:scale-105 transition duration-300">
                        <div class="absolute inset-0 bg-black/20 group-hover:bg-black/0 transition flex items-center justify-center">
                            <span class="bg-black/60 text-white text-[10px] px-2 py-1 rounded backdrop-blur-sm opacity-0 group-hover:opacity-100 transition">View Details</span>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        // Initialize Map
        function initMap(data) {
            map = L.map('map').setView([25.7617, -80.1918], 4);
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
                    .bindPopup(`<b>${hotel.name}</b><br>Rate: ${formatPrice(hotel.priceUSD)} / night`)
                    .addTo(markersGroup);
            });
            if (data.length > 0) map.setView([data[0].lat, data[0].lng], 5);
        }

        function selectHotel(id) {
            selectedHotel = hotels.find(h => h.id === id);
            document.getElementById('selected-type').innerText = selectedHotel.type;
            document.getElementById('selected-title').innerText = selectedHotel.name;
            document.getElementById('selected-location').innerHTML = `<i class="fa-solid fa-location-dot text-slate-400"></i> ${selectedHotel.address}`;
            document.getElementById('selected-price').innerText = formatPrice(selectedHotel.priceUSD);
            renderHotelList(hotels);
            calculateTotal();
        }

        // Click photo to open detail modal
        function openDetailModal(id) {
            const h = hotels.find(item => item.id === id);
            document.getElementById('modal-title').innerText = h.name;
            document.getElementById('modal-address').innerText = h.address;
            document.getElementById('modal-rating').innerText = `${h.rating} / 5.0 (${h.reviews} reviews)`;
            document.getElementById('modal-img-1').src = h.images[0];
            document.getElementById('modal-img-2').src = h.images[1] || h.images[0];
            document.getElementById('detail-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('detail-modal').classList.add('hidden');
        }

        function filterHotels() {
            const query = document.getElementById('destination').value.toLowerCase().trim();
            const filtered = hotels.filter(h => h.name.toLowerCase().includes(query) || h.location.toLowerCase().includes(query) || h.address.toLowerCase().includes(query));
            if (filtered.length > 0) {
                renderHotelList(filtered);
                updateMapMarkers(filtered);
                selectHotel(filtered[0].id);
            } else {
                renderHotelList(hotels);
                updateMapMarkers(hotels);
            }
        }

        function calculateTotal() {
            const checkin = new Date(document.getElementById('checkin').value);
            const checkout = new Date(document.getElementById('checkout').value);
            let nights = Math.ceil(Math.abs(checkout - checkin) / (1000 * 60 * 60 * 24));
            if (isNaN(nights) || nights <= 0) nights = 1;

            const roomCount = parseInt(document.getElementById('rooms').value) || 1;
            document.getElementById('calc-nights').innerText = nights;
            document.getElementById('calc-rooms-count').innerText = roomCount;

            const roomSelect = document.getElementById('room-type-select');
            const selectedOpt = roomSelect.options[roomSelect.selectedIndex];
            const multiplier = parseFloat(selectedOpt.getAttribute('data-multiplier')) || 1;
            const isAvailable = selectedOpt.getAttribute('data-available') === 'true';

            const alertBox = document.getElementById('availability-alert');
            const bookBtn = document.getElementById('book-now-btn');
            const stockBadge = document.getElementById('stock-badge');

            if (!isAvailable) {
                alertBox.classList.remove('hidden');
                stockBadge.className = 'bg-red-50 text-red-700 font-bold px-2 py-0.5 rounded-full flex items-center gap-1 border border-red-200 text-[10px]';
                stockBadge.innerHTML = `<i class="fa-solid fa-circle-xmark"></i> Out of Stock`;
                bookBtn.disabled = true;
                bookBtn.className = 'w-full bg-slate-300 text-slate-500 font-bold py-3.5 rounded-xl cursor-not-allowed text-xs uppercase';
            } else {
                alertBox.classList.add('hidden');
                stockBadge.className = 'bg-amber-50 text-amber-800 font-bold px-2 py-0.5 rounded-full flex items-center gap-1 border border-amber-200 text-[10px]';
                stockBadge.innerHTML = `<i class="fa-solid fa-box-open"></i> Limited Inventory`;
                bookBtn.disabled = false;
                bookBtn.className = 'w-full bg-emerald-600 hover:bg-emerald-700 text-white font-extrabold py-3.5 rounded-xl shadow-lg transition flex items-center justify-center gap-2 text-xs uppercase tracking-wider';
            }

            let baseCost = selectedHotel.priceUSD * multiplier * nights * roomCount;
            let addonsCost = 0;
            if (document.getElementById('addon-breakfast').checked) addonsCost += 35 * nights * roomCount;
            if (document.getElementById('addon-pickup').checked) addonsCost += 90;

            let total = baseCost + addonsCost;
            document.getElementById('calc-base').innerText = formatPrice(baseCost);
            document.getElementById('calc-addons').innerText = formatPrice(addonsCost);
            document.getElementById('calc-total').innerText = formatPrice(total);
        }

        function confirmBooking() {
            document.getElementById('v-hotel').innerText = selectedHotel.name;
            document.getElementById('v-location').innerText = selectedHotel.address;
            document.getElementById('v-checkin').innerText = document.getElementById('checkin').value;
            document.getElementById('v-checkout').innerText = document.getElementById('checkout').value;
            document.getElementById('v-total').innerText = document.getElementById('calc-total').innerText;

            const element = document.getElementById('pdf-voucher');
            alert('Reservation confirmed successfully! Downloading PDF voucher...');
            html2pdf().from(element).save(`Booking_Voucher_${selectedHotel.name}.pdf`);
        }

        function openChat() { document.getElementById('chat-modal').classList.remove('hidden'); }
        function closeChat() { document.getElementById('chat-modal').classList.add('hidden'); }
        function sendMessage() {
            const input = document.getElementById('chat-input');
            if(!input.value) return;
            const msgBox = document.getElementById('chat-messages');
            msgBox.innerHTML += `<div class="bg-blue-100 p-2 rounded-lg text-right">${input.value}</div>`;
            input.value = '';
            setTimeout(() => {
                msgBox.innerHTML += `<div class="bg-white p-2 rounded-lg border">Thank you! A support representative will assist you shortly.</div>`;
                msgBox.scrollTop = msgBox.scrollHeight;
            }, 1000);
        }
    </script>
</body>
</html>

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <title>Global Travel & Rental Services - Official Booking Hub</title>
    
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
        .bk-yellow { background-color: #d4af37; }
        #map { height: 100%; min-height: 350px; border-radius: 0.75rem; }
    </style>
</head>
<body class="text-slate-800">

    <!-- Header Navigation -->
    <header class="bk-blue text-white sticky top-0 z-50 shadow-md">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-2">
                <i class="fa-solid fa-globe text-amber-400 text-2xl"></i>
                <a href="#" class="text-xl sm:text-2xl font-black tracking-tight text-white">Global Travel Hub</a>
            </div>
            
            <div class="flex items-center gap-3">
                <button class="bg-amber-400 text-slate-900 px-3.5 py-1.5 rounded text-xs font-bold hover:bg-amber-500 transition hidden sm:block">Partner Portal</button>
                <div class="w-8 h-8 rounded-full bg-slate-700 flex items-center justify-center font-bold text-xs border border-white/30 cursor-pointer">
                    <i class="fa-solid fa-user"></i>
                </div>
            </div>
        </div>

        <!-- Sub Navigation Tabs -->
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 flex items-center gap-2 overflow-x-auto pb-3 text-sm">
            <button onclick="switchTab('flights')" id="tab-flights" class="flex items-center gap-2 px-4 py-2 rounded-full border border-white/40 bg-white/10 font-semibold text-white whitespace-nowrap transition">
                <i class="fa-solid fa-plane"></i> Flights
            </button>
            <button onclick="switchTab('cars')" id="tab-cars" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-car"></i> Car Rentals
            </button>
            <button onclick="switchTab('tours')" id="tab-tours" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-ticket"></i> Tours & Tickets
            </button>
            <button onclick="switchTab('connectivity')" id="tab-connectivity" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-wifi"></i> eSIM & Data
            </button>
            <button onclick="switchTab('services')" id="tab-services" class="flex items-center gap-2 px-4 py-2 rounded-full border border-transparent hover:bg-white/10 font-semibold text-white/90 whitespace-nowrap transition">
                <i class="fa-solid fa-shield-halved"></i> Travel Services
            </button>
        </div>
    </header>

    <!-- Search Hero Bar -->
    <section class="bk-blue pb-10 pt-4 px-3 sm:px-6">
        <div class="max-w-6xl mx-auto">
            
            <!-- FLIGHTS FORM (Aviasales Link) -->
            <div id="form-flights" class="bg-[#d4af37] p-4 rounded-xl shadow-lg space-y-3">
                <div class="text-white">
                    <h2 class="text-xl font-extrabold">Find Cheap Flights Worldwide</h2>
                    <p class="text-xs text-slate-900 font-semibold">Compare hundreds of airlines instantly</p>
                </div>
                <div class="bg-white p-4 rounded-xl grid grid-cols-1 md:grid-cols-4 gap-2">
                    <div class="border p-2.5 rounded-lg">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">From</label>
                        <input type="text" value="New York (NYC)" class="w-full font-semibold text-sm focus:outline-none bg-transparent">
                    </div>
                    <div class="border p-2.5 rounded-lg">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">To</label>
                        <input type="text" value="London (LON)" class="w-full font-semibold text-sm focus:outline-none bg-transparent">
                    </div>
                    <div class="border p-2.5 rounded-lg">
                        <label class="block text-[10px] font-bold text-slate-500 uppercase">Departure Date</label>
                        <input type="date" value="2026-09-15" class="w-full font-semibold text-xs focus:outline-none bg-transparent">
                    </div>
                    <div class="flex items-end">
                        <a href="https://aviasales.tpm.lv/LkbR8J0q" target="_blank" class="w-full bg-[#0b2545] hover:bg-[#13315c] text-white font-bold py-3 px-4 rounded-lg shadow text-center text-sm transition block">Search Flights</a>
                    </div>
                </div>
            </div>

            <!-- CAR RENTALS FORM (Multiple Rental Links Integrated) -->
            <div id="form-cars" class="bg-[#0b2545] p-4 rounded-xl shadow-lg hidden space-y-4 text-white">
                <div>
                    <h2 class="text-2xl font-extrabold">Car Rentals & Transfers</h2>
                    <p class="text-xs text-slate-300 mt-1">Book reliable cars, bikes, and airport transfers worldwide</p>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-3">
                    <a href="https://autoeurope.tpm.lv/leYqq4oc" target="_blank" class="bg-white text-slate-900 p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-car text-3xl text-blue-600 mb-2"></i>
                            <h3 class="font-bold text-sm">Auto Europe</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Global car rental network</p>
                        </div>
                        <span class="mt-4 bg-blue-600 text-white text-xs font-bold py-2 rounded block">Book Car</span>
                    </a>
                    <a href="https://localrent.tpm.lv/k3JC1w22" target="_blank" class="bg-white text-slate-900 p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-car-side text-3xl text-emerald-600 mb-2"></i>
                            <h3 class="font-bold text-sm">LocalRent</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Local car rental deals</p>
                        </div>
                        <span class="mt-4 bg-emerald-600 text-white text-xs font-bold py-2 rounded block">Book Car</span>
                    </a>
                    <a href="https://economybookings.tpm.lv/8xoVpB6R" target="_blank" class="bg-white text-slate-900 p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-tags text-3xl text-amber-600 mb-2"></i>
                            <h3 class="font-bold text-sm">Economy Bookings</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Best economy rates</p>
                        </div>
                        <span class="mt-4 bg-amber-600 text-white text-xs font-bold py-2 rounded block">Compare Cars</span>
                    </a>
                    <a href="https://qeeq.tpm.lv/Jk6f2YEI" target="_blank" class="bg-white text-slate-900 p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-shield-car text-3xl text-indigo-600 mb-2"></i>
                            <h3 class="font-bold text-sm">QEEQ</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Price drop protection</p>
                        </div>
                        <span class="mt-4 bg-indigo-600 text-white text-xs font-bold py-2 rounded block">Rent Now</span>
                    </a>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 pt-2">
                    <a href="https://gettransfer.tpm.lv/VQ8SxFBs" target="_blank" class="bg-white/10 border border-white/20 p-3 rounded-lg flex items-center justify-between hover:bg-white/20 transition">
                        <span class="text-xs font-bold"><i class="fa-solid fa-taxi mr-2 text-amber-400"></i> GetTransfer (Airport Transfers)</span>
                        <i class="fa-solid fa-arrow-right text-xs"></i>
                    </a>
                    <a href="https://getrentacar.tpm.lv/edGLJb3R" target="_blank" class="bg-white/10 border border-white/20 p-3 rounded-lg flex items-center justify-between hover:bg-white/20 transition">
                        <span class="text-xs font-bold"><i class="fa-solid fa-key mr-2 text-amber-400"></i> GetRentACar Hub</span>
                        <i class="fa-solid fa-arrow-right text-xs"></i>
                    </a>
                    <a href="https://bikesbooking.tpm.lv/4g1Xc0Eh" target="_blank" class="bg-white/10 border border-white/20 p-3 rounded-lg flex items-center justify-between hover:bg-white/20 transition">
                        <span class="text-xs font-bold"><i class="fa-solid fa-bicycle mr-2 text-amber-400"></i> BikesBooking (Bikes & Scooters)</span>
                        <i class="fa-solid fa-arrow-right text-xs"></i>
                    </a>
                </div>
            </div>

            <!-- TOURS & TICKETS FORM (Klook, Tiqets, GoCity, Wegotrip) -->
            <div id="form-tours" class="bg-[#d4af37] p-4 rounded-xl shadow-lg hidden space-y-4">
                <div class="text-slate-900">
                    <h2 class="text-xl font-extrabold">Tours, Attractions & Activities</h2>
                    <p class="text-xs font-semibold">Book skip-the-line tickets and guided city tours worldwide</p>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-3">
                    <a href="https://klook.tpm.lv/8wPSVTZI" target="_blank" class="bg-white p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-mountain-city text-3xl text-orange-500 mb-2"></i>
                            <h3 class="font-bold text-sm text-slate-900">Klook</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Activities & attractions</p>
                        </div>
                        <span class="mt-4 bg-orange-500 text-white text-xs font-bold py-2 rounded block">Explore</span>
                    </a>
                    <a href="https://tiqets.tpm.lv/VlBob9V6" target="_blank" class="bg-white p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-landmark text-3xl text-purple-600 mb-2"></i>
                            <h3 class="font-bold text-sm text-slate-900">Tiqets</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Museums & instant passes</p>
                        </div>
                        <span class="mt-4 bg-purple-600 text-white text-xs font-bold py-2 rounded block">Get Tickets</span>
                    </a>
                    <a href="https://gocity.tpm.lv/I6sd5yoD" target="_blank" class="bg-white p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-city text-3xl text-blue-600 mb-2"></i>
                            <h3 class="font-bold text-sm text-slate-900">Go City</h3>
                            <p class="text-[11px] text-slate-500 mt-1">All-inclusive sightseeing passes</p>
                        </div>
                        <span class="mt-4 bg-blue-600 text-white text-xs font-bold py-2 rounded block">View Passes</span>
                    </a>
                    <a href="https://wegotrip.tpm.lv/g4jnbaad" target="_blank" class="bg-white p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-headphones text-3xl text-emerald-600 mb-2"></i>
                            <h3 class="font-bold text-sm text-slate-900">Wegotrip</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Audio guides & excursions</p>
                        </div>
                        <span class="mt-4 bg-emerald-600 text-white text-xs font-bold py-2 rounded block">Book Tour</span>
                    </a>
                </div>
            </div>

            <!-- CONNECTIVITY FORM (Yesim, Airalo, Drimsim) -->
            <div id="form-connectivity" class="bg-[#0b2545] p-4 rounded-xl shadow-lg hidden space-y-4 text-white">
                <div>
                    <h2 class="text-2xl font-extrabold">Global eSIM & Internet Connectivity</h2>
                    <p class="text-xs text-slate-300 mt-1">Stay connected worldwide without high roaming fees</p>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
                    <a href="https://yesim.tpm.lv/gqNjfsQ7" target="_blank" class="bg-white text-slate-900 p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-sim-card text-3xl text-blue-600 mb-2"></i>
                            <h3 class="font-bold text-sm">Yesim eSIM</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Stable mobile data worldwide</p>
                        </div>
                        <span class="mt-4 bg-blue-600 text-white text-xs font-bold py-2 rounded block">Get eSIM</span>
                    </a>
                    <a href="https://airalo.tpm.lv/oBwdtAXD" target="_blank" class="bg-white text-slate-900 p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-signal text-3xl text-orange-500 mb-2"></i>
                            <h3 class="font-bold text-sm">Airalo</h3>
                            <p class="text-[11px] text-slate-500 mt-1">World's first eSIM store</p>
                        </div>
                        <span class="mt-4 bg-orange-500 text-white text-xs font-bold py-2 rounded block">Shop eSIM</span>
                    </a>
                    <a href="https://drimsim.tpm.lv/I6YGGiZD" target="_blank" class="bg-white text-slate-900 p-4 rounded-xl shadow hover:bg-slate-50 transition text-center flex flex-col justify-between">
                        <div>
                            <i class="fa-solid fa-globe text-3xl text-emerald-600 mb-2"></i>
                            <h3 class="font-bold text-sm">Drimsim</h3>
                            <p class="text-[11px] text-slate-500 mt-1">Universal SIM for travelers</p>
                        </div>
                        <span class="mt-4 bg-emerald-600 text-white text-xs font-bold py-2 rounded block">Order SIM</span>
                    </a>
                </div>
            </div>

            <!-- SERVICES FORM (Insurance, Luggage, Compensation, Intui, Radical) -->
            <div id="form-services" class="bg-[#d4af37] p-4 rounded-xl shadow-lg hidden space-y-4">
                <div class="text-slate-900">
                    <h2 class="text-xl font-extrabold">Essential Travel Services & Protection</h2>
                    <p class="text-xs font-semibold">Insurance, luggage storage, flight compensation & transfers</p>
                </div>
                <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-3">
                    <a href="https://tpm.lv/LM3BxMOS" target="_blank" class="bg-white p-3 rounded-lg shadow hover:bg-slate-50 text-center flex flex-col justify-between">
                        <i class="fa-solid fa-suitcase-rolling text-2xl text-blue-600 mb-1"></i>
                        <span class="text-xs font-bold text-slate-800">Travelpayouts Hub</span>
                    </a>
                    <a href="https://ektatraveling.tpm.lv/zx8HM9Hz" target="_blank" class="bg-white p-3 rounded-lg shadow hover:bg-slate-50 text-center flex flex-col justify-between">
                        <i class="fa-solid fa-heart-pulse text-2xl text-red-600 mb-1"></i>
                        <span class="text-xs font-bold text-slate-800">EKTA Insurance</span>
                    </a>
                    <a href="https://radicalstorage.tpm.lv/ouRqyZCP" target="_blank" class="bg-white p-3 rounded-lg shadow hover:bg-slate-50 text-center flex flex-col justify-between">
                        <i class="fa-solid fa-box-archive text-2xl text-amber-600 mb-1"></i>
                        <span class="text-xs font-bold text-slate-800">Radical Storage</span>
                    </a>
                    <a href="https://airhelp.tpm.lv/UhCIDYTV" target="_blank" class="bg-white p-3 rounded-lg shadow hover:bg-slate-50 text-center flex flex-col justify-between">
                        <i class="fa-solid fa-plane-circle-exclamation text-2xl text-indigo-600 mb-1"></i>
                        <span class="text-xs font-bold text-slate-800">AirHelp</span>
                    </a>
                    <a href="https://compensair.tpm.lv/9dNNHjiN" target="_blank" class="bg-white p-3 rounded-lg shadow hover:bg-slate-50 text-center flex flex-col justify-between">
                        <i class="fa-solid fa-file-invoice-dollar text-2xl text-emerald-600 mb-1"></i>
                        <span class="text-xs font-bold text-slate-800">Compensair</span>
                    </a>
                    <a href="https://intui.tpm.lv/lRJEmvXr" target="_blank" class="bg-white p-3 rounded-lg shadow hover:bg-slate-50 text-center flex flex-col justify-between">
                        <i class="fa-solid fa-van-shuttle text-2xl text-cyan-600 mb-1"></i>
                        <span class="text-xs font-bold text-slate-800">Intui.travel</span>
                    </a>
                </div>
            </div>

        </div>
    </section>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 py-8 grid grid-cols-1 lg:grid-cols-12 gap-6">

        <!-- Left Column: Dynamic Listings & Map View -->
        <div class="lg:col-span-7 space-y-4">
            <div class="flex justify-between items-center bg-white p-3 rounded-lg border shadow-sm">
                <div>
                    <h2 class="font-bold text-base text-slate-900">Featured Global Destinations</h2>
                    <p class="text-xs text-slate-500">Explore top locations with integrated travel partners</p>
                </div>
                <button onclick="scrollToMap()" class="px-3 py-1.5 bg-blue-50 text-[#0b2545] font-bold rounded text-xs hover:bg-blue-100 transition flex items-center gap-1.5">
                    <i class="fa-solid fa-map-location-dot"></i> Show on map
                </button>
            </div>

            <div id="hotel-list" class="space-y-4"></div>

            <div id="map-section" class="bg-white p-4 rounded-xl border shadow-sm mt-6">
                <h3 class="font-bold text-sm mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-map-pin text-red-500"></i> Interactive Destination Location Map
                </h3>
                <div id="map" class="shadow-inner"></div>
            </div>
        </div>

        <!-- Right Column: Booking Quick Summary & Voucher Panel -->
        <div class="lg:col-span-5 space-y-4">
            <div class="bg-white rounded-xl border shadow-lg p-5 sticky top-20">
                <div class="border-b pb-3 mb-3">
                    <span id="selected-type" class="text-[10px] font-bold uppercase text-amber-800 bg-amber-100 px-2 py-0.5 rounded">Global Partner Booking</span>
                    <h3 id="selected-title" class="text-lg font-extrabold text-slate-900 mt-1">London City Explorer Pass</h3>
                    <p id="selected-location" class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot text-slate-400"></i> London · Instant Confirmation</p>
                </div>

                <div class="flex justify-between items-center mb-4 bg-slate-50 p-3 rounded-lg border">
                    <div>
                        <span class="text-xs text-slate-500 block">Service Fee / Pass</span>
                        <span id="selected-price" class="text-xl font-black text-slate-900">$ 85</span>
                    </div>
                    <span class="bg-emerald-100 text-emerald-800 text-xs font-bold px-2 py-1 rounded">
                        <i class="fa-solid fa-check"></i> Instant E-Voucher
                    </span>
                </div>

                <div class="mb-4 space-y-2">
                    <label class="block text-xs font-bold text-slate-700">Select Service Provider:</label>
                    <select id="room-type-select" onchange="calculateTotal()" class="w-full bg-slate-100 border rounded-lg p-2.5 text-xs font-semibold focus:outline-none">
                        <option value="klook" data-price="85">Klook Tour Package ($85)</option>
                        <option value="tiqets" data-price="45">Tiqets Museum Pass ($45)</option>
                        <option value="gocity" data-price="120">Go City All-Inclusive Pass ($120)</option>
                        <option value="wegotrip" data-price="30">Wegotrip Audio Guide ($30)</option>
                    </select>
                </div>

                <div class="bg-slate-50 p-3 rounded-lg border space-y-1.5 text-xs mb-4">
                    <div class="flex justify-between text-slate-600">
                        <span>Items / Travelers:</span>
                        <span id="calc-nights">1 Traveler</span>
                    </div>
                    <div class="border-t pt-2 flex justify-between font-extrabold text-slate-900 text-sm">
                        <span>Total Price:</span>
                        <span id="calc-total" class="text-[#0b2545]">$ 85</span>
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
                    <i class="fa-solid fa-lock"></i> Confirm Booking & Download PDF Voucher
                </button>
            </div>
        </div>
    </main>

    <!-- Hidden Printable Voucher Template -->
    <div class="hidden">
        <div id="pdf-voucher" class="p-8 bg-white text-slate-800 max-w-2xl mx-auto border-2 border-slate-200">
            <div class="flex justify-between items-center border-b pb-4 mb-6">
                <div>
                    <h1 class="text-2xl font-bold text-[#0b2545]">Global Travel Hub</h1>
                    <p class="text-xs text-slate-500">Official Partner Booking Confirmation Voucher</p>
                </div>
                <div class="text-right">
                    <span class="text-xs font-bold bg-emerald-100 text-emerald-800 px-3 py-1 rounded-full">CONFIRMED</span>
                    <p class="text-xs text-slate-400 mt-1">Confirmation No: <span id="voucher-id">GTH-928410</span></p>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4 mb-6 text-sm">
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Service / Package</p>
                    <p id="v-hotel" class="font-bold text-slate-900">London City Explorer Pass</p>
                    <p id="v-location" class="text-xs text-slate-600">London Downtown</p>
                </div>
                <div>
                    <p class="text-xs text-slate-400 uppercase font-bold">Booking Date</p>
                    <p class="font-bold text-slate-900"><span id="v-checkin">2026-09-05</span></p>
                </div>
            </div>

            <div class="border-t border-b py-4 mb-6 space-y-2 text-sm">
                <div class="flex justify-between">
                    <span>Selected Category:</span>
                    <span id="v-room" class="font-bold">Klook Tour Package</span>
                </div>
                <div class="flex justify-between">
                    <span>Total Amount Paid:</span>
                    <span id="v-total" class="font-bold text-[#0b2545]">$ 85</span>
                </div>
                <div class="flex justify-between">
                    <span>Payment Method:</span>
                    <span id="v-payment" class="font-bold text-emerald-600">Visa Card</span>
                </div>
            </div>

            <div class="flex justify-between items-center text-xs text-slate-500">
                <p>For support or inquiries, visit Global Travel Hub Help Center.<br>Official Affiliate Booking Platform</p>
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
                name: "London City Explorer Pass",
                type: "Sightseeing Pass",
                location: "London",
                address: "Central London · Skip-the-line Access",
                priceUSD: 85,
                rating: 9.4,
                image: "https://images.unsplash.com/photo-1513635269975-59663e0ac1ad?auto=format&fit=crop&w=600&q=80",
                lat: 51.5074,
                lng: -0.1278
            },
            {
                id: 2,
                name: "Paris Museum & Louvre Tour",
                type: "Museum Pass",
                location: "Paris",
                address: "Paris City Center · Audio Guide Included",
                priceUSD: 45,
                rating: 9.6,
                image: "https://images.unsplash.com/photo-1502602898657-3e91760cbb34?auto=format&fit=crop&w=600&q=80",
                lat: 48.8566,
                lng: 2.3522
            },
            {
                id: 3,
                name: "New York All-Inclusive Pass",
                type: "Attraction Bundle",
                location: "New York",
                address: "Manhattan · 100+ Top Attractions",
                priceUSD: 120,
                rating: 9.8,
                image: "https://images.unsplash.com/photo-1496442226666-8d4d0e62e6e9?auto=format&fit=crop&w=600&q=80",
                lat: 40.7128,
                lng: -74.0060
            }
        ];

        let selectedHotel = hotels[0];
        let map, markersGroup;

        document.addEventListener('DOMContentLoaded', () => {
            renderHotelList(hotels);
            initMap(hotels);
            calculateTotal();
            switchTab('flights');
        });

        function switchTab(tab) {
            ['flights', 'cars', 'tours', 'connectivity', 'services'].forEach(t => {
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
                            <span class="inline-block mt-1 text-[10px] bg-emerald-50 text-emerald-700 font-bold px-1.5 py-0.5 rounded">Instant E-Voucher Available</span>
                        </div>
                        <div class="flex items-end justify-between border-t pt-2 mt-2">
                            <div>
                                <span class="text-[10px] text-slate-400 block">Package Price</span>
                                <span class="text-lg font-black text-slate-900">$ ${hotel.priceUSD}</span>
                            </div>
                            <button class="px-3 py-1.5 bg-[#0b2545] hover:bg-[#13315c] text-white font-bold text-xs rounded transition">
                                Select Pass
                            </button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function initMap(data) {
            map = L.map('map').setView([51.5074, -0.1278], 12);
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
                    .bindPopup(`<b>${hotel.name}</b><br>Price: $${hotel.priceUSD}`)
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
            const roomSelect = document.getElementById('room-type-select');
            const price = parseFloat(roomSelect.options[roomSelect.selectedIndex].getAttribute('data-price')) || 85;

            document.getElementById('calc-total').innerText = `$ ${price}`;
        }

        function confirmBooking() {
            const totalVal = document.getElementById('calc-total').innerText;
            const paymentVal = document.querySelector('input[name="payment"]:checked').value;
            const roomSelectElem = document.getElementById('room-type-select');
            const roomText = roomSelectElem.options[roomSelectElem.selectedIndex].text;

            document.getElementById('v-hotel').innerText = selectedHotel.name;
            document.getElementById('v-location').innerText = selectedHotel.address;
            document.getElementById('v-room').innerText = roomText;
            document.getElementById('v-total').innerText = totalVal;
            document.getElementById('v-payment').innerText = paymentVal + ' Card';

            const element = document.getElementById('pdf-voucher');
            alert(`Booking Confirmed! (Paid via ${paymentVal})\nDownloading your PDF voucher now...`);
            html2pdf().from(element).save(`Global_Travel_Voucher_${selectedHotel.name.replace(/\s+/g, '_')}.pdf`);
        }

        function scrollToMap() {
            document.getElementById('map-section').scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>

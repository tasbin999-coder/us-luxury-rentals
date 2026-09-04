<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>StaySuite - Hotel & Vacation Rental Booking</title>

    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- html2pdf.js for PDF Voucher Generation -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');
        body { font-family: 'Inter', sans-serif; }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 pb-12">

    <!-- Top Blue Header Navbar -->
    <header class="bg-[#003580] text-white px-4 py-3 sticky top-0 z-40 shadow-md">
        <div class="max-w-xl mx-auto flex items-center justify-between">
            <span class="text-xl font-black tracking-tight">StaySuite</span>
            <div class="flex items-center gap-3">
                <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center text-sm font-bold">
                    <i class="fa-solid fa-bell"></i>
                </div>
                <div class="w-8 h-8 rounded-full bg-white/10 flex items-center justify-center text-sm font-bold">
                    <i class="fa-solid fa-bars"></i>
                </div>
            </div>
        </div>

        <!-- Category Tabs (Stays, Flights, Car rental) -->
        <div class="max-w-xl mx-auto flex gap-2 overflow-x-auto pt-3 pb-1 scrollbar-none text-xs font-semibold">
            <button class="bg-white/20 px-4 py-2 rounded-full flex items-center gap-2 border border-white/30 whitespace-nowrap">
                <i class="fa-solid fa-bed"></i> Stays
            </button>
            <button class="px-4 py-2 rounded-full flex items-center gap-2 hover:bg-white/10 whitespace-nowrap">
                <i class="fa-solid fa-plane"></i> Flights
            </button>
            <button class="px-4 py-2 rounded-full flex items-center gap-2 hover:bg-white/10 whitespace-nowrap">
                <i class="fa-solid fa-car"></i> Car rental
            </button>
        </div>
    </header>

    <!-- Main Container -->
    <main class="max-w-xl mx-auto p-3 space-y-4">

        <!-- Booking.com Style Yellow Search Box -->
        <div class="bg-[#febb02] p-3 rounded-2xl shadow-lg space-y-2.5 text-slate-900">
            <!-- Location Input -->
            <div class="bg-white rounded-xl px-3 py-2.5 flex items-center justify-between border-2 border-amber-400">
                <div class="flex items-center gap-2.5 w-full">
                    <i class="fa-solid fa-magnifying-glass text-slate-400"></i>
                    <input type="text" id="search-query" value="El Paso" oninput="filterProperties()" placeholder="Where are you going?" class="w-full text-sm font-semibold bg-transparent focus:outline-none">
                </div>
                <i class="fa-solid fa-xmark text-slate-400 cursor-pointer" onclick="document.getElementById('search-query').value=''; filterProperties();"></i>
            </div>

            <!-- Date Selection Row -->
            <div class="grid grid-cols-2 gap-2">
                <div class="bg-white rounded-xl p-2.5 border border-slate-200">
                    <span class="text-[10px] uppercase font-bold text-slate-400 block">Check-in date</span>
                    <input type="date" id="checkin-date" value="2026-09-04" class="text-xs font-bold bg-transparent w-full focus:outline-none mt-0.5">
                </div>
                <div class="bg-white rounded-xl p-2.5 border border-slate-200">
                    <span class="text-[10px] uppercase font-bold text-slate-400 block">Check-out date</span>
                    <input type="date" id="checkout-date" value="2026-09-05" class="text-xs font-bold bg-transparent w-full focus:outline-none mt-0.5">
                </div>
            </div>

            <!-- Guests & Rooms Selector Row -->
            <div class="grid grid-cols-3 gap-2 bg-white rounded-xl p-2.5 border border-slate-200 text-xs font-semibold">
                <div>
                    <span class="text-[9px] uppercase text-slate-400 block">Adults</span>
                    <select id="adults-count" class="w-full bg-transparent font-bold focus:outline-none mt-0.5">
                        <option value="1">1 adult</option>
                        <option value="2" selected>2 adults</option>
                        <option value="3">3 adults</option>
                    </select>
                </div>
                <div>
                    <span class="text-[9px] uppercase text-slate-400 block">Children</span>
                    <select id="children-count" class="w-full bg-transparent font-bold focus:outline-none mt-0.5">
                        <option value="0" selected>0 children</option>
                        <option value="1">1 child</option>
                        <option value="2">2 children</option>
                    </select>
                </div>
                <div>
                    <span class="text-[9px] uppercase text-slate-400 block">Rooms</span>
                    <select id="rooms-count" class="w-full bg-transparent font-bold focus:outline-none mt-0.5">
                        <option value="1" selected>1 room</option>
                        <option value="2">2 rooms</option>
                    </select>
                </div>
            </div>

            <!-- Search Action Button -->
            <button onclick="filterProperties()" class="w-full bg-[#0066f0] hover:bg-[#004bb5] text-white font-bold py-3.5 rounded-xl shadow transition text-sm">
                Search
            </button>
        </div>

        <!-- Property List Section -->
        <div id="property-list" class="space-y-3">
            <!-- Dynamically populated via script -->
        </div>

        <!-- Detailed Modal View (Image 2 Inspired Detail View) -->
        <div id="detail-modal" class="fixed inset-0 bg-black/70 z-50 hidden flex justify-end flex-col">
            <div class="bg-white rounded-t-3xl max-h-[90vh] overflow-y-auto p-4 space-y-4">
                <div class="flex justify-between items-center border-b pb-3">
                    <h3 id="modal-title" class="font-extrabold text-base text-slate-900">Property Details</h3>
                    <button onclick="closeModal()" class="w-8 h-8 rounded-full bg-slate-100 flex items-center justify-center font-bold text-slate-600">
                        <i class="fa-solid fa-xmark"></i>
                    </button>
                </div>

                <!-- Property Image Gallery Carousel Preview -->
                <div class="h-48 rounded-xl overflow-hidden relative">
                    <img id="modal-img" src="" alt="Property" class="w-full h-full object-cover">
                    <span class="absolute bottom-2 right-2 bg-black/70 text-white text-[10px] px-2 py-1 rounded">1 / 5 Photos</span>
                </div>

                <!-- Basic Property Info -->
                <div>
                    <div id="modal-stars" class="text-amber-500 text-xs mb-1"></div>
                    <h4 id="modal-name" class="font-bold text-lg text-slate-900"></h4>
                    <p id="modal-address" class="text-xs text-slate-500 mt-0.5"><i class="fa-solid fa-location-dot"></i> <span id="modal-loc-text"></span></p>
                </div>

                <!-- Quick Facilities -->
                <div class="grid grid-cols-2 gap-2 text-xs text-slate-600 bg-slate-50 p-3 rounded-xl">
                    <div><i class="fa-solid fa-wifi text-blue-600"></i> Free high-speed Wi-Fi</div>
                    <div><i class="fa-solid fa-square-parking text-emerald-600"></i> Free parking space</div>
                    <div><i class="fa-solid fa-snowflake text-cyan-600"></i> Air conditioning</div>
                    <div><i class="fa-solid fa-mug-hot text-amber-600"></i> Breakfast included</div>
                </div>

                <!-- Room selection choices -->
                <div class="space-y-2">
                    <h5 class="text-xs font-bold uppercase tracking-wider text-slate-500">Available Options</h5>
                    <div class="border rounded-xl p-3 space-y-2 bg-slate-50/50">
                        <div class="flex justify-between items-start text-xs">
                            <div>
                                <p class="font-bold text-slate-900">Standard Double Room with Free Wi-Fi</p>
                                <p class="text-emerald-700 text-[10px] font-semibold mt-0.5">Free cancellation • No prepayment needed</p>
                            </div>
                            <span id="modal-price" class="font-extrabold text-blue-900 text-sm">$120</span>
                        </div>
                        <button onclick="confirmBooking()" class="w-full bg-[#0066f0] hover:bg-[#004bb5] text-white text-xs font-bold py-2.5 rounded-lg shadow">
                            Reserve Now & Get Voucher
                        </button>
                    </div>
                </div>
            </div>
        </div>

    </main>

    <!-- Hidden Voucher Template for PDF Generation -->
    <div class="hidden">
        <div id="pdf-voucher" class="p-6 bg-white text-slate-800 max-w-md mx-auto border rounded-xl">
            <div class="flex justify-between items-center border-b pb-3 mb-4">
                <div>
                    <h1 class="text-lg font-black text-[#003580]">StaySuite Booking</h1>
                    <p class="text-[10px] text-slate-500">Verified Reservation Voucher</p>
                </div>
                <span class="text-[10px] font-bold bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded">CONFIRMED</span>
            </div>
            <div class="space-y-2 text-xs">
                <p><strong>Property:</strong> <span id="v-hotel-name"></span></p>
                <p><strong>Location:</strong> <span id="v-hotel-loc"></span></p>
                <p><strong>Check-in:</strong> <span id="v-checkin"></span></p>
                <p><strong>Check-out:</strong> <span id="v-checkout"></span></p>
                <p><strong>Total Amount:</strong> <span id="v-price" class="font-bold text-[#0066f0]"></span></p>
            </div>
            <div class="mt-4 pt-3 border-t text-[10px] text-slate-400 flex justify-between items-center">
                <span>Booking ID: BK-849201</span>
                <span>Scan for support</span>
            </div>
        </div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        const properties = [
            {
                id: 1,
                name: "Americas Hotel - El Paso Airport / Medical Center",
                location: "El Paso",
                address: "El Paso • 5.4 km from centre",
                stars: 2,
                rating: 8.6,
                ratingText: "Fabulous",
                reviews: 938,
                price: 110,
                image: "https://images.unsplash.com/photo-1566073771259-6a8506099945?auto=format&fit=crop&w=600&q=80"
            },
            {
                id: 2,
                name: "Comfort Suites El Paso Airport",
                location: "El Paso",
                address: "El Paso • 8.9 km from centre",
                stars: 4,
                rating: 8.2,
                ratingText: "Very good",
                reviews: 452,
                price: 145,
                image: "https://images.unsplash.com/photo-1582719478250-c89cae4dc85b?auto=format&fit=crop&w=600&q=80"
            },
            {
                id: 3,
                name: "Quality Inn & Suites Airport",
                location: "El Paso",
                address: "El Paso • 7.6 km from centre",
                stars: 3,
                rating: 8.0,
                ratingText: "Very good",
                reviews: 920,
                price: 95,
                image: "https://images.unsplash.com/photo-1542314831-068cd1dbfeeb?auto=format&fit=crop&w=600&q=80"
            }
        ];

        let activeProperty = properties[0];

        document.addEventListener('DOMContentLoaded', () => {
            renderProperties(properties);
        });

        function renderProperties(data) {
            const container = document.getElementById('property-list');
            container.innerHTML = '';

            if (data.length === 0) {
                container.innerHTML = `<div class="bg-white p-6 rounded-2xl text-center text-xs text-slate-500">No properties found matching your search.</div>`;
                return;
            }

            data.forEach(prop => {
                const card = document.createElement('div');
                card.className = `bg-white rounded-2xl overflow-hidden shadow-sm border border-slate-200 flex flex-col sm:flex-row cursor-pointer hover:shadow-md transition`;
                card.onclick = () => openModal(prop.id);

                let starsHtml = '';
                for(let i=0; i<prop.stars; i++) starsHtml += '<i class="fa-solid fa-star text-amber-400 text-[10px]"></i>';

                card.innerHTML = `
                    <div class="sm:w-5/12 h-40 relative">
                        <img src="${prop.image}" alt="${prop.name}" class="w-full h-full object-cover">
                    </div>
                    <div class="sm:w-7/12 p-3.5 flex flex-col justify-between">
                        <div>
                            <div class="flex items-start justify-between gap-1">
                                <h3 class="font-bold text-xs text-slate-900 leading-snug">${prop.name}</h3>
                                <div class="flex gap-0.5">${starsHtml}</div>
                            </div>
                            <div class="flex items-center gap-1.5 mt-1">
                                <span class="bg-[#003580] text-white font-bold text-[10px] px-1.5 py-0.5 rounded">${prop.rating}</span>
                                <span class="font-bold text-[11px] text-slate-800">${prop.ratingText}</span>
                                <span class="text-[10px] text-slate-400">• ${prop.reviews} reviews</span>
                            </div>
                            <p class="text-[11px] text-slate-500 mt-1.5"><i class="fa-solid fa-location-dot"></i> ${prop.address}</p>
                        </div>
                        <div class="flex justify-between items-end border-t pt-2 mt-2">
                            <span class="text-[10px] text-slate-400">1 night, 2 adults</span>
                            <span class="font-black text-sm text-slate-900">$${prop.price}</span>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function filterProperties() {
            const query = document.getElementById('search-query').value.toLowerCase().trim();
            const filtered = properties.filter(p => p.name.toLowerCase().includes(query) || p.location.toLowerCase().includes(query));
            renderProperties(filtered);
        }

        function openModal(id) {
            activeProperty = properties.find(p => p.id === id);
            document.getElementById('modal-name').innerText = activeProperty.name;
            document.getElementById('modal-loc-text').innerText = activeProperty.address;
            document.getElementById('modal-img').src = activeProperty.image;
            document.getElementById('modal-price').innerText = `$${activeProperty.price}`;
            
            let starsHtml = '';
            for(let i=0; i<activeProperty.stars; i++) starsHtml += '<i class="fa-solid fa-star"></i>';
            document.getElementById('modal-stars').innerHTML = starsHtml;

            document.getElementById('detail-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('detail-modal').classList.add('hidden');
        }

        function confirmBooking() {
            document.getElementById('v-hotel-name').innerText = activeProperty.name;
            document.getElementById('v-hotel-loc').innerText = activeProperty.address;
            document.getElementById('v-checkin').innerText = document.getElementById('checkin-date').value;
            document.getElementById('v-checkout').innerText = document.getElementById('checkout-date').value;
            document.getElementById('v-price').innerText = `$${activeProperty.price}`;

            const element = document.getElementById('pdf-voucher');
            alert('Reservation confirmed successfully! Downloading PDF voucher...');
            html2pdf().from(element).save(`Booking_${activeProperty.name.substring(0, 10)}.pdf`);
            closeModal();
        }
    </script>
</body>
</html>

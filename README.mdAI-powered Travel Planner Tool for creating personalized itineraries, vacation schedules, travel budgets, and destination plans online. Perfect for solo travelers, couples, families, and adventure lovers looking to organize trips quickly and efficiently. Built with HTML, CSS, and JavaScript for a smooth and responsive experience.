<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Ultimate Travel Planner | Forms + Hotel + Weather + Map + Checklist</title>
    <!-- Leaflet CSS + JS -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, 'Segoe UI', 'Helvetica Neue', sans-serif;
        }
        body {
            background: #eef2f8;
            padding: 2rem 1rem;
        }
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        h1 {
            font-size: 1.9rem;
            color: #1e3a5f;
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 8px;
        }
        .sub {
            color: #2c5282;
            margin-bottom: 2rem;
            border-left: 4px solid #2b6cb0;
            padding-left: 1rem;
        }
        /* cards */
        .card {
            background: white;
            border-radius: 28px;
            padding: 1.5rem;
            box-shadow: 0 12px 25px rgba(0,0,0,0.08);
            margin-bottom: 1.8rem;
            border: 1px solid #e2edf7;
        }
        .card h2 {
            font-size: 1.5rem;
            margin-bottom: 1rem;
            color: #0f2b3f;
            display: flex;
            align-items: center;
            gap: 10px;
            border-left: 5px solid #3182ce;
            padding-left: 15px;
        }
        .input-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 1.2rem;
            margin-bottom: 1.5rem;
            align-items: flex-end;
        }
        .field {
            flex: 1;
            min-width: 160px;
        }
        .field label {
            font-weight: 600;
            display: block;
            margin-bottom: 6px;
            font-size: 0.85rem;
        }
        input, select, textarea {
            width: 100%;
            padding: 10px 14px;
            border-radius: 20px;
            border: 1.5px solid #cbd5e0;
            background: white;
        }
        button {
            background: #2c5282;
            border: none;
            padding: 10px 22px;
            border-radius: 40px;
            color: white;
            font-weight: bold;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            transition: 0.2s;
        }
        button:hover { background: #1a3a5c; transform: scale(0.97);}
        .btn-secondary {
            background: #4a5568;
        }
        .btn-secondary:hover { background: #2d3748; }
        .hotel-item, .checklist-item {
            background: #f7fafc;
            border-radius: 20px;
            padding: 0.8rem;
            margin-bottom: 0.7rem;
            border-left: 4px solid #3182ce;
        }
        .flex-between {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
        }
        .map-container {
            height: 280px;
            border-radius: 24px;
            margin: 1rem 0;
            border: 2px solid #cbd5e0;
        }
        .weather-box {
            background: #e6f0ff;
            border-radius: 20px;
            padding: 1rem;
            margin-top: 0.5rem;
        }
        hr { margin: 1rem 0; }
        .badge {
            background: #e2e8f0;
            padding: 4px 12px;
            border-radius: 50px;
            font-size: 0.7rem;
        }
        i { margin-right: 4px; }
        .delete-btn {
            background: #e53e3e;
            padding: 4px 12px;
            font-size: 0.75rem;
        }
        .delete-btn:hover { background: #c53030; }
        @media (max-width: 760px) {
            .input-grid { flex-direction: column; }
        }
    </style>
</head>
<body>
<div class="container">
    <h1><i class="fas fa-earth-asia"></i> TripForge Pro</h1>
    <div class="sub">📋 Forms for Hotel, Weather, Packing & Map • plus auto-planning</div>

    <!-- MAIN TRIP PLANNER FORM (destination, days, budget, travelers) -->
    <div class="card">
        <h2><i class="fas fa-pen-ruler"></i> Plan Your Trip</h2>
        <div class="input-grid">
            <div class="field"><label>📍 Destination</label><input type="text" id="destMain" value="Rome, Italy"></div>
            <div class="field"><label>📅 Days</label><input type="number" id="daysMain" value="3" min="1"></div>
            <div class="field"><label>💸 Budget</label><select id="budgetMain"><option value="low">Low</option><option value="medium" selected>Medium</option><option value="high">High</option></select></div>
            <div class="field"><label>👥 Travelers</label><select id="travelersMain"><option value="solo">Solo</option><option value="couple">Couple</option><option value="family">Family</option></select></div>
            <div class="field"><button id="generatePlanBtn"><i class="fas fa-magic"></i> Generate Itinerary</button></div>
        </div>
        <div id="itineraryResult" style="background:#f9f9ff; border-radius: 20px; padding: 1rem; margin-top: 1rem;"><em>Click generate to see itinerary & budget</em></div>
        <div id="budgetResult" class="weather-box" style="margin-top: 10px;"></div>
    </div>

    <!-- FORM: HOTEL SUGGESTIONS (add custom hotels with affiliate links) -->
    <div class="card">
        <h2><i class="fas fa-hotel"></i> Hotel Suggestions Manager (Affiliate ready)</h2>
        <div class="input-grid">
            <div class="field"><label>Hotel Name</label><input type="text" id="hotelName" placeholder="Grand Plaza"></div>
            <div class="field"><label>Price / Night</label><input type="text" id="hotelPrice" placeholder="$120"></div>
            <div class="field"><label>Affiliate Link (URL)</label><input type="url" id="hotelLink" placeholder="https://booking.com/..."></div>
            <div class="field"><label>Description</label><input type="text" id="hotelDesc" placeholder="Central, pool, breakfast"></div>
            <div><button id="addHotelBtn"><i class="fas fa-plus-circle"></i> Add Hotel</button></div>
        </div>
        <div id="hotelListContainer">
            <div class="badge">✨ Default suggestions (you can add more below)</div>
            <div id="dynamicHotels"></div>
        </div>
    </div>

    <!-- FORM: WEATHER INFORMATION (manual or auto) -->
    <div class="card">
        <h2><i class="fas fa-cloud-sun-rain"></i> Weather Information Form</h2>
        <div class="input-grid">
            <div class="field"><label>🌡️ Manual Weather Text</label><input type="text" id="weatherManual" placeholder="e.g., Sunny 24°C, light breeze"></div>
            <div class="field"><label>Or fetch auto for destination</label><button id="autoWeatherBtn" class="btn-secondary"><i class="fas fa-sync-alt"></i> Auto Weather (from Destination)</button></div>
        </div>
        <div id="weatherDisplay" class="weather-box"><i class="fas fa-info-circle"></i> Weather will appear here (auto or manual)</div>
    </div>

    <!-- FORM: PACKING CHECKLIST (add custom items) -->
    <div class="card">
        <h2><i class="fas fa-check-double"></i> Packing Checklist Builder</h2>
        <div class="input-grid">
            <div class="field"><label>➕ New Item</label><input type="text" id="newPackingItem" placeholder="Power bank, Raincoat..."></div>
            <div><button id="addPackingBtn"><i class="fas fa-plus"></i> Add to Checklist</button></div>
        </div>
        <div id="packingListArea">
            <div class="badge">Default essentials + your custom items</div>
            <div id="packingItems"></div>
        </div>
    </div>

    <!-- FORM: MAP INTEGRATION (manual lat/lon or address) -->
    <div class="card">
        <h2><i class="fas fa-map-location-dot"></i> Map Integration Form</h2>
        <div class="input-grid">
            <div class="field"><label>Latitude</label><input type="text" id="mapLat" placeholder="41.9028"></div>
            <div class="field"><label>Longitude</label><input type="text" id="mapLon" placeholder="12.4964"></div>
            <div class="field"><label>Or Address</label><input type="text" id="mapAddress" placeholder="Eiffel Tower, Paris"></div>
            <div><button id="updateMapBtn"><i class="fas fa-map-pin"></i> Update Map</button></div>
        </div>
        <div id="mapDiv" class="map-container"></div>
        <div class="badge">Click on map to get coordinates & fill form automatically</div>
    </div>

    <!-- Travel tips section -->
    <div class="card">
        <h2><i class="fas fa-lightbulb"></i> Smart Travel Tips</h2>
        <div id="tipsContainer"></div>
    </div>
    <footer style="text-align: center; margin-top: 1rem;">✅ All forms work independently – add hotels, packing items, custom weather, map jump.</footer>
</div>

<script>
    // ---------- GLOBAL STORAGE ----------
    let customHotels = [];    // stores {name, price, link, desc}
    let customPacking = [];   // stores strings

    // Map instance
    let map = null;
    let marker = null;
    
    // Helper: refresh hotel list UI
    function renderHotels() {
        const container = document.getElementById('dynamicHotels');
        let html = '';
        // default static suggestions
        const defaultHotels = [
            { name: "Sunset Central Inn", price: "$85/night", link: "https://www.booking.com/searchresults.html?ss=rome&aid=123456", desc: "Cozy rooms, free wifi" },
            { name: "Luxury Art Hotel", price: "$210/night", link: "https://www.booking.com/searchresults.html?ss=rome&aid=123456", desc: "Museum district, spa" }
        ];
        const allDisplay = [...defaultHotels, ...customHotels];
        allDisplay.forEach((hotel, idx) => {
            const isCustom = idx >= defaultHotels.length;
            html += `
                <div class="hotel-item">
                    <div class="flex-between">
                        <strong>🏨 ${hotel.name}</strong>
                        <span class="badge">${hotel.price}</span>
                    </div>
                    <div style="font-size:0.85rem; margin: 6px 0;">${hotel.desc}</div>
                    <div class="flex-between">
                        <a href="${hotel.link}" target="_blank" rel="sponsored noopener"><i class="fas fa-link"></i> Book with affiliate link</a>
                        ${isCustom ? `<button class="delete-btn" data-hotel-idx="${idx - defaultHotels.length}"><i class="fas fa-trash"></i> Remove</button>` : ''}
                    </div>
                </div>
            `;
        });
        container.innerHTML = html || '<em>No hotels added yet. Use form above.</em>';
        // attach delete events
        document.querySelectorAll('.delete-btn').forEach(btn => {
            btn.addEventListener('click', (e) => {
                const idx = btn.getAttribute('data-hotel-idx');
                if(idx !== null) customHotels.splice(parseInt(idx), 1);
                renderHotels();
            });
        });
    }

    function renderPacking() {
        const defaultItems = ["🧳 Passport & tickets", "🔋 Power bank", "👟 Walking shoes", "🧴 Sunscreen", "💊 First aid kit"];
        const allItems = [...defaultItems, ...customPacking];
        const container = document.getElementById('packingItems');
        container.innerHTML = `
            <div class="packing-grid" style="display: flex; flex-wrap: wrap; gap: 12px;">
                ${allItems.map((item, idx) => {
                    const isCustom = idx >= defaultItems.length;
                    return `<label style="background:#eef2ff; border-radius: 40px; padding: 6px 14px; display: inline-flex; align-items: center; gap: 8px;">
                                <input type="checkbox" class="pack-check"> ${item}
                                ${isCustom ? `<button class="delete-pack" data-pack-idx="${idx - defaultItems.length}" style="background:none; border:none; color:#e53e3e; cursor:pointer;"><i class="fas fa-times-circle"></i></button>` : ''}
                            </label>`;
                }).join('')}
            </div>
            <div style="margin-top: 10px;"><button id="resetAllChecks" style="background:#718096; font-size:0.8rem;">Uncheck all</button></div>
        `;
        document.querySelectorAll('.delete-pack').forEach(btn => {
            btn.addEventListener('click', (e) => {
                const idx = btn.getAttribute('data-pack-idx');
                if(idx !== null) customPacking.splice(parseInt(idx), 1);
                renderPacking();
            });
        });
        const resetBtn = document.getElementById('resetAllChecks');
        if(resetBtn) resetBtn.onclick = () => document.querySelectorAll('.pack-check').forEach(cb => cb.checked = false);
    }

    // Add hotel
    document.getElementById('addHotelBtn').addEventListener('click', () => {
        const name = document.getElementById('hotelName').value.trim();
        const price = document.getElementById('hotelPrice').value.trim();
        const link = document.getElementById('hotelLink').value.trim();
        const desc = document.getElementById('hotelDesc').value.trim();
        if(!name || !price) { alert("Hotel name & price required"); return; }
        customHotels.push({ name, price, link: link || "#", desc: desc || "Great value stay" });
        renderHotels();
        document.getElementById('hotelName').value = '';
        document.getElementById('hotelPrice').value = '';
        document.getElementById('hotelLink').value = '';
        document.getElementById('hotelDesc').value = '';
    });

    // Add packing item
    document.getElementById('addPackingBtn').addEventListener('click', () => {
        const newItem = document.getElementById('newPackingItem').value.trim();
        if(!newItem) return;
        customPacking.push(newItem);
        renderPacking();
        document.getElementById('newPackingItem').value = '';
    });

    // Weather Manual / Auto
    document.getElementById('autoWeatherBtn').addEventListener('click', async () => {
        const dest = document.getElementById('destMain').value.trim();
        if(!dest) { alert("Enter destination first"); return; }
        try {
            const geoUrl = `https://nominatim.openstreetmap.org/search?format=json&q=${encodeURIComponent(dest)}&limit=1`;
            const geoRes = await fetch(geoUrl, { headers: { 'User-Agent': 'TripPlanner' } });
            const geoData = await geoRes.json();
            if(!geoData.length) throw new Error("Location not found");
            const { lat, lon } = geoData[0];
            const weatherUrl = `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true&timezone=auto`;
            const wRes = await fetch(weatherUrl);
            const wData = await wRes.json();
            const temp = wData.current_weather.temperature;
            const wind = wData.current_weather.windspeed;
            const weatherText = `🌡️ Auto: ${temp}°C, Wind ${wind} km/h, ${new Date().toLocaleTimeString()}`;
            document.getElementById('weatherDisplay').innerHTML = `<i class="fas fa-cloud-sun"></i> ${weatherText}`;
        } catch(e) { document.getElementById('weatherDisplay').innerHTML = `⚠️ Auto weather failed: ${e.message}`; }
    });
    // manual weather set
    document.getElementById('weatherManual').addEventListener('change', function() {
        if(this.value) document.getElementById('weatherDisplay').innerHTML = `<i class="fas fa-pen"></i> Manual: ${this.value}`;
    });

    // ---------- MAP INTEGRATION (form & click) ----------
    function initMap(lat=41.9028, lng=12.4964) {
        if(map) map.remove();
        map = L.map('mapDiv').setView([lat, lng], 12);
        L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', {
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OSM</a>'
        }).addTo(map);
        if(marker) map.removeLayer(marker);
        marker = L.marker([lat, lng]).addTo(map).bindPopup("📍 Selected location").openPopup();
        map.on('click', function(e) {
            const { lat, lng } = e.latlng;
            document.getElementById('mapLat').value = lat.toFixed(6);
            document.getElementById('mapLon').value = lng.toFixed(6);
            if(marker) map.removeLayer(marker);
            marker = L.marker([lat, lng]).addTo(map).bindPopup(`Lat: ${lat.toFixed(4)}, Lng: ${lng.toFixed(4)}`).openPopup();
        });
    }
    document.getElementById('updateMapBtn').addEventListener('click', async () => {
        let lat = parseFloat(document.getElementById('mapLat').value);
        let lon = parseFloat(document.getElementById('mapLon').value);
        const address = document.getElementById('mapAddress').value.trim();
        if(address && (isNaN(lat) || isNaN(lon))) {
            try {
                const geo = await fetch(`https://nominatim.openstreetmap.org/search?format=json&q=${encodeURIComponent(address)}&limit=1`, { headers: { 'User-Agent': 'TripMap' } });
                const data = await geo.json();
                if(data.length) { lat = parseFloat(data[0].lat); lon = parseFloat(data[0].lon); }
                else alert("Address not found");
            } catch(e) { alert("Geocoding error"); return; }
        }
        if(!isNaN(lat) && !isNaN(lon)) {
            if(!map) initMap(lat, lon);
            else {
                map.setView([lat, lon], 13);
                if(marker) map.removeLayer(marker);
                marker = L.marker([lat, lon]).addTo(map).bindPopup("📍 Custom location").openPopup();
            }
            document.getElementById('mapLat').value = lat;
            document.getElementById('mapLon').value = lon;
        } else alert("Enter valid lat/lon or address");
    });

    // ----- Trip Generation Logic (itinerary, budget, tips) -----
    function getPeopleCount(t) { return {solo:1, couple:2, family:4}[t] || 2; }
    function calculateBudget(budget, days, travelers) {
        const people = getPeopleCount(travelers);
        let dailyPP = budget==='low'?55:(budget==='medium'?120:280);
        let total = dailyPP * days * people;
        if(travelers==='couple') total = total * 0.85;
        if(travelers==='family') total = total * 0.78;
        return { total: Math.round(total), dailyPP };
    }
    function buildItinerary(dest, days, travelers) {
        let arr = [];
        for(let i=1;i<=days;i++) {
            if(i===1) arr.push(`Day 1: Arrival in ${dest}, check-in, welcome dinner & evening walk.`);
            else if(i===days) arr.push(`Day ${days}: Last souvenirs, brunch, transfer to airport.`);
            else arr.push(`Day ${i}: Explore ${dest} - ${travelers==='couple'?'romantic tour + wine tasting':(travelers==='family'?'kid-friendly museum & park':'city highlights & culture')}`);
        }
        return arr;
    }
    function updateTips(travelers, budget) {
        let tips = [`🧾 Carry local currency & digital copy of documents`, `🚇 Use public transport passes`, `🍜 Try local street food`];
        if(travelers === 'family') tips.push(`👨‍👩‍👧‍👦 Book family-friendly tours in advance.`);
        if(budget === 'low') tips.push(`💸 Use hostelworld or budget hotel forms above.`);
        if(budget === 'high') tips.push(`✨ Luxury tip: book private guided tours.`);
        document.getElementById('tipsContainer').innerHTML = tips.map(t => `<div class="weather-box" style="margin-bottom:8px;">✔️ ${t}</div>`).join('');
    }

    document.getElementById('generatePlanBtn').addEventListener('click', () => {
        const dest = document.getElementById('destMain').value.trim() || "Unknown";
        const days = parseInt(document.getElementById('daysMain').value) || 3;
        const budget = document.getElementById('budgetMain').value;
        const travelers = document.getElementById('travelersMain').value;
        const itinerary = buildItinerary(dest, days, travelers);
        const budgetCalc = calculateBudget(budget, days, travelers);
        const people = getPeopleCount(travelers);
        document.getElementById('itineraryResult').innerHTML = `<strong>🗺️ Suggested Itinerary for ${dest}</strong><ul>${itinerary.map(i=>`<li>${i}</li>`).join('')}</ul>`;
        document.getElementById('budgetResult').innerHTML = `<strong>💰 Estimated budget: $${budgetCalc.total}</strong> for ${people} traveler(s), ${days} days ($${budgetCalc.dailyPP}/person/day) - ${budget.toUpperCase()} style.`;
        updateTips(travelers, budget);
        // also update auto weather if needed
    });

    // Initial render
    renderHotels();
    renderPacking();
    initMap(41.9028, 12.4964); // rome default
    // set initial default tips
    updateTips('family', 'medium');
    document.getElementById('weatherDisplay').innerHTML = '🌦️ Use "Auto Weather" or type manual forecast.';
    // link click map sample coordinates fill from address event
</script>
</body>
</html>

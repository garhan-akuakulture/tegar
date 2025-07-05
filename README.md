<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Analisis Usaha Budidaya Ikan</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { 
            font-family: 'Inter', sans-serif; 
            background-color: #020617; 
            color: #f8fafc; 
            overflow-x: hidden;
        }
        #interactive-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0; 
        }
        .main-content {
            position: relative;
            z-index: 1; 
        }
        .card { 
            background-color: rgba(15, 23, 42, 0.8); 
            backdrop-filter: blur(16px); 
            -webkit-backdrop-filter: blur(16px);
            border-radius: 1rem; 
            padding: 2.5rem; 
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        .main-button {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }
        label { color: #cbd5e1; }
        .card h2, .card h3 { color: #f1f5f9; }
        input, select {
            background-color: rgba(15, 23, 42, 0.5) !important; 
            border-color: #334155 !important; 
            color: white !important;
        }
        input:focus, select:focus {
            border-color: #6366f1 !important; 
            --tw-ring-color: #6366f1 !important; 
        }
        .result-item { 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            padding: 1rem 0.5rem; 
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        .result-item:last-child { border-bottom: none; }
        .result-item span:first-child { color: #94a3b8; }
        .result-item span:last-child { font-weight: 700; }
        .profit { color: #4ade80; } /* green-400 */
        .loss { color: #f87171; } /* red-400 */
    </style>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
</head>
<body class="p-4 md:p-8">
<canvas id="interactive-bg"></canvas>
<div class="main-content max-w-3xl mx-auto">
    <div class="text-center mb-12">
        <h1 class="text-4xl md:text-5xl font-extrabold text-white bg-clip-text text-transparent bg-gradient-to-r from-teal-400 to-blue-500">Analisis Finansial Akuakultur</h1>
        <p class="text-lg text-slate-400 mt-2">Hitung profitabilitas usaha budidaya Anda</p>
    </div>
    
    <div class="space-y-8">
        <!-- Kolom Input -->
        <div class="card">
            <h2 class="text-2xl font-bold mb-6 border-b border-slate-700 pb-4 flex items-center gap-3">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-teal-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z" /></svg>
                Input Data Usaha
            </h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <!-- Modal Usaha -->
                <div class="space-y-4">
                    <h3 class="text-lg font-semibold text-slate-300 border-b border-slate-600 pb-2">Modal Usaha</h3>
                    <div>
                        <label for="harga_bibit" class="block text-sm font-medium mb-1">Harga Bibit (Rp / ekor)</label>
                        <input type="number" id="harga_bibit" placeholder="Contoh: 500" class="mt-1 block w-full p-3 rounded-md shadow-sm">
                    </div>
                    <div>
                        <label for="harga_pakan" class="block text-sm font-medium mb-1">Harga Pakan (Rp / kg)</label>
                        <input type="number" id="harga_pakan" placeholder="Contoh: 12000" class="mt-1 block w-full p-3 rounded-md shadow-sm">
                    </div>
                    <div>
                        <label for="biaya_operasional" class="block text-sm font-medium mb-1">Biaya Operasional Lain (Rp)</label>
                        <input type="number" id="biaya_operasional" placeholder="Listrik, air, obat, dll." class="mt-1 block w-full p-3 rounded-md shadow-sm">
                    </div>
                </div>
                <!-- Data Panen -->
                <div class="space-y-4">
                    <h3 class="text-lg font-semibold text-slate-300 border-b border-slate-600 pb-2">Data Panen</h3>
                    <div>
                        <label for="jumlah_bibit" class="block text-sm font-medium mb-1">Jumlah Bibit Ditebar (ekor)</label>
                        <input type="number" id="jumlah_bibit" placeholder="Contoh: 1000" class="mt-1 block w-full p-3 rounded-md shadow-sm">
                    </div>
                    <div>
                        <label for="total_pakan" class="block text-sm font-medium mb-1">Total Pakan Dihabiskan (kg)</label>
                        <input type="number" id="total_pakan" placeholder="Contoh: 120" class="mt-1 block w-full p-3 rounded-md shadow-sm">
                    </div>
                    <div>
                        <label for="total_bobot_panen" class="block text-sm font-medium mb-1">Total Bobot Panen (kg)</label>
                        <input type="number" id="total_bobot_panen" placeholder="Contoh: 110" class="mt-1 block w-full p-3 rounded-md shadow-sm">
                    </div>
                     <div>
                        <label for="harga_jual" class="block text-sm font-medium mb-1">Harga Jual Ikan (Rp / kg)</label>
                        <input type="number" id="harga_jual" placeholder="Contoh: 25000" class="mt-1 block w-full p-3 rounded-md shadow-sm">
                    </div>
                </div>
            </div>
            <button id="calculate-btn" class="main-button mt-8 w-full bg-indigo-600 text-white font-bold py-3 px-4 rounded-lg hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-all duration-200 transform hover:scale-105">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 7h6m0 10v-3m-3 3h.01M9 17h.01M9 14h.01M12 14h.01M15 11h.01M12 11h.01M9 11h.01M7 21h10a2 2 0 002-2V5a2 2 0 00-2-2H7a2 2 0 00-2 2v14a2 2 0 002 2z" /></svg>
                <span>Analisis Usaha</span>
            </button>
        </div>

        <!-- Kolom Hasil -->
        <div id="result-container" class="space-y-8" style="display: none;">
            <div class="card">
                <h2 class="text-2xl font-bold mb-4 border-b border-slate-700 pb-4 flex items-center gap-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-teal-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M9 17v-2m3 2v-4m3 4v-6m2 10H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" /></svg>
                    Laporan Keuangan
                </h2>
                <div class="mt-4 space-y-2">
                    <div class="result-item"><span>Total Modal</span><span id="hasil-modal" class="font-bold text-lg"></span></div>
                    <div class="result-item"><span>Total Pendapatan</span><span id="hasil-pendapatan" class="font-bold text-lg"></span></div>
                    <div class="result-item"><span>Keuntungan / Kerugian</span><span id="hasil-keuntungan" class="font-bold text-xl"></span></div>
                </div>
            </div>

            <div class="card">
                 <h2 class="text-2xl font-bold mb-4 border-b border-slate-700 pb-4 flex items-center gap-3">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-teal-400" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M13 10V3L4 14h7v7l9-11h-7z" /></svg>
                    Analisis Kelayakan Usaha
                </h2>
                 <div class="mt-4 space-y-2">
                    <div class="result-item"><span>BEP (Produksi)</span><span id="hasil-bep-produksi" class="font-bold text-lg"></span></div>
                    <div class="result-item"><span>BEP (Harga)</span><span id="hasil-bep-harga" class="font-bold text-lg"></span></div>
                    <div class="result-item"><span>R/C Ratio</span><span id="hasil-rc-ratio" class="font-bold text-lg"></span></div>
                </div>
                <div id="status-kelayakan" class="mt-6 text-center"></div>
            </div>
        </div>
    </div>
    <div id="error-message" class="mt-6 text-center text-red-400 font-semibold p-4 bg-red-500/10 rounded-lg" style="display: none;"></div>
    <footer class="text-center mt-12 text-sm text-slate-500">
        <p>&copy; 2025 Smart Aquaqulture System by Tegar.</p>
        <p class="mt-1">Kontak: <a href="mailto:tegarraihan211204@gmail.com" class="text-indigo-400 hover:underline">tegarraihan211204@gmail.com</a></p>
    </footer>
</div>

<script>
// --- SCRIPT UNTUK BACKGROUND PERIKANAN INTERAKTIF ---
const canvas = document.getElementById('interactive-bg');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let fishArray = [];
let ripplesArray = [];

const mouse = { x: null, y: null };

canvas.addEventListener('mousemove', function(event) {
    mouse.x = event.x;
    mouse.y = event.y;
    if (Math.random() > 0.9) {
        ripplesArray.push(new Ripple(mouse.x, mouse.y));
    }
});
canvas.addEventListener('click', function(event) {
    mouse.x = event.x;
    mouse.y = event.y;
    for (let i = 0; i < 5; i++) {
         ripplesArray.push(new Ripple(mouse.x, mouse.y));
    }
});


class Ripple {
    constructor(x, y) {
        this.x = x;
        this.y = y;
        this.radius = Math.random() * 5 + 1;
        this.maxRadius = Math.random() * 20 + 30;
        this.opacity = 1;
        this.speed = Math.random() * 0.5 + 0.2;
    }
    update() {
        this.radius += this.speed;
        if (this.radius > this.maxRadius) {
            this.opacity -= 0.05;
        }
    }
    draw() {
        ctx.strokeStyle = `rgba(107, 114, 128, ${this.opacity})`;
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
        ctx.stroke();
    }
}

function animate() {
    ctx.clearRect(0,0,innerWidth, innerHeight);
    ripplesArray.forEach((ripple, index) => {
        ripple.update();
        ripple.draw();
        if (ripple.opacity <= 0) {
            ripplesArray.splice(index, 1);
        }
    });
    requestAnimationFrame(animate);
}
animate();

window.addEventListener('resize', function() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
});


// --- SCRIPT UNTUK LOGIKA KALKULATOR ---
document.addEventListener('DOMContentLoaded', () => {

    const elements = {
        calculateBtn: document.getElementById('calculate-btn'),
        resultContainer: document.getElementById('result-container'),
        errorMessage: document.getElementById('error-message'),
        inputs: {
            hargaBibit: document.getElementById('harga_bibit'),
            hargaPakan: document.getElementById('harga_pakan'),
            biayaOperasional: document.getElementById('biaya_operasional'),
            jumlahBibit: document.getElementById('jumlah_bibit'),
            totalPakan: document.getElementById('total_pakan'),
            totalBobotPanen: document.getElementById('total_bobot_panen'),
            hargaJual: document.getElementById('harga_jual'),
        },
        outputs: {
            modal: document.getElementById('hasil-modal'),
            pendapatan: document.getElementById('hasil-pendapatan'),
            keuntungan: document.getElementById('hasil-keuntungan'),
            bepProduksi: document.getElementById('hasil-bep-produksi'),
            bepHarga: document.getElementById('hasil-bep-harga'),
            rcRatio: document.getElementById('hasil-rc-ratio'),
            statusKelayakan: document.getElementById('status-kelayakan'),
        }
    };
    
    function formatRupiah(angka) {
        return new Intl.NumberFormat('id-ID', {
            style: 'currency',
            currency: 'IDR',
            minimumFractionDigits: 0
        }).format(angka);
    }

    const handleCalculation = () => {
        elements.errorMessage.style.display = 'none';
        
        const inputs = {
            hargaBibit: parseFloat(elements.inputs.hargaBibit.value),
            hargaPakan: parseFloat(elements.inputs.hargaPakan.value),
            biayaOperasional: parseFloat(elements.inputs.biayaOperasional.value) || 0,
            jumlahBibit: parseInt(elements.inputs.jumlahBibit.value),
            totalPakan: parseFloat(elements.inputs.totalPakan.value),
            totalBobotPanen: parseFloat(elements.inputs.totalBobotPanen.value),
            hargaJual: parseFloat(elements.inputs.hargaJual.value),
        };
        
        if (Object.values(inputs).some(val => isNaN(val))) {
            elements.errorMessage.textContent = 'Error: Semua kolom input harus diisi dengan angka yang valid.';
            elements.errorMessage.style.display = 'block';
            return;
        }

        // --- Perhitungan Finansial ---
        const modalBibit = inputs.hargaBibit * inputs.jumlahBibit;
        const modalPakan = inputs.hargaPakan * inputs.totalPakan;
        const totalModal = modalBibit + modalPakan + inputs.biayaOperasional;
        
        const totalPendapatan = inputs.totalBobotPanen * inputs.hargaJual;
        
        const keuntungan = totalPendapatan - totalModal;
        
        const bepProduksi = totalModal / inputs.hargaJual;
        const bepHarga = totalModal / inputs.totalBobotPanen;
        const rcRatio = totalPendapatan / totalModal;

        // --- Tampilkan Hasil ---
        elements.outputs.modal.textContent = formatRupiah(totalModal);
        elements.outputs.pendapatan.textContent = formatRupiah(totalPendapatan);
        elements.outputs.keuntungan.textContent = formatRupiah(keuntungan);
        
        if (keuntungan > 0) {
            elements.outputs.keuntungan.className = 'font-bold text-xl profit';
        } else {
            elements.outputs.keuntungan.className = 'font-bold text-xl loss';
        }

        elements.outputs.bepProduksi.textContent = `${bepProduksi.toFixed(2)} kg`;
        elements.outputs.bepHarga.textContent = `${formatRupiah(bepHarga)} / kg`;
        elements.outputs.rcRatio.textContent = rcRatio.toFixed(2);
        
        if (rcRatio > 1) {
            elements.outputs.statusKelayakan.innerHTML = `<span class="inline-block px-4 py-2 text-sm font-semibold text-green-900 bg-green-200 rounded-full">Usaha Layak Dijalankan</span>`;
        } else {
            elements.outputs.statusKelayakan.innerHTML = `<span class="inline-block px-4 py-2 text-sm font-semibold text-red-900 bg-red-200 rounded-full">Usaha Tidak Layak Dijalankan</span>`;
        }

        elements.resultContainer.style.display = 'block';
    };

    elements.calculateBtn.addEventListener('click', handleCalculation);
});
</script>

</body>
</html>

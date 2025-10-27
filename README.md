<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interaktif: Teknik Pemijahan Koi</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Earth (Amber/Neutral) -->
    <!-- Application Structure Plan: Desain SPA ini menggunakan navigasi berbasis tab ('Ringkasan', 'Metode', 'Data') untuk memisahkan gambaran umum, proses interaktif, dan data pendukung. Struktur ini dipilih untuk memandu pengguna dari konsep umum ke detail spesifik, memprioritaskan alur belajar. Interaksi utamanya ada di tab 'Metode', di mana pengguna dapat memilih metode (Alami, Semi-Buatan, Buatan) dan secara dinamis melihat perubahan panduan langkah-demi-langkah dan data kuncinya. Ini lebih unggul dari laporan statis karena memungkinkan perbandingan langsung dan fokus pada proses. -->
    <!-- Visualization & Content Choices: Data Jurnal -> Goal: Membandingkan performa -> Viz: Chart.js Bar Chart ('Tingkat Keberhasilan') -> Interaction: Tooltip saat hover -> Justification: Perbandingan visual FR & HR antar metode lebih cepat dipahami daripada teks. (Chart.js/Canvas). Proses Pemijahan -> Goal: Menjelaskan 3 alur proses -> Viz: Diagram Proses Interaktif (HTML/Tailwind) -> Interaction: Tombol (Alami, Semi-Buatan, Buatan) untuk mengubah konten -> Justification: Memecah kerumitan menjadi langkah-langkah yang dapat dikelola dan dibandingkan secara langsung. (HTML/CSS/JS). Daftar Jurnal -> Goal: Memberi referensi -> Viz: Daftar HTML -> Interaction: Tidak ada -> Justification: Kredibilitas dan sumber. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FFFAF0; 
        }
        .tab-btn {
            transition: all 0.3s ease;
        }
        .tab-btn.active {
            background-color: #B45309; 
            color: white;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        .tab-btn:not(.active) {
            background-color: #FDE68A; 
            color: #92400E; 
        }
        .tab-btn:not(.active):hover {
            background-color: #FCD34D;
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .method-btn {
            transition: all 0.3s ease;
        }
        .method-btn.active {
            background-color: #15803D; 
            color: white;
            transform: scale(1.05);
        }
        .method-btn:not(.active) {
            background-color: #D1FAE5; 
            color: #065F46;
        }
        .method-btn:not(.active):hover {
            background-color: #A7F3D0;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 350px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 400px;
            }
        }
    </style>
</head>
<body class="bg-amber-50 text-gray-800">

    <div class="max-w-7xl mx-auto p-4 sm:p-8">
        
        <header class="text-center mb-8">
            <h1 class="text-4xl font-bold text-amber-900 mb-2">Aplikasi Interaktif: Teknik Pemijahan Ikan Koi</h1>
            <p class="text-lg text-amber-800">Menjelajahi Data dan Metode Pembenihan Ikan Koi (Cyprinus carpio) dari Jurnal Penelitian</p>
        </header>

        <nav class="flex justify-center space-x-2 sm:space-x-4 mb-8">
            <button id="tab-btn-ringkasan" class="tab-btn active py-2 px-4 sm:px-6 rounded-lg font-semibold shadow-md" onclick="showTab('ringkasan')">Ringkasan</button>
            <button id="tab-btn-metode" class="tab-btn py-2 px-4 sm:px-6 rounded-lg font-semibold shadow-md" onclick="showTab('metode')">Metode Pemijahan</button>
            <button id="tab-btn-data" class="tab-btn py-2 px-4 sm:px-6 rounded-lg font-semibold shadow-md" onclick="showTab('data')">Data & Jurnal</button>
        </nav>

        <main>
            <section id="content-ringkasan" class="content-section active bg-white p-6 sm:p-8 rounded-xl shadow-lg">
                <h2 class="text-3xl font-semibold text-amber-900 mb-4">Gambaran Umum Pemijahan Koi</h2>
                <p class="text-gray-700 mb-6 leading-relaxed">
                    Selamat datang! Aplikasi ini mengubah data jurnal teknis mengenai pemijahan ikan koi menjadi panduan yang mudah dipahami. Pemijahan adalah proses krusial dalam budidaya untuk menghasilkan benih berkualitas. Keberhasilannya diukur oleh beberapa metrik kunci. Mulai di sini untuk melihat gambaran umum dan metrik keberhasilan utama.
                </p>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 text-center">
                    <div class="bg-blue-50 p-6 rounded-lg shadow-md">
                        <h3 class="text-xl font-semibold text-blue-800 mb-2">Fekunditas</h3>
                        <p class="text-blue-700">Jumlah telur yang dihasilkan oleh induk betina. Sangat bervariasi tergantung ukuran dan strain induk.</p>
                    </div>
                    <div class="bg-green-50 p-6 rounded-lg shadow-md">
                        <h3 class="text-xl font-semibold text-green-800 mb-2">Fertilization Rate (FR)</h3>
                        <p class="text-green-700">Persentase telur yang berhasil dibuahi. Data jurnal menunjukkan angka <strong>80% - 91%</strong>.</p>
                        <p class="text-sm text-gray-500 mt-2">(Telur fertil berwarna bening)</p>
                    </div>
                    <div class="bg-yellow-50 p-6 rounded-lg shadow-md">
                        <h3 class="text-xl font-semibold text-yellow-800 mb-2">Hatching Rate (HR)</h3>
                        <p class="text-yellow-700">Persentase telur yang berhasil menetas menjadi larva. Data jurnal mencatat angka <strong>75% - 87%</strong>.</p>
                        <p class="text-sm text-gray-500 mt-2">(Menetas dalam 2-3 hari)</p>
                    </div>
                </div>
            </section>

            <section id="content-metode" class="content-section bg-white p-6 sm:p-8 rounded-xl shadow-lg">
                <h2 class="text-3xl font-semibold text-amber-900 mb-4">Panduan Interaktif Metode Pemijahan</h2>
                <p class="text-gray-700 mb-6 leading-relaxed">
                    Jelajahi tiga metode utama pemijahan ikan koi. Klik tombol di bawah (Alami, Semi-Buatan, Buatan) untuk melihat panduan langkah-demi-langkah, data kunci, dan poin penting tiap metode secara dinamis.
                </p>
                
                <div class="flex flex-col sm:flex-row justify-center space-y-3 sm:space-y-0 sm:space-x-4 mb-8">
                    <button id="method-btn-alami" class="method-btn active py-3 px-6 rounded-lg font-semibold text-lg shadow-md" onclick="showMethod('alami')">🐟 Alami</button>
                    <button id="method-btn-semi" class="method-btn py-3 px-6 rounded-lg font-semibold text-lg shadow-md" onclick="showMethod('semi')">💉 Semi-Buatan</button>
                    <button id="method-btn-buatan" class="method-btn py-3 px-6 rounded-lg font-semibold text-lg shadow-md" onclick="showMethod('buatan')">🧪 Buatan (Stripping)</button>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div class="lg:col-span-2">
                        <h3 class="text-2xl font-semibold text-gray-800 mb-4" id="method-title">Metode: Alami</h3>
                        <ol class="relative border-l border-gray-300 space-y-6 pl-4">
                            <li class="ml-4">
                                <div class="absolute w-3 h-3 bg-gray-400 rounded-full -left-1.5 border border-white"></div>
                                <h4 class="text-lg font-semibold text-gray-900" id="step-1-title">Seleksi Induk</h4>
                                <p class="text-gray-600" id="step-1-desc">Pilih induk jantan (operkulum kasar, keluar sperma) dan betina (perut lunak, genital bengkak) yang matang gonad.</p>
                            </li>
                            <li class="ml-4">
                                <div class="absolute w-3 h-3 bg-gray-400 rounded-full -left-1.5 border border-white"></div>
                                <h4 class="text-lg font-semibold text-gray-900" id="step-2-title">Persiapan Kolam & Kakaban</h4>
                                <p class="text-gray-600" id="step-2-desc">Siapkan kolam/bak yang bersih dan pasang kakaban (media ijuk/waring) sebagai tempat telur menempel.</p>
                            </li>
                            <li class="ml-4">
                                <div class="absolute w-3 h-3 bg-gray-400 rounded-full -left-1.5 border border-white"></div>
                                <h4 class="text-lg font-semibold text-gray-900" id="step-3-title">Proses Pemijahan</h4>
                                <p class="text-gray-600" id="step-3-desc">Masukkan induk (rasio 1:1 atau 2:1) ke kolam pada sore hari. Pemijahan terjadi alami di malam/dini hari.</p>
                            </li>
                            <li class="ml-4">
                                <div class="absolute w-3 h-3 bg-gray-400 rounded-full -left-1.5 border border-white"></div>
                                <h4 class="text-lg font-semibold text-gray-900" id="step-4-title">Penetasan & Perawatan</h4>
                                <p class="text-gray-600" id="step-4-desc">Pindahkan induk setelah memijah (agar telur tidak dimakan). Pindahkan kakaban ke bak penetasan. Telur menetas dalam 2-3 hari. Beri pakan larva (Artemia/Daphnia) setelah kantung telur habis.</p>
                            </li>
                        </ol>
                    </div>
                    <div class="bg-gray-50 p-6 rounded-lg shadow-inner">
                        <h3 class="text-2xl font-semibold text-gray-800 mb-4">Data Kunci</h3>
                        <ul class="space-y-3">
                            <li class="flex items-start">
                                <span class="text-green-600 font-bold mr-2">✓</span>
                                <div>
                                    <h5 class="font-semibold">Induksi Hormon</h5>
                                    <p class="text-gray-600" id="data-hormon">Tidak ada. Proses bergantung 100% pada kesiapan alami induk.</p>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-green-600 font-bold mr-2">✓</span>
                                <div>
                                    <h5 class="font-semibold">Proses Ovulasi</h5>
                                    <p class="text-gray-600" id="data-ovulasi">Terjadi secara alami di kolam pemijahan.</p>
                                </div>
                            </li>
                            <li class="flex items-start">
                                <span class="text-green-600 font-bold mr-2">✓</span>
                                <div>
                                    <h5 class="font-semibold">Pembuahan</h5>
                                    <p class="text-gray-600" id="data-pembuahan">Eksternal, terjadi secara alami di kakaban saat jantan menyemprotkan sperma ke telur yang dikeluarkan betina.</p>
                                </div>
                            </li>
                             <li class="flex items-start">
                                <span class="text-green-600 font-bold mr-2">✓</span>
                                <div>
                                    <h5 class="font-semibold">Poin Penting</h5>
                                    <p class="text-gray-600" id="data-poin">Tingkat stres induk rendah, namun waktu pemijahan tidak seragam.</p>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </section>

            <section id="content-data" class="content-section bg-white p-6 sm:p-8 rounded-xl shadow-lg">
                <h2 class="text-3xl font-semibold text-amber-900 mb-4">Data Visual & Referensi</h2>
                <p class="text-gray-700 mb-6 leading-relaxed">
                    Bagian ini menyajikan perbandingan visual dari data keberhasilan yang dilaporkan dalam berbagai jurnal penelitian. Data ini merupakan agregat dan dapat bervariasi tergantung kondisi lapangan. Di bawah grafik, Anda akan menemukan daftar referensi lengkap yang digunakan untuk membangun aplikasi ini.
                </p>

                <div class="bg-gray-50 p-4 sm:p-6 rounded-lg shadow-inner mb-8">
                     <h3 class="text-2xl font-semibold text-gray-800 mb-4 text-center">Perbandingan Tingkat Keberhasilan (Data Jurnal)</h3>
                    <div class="chart-container">
                        <canvas id="metricsChart"></canvas>
                    </div>
                </div>

                <div>
                    <h3 class="text-2xl font-semibold text-gray-800 mb-4">Referensi Jurnal (10 Tahun Terakhir)</h3>
                    <ul class="list-disc list-inside space-y-2 text-gray-700">
                        <li>Ritonga, L. BR, dkk. (2024). "Teknik Pemijahan Ikan Koi (Cyprinus Carpio) Secara Buatan...". <i>JURNAL LEMURU</i>.</li>
                        <li>Nurhayati, D., Hastuti, S., & Dwiastuti, S. A. (2022). "Performa Reproduksi Ikan Koi (Cyprinus Carpio) dengan Strain Berbeda". <i>Sains Akuakultur Tropis</i>.</li>
                        <li>Ritonga, L. BR, dkk. (2022). "Pembenihan Ikan Koi (Cyprinus Carpio) Secara Alami...". <i>Chanos Chanos</i>.</li>
                        <li>Hendriana, A., dkk. (2021). "Metode Pembenihan Ikan koi Cyprinus carpio dalam menghasilkan benih berkualitas...". <i>Jurnal Perikanan Terapan</i>.</li>
                        <li>Ishaqi, A. M. A., & Sari, P. D. W. (2019). "Pemijahan Ikan Koi (Cyprinus Carpio) dengan Metode Semi Buatan...". <i>Jurnal Perikanan dan Kelautan</i>.</li>
                        <li>Jurnal dari Universitas Brawijaya (2024). "TEKNIK DAN ANALISA USAHA PEMBENIHAN IKAN KOI...". <i>Journal UBB</i>.</li>
                        <li>Jurnal dari BRIN (2024). "ANALISIS PRODUKSI DAN DISTRIBUSI PEMBENIHAN IKAN KOI...". <i>ejournal brin</i>.</li>
                    </ul>
                </div>
            </section>
        </main>

    </div>

    <script>
        let currentTab = 'ringkasan';
        let currentMethod = 'alami';
        let metricsChart;

        const methodData = {
            'alami': {
                title: 'Metode: Alami',
                steps: [
                    { title: 'Seleksi Induk', desc: 'Pilih induk jantan (operkulum kasar, keluar sperma) dan betina (perut lunak, genital bengkak) yang matang gonad.' },
                    { title: 'Persiapan Kolam & Kakaban', desc: 'Siapkan kolam/bak yang bersih dan pasang kakaban (media ijuk/waring) sebagai tempat telur menempel.' },
                    { title: 'Proses Pemijahan', desc: 'Masukkan induk (rasio 1:1 atau 2:1) ke kolam pada sore hari. Pemijahan terjadi alami di malam/dini hari.' },
                    { title: 'Penetasan & Perawatan', desc: 'Pindahkan induk setelah memijah (agar telur tidak dimakan). Pindahkan kakaban ke bak penetasan. Telur menetas dalam 2-3 hari. Beri pakan larva (Artemia/Daphnia) setelah kantung telur habis.' }
                ],
                data: {
                    hormon: 'Tidak ada. Proses bergantung 100% pada kesiapan alami induk.',
                    ovulasi: 'Terjadi secara alami di kolam pemijahan.',
                    pembuahan: 'Eksternal, terjadi secara alami di kakaban saat jantan menyemprotkan sperma ke telur yang dikeluarkan betina.',
                    poin: 'Tingkat stres induk rendah, namun waktu pemijahan tidak seragam.'
                }
            },
            'semi': {
                title: 'Metode: Semi-Buatan',
                steps: [
                    { title: 'Seleksi & Induksi Hormon', desc: 'Pilih induk matang gonad. Suntik induk betina (kadang jantan) dengan hormon perangsang (misal Ovaprim 0.5 ml/kg).' },
                    { title: 'Persiapan Kolam & Kakaban', desc: 'Siapkan kolam/bak bersih dengan kakaban, sama seperti metode alami.' },
                    { title: 'Proses Pemijahan Alami', desc: 'Masukkan induk yang telah disuntik ke kolam. Hormon akan memicu ovulasi serentak, induk akan memijah (kawin) secara alami di kakaban.' },
                    { title: 'Penetasan & Perawatan', desc: 'Pindahkan induk setelah memijah. Pindahkan kakaban ke bak penetasan. Telur menetas dalam 2-3 hari. Lanjut perawatan larva.' }
                ],
                data: {
                    hormon: 'Ya, digunakan (misal Ovaprim, Ovaspek) untuk merangsang dan menyeragamkan ovulasi.',
                    ovulasi: 'Dipicu oleh hormon, namun pelepasan telur terjadi secara alami di kolam.',
                    pembuahan: 'Eksternal, terjadi secara alami di kakaban. Keberhasilan lebih serentak.',
                    poin: 'Waktu pemijahan lebih terprediksi dan seragam. Produksi bisa terjadwal.'
                }
            },
            'buatan': {
                title: 'Metode: Buatan (Stripping)',
                steps: [
                    { title: 'Seleksi & Induksi Hormon', desc: 'Suntik induk betina dan jantan dengan hormon. Tunggu 8-10 jam hingga induk betina siap ovulasi.' },
                    { title: 'Stripping (Pengurutan)', desc: 'Keluarkan telur dari betina dengan mengurut perut (stripping) ke wadah kering. Lakukan hal yang sama pada jantan untuk mengeluarkan sperma.' },
                    { title: 'Pembuahan Buatan', desc: 'Campur telur dan sperma di wadah. Tambahkan larutan NaCl fisiologis, aduk perlahan selama 1-2 menit. Bilas telur dengan air bersih.' },
                    { title: 'Penetasan & Perawatan', desc: 'Tebar telur yang telah dibuahi ke wadah penetasan (akuarium/bak) dengan aerasi. Telur menetas dalam 2-3 hari. Lanjut perawatan larva.' }
                ],
                data: {
                    hormon: 'Ya, wajib digunakan untuk memicu ovulasi dan spermiasi secara presisi.',
                    ovulasi: 'Dipicu hormon, telur dikeluarkan paksa (stripping) oleh manusia.',
                    pembuahan: 'Eksternal, dilakukan secara buatan oleh manusia di dalam wadah (in-vitro).',
                    poin: 'Kontrol paling tinggi, FR bisa sangat tinggi (90%+), namun induk rentan stres.'
                }
            }
        };

        function showTab(tabName) {
            currentTab = tabName;
            
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById('tab-btn-' + tabName).classList.add('active');
            
            document.querySelectorAll('.content-section').forEach(section => section.classList.remove('active'));
            document.getElementById('content-' + tabName).classList.add('active');

            if (tabName === 'data') {
                renderChart();
            }
        }

        function showMethod(methodName) {
            currentMethod = methodName;

            document.querySelectorAll('.method-btn').forEach(btn => btn.classList.remove('active'));
            document.getElementById('method-btn-' + methodName).classList.add('active');

            const data = methodData[methodName];
            
            document.getElementById('method-title').textContent = data.title;

            for (let i = 0; i < data.steps.length; i++) {
                document.getElementById(`step-${i+1}-title`).textContent = data.steps[i].title;
                document.getElementById(`step-${i+1}-desc`).textContent = data.steps[i].desc;
            }

            document.getElementById('data-hormon').textContent = data.data.hormon;
            document.getElementById('data-ovulasi').textContent = data.data.ovulasi;
            document.getElementById('data-pembuahan').textContent = data.data.pembuahan;
            document.getElementById('data-poin').textContent = data.data.poin;
        }
        
        function renderChart() {
            const ctx = document.getElementById('metricsChart').getContext('2d');
            
            const chartData = {
                labels: ['Alami (Jurnal)', 'Semi-Buatan (Jurnal)', 'Buatan (Jurnal)'],
                datasets: [
                    {
                        label: 'Fertilization Rate (FR) %',
                        data: [81, 85, 90.4],
                        backgroundColor: 'rgba(54, 162, 235, 0.6)', 
                        borderColor: 'rgba(54, 162, 235, 1)',
                        borderWidth: 1
                    },
                    {
                        label: 'Hatching Rate (HR) %',
                        data: [75, 80, 82.9], 
                        backgroundColor: 'rgba(75, 192, 192, 0.6)', 
                        borderColor: 'rgba(75, 192, 192, 1)',
                        borderWidth: 1
                    }
                ]
            };

            if (metricsChart) {
                metricsChart.destroy();
            }

            metricsChart = new Chart(ctx, {
                type: 'bar',
                data: chartData,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            title: {
                                display: true,
                                text: 'Persentase (%)'
                            }
                        }
                    },
                    plugins: {
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    let label = context.dataset.label || '';
                                    if (label) {
                                        label += ': ';
                                    }
                                    if (context.parsed.y !== null) {
                                        label += context.parsed.y + '%';
                                    }
                                    return label;
                                }
                            }
                        }
                    }
                }
            });
        }
        
        document.addEventListener('DOMContentLoaded', () => {
            showTab(currentTab);
            showMethod(currentMethod);
        });

    </script>

</body>
</html>

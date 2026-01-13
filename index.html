<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PDF PPT Viewer</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0f172a;
            color: #f8fafc;
            overflow: hidden;
            margin: 0;
        }

        /* Navigasi Overlay */
        .nav-btn {
            position: fixed;
            top: 0;
            bottom: 0;
            width: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(0, 0, 0, 0);
            border: none;
            color: rgba(255, 255, 255, 0.1);
            cursor: pointer;
            transition: all 0.3s ease;
            z-index: 50;
            outline: none;
        }

        .nav-btn:hover {
            background: rgba(255, 255, 255, 0.03);
            color: rgba(255, 255, 255, 0.6);
        }

        .nav-btn.prev { left: 0; }
        .nav-btn.next { right: 0; }

        .nav-btn svg {
            width: 40px;
            height: 40px;
        }

        /* Status Page */
        #page-info {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.5);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            opacity: 0.4;
            transition: opacity 0.3s;
            pointer-events: none;
            z-index: 60;
        }

        #viewer-container:hover #page-info {
            opacity: 1;
        }

        /* Canvas Wrapper */
        #canvas-wrapper {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            width: 100vw;
            background-color: #000;
        }

        canvas {
            box-shadow: 0 0 50px rgba(0,0,0,0.5);
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
        }

        .hidden { display: none !important; }

        /* Area Upload */
        #upload-screen {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            background: radial-gradient(circle at center, #1e293b 0%, #0f172a 100%);
        }

        .upload-box {
            border: 2px dashed rgba(255,255,255,0.1);
            padding: 3rem;
            border-radius: 1.5rem;
            transition: all 0.3s;
            cursor: pointer;
        }

        .upload-box:hover {
            border-color: #38bdf8;
            background: rgba(56, 189, 248, 0.05);
        }
    </style>
</head>
<body>

    <!-- Upload Screen -->
    <div id="upload-screen">
        <div class="upload-box" onclick="document.getElementById('file-input').click()">
            <svg class="w-16 h-16 mx-auto mb-4 text-sky-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
            </svg>
            <h1 class="text-2xl font-semibold mb-2">Unggah PDF Anda</h1>
            <p class="text-slate-400 mb-6">Klik atau seret file PDF untuk memulai presentasi</p>
            <button class="bg-sky-600 hover:bg-sky-500 text-white px-6 py-2 rounded-lg font-medium transition">
                Pilih File
            </button>
            <input type="file" id="file-input" class="hidden" accept="application/pdf">
        </div>
    </div>

    <!-- Viewer Screen -->
    <div id="viewer-screen" class="hidden">
        <button class="nav-btn prev" id="prev-page">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path></svg>
        </button>
        
        <button class="nav-btn next" id="next-page">
            <svg fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
        </button>

        <div id="page-info">
            Halaman <span id="page-num">1</span> dari <span id="page-count">0</span>
        </div>

        <div id="canvas-wrapper">
            <canvas id="pdf-canvas"></canvas>
        </div>
    </div>

    <script>
        const pdfjsLib = window['pdfjs-dist/build/pdf'];
        pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

        let pdfDoc = null,
            pageNum = 1,
            pageRendering = false,
            pageNumPending = null,
            scale = 2, // Kualitas render tinggi
            canvas = document.getElementById('pdf-canvas'),
            ctx = canvas.getContext('2d');

        const uploadScreen = document.getElementById('upload-screen');
        const viewerScreen = document.getElementById('viewer-screen');
        const fileInput = document.getElementById('file-input');

        /**
         * Render halaman spesifik
         */
        function renderPage(num) {
            pageRendering = true;
            
            pdfDoc.getPage(num).then((page) => {
                const viewport = page.getViewport({ scale: scale });
                
                // Sesuaikan canvas dengan viewport
                canvas.height = viewport.height;
                canvas.width = viewport.width;

                const renderContext = {
                    canvasContext: ctx,
                    viewport: viewport
                };
                
                const renderTask = page.render(renderContext);

                renderTask.promise.then(() => {
                    pageRendering = false;
                    if (pageNumPending !== null) {
                        renderPage(pageNumPending);
                        pageNumPending = null;
                    }
                });
            });

            document.getElementById('page-num').textContent = num;
        }

        /**
         * Antrian render jika sedang merender halaman lain
         */
        function queueRenderPage(num) {
            if (pageRendering) {
                pageNumPending = num;
            } else {
                renderPage(num);
            }
        }

        /**
         * Navigasi
         */
        function onPrevPage() {
            if (pageNum <= 1) return;
            pageNum--;
            queueRenderPage(pageNum);
        }

        function onNextPage() {
            if (pageNum >= pdfDoc.numPages) return;
            pageNum++;
            queueRenderPage(pageNum);
        }

        /**
         * Keluar dari mode viewer (Escape)
         */
        function exitViewer() {
            viewerScreen.classList.add('hidden');
            uploadScreen.classList.remove('hidden');
            pdfDoc = null;
            pageNum = 1;
            fileInput.value = ""; // Reset input
        }

        /**
         * Load Document
         */
        fileInput.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file && file.type === 'application/pdf') {
                const reader = new FileReader();
                reader.onload = function() {
                    const typedarray = new Uint8Array(this.result);

                    pdfjsLib.getDocument(typedarray).promise.then((pdfDoc_) => {
                        pdfDoc = pdfDoc_;
                        document.getElementById('page-count').textContent = pdfDoc.numPages;
                        
                        // Switch UI
                        uploadScreen.classList.add('hidden');
                        viewerScreen.classList.remove('hidden');
                        
                        pageNum = 1;
                        renderPage(pageNum);
                    }).catch(err => {
                        console.error("Error loading PDF: ", err);
                        alert("Gagal memuat PDF. Pastikan file tidak rusak.");
                    });
                };
                reader.readAsArrayBuffer(file);
            }
        });

        // Event Listeners
        document.getElementById('prev-page').addEventListener('click', onPrevPage);
        document.getElementById('next-page').addEventListener('click', onNextPage);

        // Keyboard Controls
        window.addEventListener('keydown', (e) => {
            if (viewerScreen.classList.contains('hidden')) return;

            if (e.key === 'ArrowLeft') {
                onPrevPage();
            } else if (e.key === 'ArrowRight' || e.key === ' ') {
                onNextPage();
            } else if (e.key === 'Escape') {
                exitViewer();
            }
        });

        // Auto-resize handling (optional but good for PPT feel)
        window.addEventListener('resize', () => {
            if (pdfDoc && !viewerScreen.classList.contains('hidden')) {
                queueRenderPage(pageNum);
            }
        });
    </script>
</body>
</html>

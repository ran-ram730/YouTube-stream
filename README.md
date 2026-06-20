<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YouTube-stream</title>
    <!-- Tailwind CSS for UI styling -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome for icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Custom scrollbar for better UI experience */
        ::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #1f2937;
        }
        ::-webkit-scrollbar-thumb {
            background: #ef4444;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #dc2626;
        }
    </style>
</head>
<body class="bg-gray-900 text-gray-100 min-h-screen font-sans flex flex-col">

    <!-- Header Section -->
    <header class="bg-gray-800 border-b border-gray-700 py-4 px-6 shadow-md">
        <div class="max-w-7xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4">
            <div class="flex items-center gap-3">
                <div class="bg-red-600 p-2.5 rounded-lg text-white animate-pulse">
                    <i class="fa-brands fa-youtube text-2xl"></i>
                </div>
                <div>
                    <h1 class="text-xl md:text-2xl font-bold tracking-tight text-white">YouTube Multi-Streamer</h1>
                    <p class="text-xs text-gray-400">Ek sath jitni baar chahein, video play karein aur views analyze karein</p>
                </div>
            </div>
            <div class="flex items-center gap-2 text-xs bg-gray-900 px-3 py-1.5 rounded-full text-gray-400 border border-gray-700">
                <span class="inline-block w-2.5 h-2.5 rounded-full bg-green-500 animate-ping"></span>
                <span>Active Streams Monitor</span>
            </div>
        </div>
    </header>

    <!-- Main Content Area -->
    <main class="flex-grow max-w-7xl w-full mx-auto p-4 md:p-6 flex flex-col gap-6">
        
        <!-- Control Panel Card -->
        <section class="bg-gray-800 border border-gray-700 rounded-xl p-5 shadow-lg">
            <h2 class="text-lg font-semibold mb-4 text-gray-200 flex items-center gap-2">
                <i class="fa-solid fa-sliders text-red-500"></i> Video Aur Stream Control Setup
            </h2>
            
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-5">
                <!-- Left: YouTube URL Input (6 Cols) -->
                <div class="lg:col-span-6 flex flex-col gap-2">
                    <label for="videoUrl" class="text-sm font-medium text-gray-300">YouTube Video Link (URL) dalein:</label>
                    <div class="relative">
                        <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
                            <i class="fa-brands fa-youtube text-gray-500 text-lg"></i>
                        </div>
                        <input type="text" id="videoUrl" 
                               class="block w-full pl-10 pr-3 py-3 bg-gray-900 border border-gray-600 rounded-lg text-white placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent transition-all" 
                               placeholder="https://www.youtube.com/watch?v=xxxxxx ya https://youtu.be/xxxxxx"
                               value="https://www.youtube.com/watch?v=dQw4w9WgXcQ">
                    </div>
                    <span class="text-xs text-gray-400">Sahi YouTube link automatically detect hokar embed code me badal jayegi.</span>
                </div>

                <!-- Middle: Play Count Input (3 Cols) -->
                <div class="lg:col-span-3 flex flex-col gap-2">
                    <label for="playCount" class="text-sm font-medium text-gray-300">Kitne Baar Play Karna Hai? (Count):</label>
                    <div class="flex gap-2">
                        <input type="number" id="playCount" min="1" max="1000" value="10"
                               class="w-full px-3 py-3 bg-gray-900 border border-gray-600 rounded-lg text-white text-center font-bold focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent transition-all">
                    </div>
                    <div class="flex gap-1 justify-between">
                        <button onclick="setQuickCount(10)" class="text-xs bg-gray-700 hover:bg-gray-600 px-2 py-1 rounded transition">10x</button>
                        <button onclick="setQuickCount(50)" class="text-xs bg-gray-700 hover:bg-gray-600 px-2 py-1 rounded transition">50x</button>
                        <button onclick="setQuickCount(100)" class="text-xs bg-gray-700 hover:bg-gray-600 px-2 py-1 rounded transition">100x</button>
                        <button onclick="setQuickCount(200)" class="text-xs bg-gray-700 hover:bg-gray-600 px-2 py-1 rounded transition">200x</button>
                        <button onclick="setQuickCount(500)" class="text-xs bg-gray-700 hover:bg-gray-600 px-2 py-1 rounded transition font-bold text-red-400">500x</button>
                    </div>
                </div>

                <!-- Right: Grid Columns & Options (3 Cols) -->
                <div class="lg:col-span-3 flex flex-col gap-2">
                    <label for="gridCols" class="text-sm font-medium text-gray-300">Layout (Ek line me kitne video):</label>
                    <select id="gridCols" class="w-full px-3 py-3 bg-gray-900 border border-gray-600 rounded-lg text-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent transition-all">
                        <option value="grid-cols-1">1 Column (Bada Size)</option>
                        <option value="sm:grid-cols-2">2 Columns</option>
                        <option value="sm:grid-cols-2 md:grid-cols-3" selected>3 Columns (Behtareen)</option>
                        <option value="sm:grid-cols-2 md:grid-cols-4">4 Columns</option>
                        <option value="sm:grid-cols-3 md:grid-cols-6">6 Columns (Chhota Size)</option>
                    </select>

                    <div class="flex items-center gap-2 mt-2">
                        <input type="checkbox" id="muteByDefault" checked class="w-4 h-4 bg-gray-950 text-red-600 border-gray-600 rounded focus:ring-red-500">
                        <label for="muteByDefault" class="text-xs text-gray-300 cursor-pointer select-none">
                            Mute play karein (Autoplay policy ke liye recommended)
                        </label>
                    </div>
                </div>
            </div>

            <!-- Action Buttons -->
            <div class="mt-6 flex flex-wrap gap-3 items-center justify-between border-t border-gray-700 pt-5">
                <div class="flex fleix-wrap gap-2">
                    <button id="btnGenerate" onclick="generateStreams()" class="bg-red-600 hover:bg-red-700 text-white font-bold px-6 py-3 rounded-lg flex items-center gap-2 transition duration-200 transform active:scale-95 shadow-md">
                        <i class="fa-solid fa-play"></i> Play Streams Start
                    </button>
                    <button id="btnClear" onclick="clearStreams()" class="bg-gray-700 hover:bg-gray-600 text-gray-200 font-medium px-4 py-3 rounded-lg flex items-center gap-2 transition duration-200 active:scale-95">
                        <i class="fa-solid fa-trash-can"></i> Clear now
                    </button>
                </div>
                
                <!-- Quick Instructions Warning -->
                <div class="text-xs text-amber-400 bg-amber-950/40 border border-amber-900/50 p-2.5 rounded-lg max-w-md flex items-start gap-2">
                    <i class="fa-solid fa-circle-exclamation mt-0.5 text-base flex-shrink-0"></i>
                    <span><strong>Note:</strong> Ek sath 100+ videos play karne par browser hanging/lag ho sakta hai, yeh aapke system aur internet speed par depend karega.</span>
                </div>
            </div>
        </section>

        <!-- Stats Panel (Hidden until played) -->
        <section id="statsPanel" class="hidden bg-gray-800 border border-gray-700 rounded-xl p-4 shadow-md flex-wrap items-center justify-between gap-4">
            <div class="flex items-center gap-4">
                <div class="text-sm">
                    <span class="text-gray-400">play Streams:</span>
                    <span id="activeCountBadge" class="ml-1 text-lg font-bold text-red-500">0</span>
                </div>
                <div class="h-6 w-px bg-gray-700"></div>
                <div class="text-sm">
                    <span class="text-gray-400">Video ID:</span>
                    <span id="currentVideoId" class="ml-1 font-mono text-gray-300">N/A</span>
                </div>
            </div>
            
            <div class="flex items-center gap-3">
                <button onclick="scrollWindowTo('streamsContainer')" class="text-xs bg-gray-900 hover:bg-gray-700 text-gray-300 px-3 py-1.5 rounded-md border border-gray-700 transition">
                    <i class="fa-solid fa-arrow-down"></i> Videos Par Jayein
                </button>
            </div>
        </section>

        <!-- Dynamic Streams Grid Wrapper -->
        <section class="flex flex-col gap-4">
            <div class="flex items-center justify-between">
                <h3 class="text-lg font-semibold text-gray-200 flex items-center gap-2">
                    <i class="fa-solid fa-tv text-red-500"></i> Video Streams Viewport
                </h3>
                <span id="streamIndicatorText" class="text-xs text-gray-500">Koi video abhi active nahi hai.</span>
            </div>

            <!-- This is where multiple iFrames will render dynamically -->
            <div id="streamsContainer" class="grid gap-4 w-full">
                <!-- Initial Empty State -->
                <div id="emptyState" class="col-span-full py-16 px-4 flex flex-col items-center justify-center text-center bg-gray-800 rounded-xl border border-dashed border-gray-700">
                    <div class="w-20 h-20 bg-gray-900/60 rounded-full flex items-center justify-center text-gray-600 mb-4">
                        <i class="fa-brands fa-youtube text-4xl"></i>
                    </div>
                    <h4 class="text-lg font-medium text-gray-300">Abhi tak koi stream set nahi hui hai</h4>
                    <p class="text-sm text-gray-500 mt-1 max-w-sm">Apne YouTube video ka link upar box me dalein aur "Play Streams Start" button par click karein.</p>
                </div>
            </div>
        </section>

    </main>

    <!-- Detailed Explanation and FAQ Accordion -->
    <section class="max-w-7xl w-full mx-auto px-4 md:px-6 pb-12 mt-6">
        <div class="bg-gray-800/80 border border-gray-700 rounded-xl p-5 shadow-sm">
            <h3 class="text-md font-bold text-gray-200 mb-3 flex items-center gap-2">
                <i class="fa-solid fa-circle-question text-red-500"></i> Is Website Ko Sahi Se Kaise Use Karein?
            </h3>
            <ul class="space-y-3 text-sm text-gray-300 list-inside list-disc">
                <li><strong>Link format:</strong> Aap normal link (<code class="bg-gray-950 px-1 py-0.5 rounded text-red-400">https://www.youtube.com/watch?v=...</code>) ya share link (<code class="bg-gray-950 px-1 py-0.5 rounded text-red-400">https://youtu.be/...</code>) koi bhi use kar sakte hain. Website automatic convert kar degi.</li>
                <li><strong>Auto-Play Rule:</strong> Google Chrome aur dusre browsers automatic sound play karne se rokte hain. Isliye video auto-play hone ke liye <strong>Mute check-box</strong> ko tick rakhna zaruri hai. Play hone ke baad aap manually sound icon par click karke unmute kar sakte hain.</li>
                <li><strong>Views badhane ke liye tips:</strong> Agar aap self-testing ya views observe kar rahe hain, to lagatar same IP address se play na karein (VPN use kar sakte hain).</li>
                <li><strong>System lag solution:</strong> Agar lag ho, to columns layout ko 6 Columns (Chhota Size) select karein aur multiple Tabs me chalane ki jagah ek hi tab me play karein.</li>
            </ul>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-950 py-6 px-4 border-t border-gray-800 text-center text-sm text-gray-500">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            <p>© 2026 YouTube Multiplier Web Utility. All rights reserved.</p>
            <div class="flex gap-4">
                <span class="hover:text-red-500 cursor-pointer">Privacy Policy</span>
                <span class="hover:text-red-500 cursor-pointer">Terms of Use</span>
                <span class="hover:text-red-500 cursor-pointer">Support</span>
            </div>
        </div>
    </footer>

    <!-- Custom Notification Toast -->
    <div id="toast" class="fixed bottom-5 right-5 bg-gray-800 border-l-4 border-red-500 text-gray-100 px-4 py-3 rounded-md shadow-2xl transition-all duration-300 transform translate-y-20 opacity-0 pointer-events-none flex items-center gap-2 max-w-sm">
        <i class="fa-solid fa-circle-info text-red-500"></i>
        <span id="toastMessage">Safaralata purvak load ho gaya!</span>
    </div>

    <!-- Scripting for application behavior -->
    <script>
        // Set Quick number of plays helper function
        function setQuickCount(num) {
            document.getElementById('playCount').value = num;
            showToast(`Play count ko set kiya gaya: ${num}`);
        }

        // Custom Notification helper
        function showToast(message) {
            const toast = document.getElementById('toast');
            const toastMsg = document.getElementById('toastMessage');
            toastMsg.innerText = message;
            
            // Bring into view
            toast.classList.remove('translate-y-20', 'opacity-0', 'pointer-events-none');
            toast.classList.add('translate-y-0', 'opacity-100');
            
            // Dismiss after 3 seconds
            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0', 'pointer-events-none');
            }, 3000);
        }

        // YouTube video id extraction regex
        function getYouTubeVideoId(url) {
            const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
            const match = url.match(regExp);
            return (match && match[2].length === 11) ? match[2] : null;
        }

        // Clear all active iFrames
        function clearStreams() {
            const container = document.getElementById('streamsContainer');
            container.innerHTML = `
                <div id="emptyState" class="col-span-full py-16 px-4 flex flex-col items-center justify-center text-center bg-gray-800 rounded-xl border border-dashed border-gray-700">
                    <div class="w-20 h-20 bg-gray-900/60 rounded-full flex items-center justify-center text-gray-600 mb-4">
                        <i class="fa-brands fa-youtube text-4xl"></i>
                    </div>
                    <h4 class="text-lg font-medium text-gray-300">Abhi tak koi stream set nahi hui hai</h4>
                    <p class="text-sm text-gray-500 mt-1 max-w-sm">Apne YouTube video ka link upar box me dalein aur "Play Streams Start" button par click karein.</p>
                </div>
            `;
            
            document.getElementById('statsPanel').classList.add('hidden');
            document.getElementById('streamIndicatorText').innerText = "Koi video abhi active nahi hai.";
            document.getElementById('streamIndicatorText').classList.add('text-gray-500');
            document.getElementById('streamIndicatorText').classList.remove('text-green-500');
            showToast('Sabhi active videos ko saaf kar diya gaya.');
        }

        // Window scroll helper
        function scrollWindowTo(elementId) {
            const element = document.getElementById(elementId);
            if(element) {
                element.scrollIntoView({ behavior: 'smooth' });
            }
        }

        // Core processing logic
        function generateStreams() {
            const videoUrlInput = document.getElementById('videoUrl').value.trim();
            const playCount = parseInt(document.getElementById('playCount').value);
            const gridLayoutClass = document.getElementById('gridCols').value;
            const muteSetting = document.getElementById('muteByDefault').checked;
            
            if (!videoUrlInput) {
                showToast('Kripya pehle YouTube video URL link dalein.');
                return;
            }

            const videoId = getYouTubeVideoId(videoUrlInput);
            if (!videoId) {
                showToast('Sahi YouTube link nahi mila. Kripya valid YouTube URL dalein.');
                return;
            }

            if (isNaN(playCount) || playCount <= 0) {
                showToast('Kripya streams ki sankhya sahi (1 ya usse upar) enter karein.');
                return;
            }

            if(playCount > 1000) {
                showToast('System lag se bachne ke liye maximum limit 1000 hai.');
                return;
            }

            const container = document.getElementById('streamsContainer');
            container.innerHTML = ''; // Clear previous content and empty state

            // Set grid classes
            container.className = `grid gap-4 w-full ${gridLayoutClass}`;

            showToast(`${playCount} streams create ho rahi hain. Kripya dhyan dein...`);

            // Build YouTube embed URL query params
            // enablejsapi=1 lets us hook if required, autoplay=1 runs immediately, mute=1 for chrome autoplay policy bypass
            let embedUrl = `https://www.youtube.com/embed/${videoId}?autoplay=1&playlist=${videoId}&loop=1&enablejsapi=1`;
            if (muteSetting) {
                embedUrl += '&mute=1';
            }

            // Create individual blocks
            for (let i = 1; i <= playCount; i++) {
                const streamCard = document.createElement('div');
                streamCard.className = "bg-gray-800 border border-gray-700 rounded-lg overflow-hidden flex flex-col shadow-md hover:border-red-500 transition duration-150";
                
                streamCard.innerHTML = `
                    <div class="relative w-full pb-[56.25%] bg-black">
                        <iframe 
                            src="${embedUrl}" 
                            title="YouTube Player #${i}"
                            class="absolute top-0 left-0 w-full h-full"
                            frameborder="0" 
                            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
                            allowfullscreen
                            loading="lazy">
                        </iframe>
                    </div>
                    <div class="p-2 bg-gray-900 border-t border-gray-800 flex justify-between items-center text-xs text-gray-400">
                        <span class="font-bold text-red-500">Stream #${i}</span>
                        <div class="flex items-center gap-1.5">
                            <span class="inline-block w-2 h-2 rounded-full bg-green-500"></span>
                            <span>Playing</span>
                        </div>
                    </div>
                `;
                container.appendChild(streamCard);
            }

            // Update Statistics and Badges
            const statsPanel = document.getElementById('statsPanel');
            statsPanel.classList.remove('hidden');
            document.getElementById('activeCountBadge').innerText = playCount;
            document.getElementById('currentVideoId').innerText = videoId;
            
            const indicatorText = document.getElementById('streamIndicatorText');
            indicatorText.innerText = `${playCount} Active Video Streams chal rahe hain.`;
            indicatorText.classList.remove('text-gray-500');
            indicatorText.classList.add('text-green-500');

            // Automatically scroll to the grid viewport
            setTimeout(() => {
                scrollWindowTo('statsPanel');
            }, 300);
        }
    </script>
</body>
</html>

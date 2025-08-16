<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Interaction Counter</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Simple transition for showing/hiding sections */
        .section {
            transition: opacity 0.3s ease-in-out;
        }
    </style>
</head>
<body class="bg-gray-100 flex items-center justify-center min-h-screen">

    <div class="w-full max-w-md mx-auto bg-white rounded-2xl shadow-lg p-6 md:p-8 space-y-6">

        <!-- ===== Setup Section ===== -->
        <div id="setup-section" class="section space-y-4">
            <h1 class="text-2xl font-bold text-gray-800 text-center">Event Counter</h1>
            <p class="text-center text-gray-500">Enter the name of your event to begin.</p>
            <div>
                <label for="event-name-input" class="text-sm font-medium text-gray-700">Event Name</label>
                <input type="text" id="event-name-input" class="mt-1 block w-full px-4 py-3 bg-gray-50 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500" placeholder="e.g., Holbrook Street Fair">
            </div>
            <button id="start-btn" class="w-full bg-blue-600 text-white font-bold py-3 px-4 rounded-lg hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 transition-transform transform hover:scale-105">
                Start Event
            </button>
        </div>

        <!-- ===== Counter Section ===== -->
        <div id="counter-section" class="section hidden space-y-6">
            <h2 id="event-name-display" class="text-xl font-bold text-gray-800 text-center truncate"></h2>
            
            <!-- Interaction Counters -->
            <div class="space-y-4">
                <!-- Tier 1: Passersby -->
                <div class="p-4 bg-gray-50 rounded-lg">
                    <p class="text-sm font-semibold text-gray-600">Total Passersby</p>
                    <div class="flex items-center justify-between mt-2">
                        <span id="passersby-count" class="text-4xl font-bold text-gray-800">0</span>
                        <div class="flex items-center space-x-2">
                            <button data-counter="passersby" data-action="minus" class="undo-btn w-12 h-12 bg-gray-200 text-gray-600 rounded-full text-2xl font-bold flex items-center justify-center hover:bg-gray-300">-</button>
                            <button data-counter="passersby" data-action="plus" class="add-btn w-16 h-16 bg-blue-500 text-white rounded-full text-3xl font-bold flex items-center justify-center hover:bg-blue-600">+</button>
                        </div>
                    </div>
                </div>

                <!-- Tier 2: Impressions -->
                <div class="p-4 bg-gray-50 rounded-lg">
                    <p class="text-sm font-semibold text-gray-600">Impressions / Stops</p>
                    <div class="flex items-center justify-between mt-2">
                        <span id="impressions-count" class="text-4xl font-bold text-gray-800">0</span>
                        <div class="flex items-center space-x-2">
                            <button data-counter="impressions" data-action="minus" class="undo-btn w-12 h-12 bg-gray-200 text-gray-600 rounded-full text-2xl font-bold flex items-center justify-center hover:bg-gray-300">-</button>
                            <button data-counter="impressions" data-action="plus" class="add-btn w-16 h-16 bg-green-500 text-white rounded-full text-3xl font-bold flex items-center justify-center hover:bg-green-600">+</button>
                        </div>
                    </div>
                </div>

                <!-- Tier 3: Brief Interactions -->
                <div class="p-4 bg-gray-50 rounded-lg">
                    <p class="text-sm font-semibold text-gray-600">Brief Interactions (Took Item)</p>
                    <div class="flex items-center justify-between mt-2">
                        <span id="brief-count" class="text-4xl font-bold text-gray-800">0</span>
                        <div class="flex items-center space-x-2">
                            <button data-counter="brief" data-action="minus" class="undo-btn w-12 h-12 bg-gray-200 text-gray-600 rounded-full text-2xl font-bold flex items-center justify-center hover:bg-gray-300">-</button>
                            <button data-counter="brief" data-action="plus" class="add-btn w-16 h-16 bg-yellow-500 text-white rounded-full text-3xl font-bold flex items-center justify-center hover:bg-yellow-600">+</button>
                        </div>
                    </div>
                </div>

                <!-- Tier 4: Meaningful Interactions -->
                <div class="p-4 bg-gray-50 rounded-lg">
                    <p class="text-sm font-semibold text-gray-600">Meaningful Interactions (Spoke)</p>
                    <div class="flex items-center justify-between mt-2">
                        <span id="meaningful-count" class="text-4xl font-bold text-gray-800">0</span>
                        <div class="flex items-center space-x-2">
                            <button data-counter="meaningful" data-action="minus" class="undo-btn w-12 h-12 bg-gray-200 text-gray-600 rounded-full text-2xl font-bold flex items-center justify-center hover:bg-gray-300">-</button>
                            <button data-counter="meaningful" data-action="plus" class="add-btn w-16 h-16 bg-red-500 text-white rounded-full text-3xl font-bold flex items-center justify-center hover:bg-red-600">+</button>
                        </div>
                    </div>
                </div>
            </div>

            <button id="end-btn" class="w-full bg-gray-700 text-white font-bold py-3 px-4 rounded-lg hover:bg-gray-800 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500">
                End Event & View Totals
            </button>
        </div>

        <!-- ===== Summary Section ===== -->
        <div id="summary-section" class="section hidden space-y-4">
            <h2 class="text-2xl font-bold text-gray-800 text-center">Event Summary</h2>
            <div class="p-4 bg-blue-50 border border-blue-200 rounded-lg space-y-3 text-center">
                <p class="font-semibold text-lg text-blue-800" id="summary-event-name"></p>
                <div class="grid grid-cols-2 gap-4 text-left pt-2">
                    <p class="font-medium text-gray-600">Total Passersby:</p>
                    <p id="summary-passersby" class="font-bold text-xl text-gray-800 text-right"></p>
                    
                    <p class="font-medium text-gray-600">Impressions:</p>
                    <p id="summary-impressions" class="font-bold text-xl text-gray-800 text-right"></p>
                    
                    <p class="font-medium text-gray-600">Brief Interactions:</p>
                    <p id="summary-brief" class="font-bold text-xl text-gray-800 text-right"></p>
                    
                    <p class="font-medium text-gray-600">Meaningful Interactions:</p>
                    <p id="summary-meaningful" class="font-bold text-xl text-gray-800 text-right"></p>
                </div>
            </div>
            <p class="text-xs text-center text-gray-500">Screenshot this page or copy the totals into your spreadsheet.</p>
            <button id="reset-btn" class="w-full bg-blue-600 text-white font-bold py-3 px-4 rounded-lg hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                Start New Event
            </button>
        </div>

    </div>

    <script>
        // --- DOM Elements ---
        const setupSection = document.getElementById('setup-section');
        const counterSection = document.getElementById('counter-section');
        const summarySection = document.getElementById('summary-section');

        const eventNameInput = document.getElementById('event-name-input');
        const eventNameDisplay = document.getElementById('event-name-display');
        
        const startBtn = document.getElementById('start-btn');
        const endBtn = document.getElementById('end-btn');
        const resetBtn = document.getElementById('reset-btn');

        // --- State ---
        let eventName = '';
        const counts = {
            passersby: 0,
            impressions: 0,
            brief: 0,
            meaningful: 0,
        };

        // --- Functions ---

        /**
         * Updates the count display on the UI for a specific counter.
         * @param {string} counterName - The name of the counter (e.g., 'passersby').
         */
        function updateCountDisplay(counterName) {
            const countElement = document.getElementById(`${counterName}-count`);
            if (countElement) {
                countElement.textContent = counts[counterName];
            }
        }

        /**
         * Handles the start of an event.
         */
        function startEvent() {
            const name = eventNameInput.value.trim();
            if (name === '') {
                alert('Please enter an event name.');
                return;
            }
            eventName = name;
            eventNameDisplay.textContent = eventName;

            setupSection.classList.add('hidden');
            counterSection.classList.remove('hidden');
        }

        /**
         * Handles the end of an event and displays the summary.
         */
        function endEvent() {
            // Populate summary details
            document.getElementById('summary-event-name').textContent = eventName;
            document.getElementById('summary-passersby').textContent = counts.passersby;
            document.getElementById('summary-impressions').textContent = counts.impressions;
            document.getElementById('summary-brief').textContent = counts.brief;
            document.getElementById('summary-meaningful').textContent = counts.meaningful;

            counterSection.classList.add('hidden');
            summarySection.classList.remove('hidden');
        }

        /**
         * Resets the application to its initial state for a new event.
         */
        function resetApp() {
            eventName = '';
            eventNameInput.value = '';
            
            // Reset counts
            counts.passersby = 0;
            counts.impressions = 0;
            counts.brief = 0;
            counts.meaningful = 0;

            // Update all displays
            updateCountDisplay('passersby');
            updateCountDisplay('impressions');
            updateCountDisplay('brief');
            updateCountDisplay('meaningful');
            
            summarySection.classList.add('hidden');
            setupSection.classList.remove('hidden');
        }

        // --- Event Listeners ---

        startBtn.addEventListener('click', startEvent);
        endBtn.addEventListener('click', endEvent);
        resetBtn.addEventListener('click', resetApp);

        // Add event listeners to all counter buttons (+ and -)
        counterSection.addEventListener('click', (e) => {
            const target = e.target.closest('button');
            if (!target || (!target.classList.contains('add-btn') && !target.classList.contains('undo-btn'))) {
                return;
            }

            const counter = target.dataset.counter;
            const action = target.dataset.action;

            if (action === 'plus') {
                counts[counter]++;
            } else if (action === 'minus') {
                // Prevent count from going below zero
                if (counts[counter] > 0) {
                    counts[counter]--;
                }
            }
            
            updateCountDisplay(counter);
        });

    </script>
</body>
</html>

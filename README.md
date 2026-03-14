<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title> GANESHA HOSPITAL | Hospital Management System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc;
        }

        .sidebar-link.active {
            background-color: #eff6ff;
            border-right: 4px solid #2563eb;
            color: #2563eb;
        }

        .custom-scroll::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scroll::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        .custom-scroll::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 10px;
        }

        .ai-glow {
            box-shadow: 0 0 15px rgba(59, 130, 246, 0.5);
            border: 1px solid rgba(59, 130, 246, 0.3);
        }

        .loading-dots:after {
            content: '.';
            animation: dots 1.5s steps(5, end) infinite;
        }

        @keyframes dots {
            0%, 20% { content: '.'; }
            40% { content: '..'; }
            60% { content: '...'; }
            80%, 100% { content: ''; }
        }
    </style>
</head>
<body class="h-screen overflow-hidden flex text-slate-900">

    <!-- Sidebar -->
    <aside class="w-64 bg-white border-r border-slate-200 flex-shrink-0 flex flex-col hidden md:flex">
        <div class="p-6">
            <div class="flex items-center gap-3 text-blue-600">
                <i class="fas fa-hospital-alt text-2xl"></i>
                <h1 class="font-bold text-xl tracking-tight text-slate-800">Ganesha Care</h1>
            </div>
        </div>

        <nav class="mt-4 flex-1">
            <a href="#" onclick="showSection('dashboard')" id="nav-dashboard" class="sidebar-link active flex items-center px-6 py-4 text-slate-600 hover:bg-slate-50 transition-colors">
                <i class="fas fa-th-large w-6"></i>
                <span class="font-medium">Dashboard</span>
            </a>
            <a href="#" onclick="showSection('patients')" id="nav-patients" class="sidebar-link flex items-center px-6 py-4 text-slate-600 hover:bg-slate-50 transition-colors">
                <i class="fas fa-user-injured w-6"></i>
                <span class="font-medium">Patients</span>
            </a>
            <a href="#" onclick="showSection('ai-assistant')" id="nav-ai-assistant" class="sidebar-link flex items-center px-6 py-4 text-blue-600 bg-blue-50/50 hover:bg-blue-100 transition-colors">
                <i class="fas fa-sparkles w-6"></i>
                <span class="font-bold">✨ AI Assistant</span>
            </a>
            <a href="#" onclick="showSection('appointments')" id="nav-appointments" class="sidebar-link flex items-center px-6 py-4 text-slate-600 hover:bg-slate-50 transition-colors">
                <i class="fas fa-calendar-check w-6"></i>
                <span class="font-medium">Appointments</span>
            </a>
            <a href="#" onclick="showSection('billing')" id="nav-billing" class="sidebar-link flex items-center px-6 py-4 text-slate-600 hover:bg-slate-50 transition-colors">
                <i class="fas fa-file-invoice-dollar w-6"></i>
                <span class="font-medium">Billing</span>
            </a>
            <a href="#" onclick="showSection('doctors')" id="nav-doctors" class="sidebar-link flex items-center px-6 py-4 text-slate-600 hover:bg-slate-50 transition-colors">
                <i class="fas fa-user-md w-6"></i>
                <span class="font-medium">Doctors</span>
            </a>
        </nav>

        <div class="p-6 border-t border-slate-100">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-full bg-blue-100 flex items-center justify-center text-blue-600 font-bold" id="user-avatar">
                    ??
                </div>
                <div>
                    <p class="text-sm font-semibold text-slate-800" id="user-name">Initializing...</p>
                    <p class="text-xs text-slate-500" id="user-id-display">Connecting...</p>
                </div>
            </div>
        </div>
    </aside>

    <!-- Main Content -->
    <main class="flex-1 flex flex-col min-w-0 overflow-hidden">
        <!-- Header -->
        <header class="h-16 bg-white border-b border-slate-200 flex items-center justify-between px-8 flex-shrink-0">
            <div class="flex items-center gap-4">
                <button class="md:hidden text-slate-600 text-xl"><i class="fas fa-bars"></i></button>
                <h2 id="page-title" class="text-lg font-semibold text-slate-800">Hospital Dashboard</h2>
            </div>
            <div class="flex items-center gap-6">
                <div class="relative hidden sm:block">
                    <input type="text" placeholder="Search records..." class="pl-10 pr-4 py-2 bg-slate-100 border-none rounded-lg text-sm focus:ring-2 focus:ring-blue-400 outline-none w-64">
                    <i class="fas fa-search absolute left-3 top-2.5 text-slate-400"></i>
                </div>
                <button class="relative text-slate-400 hover:text-slate-600">
                    <i class="fas fa-bell text-xl"></i>
                    <span class="absolute -top-1 -right-1 w-4 h-4 bg-red-500 rounded-full border-2 border-white text-[10px] text-white flex items-center justify-center">3</span>
                </button>
            </div>
        </header>

        <!-- Content Area -->
        <div id="content-viewport" class="flex-1 overflow-y-auto p-8 custom-scroll">
            
            <!-- Dashboard Section -->
            <section id="section-dashboard" class="space-y-8">
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex items-center justify-between mb-4">
                            <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-lg flex items-center justify-center text-xl">
                                <i class="fas fa-users"></i>
                            </div>
                            <span class="text-green-500 text-sm font-medium">+12% <i class="fas fa-arrow-up"></i></span>
                        </div>
                        <h3 class="text-slate-500 text-sm font-medium">Total Patients</h3>
                        <p class="text-2xl font-bold text-slate-800 mt-1" id="stat-patients">0</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex items-center justify-between mb-4">
                            <div class="w-12 h-12 bg-purple-50 text-purple-600 rounded-lg flex items-center justify-center text-xl">
                                <i class="fas fa-calendar-check"></i>
                            </div>
                            <span class="text-green-500 text-sm font-medium">+5% <i class="fas fa-arrow-up"></i></span>
                        </div>
                        <h3 class="text-slate-500 text-sm font-medium">Appointments</h3>
                        <p class="text-2xl font-bold text-slate-800 mt-1" id="stat-appointments">0</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm bg-gradient-to-br from-blue-50 to-white ai-glow">
                        <div class="flex items-center justify-between mb-4">
                            <div class="w-12 h-12 bg-blue-600 text-white rounded-lg flex items-center justify-center text-xl">
                                <i class="fas fa-robot"></i>
                            </div>
                            <span class="text-blue-600 text-xs font-bold uppercase tracking-wider">Powered by Gemini</span>
                        </div>
                        <h3 class="text-slate-500 text-sm font-medium">AI Support Status</h3>
                        <p class="text-xl font-bold text-slate-800 mt-1">✨ AI Ready</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl border border-slate-200 shadow-sm">
                        <div class="flex items-center justify-between mb-4">
                            <div class="w-12 h-12 bg-emerald-50 text-emerald-600 rounded-lg flex items-center justify-center text-xl">
                                <i class="fas fa-wallet"></i>
                            </div>
                            <span class="text-green-500 text-sm font-medium">+22% <i class="fas fa-arrow-up"></i></span>
                        </div>
                        <h3 class="text-slate-500 text-sm font-medium">Daily Revenue</h3>
                        <p class="text-2xl font-bold text-slate-800 mt-1">$4,250</p>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <!-- Recent Patients -->
                    <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                        <div class="p-6 border-b border-slate-100 flex items-center justify-between">
                            <h3 class="font-bold text-slate-800">Recent Registrations</h3>
                            <button onclick="showSection('patients')" class="text-blue-600 text-sm font-medium hover:underline">View All</button>
                        </div>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left">
                                <thead class="bg-slate-50 text-slate-500 text-xs uppercase">
                                    <tr>
                                        <th class="px-6 py-3 font-semibold">Patient</th>
                                        <th class="px-6 py-3 font-semibold">ID</th>
                                        <th class="px-6 py-3 font-semibold">Status</th>
                                    </tr>
                                </thead>
                                <tbody id="recent-patients-list" class="divide-y divide-slate-100"></tbody>
                            </table>
                        </div>
                    </div>

                    <!-- Upcoming Appointments -->
                    <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                        <div class="p-6 border-b border-slate-100 flex items-center justify-between">
                            <h3 class="font-bold text-slate-800">Today's Schedule</h3>
                            <button onclick="showSection('appointments')" class="text-blue-600 text-sm font-medium hover:underline">Full Schedule</button>
                        </div>
                        <div id="today-appointments-list" class="p-2 space-y-2"></div>
                    </div>
                </div>
            </section>

            <!-- AI Assistant Section -->
            <section id="section-ai-assistant" class="hidden space-y-6">
                <div class="max-w-4xl mx-auto space-y-6">
                    <div class="bg-gradient-to-r from-blue-600 to-indigo-700 p-8 rounded-2xl text-white shadow-xl">
                        <h3 class="text-3xl font-bold mb-2">✨ Ganesha AI Medical Assistant</h3>
                        <p class="text-blue-100 opacity-90">Enter patient symptoms or medical queries below for instant AI-powered analysis and recommendations.</p>
                    </div>

                    <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden">
                        <div class="p-6 space-y-4">
                            <div>
                                <label class="block text-sm font-semibold text-slate-700 mb-2">Describe Symptoms / Query</label>
                                <textarea id="ai-input" rows="4" class="w-full px-4 py-3 border border-slate-200 rounded-xl focus:ring-2 focus:ring-blue-400 outline-none transition-all" placeholder="Example: Patient has severe headache, nausea, and sensitivity to light..."></textarea>
                            </div>
                            <button onclick="askAIAssistant()" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 rounded-xl transition-all shadow-lg flex items-center justify-center gap-2">
                                <i class="fas fa-magic"></i> Generate ✨ AI Analysis
                            </button>
                        </div>
                        
                        <!-- AI Result Display -->
                        <div id="ai-result-container" class="hidden border-t border-slate-100 bg-slate-50/50 p-6 animate-pulse">
                             <div id="ai-loading" class="text-blue-600 font-medium flex items-center gap-2">
                                 <i class="fas fa-circle-notch fa-spin"></i> Analyzing medical data<span class="loading-dots"></span>
                             </div>
                             <div id="ai-content" class="hidden space-y-4 prose prose-slate max-w-none">
                                 <!-- AI Response goes here -->
                             </div>
                        </div>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div class="bg-amber-50 border border-amber-200 p-4 rounded-xl flex gap-3">
                            <i class="fas fa-exclamation-triangle text-amber-500 mt-1"></i>
                            <p class="text-xs text-amber-800">
                                <strong>Disclaimer:</strong> This AI tool is for professional assistance only. It should not replace clinical judgment or official medical advice. Always verify results.
                            </p>
                        </div>
                        <div class="bg-blue-50 border border-blue-200 p-4 rounded-xl flex gap-3">
                            <i class="fas fa-lightbulb text-blue-500 mt-1"></i>
                            <p class="text-xs text-blue-800">
                                <strong>Tip:</strong> Be specific about patient history, duration of symptoms, and any visible signs for better accuracy.
                            </p>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Patients Section -->
            <section id="section-patients" class="hidden space-y-6">
                <div class="flex items-center justify-between">
                    <h3 class="text-2xl font-bold text-slate-800">Patient Directory</h3>
                    <button onclick="openModal('patientModal')" class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center gap-2">
                        <i class="fas fa-plus"></i> New Patient
                    </button>
                </div>
                <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                    <table class="w-full text-left">
                        <thead class="bg-slate-50 text-slate-500 text-xs uppercase">
                            <tr>
                                <th class="px-6 py-4">Name</th>
                                <th class="px-6 py-4">ID</th>
                                <th class="px-6 py-4">Status</th>
                                <th class="px-6 py-4">✨ AI Summary</th>
                                <th class="px-6 py-4">Actions</th>
                            </tr>
                        </thead>
                        <tbody id="full-patients-list" class="divide-y divide-slate-100"></tbody>
                    </table>
                </div>
            </section>

            <!-- Appointments Section -->
            <section id="section-appointments" class="hidden space-y-6">
                <div class="flex items-center justify-between">
                    <h3 class="text-2xl font-bold text-slate-800">Appointment Management</h3>
                    <button onclick="openModal('appointmentModal')" class="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center gap-2">
                        <i class="fas fa-calendar-plus"></i> Schedule New
                    </button>
                </div>
                <div id="appointments-master-list" class="space-y-4"></div>
            </section>

            <!-- Billing Section -->
            <section id="section-billing" class="hidden space-y-6">
                 <h3 class="text-2xl font-bold text-slate-800">Financial Overview</h3>
                 <div class="bg-white rounded-xl border border-slate-200 shadow-sm overflow-hidden">
                    <table class="w-full text-left">
                        <thead class="bg-slate-50 text-slate-500 text-xs uppercase">
                            <tr>
                                <th class="px-6 py-4">Invoice #</th>
                                <th class="px-6 py-4">Patient Name</th>
                                <th class="px-6 py-4">Date</th>
                                <th class="px-6 py-4">Amount</th>
                                <th class="px-6 py-4">Status</th>
                            </tr>
                        </thead>
                        <tbody id="billing-list" class="divide-y divide-slate-100"></tbody>
                    </table>
                </div>
            </section>

            <!-- Doctors Section -->
            <section id="section-doctors" class="hidden space-y-6">
                 <h3 class="text-2xl font-bold text-slate-800">Medical Staff</h3>
                 <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="doctors-list"></div>
            </section>

        </div>
    </main>

    <!-- Modal: New Patient -->
    <div id="patientModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50 hidden opacity-0 transition-opacity">
        <div class="bg-white rounded-2xl w-full max-w-md p-8 shadow-2xl m-4">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold text-slate-800">Add New Patient</h3>
                <button onclick="closeModal('patientModal')" class="text-slate-400 hover:text-slate-600"><i class="fas fa-times"></i></button>
            </div>
            <form id="patientForm" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-slate-600 mb-1">Full Name</label>
                    <input type="text" name="name" required class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">Age</label>
                        <input type="number" name="age" required class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">Gender</label>
                        <select name="gender" class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                            <option>Male</option><option>Female</option><option>Other</option>
                        </select>
                    </div>
                </div>
                <div>
                    <label class="block text-sm font-medium text-slate-600 mb-1">Phone Number</label>
                    <input type="tel" name="phone" required class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                </div>
                <div>
                    <label class="block text-sm font-medium text-slate-600 mb-1">Medical Note</label>
                    <textarea name="notes" rows="3" class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none"></textarea>
                </div>
                <button type="submit" class="w-full bg-blue-600 text-white py-3 rounded-lg font-bold hover:bg-blue-700 shadow-lg">Register Patient</button>
            </form>
        </div>
    </div>

    <!-- Modal: Appointment -->
    <div id="appointmentModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50 hidden opacity-0 transition-opacity">
        <div class="bg-white rounded-2xl w-full max-w-md p-8 shadow-2xl m-4">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold text-slate-800">Schedule Appointment</h3>
                <button onclick="closeModal('appointmentModal')" class="text-slate-400 hover:text-slate-600"><i class="fas fa-times"></i></button>
            </div>
            <form id="appointmentForm" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-slate-600 mb-1">Patient Name</label>
                    <input type="text" name="patientName" required class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                </div>
                <div>
                    <label class="block text-sm font-medium text-slate-600 mb-1">Doctor</label>
                    <select name="doctor" class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                        <option>Dr. Sarah Wilson</option>
                        <option>Dr. James Miller</option>
                        <option>Dr. Emily Chen</option>
                    </select>
                </div>
                <div class="grid grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">Time</label>
                        <input type="time" name="time" required class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-slate-600 mb-1">Date</label>
                        <input type="date" name="date" required class="w-full px-4 py-2 border border-slate-200 rounded-lg outline-none">
                    </div>
                </div>
                <button type="submit" class="w-full bg-blue-600 text-white py-3 rounded-lg font-bold hover:bg-blue-700 shadow-lg">Schedule</button>
            </form>
        </div>
    </div>

    <!-- Alert Toast -->
    <div id="toast" class="fixed bottom-8 right-8 bg-slate-800 text-white px-6 py-3 rounded-xl shadow-2xl transform translate-y-24 transition-transform duration-300 flex items-center gap-3 z-[100]">
        <i id="toast-icon" class="fas fa-check-circle text-green-400"></i>
        <span id="toast-message">Action successful!</span>
    </div>

    <!-- Summary Modal -->
    <div id="summaryModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50 hidden opacity-0 transition-opacity">
        <div class="bg-white rounded-2xl w-full max-w-lg p-8 shadow-2xl m-4">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-xl font-bold text-slate-800 flex items-center gap-2">✨ AI Note Summary</h3>
                <button onclick="closeModal('summaryModal')" class="text-slate-400 hover:text-slate-600"><i class="fas fa-times"></i></button>
            </div>
            <div id="summary-content" class="text-slate-600 text-sm leading-relaxed p-4 bg-blue-50/50 rounded-xl border border-blue-100">
                Processing...
            </div>
            <button onclick="closeModal('summaryModal')" class="mt-6 w-full bg-slate-100 py-2 rounded-lg font-semibold text-slate-700 hover:bg-slate-200">Close</button>
        </div>
    </div>

    <!-- Firebase SDK -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInWithCustomToken, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc, collection, query, onSnapshot, addDoc, deleteDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // CONFIG
        const apiKey = ""; // Gemini Key (empty string as requested)
        const GEMINI_API_URL = "https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent";
        
        const firebaseConfig = JSON.parse(__firebase_config);
        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const db = getFirestore(app);
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

        let currentUser = null;
        let patients = [];
        let appointments = [];

        // INITIALIZE AUTH (Rule 3)
        const initAuth = async () => {
            try {
                if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                    await signInWithCustomToken(auth, __initial_auth_token);
                } else {
                    await signInAnonymously(auth);
                }
            } catch (err) {
                console.error("Auth Error", err);
            }
        };
        initAuth();

        onAuthStateChanged(auth, (user) => {
            if (user) {
                currentUser = user;
                document.getElementById('user-avatar').innerText = user.uid.substring(0, 2).toUpperCase();
                document.getElementById('user-name').innerText = "Hospital Staff";
                document.getElementById('user-id-display').innerText = user.uid;
                setupFirestoreListeners();
            }
        });

        // FIRESTORE LISTENERS (Rule 1 & 2)
        function setupFirestoreListeners() {
            if (!currentUser) return;

            // Patients Collection
            const patientsCol = collection(db, 'artifacts', appId, 'public', 'data', 'patients');
            onSnapshot(patientsCol, (snapshot) => {
                patients = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                renderData();
            }, (err) => console.error("Patients Sync Error", err));

            // Appointments Collection
            const apptsCol = collection(db, 'artifacts', appId, 'public', 'data', 'appointments');
            onSnapshot(apptsCol, (snapshot) => {
                appointments = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                renderData();
            }, (err) => console.error("Appts Sync Error", err));
        }

        // DATABASE OPERATIONS
        window.addPatientToDB = async (data) => {
            if (!currentUser) return;
            try {
                const col = collection(db, 'artifacts', appId, 'public', 'data', 'patients');
                await addDoc(col, { ...data, createdAt: new Date().toISOString() });
                showToast("Patient saved to Database");
            } catch (err) {
                showToast("DB Save Error", "error");
            }
        };

        window.deletePatientFromDB = async (id) => {
            if (!currentUser) return;
            try {
                const docRef = doc(db, 'artifacts', appId, 'public', 'data', 'patients', id);
                await deleteDoc(docRef);
                showToast("Record deleted from DB");
            } catch (err) {
                showToast("Delete Error", "error");
            }
        };

        window.addAppointmentToDB = async (data) => {
             if (!currentUser) return;
             const col = collection(db, 'artifacts', appId, 'public', 'data', 'appointments');
             await addDoc(col, { ...data, status: 'Scheduled' });
             showToast("Appointment Scheduled");
        };

        // GEMINI AI LOGIC
        async function callGemini(prompt, systemInstruction = "") {
            const payload = {
                contents: [{ parts: [{ text: prompt }] }],
                systemInstruction: systemInstruction ? { parts: [{ text: systemInstruction }] } : undefined
            };

            for (let i = 0; i < 5; i++) {
                try {
                    const response = await fetch(`${GEMINI_API_URL}?key=${apiKey}`, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    if (!response.ok) throw new Error('API request failed');
                    const result = await response.json();
                    return result.candidates?.[0]?.content?.parts?.[0]?.text;
                } catch (error) {
                    if (i === 4) throw error;
                    await new Promise(r => setTimeout(r, Math.pow(2, i) * 1000));
                }
            }
        }

        window.askAIAssistant = async () => {
            const queryText = document.getElementById('ai-input').value;
            if (!queryText.trim()) return showToast('Please enter a query', 'error');

            const container = document.getElementById('ai-result-container');
            const loading = document.getElementById('ai-loading');
            const content = document.getElementById('ai-content');

            container.classList.remove('hidden');
            loading.classList.remove('hidden');
            content.classList.add('hidden');

            const sysPrompt = "You are a senior medical consultant. Provide brief analysis of symptoms and suggest precautions.";
            try {
                const res = await callGemini(queryText, sysPrompt);
                content.innerHTML = res.replace(/\n/g, '<br>');
                loading.classList.add('hidden');
                content.classList.remove('hidden');
            } catch (e) { showToast("AI Error", "error"); }
        };

        window.summarizePatientNote = async (patientId) => {
            const patient = patients.find(p => p.id === patientId);
            openModal('summaryModal');
            const contentEl = document.getElementById('summary-content');
            contentEl.innerHTML = '✨ Reading...';
            try {
                const res = await callGemini(`Summarize this patient note: ${patient.notes}`, "Summarize in 3 short points.");
                contentEl.innerHTML = res.replace(/\n/g, '<br>');
            } catch (e) { contentEl.innerHTML = "Error."; }
        };

        // UI HELPERS
        window.showSection = (sectionId) => {
            const sections = ['dashboard', 'patients', 'ai-assistant', 'appointments', 'billing', 'doctors'];
            sections.forEach(s => {
                document.getElementById(`section-${s}`).classList.add('hidden');
                document.getElementById(`nav-${s}`).classList.remove('active');
            });
            document.getElementById(`section-${sectionId}`).classList.remove('hidden');
            document.getElementById(`nav-${sectionId}`).classList.add('active');
            renderData();
        };

        window.openModal = (id) => {
            const el = document.getElementById(id);
            el.classList.remove('hidden');
            setTimeout(() => el.classList.remove('opacity-0'), 10);
        };

        window.closeModal = (id) => {
            const el = document.getElementById(id);
            el.classList.add('opacity-0');
            setTimeout(() => el.classList.add('hidden'), 250);
        };

        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            document.getElementById('toast-message').innerText = message;
            toast.classList.remove('translate-y-24');
            setTimeout(() => toast.classList.add('translate-y-24'), 3000);
        }

        function renderData() {
            document.getElementById('stat-patients').innerText = patients.length;
            document.getElementById('stat-appointments').innerText = appointments.length;

            const patientBody = document.getElementById('full-patients-list');
            patientBody.innerHTML = patients.map(p => `
                <tr>
                    <td class="px-6 py-4 font-bold">${p.name}</td>
                    <td class="px-6 py-4 text-xs font-mono">${p.id.substring(0,8)}</td>
                    <td class="px-6 py-4"><span class="px-2 py-1 rounded-full text-[10px] bg-blue-100">${p.status || 'Outpatient'}</span></td>
                    <td class="px-6 py-4"><button onclick="summarizePatientNote('${p.id}')" class="text-xs text-blue-600">✨ Summarize</button></td>
                    <td class="px-6 py-4"><button onclick="deletePatientFromDB('${p.id}')" class="text-red-500"><i class="fas fa-trash"></i></button></td>
                </tr>
            `).join('');

            const apptBody = document.getElementById('appointments-master-list');
            apptBody.innerHTML = appointments.map(a => `
                <div class="p-4 bg-white border rounded-xl flex justify-between items-center">
                    <div><h5 class="font-bold">${a.patientName}</h5><p class="text-xs text-slate-500">${a.doctor} • ${a.time}</p></div>
                    <span class="text-[10px] px-2 py-1 bg-slate-100 rounded-full">${a.status}</span>
                </div>
            `).join('');

            document.getElementById('recent-patients-list').innerHTML = patients.slice(-3).map(p => `
                <tr><td class="px-6 py-3">${p.name}</td><td class="px-6 py-3 text-xs">${p.id.substring(0,6)}</td><td class="px-6 py-3 text-xs">${p.status || 'Active'}</td></tr>
            `).join('');
        }

        document.getElementById('patientForm').onsubmit = function(e) {
            e.preventDefault();
            const fd = new FormData(this);
            addPatientToDB({
                name: fd.get('name'),
                age: fd.get('age'),
                gender: fd.get('gender'),
                notes: fd.get('notes')
            });
            this.reset(); closeModal('patientModal');
        };

        document.getElementById('appointmentForm').onsubmit = function(e) {
            e.preventDefault();
            const fd = new FormData(this);
            addAppointmentToDB({
                patientName: fd.get('patientName'),
                doctor: fd.get('doctor'),
                time: fd.get('time'),
                date: fd.get('date')
            });
            this.reset(); closeModal('appointmentModal');
        };

    </script>
</body>
</html>

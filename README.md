
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Account | Green Energy</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
        .tier-card { transition: all 0.3s ease; }
        .tier-card:hover { transform: translateY(-5px); }
    </style>
</head>
<body class="bg-slate-50 pb-32">

    <div class="max-w-lg mx-auto p-6">
        <h1 class="text-3xl font-black text-slate-800 mb-6">Profile</h1>

        <div class="bg-slate-900 rounded-[2.5rem] p-8 text-white shadow-xl mb-6 relative overflow-hidden">
            <div class="relative z-10">
                <div class="flex justify-between items-start">
                    <div>
                        <p class="text-emerald-400 text-[10px] font-bold uppercase tracking-widest opacity-80">Available Balance</p>
                        <h2 id="acc_balance" class="text-4xl font-black mt-1">₦0.00</h2>
                        
                        <p class="text-slate-400 text-[10px] font-bold uppercase mt-4 tracking-widest">Total Income</p>
                        <p id="total_income" class="text-lg font-black text-emerald-400">₦0.00</p>
                    </div>
                    <div class="text-right">
                        <span id="current_tier_badge" class="bg-emerald-500 text-[10px] font-black px-3 py-1 rounded-full uppercase tracking-tighter">Tier 1</span>
                        <button onclick="openTierModal()" class="block mt-4 bg-white/10 hover:bg-white/20 text-white text-[9px] font-black uppercase px-4 py-2 rounded-xl transition-all border border-white/10">
                            Upgrade Tier
                        </button>
                    </div>
                </div>
            </div>
            <div class="absolute -bottom-10 -right-10 w-32 h-32 bg-emerald-500/10 rounded-full blur-3xl"></div>
        </div>
<div class="grid grid-cols-2 gap-3 mb-8">
            <button onclick="showSection('products')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-blue-50 rounded-2xl flex items-center justify-center text-blue-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">My Products</span>
            </button>
            <button onclick="showSection('deposits')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-emerald-50 rounded-2xl flex items-center justify-center text-emerald-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">Deposit History</span>
            </button>
            <button onclick="showSection('withdrawals')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-amber-50 rounded-2xl flex items-center justify-center text-amber-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">Withdrawals</span>
            </button>
            <button onclick="showSection('team')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-purple-50 rounded-2xl flex items-center justify-center7 text-purple-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">My Team</span>
            </button>
        </div>

        <div id="section_container" class="space-y-4">
            </div>

        <button onclick="logout()" class="w-full mt-10 text-slate-400 text-[10px] font-black uppercase tracking-widest hover:text-red-500 transition-all">
            Sign Out Account
        </button>
    </div>

    <div id="tier_modal" class="fixed inset-0 bg-slate-900/90 backdrop-blur-md z-[1000] hidden overflow-y-auto p-6">
        <div class="max-w-md mx-auto">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-white font-black text-xl uppercase italic">Select Tier</h3>
                <button onclick="closeTierModal()" class="text-white/50 hover:text-white">
                    <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            <div id="tier_list" class="space-y-4 pb-20">
                </div>
        </div>
    </div>
<div class="grid grid-cols-2 gap-3 mb-8">
            <button onclick="showSection('products')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-blue-50 rounded-2xl flex items-center justify-center text-blue-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">My Products</span>
            </button>
            <button onclick="showSection('deposits')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-emerald-50 rounded-2xl flex items-center justify-center text-emerald-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">Deposit History</span>
            </button>
            <button onclick="showSection('withdrawals')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-amber-50 rounded-2xl flex items-center justify-center text-amber-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 9V7a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2m2 4h10a2 2 0 002-2v-6a2 2 0 00-2-2H9a2 2 0 00-2 2v6a2 2 0 002 2zm7-5a2 2 0 11-4 0 2 2 0 014 0z"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">Withdrawals</span>
            </button>
            <button onclick="showSection('team')" class="bg-white p-4 rounded-3xl border border-slate-100 shadow-sm flex flex-col items-center gap-2 hover:bg-slate-50 transition-all">
                <div class="w-10 h-10 bg-purple-50 rounded-2xl flex items-center justify-center text-purple-500">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z"></path></svg>
                </div>
                <span class="text-[10px] font-black uppercase text-slate-600">My Team</span>
            </button>
        </div>

        <div id="section_container" class="space-y-4">
            </div>

        <button onclick="logout()" class="w-full mt-10 text-slate-400 text-[10px] font-black uppercase tracking-widest hover:text-red-500 transition-all">
            Sign Out Account
        </button>
    </div>

    <div id="tier_modal" class="fixed inset-0 bg-slate-900/90 backdrop-blur-md z-[1000] hidden overflow-y-auto p-6">
        <div class="max-w-md mx-auto">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-white font-black text-xl uppercase italic">Select Tier</h3>
                <button onclick="closeTierModal()" class="text-white/50 hover:text-white">
                    <svg class="w-8 h-8" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>
                </button>
            </div>
            <div id="tier_list" class="space-y-4 pb-20">
                </div>
        </div>
    </div>
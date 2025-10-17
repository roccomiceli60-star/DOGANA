<!DOCTYPE html>
<html lang="it"><head>
<meta charset="utf-8"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Calcolo Dazi Doganali - Light</title>
<link crossorigin="" href="https://fonts.gstatic.com" rel="preconnect"/>
<link as="style" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&amp;display=swap" onload="this.rel='stylesheet'" rel="stylesheet"/>
<script src="https://cdn.tailwindcss.com?plugins=forms,container-queries"></script>
<link href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200" rel="stylesheet"/>
<link href="data:image/x-icon;base64," rel="icon" type="image/x-icon"/>
<script>
    tailwind.config = {
        darkMode: "class",
        theme: {
            extend: {
                colors: {
                    "background-light": "#f7f8fa",
                    "background-dark": "#121212",
                    "surface-light": "#ffffff",
                    "surface-dark": "#1e1e1e",
                    "primary-light": "#3b82f6",
                    "primary-dark": "#60a5fa",
                    "text-light": "#1f2937",
                    "text-dark": "#f9fafb",
                    "text-secondary-light": "#6b7280",
                    "text-secondary-dark": "#9ca3af",
                    "border-light": "#e5e7eb",
                    "border-dark": "#374151",
                },
                fontFamily: {
                    sans: ["Inter", "sans-serif"],
                },
                borderRadius: {
                    "xl": "1rem",
                    "2xl": "1.5rem",
                },
            },
        },
    };
    // Funzione per cambiare tema
    function toggleTheme() {
        const isDarkMode = document.documentElement.classList.toggle('dark');
        localStorage.setItem('theme', isDarkMode ? 'dark' : 'light');
        updateThemeIcon(isDarkMode);
    }

    function updateThemeIcon(isDarkMode) {
        const themeIcon = document.querySelector('.material-symbols-outlined');
        if (isDarkMode) {
            themeIcon.textContent = 'light_mode';
        } else {
            themeIcon.textContent = 'dark_mode';
        }
    }

    // Applica il tema salvato al caricamento della pagina
    document.addEventListener('DOMContentLoaded', () => {
        const savedTheme = localStorage.getItem('theme') || 'light';
        const isDarkMode = savedTheme === 'dark';
        if (isDarkMode) {
            document.documentElement.classList.add('dark');
        }
        updateThemeIcon(isDarkMode);
    });
</script>
<style>
    body {
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }
    .material-symbols-outlined {
        font-variation-settings: 'FILL' 0, 'wght' 300, 'GRAD' 0, 'opsz' 24;
    }
</style>
  </head>
<body class="font-sans bg-background-light text-text-light dark:bg-background-dark h-screen overflow-hidden">
<div class="relative flex h-full w-full flex-col group/design-root dark:text-text-dark">
<main class="flex-grow p-4 flex flex-col justify-between">
<div class="flex justify-between items-center mb-4">
    <h1 class="text-xl font-bold">Calcolo Dazi</h1>
    <button class="flex items-center justify-center rounded-full h-9 w-9 text-text-light dark:text-text-dark" onclick="toggleTheme()">
        <span class="material-symbols-outlined text-base">dark_mode</span>
    </button>
</div>
<div class="bg-surface-light dark:bg-surface-dark p-3 rounded-xl space-y-2 border border-border-light dark:border-border-dark text-center">
<p class="text-text-secondary-light dark:text-text-secondary-dark text-sm font-medium">Totale da pagare</p>
<p id="total-to-pay" class="text-primary-light dark:text-primary-dark text-4xl font-extrabold">€7.00</p>
</div>
<div class="grid grid-cols-2 gap-3">
<div class="relative">
<span class="material-symbols-outlined absolute left-3 top-1/2 -translate-y-1/2 text-text-secondary-light dark:text-text-secondary-dark text-lg">shopping_bag</span>
<input class="w-full rounded-lg border border-border-light dark:border-border-dark bg-surface-light dark:bg-surface-dark placeholder-text-secondary-light dark:placeholder-text-secondary-dark focus:ring-2 focus:ring-primary-light dark:focus:ring-primary-dark focus:border-primary-light dark:focus:border-primary-dark h-12 pl-10 pr-3 text-base" id="itemValue" placeholder="Valore" type="text"/>
</div>
<div class="relative">
<span class="material-symbols-outlined absolute left-3 top-1/2 -translate-y-1/2 text-text-secondary-light dark:text-text-secondary-dark text-lg">local_shipping</span>
<input class="w-full rounded-lg border border-border-light dark:border-border-dark bg-surface-light dark:bg-surface-dark placeholder-text-secondary-light dark:placeholder-text-secondary-dark focus:ring-2 focus:ring-primary-light dark:focus:ring-primary-dark focus:border-primary-light dark:focus:border-primary-dark h-12 pl-10 pr-3 text-base" id="shippingCost" placeholder="Spedizione" type="text"/>
</div>
</div>
<div class="bg-surface-light dark:bg-surface-dark p-3 rounded-xl space-y-2 border border-border-light dark:border-border-dark">
<h2 class="text-base font-semibold text-text-light dark:text-text-dark">Riepilogo Costi</h2>
<div class="space-y-1 text-sm">
<div class="flex justify-between items-center">
<p class="text-text-secondary-light dark:text-text-secondary-dark">IVA (22%)</p>
<p id="iva-amount" class="font-medium text-text-light dark:text-text-dark">€0.00</p>
</div>
<div class="flex justify-between items-center">
<p class="text-text-secondary-light dark:text-text-secondary-dark">Dazi (2.7% se > 150€)</p>
<p id="dazi-amount" class="font-medium text-text-light dark:text-text-dark">€0.00</p>
</div>
<div class="flex justify-between items-center">
<div class="flex items-center gap-1">
<p class="text-text-secondary-light dark:text-text-secondary-dark">Oneri del vettore</p>
</div>
<p id="oneri-amount" class="font-medium text-text-light dark:text-text-dark">€7.00</p>
</div>
<hr class="border-border-light dark:border-border-dark my-2"/>
<div class="flex justify-between items-center font-bold">
    <p class="text-text-light dark:text-text-dark">Totale finale</p>
    <p id="grand-total" class="text-primary-light dark:text-primary-dark text-lg">€0.00</p>
</div>
</div>
</div>
<div class="bg-surface-light dark:bg-surface-dark p-3 rounded-xl border border-border-light dark:border-border-dark">
<h2 class="text-sm font-semibold text-text-light dark:text-text-dark mb-1">Soglie attuali</h2>
<ul class="space-y-0.5 text-xs text-text-secondary-light dark:text-text-secondary-dark list-disc list-inside">
<li><span class="font-semibold text-text-light dark:text-text-dark">Fino a 22€:</span> IVA 22% + Oneri 3€</li>
<li><span class="font-semibold text-text-light dark:text-text-dark">Da 22,01€ a 150€:</span> IVA 22% + Oneri 7€</li>
<li><span class="font-semibold text-text-light dark:text-text-dark">Da 150,01€ a 1000€:</span> Dazio 2,7% + IVA 22% + Oneri 7€</li>
<li><span class="font-semibold text-text-light dark:text-text-dark">Oltre 1000€:</span> Dazio 2,7% + IVA 22% + Oneri 21€</li>
</ul>
</div>
</main>
</div>
<script>
    function calculateDuties() {
        const itemValue = parseFloat(document.getElementById('itemValue').value) || 0;
        const shippingCost = parseFloat(document.getElementById('shippingCost').value) || 0;

        const totalValue = itemValue + shippingCost;

        let iva = 0;
        let dazi = 0;
        let oneriVettore = 0;

        if (totalValue > 0 && totalValue <= 22) {
            oneriVettore = 3.00;
            iva = totalValue * 0.22;
        } else if (totalValue > 22 && totalValue <= 150) {
            oneriVettore = 7.00;
            iva = totalValue * 0.22;
        } else if (totalValue > 150 && totalValue <= 1000) {
            oneriVettore = 7.00;
            dazi = totalValue * 0.027;
            iva = (totalValue + dazi) * 0.22;
        } else if (totalValue > 1000) {
            oneriVettore = 21.00;
            dazi = totalValue * 0.027;
            iva = (totalValue + dazi) * 0.22;
        }

        const totalToPay = iva + dazi + oneriVettore;
        const grandTotal = itemValue + shippingCost + totalToPay;

        // Update UI
        document.getElementById('total-to-pay').textContent = `€${totalToPay.toFixed(2)}`;
        document.getElementById('iva-amount').textContent = `€${iva.toFixed(2)}`;
        document.getElementById('dazi-amount').textContent = `€${dazi.toFixed(2)}`;
        document.getElementById('oneri-amount').textContent = `€${oneriVettore.toFixed(2)}`;
        document.getElementById('grand-total').textContent = `€${grandTotal.toFixed(2)}`;
    }

    document.getElementById('itemValue').addEventListener('input', calculateDuties);
    document.getElementById('shippingCost').addEventListener('input', calculateDuties);

    // Initial calculation on page load
    calculateDuties();
</script>
</body></html>

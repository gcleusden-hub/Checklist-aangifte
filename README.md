<!DOCTYPE html>
<html lang="nl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beoordelingsformulier Gesprek Aangifte</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.2);
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        header h1 {
            font-size: 28px;
            margin-bottom: 10px;
        }
        
        .progress-container {
            background: white;
            padding: 20px 30px;
            border-bottom: 2px solid #f0f0f0;
        }
        
        .progress-bar-bg {
            width: 100%;
            height: 30px;
            background: #e0e0e0;
            border-radius: 15px;
            overflow: hidden;
            position: relative;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            width: 0%;
            transition: width 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 14px;
        }
        
        .progress-text {
            margin-top: 10px;
            text-align: center;
            color: #555;
            font-size: 14px;
        }
        
        main {
            padding: 30px;
        }
        
        .category {
            margin-bottom: 30px;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            overflow: hidden;
        }
        
        .category-header {
            background: #f8f9fa;
            padding: 15px 20px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: background 0.2s;
        }
        
        .category-header:hover {
            background: #e9ecef;
        }
        
        .category-header h2 {
            color: #2a5298;
            font-size: 20px;
        }
        
        .category-toggle {
            font-size: 24px;
            color: #666;
            transition: transform 0.3s;
        }
        
        .category-toggle.open {
            transform: rotate(180deg);
        }
        
        .category-content {
            padding: 20px;
            display: none;
        }
        
        .category-content.open {
            display: block;
        }
        
        .criterion {
            display: flex;
            align-items: flex-start;
            padding: 15px;
            margin-bottom: 10px;
            background: #f8f9fa;
            border-radius: 5px;
            transition: all 0.2s;
        }
        
        .criterion:hover {
            background: #e9ecef;
        }
        
        .criterion.checked {
            background: #d4edda;
            border-left: 4px solid #28a745;
        }
        
        .criterion input[type="checkbox"] {
            width: 20px;
            height: 20px;
            margin-right: 15px;
            cursor: pointer;
            flex-shrink: 0;
            margin-top: 2px;
        }
        
        .criterion label {
            cursor: pointer;
            flex: 1;
            line-height: 1.6;
            color: #333;
        }
        
        .criterion label ul {
            margin-top: 8px;
            margin-left: 20px;
        }
        
        .criterion label li {
            margin-bottom: 5px;
            color: #555;
        }
        
        .buttons-container {
            display: flex;
            gap: 10px;
            justify-content: center;
            padding: 20px;
            border-top: 2px solid #f0f0f0;
        }
        
        button {
            padding: 12px 30px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 600;
        }
        
        .btn-reset {
            background: #dc3545;
            color: white;
        }
        
        .btn-reset:hover {
            background: #c82333;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        
        .btn-export {
            background: #28a745;
            color: white;
        }
        
        .btn-export:hover {
            background: #218838;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        
        .btn-print {
            background: #007bff;
            color: white;
        }
        
        .btn-print:hover {
            background: #0056b3;
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }
        
        @media print {
            body {
                background: white;
                padding: 0;
            }
            
            .container {
                box-shadow: none;
            }
            
            .buttons-container {
                display: none;
            }
            
            .category-content {
                display: block !important;
            }
            
            .category-toggle {
                display: none;
            }
        }
        
        @media (max-width: 768px) {
            header h1 {
                font-size: 22px;
            }
            
            main {
                padding: 20px;
            }
            
            .buttons-container {
                flex-direction: column;
            }
            
            button {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>📋 Beoordelingsformulier Gesprek Aangifte</h1>
            <p>Klik op de criteria die je hebt behaald</p>
        </header>
        
        <div class="progress-container">
            <div class="progress-bar-bg">
                <div class="progress-bar" id="progressBar">0%</div>
            </div>
            <div class="progress-text" id="progressText">0 van 37 criteria behaald</div>
        </div>
        
        <main>
            <!-- 1.1 Contact maken -->
            <div class="category">
                <div class="category-header" onclick="toggleCategory(this)">
                    <h2>1.1 Contact maken</h2>
                    <span class="category-toggle">▼</span>
                </div>
                <div class="category-content open">
                    <div class="criterion">
                        <input type="checkbox" id="c1" onchange="updateProgress()">
                        <label for="c1">Contact maken waardoor klant zich op zijn gemak voelt; empathie en reflecteren</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c2" onchange="updateProgress()">
                        <label for="c2">Vragen naar het doel van de klant, uitleg consequenties van het doen van aangifte, open staan voor bemiddeling (kan ook bij afronding)</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c3" onchange="updateProgress()">
                        <label for="c3">Uitleg over de aanwijzing slachtofferzorg, rechten als slachtoffer vertellen, uitreiken of bespreken aangiftefolder</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c4" onchange="updateProgress()">
                        <label for="c4">Vragen naar en beoordelen van beschermingsbehoefte en kwetsbaarheid als slachtoffer. Uitleg mogelijkheid domicilie / bijstaan familielid of advocaat</label>
                    </div>
                </div>
            </div>
            
            <!-- 1.2 Informatie verzamelen -->
            <div class="category">
                <div class="category-header" onclick="toggleCategory(this)">
                    <h2>1.2 Informatie verzamelen</h2>
                    <span class="category-toggle">▼</span>
                </div>
                <div class="category-content">
                    <div class="criterion">
                        <input type="checkbox" id="c5" onchange="updateProgress()">
                        <label for="c5">Laat de klant zijn verhaal vertellen</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c6" onchange="updateProgress()">
                        <label for="c6">Verzamelt algemene informatie door de juiste vragen te stellen: verzamelt zaakgerichte informatie (o.a. 7W's)
                            <ul>
                                <li>Wat</li>
                                <li>Wanneer</li>
                                <li>Waar</li>
                                <li>Wie</li>
                                <li>Waarom</li>
                                <li>Hoe / Welke wijze</li>
                                <li>Waarmee</li>
                            </ul>
                            Stellen van open vragen zonder suggestie
                        </label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c7" onchange="updateProgress()">
                        <label for="c7">Luistert aandachtig</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c8" onchange="updateProgress()">
                        <label for="c8">Vraagt door</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c9" onchange="updateProgress()">
                        <label for="c9">Vat samen tussendoor of parafraseert</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c10" onchange="updateProgress()">
                        <label for="c10">Komt tot een probleem definitie</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c11" onchange="updateProgress()">
                        <label for="c11">Reflecteert op het gevoel van de klant</label>
                    </div>
                </div>
            </div>
            
            <!-- 1.3 Probleem aanpakken -->
            <div class="category">
                <div class="category-header" onclick="toggleCategory(this)">
                    <h2>1.3 Probleem aanpakken</h2>
                    <span class="category-toggle">▼</span>
                </div>
                <div class="category-content">
                    <div class="criterion">
                        <input type="checkbox" id="c12" onchange="updateProgress()">
                        <label for="c12">Legt de consequenties van het doen van aangifte uit en informatie over verder verloop</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c13" onchange="updateProgress()">
                        <label for="c13">Noteren van personalia van de betrokken partijen
                            <ul>
                                <li>Aangever</li>
                                <li>Info Getuigen</li>
                                <li>Info Verdachten</li>
                                <li>Inclusief telefoon en emailadres</li>
                            </ul>
                        </label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c14" onchange="updateProgress()">
                        <label for="c14">Plaats, de dag en datum, tijdstip(pen)</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c15" onchange="updateProgress()">
                        <label for="c15">Juiste artikel en strafbare feit vaststellen</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c16" onchange="updateProgress()">
                        <label for="c16">Situatieschets laten maken</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c17" onchange="updateProgress()">
                        <label for="c17">Elementen en bestanddelen van het artikel + causaal verband leggen
                            <ul>
                                <li>Goederen</li>
                                <li>Eigenaar</li>
                                <li>Toestemming</li>
                                <li>Schade</li>
                                <li>Pijn/letsel</li>
                                <li>Opzet</li>
                                <li>Nacht, woning, erf woning, buiten medeweten/wil rechthebbende</li>
                                <li>Braak, inklimmen, valse sleutel</li>
                                <li>Enz</li>
                            </ul>
                        </label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c18" onchange="updateProgress()">
                        <label for="c18">Vragen naar redenen van wetenschap</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c19" onchange="updateProgress()">
                        <label for="c19">Noteert relevante typische daderwetenschappen zoals decor en bijzonderheden</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c20" onchange="updateProgress()">
                        <label for="c20">Waarnemingsomstandigheden
                            <ul>
                                <li>Afstand / vrij zicht?</li>
                                <li>Weer</li>
                                <li>Verlichting</li>
                                <li>Hoe lang gezien</li>
                                <li>Hoe voelde u zich / gezichtsvermogen</li>
                            </ul>
                        </label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c21" onchange="updateProgress()">
                        <label for="c21">Sporen op de PD - omschrijf gedetailleerd</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c22" onchange="updateProgress()">
                        <label for="c22">Zijn er getuigen of camerabeelden?</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c23" onchange="updateProgress()">
                        <label for="c23">Signalementen / eigen signalement aangever</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c24" onchange="updateProgress()">
                        <label for="c24">Schade/letsel en omschrijving hiervan (goederen)</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c25" onchange="updateProgress()">
                        <label for="c25">Waarde van de schade/het goed zo concreet mogelijk. Heeft aangever aankoopbewijzen/bonnen? Is de aangever verzekerd?</label>
                    </div>
                </div>
            </div>
            
            <!-- 1.4 Gesprek afronden -->
            <div class="category">
                <div class="category-header" onclick="toggleCategory(this)">
                    <h2>1.4 Gesprek afronden</h2>
                    <span class="category-toggle">▼</span>
                </div>
                <div class="category-content">
                    <div class="criterion">
                        <input type="checkbox" id="c26" onchange="updateProgress()">
                        <label for="c26">Informeert over wat er verder gebeurd met de aangifte (info doen valse aangifte strafbaar als hiertoe aanleiding is; niet standaard)</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c27" onchange="updateProgress()">
                        <label for="c27">Vat de gehele aangifte samen</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c28" onchange="updateProgress()">
                        <label for="c28">Laten ondertekenen of afspraak maken om te ondertekenen</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c29" onchange="updateProgress()">
                        <label for="c29">Vraagt aan de aangever of deze verder nog vragen heeft</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c30" onchange="updateProgress()">
                        <label for="c30">Schadevergoeding gewenst en uitleg voegen in het strafproces, eventueel civiele partij</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c31" onchange="updateProgress()">
                        <label for="c31">Slachtofferhulp herhalen en uitleg en vraag ja/nee</label>
                    </div>
                    <div class="criterion">
                        <input type="checkbox" id="c32" onchange="updateProgress()">
                        <label for="c32">Op de hoogte gehouden worden en hoe? Met uitleg DigiD</label>
                    </div>
                </div>
            </div>
            
            <!-- 1.5 Professioneel en integer handelen -->
            <div class="category">
                <div class="category-header" onclick="toggleCategory(this)">
                    <h2>1.5 Professioneel en integer handelen</h2>
                    <span class="category-toggle">▼</span>
                </div>
                <div class="category-content">
                    <div class="criterion">
                        <input type="checkbox" id="c33" onchange="updateProgress()">
                        <label for="c33">Conform waarden en missie Nationale Politie
                            <ul>
                                <li>Dienstverleningsconcept Nationale Politie</li>
                                <li>Kernwaarden: integer, betrouwbaar, moedig en verbindend</li>
                                <li>Rekening houden met verschillen tussen mensen</li>
                            </ul>
                        </label>
                    </div>
                </div>
            </div>
        </main>
        
        <div class="buttons-container">
            <button class="btn-reset" onclick="resetForm()">🔄 Reset alles</button>
            <button class="btn-export" onclick="exportResults()">💾 Download resultaten</button>
            <button class="btn-print" onclick="window.print()">🖨️ Print formulier</button>
        </div>
    </div>
    
    <script>
        // Totaal aantal criteria
        const TOTAL_CRITERIA = 33;
        
        // Toggle categorie open/dicht
        function toggleCategory(header) {
            const content = header.nextElementSibling;
            const toggle = header.querySelector('.category-toggle');
            
            content.classList.toggle('open');
            toggle.classList.toggle('open');
        }
        
        // Update voortgangsbalk
        function updateProgress() {
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            const checked = document.querySelectorAll('input[type="checkbox"]:checked');
            const percentage = Math.round((checked.length / TOTAL_CRITERIA) * 100);
            
            document.getElementById('progressBar').style.width = percentage + '%';
            document.getElementById('progressBar').textContent = percentage + '%';
            document.getElementById('progressText').textContent = `${checked.length} van ${TOTAL_CRITERIA} criteria behaald`;
            
            // Update visuele feedback per criterium
            checkboxes.forEach(checkbox => {
                const criterion = checkbox.parentElement;
                if (checkbox.checked) {
                    criterion.classList.add('checked');
                } else {
                    criterion.classList.remove('checked');
                }
            });
            
            // Sla voortgang op in localStorage
            saveProgress();
        }
        
        // Reset formulier
        function resetForm() {
            if (confirm('Weet je zeker dat je alle voortgang wilt wissen?')) {
                const checkboxes = document.querySelectorAll('input[type="checkbox"]');
                checkboxes.forEach(checkbox => {
                    checkbox.checked = false;
                });
                updateProgress();
                localStorage.removeItem('beoordelingsformulier');
            }
        }
        
        // Sla voortgang op
        function saveProgress() {
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            const state = {};
            checkboxes.forEach(checkbox => {
                state[checkbox.id] = checkbox.checked;
            });
            localStorage.setItem('beoordelingsformulier', JSON.stringify(state));
        }
        
        // Laad voortgang
        function loadProgress() {
            const saved = localStorage.getItem('beoordelingsformulier');
            if (saved) {
                const state = JSON.parse(saved);
                Object.keys(state).forEach(id => {
                    const checkbox = document.getElementById(id);
                    if (checkbox) {
                        checkbox.checked = state[id];
                    }
                });
                updateProgress();
            }
        }
        
        // Exporteer resultaten als tekst
        function exportResults() {
            const checkboxes = document.querySelectorAll('input[type="checkbox"]');
            const checked = document.querySelectorAll('input[type="checkbox"]:checked');
            
            let text = 'BEOORDELINGSFORMULIER GESPREK AANGIFTE\n';
            text += '========================================\n\n';
            text += `Behaalde criteria: ${checked.length} van ${TOTAL_CRITERIA} (${Math.round((checked.length / TOTAL_CRITERIA) * 100)}%)\n\n`;
            
            const categories = document.querySelectorAll('.category');
            categories.forEach(category => {
                const title = category.querySelector('h2').textContent;
                text += `\n${title}\n`;
                text += '-'.repeat(title.length) + '\n';
                
                const criteria = category.querySelectorAll('.criterion');
                criteria.forEach(criterion => {
                    const checkbox = criterion.querySelector('input[type="checkbox"]');
                    const label = criterion.querySelector('label').textContent.trim();
                    const status = checkbox.checked ? '✓' : '✗';
                    text += `${status} ${label}\n`;
                });
            });
            
            // Download als tekstbestand
            const blob = new Blob([text], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `beoordelingsformulier_${new Date().toISOString().split('T')[0]}.txt`;
            a.click();
            URL.revokeObjectURL(url);
        }
        
        // Laad opgeslagen voortgang bij laden pagina
        window.addEventListener('load', loadProgress);
    </script>
</body>
</html>

# Kalkulator wynagrodzenia netto we Włoszech

> Od brutto do netto we Włoszech w 2026 roku: składki pracownika, podatek dochodowy IRPEF z ulgami, dodatki regionalne i gminne dla Mediolanu, Rzymu, Turynu, Bolonii i Neapolu.


<section> <span class="eyebrow">Kalkulator netto</span> <h1 id="ile-twoj-pracownik-dostanie-na-reke-we-wloszech">Ile Twój pracownik dostanie na rękę we Włoszech</h1> <p class="lede">Podaj roczne wynagrodzenie brutto i miasto. Szacunek stosuje zasady z 2026 roku: składki pracownika, podatek dochodowy z ulgami dla pracowników i dodatki lokalne. Przydaje się, gdy kandydat porównuje ofertę z polską pensją „na rękę”.</p> </section> <section> <div class="grid"> <form class="panel" id="nf" style="display:grid;gap:16px"> <label for="g">Roczne wynagrodzenie brutto, RAL (EUR)<input id="g" type="number" min="10000" step="1000" value="50000"></label> <label for="city">Miasto<select id="city"><option value="Milan">Mediolan</option><option value="Rome">Rzym</option><option value="Turin">Turyn</option><option value="Bologna">Bolonia</option><option value="Naples">Neapol</option></select></label> <label for="inst">Wypłacane w<select id="inst"><option value="13">13 ratach</option><option value="14">14 ratach</option><option value="12">12 ratach (13./14. proporcjonalnie)</option></select></label> </form> <div class="panel" style="min-width:0"><div class="tbl"><table id="nt"><thead><tr><th>Pozycja</th><th class="num">Rocznie</th></tr></thead><tbody></tbody></table></div> <p id="nm" style="margin-bottom:0;font-weight:600"></p></div> </div>  </section> <section class="prose"> <h2 id="jak-dziala-obliczenie">Jak działa obliczenie</h2> <ol> <li>Pracownik płaci 9,19% składek od wynagrodzenia brutto, plus 1% od części powyżej 56 224 € rocznie.</li> <li>Podatek dochodowy (IRPEF) nalicza się od reszty: 23% do 28 000 €, 33% od 28 000 do 50 000 €, 43% powyżej.</li> <li>Ulgi dla pracowników obniżają podatek. Są największe przy niskich pensjach i spadają do zera przy 50 000 €. Między 20 000 a 40 000 € działa dodatkowa ulga do 1000 €.</li> <li>Doliczane są dodatki regionalny i gminny, chyba że dochód jest poniżej progu zwolnienia w danym mieście.</li> </ol> <p>Nic z tego nie zmienia Twojego kosztu jako pracodawcy: zobacz <a href="kalkulator-kosztow.html">kalkulator kosztów pracodawcy</a>.</p> </section> <script>(function(){const N = {"status":"secondary","source":"data/params/2026.yaml (irpef, inps, addizionali); TUIR art. 11 and 13; L. 207/2024; L. 199/2025","employee_inps":0.0919,"extra_1pct_above":56224,"irpef":[[28000,0.23],[50000,0.33],[null,0.43]],"cities":{"Milan":{"region":"Lombardia","regional":[[null,0.0123]],"municipal":0.008,"exempt":23000},"Rome":{"region":"Lacjum","regional":[[28000,0.0173],[null,0.0333]],"municipal":0.009,"exempt":14000},"Turin":{"region":"Piemont","regional":[[null,0.0162]],"municipal":0.008,"municipal_note":"0.8% to 1.2% by band; 0.8% used","exempt":11790},"Bologna":{"region":"Emilia-Romania","regional":[[null,0.0133]],"municipal":0.008,"exempt":15000},"Naples":{"region":"Kampania","regional":[[null,0.0173]],"municipal":0.01,"exempt":12000}}};

const eur = n => (n < 0 ? '−' : '') + Math.round(Math.abs(n)).toLocaleString('pl-PL') + ' €';
function bands(x, b){ let t = 0, lo = 0; for (const [hi, r] of b){ const top = hi ?? Infinity; if (x > lo) t += (Math.min(x, top) - lo) * r; lo = top; } return t; }
function credit(r){ if (r <= 15000) return 1955; if (r <= 28000) return 1910 + 1190 * (28000 - r) / 13000; if (r <= 50000) return 1910 * (50000 - r) / 22000 + (r > 25000 && r <= 35000 ? 65 : 0); return 0; }
function extra(r){ if (r > 20000 && r <= 32000) return 1000; if (r > 32000 && r < 40000) return 1000 * (40000 - r) / 8000; return 0; }
function calc(){
  const g = +document.getElementById('g').value || 0, c = N.cities[document.getElementById('city').value], n = +document.getElementById('inst').value;
  const inps = g * N.employee_inps + Math.max(0, g - N.extra_1pct_above) * 0.01;
  const tx = g - inps;
  const irpef = Math.max(0, bands(tx, N.irpef) - credit(tx) - extra(tx));
  const reg = bands(tx, c.regional), mun = tx > c.exempt ? tx * c.municipal : 0;
  const net = g - inps - irpef - reg - mun;
  const rows = [['Wynagrodzenie brutto', g], ['Składki pracownika', -inps], ['Podatek dochodowy (IRPEF) po ulgach', -irpef], [`Dodatek regionalny (${c.region})`, -reg], ['Dodatek gminny', -mun]];
  document.querySelector('#nt tbody').innerHTML = rows.map(([k, v]) => `<tr><td>${k}</td><td class="num">${eur(v)}</td></tr>`).join('') + `<tr><td><b>Netto</b></td><td class="num"><b>${eur(net)}</b></td></tr>`;
  document.getElementById('nm').textContent = `Około ${eur(net / n)} netto w każdym z ${n} miesięcznych pasków (${(net / g * 100).toFixed(0)}% brutto).`;
}
document.getElementById('nf').addEventListener('input', calc); document.getElementById('nf').addEventListener('submit', e => e.preventDefault()); calc();
})();</script>


---
Source: https://zatrudnieniewewloszech.com/kalkulator-netto.html

# Poproś o wycenę

> Poproś o wycenę zatrudnienia pracownika we Włoszech. Trzy krótkie kroki, odpowiedź w ciągu jednego dnia roboczego.


<section> <span class="eyebrow">Wycena</span> <h1 id="powiedz-nam-kogo-chcesz-zatrudnic">Powiedz nam, kogo chcesz zatrudnić</h1> <p class="lede">Trzy krótkie kroki. W ciągu jednego dnia roboczego odpowiadamy z pełnym kosztem i zarysem umowy.</p> </section> <section> <form id="lead" class="panel" style="display:grid;gap:18px;max-width:640px" novalidate> <p id="stepinfo" class="tag" style="justify-self:start">Krok 1 z 3</p> <fieldset data-step="1" style="border:0;padding:0;margin:0;display:grid;gap:14px"> <label for="email">Służbowy e-mail<input id="email" type="email" autocomplete="email" required></label> <label for="company">Firma<input id="company" autocomplete="organization"></label> </fieldset> <fieldset data-step="2" hidden style="border:0;padding:0;margin:0;display:grid;gap:14px"> <label for="service">Czego potrzebujesz?<select id="service"><option>Employer of Record</option><option>Obsługa płac (mamy spółkę we Włoszech)</option><option>Wiza / Niebieska Karta</option><option>Rekrutacja</option></select></label> <label for="count">Ile osób we Włoszech?<input id="count" type="number" min="1" value="1"></label> <label for="city">Miasto lub region<input id="city" placeholder="Mediolan, Rzym, zdalnie…"></label> <label for="salary">Planowane roczne wynagrodzenie brutto (EUR)<input id="salary" type="number" step="1000"></label> </fieldset> <fieldset data-step="3" hidden style="border:0;padding:0;margin:0;display:grid;gap:14px"> <label for="name">Imię i nazwisko<input id="name" autocomplete="name"></label> <label for="start">Planowana data rozpoczęcia<input id="start" type="date"></label> <label for="notes">Coś jeszcze?<textarea id="notes" rows="4"></textarea></label> <label style="display:flex;gap:10px;align-items:flex-start;font-weight:400"><input id="consent" type="checkbox" style="width:auto;margin-top:5px">Wyrażam zgodę na przetwarzanie moich danych przez ZatrudnienieWeWłoszech w celu odpowiedzi na to zapytanie (polityka prywatności).</label> </fieldset> <p id="msg" role="status" style="margin:0;color:var(--accent)"></p> <div class="cta"><button type="button" class="btn ghost" id="back" hidden>Wstecz</button><button type="submit" class="btn" id="next">Dalej</button></div> </form> </section> <script>
// Il passo 1 salva subito l'email (lead abbandonato recuperabile dal nurturing). Endpoint del worker: /api/lead.
const f = document.getElementById('lead'); let step = 1;
// Oggetto dalla pagina partner: ?subject=Partner precompila le note.
{ const sj = new URLSearchParams(location.search).get('subject'); if (sj) document.getElementById('notes').value = '[' + sj.slice(0, 40) + '] '; }
const sets = [...f.querySelectorAll('fieldset')];
const data = () => Object.fromEntries([...f.querySelectorAll('input,select,textarea')].map(e => [e.id, e.type === 'checkbox' ? e.checked : e.value]));
async function save(final){ try { await fetch('/api/lead', {method:'POST', headers:{'Content-Type':'application/json'}, body: JSON.stringify({...data(), step, final, brand:'zatrudnieniewewloszech'})}); } catch(e){} }
function show(){ sets.forEach(s => s.hidden = +s.dataset.step !== step);
  document.getElementById('stepinfo').textContent = `Krok ${step} z 3`;
  document.getElementById('back').hidden = step === 1;
  document.getElementById('next').textContent = step === 3 ? 'Wyślij zapytanie' : 'Dalej'; }
// Ripresa dal link nelle email: ?resume=<token> precompila i campi e salta al passo successivo.
(async () => { const tok = new URLSearchParams(location.search).get('resume'); if (!tok) return;
  try { const r = await fetch('/api/lead/' + encodeURIComponent(tok)); if (!r.ok) return; const d = await r.json();
    for (const [k, v] of Object.entries(d)) { const el = document.getElementById(k); if (el && v != null) el.value = v; }
    step = d.step || 2; show(); } catch(e){} })();
document.getElementById('back').onclick = () => { step--; show(); };
f.addEventListener('submit', e => { e.preventDefault(); const m = document.getElementById('msg'); m.textContent = '';
  if (step === 1 && !document.getElementById('email').checkValidity()) { m.textContent = 'Podaj poprawny służbowy e-mail, aby przejść dalej.'; return; }
  if (step === 3 && !document.getElementById('consent').checked) { m.textContent = 'Zaznacz zgodę, abyśmy mogli odpowiedzieć.'; return; }
  save(step === 3);
  if (step < 3) { step++; show(); } else { f.querySelectorAll('fieldset,.cta').forEach(x => x.hidden = true); m.textContent = 'Dziękujemy. Odpowiemy w ciągu jednego dnia roboczego.'; } });
</script>


---
Source: https://zatrudnieniewewloszech.com/kontakt.html

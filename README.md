# Sara & Nicolò — sito matrimonio

Sito statico in un singolo file (`index.html`). Tutto incluso: font da Google Fonts,
illustrazioni in SVG inline, animazioni CSS/JS vanilla, form RSVP funzionante.

## Pubblicare il sito (5 minuti, senza account complicati)

### Opzione 1 — Netlify Drop (consigliato per iniziare)
1. Vai su https://app.netlify.com/drop
2. Trascina la cartella che contiene `index.html`
3. Ottieni un URL del tipo `https://nome-casuale-12345.netlify.app`
4. (Opzionale) crea account gratuito → puoi rinominare in `sara-e-nicolo.netlify.app`
5. (Opzionale, più avanti) puoi collegare un dominio personalizzato tipo `saraenicolo.it`

### Opzione 2 — Vercel / GitHub Pages
Stessa logica: zip della cartella → upload. Per GitHub Pages serve un repo,
Claude Code può aiutarti a configurarlo se vuoi.

## Far funzionare il form RSVP (vero)

Adesso il form mostra solo un messaggio di conferma — non manda davvero
i dati a nessuno. Per riceverli via email basta collegarlo a **Formspree**:

1. Vai su https://formspree.io e crea un account gratuito (50 invii/mese gratis,
   sufficienti per un matrimonio).
2. Crea un nuovo form, ti darà un endpoint del tipo `https://formspree.io/f/xyzabcd`.
3. Apri `index.html` e cerca questa riga (verso la fine):
   ```html
   <form id="rsvp-form" class="form" onsubmit="return submitRSVP(event)">
   ```
4. Sostituiscila con:
   ```html
   <form id="rsvp-form" class="form" action="https://formspree.io/f/xyzabcd" method="POST">
   ```
   (al posto di `xyzabcd` il tuo codice Formspree)
5. Più giù, sostituisci tutta la funzione `submitRSVP` con qualcosa tipo:
   ```js
   formEl.addEventListener('submit', function(){
     // (Formspree fa il submit vero per noi; qui aggiorniamo solo la UI)
     setTimeout(function(){ showStep('done'); }, 50);
   });
   ```
6. Le risposte arriveranno via email. Su Formspree puoi anche scaricarle in CSV.

Alternative a Formspree (tutte gratuite per piccoli volumi):
- **Tally** (tally.so) — bello e potente, integrabile via iframe se preferisci
- **Google Forms** + un link "Conferma su modulo Google" (più brutto ma 0 setup)
- **Netlify Forms** (se hai pubblicato su Netlify) — basta aggiungere `netlify` come
  attributo al `<form>`. Anche questo gestisce le risposte gratis.

## Cosa modificare nel sito

Tutti i punti da personalizzare sono già marcati con commenti chiari nell'HTML.
I principali:

- **Sezione "Il racconto"**: il testo è un placeholder in tono Wanderhome.
  Sostituiscilo con la vostra storia vera (paragrafi 1-3 nel `<div class="story">`).
- **"Le piccole cose" (memoriae)**: tre frasette personali ("il primo tè",
  "la prima casa", "il convento"). Sentiti libero/a di cambiare i titoli e i
  sottotitoli con vostri ricordi reali.
- **Filo della giornata**: orari attuali sono 11:00 → 22:30. Aggiusta i tempi
  veri (taglio torta, festa, ecc.) man mano che li definisci con i fornitori.
- **Footer**: "S · N" e la frase "a presto, tra i cedri".

## Inserire foto vere

Quando avrai foto vostre / dei luoghi, sostituisci gli SVG nelle aree
`.illust-a`, `.illust-b`, `.place-illust`. Basta rimpiazzare l'intero `<svg>`
con un `<img src="...">`.

## Hosting delle immagini
Mettile in una cartella `img/` accanto a `index.html` (es. `img/villa.jpg`),
poi `<img src="img/villa.jpg" alt="...">`.

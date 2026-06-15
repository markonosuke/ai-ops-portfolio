# Livello 0 — Basi n8n e integrazione AI

## Blocco A — Fondamenta n8n

### Trigger (cosa avvia un workflow)
- Manual — avvio a mano, per i test
- Schedule — avvio automatico a orario o intervallo fisso
- Webhook — avvio quando arriva una chiamata HTTP dall'esterno

### Nodi principali
- IF — biforcazione su una condizione (ramo vero / ramo falso)
- Switch — biforcazione su piu' rami (piu' di due esiti)
- Filter — lascia passare solo gli item che rispettano una condizione
- Edit Fields (Set) — crea o modifica campi
- Code — esegue JavaScript (il codice lo fornisce Claude, si incolla)

### Fixed vs Expression (punto da fissare)
Ogni campo n8n puo' stare in due modalita':
- Fixed — valore FISSO, sempre lo stesso (es. un indirizzo scritto a mano)
- Expression — valore DINAMICO, calcolato dai dati in arrivo (es. {{ $json.email }})
Regola: se il valore cambia in base ai dati -> Expression. Se e' sempre uguale -> Fixed.
Il segnale dell'Expression sono le doppie graffe {{ }}.

### Sintassi dei dati
- {{ $json.campo }} — prende un campo dai dati in arrivo dal nodo precedente
- $('Nome nodo').first().json — prende i dati da un nodo specifico per nome (non solo il precedente)

## Blocco B — HTTP Request e API

### Chiamare API esterne
Il nodo HTTP Request manda richieste ad altri sistemi (Claude, Supabase, Google Sheets...).
- GET per leggere, POST per inviare o scrivere
- le credenziali vanno negli headers

### Headers delle chiavi
- Claude API -> header x-api-key
- Supabase  -> header apikey

## Blocco C — Integrazione AI (Claude / Gemini)

### Prompt con output JSON strutturato
Per una risposta JSON pulita da Claude:
- temperature 0 (risposta deterministica, niente fantasia)
- max_tokens 200 per JSON breve / 1024 per testo libero

### Estrarre la risposta
Claude restituisce il testo annidato: serve un nodo Code dopo per prendere content[0].text.
Se la risposta arriva sporca di markdown (blocco ```json ... ```), si pulisce con .replace().

## Blocco D — Database Supabase

### Logging via HTTP Request diretto
Il nodo Supabase nativo e' risultato instabile -> si usa HTTP Request diretto.
GET per leggere, POST per scrivere. Chiave nell'header apikey.

### Gotcha return=minimal
Con l'opzione return=minimal, Supabase NON restituisce dati al nodo successivo.
Se ti serve il dato salvato nel passo dopo, non usare return=minimal.

## Blocco E — Webhook

### Test URL vs Production URL
- Test URL — attivo solo mentre il workflow e' in "Listen for test event", serve per provare
- Production URL — attivo sempre, ma solo dopo aver fatto Publish del workflow

### Dove arrivano i dati
I dati del Webhook arrivano annidati dentro body:
$json.body.document_text   (non $json.document_text)

## Blocco F — Lezioni chiave (gotcha dai progetti)
- Nel join usare ||| e non \n: lo \n rompe il JSON
- Nodo Supabase nativo instabile -> HTTP Request diretto
- Code dopo Claude sempre necessario per estrarre content[0].text
- temperature 0 + max_tokens 200 per JSON
- Claude key in header x-api-key, Supabase key in header apikey
- Supabase return=minimal non restituisce dati al nodo dopo
- Dati Webhook in $json.body.campo, non $json.campo
- Nome dei campi: corrispondenza esatta, altrimenti undefined silenzioso

## Blocco G — GitHub
- Repo = archivio del progetto con lo storico completo delle modifiche
- Commit = una modifica salvata, con messaggio descrittivo
- main = il ramo principale, la versione ufficiale
- Caricare file: Add file -> Create new file / Upload files
- Creare una cartella: scrivila nel nome del file con la barra (es. docs/nome.md)
- README template: Problema, Soluzione, Architettura, Logica, Tool utilizzati, Risultati stimati, Competenze dimostrate

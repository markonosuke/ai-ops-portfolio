# Livello 1 — Fondamenta tecniche

## Blocco 1 — Parsing

### Array
Lista ordinata di elementi, tra parentesi quadre [ ].
Si accede per posizione (indice), e si conta DA ZERO.
  const disegni = ["DWG-01", "DWG-02", "DWG-03"];
  // posizione 0 = "DWG-01", posizione 1 = "DWG-02", ...
Gli elementi possono essere valori semplici o oggetti (righe con più campi).

### Il segnaposto prima della freccia
In map, filter e reduce, il nome prima di => (p, riga, acc...) e' INVENTATO da chi scrive.
Non gli dai mai un valore: lo riempie il metodo, un elemento alla volta.
  pesi.filter(p => p > 25)      // p e' uguale a banana, conta solo la posizione
Regola: tu lo NOMINI, non lo IMPOSTI mai.

### map — trasforma tutto
Applica la stessa operazione a ogni elemento. N entrano, N escono.
  const doppi = pesi.map(p => p * 2);   // [10,20] diventa [20,40]

### filter — seleziona
Tiene solo gli elementi che rispettano una condizione (domanda si/no).
N entrano, N o meno escono.
  const pesanti = pesi.filter(p => p > 25);
Nota: === significa "e' uguale a?" (confronto). = singolo invece ASSEGNA.

### reduce — riduce a un valore unico
Scorre l'array accumulando un totale parziale. Restituisce UN valore solo, non un array.
  const totale = pesi.reduce((acc, p) => acc + p, 0);
- primo segnaposto (acc) = accumulatore (ruolo fisso, deciso da reduce)
- secondo segnaposto (p) = elemento di turno
- lo 0 finale = valore di partenza dell'accumulatore

### split e join — inversi
split: stringa -> array, tagliando su un separatore
  "A-B-C".split("-")  // ["A","B","C"]
join: array -> stringa, incollando con un separatore
  ["A","B","C"].join(" | ")  // "A | B | C"
Lezione progetti: nel join usare ||| e non \n, perche' \n rompe il JSON.

## Blocco 2 — JSON avanzato

### Oggetto
Contenitore di campi nome:valore, tra graffe { }. Come una riga di BOM.
  const componente = { codice: "P-1001", peso: 12 };
Accesso per NOME del campo, col punto:
  componente.peso   // 12

### Punto vs Quadra (la regola chiave)
- punto .campo  -> entri in un OGGETTO, accedi per NOME
- quadra [n]    -> entri in un ARRAY, accedi per POSIZIONE

### Nidificazione
Un campo puo' contenere un altro oggetto o un array. Si naviga a tappe.
  documento.body.document_text     // entra in body, poi prende document_text
  risposta.content[0].text         // content e' un array -> [0] -> poi .text
Per questo in n8n il dato Webhook e' in $json.body.document_text (annidato in body).
Per questo serve il Code dopo Claude: scava fino a content[0].text.

### Corrispondenza esatta del nome
Il nome del campo deve combaciare carattere per carattere.
  citta != citta-con-accento, Citta != citta, document_text != documenttext
Se sbagli non da' errore: restituisce undefined (vuoto). Causa numero uno di workflow rotti.
Regola: copia il nome esatto dal nodo precedente, non fidarti della memoria.

### $json
Parola di n8n (non JavaScript): i dati in arrivo dal nodo precedente.
Il $ segnala "parola speciale di n8n". Il resto (.body.document_text) e' navigazione normale.

## Blocco 3 — API REST

Una richiesta = un ordine strutturato. 4 parti: metodo, URL, headers, body.
La risposta = codice di stato + body.

### Metodo
- GET  -> leggi/chiedi dati (di solito senza body)
- POST -> invia/scrivi dati (con body)

### Headers
Informazioni di servizio, non il contenuto. Chi sei, in che formato.
- x-api-key  -> chiave per Claude
- apikey     -> chiave per Supabase
- Content-Type: application/json -> "il body che mando e' JSON"

### Body
Il contenuto vero che spedisci (di solito solo nelle POST).
Es. POST a Claude: body con model, max_tokens, messages.

### Codici di risposta
- 2xx -> ok (200 = fatto)
- 4xx -> colpa della richiesta (401 = chiave sbagliata/mancante, 404 = URL/risorsa errata)
- 5xx -> colpa del server
Debug: 401 -> controlla la chiave API, non il prompt. 404 -> controlla l'URL.

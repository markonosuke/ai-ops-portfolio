# Progetto 04 — AI Document Summarizer

## Descrizione
Workflow che riceve un documento di testo via webhook, lo invia a Claude per generare un riassunto strutturato, manda il riassunto via email e logga l'esecuzione su database.

## Trigger
Webhook POST — riceve un JSON con il campo testo

## Flusso
Webhook → HTTP Request (Claude API) → Code in JavaScript → Send Email (Resend) → HTTP Request (Supabase)

## Logica
- Il Webhook riceve il documento come JSON via POST
- HTTP Request invia il testo a Claude API con prompt di riassunto
- Code in JavaScript estrae il riassunto dalla risposta di Claude
- Resend invia email con il riassunto
- HTTP Request logga l'esecuzione su Supabase

## Prompt engineering
Claude riceve un prompt strutturato che richiede un riassunto in 3-5 punti bullet, in italiano, focalizzato sulle informazioni chiave e le azioni richieste. Output solo riassunto, senza introduzioni.

## Tool utilizzati
- n8n
- Claude API (riassunto testo)
- Resend (invio email)
- Supabase (logging)

## Competenze dimostrate
- Webhook POST con body JSON
- Chiamata diretta a Claude API via HTTP Request
- Prompt engineering per generazione contenuto
- Estrazione dati da risposta API con Code node
- Logging su database PostgreSQL

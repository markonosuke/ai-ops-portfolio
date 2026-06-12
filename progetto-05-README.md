# Progetto 05 — AI Cost Estimator

## Descrizione
Sistema di preventivazione automatica per officine metalmeccaniche. Riceve la descrizione di un pezzo via webhook, calcola tramite Claude AI il materiale grezzo necessario, le ore di lavorazione e il costo totale di produzione, invia il preventivo via email e logga l'esecuzione su database.

## Trigger
Webhook POST — riceve un JSON con i dati del pezzo (tipo, materiale, dimensioni, spessore, quantità)

## Flusso
Webhook → HTTP Request (Claude API) → Code in JavaScript → Send Email (Resend) → HTTP Request (Supabase)

## Logica
- Il Webhook riceve i dati del pezzo via POST
- HTTP Request invia i dati a Claude con prompt strutturato di preventivazione
- Claude restituisce un JSON con calcoli di materiale, ore e costi
- Code in JavaScript estrae e parsa il JSON dalla risposta di Claude
- Resend invia email con preventivo formattato in HTML
- HTTP Request logga l'esecuzione su Supabase

## Output del preventivo
- Materiale grezzo necessario (kg)
- Quantità bulloni
- Ore di lavorazione stimate
- Costo materiale (€)
- Costo manodopera (€)
- Costo totale (€)
- Note tecniche

## Prezzi di riferimento usati nel prompt
- Lamiera acciaio: 1.20 €/kg
- Lamiera inox: 4.50 €/kg
- Profilati: 1.50 €/kg
- Bulloneria: 0.30 €/pz
- Manodopera: 35 €/ora

## Tool utilizzati
- n8n
- Claude API (calcolo preventivo)
- Resend (invio email)
- Supabase (logging)

## Competenze dimostrate
- Webhook POST con body JSON strutturato
- Prompt engineering per output JSON strutturato da LLM
- Parsing JSON con pulizia markdown (rimozione backtick)
- Email HTML formattata con dati dinamici
- Logging su database PostgreSQL
- Caso d'uso reale: preventivazione officina metalmeccanica

# Progetto 02 — PDM Revision Notifier

## Descrizione
Workflow automatico che monitora un Google Sheet con documenti CAD/PDM e invia email di notifica quando un documento entra in stato di revisione.

## Trigger
Schedule — esecuzione periodica automatica

## Flusso
Schedule Trigger → HTTP Request → Code in JavaScript → Filter → Edit Fields → Send Email

## Logica
- HTTP Request legge i dati dal Google Sheet
- Code in JavaScript analizza e formatta i dati
- Filter seleziona solo i documenti in stato revisione
- Edit Fields prepara i campi per l'email
- Resend invia la notifica al responsabile

## Tool utilizzati
- n8n
- Google Sheets (fonte dati)
- Resend (invio email)

## Competenze dimostrate
- Schedule trigger
- HTTP Request verso API esterna
- Manipolazione dati con JavaScript
- Filtering condizionale
- Invio email automatico

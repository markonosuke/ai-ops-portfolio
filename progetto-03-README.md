# Progetto 03 — Drawing Approval Agent

## Descrizione
Agente AI che verifica la completezza dei campi obbligatori di un disegno tecnico industriale e invia email di approvazione o rifiuto in base all'esito della verifica.

## Trigger
Webhook — attivato da URL con query parameters

## Flusso
Webhook → Claude AI → Code in JavaScript → IF → Email approvazione / Email rifiuto

## Logica
- Il Webhook riceve i dati del documento via query parameters
- Claude AI verifica la presenza di tutti i campi obbligatori
- Code in JavaScript analizza la risposta JSON di Claude
- IF instrada verso approvazione o rifiuto
- Resend invia l'email corrispondente all'esito

## Campi verificati
- Numero documento
- Titolo
- Revisione
- Data
- Progettista
- Nr. Commessa
- Materiale
- Peso

## Tool utilizzati
- n8n
- Claude API (verifica campi)
- Resend (invio email)

## Competenze dimostrate
- Webhook trigger con query parameters
- Integrazione Claude API con prompt engineering
- Output JSON strutturato da LLM
- Logica condizionale IF
- Invio email differenziato per esito

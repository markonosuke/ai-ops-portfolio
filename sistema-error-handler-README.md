# Sistema — Error Handler

## Descrizione
Workflow di sistema che intercetta automaticamente gli errori da tutti gli altri workflow, invia una notifica email immediata e registra l'evento su database per analisi storica.

## Trigger
Error Trigger — si attiva automaticamente quando qualsiasi workflow collegato genera un errore

## Flusso
Error Trigger → Code in JavaScript → Send a new email (Resend)
                                   → HTTP Request (Supabase)

## Logica
- Error Trigger cattura i dati dell'errore
- Code in JavaScript estrae workflow, nodo e messaggio di errore
- Resend invia email di notifica immediata
- HTTP Request logga l'evento su Supabase

## Dati loggati
- Nome workflow che ha generato l'errore
- Nodo specifico che ha fallito
- Messaggio di errore
- Timestamp

## Tool utilizzati
- n8n
- Resend (notifica email)
- Supabase (logging persistente)

## Competenze dimostrate
- Error Trigger e gestione errori globale
- Estrazione dati con Code node
- Notifica email automatica
- Logging su database PostgreSQL via API REST

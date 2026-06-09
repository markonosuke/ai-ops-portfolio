# Progetto 01 — Document Classifier AI

## Problema
La gestione manuale dei documenti tecnici in un impianto 
industriale richiede ore di lavoro ogni settimana.
Ogni documento deve essere letto, classificato e smistato 
alla persona giusta manualmente.

## Soluzione
Sistema automatico che riceve un documento via Webhook,
lo classifica con Claude AI e lo smista automaticamente
in 4 categorie con messaggi personalizzati.

## Architettura
Webhook → Claude AI → Code → Switch → Azione

## Tool usati
- n8n (workflow automation)
- Claude Haiku API (classificazione AI)
- Webhook trigger (integrazione esterna)

## Risultati stimati
- Classificazione: 0 minuti vs 5-10 minuti manuale
- Errori di smistamento: 0% vs 15% manuale
- Disponibilità: 24/7 vs orario lavorativo

## Come installarlo
1. Importa il file JSON in n8n
2. Configura la credenziale Anthropic API
3. Attiva il workflow

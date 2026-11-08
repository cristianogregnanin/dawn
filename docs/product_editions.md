# Edizioni dei prodotti nel tema

`my_fields.events` resta un array JSON. Le nuove voci includono `edition_id`, `edition_label`, `edition_duration_days` e `edition_bookable`. Rails pubblica insieme le giornate della stessa edizione anche quando, nel calendario originale, sono separate o intercalate con quelle di un'altra edizione.

La scheda della collezione mostra la prima giornata futura di un'edizione ancora prenotabile. Mostra «Dal … al …» solo quando un unico intervallo copre l'intera durata dell'edizione; altrimenti mostra la prima data e «Durata: N giorni». «Altre date disponibili» compare solo se esiste un'altra edizione prenotabile. Le giornate residue di un'edizione già iniziata restano nella pagina prodotto, ma non compaiono come nuova partenza nella scheda della collezione. Rails mantiene il tag `prossime uscite` solo se almeno un'edizione è ancora prenotabile.

Nella pagina prodotto, «Date disponibili» presenta le giornate future per edizione. Il modulo di contatto invia l'ID stabile dell'edizione insieme alle date mostrate. Un'edizione già iniziata resta visibile ma non è selezionabile nel modulo. Il percorso precedente rimane attivo per i prodotti il cui JSON non contiene ancora `edition_id`: rimuoverlo solo dopo il confronto dei dati pubblicati e la verifica del tema di sviluppo con date separate e intercalate.

Il tema preferisce i metafield tipizzati `custom.activity_is_course` e `custom.activity_duration_days`, se esistono; altrimenti usa i precedenti `my_fields.is_course` e `my_fields.duration`.

## Traduzioni

Le etichette fisse di Liquid usano `locales/it.json` e `locales/en.default.json`. Le impostazioni salvate nei template JSON e i contenuti dei metaobject richiedono invece una traduzione nel negozio Shopify, per esempio con Translate & Adapt o con l'Admin API dotata di `write_translations`. Non cambiare il testo sorgente italiano in un template per ottenere la versione inglese: cambierebbe anche la pagina italiana.

Nei 19 template JSON di prodotto si trovano 36 occorrenze di «Richiedi informazioni», 18 di «Domande?», 16 di «Difficoltà» e una di «Luoghi e Dettagli Logistici». Sono presenti anche etichette come «Tempo medio di percorrenza» e «Dislivello» nei blocchi rich text. L'8 novembre 2026, nell'anteprima `/en` dei tre prodotti allora presenti in «Prossime uscite», «Luoghi e Dettagli Logistici» e «Domande?» erano ancora in italiano, mentre «Richiedi informazioni» risultava tradotto. Questo campione non dimostra lo stato delle altre pagine.

Traduzioni consigliate: «Request information», «Questions?», «Difficulty», «Locations and logistics», «Average walking time», «Elevation gain». Prima di registrarle, censire le chiavi traducibili effettive e le traduzioni già presenti nello shop: l'editor del tema può rigenerare i JSON dei template. Shopify espone queste impostazioni come risorse `ONLINE_STORE_THEME_JSON_TEMPLATE`.

Per la verifica locale eseguire `shopify theme check` e aprire il tema di sviluppo con `shopify theme dev`. Il tema di sviluppo non pubblica il tema live. Se la CLI segnala un disallineamento tra ID del tema di sviluppo e tema live, fermare il processo e creare una nuova sessione di sviluppo senza usare `--allow-live`.

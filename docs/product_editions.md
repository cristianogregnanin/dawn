# Product editions in the storefront

`my_fields.events` remains a JSON array. New entries include `edition_id`, `edition_label`, and `edition_bookable`. Days belonging to an edition are published together even when they are separated by days or by other editions in the Rails calendar. The product date panel shows future dates and the contact form submits a stable edition ID together with all of its displayed dates. An edition that has already begun stays visible but is not offered in the form.

The upcoming collection card considers only future days whose `edition_bookable` value is not `false`. It counts only bookable editions for the "More dates available" label. Rails keeps the `prossime uscite` product tag only while at least one bookable edition exists. The product page may still display remaining days of an edition in progress after the product leaves that collection.

The theme reads `custom.activity_is_course` and `custom.activity_duration_days` when those typed metafields exist. Until the Rails migration publishes them, it falls back to the current `my_fields.is_course` and `my_fields.duration` JSON values.

The legacy renderer and form path remain active for products whose JSON has no edition ID. Remove them only after the Rails backfill, dev-theme verification with separated and interleaved dates, and live data comparison are complete.

Fixed Liquid labels use `locales/it.json` and `locales/en.default.json`. Text saved in JSON template settings, such as difficulty labels and accordion headings, needs a Shopify content translation through Translate & Adapt; Liquid locale keys do not translate merchant-editable settings. Check each product under `/en` after those translations are entered.

Inventory of untranslated source settings in the 19 product JSON templates: `Richiedi informazioni` occurs in 19 templates, `Difficoltà` in 16, `Domande?` in 18, and `Luoghi e Dettagli Logistici` in one. These are source settings, not locale-file strings. Suggested English values are `Request information`, `Difficulty`, `Questions?`, and `Locations and logistics`. Audit the actual translatable keys and current translations in Shopify before registering changes; the theme editor can regenerate template JSON. Shopify identifies these settings as `ONLINE_STORE_THEME_JSON_TEMPLATE` resources.

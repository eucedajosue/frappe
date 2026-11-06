# Customizaciones de Compumundo en Frappe (rama `version-16-custom`)

Fork = `version-16` de upstream + lo de abajo. Ver también `apps/erpnext/CUSTOMIZACIONES.md`
(flujo de merge, validaciones y guía de conflictos).

Lista real actual: `git diff --stat version-16 version-16-custom`

| Archivo | Qué hace nuestro cambio | Si hay conflicto |
|---|---|---|
| `frappe/desk/search.py` | Búsqueda por varias palabras: `get_search_terms`, `filter_by_search_terms`; cada término se agrega a `or_filters` y los resultados se filtran en Python (`all(term in haystack)`). Trae un margen de candidatos (`page_length * 5`, mínimo 50) cuando hay varios términos. | Conservar upstream y reponer las dos funciones, el uso de `match_terms` y el filtrado final. |
| `frappe/tests/test_search.py` | Añade `test_search_matches_words_in_any_order` (busca "Manager System" y espera "System Manager"). Respecto a `version-16`, la rama custom no tiene las pruebas `test_relevance_skipped_without_txt` y `test_empty_search_still_orders_by_idx`: si vuelven a aparecer tras un merge, deben pasar con nuestro `search.py` (revisar que la lógica de relevancia de upstream no se haya perdido). | Conservar la prueba nuestra y las de upstream; ejecutarlas. |
| `frappe/public/js/frappe/widgets/links_widget.js` | Tooltips en pantallas táctiles: `trigger: "focus"` en táctil, `container: "body"`, `boundary: "viewport"`, sin descripción en táctil. | Conservar upstream y reponer `is_touchscreen`. |
| `frappe/public/scss/desk/desktop.scss` | Iconos del escritorio en móvil vertical (`@media (max-width: 480px) and (orientation: portrait)`). | Es un bloque añadido al final: conservar ambos. |
| `frappe/locale/es.po` | Una traducción vaciada (`msgstr "Torta"` → `""`). | Gana upstream. |

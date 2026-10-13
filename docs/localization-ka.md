# Georgian interface

> **Last reviewed:** 2026-10-13 · **Last updated:** 2026-10-13 · **Change:** minor (Georgian notes and terminology; catalog brought up to date with upstream main, 194 rows added) · **Target:** Adobe Illustrator 2026 (30.x)

Choose **Edit › Preferences… › User Interface › Language › ქართული** (on macOS also
**VectorCraft › Language › ქართული**), or follow a Georgian system language (`ka`, `ka-GE`,
`ka_GE.UTF-8`; `VECTORCRAFT_LOCALE=ka` does the same for a headless run or a launch while the preference
is `auto`). The catalog code is `ka`; `app.language` with `{"lang":"ka"}` selects it explicitly, and the
choice is saved as the `interfaceLanguage` preference. Document text, command ids, menu paths used by
scripts, CLI/MCP/control responses and file paths do not change.

`crates/ui-egui/src/i18n/ka.tsv` has about 4,590 rows: every menu string, command label and `tl!`
literal (panels, dialogs, tooltips, Preferences), the `@plural` rows and the `@msg` status and error
messages, held complete by the tests. Left in English on purpose (`MENU_KEEP_AS_IS`): the product name,
language names, OpenType, the built-in workspace names and the bracketed perspective grid preset names;
units (pt, px, mm, in) and format names stay Latin. It is written from the meaning of the English labels,
following the shared Georgian glossary of the Craft apps; no proprietary translation resources were
consulted. Drafted with AI assistance; a native-speaker review is pending (doubtful terms are queued).

## Georgian script

- **No case.** Mkhedruli has no capitals, so UI text never uses Mtavruli (a test fails on any
  `U+1C90–U+1CBF` letter in `ka.tsv`). Type › Change Case › Title Case and Sentence case leave Georgian
  lower case (and bring Mtavruli back to it) instead of capitalizing it (`capitalizes` guard in
  `crates/engine/src/cmd/typemenu.rs`); UPPER CASE still gives Mtavruli, as Unicode defines it.
- **Counts.** A noun after a number stays singular, so every `@plural` row has one count-neutral form:
  `შრე: {n}` rather than a number glued to a noun.
- **Fonts.** The bundled UI fonts (Source Sans 3, JetBrains Mono) have no Georgian. The desktop app adds
  the first installed face of `theme::GEORGIAN_FONTS` (SF Georgian, Arial Unicode, Sylfaen, Noto Sans
  Georgian, DejaVu Sans) to every family from the first frame. craft-fonts has no Georgian face yet, so
  the web build shows Georgian as boxes until it carries Noto Sans Georgian (OFL) and fetches it as it
  does Noto Sans Thai.
- **Numbers and dates.** The app has no per-language number or date formats, so Georgian uses the same
  ones as the other languages.

## Terminology

Follow this table when adding strings; it is the Georgian as the catalog has it now.

| Source | Georgian |
|---|---|
| File / Edit / Object / Type / Select / Effect / View / Window / Help | ფაილი / რედაქტირება / ობიექტი / ტექსტი / მონიშვნა / ეფექტი / ჩვენება / ფანჯარა / დახმარება |
| Undo / Redo / Paste | დაბრუნება / ხელახლა შესრულება / ჩასმა |
| Artboard / Artboard Tool | სამუშაო დაფა / სამუშაო დაფის ხელსაწყო |
| Layers | შრეები |
| Path / Anchor Point Tool | ტრაექტორია / საყრდენი წერტილის ხელსაწყო |
| Stroke / Fill | კონტური / შევსება |
| Swatches | ფერის ნიმუშები |
| Gradient / Pattern | გრადიენტი / პატერნი |
| Appearance / Expand Appearance | იერსახე / იერსახის გაშლა |
| Graphic Styles | გრაფიკული სტილები |
| Character / Symbols | სიმბოლო / სიმბოლოები |
| Pathfinder | ტრაექტორიების ოპერაციები |
| Selection Tool / Direct Selection Tool | მონიშვნის ხელსაწყო / პირდაპირი მონიშვნის ხელსაწყო |
| Pen Tool / Curvature Tool | კალმის ხელსაწყო / მრუდის ხელსაწყო |
| Shape Builder Tool | ფიგურების კონსტრუქტორის ხელსაწყო |
| Image Trace | გამოსახულების ვექტორიზაცია |
| Offset Path… | ტრაექტორიის წანაცვლება… |
| Clipping Mask | მომჭრელი ნიღაბი |
| Opacity / Blend | გაუმჭვირვალობა / გადასვლა |
| Brushes | ფუნჯები |
| Align / Transform | სწორება / გარდაქმნა |
| Group / Ungroup | დაჯგუფება / დაჯგუფების მოხსნა |
| Snap to Point | წერტილზე მიბმა |
| Reset / Presets | ჩამოყრა / პრესეტები |
| Preferences… | პარამეტრები… |

Commands are verbal nouns (შენახვა, გახსნა), tools are genitive + ხელსაწყო ("X Tool" = X-ის ხელსაწყო).

## Maintenance

Add a row `context<TAB>English<TAB>Georgian` to `ka.tsv` (empty context for plain UI strings, `@msg` for
status and error messages, `@plural` for `one|other` sources, `@id` for a command id). Keep placeholders
(`{n}`, `{name}`, `{_1}`), backticks, ellipses and the leading or trailing spaces of fragments exactly.
`cargo test -p vectorcraft-ui-egui --lib i18n` checks it: well-formed rows and matching placeholders
(`bundled_catalogs_are_consistent`), every menu string, `tl!` literal and message translated
(`complete_languages_translate_every_menu_string`, `every_tl_literal_is_translated`,
`complete_languages_translate_every_message`), no Mtavruli and the core vocabulary
(`georgian_reads_as_georgian`), and glyph coverage where a Georgian font is installed
(`bundled_fonts_cover_the_catalogs`). Untranslated strings fall back to English.

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-13 | minor | Georgian notes and terminology; 194 rows for strings added upstream (graphs, relinking, 3D and Materials, grid tool options, file filters) |

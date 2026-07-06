---
name: pattern-picker
description: 'Choose the right interaction pattern per situation with decision tables - modal vs page vs inline, undo vs confirm dialog, toast vs banner, tabs vs accordion, dropdown vs radio, pagination vs infinite scroll, wizard vs single form. Use this skill whenever designing or building ANY interactive behavior; whenever the user asks "moet dit een popup zijn", "hoe toon ik deze melding", "dropdown of knoppen", or when a UI feels annoying (confirm-dialogen overal, toasts die verdwijnen met belangrijke info, hamburgermenu op desktop). Interaction stays boring and familiar so the visual identity (ui-concept-forge) can be original.'
---

# Pattern Picker

Users spend most of their life in OTHER interfaces — that is where their expectations come from. Original visuals delight; original interaction patterns confuse. So the rule is: creativity in the look (ui-concept-forge), convention in the behavior. This skill is the convention book: per situation, the pattern that matches user expectations, with the reason why.

## Modal vs nieuwe pagina vs inline

- **Inline** (bewerken op de plek zelf): kleine wijziging van één waarde, context mag niet verloren gaan. Klik → veld wordt bewerkbaar → blur/enter bewaart.
- **Modal**: één korte, afgebakende taak (< ~1 minuut) waarna je terug wilt naar waar je was — bevestigen, hernoemen, snel aanmaken. Nooit: lange formulieren, multi-step, of iets waar mensen naartoe willen kunnen linken. Escape en klik-buiten sluiten hem; focus komt terug waar hij was (frontend-quality-gates).
- **Nieuwe pagina**: complexe of langere taken, alles wat een eigen URL verdient (deelbaar, terugknop werkt), alles met meer dan een handvol velden.
- Modal-in-modal is altijd een ontwerpfout — de taak was te groot voor een modal.

## Undo vs confirm-dialoog

- **Omkeerbaar** (verplaatsen, archiveren, verwijderen-met-prullenbak): voer direct uit + toon "Ongedaan maken" (toast, ~7s). Undo respecteert de flow; confirms trainen mensen om blind OK te klikken — daarna beschermt geen enkele confirm meer.
- **Onomkeerbaar en zwaar** (permanent verwijderen, versturen naar klanten, betalen): confirm die het GEVOLG benoemt ("Dit verwijdert 34 facturen definitief"), met de destructieve knop niet als default.
- **Catastrofaal** (account/project weg): laat de naam overtypen. Frictie is hier een feature.

## Toast vs banner vs inline melding

- **Toast** (verdwijnt vanzelf): bevestiging van gelukte acties die geen reactie vragen ("Opgeslagen"). NOOIT voor fouten of info waarop gehandeld moet worden — die verdwijnt voordat iemand hem las.
- **Banner** (blijft staan tot opgelost/gesloten): systeembrede toestanden — offline, betaalprobleem, onderhoudsmelding.
- **Inline**: alles wat bij één element hoort, vooral formulierfouten naast het veld (form-craft). Fout van een submit? Inline bij de knop + focus erheen, geen toast.

## Tabs vs accordion vs aparte paginas

- **Tabs**: parallelle weergaven van hetzelfde object (Details / Activiteit / Instellingen), max ~5, labels van één woord. Tab-state in de URL zodat verversen en delen werkt.
- **Accordion**: scanbare lijst waarvan de meeste items dicht blijven (FAQ, optionele instellingen). Niet voor content die iedereen moet zien — verstopt is verstopt.
- **Aparte paginas**: wezenlijk verschillende taken. Tabs die eigenlijk navigatie zijn, verwarren de terugknop.

## Opties kiezen: radio/segmented vs dropdown

- **2–5 opties**: toon ze allemaal (radio groep of segmented control). Zichtbaar kiezen is één interactie; een dropdown zijn er drie én verbergt de opties.
- **6+ opties**: dropdown; **10+ of onvoorspelbaar** (landen): doorzoekbare select.
- Binaire aan/uit met direct effect: toggle. Aan/uit dat pas na "Opslaan" geldt: checkbox. Toggle die niet direct iets doet, voelt kapot.

## Lijsten: paginering vs infinite scroll vs load-more

- **Paginering**: doelgericht zoeken en terug kunnen keren naar een item ("stond op pagina 3"), tabellen, beheer-schermen.
- **Infinite scroll**: alleen voor leunstoel-feeds zonder doel. Nadelen zijn reëel: footer onbereikbaar, positie kwijt na terugknop.
- **Load-more knop**: het redelijke midden — gebruiker houdt controle, positie blijft.

## Wizard vs één formulier

Eén scherm zolang het overzichtelijk blijft (tot ~7 velden, form-craft); daarboven een wizard met voortgang en werkende terugknop. Wizard-stappen per onderwerp, makkelijkste eerst (investering groeit).

## Navigatie: zichtbaar vs hamburger

Desktop: top-level navigatie zichtbaar — verstopte navigatie wordt minder gebruikt. Hamburger is een mobiel compromis, geen stijlkeuze; overweeg op mobiel eerst een bottom-bar met de 3–5 kernbestemmingen (duimzone, responsive-craft).

## Tooltip vs helper text

Essentieel om de taak te doen → zichtbare helper text. Aardig om te weten → tooltip. Als de UI zonder tooltip onbegrijpelijk is, is de tooltip een pleister op een naming-probleem (design:ux-copy).

## Meta-regel

Twijfel tussen twee patronen? Kies wat de doelgroep dagelijks al ziet in de apps die ze gebruiken. Het "saaie" patroon dat werkt verslaat het interessante patroon dat uitleg nodig heeft — bewaar de originaliteit voor waar hij loont: het beeld, niet het gedrag.

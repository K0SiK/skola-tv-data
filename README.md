# Škola na TV – obsah pro učení

Veřejné úložiště učiva pro aplikaci **Škola na TV** (Android TV).

Aplikace si při spuštění stahuje tento soubor:

```
https://raw.githubusercontent.com/K0SiK/skola-tv-data/main/content.json
```

a ukládá si offline kopii. Po úpravě na GitHubu stačí hru v televizi zavřít
a znovu otevřít, případně na domovské obrazovce stisknout **🔄 Aktualizovat**.

## Struktura

```
předmět → téma → otázky
```

- **Předmět** má název, emoji a barvu.
- **Téma** má název, popis, velikost kola, volbu známkování a otázky.
- **Otázka** má zadání, 2–4 možnosti, správnou odpověď a vysvětlení.

## Formát

```json
{
  "version": 1,
  "subjects": [
    {
      "id": "cestina",
      "title": "Český jazyk",
      "emoji": "📚",
      "color": "#2563EB",
      "topics": [
        {
          "id": "znamenka",
          "title": "Doplň znaménko",
          "description": "Doplň na konec věty tečku, otazník nebo vykřičník.",
          "roundSize": 10,
          "grading": true,
          "questions": [
            {
              "prompt": "Co si zítra vezmeš na sebe do školy ___",
              "options": [
                { "text": ".", "label": "Tečka" },
                { "text": "?", "label": "Otazník" },
                { "text": "!", "label": "Vykřičník" }
              ],
              "answer": "?",
              "explanation": "Je to věta tázací.",
              "hint": "Začíná tázacím slovem CO. Ptáme se, patří sem otazník."
            }
          ]
        }
      ]
    }
  ]
}
```

### Pole

- `id` – krátký unikátní identifikátor bez diakritiky (např. `matematika`).
- `title`, `description` – texty zobrazené v televizi.
- `emoji` – jeden emoji znak předmětu.
- `color` – barva karty ve formátu `#RRGGBB`.
- `roundSize` – kolik otázek se vybere do jednoho kola (výchozí 10).
- `grading` – `true` = na konci známka 1–5, `false` = jen body.
- `prompt` – zadání otázky.
- `options` – 2 až 4 možnosti. `text` je povinný, `label` nepovinný
  (hodí se pro symboly, např. tečka/otazník/vykřičník).
- `answer` – musí přesně odpovídat textu jedné z možností.
- `explanation` – krátké vysvětlení správné odpovědi.
- `hint` – nepovinná pomůcka.

Aplikace si pamatuje použité otázky, takže se neopakují, dokud se
nevystřídá celá zásoba daného tématu.

## Jak přidat předmět nebo téma

1. Otevřete `content.json` a klikněte na **Edit**.
2. Zkopírujte existující předmět/téma a upravte `id`, `title`, `emoji`,
   `color` a otázky.
3. Commitněte do větve `main`.
4. V televizi stiskněte **🔄 Aktualizovat**.

## Generování dalšího učiva

Připravený prompt pro jiný model je v
[`PROMPT-generovani-obsahu.md`](PROMPT-generovani-obsahu.md).

## Bezpečnost

Repozitář je veřejný pouze pro čtení. Upravovat ho může jen vlastník účtu.
Aplikace funguje i offline s poslední staženou kopií.

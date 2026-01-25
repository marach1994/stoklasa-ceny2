# Stoklasa Ceny - Mamtex Marže Kalkulátor

## Popis
Automatický nástroj pro stahování produktového feedu z Mamtex.cz, výpočet marží a export pro Napojse.cz.

## Struktura projektu
```
stoklasa-ceny2/
├── mamtex_marze.py          # Hlavní Python skript
├── marze_export.csv         # Výstupní CSV (generuje se automaticky)
├── .github/workflows/
│   └── update.yml           # GitHub Actions - denní aktualizace
├── .gitignore
└── README.md
```

## Výstupní CSV sloupce
| Sloupec | Popis |
|---------|-------|
| Kód produktu | Kód z Mamtex feedu |
| Název | Název produktu |
| Nákupní cena | Cena od dodavatele |
| Prodejní cena | Prodejní cena |
| Marže Kč | Prodejní - Nákupní |
| Marže % | ((Prodejní - Nákupní) / Prodejní) × 100 |
| Multishop | Marže % zaokrouhlená na 5 (hladiny) |

## Zaokrouhlení Multishop
- 27% → 30% (nahoru)
- 24% → 25% (nahoru)
- 51% → 50% (dolů - zbytek 1)
- 63% → 65% (nahoru)

Pravidlo: Zbytek po dělení 5 je 1 → dolů, jinak nahoru.

## URL pro Napojse
```
https://raw.githubusercontent.com/marach1994/stoklasa-ceny2/main/marze_export.csv
```

## Zdrojový feed (Mamtex)
```
https://www.mamtex.cz/export/products.csv?patternId=279&partnerId=8&hash=98f603114b86c6b8be3cc9563c71ce983ce16ff98eb32df69d8cb32b73ada2ba&supplierId=316
```

## Automatická aktualizace
- **Kdy:** Každý den v 7:00 CET (6:00 UTC)
- **Jak:** GitHub Actions workflow
- **Ruční spuštění:** https://github.com/marach1994/stoklasa-ceny2/actions → Run workflow

## Nastavení GitHub repo (důležité!)
Pro fungování automatické aktualizace:
1. Jdi na: https://github.com/marach1994/stoklasa-ceny2/settings/actions
2. Scrolluj na **"Workflow permissions"**
3. Vyber **"Read and write permissions"**
4. Klikni **Save**

## Lokální spuštění
```bash
cd C:\Vibecode\stoklasa-ceny2
python mamtex_marze.py
```

## Požadavky
- Python 3.11+
- Žádné externí knihovny (používá pouze standardní knihovnu)

## Historie vývoje
- **v1:** Základní skript - stažení, výpočet marže
- **v2:** Menší feed (supplierId=316), kódování Windows-1250, české názvy sloupců
- **v3:** Retry logika, User-Agent hlavička
- **v4-v14:** Opravy GitHub Actions workflow
- **Finální:** Nové repo stoklasa-ceny2 s čistou historií

## Kontakt
- GitHub: marach1994
- Email: Marach1994@gmail.com

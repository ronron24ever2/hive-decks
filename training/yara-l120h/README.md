# Operatøropplæring · fjernstyrt L120H · Yara Porsgrunn

**Live URL:** https://presentations.hiveautonomy.no/training/yara-l120h/

18-slide HTML-deck for Fase 1 av operatøropplæringen. Bygd som webside, ikke PowerPoint — fungerer i alle moderne nettlesere, lazy-loader video, kan deles via direktelenke.

## Hvordan bruke decken

| Tast / handling | Effekt |
|---|---|
| Pil høyre · mellomrom · klikk høyre side | Neste slide |
| Pil venstre · klikk venstre side | Forrige slide |
| `f` | Fullskjerm |
| `Home` / `End` | Første / siste slide |
| `#s7` i URL | Hopper rett til slide 7 |

Decken kan vises på operatør-stasjonen, projisert på lerret, eller delt som lenke. Ingen installasjon, ingen PowerPoint, ingen lisens. Den fungerer på laptop, iPad, og phone.

## Hvordan gjøre endringer i decken

To fremgangsmåter, etter hva som passer deg.

### A — Du sender ønsker tilbake til Ronny / Hive

Skriv hva du vil endre i Slack eller mail. Eksempel:
> "Slide 4 — bytt rekkefølge på pillarene. Yara HMS skal stå sist, ikke først."
> "Slide 16 — Yara HSE-leder Porsgrunn er Per Hansen, +47 92 12 34 56, per.hansen@yara.com."
> "Slide 5 — bildet stemmer ikke med vår L120H. Vi sender bedre foto."

Ronny pusher ny versjon. Du får oppdatert lenke samme dag.

### B — Du gjør endringene selv via Claude / Claude Code

Hvis du vil iterere selv, fortsett til **Med Claude Code**-seksjonen lenger ned.

## Med Claude Code (for Ravi)

Claude Code er et terminal-verktøy som lar deg snakke naturlig med en agent som redigerer filer for deg. Du trenger ikke kode HTML — agenten gjør det.

### Førstegangs-oppsett (5 minutter)

1. **Installer Claude Code:** https://docs.claude.com/en/docs/claude-code/quickstart
2. **Pakk ut ZIP-en** du har fått fra Ronny til en mappe, for eksempel:
   ```
   ~/Documents/yara-training-deck/
   ```
3. **Åpne terminalen** og gå inn i mappen:
   ```
   cd ~/Documents/yara-training-deck/
   ```
4. **Start Claude Code:**
   ```
   claude
   ```

Claude Code leser `AGENTS.md` automatisk og vet alt den trenger om decken.

### Eksempler på hva du kan be agenten gjøre

Skriv på vanlig norsk eller engelsk:

- *"Endre tittel på slide 1 fra 'Fjernstyrt L120H' til 'Fjernstyrt hjullaster'."*
- *"Bytt foto på slide 7 til den nye operatør-stasjonen-bildet jeg har lagt i mappen yara-training-assets/. Filen heter operator-chair-v2.jpg."*
- *"Slide 13 — endre 'Hive support hvis > 1 min' til 'Hive support hvis > 2 min' i alle radene som matcher."*
- *"Legg til en ny slide etter slide 15 som forklarer Phase 3-sertifiseringen mer detaljert."*
- *"Komprimer alle bilder under 500 KB."*
- *"Eksporter decken som PDF."*

### Etter du har gjort endringer

Test lokalt først:
```
open index.html
```

Hvis det ser bra ut, send filene tilbake til Ronny — han pusher til presentations.hiveautonomy.no.

## Filstruktur

```
yara-l120h/
├── index.html                    Selve decken (HTML + CSS + JS i én fil)
├── README.md                     Denne filen — for deg
├── AGENTS.md                     For Claude Code når du redigerer
└── yara-training-assets/
    ├── yara-hero.jpg             Forsidebilde
    ├── operator-chair.jpg        Slide 2, 7
    ├── retrofit.jpg              Slide 5 (sensors)
    ├── sensors.jpg               Slide 5 (alternative)
    ├── ops-centre.jpg            Slide 6
    ├── safety.jpg                Slide 9
    ├── yara-detail.jpg           Slide 17 (placeholder for Yara-installasjon)
    ├── miljo-hero.jpg            Slide 18 close
    ├── miljo-23.jpg, miljo-30.jpg, miljo-action.jpg   Reserve
    ├── joystick.jpg, hero.jpg    Reserve
    ├── hive-logo.png             Logo for lyse slides
    ├── hive-logo-white.png       Logo for mørke slides
    ├── yara-loader.mp4           Slide 14 video (Yara-loader, 14.6 MB)
    ├── yara-loader-still.jpg     Poster-bilde for video
    └── presis-vikafjellet.mp4    Reserve (Presis-video)
```

## Når trenger den oppdatering

| Når | Hva |
|---|---|
| Fase 2 starter | Tutorial-videoer for oppstart, E-stop, fault handling, HMI legges inn (slide 10, 11, 12, 13) |
| Yara-installasjon på plass | Slide 17 bilde byttes |
| HMI-design låst | Slide 12 wireframe byttes til ekte screenshot |
| Yara HSE-kontakter er bekreftet | Slide 16 navne/numre fylles inn |
| Software-release | Vurder om prosedyrer/feilmeldinger har endret seg |

## Spørsmål

Ronny — `liverod@gmail.com` · `+47 [TBC]`
Hive support — `+47 38 13 46 00` · `support@hiveautonomy.no`

# Portfolio — Quarto + GitHub Pages

Sito statico con [Quarto](https://quarto.org/), deploy automatico su GitHub Pages.

## Setup iniziale (una tantum)

### 1. Installa Quarto in locale

Scarica da <https://quarto.org/docs/get-started/> (Windows/Mac/Linux, gratuito).

Verifica:
```bash
quarto --version
```

### 2. Crea repo GitHub

1. Su GitHub, crea un repo **pubblico** chiamato `portfolio` (o come preferisci)
2. In locale:
   ```bash
   cd portfolio/
   git init
   git add .
   git commit -m "Initial portfolio scaffold"
   git branch -M main
   git remote add origin https://github.com/EugenioRss/portfolio.git
   git push -u origin main
   ```

### 3. Abilita GitHub Pages

1. Vai su **Settings → Pages** del repo
2. Source: **Deploy from a branch**
3. Branch: **gh-pages** / folder: **/ (root)** → Save
4. (Il branch `gh-pages` verrà creato automaticamente dalla GitHub Action al primo push)

### 4. Personalizza

Sostituisci ovunque trovi `EugenioRss`, `Eugenio Rossini`, `eu.rossini@gmail.com`, `eugenio-rossini`:
- `_quarto.yml`
- `index.qmd`
- `about.qmd`

Aggiungi:
- `assets/images/profile.jpg` — foto profilo (round, ~400x400)
- `assets/images/favicon.png` — favicon (32x32 o 64x64)
- `assets/images/placeholder.png` — thumbnail fallback dei progetti

## Workflow giornaliero

### Preview locale
```bash
quarto preview
```
Apre `http://localhost:XXXX` con hot reload.

### Aggiungere un nuovo progetto
```bash
cp projects/_template.qmd projects/aerospace/nome-progetto.qmd
# edita il nuovo file
```

Il front matter `categories:` controlla i tag mostrati nella listing.
Imposta `draft: true` finché il progetto non è pronto (sarà nascosto dal sito).

### Pubblicare
```bash
git add .
git commit -m "Add project: nome progetto"
git push
```

La GitHub Action si avvia, builda e deploya. Dopo ~2 minuti il sito è online su:
`https://EugenioRss.github.io/portfolio/`

## Struttura

```
portfolio/
├── _quarto.yml              ← config sito
├── index.qmd                ← homepage
├── about.qmd                ← bio + skills
├── styles.css               ← CSS custom
├── projects/
│   ├── index.qmd            ← listing con 3 sezioni
│   ├── _template.qmd        ← copia questo per nuovi progetti
│   ├── aerospace/
│   ├── industrial/
│   └── genai/
├── assets/
│   ├── images/              ← thumbnail, profilo, favicon
│   └── diagrams/            ← architetture (SVG da draw.io/Excalidraw)
└── .github/workflows/
    └── publish.yml          ← deploy automatico
```

## Domini personalizzati (opzionale, free)

Se in futuro vuoi un dominio tipo `tuonome.dev`:
1. Compralo (~10€/anno)
2. Aggiungi un file `CNAME` nella root con il dominio
3. Configura DNS come da [guida GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

Tutto il resto resta gratuito.

# Zora Films v5 — Cloudflare Pages / GitHub

**Arhitektura:** statički, već izgrađen Lovable export. Nema Vite/Bun/Nitro/Pages Functions builda.

## Postojeći projekt
- Cloudflare Pages projekt: `zora-films`
- GitHub repozitorij: `ZoraFilmsProduction/ZORA-FILMS`
- Branch: `main`
- Framework: `None`
- Build command: `exit 0` (ili prazno ako je postojeća postavka već uspješna)
- Build output directory: `public`
- Root directory: root repozitorija (prazno)
- Deployment: GitHub push na `main` pokreće novi build

## Zamjena v3 novim v5 buildom
1. U GitHub Desktopu odaberi **ZORA-FILMS** repozitorij i `main`.
2. Otvori `Repository > Show in Finder`.
3. U postojećem repozitoriju makni **staru mapu `public`** (ne kopirati nove datoteke preko nje bez čišćenja), zatim iz ovoga ZIP-a kopiraj **novu mapu `public`** i po želji `.gitignore`/ovaj dokument. Ostaviti `.git` netaknut.
4. Ako u korijenu starog repozitorija postoji **`functions/`**, ukloni je: v5 nema serversku kontaktnu funkciju. Također makni eventualne stare `wrangler.json`/`wrangler.toml` samo ako su iz ranije verzije i nisu potrebni trenutačno uspješnoj konfiguraciji, nakon provjere.
5. U GitHub Desktopu pregledaj promjene (stari asseti se uklanjaju, novi dodaju), napravi commit i `Push origin`.
6. Cloudflare > Workers & Pages > `zora-films` > Deployments: potvrdi **Success** najnovijeg `main` commita.
7. Testiraj `https://zora-films.pages.dev/`, `https://zora-films.pages.dev/contact` i svih 11 podstranica `/work/...` prije prebacivanja domene.

## Kontakt / e-mail
V5 nema kontaktni obrazac i ne šalje automatske e-mailove. Gumb i kontakt stranica koriste `mailto:production@zorafilms.com`; primanje ostaje preko Google Workspacea. `RESEND_API_KEY`, Supabase i e-mail Functions **nisu potrebni v5**. Ako postoje od prije, ne treba ih za ovaj v5, no brisanje DNS/MX zapisa nije potrebno i nije preporučeno.

## Namjerno nepromijenjeno
Sve 431 izvorne datoteke iz `Zora-Films-Cloudflare-Pages_v5.zip` byte-identične su u `public/`. Nisu dirani dizajn, fotografije, video, favicon, HTML, CSS, JS, fontovi ili linkovi. Nisu dodane nepotrebne funkcije, `_redirects`, `wrangler deploy` niti bilo kakva nova integracija.

## Provjere
- ZIP CRC: bez oštećenja.
- 13 HTML stranica, 19 JS, 371 slika i 10 videa: struktura, sintaksa odnosno dekodiranje provjereni.
- 671 lokalna HTML/CSS referenca: sve pronalaze datoteke ili predviđene Pages putanje.
- 431 statički asset: znatno ispod Pages limita broja datoteka.
- Najveća datoteka: <25 MiB, ispod Pages limita po datoteci.
- Automatski test u Chromiumu **nije izvršen** jer okruženje odbija lokalnu navigaciju `ERR_BLOCKED_BY_ADMINISTRATOR`. Live Cloudflare deployment i prikaz u stvarnom browseru potrebno je potvrditi nakon pusha.

## Domena
Ne dirati Google Workspace MX zapise. Novu v5 verziju najprije provjeriti na `.pages.dev` domeni, tek zatim objaviti/pozicionirati kao produkciju. Postojeći DNS za `zorafilms.com` i `www.zorafilms.com` treba zasebno provjeriti, ne pretpostavljati stanje.

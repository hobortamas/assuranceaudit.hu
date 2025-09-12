# Assurance Audit – feltöltési csomag

Ez a csomag egy **kész, statikus weboldal** sablont tartalmaz (magyar + angol), amit egyszerűen feltölthetsz a GitHub repository-dba, és a GitHub Pages segítségével azonnal elérhető lesz a `www.assuranceaudit.hu` címen.

## Mit tartalmaz a csomag?
- `index.html` — fő oldalfájl (könnyen szerkeszthető).
- `style.css` — stíluslap.
- `CNAME` — a saját domain neve (`www.assuranceaudit.hu`), így GitHub Pages-hez köthető.
- `README.md` — ez a fájl (magyarul).

## Előzetes lépés: mentés / biztonsági másolat
Ha már van tartalom a repository-dban, **ajánlott** biztonsági másolatot készíteni, mielőtt törölsz bármit.
- GitHub webes felület: `Code` → `Download ZIP` (letölti a jelenlegi tárolót).
- Git CLI: `git clone git@github.com:username/assuranceaudit.hu.git`

### Töröljem előtte az eddigi fájlokat?
- **Nem kötelező**, de erősen ajánlott, ha tiszta lappal szeretnél kezdeni (elkerülhetők a régi fájlok miatti ütközések, CNAME konfliktusok stb.).
- Két egyszerű lehetőség:
  1. **Web UI**: GitHub → repository → jelöld ki a fájlokat egyesével és töröld (minden törlés után commit). Ha sok fájl van, ez kényelmetlen.
  2. **Git CLI (ajánlott, gyors)**:
     ```bash
     git clone git@github.com:YOURUSERNAME/assuranceaudit.hu.git
     cd assuranceaudit.hu
     git rm -r *
     git commit -m "Remove old site to start fresh"
     git push origin main
     ```
  3. **(Alternatíva) Töröld a repository-t, majd hozd létre újra** — egyszerű megoldás, de elveszhetnek a repo kiegészítő adatai (issues, wiki) — csak akkor javasolt, ha nincs fontos tartalom.

## Feltöltés GitHub webes felülettel (gyors, kódismeret nélkül)
1. Menj a GitHub → `assuranceaudit.hu` repository → `Code` fül.
2. Kattints `Add file` → `Upload files`.
3. Húzd be a csomag fájljait (index.html, style.css, CNAME, README.md).
4. Commit (alul): írj egy üzenetet (pl. "Initial site upload") → `Commit changes`.
5. Menj a `Settings` → `Pages` pontra. Válaszd a `main` branch-et, root mappát, majd `Save`.
6. A `Custom domain` mezőbe írd be: `www.assuranceaudit.hu` (ha nincs CNAME fájl a repo-ban, itt megadható — de a csomagban már benne van).
7. Ha a DNS beállításaid helyesek (lásd lent), pipáld be az `Enforce HTTPS` opciót, amikor megjelenik.

## Feltöltés Git CLI-vel (ajánlott, profibb)
```bash
# clónozd le a repo-t
git clone git@github.com:YOURUSERNAME/assuranceaudit.hu.git
cd assuranceaudit.hu

# másold ide (vagy másold) a csomag fájljait ide, majd:
git add index.html style.css CNAME README.md
git commit -m "Initial site upload"
git push origin main
```

## DNS beállítások (Sybell DNS)
A GitHub Pages működéséhez a domain DNS-ét a tárhelyszolgáltatónál kell beállítanod (Sybell esetén a DNS zóna szerkesztőben):
- Gyökér domain (`assuranceaudit.hu`) A rekordok (GitHub Pages IP-jei):
  ```
  @  A  185.199.108.153
  @  A  185.199.109.153
  @  A  185.199.110.153
  @  A  185.199.111.153
  ```
- `www` CNAME rekord (irányítson a GitHub Pages felhasználói hostodra):
  ```
  www  CNAME  YOURUSERNAME.github.io.
  ```
**Megjegyzés:** a `YOURUSERNAME` helyére a GitHub-felhasználónevedet írd. A CNAME cél végén érdemes a pont (`.`) használata.

A DNS-frissülés eltarthat pár órától 48 óráig. Miután a DNS él, a GitHub Pages beállításoknál megjelenik az `Enforce HTTPS` opció — pipáld be.

## Gyakori hibák és tippek
- Ha korábban már volt CNAME fájl a repo-ban egy másik domainnel, lehet, hogy ütközés történik. Ellenőrizd a `CNAME` fájlt és győződj meg róla, hogy `www.assuranceaudit.hu` szerepel benne.
- Ha nem szeretnél gyökérdomainről (`assuranceaudit.hu`) működtetni a weboldalt, elég csak a `www` aldomain.
- Célszerű előbb feltölteni az `index.html` tartalmát és ellenőrizni a GitHub Pages URL-t (pl. `https://YOURUSERNAME.github.io/assuranceaudit.hu/`), majd utána beállítani a saját domaint.

---
Ha szeretnéd, segíthetek a DNS beállítások ellenőrzésében (mondj egyet-kettőt, amit a Sybell adminban látsz), vagy végigvezetlek a GitHub feltöltésen lépésről lépésre.

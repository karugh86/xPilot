
# xPilot Demo (Option A: Vercel + Neon)

**Ziel:** In wenigen Schritten eine verkaufsreife Demo (mit Testdaten) online stellen.

## 1) Voraussetzungen
- Vercel-Account (GitHub Login).
- Neon (Postgres) – Free-Tier.
- (Optional) Mailtrap/Resend für E-Mail-Login. Für die Demo ist kein Login notwendig.

## 2) Deploy-Schritte (idiotensicher)

### A) Repo bereitstellen
1. GitHub → New Repository → **xpilot** (Public oder Private).
2. „Upload files“ → gesamten Inhalt dieses Projekts hochladen.
3. Committen.

### B) Neon-DB anlegen
1. https://neon.tech → „New Project“.
2. `DATABASE_URL` kopieren.

### C) Vercel Projekt importieren
1. https://vercel.com → „New Project“ → Importiere dein GitHub-Repo.
2. **Root Directory** = `apps/web` (im Import-Dialog einstellen).
3. Environment Variables setzen:
```
DATABASE_URL=<<von Neon>>
NEXTAUTH_URL=https://<dein-projekt>.vercel.app
EMAIL_SERVER=smtp://username:password@smtp.host:587
EMAIL_FROM="xPilot Demo <no-reply@xpilot.local>"
DEFAULT_TENANT=demo-werke-gmbh
DEMO_DEV_LOGIN=true
```
4. Build startet automatisch. (Build-Script führt `prisma generate` und `prisma migrate deploy` aus.)

### D) Demo-Daten anlegen
1. Öffne die Vercel-URL (z. B. `https://xpilot-demo.vercel.app`).
2. Auf der Startseite „**Demo-Daten anlegen**“ klicken (POST `/api/v1/setup`).

## 3) Inhalte
- **Assets**: DEMO-L100 (Linie), DEMO-P101 (Pumpe) inkl. Zähler.
- **Work Orders**: 5 WOs in allen Status.
- **Maintenance Plans**: Zeit & Nutzung.
- **Mandant**: `demo-werke-gmbh` mit Demo-Banner.

## 4) Hinweise
- Keine urheberrechtlich geschützten Inhalte;
- Multi-Tenant vorbereitet (DEFAULT_TENANT), Wildcard-Subdomains später;
- Weitere Module (Inventory/Reservierung, Checklists Offline, White-Label-Mails, Webhooks) folgen in der nächsten Iteration.

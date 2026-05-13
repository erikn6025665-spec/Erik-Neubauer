# ElektroPlaner Global SaaS

Produktionsnahes Next.js-SaaS-Projekt für eine weltweit nutzbare Elektroplanungs-Plattform.

## Enthalten
- Professionelles globales Redesign
- Supabase Auth für echtes Login/Register
- Stripe Checkout für kostenpflichtige Monatsabos
- Stripe Webhook zur Aktivierung des Dashboard-Zugangs
- Geschütztes Dashboard
- Serverseitig wiederverwendbare echte Vorplanungs-Berechnungen: Strom, Sicherung, Kabelquerschnitt, Spannungsfall
- Supabase Tabellen mit Row Level Security
- Projekt-Speicherung pro Benutzer

## Setup
1. `npm install`
2. `.env.example` zu `.env.local` kopieren und echte Werte eintragen
3. In Supabase SQL Editor `supabase/schema.sql` ausführen
4. In Stripe ein Produkt + monatlichen Preis erstellen und Price ID eintragen
5. Stripe Webhook auf `/api/stripe/webhook` setzen mit Events:
   - `checkout.session.completed`
   - `customer.subscription.updated`
   - `customer.subscription.deleted`
6. Lokal starten: `npm run dev`
7. Deployment: Vercel verbinden, Environment Variables setzen, Domain verbinden

## Wichtig
Diese Software erstellt professionelle Vorplanungswerte. Sie ersetzt keine Elektrofachkraft und keine lokale Normenprüfung. Vor Installation müssen RCD/GFCI, Abschaltbedingungen, Verlegeart, Häufung, Temperatur, Spannungsfall, Selektivität, Erdungssystem und lokale Vorschriften geprüft werden.


## Advanced Engineering Suite
Neue Route: `/dashboard/advanced`

Enthaltene Erweiterungen:
- CAD-Import-Workflow mit Symbol-/Textanalyse als API-Vorbereitung (`/api/advanced/cad`)
- automatische Stromlauf-/Single-Line-Vorplanung aus Stromkreislasten
- BIM-Datenmodell für IFC/Revit-Property-Sets (`/api/advanced/bim`)
- PV- und Wallbox-Vorplanung mit Peak-Load- und Jahresertragslogik (`/api/advanced/pv-wallbox`)
- AI-Agenten-Workflow für Lasten, Stromkreise, Norm-Checkliste und Dokumentation (`/api/advanced/agents`)
- Mobile/PWA-Vorschau unter `/mobile`
- internationale Norm-Workflows für IEC, DIN VDE, OVE, NIN, BS 7671, NEC, CEC und AS/NZS

### Realistische Produktionshinweise
DWG/DXF/IFC-Dateien sind komplexe technische Formate. Dieses Paket enthält die SaaS-Architektur, Datenmodelle, API-Routen und vorbereitete Analyse-Workflows. Für echte Datei-Parser sollten später spezialisierte CAD/BIM-Services oder Serverbibliotheken angebunden werden. Alle Ergebnisse bleiben Vorplanung und benötigen Prüfung durch eine Elektrofachkraft.

## Neu: Safety & Compliance Precheck
Die normale Elektroberechnung enthält jetzt zusätzlich eine automatische Vorprüfung für:
- RCD/GFCI-Konzept und Typ
- Abschaltbedingungen / Fault-Loop-Impedanz / Abschaltzeit
- Verlegeart, Häufung und Umgebungstemperatur-Derating
- Spannungsfall gegen den gewählten Grenzwert
- Selektivität über Upstream-/Main-Breaker-Werte
- Erdungssystem TN-S, TN-C-S, TT, IT, TN-C
- Kurzschlussfestigkeit: PSCC gegen Geräteschaltvermögen
- lokale Vorschriften / bestätigte Normenprüfung

Wichtig: Diese Prüfung erzeugt Ampel-/Risikohinweise und blockierende Review-Punkte. Sie ersetzt keine Elektrofachkraft, keine Messung und keine lokale Abnahme.

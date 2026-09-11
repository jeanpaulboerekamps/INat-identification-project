# iNaturalist Identification Project Dashboard — v2

Een statische webapp die iNaturalist-**identificaties** centraal stelt in plaats van observaties.

## Starten

Gebruik bij voorkeur een lokale webserver:

```bash
cd inat-identification-dashboard
python3 -m http.server 8000
```

Open daarna `http://localhost:8000`.

## Nieuw in v2

- taxon zoeken op naam via `/v1/taxa/autocomplete`
- gebied zoeken op naam via `/v1/places/autocomplete`
- deelbare project-URL's waarin alle filters zijn opgenomen
- iNaturalist-achtige projectheader, tabs, KPI's en ranglijsten
- normale snelle dashboardmodus met API-aggregaties + 200 recente IDs
- **Volledige analyse** die rustig door identificaties pagineert
- nauwkeurige unieke observatietelling en volledige tijdreeks tot 10.000 IDs
- activiteit wordt automatisch per dag, week of maand gebucket afhankelijk van de periode
- CSV-export gebruikt de volledige dataset wanneer die geladen is
- projecten lokaal opslaan in `localStorage`

## Filters

- datum waarop de identificatie is aangemaakt (`d1`, `d2`)
- taxon
- iNaturalist place
- identifier / user ID
- improving / leading / supporting / maverick
- IDs op eigen observaties wel/niet meenemen
- alleen huidige IDs

## API-routes

De app gebruikt de openbare iNaturalist v1 API:

- `/identifications`
- `/identifications/categories`
- `/identifications/identifiers`
- `/identifications/species_counts`
- `/taxa/autocomplete`
- `/places/autocomplete`

Requests voor dashboards en volledige analyse worden bewust na elkaar uitgevoerd met ongeveer één seconde pauze om de publieke API niet onnodig te belasten.

## Limiet volledige analyse

De browserversie stopt bewust bij 10.000 identificaties. Dat voorkomt dat één dashboard tientallen of honderden API-calls veroorzaakt. Bij grotere projecten is een kleine backend met caching de betere architectuur.

## Logische productieversie

Een productieversie kan een FastAPI/Node-backend toevoegen voor server-side caching, volledige aggregaties zonder browserlimiet, permanente project-slugs, gebruikersaccounts/OAuth, gedeelde projecten en periodieke snapshots.

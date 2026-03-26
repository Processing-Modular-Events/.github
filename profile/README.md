# Processing Modular Events

**Plateforme de traitement d'evenements modulaire** — Un moteur event-driven avec un systeme de modules ouvert, inspire d'Obsidian et Grafana.

---

## Comment ca marche

Un **core** ingere des evenements en temps reel via Apache Kafka. Des **modules** independants se greffent dessus pour traiter ces evenements — detection de fraude, analytics, metriques, ou n'importe quelle logique metier.

N'importe quel developpeur peut creer son propre module en important le SDK (`pme-sdk`).

```
Evenement -> Core (Kafka + Elasticsearch) -> Modules (plug-and-play)
```

## Repositories

| Repo | Description | |
|------|-------------|---|
| [`pme-sdk`](https://github.com/Processing-Modular-Events/pme-sdk) | SDK pour developper des modules | ![Public](https://img.shields.io/badge/-public-brightgreen) |
| [`pme-core`](https://github.com/Processing-Modular-Events/pme-core) | Moteur — Spring Boot, Kafka, Elasticsearch | ![Private](https://img.shields.io/badge/-private-red) |
| [`pme-module-fraud`](https://github.com/Processing-Modular-Events/pme-module-fraud) | Module de detection de fraude | ![Private](https://img.shields.io/badge/-private-red) |
| [`pme-module-analytics`](https://github.com/Processing-Modular-Events/pme-module-analytics) | Module d'agregation et d'analyse | ![Public](https://img.shields.io/badge/-public-brightgreen) |
| [`pme-module-metrics`](https://github.com/Processing-Modular-Events/pme-module-metrics) | Module de metriques temps reel | ![Public](https://img.shields.io/badge/-public-brightgreen) |
| [`pme-docs`](https://github.com/Processing-Modular-Events/pme-docs) | Documentation SDK (MkDocs) | ![Public](https://img.shields.io/badge/-public-brightgreen) |

## Architecture

```mermaid
graph TB
    SDK["pme-sdk\nEventModule · EventContext\nEvent · ModuleConfig"]
    CORE["pme-core\nREST API · Kafka · Elasticsearch\nModule Loader"]

    SDK -->|depends on| FRAUD[Fraud]
    SDK -->|depends on| ANALYTICS[Analytics]
    SDK -->|depends on| METRICS[Metrics]
    SDK -->|depends on| YOURS[Your module]

    CORE -->|loads| FRAUD
    CORE -->|loads| ANALYTICS
    CORE -->|loads| METRICS
    CORE -->|loads| YOURS
```

## Stack

Java 25 · Spring Boot 3.x · Apache Kafka · Elasticsearch · Kibana · Docker

## Licence

MIT — Built by [@capellegab](https://github.com/capellegab)

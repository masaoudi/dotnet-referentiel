# 🗄️ Data & Bases de données

SQL Server, MySQL, Lucene, ClickHouse.

## Bases relationnelles

### SQL Server

- Base de données Microsoft
- **T-SQL**
- Versions : 2008, 2019, 2022
- Outils : SSMS, Azure Data Studio

### MySQL

- Base open-source
- Très populaire sur le web
- Moteurs : InnoDB, MyISAM
- Outils : MySQL Workbench

## Bases non relationnelles

### Lucene

- Moteur de recherche **full-text**
- Index inversé
- Base de Lucene : Elasticsearch, Solr
- Recherche rapide dans gros volumes

### ClickHouse

- Base **colonnaire OLAP**
- Très rapide pour analytics
- Traitement de milliards de lignes
- Idéal pour reporting temps réel

## Relationnel vs Non relationnel

| Critère | Relationnel (SQL) | Non relationnel (NoSQL) |
|---------|:-----------------:|:-----------------------:|
| Schéma | Fixe, tabulaire | Flexible |
| Requêtes | SQL | API spécifique |
| Transactions | ACID | BASE (souvent) |
| Scalabilité | Verticale | Horizontale |
| Cas d'usage | Données structurées | Big Data, temps réel |
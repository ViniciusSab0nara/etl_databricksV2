# 🛒 E-Commerce End-to-End Data Pipeline: AWS S3 + Databricks + Power BI

Pipeline de engenharia de dados ponta a ponta construído com foco no processamento de dados semiestruturados (JSON) de uma plataforma de e-commerce. O projeto abrange desde a simulação controlada de eventos e transações até a construção de um Lakehouse baseado na Arquitetura Medallion (Delta Lake) e modelagem dimensional Star Schema para consumo analítico no Power BI.

---

## 📌 Visão Geral da Arquitetura

O ecossistema foi projetado para simular o fluxo real de dados de uma empresa moderna de varejo digital:

```text
[ Data Generator ] ──> [ AWS S3 (Raw JSON) ]
                               │
                               ▼
                    ┌─────────────────────┐
                    │     DATABRICKS      │
                    │                     │
                    │   🥉 Bronze Layer   │ (Raw Delta, Schema Enforcement)
                    │          │          │
                    │          ▼          │
                    │   🥈 Silver Layer   │ (Deduplicação, Parsing de JSON, Data Quality)
                    │          │          │
                    │          ▼          │
                    │   🥇 Gold Layer     │ (Star Schema: Fatos e Dimensões)
                    └─────────────────────┘
                               │
                               ▼
                     [ POWER BI DASHBOARD ] (DirectQuery / Import via Databricks Connector)

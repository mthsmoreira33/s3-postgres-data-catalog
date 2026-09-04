# S3 to PostgreSQL Metadata Catalog Pipeline

Pipeline de dados desenvolvido em Python para catalogar e inventariar metadados de arquivos brutos armazenados no Amazon S3 em um banco de dados relacional PostgreSQL hospedado no AWS RDS.

---

## 🏗️ Arquitetura da Solução

```text
[ Amazon S3 ]               [ Google Colab / Python ]             [ AWS RDS ]
 Camada Bruta       --->       Script de Ingestão         --->    PostgreSQL
(Bucket/Imagens)              (Boto3 + Psycopg2)                 (Tabela de Catálogo)

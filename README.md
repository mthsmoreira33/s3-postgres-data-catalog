# S3 to PostgreSQL Metadata Catalog Pipeline

Pipeline de dados desenvolvido em Python para catalogar e inventariar metadados de arquivos brutos armazenados no Amazon S3 em um banco de dados relacional PostgreSQL hospedado no AWS RDS.

---

## 🏗️ Arquitetura da Solução

```text
[ Amazon S3 ]               [ Google Colab / Python ]             [ AWS RDS ]
 Camada Bruta       --->       Script de Ingestão         --->    PostgreSQL
(Bucket/Imagens)              (Boto3 + Psycopg2)                 (Tabela de Catálogo)
```

### 1 - Camada de Armazenamento (Amazon S3): Armazena os arquivos/imagens na nuvem de forma desacoplada da camada computacional.

### 2 - Camada de Ingestão e Processamento (Python): Lista os objetos contidos no bucket/prefixo via SDK boto3, extrai os nomes dos arquivos e estabelece a conexão com a base relacional.

### 3 - Camada Relacional (AWS RDS PostgreSQL): Criação da tabela e persistência dos metadados (id, nome_arquivo) via comandos DML (INSERT) gerenciados por transação (COMMIT).

### 🛠️ Tecnologias Utilizadas

- Python 3
- Boto3 (SDK da AWS para Python)
- Psycopg2-binary (Driver de conexão PostgreSQL)
- Amazon S3 (Object Storage)
- AWS RDS (Instância PostgreSQL gerenciada)

### 📋 Estrutura da Tabela no PostgreSQL
```SQL
CREATE TABLE IF NOT EXISTS catalogo_imagens (
    id SERIAL PRIMARY KEY,
    nome_arquivo VARCHAR(255) NOT NULL
);
```

### 🚀 Como Executar
1. Clonar o repositório
```Bash
git clone https://github.com/<seu-usuario>/s3-postgres-data-catalog.git
cd s3-postgres-data-catalog
```

2. Instalar dependências
```Bash
pip install -r requirements.txt
```

3. Configurar variáveis e executar
Configure suas credenciais da AWS e os parâmetros de conexão do banco diretamente nas variáveis de ambiente ou no script e execute:

```Bash
python pipeline.py
```
Snippet de código

---

### Comandos Git para subir o projeto

Execute no diretório onde estão seus arquivos locais:

```bash
git init
git add .
git commit -m "feat: implementacao do pipeline de catalogacao S3 para RDS Postgres"
git branch -M main
git remote add origin https://github.com/<seu-usuario>/<nome-do-repositorio>.git
git push -u origin main
```

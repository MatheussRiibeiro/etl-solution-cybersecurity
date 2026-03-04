# NVD Threat Intelligence ETL Pipeline

## Objetivo do Projeto
Este projeto consiste em um pipeline de Engenharia de Dados de ponta a ponta projetado para coletar, limpar e estruturar dados diários de vulnerabilidades (CVEs) divulgados pelo National Vulnerability Database (NVD/NIST). 

O objetivo é fornecer uma base de dados limpa, atualizada e confiável (Single Source of Truth) para times de Segurança da Informação (Blue Team/SOC) realizarem análises de risco, cruzamento de dados de ameaças e monitoramento de softwares afetados.

## Arquitetura de Dados (Medalhão)
O pipeline adota as melhores práticas da **Arquitetura Medalhão**, garantindo a rastreabilidade e a qualidade dos dados:

- **Camada Bronze (Raw):** Ingestão incremental dos dados brutos em formato `JSON` diretamente da API do NVD, preservando o histórico original sem alterações.
- **Camada Silver (Cleansed):** Processamento e "achatamento" (flattening) dos dados complexos utilizando Python (Pandas). Remoção de metadados desnecessários, tipagem correta e conversão para formato colunar otimizado (`CSV`/`Parquet`).
- **Camada Gold (Curated):** Carregamento dos dados refinados em um Banco de Dados Relacional, modelados para consultas analíticas rápidas e integração com ferramentas de visualização ou SIEM.

## Stack Tecnológico
* **Orquestração:** Apache Airflow
* **Linguagem & Processamento:** Python 3, Pandas, Requests
* **Containerização:** Docker & Docker Compose
* **Cloud Storage (Data Lake):** Microsoft Azure (Blob Storage / ADLS Gen2)
* **Banco de Dados:** PostgreSQL / Azure SQL (Camada Gold)

## Como Executar o Projeto (Localmente)

### Pré-requisitos
* Docker e Docker Desktop instalados.
* Conta na Microsoft Azure (com Storage Account configurada).
* Python 3.10+ para testes locais.

### Passos
1. Clone o repositório:
   ```bash
   git clone [https://github.com/SeuUsuario/nvd-etl-pipeline.git](https://github.com/SeuUsuario/nvd-etl-pipeline.git)
   cd nvd-etl-pipeline
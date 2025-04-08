# MDS lab: Agnostic Data Platform

<h1 align="center">
  <a
    target="_blank"
    href="https://github.com/guaradata/mds-lab"
  >
    <img
      align="center"
      alt="Arquitetura de dados monderna"
      src="https://github.com/guaradata/mds-lab/blob/main/docs/img/mds-lab.jpg?raw=true"
      style="height: 50%;"
    />
  </a>
</h1>

## 🧙 Introdução

### O que é Modern Data Stack (MDS)?

Conhecido em português como "Pilha de Dados Moderna" ou "Arquitetura de Dados Moderna", o MDS representa um ecossistema de tecnologias projetadas para otimizar o gerenciamento, processamento e análise de dados em escala. Neste contexto, a arquitetura apresentada utiliza componentes-chave como MinIO (armazenamento objeto compatível com S3), PostgreSQL (metadados do Hive), Apache Hive (metastore e consultas SQL), Apache Spark (processamento distribuído), Kyuubi (gateway SQL para Spark), JupyterLab (análise interativa) e Dremio (camada semântica e aceleração de consultas).

Essa combinação reflete os princípios do MDS: escalabilidade (com workers Spark distribuídos), flexibilidade (integração entre ferramentas open-source) e governança (metadados centralizados no Hive Metastore). Ao adotar containers Docker, a stack também garante portabilidade e isolamento, permitindo que pipelines de dados sejam executados desde ingestão (MinIO) até análise (Jupyter/Dremio) em um ambiente unificado.

### Destaques da arquitetura

- **Camada de Armazenamento:** MinIO como repositório econômico e compatível com cloud.

- **Metadados:** PostgreSQL + Hive Metastore para rastreabilidade de tabelas.

- **Processamento:** Spark com cluster multi-worker para paralelização de tarefas.

- **Acesso e Análise:** JupyterLab (notebooks), Kyuubi (SQL via Spark), e Dremio (otimização de queries).

Essa pilha é especialmente adequada para cenários que demandam dados lakehouse, combinando recursos de data lakes (armazenamento flexível) com warehouses (gestão estruturada).

## 📌 Objetivos

### Visão Geral

Este projeto implementa uma **Pilha de Dados Moderna (Modern Data Stack - MDS)** simplificada usando containers Docker, destinada exclusivamente para:

- Aprendizado de arquiteturas de dados modernas
- Experimentação com ferramentas open-source
- Desenvolvimento de habilidades em engenharia e análise de dados

### 🛠 Componentes da Stack

| Ferramenta         | Função Principal                          | Porta  | Observações                          |
|--------------------|------------------------------------------|-------|--------------------------------------|
| **MinIO**          | Armazenamento objeto (S3-compatível)     | 9000  | Bucket padrão: `wba`                 |
| **PostgreSQL**     | Metastore do Hive                        | 5432  | Usuário/senha: `admin`               |
| **Hive Metastore** | Gerenciamento de metadados               | 9083  | Integrado com MinIO e Spark          |
| **Spark Cluster**  | Processamento distribuído (1 master + 3 workers) | 7077, 8080 | 5GB memória por worker         |
| **JupyterLab**     | Análise interativa                       | 8888  | Pré-configurado com Spark            |
| **Dremio**         | Camada semântica e aceleração de queries | 9047  | Conecta a MinIO e Hive               |
| **Kyuubi**         | Gateway SQL para Spark                   | 10009 | Alternativa ao Hive Server           |

### ⚠️ Limitações Intencionais (Fins Educacionais)

- **Autenticação simplificada**: Credenciais padrão em todos serviços
- **Recursos limitados**: Configuração mínima para rodar em máquinas locais
- **Sem HA/Failover**: Single-point-of-failure em vários componentes
- **Sem monitoramento**: Não inclui Prometheus/Grafana

## 🎯 Casos de Estudo Recomendados

1. **Pipeline ETL Básico**
   - Ingestão de dados CSV para MinIO
   - Criação de tabelas no Hive Metastore
   - Transformação com Spark (Jupyter ou PySpark)

2. **Comparativo de Performance**
   - Queries SQL via Hive Server vs Kyuubi vs Dremio
   - Impacto do número de workers Spark

3. **Governança de Metadados**
   - Rastreamento de linhagem de dados
   - Evolução de schemas (schema evolution)

/opt/kyuubi/externals/spark-3.5.2-bin-hadoop3/bin/spark-submit --version

## Ferramentas base

- [Docker Desktop](https://www.docker.com/get-started);
- [Git](https://git-scm.com/downloads).

## 🥶 Referências

### Repositórios

- [1] - <https://github.com/kemonoske/spark-minio-delta-lakehouse-docker>
- [2] - <https://github.com/dgkatz/trino-hive-superset-docker>
- [3] - <https://github.com/le-oasis/docker-airflow-spark>
- [4] - <https://github.com/kemonoske/spark-minio-delta-lakehouse-docker>
- [5] - <https://github.com/cluster-apps-on-docker/spark-standalone-cluster-on-docker>
- [6] - <https://github.com/experientlabs/spark-dp-101>
- [7] - <https://github.com/experientlabs/spark_delta_hive_metastore>
- [8] - <https://github.com/elijahfhopp/simple-superset-compose>
- [9] - <https://github.com/wlcamargo/spark_opensource_vs_proprietary>
- [10] - <https://github.com/pcbimon/spark-minio-delta-lakehouse-docker>
- [11] - <https://github.com/edvaldo-gutierres/data-lab>
- [12] - <https://github.com/guaradata/etl-mds-marketing>

### Artigos

- [1] - <https://medium.com/@MarinAgli1/setting-up-a-spark-standalone-cluster-on-docker-in-layman-terms-8cbdc9fdd14b>
- [2] - <https://medium.com/@sanjeets1900/hadoop-hive-and-hue-with-postgress-metastore-from-scratch-fd4425d13831>
- [3] - <https://medium.com/@mariusz_kujawski/cloud-agnostic-data-platform-3aedd6d0eb3b>

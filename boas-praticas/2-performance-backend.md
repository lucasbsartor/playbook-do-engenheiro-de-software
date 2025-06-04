# 🚀 Performance de Backend: Um Guia Prático para Engenheiros

> **Backends rápidos, escaláveis e resilientes**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

## 📚 Índice

- [🚀 1. Princípios Fundamentais](#-1-princípios-fundamentais)
- [🗄️ 2. Estratégias de Cache](#-2-estratégias-de-cache)
- [🛢️ 3. Otimização de Banco de Dados](#-3-otimização-de-banco-de-dados)
- [🌐 4. Otimização de Rede](#-4-otimização-de-rede)
- [📦 5. Otimização de Respostas de API](#-5-otimização-de-respostas-de-api)
- [⚙️ 6. Processamento Assíncrono](#-6-processamento-assíncrono)
- [🏗️ 7. Balanceamento de Carga e Escalabilidade](#-7-balanceamento-de-carga-e-escalabilidade)
- [🧑‍💻 8. Otimização de Código e Arquitetura](#-8-otimização-de-código-e-arquitetura)
- [📈 9. Monitoramento e Log](#-9-monitoramento-e-log)
- [🧪 10. Testes de Performance](#-10-testes-de-performance)
- [📖 11. Leituras e Recursos Adicionais](#-11-leituras-e-recursos-adicionais)

---

## 🚀 1. Princípios Fundamentais

- **Meça Primeiro, Otimize Depois:** Use ferramentas de profiling e monitoramento para encontrar gargalos reais antes de alterar o código.
- **Foque no Caminho Crítico:** Priorize as operações mais frequentes e sensíveis à latência.
- **Projete para Escalabilidade:** Prefira escalabilidade horizontal (adicionar mais servidores) a apenas tornar componentes individuais mais rápidos.
- **Reduza Trabalho Desnecessário:** Elimine cálculos e transferências de dados redundantes.
- **Use Tracing Distribuído:** Acompanhe requisições entre serviços para identificar onde a latência se acumula.

**🔑 Principais Lições:**

- Sempre meça antes de otimizar—dados superam a intuição.
- Foque primeiro nos gargalos mais impactantes.
- Projete para escalabilidade e resiliência desde o início.

---

## 🗄️ 2. Estratégias de Cache

**Cache é sua primeira linha de defesa contra backends lentos.**

- **Cache em Camadas:**
  - **Cache HTTP:** Use headers como `Cache-Control`, `ETag` e `Last-Modified`.
  - **Cache em Nível de Aplicação:** Use Redis, Memcached ou caches em memória para dados "quentes".
  - **Cache de Banco de Dados:** Aproveite caches internos do banco ou do ORM.
  - **CDN:** Sirva conteúdo estático e dinâmico próximo dos usuários.
- **Escolha o Padrão Certo:**
  - **Cache-Aside (Lazy Loading):** Carrega no cache sob demanda. Ótimo para leituras intensas.
  - **Write-Through:** Escreve no cache e no banco ao mesmo tempo. Garante consistência.
  - **Write-Back:** Escreve no cache e depois, de forma assíncrona, no banco. Rápido, mas mais arriscado.
  - **Read-Through:** O cache busca no banco se faltar o dado.
- **Invalide de Forma Eficiente:**
  - **TTL (Time-To-Live):** Defina expiração para entradas do cache.
  - **Event-Driven:** Invalide quando os dados mudarem.
  - **Chaves Versionadas:** Altere as chaves do cache quando os dados forem atualizados.
- **Aqueça o Cache:** Preencha o cache com dados críticos na inicialização ou em horários de baixo uso.

**🧑‍💻 Exemplo: Padrão Cache-Aside (Python + Redis)**

```python
import redis
import json

def fetch_user_from_db(user_id):
    # Simula busca no banco
    return {"id": user_id, "name": "Alice"}

cache = redis.Redis(host='localhost', port=6379)

def get_user(user_id):
    key = f"user:{user_id}"
    data = cache.get(key)
    if data:
        return json.loads(data)
    user = fetch_user_from_db(user_id)
    if user:
        cache.setex(key, 3600, json.dumps(user))
        return user
    return None
```

**⚠️ Armadilhas Comuns:**

- Esquecer de definir TTL pode gerar cache desatualizado ou inchado.
- Não tratar cache stampede (muitos acessos simultâneos a dados ausentes).
- Não invalidar ou atualizar o cache quando os dados mudam.
- Cachear dados dinâmicos ou específicos de usuário em excesso.

**⚡ Ganhos Rápidos:**

- Adicione cache aos dados mais acessados primeiro.
- Use TTLs para evitar dados desatualizados e excesso de uso de memória.
- Aqueça o cache para endpoints críticos após deploys.

---

## 🛢️ 3. Otimização de Banco de Dados

**Bancos de dados costumam ser o principal gargalo—otimize-os cedo e com frequência.**

- **Pool de Conexões:**
  - Reutilize conexões para reduzir overhead.
  - Ajuste tamanho do pool e timeouts conforme a carga.
- **Indexação:**
  - Indexe colunas frequentemente consultadas, mas evite excesso de índices.
  - Use índices parciais para tabelas grandes.
- **Otimização de ORM:**
  - Analise queries geradas.
  - Use lazy/eager loading com sabedoria para evitar N+1.
  - Faça operações em lote para reduzir idas ao banco.
- **Otimização de Queries:**
  - Evite `SELECT *`—busque apenas as colunas necessárias.
  - Use paginação eficiente (prefira cursor para grandes volumes).
  - Otimize JOINs e considere desnormalizar para leituras intensas.
  - Limpe dados antigos e mantenha índices regularmente.
- **Escalabilidade e Resiliência:**
  - Use replicação para leitura e recuperação de desastres.
  - Faça sharding ou particionamento para grandes volumes.
- **Monitoramento:**
  - Ative logs de queries lentas e revise-os.
  - Use ferramentas como `EXPLAIN ANALYZE` para entender planos de execução.

**🧑‍💻 Exemplo: Paginação Eficiente (SQL)**

```sql
-- Por offset (simples, mas lento para grandes offsets)
SELECT id, name FROM users ORDER BY id LIMIT 20 OFFSET 1000;
-- Por cursor (preferido para grandes volumes)
SELECT id, name FROM users WHERE id > :last_seen_id ORDER BY id LIMIT 20;
```

**⚠️ Armadilhas Comuns:**

- Excesso de índices, que prejudica escritas.
- Usar SELECT \* ao invés de buscar só o necessário.
- Ignorar logs de queries lentas e não tunar queries.
- Não monitorar exaustão do pool de conexões.
- Confiar apenas nos padrões do ORM sem analisar o SQL gerado.

**🔑 Principais Lições:**

- Use pool de conexões e indexação adequada para ganhos imediatos.
- Evite SELECT \* e queries N+1—busque só o que precisa.
- Revise logs de queries lentas e otimize queries regularmente.

---

## 🌐 4. Otimização de Rede

- **Hospede Perto dos Usuários:** Implemente serviços em regiões próximas dos usuários.
- **Habilite HTTP Keep-Alive:** Reutilize conexões TCP para múltiplas requisições.
- **Use CDNs:** Sirva conteúdo estático e dinâmico cacheável a partir de edge locations.
- **Prefetch/Preload de Recursos:** Use hints do navegador para reduzir latência percebida.

**⚠️ Armadilhas Comuns:**

- Não habilitar keep-alive, causando excesso de handshakes TCP.
- Servir todo conteúdo de uma única região, aumentando latência para usuários distantes.
- Não usar CDN para assets estáticos.
- Exagerar no prefetch/preload, desperdiçando banda.

**⚡ Ganhos Rápidos:**

- Hospede serviços próximos dos usuários e habilite keep-alive.
- Use CDN para conteúdo estático e dinâmico cacheável.
- Prefetch/preload de recursos para performance percebida mais rápida.

---

## 📦 5. Otimização de Respostas de API

- **Limite Tamanho dos Payloads:** Restrinja tamanhos de requisições e respostas.
- **Habilite Compressão:** Use GZIP ou Brotli para respostas textuais.
- **Paginação Eficiente:** Use paginação por cursor para grandes listas.
- **Otimize Endpoints Pesados:**
  - Pré-calcule ou cacheie resultados.
  - Desloque tarefas pesadas para jobs em background.
  - Faça streaming de respostas grandes quando possível.
- **Considere GraphQL/gRPC:** Para APIs complexas, podem reduzir over-fetching e melhorar eficiência.

**🧑‍💻 Exemplo: Habilitando GZIP no Express (Node.js)**

```js
const express = require("express");
const compression = require("compression");
const app = express();
app.use(compression());
```

**⚠️ Armadilhas Comuns:**

- Esquecer de habilitar compressão para respostas textuais.
- Retornar payloads grandes sem paginação.
- Não validar ou limitar tamanhos de requisições recebidas.
- Over-fetching de dados nas respostas da API.

**🔑 Principais Lições:**

- Comprima todas as respostas textuais (GZIP/Brotli).
- Limite payloads e pagine grandes respostas.
- Cacheie ou pré-calcule resultados pesados sempre que possível.

---

## ⚙️ 6. Processamento Assíncrono

- **Desloque Tarefas Pesadas:** Use jobs em background para tarefas lentas ou não críticas (ex: processamento de imagens, e-mails).
- **Use Message Brokers:** RabbitMQ, Kafka ou AWS SQS para comunicação assíncrona confiável.

**🧑‍💻 Exemplo: Tarefa em Background com Celery (Python)**

```python
from celery import Celery
app = Celery('tasks', broker='redis://localhost:6379/0')

@app.task
def process_image(path):
    # ...processamento pesado...
    return "done"

# Na sua API:
def upload(file):
    save(file)
    process_image.delay(file.path)
    return "Processing started"
```

**⚠️ Armadilhas Comuns:**

- Não tratar falhas ou retries em jobs de background.
- Bloquear respostas da API esperando tarefas assíncronas.
- Não monitorar tamanho das filas ou saúde dos workers.
- Usar processamento assíncrono para tarefas que exigem consistência imediata.

**⚡ Ganhos Rápidos:**

- Desloque tarefas pesadas ou lentas para jobs em background imediatamente.
- Use message broker para processamento assíncrono confiável.
- Monitore tamanho das filas para identificar gargalos cedo.

---

## 🏗️ 7. Balanceamento de Carga e Escalabilidade

- **Escalabilidade Horizontal:** Adicione mais instâncias para serviços stateless.
- **Escalabilidade Vertical:** Aumente recursos de servidores individuais (use com moderação).
- **Load Balancers:** Use Nginx, HAProxy ou balanceadores de nuvem para distribuir tráfego.
- **Health Checks:** Remova instâncias não saudáveis automaticamente da rotação.

**🧑‍💻 Exemplo: Load Balancer Simples com Nginx**

```nginx
http {
  upstream backend {
    server backend1.example.com;
    server backend2.example.com;
  }
  server {
    listen 80;
    location / {
      proxy_pass http://backend;
    }
  }
}
```

**⚠️ Armadilhas Comuns:**

- Não configurar health checks, levando tráfego para instâncias com problemas.
- Armazenar estado em servidores locais, dificultando escalabilidade horizontal.
- Confiar apenas em escalabilidade vertical, que tem limites rígidos.
- Não planejar deploys sem downtime.

**🔑 Principais Lições:**

- Prefira escalabilidade horizontal para serviços stateless.
- Use health checks para manter apenas instâncias saudáveis em rotação.
- Load balancers são essenciais para alta disponibilidade.

---

## 🧑‍💻 8. Otimização de Código e Arquitetura

- **Profile Regularmente:** Use profilers para encontrar trechos lentos.
- **Escolha Algoritmos/Estruturas Eficientes:** Use hash maps, sets e ordenação/busca eficiente.
- **Otimize Caminhos Críticos:** Foque no código mais utilizado.
- **Considere a Linguagem:** Use Go ou Rust para componentes críticos de performance.
- **Decomponha Grandes Apps:** Use microsserviços ou monólitos modulares para escalabilidade independente.
- **Serviços Stateless:** Mais fáceis de escalar horizontalmente.
- **Padrões de Resiliência:**
  - **Timeouts:** Defina timeouts para chamadas externas.
  - **Retries com Backoff:** Use backoff exponencial e jitter.
  - **Circuit Breakers:** Previna falhas em cascata.
- **Batch de Requisições:** Agrupe operações similares para reduzir overhead.

**⚠️ Armadilhas Comuns:**

- Otimização prematura sem profiling.
- Usar estruturas ineficientes em caminhos críticos.
- Ignorar timeouts e retries em chamadas externas.
- Construir monólitos difíceis de escalar/manter.
- Não agrupar requisições para serviços externos.

**⚡ Ganhos Rápidos:**

- Faça profiling regularmente para encontrar gargalos reais.
- Use estruturas e algoritmos eficientes.
- Agrupe requisições para serviços externos sempre que possível.

---

## 📈 9. Monitoramento e Log

- **Monitore Métricas-Chave:** Latência, throughput, taxas de erro, uso de recursos, métricas do banco.
- **Use Ferramentas de Observabilidade:** Prometheus, Grafana, Datadog, New Relic para métricas; ELK, Splunk para logs; Jaeger, Zipkin para tracing.
- **Logging Assíncrono:** Evite que logs bloqueiem threads principais.

**🧑‍💻 Exemplo: Métrica Básica no Prometheus (Python)**

```python
from prometheus_client import Counter
requests = Counter('http_requests_total', 'Total HTTP requests')
def handle_request():
    requests.inc()
    # ...handle request...
    return "OK"
```

**⚠️ Armadilhas Comuns:**

- Não monitorar métricas-chave (latência, erros, uso de recursos).
- Logging síncrono, que pode bloquear threads principais.
- Não centralizar logs, dificultando debugging.
- Não configurar alertas para métricas críticas.

**🔑 Principais Lições:**

- Monitore latência, throughput e taxas de erro de todos os serviços.
- Use logging centralizado e tracing distribuído para visibilidade.
- Logging assíncrono evita impacto na performance.

---

## 🧪 10. Testes de Performance

- **Teste Regularmente:**
  - **Load Testing:** Simule cargas reais de usuários.
  - **Stress Testing:** Descubra pontos de quebra.
  - **Scalability Testing:** Meça carga máxima sustentável.
  - **Endurance Testing:** Detecte vazamentos de memória ao longo do tempo.
- **Automatize Testes:** Integre ao CI/CD para evitar regressões.
- **Benchmarks e Acompanhamento:** Defina baselines e monitore mudanças.

**🧑‍💻 Exemplo: Load Test Simples com Locust (Python)**

```python
from locust import HttpUser, task
class WebsiteUser(HttpUser):
    @task
    def index(self):
        self.client.get("/")
```

**⚠️ Armadilhas Comuns:**

- Testar performance só manualmente ou após incidentes.
- Não automatizar testes de carga no CI/CD.
- Ignorar resultados de testes ou não definir baselines.
- Não simular comportamento realista de usuários nos testes.

**⚡ Ganhos Rápidos:**

- Automatize testes de carga e regressão no CI/CD.
- Faça benchmarks antes e depois de grandes mudanças.
- Acompanhe tendências de performance para detectar regressões cedo.

---

## 📖 11. Leituras e Recursos Adicionais

- Artigos de Martin Fowler sobre Performance Patterns

---

> **Dica:** Performance de backend é uma jornada, não um destino. Meça, otimize e repita—sempre com dados reais.

---

**Este guia é um documento vivo. Contribua com melhorias e exemplos à medida que encontrar novos desafios!**

[Voltar ao Índice de Boas Práticas](./index.md)  
[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._

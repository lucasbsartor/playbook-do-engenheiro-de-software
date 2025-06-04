# ☁️ Boas Práticas AWS: Um Guia Prático para Engenheiros

> **Usando a AWS com a cofiança de não ficar endividado 👀**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

## 📚 Índice

- [☁️ 1. Boas Práticas de Desenvolvimento](#️-1-boas-práticas-de-desenvolvimento)
  - [🏗️ Arquitetura e Design de Aplicações](#️-arquitetura-e-design-de-aplicações)
  - [🔒 Segurança e Gerenciamento de Identidade](#-segurança-e-gerenciamento-de-identidade)
  - [📊 Observabilidade e Log](#-observabilidade-e-log)
  - [💸 Gestão e Otimização de Custos](#-gestão-e-otimização-de-custos)
  - [⚙️ Práticas Diversas de Desenvolvimento](#️-práticas-diversas-de-desenvolvimento)
- [🔧 2. Boas Práticas de Operações](#-2-boas-práticas-de-operações)
  - [🔑 Infraestrutura e Controle de Acesso](#-infraestrutura-e-controle-de-acesso)
  - [⚙️ Otimizações Específicas de Serviços](#️-otimizações-específicas-de-serviços)
- [📖 3. Leituras e Recursos Adicionais](#-3-leituras-e-recursos-adicionais)

---

## ☁️ 1. Boas Práticas de Desenvolvimento

### 🏗️ Arquitetura e Design de Aplicações

- **Projete para Statelessness:** Armazene estado em serviços gerenciados (S3, RDS, DynamoDB, ElastiCache), nunca em instâncias EC2. Isso facilita o scaling e a resiliência.
  - _Por quê:_ Simplifica o escalonamento e a recuperação.
- **Aposte em Escalabilidade Horizontal:** Use Auto Scaling Groups, AWS Lambda, ECS/EKS para escalar horizontalmente, não verticalmente.
  - _Por quê:_ Melhora a elasticidade e tolerância a falhas.
- **Aproveite Padrões Nativos AWS:** Integre com SDKs AWS, CloudWatch e IAM para permissões e monitoramento.
  - _Por quê:_ Maximiza os benefícios da nuvem e a confiabilidade.
- **Use SDKs Oficiais AWS:** Sempre interaja com a AWS via SDKs oficiais da sua linguagem.
  - _Por quê:_ Garante uso seguro, confiável e atualizado das APIs.

**💡 Exemplo: Web App Stateless (Python Flask + S3 para uploads de arquivos)**

```python
# Endpoint Flask para upload de arquivo no S3
from flask import Flask, request
import boto3
app = Flask(__name__)
s3 = boto3.client('s3')
@app.route('/upload', methods=['POST'])
def upload():
    file = request.files['file']
    # Faz upload do arquivo para o bucket S3 especificado
    s3.upload_fileobj(file, 'my-bucket', file.filename)
    return 'Uploaded!'
```

**🔑 Principais Lições:**

- Projete para statelessness e escalabilidade horizontal desde o início.
- Use serviços e SDKs nativos AWS para confiabilidade e segurança.
- Prefira serviços gerenciados a reinventar a roda.

---

### 🔒 Segurança e Gerenciamento de Identidade

- **Use IAM Roles para EC2 e Lambda:** Nunca armazene credenciais no código. Atribua roles IAM a instâncias e funções.
- **Agrupe Permissões:** Anexe políticas a grupos, não a usuários individuais.
- **Exija MFA:** Exija autenticação multifator para todos os usuários IAM, especialmente administradores.
- **Automatize Auditoria de Segurança:** Ative AWS Security Hub, GuardDuty, Config e Trusted Advisor.
- **Habilite CloudTrail:** Registre todas as chamadas de API e armazene logs com segurança no S3.
- **Planeje Gerenciamento de Chaves desde o Início:** Use AWS KMS ou Secrets Manager para chaves de criptografia e segredos.

**🧑‍💻 Exemplo: Atribuindo uma IAM Role a uma EC2 (Console AWS)**

# Este exemplo descreve os passos para atribuir uma IAM role a uma instância EC2 para permissões seguras e gerenciadas.

1. Crie uma IAM role com as permissões necessárias.
2. Anexe a role à sua instância EC2.
3. Use o SDK AWS no seu app—credenciais são fornecidas automaticamente.

**⚡ Ganhos Rápidos:**

- Nunca armazene credenciais no código—use IAM roles e gerenciadores de segredos.
- Exija MFA para todos os usuários, especialmente administradores.
- Habilite CloudTrail e automatize auditoria de segurança desde o início.

---

### 📊 Observabilidade e Log

- **Logue com Contexto:** Inclua IDs de requisição, IDs de usuário e timestamps nos logs.
- **Centralize Logs:** Envie logs para CloudWatch Logs ou faça streaming para S3/ELK para análise.
- **Use Métricas do CloudWatch:** Comece com métricas padrão, adicione customizadas conforme necessidade do app.
- **Habilite Monitoramento Detalhado:** Para recursos críticos, ative monitoramento em intervalos de 1 minuto.

**🧑‍💻 Exemplo: Métrica Customizada no CloudWatch (Node.js)**

```js
// Envia uma métrica customizada para o CloudWatch a partir de uma aplicação Node.js
const AWS = require("aws-sdk");
const cloudwatch = new AWS.CloudWatch();
cloudwatch.putMetricData({
  Namespace: "MyApp",
  MetricData: [
    {
      MetricName: "ProcessedRequests",
      Value: 1,
      Unit: "Count",
    },
  ],
});
```

**🔑 Principais Lições:**

- Centralize logs e métricas para visibilidade total.
- Use CloudWatch para métricas padrão e customizadas.
- Habilite monitoramento detalhado para recursos críticos.

---

### 💸 Gestão e Otimização de Custos

- **Configure Alertas de Faturamento:** Use CloudWatch Alarms para notificar sobre limites de gastos.
- **Cheque Limites de Serviço:** Revise e solicite aumentos antes de lançar novas cargas de trabalho.
- **Use Reserved Instances/Savings Plans:** Para workloads estáveis, comprometa-se para economizar.
- **Dimensione Recursos Corretamente:** Revise e ajuste tamanhos de recursos regularmente para atender à demanda.

**🧑‍💻 Exemplo: Configurando um Alerta de Faturamento (Console AWS)**

# Este exemplo mostra como configurar um alarme de faturamento no AWS CloudWatch para monitorar custos.

1. Acesse CloudWatch > Alarms > Create Alarm.
2. Selecione a métrica `EstimatedCharges`.
3. Defina o limite e a notificação.

**⚡ Ganhos Rápidos:**

- Configure alertas de faturamento antes de precisar deles.
- Dimensione recursos corretamente e cheque limites de serviço regularmente.
- Use Reserved Instances/Savings Plans para workloads previsíveis.

---

### ⚙️ Práticas Diversas de Desenvolvimento

- **Convenções de Nomenclatura Consistentes:** Use nomes claros e estruturados (ex: `projeto-ambiente-serviço-tipo`).
- **Implemente em Múltiplas AZs:** Garanta alta disponibilidade distribuindo recursos entre Availability Zones.
- **Valide o Fit da AWS:** Avalie se a AWS é adequada para sua carga de trabalho antes de construir ou migrar.

**🔑 Principais Lições:**

- Nomenclatura e tagging consistentes tornam ambientes AWS grandes gerenciáveis.
- Sempre implemente em múltiplas AZs para alta disponibilidade.
- Valide se a AWS é o fit certo para sua carga antes de construir.

---

## 🔧 2. Boas Práticas de Operações

### 🔑 Infraestrutura e Controle de Acesso

- **Desative SSH Sempre que Possível:** Use o Systems Manager Session Manager para acesso shell ao invés de SSH.
- **Monitore Saúde de Serviços, Não Só de Servidores:** Foque em métricas de aplicação (latência, erros).
- **Automatize Tudo:** Use CloudFormation, CDK, CodeDeploy e Lambda para provisionamento e operações.
- **Não Use Root para Tarefas Diárias:** Use usuários IAM com privilégio mínimo; reserve root para emergências.
- **Alertas Ação:** Configure CloudWatch Alarms para métricas críticas e direcione para os canais corretos.
- **Tagueie Recursos:** Use tags para projeto, ambiente, responsável e centro de custo.
- **Habilite Proteção contra Terminação:** Para instâncias fora de auto scaling, previna deleção acidental.
- **Sempre Use VPC:** Implemente todos os recursos dentro de uma VPC para isolamento e segurança.
- **Restrinja Security Groups:** Abra apenas portas necessárias para IPs ou security groups específicos.
- **Libere Elastic IPs Não Usados:** Revise e libere EIPs não associados para evitar cobranças.

**🧑‍💻 Exemplo: Tagueando Recursos (AWS CLI)**

```powershell
# Adiciona tags a uma instância EC2 com informações de projeto e ambiente
aws ec2 create-tags --resources i-1234567890abcdef0 --tags Key=Project,Value=MyApp Key=Environment,Value=Prod
```

**⚡ Ganhos Rápidos:**

- Use Session Manager ao invés de SSH para acesso seguro.
- Tagueie todos os recursos e habilite proteção contra terminação quando necessário.
- Restrinja security groups e libere Elastic IPs não utilizados.

---

### ⚙️ Otimizações Específicas de Serviços

#### Elastic Load Balancing (ELB)

- **Termine SSL no ELB:** Faça o offload de SSL/TLS no load balancer para melhor performance e gestão.
- **Pré-aqueça ELBs:** Contate o suporte AWS para pré-aquecer para picos de tráfego esperados.
- **Alinhe AZs:** Combine as AZs do Auto Scaling Group com a configuração do ELB.

#### Amazon RDS

- **Assinaturas de Eventos:** Seja notificado sobre failovers e eventos críticos.
- **Implantação Multi-AZ:** Sempre use para bancos de produção.

#### Amazon S3

- **Hífens em Nomes de Buckets:** Use hífens para compatibilidade SSL.
- **Evite Montar como Filesystem:** Use APIs S3 diretamente para apps críticos em performance.
- **Use CloudFront para Aceleração:** Coloque CloudFront na frente do S3 para performance global.
- **Prefixos Aleatórios para Escritas em Alto Volume:** Distribua escritas com prefixos aleatórios para evitar throttling.

#### Amazon ElastiCache

- **Use Endpoints de Configuração:** Para Redis Cluster Mode ou clusters Memcached, conecte via endpoint de configuração.

#### AWS Auto Scaling

- **Reduza em INSUFFICIENT_DATA:** Evite superprovisionamento em tráfego baixo.
- **Prefira Health Checks do ELB:** Use health checks do ELB para Auto Scaling Groups.
- **Evite Múltiplos Triggers de Scaling:** Previna ações de scaling conflitantes.

#### AWS Route 53

- **Use Registros ALIAS:** Para recursos AWS, use ALIAS ao invés de CNAME para domínios apex.

#### Amazon EMR

- **Diretórios S3 Dedicados para Resultados Hive:** Previna corrupção de dados isolando saídas de jobs.

**🔑 Principais Lições:**

- Faça offload de SSL no ELB e alinhe AZs para custo e performance.
- Use Multi-AZ para RDS e CloudFront para acelerar S3.
- Prefira endpoints de configuração para clusters ElastiCache.
- Use registros ALIAS no Route 53 para recursos AWS.

---

## 📖 3. Leituras e Recursos Adicionais

- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)
- [AWS Security Best Practices](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-standards-fsbp.html)
- [AWS Cost Optimization](https://aws.amazon.com/architecture/cost-optimization/)
- [AWS Documentation](https://docs.aws.amazon.com/)

---

> **Dica:** A AWS evolui rapidamente—revise estas boas práticas regularmente e mantenha-se atualizado com novos serviços e recursos.

---

**Este guia é um documento vivo. Contribua com melhorias e exemplos à medida que encontrar novos desafios!**

[Voltar ao Índice de Boas Práticas](./index.md)  
[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._

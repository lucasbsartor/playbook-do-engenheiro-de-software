# 🛡️ Segurança de APIs: Um Guia Prático para Engenheiros

> **APIs seguras e robustas**

**Autor:** Lucas de Bona Sartor  
**Data da última atualização:** Maio de 2025

---

## 📚 Índice

- [🛡️ 1. Princípios Fundamentais](#️-1-princípios-fundamentais)
- [🔐 2. Autenticação](#-2-autenticação)
- [🛂 3. Autorização (Controle de Acesso)](#-3-autorização-controle-de-acesso)
- [🧹 4. Validação e Processamento de Entradas](#-4-validação-e-processamento-de-entradas)
- [🚫 5. Tratamento de Saída e Exposição de Dados](#-5-tratamento-de-saída-e-exposição-de-dados)
- [📈 6. Monitoramento e Log](#-6-monitoramento-e-log)
- [🔑 7. Boas Práticas com JSON Web Tokens (JWT)](#-7-boas-práticas-com-json-web-tokens-jwt)
- [🔗 8. Boas Práticas com OAuth 2.0](#-8-boas-práticas-com-oauth-20)
- [🔄 9. Ciclo de Vida Seguro e CI/CD](#-9-ciclo-de-vida-seguro-e-cicd)
- [📖 10. Leituras e Recursos Adicionais](#-10-leituras-e-recursos-adicionais)

---

## 🛡️ 1. Princípios Fundamentais

**Comece por aqui: estes princípios sustentam toda API segura.**

- **Defesa em Profundidade:** Implemente camadas de controles de segurança. Se uma falhar, as outras ainda protegem.
- **Privilégio Mínimo:** Conceda a usuários/serviços apenas o acesso necessário—nada além disso.
- **Seguro por Design:** Pense em segurança desde o início, não como um complemento.
- **Monitoramento Contínuo:** Observe atividades suspeitas e responda rapidamente.
- **Assuma a Violação:** Projete como se atacantes fossem invadir—limite o dano possível.

**🔑 Principais Lições:**

- Sempre presuma que sua API será atacada—projetando para isso.
- Múltiplas camadas de segurança são melhores que uma só.
- Limite acessos e monitore continuamente.

---

## 🔐 2. Autenticação

**Autenticação = “Quem é você?”**

### ✅ Boas Práticas

- **Use Protocolos Modernos:** Prefira OAuth 2.0 e OpenID Connect (OIDC) para autenticação de usuários. Para APIs internas, considere chaves de API (com rotação), Mutual TLS ou tokens de curta duração.
- **Nunca Armazene Segredos no Código:** Guarde credenciais em variáveis de ambiente ou gerenciadores de segredos.
- **Exija Senhas Fortes:** Utilize bcrypt ou Argon2 para hash. Exija complexidade e tamanho mínimo.
- **Limite Tentativas de Login:** Previna ataques de força bruta com rate limiting e bloqueios.
- **Gerencie Sessões com Segurança:** Use IDs de sessão aleatórios e seguros. Defina timeouts e invalide ao fazer logout.

### 🧑‍💻 Exemplo: Limitação de Tentativas de Login

**Exemplo Iniciante (Pseudocódigo em Python):**

```python
def handle_login(username, password, ip):
    if too_many_attempts(ip) or too_many_attempts(username):
        return "429 Too Many Requests"
    if authenticate(username, password):
        reset_attempts(username, ip)
        return "200 OK"
    else:
        increment_attempts(username, ip)
        return "401 Unauthorized"
```

**Exemplo Avançado (Node.js/Express com Redis):**

```js
// Middleware para limitar tentativas de login por IP
const rateLimit = require("express-rate-limit");
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutos
  max: 5, // limita cada IP a 5 requisições por janela
  message: "Too many login attempts. Please try again later.",
});
app.post("/login", loginLimiter, loginHandler);
```

**⚡ Ganhos Rápidos:**

- Nunca use autenticação básica ou segredos hardcoded.
- Exija senhas fortes e gerencie sessões corretamente.
- Implemente rate limiting nos endpoints de login imediatamente.

---

## 🛂 3. Autorização (Controle de Acesso)

**Autorização = “O que você pode fazer?”**

### ✅ Boas Práticas

- **Aplique no Servidor:** Nunca confie no cliente para checagens de autorização.
- **Use RBAC ou ABAC:** Controle de Acesso Baseado em Papéis ou Atributos para flexibilidade.
- **Checagem em Nível de Recurso:** Usuários só devem acessar seus próprios dados.
- **Rate Limiting e Throttling:** Previna abusos e DDoS.
- **Sempre Use HTTPS:** Criptografe todo o tráfego da API.

### 🧑‍💻 Exemplo: Autorização de Recurso

**Exemplo Simples (Python/Flask):**

```python
@app.route('/users/<user_id>/orders')
@login_required
def get_orders(user_id):
    if current_user.id != user_id and not current_user.is_admin:
        abort(403)
    return fetch_orders(user_id)
```

**Exemplo Especialista (Node.js/Express com RBAC):**

```js
function authorize(role) {
  return (req, res, next) => {
    if (!req.user || !req.user.roles.includes(role)) {
      return res.status(403).json({ error: "Forbidden" });
    }
    next();
  };
}
app.get("/admin/data", authenticate, authorize("admin"), adminDataHandler);
```

**🔑 Principais Lições:**

- Sempre aplique autorização no lado do servidor.
- Use RBAC/ABAC para flexibilidade e segurança.
- HTTPS é obrigatório para todas as APIs.

---

## 🧹 4. Validação e Processamento de Entradas

**Nunca confie em entradas do usuário. Valide tudo.**

### ✅ Boas Práticas

- **Valide Todas as Entradas:** Cheque tipos, formatos, tamanhos e valores permitidos.
- **Sanitize as Entradas:** Previna XSS e SQL injection.
- **Whitelist, Não Blacklist:** Permita apenas valores conhecidos e seguros.
- **Valide o Content-Type:** Aceite apenas formatos esperados (ex: `application/json`).
- **Desative Recursos Perigosos:** Desative expansão de entidades XML e modos de debug em produção.

### 🧑‍💻 Exemplo: Validação de Entrada

**Exemplo Iniciante (Python):**

```python
import re
def validate_email(email):
    if not re.fullmatch(r"[^@]+@[^@]+\.[^@]+", email):
        raise ValueError("Invalid email")
```

**Exemplo Especialista (Express + Joi):**

```js
const Joi = require("joi");
const schema = Joi.object({
  email: Joi.string().email().required(),
  productId: Joi.number().integer().positive().required(),
});
app.post("/purchase", (req, res) => {
  const { error } = schema.validate(req.body);
  if (error) return res.status(400).send(error.details[0].message);
  // ...process purchase
});
```

**⚡ Ganhos Rápidos:**

- Valide e sanitize todas as entradas—nunca confie no cliente.
- Use whitelisting e checagem forte de tipos.
- Desative modos de debug e recursos perigosos em produção.

---

## 🚫 5. Tratamento de Saída e Exposição de Dados

**Não vaze dados sensíveis. Retorne apenas o necessário.**

### ✅ Boas Práticas

- **Nunca Retorne Segredos:** Não inclua senhas, tokens ou PII nas respostas.
- **Retorne Apenas Campos Necessários:** Evite `SELECT *` em queries.
- **Defina Cabeçalhos de Segurança:** Use `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY` e uma `Content-Security-Policy` restrita.
- **Remova Cabeçalhos de Fingerprinting:** Oculte detalhes do servidor (`X-Powered-By`, etc.).
- **Use Códigos de Status HTTP Corretos:** Comunique-se claramente com os clientes.

### 🧑‍💻 Exemplo: Mascarando Dados Sensíveis

```js
// Remova campos sensíveis antes de enviar dados do usuário
function sanitizeUser(user) {
  const { password, ssn, ...safeUser } = user;
  return safeUser;
}
res.json(sanitizeUser(dbUser));
```

**🔑 Principais Lições:**

- Nunca retorne segredos ou dados desnecessários nas respostas da API.
- Defina cabeçalhos de segurança e use códigos de status corretos.
- Remova cabeçalhos que identificam o servidor.

---

## 📈 6. Monitoramento e Log

**Você não pode proteger o que não vê.**

### ✅ Boas Práticas

- **Centralize Logs:** Agregue logs de todos os serviços.
- **Logue Eventos-Chave:** Requisições, respostas, erros, tentativas de autenticação, mudanças de configuração.
- **Mascarar Dados Sensíveis:** Nunca registre senhas, tokens ou PII.
- **Configure Alertas:** Notifique sobre atividades suspeitas (ex: repetidas falhas de login).
- **Revise Logs Regularmente:** Busque tendências e anomalias.

### 🧑‍💻 Exemplo: Mascarando em Logs

```python
def log_login_attempt(username, success):
    safe_username = username[:2] + "***"
    logger.info(f"Login attempt for {safe_username}: {'Success' if success else 'Failure'}")
```

**⚡ Ganhos Rápidos:**

- Centralize e revise logs regularmente.
- Mascarar dados sensíveis nos logs.
- Configure alertas para atividades suspeitas.

---

## 🔑 7. Boas Práticas com JSON Web Tokens (JWT)

**JWTs são poderosos, mas fáceis de usar incorretamente.**

### ✅ Boas Práticas

- **Use Chaves Fortes:** Proteja seus segredos de assinatura.
- **Enforce Algoritmos:** Nunca confie no `alg` do header do token—imponha isso no servidor.
- **Expiração Curta:** Use tokens de acesso de curta duração; tokens de refresh para sessões mais longas.
- **Não Armazene Dados Sensíveis no Payload:** JWTs não são criptografados!
- **Implemente Revogação:** Suporte blacklist ou invalidação de tokens.

### 🧑‍💻 Exemplo: Verificando Algoritmo do JWT (Node.js)

```js
const jwt = require("jsonwebtoken");
const expectedAlg = "HS256";
const decoded = jwt.verify(token, secret, { algorithms: [expectedAlg] });
```

**🔑 Principais Lições:**

- Use segredos fortes e imponha algoritmos no servidor.
- Mantenha JWTs de curta duração e nunca armazene dados sensíveis neles.
- Implemente revogação de tokens para segurança.

---

## 🔗 8. Boas Práticas com OAuth 2.0

**OAuth 2.0 é o padrão para autorização delegada.**

### ✅ Boas Práticas

- **Valide URIs de Redirecionamento:** Permita apenas URIs pré-registradas e correspondências exatas.
- **Prefira Authorization Code Flow com PKCE:** Especialmente para SPAs e apps mobile.
- **Use o Parâmetro `state`:** Previna ataques CSRF.
- **Defina e Valide Escopos:** Limite o que os clientes podem acessar.
- **Tokens de Curta Duração:** Use refresh tokens para sessões mais longas.

### 🧑‍💻 Exemplo: Validando Redirect URI (Python)

```python
def is_valid_redirect_uri(requested_uri, allowed_uris):
    return requested_uri in allowed_uris
```

**⚡ Ganhos Rápidos:**

- Sempre valide URIs de redirecionamento e use PKCE para clientes públicos.
- Use o parâmetro `state` para prevenir CSRF.
- Defina e valide escopos para garantir privilégio mínimo.

---

## 🔄 9. Ciclo de Vida Seguro e CI/CD

**Segurança é um processo, não um checklist.**

### ✅ Boas Práticas

- **Modelagem de Ameaças:** Identifique riscos cedo.
- **Testes de Segurança Automatizados:** Use SAST, DAST e SCA no CI/CD.
- **Revisões de Código:** Exija revisão por pares, especialmente para mudanças de segurança.
- **Mantenha Dependências Atualizadas:** Automatize a varredura de vulnerabilidades.
- **Princípio do Privilégio Mínimo:** Ferramentas de CI/CD devem ter permissões mínimas.
- **Planos de Rollback:** Esteja pronto para reverter deploys inseguros.

### 🧑‍💻 Exemplo: SCA no CI (npm)

```powershell
npm install
npm audit --production
```

**🔑 Principais Lições:**

- Integre testes de segurança ao seu pipeline CI/CD.
- Mantenha dependências atualizadas e automatize a varredura de vulnerabilidades.
- Sempre tenha um plano de rollback para deploys.

---

## 📖 10. Leituras e Recursos Adicionais

- [OWASP Top 10 API Security Risks](https://owasp.org/www-project-api-security/)

---

> **Lembre-se:** Segurança é responsabilidade de todos. Comece com estas boas práticas, continue aprendendo e sempre pense como um atacante para se defender como um profissional.

---

**Este guia é um documento vivo. Contribua com melhorias e exemplos à medida que encontrar novos desafios!**

[Voltar ao Índice de Boas Práticas](./index.md)  
[Voltar à página inicial](../index.md)

_Criado e mantido por [Lucas de Bona Sartor](https://github.com/lucasbsartor). Publicado com [GitHub Pages](https://pages.github.com/)._

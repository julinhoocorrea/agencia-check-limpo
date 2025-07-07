# 🌐 Guia Completo: Conectar Domínio Hostinger ao GitHub Pages

## 📋 Informações do Projeto
- **Repositório:** julinhoocorrea/juteste
- **URL Atual:** https://julinhoocorrea.github.io/juteste/
- **GitHub Pro:** ✅ Ativo (necessário para repositório privado)
- **Objetivo:** Conectar domínio customizado com segurança máxima

---

## 🔧 PARTE 1: Configuração DNS no Hostinger

### 1.1 Acesso ao Painel DNS
1. Acesse seu painel Hostinger
2. Vá em **"Domínios"** > **"Zona DNS"**
3. Selecione seu domínio

### 1.2 Configurar Registros A (IPv4)
Adicione os seguintes registros A:

```
Nome: @
Tipo: A
TTL: 14400
Valor: 185.199.108.153

Nome: @
Tipo: A
TTL: 14400
Valor: 185.199.109.153

Nome: @
Tipo: A
TTL: 14400
Valor: 185.199.110.153

Nome: @
Tipo: A
TTL: 14400
Valor: 185.199.111.153
```

### 1.3 Configurar Registro CNAME
```
Nome: www
Tipo: CNAME
TTL: 14400
Valor: julinhoocorrea.github.io
```

### 1.4 Configurar Registro AAAA (IPv6) - Opcional mas Recomendado
```
Nome: @
Tipo: AAAA
TTL: 14400
Valor: 2606:50c0:8000::153

Nome: @
Tipo: AAAA
TTL: 14400
Valor: 2606:50c0:8001::153

Nome: @
Tipo: AAAA
TTL: 14400
Valor: 2606:50c0:8002::153

Nome: @
Tipo: AAAA
TTL: 14400
Valor: 2606:50c0:8003::153
```

---

## 🔐 PARTE 2: Configuração GitHub Pages com Segurança

### 2.1 Tornar Repositório Privado (GitHub Pro)
1. Acesse: https://github.com/julinhoocorrea/juteste/settings
2. Role até **"Danger Zone"**
3. Clique **"Change repository visibility"**
4. Selecione **"Make private"**
5. Digite o nome do repositório para confirmar

> ⚠️ **IMPORTANTE:** Com GitHub Pro, você pode manter repositórios privados com GitHub Pages ativo!

### 2.2 Configurar Domínio Customizado
1. Vá em **Settings** > **Pages**
2. Em **"Custom domain"**, digite seu domínio: `seudominio.com`
3. Marque **"Enforce HTTPS"** (aguarde propagação DNS)
4. Clique **"Save"**

### 2.3 Configurar Arquivo CNAME
Crie o arquivo `CNAME` na raiz do repositório:
```
seudominio.com
```

---

## 🛡️ PARTE 3: Implementar Segurança Máxima

### 3.1 Configurar Branch Protection Rules
1. Vá em **Settings** > **Branches**
2. Clique **"Add rule"**
3. Configure:
   - **Branch name pattern:** `main`
   - ✅ **Require a pull request before merging**
   - ✅ **Require approvals** (mínimo 1)
   - ✅ **Dismiss stale PR approvals when new commits are pushed**
   - ✅ **Require status checks to pass before merging**
   - ✅ **Require branches to be up to date before merging**
   - ✅ **Require signed commits**
   - ✅ **Include administrators**
   - ✅ **Restrict pushes that create files exceeding 100MB**

### 3.2 Habilitar Security Features
1. **Settings** > **Security & analysis**
2. Habilite todas as opções:
   - ✅ **Dependency graph**
   - ✅ **Dependabot alerts**
   - ✅ **Dependabot security updates**
   - ✅ **Code scanning alerts**
   - ✅ **Secret scanning alerts**

### 3.3 Configurar Security Headers
Crie `.github/workflows/security-headers.yml`:

```yaml
name: Security Headers
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  security-headers:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4

    - name: Create _headers file
      run: |
        cat > _headers << 'EOF'
        /*
          X-Frame-Options: DENY
          X-Content-Type-Options: nosniff
          X-XSS-Protection: 1; mode=block
          Referrer-Policy: strict-origin-when-cross-origin
          Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self' data:; connect-src 'self' https:; frame-ancestors 'none';
          Strict-Transport-Security: max-age=63072000; includeSubDomains; preload
          Permissions-Policy: geolocation=(), microphone=(), camera=()
        EOF

    - name: Commit headers
      run: |
        git config --local user.email "action@github.com"
        git config --local user.name "GitHub Action"
        git add _headers
        git diff --staged --quiet || git commit -m "Add security headers"
        git push
```

### 3.4 Implementar CSP (Content Security Policy)
Adicione no `<head>` do HTML:

```html
<meta http-equiv="Content-Security-Policy" content="
  default-src 'self';
  script-src 'self' 'unsafe-inline' 'unsafe-eval';
  style-src 'self' 'unsafe-inline' https://fonts.googleapis.com;
  font-src 'self' https://fonts.gstatic.com;
  img-src 'self' data: https:;
  connect-src 'self' https:;
  frame-ancestors 'none';
  base-uri 'self';
  form-action 'self';
">
```

---

## 📊 PARTE 4: Monitoramento e Alertas

### 4.1 Configurar GitHub Actions para Monitoramento
Crie `.github/workflows/monitoring.yml`:

```yaml
name: Website Monitoring
on:
  schedule:
    - cron: '0 */6 * * *'  # A cada 6 horas
  workflow_dispatch:

jobs:
  monitor:
    runs-on: ubuntu-latest
    steps:
    - name: Check Website Status
      run: |
        response=$(curl -s -o /dev/null -w "%{http_code}" https://seudominio.com)
        if [ $response -ne 200 ]; then
          echo "❌ Website está offline! Status: $response"
          exit 1
        else
          echo "✅ Website está online! Status: $response"
        fi

    - name: Check SSL Certificate
      run: |
        echo | openssl s_client -servername seudominio.com -connect seudominio.com:443 2>/dev/null | openssl x509 -noout -dates

    - name: Performance Check
      run: |
        time curl -s https://seudominio.com > /dev/null
```

### 4.2 Configurar Dependabot
Crie `.github/dependabot.yml`:

```yaml
version: 2
updates:
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"

  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10
```

### 4.3 Notificações de Segurança
1. **Settings** > **Notifications**
2. Configure alertas para:
   - ✅ **Security alerts**
   - ✅ **Failed workflow runs**
   - ✅ **Dependabot alerts**

---

## 🔍 PARTE 5: Auditoria e Validação

### 5.1 Verificar Configuração DNS
```bash
# Verificar registros A
dig seudominio.com A

# Verificar CNAME
dig www.seudominio.com CNAME

# Verificar propagação
nslookup seudominio.com 8.8.8.8
```

### 5.2 Testar Segurança
- **SSL Test:** https://www.ssllabs.com/ssltest/
- **Security Headers:** https://securityheaders.com/
- **DNS Checker:** https://dnschecker.org/

### 5.3 Ferramentas de Monitoramento Externas (Recomendadas)
- **UptimeRobot:** Monitoramento gratuito 24/7
- **Google Search Console:** Monitoramento SEO
- **Cloudflare:** DNS + CDN + Segurança adicional

---

## ✅ CHECKLIST FINAL

### Antes de Começar
- [ ] Confirmar GitHub Pro ativo
- [ ] Backup do site atual
- [ ] Listar domínio a ser usado

### Configuração DNS (Hostinger)
- [ ] Registros A configurados (4 IPs)
- [ ] Registro CNAME www configurado
- [ ] Registros AAAA configurados (opcional)
- [ ] TTL definido para 14400 (4 horas)

### GitHub Pages
- [ ] Repositório tornado privado
- [ ] Domínio customizado configurado
- [ ] HTTPS enforced habilitado
- [ ] Arquivo CNAME criado na raiz

### Segurança
- [ ] Branch protection rules ativadas
- [ ] Security features habilitadas
- [ ] CSP implementado
- [ ] Security headers configurados
- [ ] Workflow de segurança criado

### Monitoramento
- [ ] GitHub Actions para monitoramento
- [ ] Dependabot configurado
- [ ] Notificações de segurança ativas
- [ ] Ferramentas externas configuradas

### Validação
- [ ] DNS propagado (24-48h)
- [ ] SSL certificado ativo
- [ ] Site acessível pelo domínio
- [ ] Headers de segurança validados
- [ ] Performance testada

---

## 🚨 PROBLEMAS COMUNS E SOLUÇÕES

### DNS não propagou
- **Aguardar:** 24-48 horas para propagação completa
- **Verificar:** TTL configurado corretamente
- **Testar:** Usar diferentes DNS (8.8.8.8, 1.1.1.1)

### SSL não funciona
- **Aguardar:** Propagação DNS completa primeiro
- **Verificar:** Enforce HTTPS habilitado no GitHub
- **Limpar:** Cache do navegador

### Site não carrega
- **Verificar:** Arquivo CNAME na raiz do repositório
- **Confirmar:** GitHub Pages habilitado
- **Checar:** Source branch configurado corretamente

### Erro 404
- **Verificar:** Arquivo index.html na raiz ou pasta configurada
- **Confirmar:** Branch source correto
- **Aguardar:** Build do GitHub Pages completar

---

## 📞 SUPORTE E RECURSOS

### Documentação Oficial
- [GitHub Pages Custom Domain](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [GitHub Security Features](https://docs.github.com/en/code-security)
- [Hostinger DNS Management](https://support.hostinger.com/en/articles/1583227-how-to-manage-dns-records)

### Contatos de Emergência
- **GitHub Support:** Com GitHub Pro, suporte prioritário disponível
- **Hostinger Support:** Chat 24/7 disponível no painel

---

## 🎯 PRÓXIMOS PASSOS RECOMENDADOS

1. **Backup Automatizado:** Configurar GitHub Actions para backup
2. **CDN:** Implementar Cloudflare para performance
3. **Monitoring:** Adicionar Google Analytics/Tag Manager
4. **SEO:** Configurar robots.txt e sitemap.xml
5. **Performance:** Otimizar imagens e recursos

---

**✅ Guia criado em:** 07/07/2025
**📧 Suporte:** Documentação atualizada com melhores práticas de segurança
**🔒 Segurança:** Implementação de proteção máxima configurada

# 📚 CONFIGURAÇÃO OFICIAL GITHUB - lojadacheck.com.br

## 🎯 **BASEADO NA DOCUMENTAÇÃO OFICIAL GITHUB**

### 📋 **REQUISITOS OFICIAIS:**
> Fonte: https://docs.github.com/pt/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

---

## 🔧 **PASSO 1: CONFIGURAÇÃO DNS NO HOSTINGER**

### **Para Domínio Apex (lojadacheck.com.br):**

#### **📍 Registros A (OBRIGATÓRIOS):**
```dns
Tipo: A | Nome: @ | Valor: 185.199.108.153 | TTL: 3600
Tipo: A | Nome: @ | Valor: 185.199.109.153 | TTL: 3600
Tipo: A | Nome: @ | Valor: 185.199.110.153 | TTL: 3600
Tipo: A | Nome: @ | Valor: 185.199.111.153 | TTL: 3600
```

#### **📍 Registro CNAME para www (RECOMENDADO):**
```dns
Tipo: CNAME | Nome: www | Valor: julinhoocorrea.github.io | TTL: 3600
```

#### **📍 Registros AAAA (OPCIONAL - IPv6):**
```dns
Tipo: AAAA | Nome: @ | Valor: 2606:50c0:8000::153 | TTL: 3600
Tipo: AAAA | Nome: @ | Valor: 2606:50c0:8001::153 | TTL: 3600
Tipo: AAAA | Nome: @ | Valor: 2606:50c0:8002::153 | TTL: 3600
Tipo: AAAA | Nome: @ | Valor: 2606:50c0:8003::153 | TTL: 3600
```

---

## ⚡ **PASSO 2: VERIFICAÇÃO OFICIAL**

### **Como o GitHub recomenda verificar:**

#### **2.1 Verificar Registros A:**
```bash
# Use dig ou nslookup para verificar:
dig lojadacheck.com.br +noall +answer -t A

# Deve retornar:
lojadacheck.com.br    3600    IN A     185.199.108.153
lojadacheck.com.br    3600    IN A     185.199.109.153
lojadacheck.com.br    3600    IN A     185.199.110.153
lojadacheck.com.br    3600    IN A     185.199.111.153
```

#### **2.2 Verificar CNAME www:**
```bash
dig www.lojadacheck.com.br +noall +answer -t CNAME

# Deve retornar:
www.lojadacheck.com.br    3600    IN CNAME    julinhoocorrea.github.io
```

---

## 🔐 **PASSO 3: CONFIGURAÇÃO GITHUB PAGES**

### **3.1 Arquivo CNAME (✅ JÁ CRIADO):**
- ✅ Arquivo `CNAME` existe com conteúdo: `lojadacheck.com.br`
- ✅ Já foi commitado no repositório

### **3.2 Configuração no GitHub:**
1. **Settings** → **Pages**
2. **Custom domain:** `lojadacheck.com.br`
3. **Save** (cria commit automático do CNAME)
4. **Aguardar propagação DNS** (até 24 horas)
5. **Enforce HTTPS:** ✅ (só após DNS resolver)

---

## ⚠️ **AVISOS OFICIAIS DO GITHUB:**

### **📋 Do que o GitHub ALERTA:**
```markdown
⚠️ "As alterações de DNS podem levar até 24 horas para serem propagadas"
⚠️ "Adicione o domínio ao GitHub ANTES de configurar DNS"
⚠️ "Não use registros DNS curingas (*.example.com)"
⚠️ "Remove registros padrão antes de continuar"
```

### **✅ Do que o GitHub RECOMENDA:**
```markdown
✅ "Verifique seu domínio antes de adicionar (para segurança)"
✅ "Configure www subdomain junto com apex domain"
✅ "Use HTTPS após DNS propagar completamente"
✅ "Remova registros conflitantes do provedor DNS"
```

---

## 🔍 **PASSO 4: VERIFICAÇÃO COMPLETA**

### **4.1 Checklist DNS (Hostinger):**
- [ ] **4 registros A** com IPs GitHub configurados
- [ ] **1 registro CNAME** (www → julinhoocorrea.github.io)
- [ ] **Registros antigos removidos** (A, CNAME conflitantes)
- [ ] **TTL configurado** para 3600 (1 hora)

### **4.2 Checklist GitHub:**
- [ ] **Domínio adicionado** nas configurações Pages
- [ ] **Arquivo CNAME** presente no repositório
- [ ] **DNS válido** (sem alerta amarelo/vermelho)
- [ ] **Site carregando** em http://lojadacheck.com.br

### **4.3 Checklist Final:**
- [ ] **Propagação DNS completa** (24-48h)
- [ ] **HTTPS ativado** (Enforce HTTPS ✅)
- [ ] **www redirecionando** para apex
- [ ] **Site 100% funcional**

---

## 🚨 **SOLUÇÃO DE PROBLEMAS OFICIAIS:**

### **Erro: "DNS valid for primary"**
```bash
Causa: DNS ainda não propagou
Solução: Aguardar 24h e verificar com dig/nslookup
```

### **Erro: "InvalidDNSError"**
```bash
Causa: Registros DNS incorretos ou conflitantes
Solução:
1. Verificar se 4 registros A estão corretos
2. Remover registros antigos/conflitantes
3. Verificar TTL não é muito alto
```

### **Erro: "www subdomain issues"**
```bash
Causa: CNAME do www incorreto
Solução: www deve apontar para julinhoocorrea.github.io
(NÃO para lojadacheck.com.br)
```

---

## 🎯 **CONFIGURAÇÃO HOSTINGER ESPECÍFICA**

### **Localização no Painel:**
```bash
📍 hPanel → Domínios → lojadacheck.com.br
📍 Gerenciar DNS / DNS Zone / Zone Editor
```

### **Configuração Exata:**
```dns
[DELETAR registros antigos]
❌ Qualquer A apontando para IPs antigos
❌ Qualquer CNAME do domínio principal (@)
❌ Registros de parking/forwarding

[ADICIONAR registros novos]
✅ A @ 185.199.108.153
✅ A @ 185.199.109.153
✅ A @ 185.199.110.153
✅ A @ 185.199.111.153
✅ CNAME www julinhoocorrea.github.io
```

---

## ⏰ **CRONOGRAMA OFICIAL:**

### **Tempo de Propagação DNS:**
```bash
📊 Hostinger: 1-4 horas
📊 ISPs Brasileiros: 6-12 horas
📊 Propagação Global: até 24 horas
📊 GitHub Validation: 10-30 minutos após DNS resolver
```

### **Verificação de Progresso:**
```bash
🔍 A cada 2 horas: https://dnschecker.org
🔍 Teste direto: http://lojadacheck.com.br
🔍 Verificar GitHub Pages: sem alertas amarelos
```

---

## 🆘 **SUPORTE OFICIAL:**

### **Em caso de problemas persistentes:**
1. **Documentação GitHub:** docs.github.com/pages
2. **Suporte Hostinger:** Chat 24/7 no hPanel
3. **GitHub Community:** github.community
4. **Verificador DNS:** dnschecker.org

---

## ✅ **STATUS ATUAL:**

### **O que já está feito:**
- ✅ **Arquivo CNAME criado**
- ✅ **Domínio adicionado no GitHub**
- ✅ **Repositório configurado**

### **O que falta fazer:**
- 🔄 **Configurar DNS no Hostinger** (você)
- 🔄 **Aguardar propagação** (24-48h)
- 🔄 **Ativar HTTPS** (após DNS ok)

**📋 Próximo passo: Configurar os 4 registros A + 1 CNAME no Hostinger exatamente como especificado acima.**

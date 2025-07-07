# 🌐 CONFIGURAR DOMÍNIO: lojadacheck.com.br

## 🎯 **OBJETIVO: Conectar seu domínio Hostinger ao sistema Agência Check**

---

## 📋 **PASSO 1: CONFIGURAR DNS NO HOSTINGER**

### **1.1 Acessar Painel Hostinger:**
1. **Login:** https://hpanel.hostinger.com
2. **Domínios** → **lojadacheck.com.br**
3. **Gerenciar DNS** ou **DNS Zone**

### **1.2 DELETAR Registros Antigos:**
```bash
❌ REMOVER todos os registros tipo:
- A records apontando para outros IPs
- CNAME records conflitantes
- Redirecionamentos/Parking
```

### **1.3 ADICIONAR Registros Netlify:**
```dns
🔹 Tipo: CNAME
   Nome: @ (ou deixar vazio)
   Valor: same-mwqdy28gx80-latest.netlify.app
   TTL: 3600

🔹 Tipo: CNAME
   Nome: www
   Valor: same-mwqdy28gx80-latest.netlify.app
   TTL: 3600
```

**📝 IMPORTANTE:** Use exatamente `same-mwqdy28gx80-latest.netlify.app`

---

## 📋 **PASSO 2: CONFIGURAR DOMÍNIO NO NETLIFY**

### **2.1 Acessar Netlify:**
1. **Login:** https://app.netlify.com
2. **Sites** → **same-mwqdy28gx80-latest**
3. **Domain settings**

### **2.2 Adicionar Domínio Customizado:**
1. **Add custom domain**
2. Digite: `lojadacheck.com.br`
3. **Verify** → **Yes, add domain**

### **2.3 Configurar SSL:**
1. **HTTPS** → **Verify DNS configuration**
2. Aguardar certificado SSL automático
3. **Force HTTPS** → ✅ Ativar

---

## ⏰ **PASSO 3: AGUARDAR PROPAGAÇÃO DNS**

### **3.1 Tempo de Propagação:**
```bash
🕐 Hostinger: 1-4 horas
🕐 DNS Global: 24-48 horas
🕐 SSL Netlify: 10-30 minutos após DNS resolver
```

### **3.2 Verificar Propagação:**
```bash
🔍 Ferramentas de verificação:
- https://dnschecker.org
- https://whatsmydns.net

✅ Digite: lojadacheck.com.br
✅ Deve aparecer: same-mwqdy28gx80-latest.netlify.app
```

---

## 🔧 **PASSO 4: CONFIGURAÇÃO AVANÇADA (OPCIONAL)**

### **4.1 Registros Adicionais (se necessário):**
```dns
🔹 Tipo: TXT (para verificação)
   Nome: @
   Valor: _netlify=your-verification-code

🔹 Tipo: MX (para email - se usar)
   Nome: @
   Valor: (manter configurações de email existentes)
```

### **4.2 Configurações de Performance:**
```bash
✅ CDN automático ativo (Netlify)
✅ Compressão Gzip habilitada
✅ Cache otimizado para assets
✅ HTTP/2 ativo automaticamente
```

---

## 🚨 **SOLUÇÃO DE PROBLEMAS**

### **Erro: "Domain not found"**
```bash
Causa: DNS ainda não propagou
Solução: Aguardar 24-48h e verificar registros DNS
```

### **Erro: "SSL Certificate failed"**
```bash
Causa: CNAME incorreto ou DNS não propagado
Solução:
1. Verificar CNAME: same-mwqdy28gx80-latest.netlify.app
2. Aguardar propagação completa
3. Renovar certificado no Netlify
```

### **Erro: "Site not loading"**
```bash
Causa: Cache do browser ou DNS local
Solução:
1. Limpar cache do browser (Ctrl+F5)
2. Testar em aba anônima
3. Testar em dispositivo diferente
```

---

## ✅ **CHECKLIST FINAL**

### **DNS Hostinger:**
- [ ] CNAME @ → same-mwqdy28gx80-latest.netlify.app
- [ ] CNAME www → same-mwqdy28gx80-latest.netlify.app
- [ ] TTL configurado para 3600
- [ ] Registros antigos removidos

### **Netlify:**
- [ ] Domínio lojadacheck.com.br adicionado
- [ ] DNS verificado e correto
- [ ] SSL certificado ativo
- [ ] Force HTTPS habilitado

### **Teste Final:**
- [ ] https://lojadacheck.com.br carrega o sistema
- [ ] https://www.lojadacheck.com.br redireciona
- [ ] Login funciona: juliocorrea@check2.com / Ju113007
- [ ] SSL certificado válido (cadeado verde)

---

## 🎯 **URLS FINAIS**

### **Após configuração completa:**
```bash
✅ Domínio principal: https://lojadacheck.com.br
✅ Com www: https://www.lojadacheck.com.br
✅ Backup Netlify: https://same-mwqdy28gx80-latest.netlify.app
```

### **Credenciais do Sistema:**
```bash
📧 Email: juliocorrea@check2.com
🔑 Senha: Ju113007
```

---

## 📞 **SUPORTE**

### **Em caso de problemas:**
1. **Hostinger**: Chat 24/7 no hPanel
2. **Netlify**: docs.netlify.com
3. **DNS Checker**: Verificar propagação online

**⏰ Tempo total estimado: 2-48 horas para funcionar completamente**

**🎉 Após completar: Seu sistema estará em lojadacheck.com.br!**

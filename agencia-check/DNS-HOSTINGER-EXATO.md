# 🎯 CONFIGURAÇÃO EXATA HOSTINGER - lojadacheck.com.br

## 📍 **ACESSE:**
https://hpanel.hostinger.com → **Domínios** → **lojadacheck.com.br** → **Gerenciar DNS**

---

## ❌ **PRIMEIRO: DELETAR ESTES REGISTROS**
```
- Qualquer registro A existente com @
- Qualquer registro CNAME existente com @
- Registros de redirecionamento/parking
```

---

## ✅ **SEGUNDO: ADICIONAR ESTES REGISTROS**

### **4 Registros A (obrigatórios):**
```
Tipo: A | Host: @ | Aponta para: 185.199.108.153 | TTL: 3600
Tipo: A | Host: @ | Aponta para: 185.199.109.153 | TTL: 3600
Tipo: A | Host: @ | Aponta para: 185.199.110.153 | TTL: 3600
Tipo: A | Host: @ | Aponta para: 185.199.111.153 | TTL: 3600
```

### **1 Registro CNAME (recomendado):**
```
Tipo: CNAME | Host: www | Aponta para: julinhoocorrea.github.io | TTL: 3600
```

---

## ⏰ **AGUARDAR:**
- **2-4 horas:** DNS propagar
- **24 horas:** Propagação global completa

## 🔍 **VERIFICAR:**
- https://dnschecker.org (digite: lojadacheck.com.br)
- Quando aparecer os 4 IPs do GitHub = DNS OK

## 🔐 **DEPOIS:**
- Voltar no GitHub Pages
- Marcar "Enforce HTTPS" ✅

**🎯 É só isso! Simples e direto conforme documentação oficial GitHub.**

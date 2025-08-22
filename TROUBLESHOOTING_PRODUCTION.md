# 🚨 Troubleshooting: Production Domain Not Serving Traffic

## 🎯 **Problema Identificado**
**Erro:** "Your Production Domain is not serving traffic"

## 🔍 **Diagnóstico Rápido (5 minutos)**

### 1. Verificar Status do Deploy
```bash
# Acesse o dashboard do Vercel
https://vercel.com/dashboard

# Verifique:
✅ Deploy foi concluído com sucesso?
✅ Domínio está configurado corretamente?
✅ SSL certificate foi gerado?
```

### 2. Testar Conectividade
```bash
# Teste 1: Acesso direto ao domínio Vercel
curl -I https://mapssearch-dashboard.vercel.app

# Teste 2: Verificar DNS (Windows)
nslookup mapssearch-dashboard.vercel.app

# Teste 3: Verificar DNS (alternativo)
dig @8.8.8.8 mapssearch-dashboard.vercel.app
```

## 🛠️ **Soluções por Ordem de Prioridade**

### **Solução 1: Verificar Configuração do Projeto** <mcreference link="https://vercel.com/docs/projects/domains/troubleshooting" index="1">1</mcreference>

**Passo 1:** Acesse Vercel Dashboard
```
→ https://vercel.com/dashboard
→ Selecione projeto "mapssearch-dashboard"
→ Aba "Settings" → "Domains"
```

**Passo 2:** Verificar configurações
```
✅ Framework: Create React App
✅ Build Command: cd frontend && npm install && npm run build
✅ Output Directory: frontend/build
✅ Root Directory: ./
```

### **Solução 2: Corrigir Build Command**

**Problema comum:** Build command incorreto

**Configuração correta:**
```json
{
  "buildCommand": "cd frontend && npm ci && npm run build",
  "outputDirectory": "frontend/build",
  "installCommand": "npm ci"
}
```

### **Solução 3: Verificar Variáveis de Ambiente** <mcreference link="https://vercel.com/guides/troubleshooting-connectivity-issues" index="3">3</mcreference>

**No Vercel Dashboard:**
```
Settings → Environment Variables

✅ REACT_APP_API_URL=https://seu-backend.vercel.app
✅ REACT_APP_NAME=Maps Search Dashboard
✅ REACT_APP_VERSION=1.0.0
✅ NODE_ENV=production
```

### **Solução 4: Limpar Cache e DNS** <mcreference link="https://vercel.com/guides/troubleshooting-connectivity-issues" index="3">3</mcreference>

**Windows (PowerShell como Admin):**
```powershell
# Limpar cache DNS
ipconfig /flushdns

# Limpar cache do navegador
# Chrome: Ctrl + Shift + Delete
# Selecionar "Cached images and files"
```

**Teste em navegador privado:**
```
Chrome: Ctrl + Shift + N
Firefox: Ctrl + Shift + P
```

### **Solução 5: Verificar Logs de Build**

**No Vercel Dashboard:**
```
→ Projeto → Deployments
→ Clique no deploy mais recente
→ Aba "Function Logs"
→ Procure por erros
```

**Erros comuns:**
```bash
# Erro de dependências
ERROR: Cannot resolve dependency

# Erro de build
ERROR: Build failed

# Erro de variáveis
ERROR: Environment variable not found
```

### **Solução 6: Redeployar Manualmente**

**Via Vercel CLI:**
```bash
# Instalar Vercel CLI
npm i -g vercel

# Login
vercel login

# Deploy manual
vercel --prod
```

**Via Dashboard:**
```
→ Deployments
→ Três pontos (...) no deploy
→ "Redeploy"
```

## 🔧 **Configuração Correta do vercel.json**

```json
{
  "version": 2,
  "builds": [
    {
      "src": "frontend/package.json",
      "use": "@vercel/static-build",
      "config": {
        "distDir": "build"
      }
    }
  ],
  "routes": [
    {
      "src": "/api/(.*)",
      "dest": "/backend/src/server.js"
    },
    {
      "src": "/(.*)",
      "dest": "/frontend/build/index.html"
    }
  ],
  "env": {
    "NODE_ENV": "production"
  },
  "functions": {
    "backend/src/server.js": {
      "maxDuration": 30
    }
  }
}
```

## 🚨 **Soluções de Emergência**

### **Opção 1: Deploy Apenas Frontend**
```bash
# Configuração simplificada
{
  "buildCommand": "cd frontend && npm ci && npm run build",
  "outputDirectory": "frontend/build"
}
```

### **Opção 2: Usar Netlify (Backup)**
```bash
# Se Vercel falhar completamente
npm install -g netlify-cli
netlify deploy --prod --dir=frontend/build
```

## 📊 **Checklist de Verificação**

```
□ Deploy concluído sem erros
□ Build command correto
□ Output directory correto
□ Variáveis de ambiente configuradas
□ DNS cache limpo
□ Testado em navegador privado
□ Logs verificados
□ SSL certificate ativo
□ Domínio verificado
□ Redeploy realizado
```

## 🆘 **Quando Contactar Suporte**

Se todas as soluções falharem:

**Vercel Support:**
- https://vercel.com/help
- Incluir: URL do projeto, logs de erro, timestamp do problema

**Informações para incluir:**
```
- URL do projeto: https://mapssearch-dashboard.vercel.app
- Repositório: LaioBomfimDev/mapssearch-dashboard
- Framework: Create React App
- Erro: Production domain not serving traffic
- Timestamp: [quando ocorreu]
- Logs de build: [anexar]
```

## ⚡ **Solução Rápida (2 minutos)**

**Se você tem pressa:**
```bash
1. Vercel Dashboard → Projeto → Settings → General
2. Alterar "Output Directory" para: frontend/build
3. Alterar "Build Command" para: cd frontend && npm ci && npm run build
4. Deployments → Redeploy último deploy
5. Aguardar 2-3 minutos
```

---

**🎯 Status:** Aguardando implementação das correções
**⏱️ Tempo estimado:** 5-15 minutos
**🔄 Última atualização:** 2025-01-16
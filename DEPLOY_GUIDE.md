# 🚀 Guia de Deploy no Vercel

Este guia explica como fazer o deploy automático do Maps Search Dashboard no Vercel.

## 📋 Pré-requisitos

- Conta no [Vercel](https://vercel.com)
- Conta no GitHub (já configurada)
- Repositório GitHub criado (✅ Concluído)

## 🔧 Configuração do Deploy

### 1. Conectar ao Vercel

1. Acesse [vercel.com](https://vercel.com) e faça login
2. Clique em **"New Project"**
3. Conecte sua conta do GitHub
4. Selecione o repositório: `LaioBomfimDev/mapssearch-dashboard`

### 2. Configurações do Projeto

**Framework Preset:** `Create React App`

**Build and Output Settings:**
- Build Command: `cd frontend && npm install && npm run build`
- Output Directory: `frontend/build`
- Install Command: `npm install`

### 3. Variáveis de Ambiente

Na seção **Environment Variables**, adicione:

```
REACT_APP_API_URL=https://seu-backend-url.vercel.app
REACT_APP_NAME=Maps Search Dashboard
REACT_APP_VERSION=1.0.0
NODE_ENV=production
```

### 4. Deploy Automático

Após a configuração:
- ✅ O Vercel fará o primeiro deploy automaticamente
- ✅ Cada push na branch `main` acionará um novo deploy
- ✅ Preview deployments para outras branches

## 🌐 URLs de Acesso

Após o deploy:
- **Frontend:** `https://mapssearch-dashboard.vercel.app`
- **Preview:** `https://mapssearch-dashboard-git-[branch].vercel.app`

## 🔄 Deploy do Backend (Opcional)

Para deploy completo com backend:

1. **Opção 1 - Railway/Render:**
   - Conecte o mesmo repositório
   - Configure para rodar `backend/src/server.js`
   - Adicione variáveis de ambiente

2. **Opção 2 - Vercel Functions:**
   - O `vercel.json` já está configurado
   - Backend será deployado como Serverless Functions

## ⚙️ Configurações Avançadas

### Custom Domain
```bash
# Via Vercel CLI
npx vercel --prod
npx vercel domains add seu-dominio.com
```

### Monitoramento
- Analytics automático do Vercel
- Logs de build e runtime
- Performance insights

## 🐛 Troubleshooting

### Build Falha
```bash
# Teste local
cd frontend
npm install
npm run build
```

### Variáveis de Ambiente
- Verifique se todas as `REACT_APP_*` estão definidas
- Redeploy após mudanças nas variáveis

### CORS Issues
- Configure CORS no backend para aceitar o domínio do Vercel
- Atualize `REACT_APP_API_URL` para a URL correta do backend

## 📱 Recursos Automáticos

✅ **HTTPS automático**
✅ **CDN global**
✅ **Compressão automática**
✅ **Cache otimizado**
✅ **Preview deployments**
✅ **Rollback instantâneo**

## 🎯 Próximos Passos

1. Configure domínio customizado
2. Configure analytics
3. Configure alertas de uptime
4. Otimize performance com Vercel Analytics

---

**🚀 Deploy Status:** ✅ Pronto para deploy
**📝 Última atualização:** 2025-01-16
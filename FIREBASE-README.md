# 🔥 Firebase Integration - Cathia Imóveis

Integração completa com Firebase para rastrear contatos e inquéritos de imóveis.

## 📋 Resumo Rápido

| Arquivo | Função |
|---------|--------|
| `firebase-config.js` | Configuração Firebase (credenciais) |
| `property-inquiry.js` | Rastreamento de cliques em imóveis |
| `contato.html` | Já integrado - salva formulários |
| `TEMPLATE-IMOVEL-FIREBASE.html` | Template com Firebase pronto |
| `GUIA-FIREBASE-RAPIDO.md` | Setup em 3 passos |
| `SETUP-FIREBASE.md` | Documentação completa |
| `EXEMPLO-IMPLEMENTACAO.md` | Como integrar em imóvel existente |

---

## 🚀 Início Rápido

### 1. Configure Firebase

```bash
# Siga as instruções em GUIA-FIREBASE-RAPIDO.md
# Resumo:
# 1. Crie projeto em firebase.google.com
# 2. Copie credenciais
# 3. Cole em firebase-config.js
```

### 2. Teste o Formulário de Contato

- Vá em `/contato.html`
- Preencha e envie
- Verifique em **Firebase Console > Firestore > contacts**

### 3. Implemente nos Imóveis

Para cada imóvel, adicione ao botão de contato:

```html
<a href="..." 
   data-inquiry-btn 
   data-property-id="imovel-X"
   data-property-name="Nome do Imóvel"
   class="btn">
   Tenho Interesse
</a>
```

E no final da página:

```html
<script type="module">
    import { initPropertyInquiry } from './assets/js/property-inquiry.js';
    initPropertyInquiry();
</script>
```

---

## 📊 O Que é Rastreado

### ✅ Contatos (formulário completo)
```
Collection: contacts
- Nome
- Email
- Telefone
- Interesse
- Mensagem
- IP
- Timestamp
```

### ✅ Inquéritos (cliques em imóveis)
```
Collection: property_inquiries
- ID do Imóvel
- Nome do Imóvel
- IP
- Timestamp
- User Agent
```

---

## 🔐 Segurança

### Desenvolvimento (teste)
```
allow read, write: if true;
```

### Produção
```
allow create: if true;
allow read, write: if false;
```

**⚠️ Mude as regras antes de publicar!**

---

## 📱 Dados Visíveis Em

**Firebase Console**
- Endereço: https://console.firebase.google.com
- Firestore Database > Collections
  - `contacts`
  - `property_inquiries`

---

## ✨ Funcionalidades

✅ Auto-save no Firestore  
✅ Timestamp automático  
✅ Captura de IP  
✅ Fallback em erro (não quebra funcionalidade)  
✅ Compatível com WhatsApp/Email/Tel links  
✅ Zero impacto no UX  

---

## 🐛 Troubleshooting

| Problema | Solução |
|----------|---------|
| Erro "permission-denied" | Mude para modo TESTE em Firestore > Regras |
| Dados não aparecem | Verifique credenciais em firebase-config.js |
| Script não carrega | Confirme que property-inquiry.js existe |
| WhatsApp não abre | Rastreamento é async, WhatsApp abre normal |

---

## 📚 Documentação

- **Rápido**: `GUIA-FIREBASE-RAPIDO.md` (3 passos)
- **Detalhado**: `SETUP-FIREBASE.md` (guia completo)
- **Prático**: `EXEMPLO-IMPLEMENTACAO.md` (caso real)

---

## 💡 Próximos Passos

1. **Dashboard Admin** - Criar página para ver dados
2. **Notificações** - Email quando novo contato chega
3. **Analytics** - Gráficos de visitantes por imóvel
4. **CRM** - Gerenciar leads

---

## 📞 Suporte

Dúvidas?
- Leia `SETUP-FIREBASE.md`
- Verifique console do navegador (F12)
- Firebase Docs: https://firebase.google.com/docs

---

**Status**: ✅ Pronto para usar

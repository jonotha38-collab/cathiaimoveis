# Guia Rápido - Firebase Cathia Imóveis

## ⚡ 3 Passos para Usar

### 1️⃣ Obter Credenciais Firebase

1. Vá em [Firebase Console](https://console.firebase.google.com/)
2. Crie um projeto (ou use um existente)
3. Vá em **Configurações > Seu apps > Web**
4. Copie o objeto `firebaseConfig`

### 2️⃣ Atualizar `firebase-config.js`

Edite `assets/js/firebase-config.js`:

```javascript
const firebaseConfig = {
    apiKey: "COLE_AQUI_SEU_API_KEY",
    authDomain: "seu-projeto.firebaseapp.com",
    projectId: "seu-projeto",
    storageBucket: "seu-projeto.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123"
};
```

### 3️⃣ Pronto! Já Funciona

- Formulário de contato (`contato.html`) → Salva automaticamente
- Cliques em imóveis → Rastreados automaticamente
- Dados visíveis em Firebase > Firestore

---

## 📊 Onde Ver os Dados

1. Firebase Console > Firestore Database
2. Coleções:
   - `contacts` = Formulário de contato
   - `property_inquiries` = Cliques em imóveis

---

## 🔧 Para Cada Imóvel Individual

Se quiser rastrear inquéritos nos botões:

```html
<a href="https://wa.me/557998129141"
   data-inquiry-btn 
   data-property-id="imovel-1"
   data-property-name="Casa no Condomínio"
   class="btn">
    Tenho Interesse
</a>
```

Depois adicione o script no final do `<body>`:

```html
<script type="module">
    import { initPropertyInquiry } from '../assets/js/property-inquiry.js';
    initPropertyInquiry();
</script>
```

---

## 🔐 Segurança - IMPORTANTE!

### Antes de Publicar (Produção)

**Modo TESTE (Desenvolvimento):**
```javascript
match /{document=**} {
    allow read, write: if true;
}
```

**Modo PRODUÇÃO:**
```javascript
match /contacts/{document=**} {
    allow create: if true;
    allow read, write: if false;
}
match /property_inquiries/{document=**} {
    allow create: if true;
    allow read, write: if false;
}
```

1. Acesse Firebase > Firestore > Regras
2. Cole as regras de produção acima
3. Clique em **Publicar**

---

## 📱 Dados Coletados

### `contacts` (Formulário)
```
- name: "João Silva"
- email: "joao@email.com"
- phone: "+55 79 99999-9999"
- subject: "Aquisição de Ativo"
- message: "Olá, tenho interesse..."
- timestamp: <quando foi enviado>
- ip: "203.0.113.0"
```

### `property_inquiries` (Clique em Imóvel)
```
- propertyId: "imovel-1"
- propertyName: "Casa no Condomínio"
- name: "João" (opcional)
- email: "joao@email.com" (opcional)
- phone: "+55 79 99999-9999" (opcional)
- timestamp: <quando clicou>
- ip: "203.0.113.0"
```

---

## ✅ Checklist

- [ ] Projeto Firebase criado
- [ ] Firestore Database ativado
- [ ] Credenciais copiadas
- [ ] `firebase-config.js` atualizado
- [ ] Regras Firestore configuradas
- [ ] Teste o formulário de contato
- [ ] Verifique dados em Firebase Console

---

## 🆘 Problemas Comuns

**P: Não aparecem dados no Firebase?**
- Verifique as regras (Firestore > Regras)
- Abra console do navegador (F12) para erros
- Confirme que está em modo TESTE

**P: Dá erro "permission-denied"?**
- As regras estão muito restritivas
- Volte para modo TESTE para desenvolvimento

**P: Quer parar de rastrear?**
- Remova `data-inquiry-btn` dos botões
- Comente a importação de `property-inquiry.js`

---

## 📞 Próximos Passos

1. **Dashboard** - Criar página admin para ver dados (requer autenticação)
2. **Alertas** - Configurar notificações por email quando novo contato chega
3. **Analytics** - Análise de visitantes por localização/tipo de imóvel

Consulte `SETUP-FIREBASE.md` para mais detalhes.

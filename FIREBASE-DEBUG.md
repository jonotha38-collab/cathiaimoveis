# 🔧 Firebase - Diagnóstico e Correção de Erros

## ❌ Erro ao Enviar Contato?

Siga este guia para diagnosticar e corrigir.

---

## Passo 1: Verificar o Erro Específico

1. Abra o navegador (Firefox/Chrome)
2. Pressione **F12** para abrir Developer Tools
3. Vá na aba **Console**
4. Preecha o formulário de contato e envie
5. Veja qual é a mensagem de erro

**Cole aqui o erro que vê:**
```
(erro aparecerá aqui)
```

---

## Erros Comuns e Soluções

### ❌ Erro: "permission-denied"

**Causa:** Regras Firestore muito restritivas

**Solução:**
1. Vá em Firebase Console > Seu Projeto > Firestore Database
2. Clique em **Regras**
3. Apague tudo e cole:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

4. Clique **Publicar**
5. Teste novamente

---

### ❌ Erro: "Failed to get document reference"

**Causa:** Credenciais incorretas ou projeto não existe

**Solução:**
1. Verifique se `firebase-config.js` tem credenciais corretas
2. Vá em Firebase Console > Configurações > Seu apps > Web
3. Copie novamente o `firebaseConfig`
4. Cole em `assets/js/firebase-config.js` (linhas 7-16)

---

### ❌ Erro: "The caller does not have permission"

**Causa:** Mesma que acima - regras muito restritivas

**Solução:** Siga as mesmas instruções da primeira solução acima

---

### ❌ Erro: "Firestore is not initialized"

**Causa:** Firestore não foi ativado ou credenciais erradas

**Solução:**
1. Vá em Firebase Console > Seu Projeto
2. Clique em **Criar banco de dados** (ou ele já existe?)
3. Se não existe, ative Firestore
4. Certifique-se que está em modo TESTE (não produção)

---

### ❌ Erro: "404 - Not Found"

**Causa:** Firebase Console não consegue se conectar

**Solução:**
1. Verifique internet
2. Limpe cache (Ctrl+Shift+Delete no Firefox/Chrome)
3. Feche e reabra o navegador
4. Tente novamente

---

## Passo 2: Verificar Credenciais

Abra `assets/js/firebase-config.js` e confirme que tem valores assim:

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXX",        // ✅ NÃO VAZIO
    authDomain: "seu-projeto.firebaseapp.com",    // ✅ NÃO VAZIO
    projectId: "seu-projeto",                      // ✅ NÃO VAZIO
    storageBucket: "seu-projeto.appspot.com",     // ✅ NÃO VAZIO
    messagingSenderId: "123456789",                // ✅ NÃO VAZIO
    appId: "1:123456789:web:abc123",              // ✅ NÃO VAZIO
};
```

**Se vê `YOUR_API_KEY` ou similar = PROBLEMA!**

### Solução:
1. Vá em https://console.firebase.google.com
2. Clique seu projeto
3. Configurações ⚙️ > Seu apps > Web
4. Copie o bloco `firebaseConfig` completo
5. Cole em `assets/js/firebase-config.js`

---

## Passo 3: Verificar Firestore

1. Firebase Console > Seu Projeto > Firestore Database
2. Procure por:
   - [ ] **Database existe?** (não deve dizer "Criar banco de dados")
   - [ ] **Está em modo TESTE?** (deve dizer na cor azul em cima)
   - [ ] **Regras permitem escrita?** (Aba "Regras" deve ter `allow write`)

---

## Passo 4: Testar Manualmente

Abra o console (F12) e execute:

```javascript
import { saveContact } from './assets/js/firebase-config.js';

await saveContact({
    name: "Teste",
    email: "teste@email.com",
    phone: "79999999999",
    subject: "teste",
    message: "Mensagem de teste"
});
```

Se funcionar, dirá `Contato salvo com ID: xxxxx`

---

## Checklist de Diagnóstico

- [ ] Abri console (F12)
- [ ] Vi o erro específico
- [ ] Criei projeto Firebase
- [ ] Ativei Firestore
- [ ] Atualizei credenciais em firebase-config.js
- [ ] Mudei regras Firestore para modo TESTE
- [ ] Testei novamente o formulário

---

## Se Ainda Não Funcionar

Verifique:

1. **Internet está funcionando?** Teste em outro site
2. **Credenciais copiar/colar corretas?** Não espaços extras
3. **Firestore está realmente ativado?** Entra em Firestore e vê database?
4. **Regras estão publicadas?** Botão "Publicar" foi clicado?

---

## Solução Nuclear (Reset Total)

Se nada funcionar:

1. Apague o projeto Firebase
2. Crie um novo projeto
3. Ative Firestore (modo TESTE)
4. Copie as credenciais NOVAS
5. Cole em firebase-config.js
6. Defina regras:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```
7. Teste novamente

---

## 💡 Dica Profissional

Quando configura Firebase pela PRIMEIRA VEZ, sempre use:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

Depois quando funcionar, mude para:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /contacts/{document=**} {
      allow create: if true;
      allow read, write: if false;
    }
    match /property_inquiries/{document=**} {
      allow create: if true;
      allow read, write: if false;
    }
  }
}
```

---

## Próximo Passo

Se resolveu, teste novamente em `/contato.html`

Se não, abra uma issue com o erro específico do console (F12)

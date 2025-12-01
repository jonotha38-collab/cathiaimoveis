# ✅ Corrigir Firebase - Guia Rápido

## Você está recebendo erro ao enviar formulário? Siga isso:

---

## 🔍 Passo 1: Verificar o Erro

1. Abra http://localhost:8000/contato.html
2. Abra Developer Tools: **F12**
3. Clique na aba **Console**
4. Preencha o formulário e clique "Solicitar Consultoria"
5. Veja a mensagem de erro que aparece

---

## 🛠️ Passo 2: Executar Verificador

1. Abra http://localhost:8000/firebase-check.html
2. Clique no botão "Executar Verificação"
3. Veja quais checks falharam

---

## 🔧 Passo 3: Corrigir Conforme o Erro

### Se vir: ❌ "Arquivo firebase-config.js"

**Problema**: Arquivo não existe ou não tem credenciais

**Solução**:
1. Confirme que `assets/js/firebase-config.js` existe
2. Abra e procure por linhas como:
```javascript
apiKey: "YOUR_API_KEY",
```

Se vir `YOUR_` = **PROBLEMA!** Não foi preenchido!

**Correção**:
1. Firebase Console > Seu Projeto > Configurações ⚙️
2. Clique em **Seu apps** ou **Aplicativos**
3. Copie o bloco `firebaseConfig` completo
4. Cole em `assets/js/firebase-config.js` (linhas 7-16)

---

### Se vir: ❌ "permission-denied" no console

**Problema**: Regras Firestore muito restritivas

**Solução**:
1. Firebase Console > Seu Projeto > Firestore Database
2. Clique em **Regras**
3. **Apague TUDO** que está lá
4. Cole isto:

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

5. Clique **Publicar**
6. Teste novamente em `/contato.html`

---

### Se vir: ❌ "Firestore is not initialized"

**Problema**: Credenciais vazias ou incorretas

**Solução**: Repita o Passo 3 acima com mais cuidado

---

## ✅ Passo 4: Testar

1. Abra `/contato.html`
2. Preencha com dados reais:
   - Nome: "Seu Nome"
   - Email: "seu@email.com"
   - Telefone: "+55 79 99999-9999"
   - Interesse: "Aquisição de Ativo"
   - Mensagem: "Teste"
3. Clique "Solicitar Consultoria"
4. Deve abrir seu cliente de email
5. Verifique em Firebase Console > Firestore > `contacts`

---

## 🚨 Se Ainda Não Funcionar

1. Abra console (F12) novamente
2. **Cole aqui a mensagem de erro exata:**

```
_____________________________________________
(cole a mensagem de erro aqui)
_____________________________________________
```

3. Se tiver mensagem de erro, verifique:

### Erro contém "permission"?
→ Verifique as regras Firestore (passo 3 acima)

### Erro contém "apiKey" ou "projectId"?
→ Credenciais não foram preenchidas

### Erro contém "failed" ou "network"?
→ Problema de internet

---

## 💡 Quick Checklist

- [ ] Criei projeto em firebase.google.com
- [ ] Ativei Firestore Database (modo TESTE)
- [ ] Copiei credenciais completas (não `YOUR_XXX`)
- [ ] Colei em `assets/js/firebase-config.js`
- [ ] Mudei regras Firestore para `allow read, write: if true;`
- [ ] Cliquei "Publicar" nas regras
- [ ] Testei formulário em `/contato.html`
- [ ] Verifiquei dados em Firebase Console > Firestore > `contacts`

---

## 📱 Teste Rápido pelo Console

Abra console (F12) e execute:

```javascript
await fetch('./assets/js/firebase-config.js')
  .then(r => r.text())
  .then(t => console.log(t.includes('YOUR_') ? '❌ CREDENCIAIS NÃO PREENCHIDAS' : '✓ CREDENCIAIS PARECEM OK'))
```

Se ver `✓ CREDENCIAIS PARECEM OK` = problema é nas regras Firestore

---

## 🎯 Resumo Rápido

```
❌ Erro ao enviar?
  ↓
Abra firebase-check.html
  ↓
Veja qual check falhou
  ↓
Siga a solução acima
  ↓
✓ Pronto!
```

---

## 💬 Ainda Não Funciona?

Verifique o arquivo **FIREBASE-DEBUG.md** para mais soluções detalhadas.


# 🚨 Firebase - Está Dando Erro? Solucione Aqui

## ⚡ Solução Rápida em 2 Minutos

### 1️⃣ Abra Este Verificador
```
http://localhost:8000/firebase-check.html
```

Clique no botão e veja o resultado.

### 2️⃣ Se vir erro em "permission-denied"

Faça isto:
1. Firebase Console > Seu Projeto > Firestore Database > **Regras**
2. Apague tudo
3. Cole:

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
5. Teste `/contato.html` novamente

### 3️⃣ Se vir erro sobre credenciais

Faça isto:
1. Firebase Console > Seu Projeto > Configurações ⚙️ > **Seu apps**
2. Copie o `firebaseConfig` inteiro
3. Cole em `assets/js/firebase-config.js` (substitua as linhas 7-16)

---

## 📖 Leia Conforme Necessário

| Situação | Arquivo |
|----------|---------|
| Quer solucionar AGORA | **CORRIGIR-FIREBASE.md** |
| Tem erro específico | **FIREBASE-DEBUG.md** |
| Quer entender tudo | **FIREBASE-IMPLEMENTACAO.md** |

---

## 🔍 Verificar Console

Abra Developer Tools: **F12**

Aba: **Console**

Procure por:
- ❌ `permission-denied` = Regras Firestore
- ❌ `apiKey` vazio = Credenciais não preenchidas
- ❌ `404` = Arquivo não encontrado
- ✅ `Contato salvo com ID:` = Funcionando!

---

## 🎯 Rápido & Fácil

```
Verificador → Vê qual check falhou → Siga solução correspondente → ✓ Resolvido
```

**Tempo: 5 minutos máximo**


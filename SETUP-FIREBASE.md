# Setup Firebase para Cathia Imóveis

## Guia de Configuração

### 1. Criar Projeto Firebase

1. Acesse [Firebase Console](https://console.firebase.google.com/)
2. Clique em "Novo Projeto"
3. Digite um nome (ex: "cathia-imoveis")
4. Configure Analytics conforme desejar
5. Clique em "Criar Projeto"

### 2. Configurar Firestore

1. No Console Firebase, vá para **Firestore Database**
2. Clique em **Criar banco de dados**
3. Escolha modo: **Iniciar no modo de teste** (para desenvolvimento)
4. Selecione localização: **Escolha a mais próxima do Brasil** (ex: `us-south1`)
5. Clique em **Criar**

### 3. Obter Credenciais

1. No Console Firebase, vá para **Configurações do Projeto** (⚙️)
2. Abra a aba **Seu apps** (ou **Aplicativos**)
3. Clique em **</> Web**
4. Registre seu app com um nome (ex: "cathia-site")
5. Copie as credenciais Firebase

Exemplo de credenciais (NÃO compartilhe):
```javascript
const firebaseConfig = {
    apiKey: "AIzaSyD...",
    authDomain: "cathia-imoveis.firebaseapp.com",
    projectId: "cathia-imoveis",
    storageBucket: "cathia-imoveis.appspot.com",
    messagingSenderId: "123456789",
    appId: "1:123456789:web:abc123def456"
};
```

### 4. Atualizar Configuração

1. Abra o arquivo `assets/js/firebase-config.js`
2. Substitua as credenciais com as do seu projeto:

```javascript
const firebaseConfig = {
    apiKey: "SEU_API_KEY",
    authDomain: "SEU_AUTH_DOMAIN",
    projectId: "SEU_PROJECT_ID",
    storageBucket: "SEU_STORAGE_BUCKET",
    messagingSenderId: "SEU_MESSAGING_SENDER_ID",
    appId: "SEU_APP_ID"
};
```

### 5. Configurar Permissões Firestore

No Console Firebase, acesse **Firestore > Regras**:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Permite leitura/escrita para todos (TESTE apenas)
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

**⚠️ IMPORTANTE**: Use regras mais restritas em produção!

### 6. Estrutura de Coleções

O Firebase criará automaticamente estas coleções:

#### `contacts`
Dados do formulário de contato:
```
{
  name: string,
  email: string,
  phone: string,
  subject: string,
  message: string,
  source: "contact_form",
  ip: string,
  timestamp: timestamp
}
```

#### `property_inquiries`
Inquéritos sobre imóveis específicos:
```
{
  propertyId: string,
  propertyName: string,
  name: string (opcional),
  email: string (opcional),
  phone: string (opcional),
  message: string (opcional),
  source: "property_page",
  ip: string,
  timestamp: timestamp
}
```

### 7. Usar nos Imóveis

Para rastrear cliques em imóveis, adicione ao botão:

```html
<a href="https://wa.me/557998129141" 
   data-inquiry-btn 
   data-property-id="imovel-1"
   data-property-name="Casa no Condomínio Morada do Rio"
   class="btn">
    Tenho Interesse
</a>
```

Depois inclua o script:
```html
<script type="module">
    import { initPropertyInquiry } from './assets/js/property-inquiry.js';
    initPropertyInquiry();
</script>
```

### 8. Visualizar Dados

1. No Console Firebase, vá para **Firestore Database**
2. Clique nas coleções para ver os dados registrados
3. Você verá timestamp, IP, e todos os dados coletados

### 9. Melhorias de Segurança (Produção)

Quando for para produção:

1. **Restrinja as regras**:
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /contacts/{document=**} {
      allow create: if request.auth != null || true;  // Apenas criação
      allow read, write: if false;  // Protege leitura
    }
    match /property_inquiries/{document=**} {
      allow create: if true;  // Permite criação
      allow read, write: if false;
    }
  }
}
```

2. **Habilite reCAPTCHA** para formulários

3. **Use variáveis de ambiente** (não exponha API keys)

## Funcionalidades Implementadas

✅ **Formulário de Contato** → Salva em `contacts`
✅ **Inquéritos de Imóveis** → Salva em `property_inquiries`
✅ **Timestamp automático** → Sabe quando foi enviado
✅ **Captura de IP** → Para análise geográfica
✅ **Fallback em Erro** → Continua funcionando mesmo se Firebase falhar
✅ **Integração com WhatsApp** → Mantém funções originais

## Troubleshooting

### Erro: "permission-denied"
- Verifique as regras Firestore
- Teste em modo de teste antes

### Erro: "Firebase SDK not available"
- Verifique a conexão com internet
- Confirme as credenciais estão corretas

### Dados não aparecem
- Abra Console Firefox/Chrome (F12)
- Procure por erros no console
- Verifique as regras Firestore

## Suporte
Para dúvidas, consulte:
- [Firebase Docs](https://firebase.google.com/docs)
- [Firestore Guide](https://firebase.google.com/docs/firestore)

# 🏠 Guia: Imóveis com Firebase em Tempo Real

## 📌 Como Funciona

### Sistema Automático
Agora a página `imoveis.html` carrega **automaticamente** todos os imóveis do Firebase! 

**Fluxo:**
1. Você adiciona um imóvel no **painel-admin.html** (painel de administração)
2. O imóvel é salvo no Firebase (collection `properties`)
3. A página `imoveis.html` detecta a mudança **em tempo real**
4. O novo imóvel aparece automaticamente no grid
5. Quando clica no imóvel, abre a página de detalhes (`imovel-firebase-dynamic.html`)

---

## ✅ Passo a Passo para Usar

### 1. Acessar o Painel Admin
- Abra: `painel-admin.html`
- Faça login com:
  - Email: `admin@cathia.com`
  - Senha: `admin123`

### 2. Adicionar Novo Imóvel
- Clique em **"Adicionar Imóvel"** (menu esquerdo)
- Preencha os campos:
  - **Nome**: Ex: "Casa no Centro"
  - **Preço**: Ex: 350000
  - **Localização**: Ex: "Centro, Aracaju - SE"
  - **Tipo**: Casa, Apartamento, Condomínio, Terreno
  - **Quartos**: Número de quartos
  - **Banheiros**: Número de banheiros
  - **Área**: Em m²
  - **Vagas**: Número de garagens
  - **URL da Imagem**: Link completo da imagem (ex: `https://...`)
  - **Descrição**: Detalhes do imóvel
  - **Exclusivo**: Marcar se for exclusivo
- Clique **"Salvar Imóvel"**

### 3. Ver na Página de Imóveis
- Abra: `imoveis.html`
- Seu novo imóvel aparecerá automaticamente no topo do grid!
- Clique no card para ver os detalhes

### 4. Editar ou Deletar
- No painel: Clique **"Editar"** para modificar
- Clique **"Deletar"** para remover (com confirmação)

---

## 📊 Estrutura do Firebase

### Collection: `properties`
Cada documento contém:
```json
{
  "title": "Casa no Condomínio Villaredo",
  "price": 560000,
  "location": "Barra dos Coqueiros, Aracaju - SE",
  "type": "casa",
  "bedrooms": 3,
  "bathrooms": 2,
  "area": 130,
  "garage": 1,
  "image": "https://exemplo.com/imagem.jpg",
  "description": "Casa com jardim...",
  "exclusive": true,
  "createdAt": "timestamp",
  "updatedAt": "timestamp"
}
```

---

## 🔄 Mantém Imóveis Antigos

Os imóveis hardcoded (aqueles que estavam no HTML) **continuam visíveis**:
- Casa no Condomínio Villaredo (imovel-1.html)
- Casa de Alto Padrão no Morada do Rio (imovel-2.html)
- Apartamento Villa Cristina (imovel-3.html)
- Casa no Villa dos Bosque (imovel-4.html)

**+ os novos imóveis do Firebase aparecem abaixo deles**

---

## 🖼️ URLs das Imagens

Você pode usar:

### Opção 1: Imagens Online
```
https://images.unsplash.com/photo-xxxxx?q=80&w=600
```

### Opção 2: Suas Próprias Imagens
1. Faça upload em um serviço gratuito:
   - **imgbb.com** (recomendado)
   - **imgur.com**
   - **Google Drive** (com link público)

2. Copie o link e cole em "URL da Imagem"

---

## 📝 Exemplo de Adicionar Imóvel

**Formulário preenchido:**
- Nome: "Apartamento de Luxo Ponta Verde"
- Preço: 950000
- Localização: "Ponta Verde, Aracaju - SE"
- Tipo: Apartamento
- Quartos: 3
- Banheiros: 2
- Área: 180
- Vagas: 2
- URL: `https://images.unsplash.com/photo-1502672260266-1c1ef2d93688`
- Descrição: "Apartamento moderno com vista para o mar..."
- Exclusivo: ✓ (marcado)

**Resultado:** Novo imóvel aparece em tempo real no grid de `imoveis.html`!

---

## 🔗 Páginas Envolvidas

| Arquivo | Função |
|---------|--------|
| `painel-admin.html` | Criar, editar, deletar imóveis |
| `imoveis.html` | Exibir grid de imóveis (carrega Firebase) |
| `imovel-firebase-dynamic.html` | Página de detalhes do imóvel |
| `assets/js/load-properties-firebase.js` | Script que conecta Firebase |
| `assets/js/admin-properties.js` | Operações CRUD no Firebase |
| `assets/js/admin-auth.js` | Autenticação do painel |

---

## ⚡ Atualizações em Tempo Real

- Quando você adiciona um imóvel no painel, ele aparece **imediatamente** em `imoveis.html`
- Quando você edita, a página atualiza **automaticamente**
- Quando você deleta, o imóvel desaparece **em tempo real**

Não precisa atualizar a página ou fazer nada manualmente!

---

## 🆘 Problemas Comuns

### Imóvel não aparece
1. Verifique se a URL da imagem é válida
2. Clique F5 na página `imoveis.html` para atualizar
3. Verifique o console do navegador (F12 → Console)

### Erro ao salvar
1. Verifique se o email/senha está correto
2. Verifique se o Firebase está habilitado
3. Tente novamente

### Imagem não carrega
- Use uma URL de imagem HTTPS (não HTTP)
- Teste a URL no navegador para confirmar que funciona

---

## 💡 Dicas

1. **Sempre use HTTPS** para URLs de imagens
2. **Descrições detalhadas** ajudam a vender mais
3. **Marque como "Exclusivo"** para destacar
4. **Ordene por preço** (mais recentes aparecem primeiro)
5. **Revise tudo** antes de salvar

---

## 📞 Contato

Para adicionar/editar imóveis, sempre acesse: `painel-admin.html`

Sua senha é: `admin123`

Bom trabalho! 🚀

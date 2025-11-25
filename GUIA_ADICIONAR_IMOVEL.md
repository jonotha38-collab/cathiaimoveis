# 📋 Guia Completo: Como Adicionar um Novo Imóvel

## 📍 Onde os Imóveis Aparecem

1. **Página Inicial (index.html)** - Seção de destaques
2. **Página de Imóveis (imoveis.html)** - Lista completa de todos os imóveis
3. **Página Individual (imovel.html)** - Detalhes completos de cada imóvel

---

## 🎯 Passo 1: Adicionar Card na Página de Imóveis (imoveis.html)

### Localização do Código
Abra o arquivo `imoveis.html` e encontre a seção:
```html
<div class="properties-grid" id="properties-grid">
```

### Estrutura do Card
Cada imóvel é um `<article>` com a classe `property-card`. Copie e cole este modelo:

```html
<article class="property-card fade-in">
    <a href="imovel-NOME-DO-IMOVEL.html">
        <div class="card-image">
            <img src="URL_DA_IMAGEM_PRINCIPAL" alt="Nome do Imóvel">
            <!-- Opcional: Tag Exclusivo -->
            <span class="tag-exclusive">Exclusivo</span>
        </div>
        <div class="card-content">
            <span class="card-price">R$ 1.500.000</span>
            <h3 class="card-title">Nome do Imóvel</h3>
            <div class="card-location">
                <i class="fas fa-map-marker-alt"></i> Bairro, Cidade - Estado
            </div>
            <div class="card-features">
                <span><i class="fas fa-bed"></i> 3</span>
                <span><i class="fas fa-bath"></i> 2</span>
                <span><i class="fas fa-ruler-combined"></i> 200m²</span>
            </div>
        </div>
    </a>
</article>
```

### Campos Obrigatórios:
- **URL_DA_IMAGEM_PRINCIPAL**: Link da foto principal (pode ser Unsplash, seu servidor, etc.)
- **R$ 1.500.000**: Preço do imóvel
- **Nome do Imóvel**: Título do imóvel
- **Bairro, Cidade - Estado**: Localização
- **3**: Número de quartos
- **2**: Número de banheiros
- **200m²**: Área total
- **imovel-NOME-DO-IMOVEL.html**: Nome do arquivo da página individual

---

## 🎯 Passo 2: Criar Página Individual do Imóvel

### Criar Novo Arquivo
1. Copie o arquivo `imovel.html`
2. Renomeie para `imovel-NOME-DO-IMOVEL.html` (ex: `imovel-apartamento-centro.html`)

### Editar os Dados

#### 1. Título da Página (linha 6):
```html
<title>Nome do Imóvel - Localização | Cathia Aguiar - Corretora de Imóveis</title>
```

#### 2. Breadcrumbs (linha 83):
```html
<a href="index.html">Home</a> / <a href="imoveis.html">Imóveis</a> / <span>Nome do Imóvel</span>
```

#### 3. Galeria de Imagens (linhas 86-94):
```html
<div class="property-gallery fade-in">
    <img src="URL_IMAGEM_PRINCIPAL_GRANDE" alt="Principal" class="main-image" id="main-image">
    <div class="thumbs">
        <img src="URL_IMAGEM_1" class="thumb active" onclick="changeImage(this)">
        <img src="URL_IMAGEM_2" class="thumb" onclick="changeImage(this)">
        <img src="URL_IMAGEM_3" class="thumb" onclick="changeImage(this)">
        <img src="URL_IMAGEM_4" class="thumb" onclick="changeImage(this)">
    </div>
</div>
```

#### 4. Informações do Imóvel (linhas 99-130):
```html
<div style="display: flex; justify-content: space-between; align-items: flex-start; margin-bottom: 1rem;">
    <div>
        <!-- Remova esta linha se não for exclusivo -->
        <span class="tag-exclusive" style="position: static; display: inline-block; margin-bottom: 0.5rem;">Exclusivo</span>
        <h1 style="margin-bottom: 0.5rem;">Nome do Imóvel</h1>
        <p style="color: var(--color-text-light);"><i class="fas fa-map-marker-alt"></i> Bairro, Cidade - Estado</p>
    </div>
    <div class="card-price" style="font-size: 2rem;">R$ 1.500.000</div>
</div>

<hr style="border: 0; border-top: 1px solid #eee; margin: 2rem 0;">

<h3>Sobre o Imóvel</h3>
<p style="margin-bottom: 1rem;">
    Descrição detalhada do imóvel aqui. Fale sobre características, localização, 
    acabamentos, diferenciais, etc.
</p>
<p>
    Continue a descrição aqui com mais detalhes sobre o imóvel.
</p>

<div class="amenities-table">
    <div class="amenity-item"><i class="fas fa-bed amenity-icon"></i> 3 Quartos</div>
    <div class="amenity-item"><i class="fas fa-bath amenity-icon"></i> 2 Banheiros</div>
    <div class="amenity-item"><i class="fas fa-car amenity-icon"></i> 2 Vagas</div>
    <div class="amenity-item"><i class="fas fa-ruler-combined amenity-icon"></i> 200m²</div>
    <!-- Adicione mais comodidades conforme necessário -->
    <div class="amenity-item"><i class="fas fa-swimming-pool amenity-icon"></i> Piscina</div>
    <div class="amenity-item"><i class="fas fa-wind amenity-icon"></i> Ar Condicionado</div>
</div>
```

---

## 🎯 Passo 3: Adicionar na Página Inicial (Opcional)

Se quiser destacar o imóvel na página inicial:

1. Abra `index.html`
2. Encontre a seção `<!-- Destaques -->` (linha 54)
3. Adicione o mesmo card que você criou em `imoveis.html`

---

## 📸 Onde Obter Imagens

### Opção 1: Unsplash (Gratuito)
- Acesse: https://unsplash.com
- Busque por: "luxury home", "modern house", "apartment"
- Clique na imagem → "Download" → Copie o link direto

### Opção 2: Suas Próprias Fotos
1. Salve as fotos na pasta `assets/img/`
2. Use o caminho: `assets/img/nome-da-foto.jpg`

### Opção 3: Links Diretos
- Use URLs de imagens hospedadas online

---

## ✅ Checklist ao Adicionar um Imóvel

- [ ] Card adicionado em `imoveis.html`
- [ ] Página individual criada (`imovel-NOME.html`)
- [ ] Todas as informações preenchidas corretamente
- [ ] Imagens adicionadas (pelo menos 1 principal)
- [ ] Preço formatado corretamente
- [ ] Link do card aponta para a página individual correta
- [ ] (Opcional) Adicionado na página inicial

---

## 🎨 Ícones Disponíveis (Font Awesome)

Use estes ícones para comodidades:
- `fa-bed` - Quartos
- `fa-bath` - Banheiros
- `fa-car` - Vagas de garagem
- `fa-ruler-combined` - Área
- `fa-swimming-pool` - Piscina
- `fa-wind` - Ar condicionado
- `fa-shield-alt` - Segurança 24h
- `fa-glass-cheers` - Área gourmet
- `fa-fire` - Lareira
- `fa-home` - Casa
- `fa-building` - Apartamento

---

## 💡 Dicas Importantes

1. **Nomes de Arquivos**: Use nomes simples, sem espaços (ex: `imovel-casa-jardim.html`)
2. **Imagens**: Use imagens de alta qualidade (mínimo 800x600px)
3. **Descrições**: Seja detalhado mas objetivo
4. **Preços**: Formate sempre como `R$ 1.500.000` (sem pontos nos milhares)
5. **Links**: Sempre verifique se os links estão corretos

---

## 🆘 Precisa de Ajuda?

Se tiver dúvidas, verifique os exemplos existentes ou entre em contato!


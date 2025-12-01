# Exemplo de Implementação - Firebase em Imóvel Existente

## Caso: Integrar Firebase em `imovel-2.html`

### Passo 1: Adicionar Atributos ao Botão

**ANTES:**
```html
<a href="https://wa.me/557998129141?text=Olá! Tenho interesse no imóvel Casa no condomínio Morada do Rio" 
   target="_blank" 
   class="btn-outline">
    Tenho Interesse via WhatsApp
</a>
```

**DEPOIS:**
```html
<a href="https://wa.me/557998129141?text=Olá! Tenho interesse no imóvel Casa no condomínio Morada do Rio" 
   target="_blank" 
   class="btn-outline"
   data-inquiry-btn 
   data-property-id="imovel-2"
   data-property-name="Casa no condomínio Morada do Rio">
    Tenho Interesse via WhatsApp
</a>
```

**O que muda:**
- Adiciona `data-inquiry-btn` - marca como botão de inquérito
- Adiciona `data-property-id` - ID único do imóvel
- Adiciona `data-property-name` - Nome completo do imóvel

### Passo 2: Adicionar Script no Final da Página

**Antes do `</body>`, adicione:**

```html
<!-- Firebase Property Inquiry Tracking -->
<script type="module">
    import { initPropertyInquiry } from './assets/js/property-inquiry.js';
    initPropertyInquiry();
</script>
```

**Localização completa:**
```html
    </div>

    <!-- Footer -->
    <footer class="footer">
        ...
    </footer>

    <!-- Script principal -->
    <script src="assets/js/main.js"></script>

    <!-- Firebase Property Inquiry Tracking -->
    <script type="module">
        import { initPropertyInquiry } from './assets/js/property-inquiry.js';
        initPropertyInquiry();
    </script>
</body>
</html>
```

---

## Exemplo Completo - Seção de Contato Atualizada

```html
<!-- Seção de Chamada para Ação -->
<section style="background: var(--color-primary-light); padding: 3rem 2rem; margin-top: 3rem; border-radius: 8px;">
    <div class="container">
        <h2 style="color: var(--color-primary); text-align: center; margin-bottom: 2rem;">
            Interessado Neste Imóvel?
        </h2>
        
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 2rem; max-width: 600px; margin: 0 auto;">
            <!-- Botão WhatsApp com rastreamento -->
            <a href="https://wa.me/557998129141?text=Olá! Tenho interesse no imóvel Casa no condomínio Morada do Rio"
               target="_blank"
               class="btn"
               data-inquiry-btn 
               data-property-id="imovel-2"
               data-property-name="Casa no condomínio Morada do Rio"
               style="display: flex; align-items: center; justify-content: center; gap: 8px; text-decoration: none;">
                <i class="fab fa-whatsapp"></i> WhatsApp
            </a>
            
            <!-- Botão Email -->
            <a href="contato.html"
               class="btn-outline"
               style="display: flex; align-items: center; justify-content: center; gap: 8px; text-decoration: none; border: 1px solid var(--color-primary);">
                <i class="fas fa-envelope"></i> E-mail
            </a>
        </div>
    </div>
</section>
```

---

## Múltiplos Botões com Rastreamento

Se tiver vários botões na página:

```html
<!-- Botão 1: WhatsApp -->
<a href="https://wa.me/557998129141"
   data-inquiry-btn 
   data-property-id="imovel-2"
   data-property-name="Casa no condomínio Morada do Rio"
   class="btn">
    WhatsApp
</a>

<!-- Botão 2: Email -->
<a href="contato.html"
   data-inquiry-btn 
   data-property-id="imovel-2"
   data-property-name="Casa no condomínio Morada do Rio"
   class="btn">
    E-mail
</a>

<!-- Botão 3: Agendar visita (liga direto) -->
<a href="tel:+5579998129141"
   data-inquiry-btn 
   data-property-id="imovel-2"
   data-property-name="Casa no condomínio Morada do Rio"
   class="btn">
    Ligar
</a>
```

Todos serão rastreados automaticamente!

---

## Dados Gravados no Firebase

Quando alguém clicar no botão com `data-inquiry-btn`, isso será salvo:

```
Collection: property_inquiries
Document: {
    propertyId: "imovel-2",
    propertyName: "Casa no condomínio Morada do Rio",
    timestamp: 2024-01-15 14:30:45,
    ip: "203.0.113.0",
    source: "property_page",
    userAgent: "Mozilla/5.0..."
}
```

---

## O que NÃO é rastreado

- Cliques em botões **sem** `data-inquiry-btn`
- Links normais sem os atributos
- Redirecionamentos para WhatsApp/Email continuam funcionando normalmente

---

## Checklist de Implementação

Para `imovel-2.html`:

- [ ] Adicione `data-inquiry-btn` ao botão WhatsApp
- [ ] Adicione `data-property-id="imovel-2"`
- [ ] Adicione `data-property-name="Casa no condomínio Morada do Rio"`
- [ ] Coloque o script de inicialização no final da página
- [ ] Teste clicando no botão
- [ ] Verifique em Firebase Console > Firestore > property_inquiries

---

## Teste Rápido

1. Abra `imovel-2.html` no navegador
2. Clique no botão de interesse
3. Vai para WhatsApp normalmente
4. Abra Firebase Console > Firestore
5. Vá em `property_inquiries`
6. Deve ver um novo documento com o clique

---

## Problemas Comuns

**P: Botão não funciona?**
- Verifique se há erro no console (F12)
- Confirme que `property-inquiry.js` existe em `assets/js/`

**P: Dados não aparecem no Firebase?**
- Verifique que `firebase-config.js` está com credenciais corretas
- Veja se as regras Firestore permitem criação

**P: WhatsApp/Email não abre?**
- O rastreamento é assíncrono, não bloqueia o link
- Testou em uma página diferente, tenta lá também

---

## Próximo Passo

Após implementar em um imóvel, faça em todos os outros também:
- Basta copiar os 3 atributos `data-*` para o botão
- Ajustar `data-property-id` e `data-property-name` para cada imóvel
- Script no final da página só precisa uma vez

**Resultado**: Dashboard completo do comportamento dos visitantes! 📊

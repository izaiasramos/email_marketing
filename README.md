# email_marketing
Email marketing estruturado com boas praticas para ser aceito pelos agentes de email

# Email Marketing Otimizado para Deliverability

Este projeto contém um exemplo de email marketing desenvolvido em HTML e CSS puro, otimizado para garantir alta compatibilidade e aceitação por agentes de email (como Gmail, Outlook, Yahoo, etc.). O objetivo é demonstrar boas práticas específicas para email marketing, evitando problemas de renderização e aumentando a probabilidade de entrega na caixa de entrada.

Após a criação do email, ele foi testado e implementado utilizando o **Mautic**, uma plataforma de automação de marketing, para disparo em um novo segmento e campanha, focando em contatos que não abriram um email anterior.

---

## Importância das Boas Práticas em Email Marketing

Emails de marketing enfrentam desafios para serem aceitos por agentes de email devido a filtros de spam, variações de renderização e restrições de segurança. Seguir boas práticas específicas é essencial para:

- **Evitar a Caixa de Spam**: Filtros de spam avaliam a estrutura do código, links e conteúdo. Um código bem estruturado reduz o risco de ser marcado como spam.
- **Garantir Renderização Correta**: Diferentes clientes de email (Gmail, Outlook, etc.) interpretam HTML/CSS de forma distinta. Um código otimizado assegura que o email seja exibido corretamente em todos os dispositivos e clientes.
- **Melhorar a Experiência do Usuário**: Um email que carrega rapidamente e é visualmente consistente aumenta o engajamento do destinatário.
- **Aumentar a Taxa de Entrega**: Boas práticas ajudam a passar por verificações de autenticação (DKIM, SPF, DMARC) e melhoram a reputação do remetente.

---

## Boas Práticas Utilizadas no Código

O código foi desenvolvido com as seguintes boas práticas para garantir compatibilidade e deliverability:

1. **Uso de DOCTYPE e Estrutura HTML Otimizada**:
   - Utilizamos `<!DOCTYPE HTML PUBLIC "-//W3C//DTD XHTML 1.0 Transitional //EN">` para garantir compatibilidade com a maioria dos clientes de email.
   - Incluímos namespaces para suporte a clientes como Outlook (`xmlns:v`, `xmlns:o`).

2. **Layout Baseado em Tabelas**:
   - O design é construído com `<table>` em vez de `<div>`, pois muitos clientes de email (como Outlook) não suportam bem layouts baseados em CSS moderno (ex.: Flexbox, Grid).
   - Exemplo:
     ```html
     <table width="100%" border="0" cellspacing="0" cellpadding="0" bgcolor="#f4f4f4">
       <tr>
         <td align="center">
           <table width="600" border="0" cellspacing="0" cellpadding="0" bgcolor="#ffffff">
             <!-- Conteúdo -->
           </table>
         </td>
       </tr>
     </table>
     ```

3. **CSS Inline e Estilos Limitados**:
   - A maior parte dos estilos foi aplicada diretamente nos elementos HTML (CSS inline) para evitar que clientes de email ignorem ou interpretem mal folhas de estilo externas.
   - Estilos gerais no `<head>` foram minimizados e usados apenas para regras amplamente suportadas (ex.: `font-family`, `color`).
   - Exemplo de estilo no `<head>`:
     ```css
     body, table, td, p, a { -webkit-text-size-adjust: 100%; -ms-text-size-adjust: 100%; }
     table, td { mso-table-lspace: 0pt; mso-table-rspace: 0pt; }
     ```

4. **Suporte Específico para Outlook**:
   - Incluímos blocos condicionais para Outlook (`<!--[if mso]>`) para ajustar renderização, como remoção de bordas arredondadas e ajustes de espaçamento.
   - Exemplo:
     ```html
     <!--[if mso]>
     <style>
       .header, .footer {
         background: #ee4135 !important;
       }
     </style>
     <![endif]-->
     ```

5. **Imagens Otimizadas**:
   - Todas as imagens possuem `alt` text para acessibilidade e caso não sejam carregadas.
   - Imagens são hospedadas em URLs públicas para garantir carregamento.
   - Exemplo:
     ```html
     <img src="https://exemplo.com/imagem.jpg" alt="Descrição da Imagem" style="border:0;">
     ```

6. **Responsividade com Media Queries**:
   - Utilizamos `@media screen` para ajustar o layout em dispositivos móveis, garantindo que o email seja legível em telas menores.
   - Exemplo:
     ```css
     @media screen and (max-width: 600px) {
       .header h1 {
         font-size: 24px;
       }
       .logo {
         width: 100px;
       }
     }
     ```

7. **Fontes Seguras e Fallback**:
   - Usamos fontes seguras para email (`Arial, sans-serif`) e evitamos fontes personalizadas que não são suportadas.
   - Exemplo:
     ```html
     <body style="font-family: Arial, sans-serif;">
     ```

8. **Links e CTAs Claros**:
   - O botão de CTA (`<a>`) foi estilizado com cores contrastantes e inclui `target="_blank"` para abrir em uma nova aba.
   - Exemplo:
     ```html
     <a href="https://www.exemplo.com.br" target="_blank" class="cta-button">www.exemplo.com.br</a>
     ```

---

## Códigos HTML e CSS a Evitar

Alguns tipos de HTML e CSS não são suportados ou podem causar problemas em agentes de email. Aqui estão os principais a evitar:

1. **Layouts Modernos com Flexbox ou Grid**:
   - Clientes como Outlook não suportam `display: flex` ou `display: grid`. Sempre use tabelas para layouts.

2. **CSS Externo ou JavaScript**:
   - Folhas de estilo externas (`<link>`) e JavaScript (`<script>`) são bloqueados pela maioria dos clientes de email por questões de segurança.
   - Solução: Use CSS inline ou no `<head>` com regras simples.

3. **Propriedades CSS Avançadas**:
   - Evite propriedades como `position: absolute`, `float`, `z-index`, `transform`, ou `animation`, pois não são amplamente suportadas.
   - Exemplo a evitar:
     ```css
     .elemento {
       position: absolute;
       top: 10px;
     }
     ```

4. **Vídeos ou Elementos Interativos**:
   - Tags `<video>`, `<iframe>`, ou formulários interativos (`<form>`) são bloqueados ou não funcionam bem.
   - Solução: Use imagens ou links para redirecionar o usuário.

5. **Imagens de Fundo com CSS**:
   - Propriedades como `background-image` não são suportadas em muitos clientes (ex.: Outlook). Use cores sólidas ou imagens inline.
   - Exemplo a evitar:
     ```css
     .secao {
       background-image: url('fundo.jpg');
     }
     ```

6. **Fontes Personalizadas**:
   - Evite `@font-face` ou fontes não seguras. Use fontes padrão como Arial, Helvetica, ou Times New Roman.

7. **Estilos Excessivos ou Complexos**:
   - Evite seletores complexos (ex.: `.classe > .subclasse`) ou pseudo-classes (ex.: `:hover`), pois não são amplamente suportados.
   - Exemplo a evitar:
     ```css
     a:hover {
       color: blue;
     }
     ```

---

## Implementação e Testes com Mautic

Após a criação do email, ele foi testado e implementado usando o **Mautic**:

1. **Criação do Email**:
   - O email foi criado no Mautic como um "Segment Email" e o código HTML/CSS foi inserido no modo "Custom HTML".

2. **Testes de Deliverability**:
   - Testes foram realizados para garantir que o email fosse aceito por agentes de email, verificando renderização em diferentes clientes (Gmail, Outlook, etc.) e usando ferramentas como Mail-Tester para avaliar o risco de spam.

3. **Integração na Campanha**:
   - O email foi integrado a uma campanha no Mautic, direcionado a um novo segmento de contatos que não abriram um email anterior, com disparos programados e acompanhamento de métricas (aberturas, cliques, etc.).

---

## Como Usar Este Projeto

1. **Clone o Repositório**:
   ```bash
   git clone https://github.com/seu-usuario/nome-do-repositorio.git
   ```

2. **Visualize o Email**:
   - Abra o arquivo `index.html` em um navegador para visualizar o design do email.

3. **Teste e Implemente**:
   - Copie o código HTML/CSS e insira-o em sua plataforma de email marketing (como Mautic, Mailchimp, etc.).
   - Realize testes de renderização e deliverability antes de enviar para sua base de contatos.

4. **Ajustes**:
   - Substitua as URLs de imagens e links pelo conteúdo real da sua campanha.
   - Ajuste cores, fontes e textos conforme necessário, mantendo as boas práticas descritas.

---

## Licença

Este projeto está licenciado sob a [MIT License](LICENSE). Sinta-se à vontade para usar, modificar e compartilhar, desde que mantenha os créditos ao autor original.

---

## Contato

Se tiver dúvidas ou sugestões, abra uma issue no repositório ou entre em contato comigo diretamente pelo GitHub.

Feito com 💻 por [Seu Nome].

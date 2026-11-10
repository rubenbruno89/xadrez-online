# ▶ COMECE AQUI — cole este prompt na sua IA

> Anexe o `.zip` (ou arraste a pasta descompactada) na sua ferramenta de IA favorita
> — Lovable, v0, Bolt, Cursor, Replit, Claude ou ChatGPT — e cole o texto abaixo.

---

Você é um engenheiro front-end sênior. Vou te entregar a **exportação estática de um site já existente** (arquivos HTML, CSS, JS e assets: imagens, fontes, ícones e mídia), gerada por uma extensão de clonagem. No pacote há um `AI_CONTEXT.md` com a stack, a paleta, a tipografia e a estrutura de seções da página.

- **Site de origem:** https://a1-1pagm8nfiumnjkb7vaek0skl2.infusion-ai.cloud/
- **Stack detectada na origem:** Tailwind CSS
- **Paleta principal:** rgb(13, 15, 20), rgb(255, 255, 255), rgb(247, 248, 250), rgb(91, 100, 114), rgb(85, 119, 246)
- **Tipografia:** Figtree
- **Breakpoints:** mobile / tablet / desktop

**Objetivo:** reconstruir este site como um projeto limpo, editável e responsivo — fiel ao visual original, mas com código organizado que eu consiga evoluir.

Faça nesta ordem:
1. Leia o `AI_CONTEXT.md` e o `index.html` para entender layout, seções, paleta e fontes.
2. Recrie a página **seção por seção** (header, hero, conteúdo, rodapé) mantendo posição, proporções, espaçamentos, cores e tipografia o mais próximo possível do original.
3. Use os **assets do pacote** (`/assets`, `/css`, `/js`). Referencie as imagens, ícones, fontes e vídeos que vieram junto — não invente novos.
4. Estruture em **componentes reutilizáveis** (usando a stack que eu indicar, ou a padrão do seu ambiente). Priorize HTML semântico e acessibilidade: foco visível, `alt` nas imagens, bom contraste.
5. Deixe **responsivo**, respeitando os breakpoints acima.
6. **Mantenha os textos e o conteúdo reais** que estão no clone.
7. Onde houver formulário, login, busca ou dados que dependam de backend, deixe a interface pronta e marque com `TODO` — não invente backend.

Regras:
- Não adicione seções, páginas ou recursos que não existem no original.
- Na dúvida sobre algum detalhe, siga o que o `AI_CONTEXT.md` descreve.
- Entregue código limpo, com comentários onde ajudarem.

Depois de reconstruir fielmente, aplique as mudanças que eu quero:

```
[DESCREVA AQUI O QUE VOCÊ QUER MUDAR]
Exemplos:
- Trocar a paleta para as cores da minha marca (#______, #______).
- Reescrever o texto do hero para: "____________".
- Remover a seção de preços e adicionar uma seção de depoimentos.
- Adaptar o conteúdo para o meu produto: ____________.
```

Comece confirmando em 2-3 linhas o que você entendeu do site e da stack; depois mãos à obra.

---

# Briefing para reconstrucao por IA

Voce recebeu um clone **estatico** de uma pagina web. Use esta descricao como
REFERENCIA de layout e estilo para reconstruir a interface como componentes na
ferramenta/stack de sua preferencia. Nao trate os arquivos como import direto — o
objetivo e recriar fielmente o visual e a estrutura, com codigo limpo.

## Identidade da pagina
- **URL de origem:** https://a1-1pagm8nfiumnjkb7vaek0skl2.infusion-ai.cloud/
- **Titulo:** Xadrez Online
- **Idioma:** pt-BR
- **Viewport:** width=device-width, initial-scale=1.0

## Stack detectada
Tecnologias identificadas na pagina de origem (use como pista para a reconstrucao):
- Tailwind CSS

## Paleta de cores (mais frequentes)
- `rgb(13, 15, 20)`
- `rgb(255, 255, 255)`
- `rgb(247, 248, 250)`
- `rgb(91, 100, 114)`
- `rgb(85, 119, 246)`

## Tipografia
- Figtree

## Estrutura / secoes (na ordem do DOM)
1. <section> [class: md:w-1/2 p-6 md:p-6] · 3 blocos filhos
2. <section> — "Nova partida" [class: md:w-1/2 p-6 flex] · 1 blocos filhos

## Outline de titulos
- H1: Nova partida

## Contagem de elementos
- Imagens: 0 · Links: 0 · Scripts: 4 · Formularios: 0

## Instrucao sugerida para a IA
> Reconstrua esta pagina como uma interface responsiva, seguindo a paleta, a
> tipografia e a ordem de secoes acima. Priorize semantica, acessibilidade e
> codigo limpo. Consulte os arquivos HTML/CSS do clone para detalhes visuais.

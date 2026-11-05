# Xadrez Online

Jogo de xadrez para duas pessoas, cada uma no seu aparelho, em tempo real. Uma pessoa cria a partida, envia o link a um amigo e quem abrir o link entra como pretas. Não precisa de cadastro nem de login.

## Funcionalidades

- **Partida por link:** quem cria joga de brancas; quem abre o link primeiro entra de pretas. Quem abre depois acompanha como espectador.
- **Regras completas:** roque, _en passant_, promoção do peão (dama, torre, bispo ou cavalo), xeque, xeque-mate, afogamento, material insuficiente, regra dos 50 lances e tripla repetição.
- **Tempo real:** os lances do adversário aparecem sozinhos, sem recarregar a página.
- **Chat entre os jogadores:** mensagens de até 500 caracteres durante a partida. Só quem está jogando vê e usa o chat; espectadores ficam de fora.
- **Empate e desistência:** proposta de empate (o adversário aceita ou recusa) e desistência com confirmação.
- **Painel da partida:** lista de lances em notação algébrica, peças capturadas, vantagem de material e indicação de quem está na vez.
- **Feito para o celular:** layout responsivo, pensado para telas pequenas.

## Como funciona

Não há contas de usuário. Ao criar ou entrar em uma partida, o navegador gera um token secreto que fica no `localStorage` (`xadrez:<hash>`). O token identifica a cor de quem joga e é exigido em toda ação: lance, empate, desistência e chat. A partida é identificada por um `hash` aleatório presente na URL (`/p/<hash>`).

As regras do xadrez rodam no navegador (`src/lib/chess.ts`): a lista de lances é reproduzida a cada atualização para montar o tabuleiro. O servidor guarda os lances e confere que a jogada vem do jogador da vez, com controle de versão por número do lance (`ply`) para evitar jogadas duplicadas ou fora de ordem.

A tela consulta o servidor a cada 2 s para os lances e a cada 3 s para o chat. As consultas pausam quando a aba fica em segundo plano e o chat deixa de consultar quando a partida termina.

## Tecnologias

- React 19, TypeScript e Vite
- Tailwind CSS 4 e lucide-react
- react-router-dom
- Banco PostgreSQL com funções de servidor em SQL

## Estrutura

```
frontend/
  src/
    pages/
      HomePage.tsx        Tela inicial e criação da partida
      GamePage.tsx        Tabuleiro, ações, lances e chat
    components/
      Board.tsx           Tabuleiro e peças
      ChatPartida.tsx     Chat entre os jogadores
      ui/                 Botão, cartão, modal, campos e avisos
    lib/
      chess.ts            Regras do xadrez
      api.ts              Chamadas às funções de servidor
      sf-ids.ts           Identificadores das funções de servidor
```

## Banco de dados

**`partidas`**

| Coluna | Tipo | Descrição |
|---|---|---|
| `id` | serial | Chave primária |
| `hash` | texto | Identificador público da partida (vai na URL) |
| `token_brancas` | texto | Token secreto de quem joga de brancas |
| `token_pretas` | texto | Token secreto de quem joga de pretas |
| `lances` | texto | Lances em notação UCI separados por espaço |
| `ply` | inteiro | Quantidade de lances jogados |
| `status` | texto | `aguardando`, `em_andamento` ou `finalizada` |
| `resultado` | texto | `1-0`, `0-1` ou `1/2-1/2` |
| `motivo` | texto | Motivo do fim (xeque-mate, desistência, acordo...) |
| `oferta_empate` | texto | Cor que propôs empate (`w` ou `b`), se houver |
| `criada_em`, `atualizada_em` | timestamp | Controle de datas |

**`mensagens`**

| Coluna | Tipo | Descrição |
|---|---|---|
| `id` | serial | Chave primária e ordem das mensagens |
| `hash` | texto | Partida a que a mensagem pertence |
| `cor` | texto | Cor de quem enviou (`w` ou `b`) |
| `texto` | texto | Conteúdo (máximo de 500 caracteres) |
| `criada_em` | timestamp | Data e hora do envio |

## Funções de servidor

| Função | O que faz |
|---|---|
| `xadrez_criar` | Cria a partida e devolve o `hash` e o token das brancas |
| `xadrez_estado` | Devolve o estado atual da partida e a cor de quem consulta |
| `xadrez_entrar` | Registra o segundo jogador como pretas |
| `xadrez_jogar` | Grava um lance, validando a vez e o número do lance |
| `xadrez_desistir` | Encerra a partida por desistência |
| `xadrez_empate` | Propõe, aceita ou recusa empate |
| `xadrez_chat_listar` | Lista as mensagens novas da partida (só para jogadores) |
| `xadrez_chat_enviar` | Envia uma mensagem (só para jogadores) |

## Rodando localmente

Requisitos: Node.js 20.19 ou superior.

```bash
cd frontend
npm install
npm run dev
```

Outros comandos úteis:

```bash
npm run build           # verificação de tipos e build de produção
npx tsc -b --noEmit     # só a verificação de tipos
npm run lint            # ESLint
```

O app depende do banco e das funções de servidor descritos acima. Sem eles, a interface abre, mas não é possível criar ou jogar partidas.

## Limitações conhecidas

- Quem perde o token (limpa os dados do navegador ou troca de aparelho) não consegue retomar o lugar na partida; passa a ver como espectador.
- Não há relógio de xadrez, ranking, histórico de partidas nem escolha de cor.
- As mensagens do chat não têm moderação, filtro de palavras nem limpeza automática.

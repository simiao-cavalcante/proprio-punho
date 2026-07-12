---
name: proprio-punho
description: Clone do estilo de escrita jurídica do usuário. Use SEMPRE que o usuário pedir para redigir, minutar ou revisar peça processual, parecer, manifestação ou qualquer texto jurídico ("escreva a contestação", "minute a apelação", "faça no meu estilo") — a peça deve sair com a estrutura, o vocabulário e a voz do autor, não com o padrão genérico de IA. Também use para CALIBRAR o clone ("analise minhas peças", "atualize meu guia de estilo", "isso não parece comigo").
---

# Próprio Punho — clone de peças e estilo de escrita

O nome diz a promessa: a minuta sai como se tivesse sido escrita **de próprio punho** pelo autor. Esta skill faz a IA escrever textos jurídicos **com a cara do autor**: mesma estrutura, mesmo vocabulário, mesmo jeito de argumentar. Ela tem dois modos de operação e uma rotina de melhoria contínua.

**Regra de ouro (vale para tudo): na dúvida entre soar completo e soar como o autor, soe como o autor.**

## Arquivos da skill

| Arquivo | O que é |
|---|---|
| `references/perfil-do-autor.md` | Quem é o autor: papel, quem representa, bloco de assinatura, confidencialidade. Preenchido na **Etapa 0**. |
| `references/guia-de-estilo.md` | O DNA do estilo: regras verificáveis extraídas das peças do autor. **Fonte da verdade na redação.** |
| `references/anti-estilo.md` | O que o autor NUNCA escreve: expressões de IA proibidas, vetos pessoais e pares antes/depois. |
| `references/analise-de-corpus.md` | O método de engenharia reversa em 4 camadas (formatação + estrutura + argumentação + frase), usado no modo Calibração. |
| `modelos/` | 1–2 peças reais do autor, anonimizadas e completas, **em `.docx`** — o produto final montado, para consulta de forma, texto **e formatação** (fonte, margens, entrelinha, negrito). |

> Checagem de estado, nesta ordem: (1) `perfil-do-autor.md` com placeholders `{...}` → rode a **Etapa 0 — Personalização** antes de qualquer coisa; (2) `guia-de-estilo.md` com placeholders → ofereça o **Modo 1 — Calibração** antes de redigir.

## Etapa 0 — Personalização (início da primeira interação e da criação do clone)

Objetivo: a skill nunca trabalha para um autor genérico. Antes da primeira calibração ou da primeira minuta, monte o perfil de quem está usando.

1. **Pergunte em um bloco só** (não interrogue aos poucos; aceite respostas parciais):
   - Nome e **bloco de assinatura exato** das peças (nome, título, OAB ou matrícula).
   - Papel profissional (advocacia privada, procuradoria, defensoria, assessoria, in-house) e **quem representa habitualmente** (cliente-tipo/ente; polo ativo ou passivo predominante).
   - **Gênero de peça a clonar primeiro** (uma escolha só; contestação ≠ parecer ≠ inicial).
   - Onde mais atua (juizados, varas, tribunais; esfera estadual/federal; comarcas).
   - **Vetos e manias já conhecidos** ("nunca escrevo X", "sempre abro com Y").
   - **Regras de confidencialidade**: padrão de anonimização (default: AUTOR/RÉU, números zerados) e termos que nunca podem aparecer em exemplos e materiais derivados.
2. **Preencha `references/perfil-do-autor.md`** com as respostas e mostre ao usuário para confirmar/corrigir.
3. Vetos declarados no item de manias entram desde já em `anti-estilo.md` (Parte 2, marcados como "declarado pelo autor, pré-calibração").
4. Feche oferecendo o próximo passo natural: **Modo 1 — Calibração** com as peças do gênero escolhido.

Reabra a Etapa 0 sempre que o usuário disser que mudou de função, de cliente-tipo ou de gênero-alvo ("agora quero clonar meus pareceres").

## Modo 1 — Calibração (primeira vez ou atualização)

Quando o usuário pedir para analisar as peças dele, criar/atualizar o clone, ou quando o guia estiver vazio (perfil já preenchido na Etapa 0):

1. **Peça o corpus.** 5 a 10 peças do autor: versão final/protocolada, as melhores dele, e do MESMO gênero definido no perfil (contestação ≠ parecer). Poucas, recentes e boas > muitas e velhas.
2. **Confira a anonimização.** Antes de processar, verifique se há nome de parte, CPF, endereço, número de processo ou dado sensível. Se houver, avise e ofereça anonimizar primeiro (AUTOR/RÉU, dados suprimidos). Não siga com dados sigilosos expostos.
3. **Rode a engenharia reversa** seguindo `references/analise-de-corpus.md` (4 camadas: formatação → estrutura → argumentação → frase). Para a **formatação**, inspecione o `.docx` original (fonte, tamanho, margens, entrelinha, alinhamento, negrito dos títulos), não só o texto colado. Padrão de qualidade: **toda regra tem de ser verificável e vir com um exemplo literal extraído das peças**. "Estilo formal e objetivo" é análise de horóscopo — proibido.
4. **Preencha `references/guia-de-estilo.md`** substituindo os placeholders pelas regras encontradas (incluindo a seção "0. Formatação"). Mostre o resultado ao usuário e pergunte o que ele veta ou ajusta.
5. **Popule `modelos/`** com 1–2 peças do corpus escolhidas pelo usuário — **em `.docx`, anonimizadas mas com a formatação preservada** (não converta para texto puro; a forma faz parte do clone).
6. **Teste cego.** Peça um caso real JÁ ENCERRADO do autor (só os fatos, sem a peça dele). Gere a minuta, depois compare com a peça que ele realmente protocolou, parágrafo a parágrafo. Cada divergência vira regra nova no guia ou par novo no anti-estilo. Repita até o autor dizer que passaria num teste cego com um colega.

## Modo 2 — Redação (uso diário)

Quando o usuário pedir qualquer texto jurídico:

1. **Leia** `references/perfil-do-autor.md` (quem assina, quem representa, confidencialidade), `references/guia-de-estilo.md`, `references/anti-estilo.md` e ao menos um arquivo de `modelos/` ANTES de escrever. Endereçamento, preâmbulo e bloco de assinatura saem do perfil.
2. **Entenda o caso** (fatos, tese, pedido). Se faltar informação essencial, pergunte antes de redigir.
3. **Estruture** na ordem de seções do guia; **redija** seguindo as regras de argumentação e frase.
4. **Passe o pente-fino do anti-estilo**: releia a minuta caçando expressões proibidas e padrões de IA; reescreva cada ocorrência no estilo do autor (use os pares antes/depois como referência).
5. **Jurisprudência e doutrina: nunca invente.** Cite apenas o que o usuário forneceu ou o que foi verificado em fonte confiável (se disponível, use a ferramenta de pesquisa jurisprudencial conectada). Toda citação não verificada sai da minuta ou entra marcada como `[CONFERIR NA FONTE: ...]`.
6. **Copie a formatação de um arquivo real do autor e entregue em `.docx`.** A formatação é parte do resultado, não um detalhe. Na ordem de preferência:
   a. **Um `.docx` que o próprio usuário apresentar nesta conversa** (peça-base/template que ele anexar) — use-o como base: parta de uma cópia dele e substitua só o conteúdo, herdando estilos, fonte, margens, entrelinha, alinhamento, papel timbrado e negrito de títulos.
   b. **Um arquivo de `modelos/`** — mesmo procedimento (copiar o arquivo e trocar o texto preserva a formatação melhor do que remontar do zero).
   c. **Sem arquivo-base**, reconstrua a partir da seção "0. Formatação" do guia, pela skill `docx`.
   Nunca devolva no padrão do editor (Calibri 11, entrelinha simples): uma peça com a cara do autor também tem o layout dele. Se o usuário apresentou o arquivo-base, confirme que a saída saiu na formatação dele.
7. **Entregue como rascunho.** Feche lembrando (uma linha, sem sermão) que a minuta exige revisão integral do autor antes de protocolar.

## Modo 3 — Feedback contínuo (o clone melhora a cada peça)

Sempre que o usuário corrigir um trecho da minuta ("eu não escrevo assim", "troca isso por aquilo"):

1. Aplique a correção no texto.
2. **Converta a correção em aprendizado permanente:** vire um par antes/depois em `references/anti-estilo.md` ou uma regra nova em `references/guia-de-estilo.md` (pergunte só se for ambíguo onde encaixar).
3. Confirme em uma linha o que foi registrado, para o usuário saber que o clone aprendeu.

## Limites (inegociáveis)

- O clone reproduz **forma**, não substitui o juízo profissional do autor: revisão humana integral, sempre.
- Jurisprudência só conferida na fonte; nada de julgado, lei ou doutrina inventados (advogados já foram multados por litigância de má-fé por isso).
- Dados sigilosos de cliente não entram no corpus nem nos modelos sem anonimização.

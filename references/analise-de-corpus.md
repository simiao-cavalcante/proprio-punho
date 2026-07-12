# Análise de corpus — engenharia reversa do estilo em 4 camadas

Método do Modo Calibração. O objetivo NÃO é elogiar o texto nem descrevê-lo em adjetivos: é extrair **regras verificáveis** que permitam a outra pessoa (ou a uma IA) reproduzir o estilo — inclusive a **formatação**, porque uma peça com a cara do autor também tem o layout dele.

> **Formatação exige o arquivo, não o texto.** As Camadas 1–3 saem do texto; a Camada 0 (formatação) só é observável no `.docx`/`.pdf` original — margens, fonte, entrelinha e negrito se perdem quando a peça é colada como texto puro. Peça os modelos em `.docx` e inspecione o arquivo (no Claude Code, via `python-docx`: `Document(...).styles['Normal'].font`, `sections[0].*_margin`, `paragraph_format.alignment/line_spacing`, e `run.bold` dos títulos).

## Padrão de qualidade de uma regra

Uma regra só entra no guia se passar nos dois testes:

1. **Verificável** — dá para checar objetivamente se uma minuta cumpre ou viola a regra. ("Períodos de 2 a 4 linhas" ✅; "escrita fluida" ❌)
2. **Exemplificada** — vem acompanhada de um trecho literal extraído do corpus que a demonstra, com indicação de qual peça.

Análise que devolve "estilo formal, objetivo e tecnicamente preciso" é **análise de horóscopo**: serve para qualquer advogado do Brasil e não ensina nada. Descarte e refaça.

## Camada 0 — Formatação e layout (o documento)

Observável só no arquivo original. Extrair como regras concretas:

- **Fonte:** família e tamanho (ex.: Times New Roman 12pt); fonte diferente em títulos?
- **Página:** margens (esq./dir./sup./inf.), tamanho do papel.
- **Espaçamento:** entrelinha (1,0 / 1,5 / duplo); espaço antes/depois do parágrafo; recuo de primeira linha.
- **Alinhamento:** corpo (justificado?), endereçamento, títulos, assinatura.
- **Endereçamento e "CONTESTAÇÃO":** centralizados? negrito? caixa alta?
- **Títulos de seção:** caixa alta? negrito? numeração? centralizados ou à esquerda?
- **Ênfase no corpo:** o que recebe negrito/itálico/sublinhado (dispositivos, teses, nomes).
- **Pedidos:** alíneas/bullets, recuo, marcador usado.
- **Bloco de assinatura:** centralizado ou à esquerda; linhas (nome, cargo, matrícula); local e data acima.

Registrar no `guia-de-estilo.md` (seção "0. Formatação") e **reproduzir na redação**: a minuta entregue em `.docx` deve nascer com essas escolhas, não com o padrão do editor.

## Camada 1 — Estrutura (a arquitetura da peça)

Investigar e responder com regras:

- Ordem das seções e nome que o autor dá a cada uma (ex.: "DOS FATOS" vs "I – SÍNTESE FÁTICA").
- Como a peça **abre**: endereçamento, qualificação, primeiro parágrafo típico.
- Como a peça **fecha**: existe frase-síntese antes dos pedidos? Como são formulados os pedidos (lista numerada, alíneas, texto corrido)?
- Títulos e subtítulos: numeração (romana, arábica, nenhuma), caixa alta ou não, negrito ou não.
- Uso de tópicos/listas vs texto corrido: quando o autor usa cada um.
- Extensão típica de cada seção em relação ao todo.

## Camada 2 — Argumentação (como o autor convence)

- Direção do raciocínio: parte do fato para o direito ou do direito para o fato?
- Como constrói cada tópico de mérito: enuncia a tese primeiro? Narra, fundamenta e conclui? Usa silogismo explícito?
- **Jurisprudência:** transcreve ementa inteira, transcreve trecho, ou parafraseia e cita no corpo? Onde entram tribunal, número e data? Usa destaque (negrito/itálico) no trecho citado?
- **Doutrina:** cita quanto e quando? Autor específico ou evita manual genérico?
- **Legislação:** transcreve o artigo ou só referencia? Como formata a transcrição?
- Como trata o argumento contrário: ignora, refuta de passagem ou dedica seção?
- Recursos retóricos recorrentes: pergunta retórica, gradação, analogia, ironia contida?

## Camada 3 — Frase (a impressão digital)

- Tamanho médio e variação dos períodos; parágrafos de quantas linhas.
- **Conectivos favoritos** (com frequência real no corpus) e conectivos que nunca aparecem.
- Pronomes de tratamento e fórmulas de referência ao juízo, às partes, ao processo.
- Latinismos: usa? Quais? Com que parcimônia? Itálico ou não?
- Ênfase tipográfica: o que vai para negrito, itálico, sublinhado, caixa alta — e o que nunca vai.
- Pontuação característica: usa travessão? dois-pontos? ponto e vírgula? parênteses explicativos?
- Vocabulário-assinatura: palavras/expressões que se repetem entre peças e são escolha do autor (não jargão obrigatório).
- Primeira pessoa: singular, plural ("requer-se" vs "o réu requer"), voz ativa vs passiva.

## Prompt-base (adaptar)

> Analise as peças anexas como um perito em estilometria. Produza uma descrição do estilo do autor em quatro camadas — formatação/layout, estrutura, argumentação e frase — composta EXCLUSIVAMENTE de regras verificáveis. Para a formatação, inspecione o próprio arquivo `.docx` (fonte, tamanho, margens, entrelinha, alinhamento, negrito de títulos), não só o texto. Cada regra deve: (a) ser objetivamente checável em um texto/arquivo novo; (b) vir com um exemplo literal extraído das peças, indicando de qual peça saiu. Proibido usar adjetivos genéricos como "formal", "objetivo", "claro" ou "técnico" sem a regra concreta que os materializa. Ao final, liste também o que o autor NUNCA faz (padrões ausentes no corpus que seriam comuns em outros advogados).

A seção final ("o que o autor nunca faz") alimenta o `anti-estilo.md`.

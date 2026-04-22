# Dashboard de Pagamentos

Portal consultável pelos diretores + ferramenta interna de atualização diária.

## Arquivos

| Arquivo | O que é | Quem acessa |
|---|---|---|
| `index.html` | Dashboard público com KPIs, tabelas e prévia | Diretores (via URL) |
| `atualizar.html` | Ferramenta de drag-and-drop que processa as planilhas | Só você |
| `data.json` | Dados processados que o dashboard consome | Gerado pela ferramenta |

## Setup inicial (uma vez só)

1. Crie um repositório no GitHub (pode ser privado se o plano permitir GitHub Pages privado).
2. Suba os 3 arquivos (`index.html`, `atualizar.html`, `data.json`) na raiz.
3. Em **Settings → Pages**, selecione a branch (`main`) e pasta (`/ (root)`). Salve.
4. Aguarde ~1 minuto. A URL será `https://SEUUSUARIO.github.io/NOMEDOREPO/`.
5. Compartilhe a URL com os diretores. Salve também `…/atualizar.html` nos favoritos seus.

## Rotina diária

1. Abra `atualizar.html` no seu navegador.
2. Arraste os 4 arquivos (3 Consultas `.xlsx` + `scfldan0.csv`). Ordem e nome não importam.
3. Clique em **Baixar data.json**.
4. No GitHub: abra o repositório, clique em `data.json`, clique no ícone de lápis, arraste o arquivo baixado por cima. Commit.
5. Em ~1 minuto o dashboard está atualizado para todos.

## Paleta

- `#3C003C` — Magenta escuro (base, headers)
- `#FF6E00` — Laranja (acentos, CTAs, KPI em destaque)

## Detecção automática dos arquivos

A ferramenta identifica cada arquivo pelo **conteúdo**, não pelo nome:

- CSV começando com `SE2;…` → pagamentos realizados (Protheus)
- XLSX com coluna `TIPO DE DESPESA` → reembolsos
- XLSX com coluna `VALOR TOTAL SERVIÇO` → NFs de serviço (motoristas)
- XLSX com `N. TITULO` + `HISTÓRICO` (sem `TIPO DE DESPESA`) → NFs de título (boletos)

Se um arquivo não for reconhecido, aparece com selo vermelho — geralmente é sinal de que o ERP mudou o layout; avise o responsável para ajustarmos o parser.

## Privacidade

Todo o processamento acontece **no seu navegador**. As planilhas nunca saem da sua máquina.
Só o `data.json` gerado (agregados + linhas normalizadas) vai para o GitHub.

Se o repositório for público, considere colocar uma camada simples de senha em JS no `index.html` ou migrar para um repo privado com GitHub Pages privado.

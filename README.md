# Portfólio — Evandro Costa

Landing page estática de portfólio de automação e dados. HTML + CSS puros, sem
build, sem dependências de runtime. As fontes vêm do Google Fonts via CDN.

```
index.html          página inteira
css/tokens.css      design tokens (cores, tipografia, espaço, motion)
css/site.css        estilos da página — importa tokens.css
assets/og.png       imagem de preview (1200×630) para link em redes sociais
assets/favicon.svg  ícone
.nojekyll           impede o Jekyll do Pages de ignorar arquivos
PORTFOLIO_BRIEF.md  brief de conteúdo e direção visual (fonte de verdade)
```

## Rodar localmente

Abrir `index.html` no navegador já funciona. Para servir por HTTP (recomendado,
evita diferenças de caminho relativo):

```bash
python -m http.server 8000
```

Depois acesse `http://localhost:8000`.

## Publicar no GitHub Pages

1. Suba o repositório para `github.com/ealost/<nome-do-repo>`.
2. **Settings → Pages → Build and deployment**: source `Deploy from a branch`,
   branch `main`, pasta `/ (root)`.
3. O site sai em `https://ealost.github.io/<nome-do-repo>/`.

Nenhum workflow do Actions é necessário — não há etapa de build.

### Se o nome do repositório mudar

Os `<meta>` de OpenGraph usam URL absoluta (crawlers exigem). Atualize as quatro
ocorrências em `index.html` para o domínio final:

- `link rel="canonical"`
- `og:url`
- `og:image`
- `twitter:image`

Todos os outros caminhos (`css/`, `assets/`) são relativos e funcionam tanto em
project site (`/repo/`) quanto em user site (`ealost.github.io`).

## Editar conteúdo

Os projetos são blocos `<article class="tile">` dentro de `.bento`. O tamanho vem
da classe:

| Classe                  | Largura na grade de 6 colunas |
| ----------------------- | ----------------------------- |
| `tile tile--lead`       | metade (3 col), destaque       |
| `tile tile--wide`       | metade (3 col)                 |
| `tile`                  | um terço (2 col)               |

Em telas abaixo de 60rem tudo colapsa para 2 colunas e cada tile ocupa a linha
inteira.

Cores e tipografia estão todas em `css/tokens.css` — nenhum valor de cor está
escrito direto no `site.css`.

## Anonimização

O conteúdo é público e não cita nomes de empresas, sistemas proprietários,
tabelas, CNPJs, placas, e-mails internos, endpoints ou IDs. Ao editar, manter a
descrição por função ("o ERP", "o data warehouse", "a API do banco").

## Números

Os três números do card de editais (~5 min, 60–150 páginas, ~R$ 3) vieram do
brief. Nenhuma outra métrica foi inventada — se quiser adicionar mais, use dados
reais medidos.

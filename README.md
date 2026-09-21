# CalhaPro: página de manutenção

Página estática exibida em [www.calhapro.com.br](https://www.calhapro.com.br) enquanto a plataforma está em manutenção. É um único arquivo HTML, sem build e sem dependências, hospedado no GitHub Pages.

O brasão do CalhaPro aparece no cabeçalho e no favicon, em SVG embutido no próprio HTML (nítido em qualquer tamanho e sem requisição extra).

Ao carregar, uma animação mostra uma chapa plana sendo medida, dobrada até virar o perfil de uma calha e testada com água. A página segue a paleta do CalhaPro, tem modo escuro automático, é responsiva e respeita a preferência de "reduzir movimento" do sistema.

## Estrutura

| Arquivo      | Função                                                                                   |
| ------------ | ---------------------------------------------------------------------------------------- |
| `index.html` | A página de manutenção (HTML, CSS e JavaScript em um só arquivo).                        |
| `404.html`   | Cópia idêntica do `index.html`. Faz qualquer rota (`/login`, `/precos`…) mostrar o aviso. |
| `CNAME`      | Informa ao GitHub Pages o domínio personalizado (`www.calhapro.com.br`).                 |
| `apple-touch-icon.png` | Ícone do brasão para quando alguém adiciona a página à tela inicial do iPhone.  |

> Sempre que editar o `index.html`, replique a alteração no `404.html`.

## Como configurar

No início do `<script>` do `index.html` (e do `404.html`) existe um bloco de configuração:

```js
var CONFIG = { retorno: null, email: "" };
```

| Campo     | O que faz                                                                                             | Exemplo                        |
| --------- | ----------------------------------------------------------------------------------------------------- | ------------------------------ |
| `retorno` | Data e hora previstas para a volta. Se `null` ou já passada, a página mostra "Em breve" ou "Em instantes". | `"2026-09-21T14:00:00-03:00"`  |
| `email`   | Contato de suporte exibido na legenda. Se vazio, a linha de contato fica oculta.                      | `"contato@calhapro.com.br"`    |

Para ajustar textos ou cores, edite o próprio HTML. As cores ficam nas variáveis CSS do `:root`.

## Testar localmente

Abra o `index.html` no navegador, ou sirva a pasta:

```bash
python3 -m http.server 8000
# acesse http://localhost:8000
```

## Publicar no GitHub Pages

1. Crie um repositório e envie os arquivos para a raiz da branch `main`.
2. Vá em **Settings → Pages**.
3. Em **Build and deployment**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`.
4. Em **Custom domain**, confirme `www.calhapro.com.br` (o arquivo `CNAME` já cuida disso).
5. Configure o DNS (abaixo) e, quando o certificado for emitido, marque **Enforce HTTPS**.

### DNS

No provedor do domínio (Registro.br, Cloudflare, etc.):

| Tipo    | Nome  | Valor                  |
| ------- | ----- | ---------------------- |
| `CNAME` | `www` | `SEU-USUARIO.github.io` |

Para o domínio sem `www` (`calhapro.com.br`), crie também estes registros `A`:

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

A propagação do DNS pode levar de alguns minutos a algumas horas.

## Voltar ao site normal

1. Restaure no DNS os registros que apontavam para a hospedagem original do CalhaPro.
2. Aguarde a propagação.
3. Opcional: remova o domínio em **Settings → Pages** e apague o arquivo `CNAME`, para o GitHub Pages não reivindicar o domínio.

Enquanto o DNS apontar para o GitHub, o site real fica fora do ar. Se o TTL dos registros for alto, reduza-o antes de iniciar a manutenção para que a volta seja mais rápida.

## Observações

- **SEO:** o GitHub Pages não consegue responder com o código HTTP 503, que é o padrão para manutenção. Por isso a página usa `<meta name="robots" content="noindex, nofollow">`, para evitar que o Google indexe o aviso como se fosse o site. Ao encerrar a manutenção essa página sai do ar junto com a tag, então nada precisa ser revertido no site real.
- **Fontes:** Plus Jakarta Sans, Inter e JetBrains Mono são carregadas do Google Fonts. Sem conexão com o Google, a página usa as fontes do sistema e continua funcionando.
- **Sem cookies, sem rastreamento e sem requisições a APIs.**

## Licença

Uso interno do projeto CalhaPro.

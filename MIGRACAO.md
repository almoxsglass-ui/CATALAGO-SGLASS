# Migração do catálogo SGLASS

## Recuperado para esta cópia

- Aplicação React/Vite com backend Convex, PWA, catálogo, orçamento, administração e vistas explodidas.
- 231 produtos exportados da planilha local para `data/products.csv`; a planilha original também fica em `data/Catálogo SGlass.xlsx`.
- 179 imagens originais em `public/produtos`. A associação local é pelo código do produto; para itens sem arquivo local, o CSV conserva a URL que veio da planilha.
- As imagens locais das vistas explodidas e os ícones da marca permanecem em `public/diagramas` e `public/icons`.
- O esquema Convex agora declara as tabelas de produtos e categorias usadas pelas queries e mutations copiadas.
- Login foi desacoplado do SDK Hercules e usa OIDC genérico, com ponte para autenticação Convex.

## Publicação preparada

- Cloudflare Pages: `wrangler.toml` aponta para `dist` e `public/_redirects` encaminha rotas SPA para `index.html`.
- A configuração de exemplo está em `.env.example`. Não colocar segredos neste arquivo; variáveis locais reais ficam em `.env.local`, ignorado pelo Git.

## Itens que dependem da conta do proprietário

1. Criar ou selecionar um deployment Convex independente e usar sua URL em `VITE_CONVEX_URL`.
2. Escolher um provedor OIDC e configurar os redirects para o domínio Cloudflare e para o endereço local de desenvolvimento. Configurar `VITE_OIDC_AUTHORITY` e `VITE_OIDC_CLIENT_ID` no build e os valores correspondentes `OIDC_ISSUER_URL` e `OIDC_APPLICATION_ID` no Convex. O emissor deve corresponder ao claim `iss` e o application ID ao claim `aud` do token.
3. Publicar o código no Cloudflare Pages depois que o backend e o login estiverem configurados.
4. Entrar na área administrativa e importar `data/products.csv`; o importador divide as 231 linhas em lotes.
5. Recuperar do backup do banco os dados de configuração, usuários e registros das vistas explodidas. Os PNGs preservados não incluem os pontos interativos/hotspots que ficam armazenados nos registros Convex.

Nenhuma configuração de conta, chave privada ou valor de ambiente foi copiado para esta pasta. A publicação externa ainda não foi feita.

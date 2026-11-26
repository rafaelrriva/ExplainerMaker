# Estúdio de Explainers

Gerador de prompts para animações em canvas (**Explainer** e **Vinheta**), com 13 estilos, prévia ao vivo e identidades de marca (TribeMD, TribeMD Academy, Oncologia Brasil, Bipp, Hemomeeting e Genérico).

É uma página estática, sem build e sem dependências.

## Usar localmente
Abra o `index.html` no navegador. Se os logos não carregarem, sirva a pasta com:

```bash
python3 -m http.server 8000
```

e acesse http://localhost:8000.

## Publicar no GitHub Pages
1. Crie um repositório e envie estes arquivos para a branch `main`.
2. Vá em **Settings → Pages → Build and deployment**, escolha **Deploy from a branch**, depois `main` e `/ (root)`.
3. O site vai ficar em `https://<usuario>.github.io/<repositorio>/`.

## Estrutura
- `index.html`: o estúdio inteiro (estilos, prévia, formulário e geração do prompt).
- `logos/`: logos usados nos cartões de identidade.

As preferências ficam salvas no `localStorage` do navegador.

> Os logos são marcas registradas dos seus donos. Se o repositório for público, confirme se pode publicá-los.

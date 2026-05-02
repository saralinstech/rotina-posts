# rotina-posts — Suapage

Repositório central de conteúdo da Suapage. Fonte da verdade para calendários, criativos e identidade visual, acessível de qualquer máquina pelo navegador.

---

## Estrutura de pastas

```
rotina-posts/
│
├── identidade-visual/
│   ├── perfil-marca.md          ← cole aqui antes de gerar qualquer coisa
│   └── assets/
│       └── (logos, cores, fontes em imagem)
│
├── calendario/
│   └── 2025/
│       └── junho-2025.xlsx      ← gerado pela skill content-calendar
│
├── criativos/
│   └── 2025/
│       └── junho/
│           └── semana-1/
│               ├── slide_01.png
│               └── slide_02.png
│
├── skills/
│   ├── content-calendar.md
│   └── instagram-carousel.md
│
└── README.md
```

---

## Como usar de qualquer máquina

### Gerar o calendário do mês

1. Abra o GitHub, vá em `identidade-visual/perfil-marca.md` e clique em **Raw**
2. Copie o conteúdo completo
3. Abra o Claude.ai e cole com o comando: `gerar calendário do próximo mês com esse perfil de marca`
4. Baixe o `.xlsx` gerado
5. No GitHub, navegue até `calendario/2025/` e clique em **Add file > Upload files**
6. Faça upload do `.xlsx` e confirme

### Criar os criativos da semana

1. No GitHub, abra o `.xlsx` do mês e clique em **Download**
2. Abra o Claude.ai e envie o arquivo com o comando: `criar carrossel da semana X com base nesse calendário`
3. Aprove o mockup visual
4. Baixe os PNGs exportados
5. No GitHub, navegue até `criativos/2025/mes/semana-X/` e faça upload dos PNGs

---

## Convenção de nomes

| Tipo | Formato | Exemplo |
|---|---|---|
| Calendário | `mes-ano.xlsx` | `junho-2025.xlsx` |
| Pasta de criativos | `semana-N` | `semana-1` |
| Slides exportados | `slide_NN.png` | `slide_01.png` |

---

## Skills utilizadas

- `content-calendar` — gera o calendário mensal em `.xlsx`
- `instagram-carousel` — gera mockup interativo e exporta os PNGs por slide
- `suapage-identidade-visual` — aplica a identidade visual da Suapage em todos os criativos

Todas rodam no Claude.ai pelo navegador, sem instalação.

# Foco Total! 🧠✨

Jogo de foco e reflexo para crianças de 6 a 12 anos, pensado para exercitar habilidades geralmente afetadas no TDAH:

- **Atenção seletiva** — tocar só nas bolhas que combinam com a regra
- **Controle de impulso** — resistir a tocar nas bolhas erradas (tarefa estilo *go/no-go*)
- **Flexibilidade cognitiva** — a regra muda a cada nível (cor → emoji → "evite as bombas")
- **Atenção sustentada** — níveis curtos com recompensas frequentes (estrelas, sequências, sons)

> ⚠️ O jogo é um exercício divertido, não um tratamento. Não substitui acompanhamento médico/psicológico.

## Testar rápido (sem compilar)

Abra `www/index.html` em qualquer navegador do celular ou PC. Funciona offline.

## Compartilhar com iPhone (e Android) — link na web 🔗

O jogo é um **PWA**: hospede a pasta `www/` e compartilhe o link. No iPhone, a pessoa abre no Safari e toca em **Compartilhar > Adicionar à Tela de Início** — vira um app com ícone, tela cheia e funciona offline. Não precisa de App Store.

Hospedagem grátis (escolha uma):

**Netlify Drop (mais fácil, sem conta de programador)**
1. Acesse [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arraste a pasta `www` para a página
3. Pronto — copie o link gerado (ex: `https://foco-total.netlify.app`) e compartilhe

**GitHub Pages**
1. Crie um repositório e envie o conteúdo da pasta `www` para a raiz
2. Em Settings > Pages, ative o GitHub Pages na branch principal
3. Compartilhe o link `https://seuusuario.github.io/seurepositorio`

Instruções para mandar junto com o link:
- **iPhone**: abrir no Safari → botão Compartilhar → "Adicionar à Tela de Início"
- **Android**: abrir no Chrome → menu ⋮ → "Adicionar à tela inicial"

## App nativo iOS (opcional, avançado)

Requer um **Mac com Xcode** e, para distribuir a outras pessoas, conta Apple Developer (US$ 99/ano):

```bash
npm install
npx cap add ios
npx cap open ios
```

Para a maioria dos casos, o link PWA acima resolve sem custo.

## Gerar o APK sem instalar nada (GitHub Actions) ☁️

O projeto já inclui um robô de build (`.github/workflows/build-apk.yml`). Passos:

1. Crie uma conta grátis no [github.com](https://github.com) e um repositório novo (ex: `foco-total`)
2. Envie TODOS os arquivos do projeto para o repositório (pode arrastar pelo site: **Add file > Upload files** — inclua a pasta `.github`)
3. Vá na aba **Actions** do repositório e aguarde o build "Gerar APK Android" terminar (~5 min)
4. Clique no build concluído e baixe o arquivo **foco-total-apk** (seção *Artifacts*)
5. Dentro do zip baixado está o `app-debug.apk` — mande para seus amigos pelo WhatsApp/Drive
6. No celular: tocar no APK e instalar (ative "instalar de fontes desconhecidas" se pedir)

## Gerar o APK no seu PC (alternativa)

Pré-requisitos: [Node.js](https://nodejs.org) (18+) e [Android Studio](https://developer.android.com/studio).

```bash
cd foco-total
npm install
npx cap add android
npx cap sync android
npx cap open android
```

No Android Studio:

1. Aguarde a sincronização do Gradle terminar.
2. **Build > Build Bundle(s)/APK(s) > Build APK(s)**.
3. O APK fica em `android/app/build/outputs/apk/debug/app-debug.apk`.
4. Copie para o celular e instale (ative "instalar apps de fontes desconhecidas").

Para testar direto num celular conectado via USB (com depuração USB ativa):

```bash
npx cap run android
```

## Estrutura

```
foco-total/
├── www/
│   ├── index.html        # o jogo inteiro (HTML + CSS + JS, sem dependências)
│   ├── manifest.json     # config do PWA
│   ├── sw.js             # cache offline
│   └── icon-*.png        # ícones do app
├── capacitor.config.json # config do app (id: com.cleytondev.focototal)
├── package.json
└── README.md
```

## Personalizar

Tudo fica em `www/index.html`:

- `GOOD_EMOJIS` / `BAD_EMOJIS` — itens das bolhas
- `COLORS` — cores das bolhas
- `speed()` e `spawnEvery()` — dificuldade
- `goal` em `beginLevel()` — acertos necessários por nível

Depois de editar, rode `npx cap sync android` (ou `ios`) e gere o app de novo.

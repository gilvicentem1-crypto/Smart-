# AgroSmart Connect — versão Web / PWA

Aplicação autónoma em HTML/CSS/JS puro (sem passos de build), instalável como PWA
e pronta para embrulhar num APK Android. Layout em azul padrão UNESCO, com 4 idiomas
(PT/EN/FR/ES) e os 5 módulos da proposta.

## Ficheiros

- `index.html` — a aplicação completa (interface + lógica)
- `manifest.json` — torna a app instalável ("Adicionar ao ecrã principal")
- `sw.js` — service worker, cria cache offline do essencial da app
- `icon-192.svg`, `icon-512.svg` — ícones da app

## O que é real vs. simulado

- **Mercado, Formação, Alertas, Dados**: dados de exemplo (mock), fáceis de ligar
  a uma API real mais tarde — basta substituir os arrays em `T[lang]` por chamadas `fetch`.
- **Assistente**: funciona 100% offline com respostas baseadas em palavras-chave
  (sem custos, sem servidor). Se quiser respostas geradas por IA real (como na
  demonstração dentro do Claude), é necessário um pequeno backend que guarde a
  chave de API em segurança — nunca coloque uma chave de API da Anthropic
  diretamente neste HTML, pois ficaria visível a qualquer visitante do site.

## 1. Publicar como site (GitHub Pages)

1. Crie um repositório novo no GitHub (ex: `agrosmart-connect`)
2. Carregue os 5 ficheiros desta pasta para a raiz do repositório
3. Em **Settings → Pages**, escolha a branch `main` e a pasta `/root`
4. Guarde — o site fica disponível em `https://SEU-UTILIZADOR.github.io/agrosmart-connect/`

No telemóvel, ao abrir esse link no Chrome, aparece a opção **"Adicionar ao ecrã
principal"** — a partir daí a app abre em ecrã inteiro, como uma app nativa.

## 2. Converter em APK Android (sem programar)

Depois de publicado (passo 1), use o **PWABuilder**, ferramenta gratuita da Microsoft:

1. Aceda a **https://www.pwabuilder.com**
2. Cole o link do seu site publicado (ex: `https://SEU-UTILIZADOR.github.io/agrosmart-connect/`)
3. Clique em **Start** — a ferramenta analisa o `manifest.json` e o `sw.js` automaticamente
4. Escolha **Android** → **Generate Package**
5. Descarrega um `.apk` (para testar/instalar diretamente) ou `.aab` (para publicar na Google Play)

Isto gera uma **TWA (Trusted Web Activity)** — um APK real que embrulha o site,
sem necessidade de reescrever nada em Java/Kotlin.

## 3. Alternativa: Capacitor (mais controlo, requer Android Studio)

Se mais tarde quiser acesso a funcionalidades nativas (câmara, notificações push, etc.):

```bash
npm install @capacitor/core @capacitor/cli
npx cap init "AgroSmart Connect" "com.agrosmart.connect"
npx cap add android
npx cap copy
npx cap open android   # abre no Android Studio para compilar o APK
```

Isto requer Android Studio instalado no seu computador — não é algo que se
consiga fazer só a partir do telemóvel.

# Tostão — gestor financeiro de bolso com IA

App para Android que roda 100% no celular (dados salvos só nele).

## O que ele faz
- **Lançar por voz ou texto:** "gastei 45 no mercado hoje", "paguei 30 de Uber dia 15", "recebi 1200 de salário", "gastei 30 no uber e 50 no mercado ontem". Interpreta no próprio celular, grátis, e você confere antes de salvar.
- **Dívidas:** cadastre cada credor, marque se está negativada, registre pagamentos e peça um plano à IA.
- **Metas:** ex. "Enxoval do Theo", com cálculo de quanto guardar por mês até o prazo.
- **Categorias:** Mercado, Alimentação fora, Transporte, Moradia, Contas, Dívidas, Theo, IA e assinaturas, Saúde, Lazer.
- **Assistente (DeepSeek):** responde com base no seu resumo do mês.

## Custo zero: duas formas de usar a IA
1. **Sem chave (grátis):** toque numa pergunta no Assistente. O app copia seu resumo + a pergunta; cole no app do DeepSeek que você já tem.
2. **Com chave da API:** em Configurações cole a chave do DeepSeek. A API é separada do app/chat e funciona com crédito pré-pago (consulte o preço atual em platform.deepseek.com). O app só envia um resumo, não todos os lançamentos, para gastar pouco.

O parser de voz/texto não usa IA por padrão, então lançar gastos não custa nada.

## Gerar o APK sem instalar nada (GitHub Actions, grátis)
1. Crie um repositório no GitHub (pode ser privado) e envie esta pasta inteira (inclusive `.github`).
2. No repositório: aba **Actions** → **Gerar APK** → **Run workflow**.
3. Quando terminar (uns 5 min), abra a execução e baixe o artefato **tostao-apk** (um zip com `app-debug.apk`).
4. Mande o APK para o celular, abra e permita "instalar de fontes desconhecidas".

## Gerar o APK no seu PC (Windows) com Android Studio
```
npm install
npx cap add android
npx cap sync android
npx cap open android
```
No Android Studio: **Build → Build APK(s)**.
Antes de compilar, em `android/app/src/main/AndroidManifest.xml` adicione dentro de `<manifest>`:
```xml
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<queries>
  <intent><action android:name="android.speech.RecognitionService" /></intent>
</queries>
```

## Testar no navegador do PC
Abra `www/index.html` no Chrome. A voz funciona no Chrome; a chamada ao DeepSeek pode ser bloqueada por CORS no navegador, mas funciona no APK (o Capacitor faz a requisição nativa).

## Observações
- O app guarda os dados no armazenamento do próprio app. Use **Configurações → Copiar backup** de vez em quando.
- A voz no APK abre a janela de reconhecimento do Google (precisa de internet e do app Google instalado).
- Regras de negociação de dívida mudam; a IA avisa para confirmar nos canais oficiais.

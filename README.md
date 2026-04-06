# 🤖 WaBot Pro — Automação WhatsApp Business

## O que é
Aplicativo Android que envia mensagens automaticamente para múltiplos grupos do WhatsApp Business usando o Serviço de Acessibilidade do Android.

---

## 📁 Estrutura do Projeto

```
WhatsAppBot/
├── app/
│   ├── build.gradle
│   └── src/main/
│       ├── AndroidManifest.xml
│       ├── java/com/wabotpro/
│       │   ├── MainActivity.java          ← Tela principal
│       │   ├── WaBotAccessibilityService.java  ← Motor da automação
│       │   ├── BotService.java            ← Serviço de comunicação
│       │   └── GrupoAdapter.java          ← Lista de grupos
│       └── res/
│           ├── layout/
│           │   ├── activity_main.xml
│           │   └── item_grupo.xml
│           ├── values/
│           │   ├── strings.xml
│           │   └── styles.xml
│           └── xml/
│               └── accessibility_service_config.xml
├── build.gradle
└── settings.gradle
```

---

## 🔨 Como Compilar (Android Studio)

### Pré-requisitos
- Android Studio Hedgehog ou mais recente
- JDK 17+
- Android SDK 34

### Passos
1. Abra o Android Studio
2. **File → Open** → selecione a pasta `WhatsAppBot/`
3. Aguarde o Gradle sincronizar
4. Conecte seu celular com **Modo Desenvolvedor** ativado
5. Clique em **▶ Run** (ou `Shift+F10`)

### Gerar APK para distribuição
1. **Build → Generate Signed Bundle/APK**
2. Selecione **APK**
3. Crie ou selecione um keystore
4. Escolha **release**
5. O APK estará em `app/release/app-release.apk`

---

## 📱 Como Usar o App

### 1. Instalar e Ativar Acessibilidade
Ao abrir o app pela primeira vez, ele pedirá para ativar o Serviço de Acessibilidade:
- Vá em **Configurações → Acessibilidade → WaBot Pro**
- Ative o serviço
- Volte ao app

### 2. Adicionar Grupos
- Toque em **➕ Adicionar Grupo**
- Digite o nome **exato** do grupo como aparece no WhatsApp Business
- Repita para todos os grupos desejados
- Os grupos são salvos automaticamente

### 3. Digitar a Mensagem
- Digite (ou cole) sua mensagem no campo de texto
- Suporta texto, links e emojis

### 4. Iniciar Envio
- Toque em **🚀 INICIAR ENVIO**
- O WhatsApp Business abrirá automaticamente
- **Não mexa no celular** durante o processo
- O bot irá:
  1. Buscar o grupo pelo nome
  2. Abrir o grupo
  3. Colar a mensagem
  4. Aguardar 5 segundos
  5. Enviar
  6. Repetir para o próximo grupo
- Ao final aparece: **"✅ FINALIZADO!"**

---

## ⚙️ Como Funciona

```
[App] → salva grupos + mensagem
     → abre WhatsApp Business
     → [AccessibilityService] monitora a tela
        → busca grupo por nome
        → clica no grupo
        → localiza campo de mensagem
        → cola o texto
        → aguarda 5 segundos
        → clica em Enviar
        → volta e repete para próximo grupo
        → ao terminar: exibe "FINALIZADO"
```

---

## ⚠️ Notas Importantes

- **WhatsApp Business** deve estar instalado (`com.whatsapp.w4b`)
- O app também funciona com WhatsApp comum (`com.whatsapp`)
- Os nomes dos grupos devem ser **exatos** (maiúsculas/minúsculas importam)
- **Não use o celular** durante o envio
- Mantenha a tela ligada
- Intervalo de 5 segundos entre envios é configurado no código (`WaBotAccessibilityService.java`)

---

## 🔧 Personalizar o Intervalo de Espera

Em `WaBotAccessibilityService.java`, linha com `5000`:
```java
// Aguarda 5 segundos antes de enviar
handler.postDelayed(() -> enviarMensagem(getRootInActiveWindow()), 5000);
```
Mude `5000` para o tempo desejado em milissegundos (ex: `3000` = 3 segundos).

---

## 📋 Requisitos
- Android 7.0+ (API 24)
- WhatsApp Business instalado
- Serviço de Acessibilidade ativado

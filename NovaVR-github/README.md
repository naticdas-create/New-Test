# NovaVR (Android) — navegador flutuante com câmera, mãos e YouTube

## Montar o projeto (5 minutos)
1. Android Studio → New Project → **Empty Views Activity**. Nome `NovaVR`, pacote `com.novavr`, Kotlin, Min SDK 26.
2. Copie `app/src/main/java/com/novavr/*.kt` para o mesmo caminho do seu projeto (apague o MainActivity.kt padrão).
3. Substitua o `AndroidManifest.xml` pelo deste pacote (mantenha o `@style/Theme...` se o seu tema padrão tiver outro nome).
4. Abra o projeto no Android Studio e aguarde a sincronização do Gradle (as dependências já estão em `app/build.gradle.kts`).
5. Baixe o modelo de mãos e coloque em `app/src/main/assets/hand_landmarker.task`:
   https://storage.googleapis.com/mediapipe-models/hand_landmarker/hand_landmarker/float16/1/hand_landmarker.task
6. Rode em um celular real (não funciona em emulador).

## Como usar
- Coloque o celular no VR Box na horizontal. O fundo é a câmera traseira.
- **Mão:** aponte com o polegar e o indicador (o ponto branco). **Junte os dedos (pinça)** para clicar. Pinça e arrastar rola a página.
- **Olhar:** sem mão visível, fixe o ponto em um botão por 1,2 s.
- Barra: ← voltar, ▶ YouTube, ABC teclado, ⌖ recentrar, ✕ sair.
- No teclado, "Ir" abre o endereço, ou pesquisa no YouTube se for texto comum.

## Rastreamento sem ARCore
- O projeto usa CameraX + MediaPipe para a imagem e as mãos, e o giroscópio para orientação da cabeça.
- O deslocamento translacional é aproximado por passos detectados no acelerômetro. A estimativa visual de expansão/recuo da imagem serve apenas como indicação de sentido; não fornece posição 6DoF métrica confiável.
- Portanto, as janelas ficam fixas no mundo virtual enquanto o usuário usa os passos virtuais/botões. Isso não equivale ao rastreamento espacial do Meta Quest 3.
- A mão desenhada nesta versão é uma sobreposição 2D estimada pelos 21 landmarks. Ainda não é uma malha 3D com oclusão física real da mão sobre cada janela.
- É obrigatório adicionar `app/src/main/assets/hand_landmarker.task` conforme a etapa 5 acima; esse modelo não vem incluído no ZIP.
- **Roblox:** o app do celular não transforma o Roblox em um runtime VR nativo. Espelhamento da tela e controles externos ficam para uma etapa separada.

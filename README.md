# 📱 Softwell App: Bem-estar no Trabalho

![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)
![Android](https://img.shields.io/badge/Android-34A853?style=for-the-badge&logo=android&logoColor=white)
![Jetpack Compose](https://img.shields.io/badge/Jetpack%20Compose-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white)
![Material 3](https://img.shields.io/badge/Material%203-757575?style=for-the-badge&logo=materialdesign&logoColor=white)
![Retrofit](https://img.shields.io/badge/Retrofit-000000?style=for-the-badge&logo=square&logoColor=white)
![Room](https://img.shields.io/badge/Room-4285F4?style=for-the-badge&logo=sqlite&logoColor=white)

> Aplicativo Android nativo da plataforma Softwell, desenvolvido para monitorar o bem-estar e mapear riscos psicossociais de colaboradores. Por meio do app, o colaborador registra seu estado emocional diário, responde a avaliações psicossociais e participa de votações de ações corporativas. O administrador conta com uma área restrita para acompanhamento dos indicadores da equipe.

📅 **Projeto desenvolvido em equipe para o Challenge FIAP (2025).**  
🖥️ **API Backend (Java / Spring Boot) que alimenta este app:** [Softwell-Challenge/backend-softwell](https://github.com/Geovani237/backend-softwell)

---

## 📸 Capturas de Tela

<!-- Substitua as URLs das imagens ou desmantenha o comentário ao adicionar os prints no repositório -->
<!--
<p align="center">
  <img src="docs/login.png" width="200" alt="Tela de Login"/>
  <img src="docs/dashboard.png" width="200" alt="Dashboard Colaborador"/>
  <img src="docs/questionario.png" width="200" alt="Questionário Psicossocial"/>
  <img src="docs/admin.png" width="200" alt="Painel Admin"/>
</p>
-->

---

## ✨ Funcionalidades

### 👤 Colaborador
- **Autenticação:** Cadastro e login com injeção automática do Bearer Token JWT em todas as requisições HTTP.
- **Registro do Humor:** Pop-up intuitivo com seleção por emojis para registro do estado emocional diário.
- **Questionário Psicossocial:** Avaliação dividida em 5 temas, com componentes dinâmicos (listas, sliders e escalas numéricas).
- **Histórico de Humor:** Visualização de registros anteriores com suporte a filtro por data (`DatePicker`).
- **Área de Apoio:** Dicas de bem-estar e conteúdo educativo distribuídos em cards expansíveis.
- **Votação de Atividades:** Votação mensal em ações de bem-estar propostas pela organização.
- **Customização de Tema:** Suporte nativo à alternância entre tema claro e escuro (*Light/Dark Mode*).

### 🛠️ Administrador
- **Área Restrita:** Controle de acesso dinâmico validando a *role* do perfil contida na estrutura do JWT.
- **Gestão de Parâmetros:** Cadastro e controle das opções de humor (limite de até 9) e atividades para votação.
- **Métricas & Indicadores:** Painel com cálculo de médias por tema psicossocial.
- **Relatório de Engajamento:** Consolidação dos votos registrados nas ações corporativas.

---

## 🛠️ Tecnologias Utilizadas

| Categoria | Tecnologias |
| :--- | :--- |
| **Linguagem Base** | Kotlin |
| **Interface / UI** | Jetpack Compose, Material 3, Material Icons Extended |
| **Navegação** | Navigation Compose |
| **Arquitetura** | MVVM (ViewModel + ViewModelFactory) |
| **Rede & API** | Retrofit 2, Gson / Moshi, OkHttp Auth Interceptor |
| **Autenticação & JWT** | JWTDecode (decodificação de tokens no app) |
| **Persistência Local** | Room (SQLite) |
| **Carregamento de Mídia**| Coil (imagem assíncrona) |
| **Build & Tooling** | Gradle (Kotlin DSL), KAPT |

> 📱 **Compatibilidade de Hardware:** Android 14+ (`minSdk 34`, `targetSdk 36`).

---

## 🏗️ Arquitetura do Projeto

O aplicativo adota o padrão **MVVM (Model-View-ViewModel)** com separação de responsabilidades. As telas (*Composables*) cuidam puramente da renderização da interface e repasse de eventos. Os ViewModels orquestram o estado da tela (`StateFlow` / `LiveData`) e coordenam as chamadas à API via Retrofit ou ao banco local via Room.

```text
app/src/main/java/br/com/fiap/softwell/
├── screens/      # Telas (Login, Cadastro, Dashboard, Psicossocial, Histórico, Apoio, Admin)
├── components/   # Componentes reutilizáveis (cards expansíveis, dropdowns, sliders, escalas)
├── viewmodel/    # ViewModels e ViewModelFactories
├── service/      # Retrofit Interfaces, OkHttp Auth Interceptor e gerenciador de Token
├── database/     # Camada Room: DAOs, AppDatabase e Repositórios locais
├── model/        # Data Classes, DTOs e enums do domínio
└── ui/theme/     # Design System: Paleta de cores, tipografia e temas (Light/Dark)
```

> 💡 **Destaque:** Um interceptor customizado do OkHttp captura e anexa o cabeçalho `Authorization: Bearer <token>` de forma transparente para todas as chamadas REST.

---

## 🚀 Como Executar o Projeto

### 📋 Pré-requisitos
- **Android Studio** (versão recente - Ladybug ou superior recomendada).
- **Emulador Android** ou **Dispositivo Físico** rodando Android 14+ (`API level 34`).
- Instância ativa da [API Backend Softwell](https://github.com/Geovani237/backend-softwell).

### 🔧 Passo a Passo

1. **Clonar o repositório:**
   ```bash
   git clone [https://github.com/Softwell-Challenge/Softwell.git](https://github.com/Softwell-Challenge/Softwell.git)
   ```

2. **Abrir no Android Studio:**
   Abra a pasta do projeto clonado no Android Studio e aguarde o download das dependências via Gradle.

3. **Configurar o Endereço da API:**
   Ajuste a constante `BASE_URL` no arquivo `service/RetrofitFactory.kt`:

   ```kotlin
   // Emulador do Android Studio comunicando com a API na mesma máquina:
   private const val BASE_URL = "[http://10.0.2.2:8080/](http://10.0.2.2:8080/)"

   // Dispositivo físico via Wi-Fi (substitua pelo IP local da sua máquina):
   // private const val BASE_URL = "[http://192.168.0.10:8080/](http://192.168.0.10:8080/)"
   ```

4. **Executar a Aplicação:**
   Selecione o dispositivo/emulador desejado e clique em **Run (Shift + F10)**.

---

## 👥 Equipe do Projeto

| Integrante | GitHub |
| :--- | :--- |
| **Geovani Carlos de Souza** | [@Geovani237](https://github.com/Geovani237) |
| **Iago Pachiani** | [@IagoPachiani](https://github.com/iagovalverde) |
| **Pedro Marquesini** | [@PedroMarquesini](https://github.com/pedromarquesini) |
| **Bruno Ferreira** | [@BrunoFerreira](https://github.com/Brunoeugenio01) |

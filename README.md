# Afya Pedagógico — Admin Dashboard

Dashboard administrativo fictício desenvolvido em **Blazor WebAssembly Standalone** utilizando a biblioteca de componentes **MudBlazor 9**.

---

## 👤 Identificação
[PREENCHER PELO ALUNO]

---

## 🎯 Objetivo do Projeto
[PREENCHER PELO ALUNO]

---

## 🛠️ Tecnologias Utilizadas
- **Linguagem & Plataforma**: C# / .NET SDK 10 (versão 10.0.401)
- **Framework Web**: Blazor WebAssembly (Standalone / PWA Ready)
- **Biblioteca de Componentes & Design System**: MudBlazor 9.x
- **Tipografia**: Google Fonts (Inter e Roboto)
- **Ícones**: Material Design Icons (via pacote nativo `MudBlazor`)
- **Gráficos**: `MudChart` (Line, Area e Donut com MudBlazor 9 Chart API)

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
- [.NET SDK 10.0+](https://dotnet.microsoft.com/) instalado. Verifique com:
  ```powershell
  dotnet --version
  # Deve retornar 10.0.x (ex.: 10.0.401)
  ```

### Passos para Execução
1. Clone ou acerte o diretório do projeto:
   ```powershell
   cd afya-admin
   ```
2. Restaure as dependências e compile:
   ```powershell
   dotnet build
   ```
3. Execute o servidor de desenvolvimento com Hot Reload:
   ```powershell
   dotnet watch
   ```
   Ou simplesmente:
   ```powershell
   dotnet run
   ```
4. Abra o navegador na URL informada no terminal (geralmente `http://localhost:5147` ou na porta configurada em `Properties/launchSettings.json`).

---

## 📂 Árvore de Pastas e Estrutura do Projeto

```text
afya-admin/
├── .docs/                    # Documentação do projeto, tutoriais e especificações
│   └── tutorial.md           # Roteiro passo a passo e referência técnica
├── docs/                     # Documentação de apoio e capturas de tela
│   └── prints/               # Imagens de evidência dos testes do dashboard
├── Components/               # Componentes visuais modulares e funções auxiliares
│   ├── Ui.cs                 # Funções auxiliares (iniciais de nomes, classes de fundo pastel)
│   ├── CabecalhoPagina.razor # Título, subtítulo e slot de ações da página
│   ├── SeletorPeriodo.razor  # Menu dropdown de períodos com @bind-Valor
│   ├── DashboardCard.razor   # Card estrutural reutilizável com slots de menu e ações
│   ├── KpiCard.razor         # Card de indicador com mini gráfico de sparkline
│   ├── GraficoReceita.razor  # Gráfico de linhas: evolução da Receita x Meta
│   ├── GraficoDistribuicaoClientes.razor # Gráfico de rosca (Donut) com total no centro
│   ├── PerformanceProjetos.razor         # Lista de progresso dos projetos principais
│   ├── AtividadesRecentes.razor          # Feed de atividades recentes da equipe
│   └── ProjetosRecentes.razor            # Tabela de projetos com layout adaptável
├── Data/                     # Camada de modelos e dados da aplicação
│   └── DashboardData.cs      # Records tipados e dados simulados (fake)
├── Layout/                   # Estrutura mestra da aplicação
│   ├── MainLayout.razor      # Layout com AppBar, Drawer responsivo e MudTheme
│   └── NavMenu.razor         # Menu lateral plano separado por divisores
├── Pages/                    # Páginas da aplicação
│   ├── Dashboard.razor       # Página principal que orquestra o layout em MudGrid
│   └── NotFound.razor        # Página padrão de erro 404
├── Properties/               # Configurações de execução
│   └── launchSettings.json   # Perfis de portas e variáveis de ambiente
├── wwwroot/                  # Arquivos estáticos servidos diretamente ao navegador
│   ├── css/app.css           # Estilos base de loading e tratamento de erro
│   ├── img/alex-morgan.jpg   # Foto de perfil utilizada no menu de usuário
│   ├── favicon.png           # Ícone da aba do navegador
│   ├── icon-192.png          # Ícone de aplicação PWA
│   └── index.html            # Host HTML único com inclusão de fontes e scripts
├── _Imports.razor            # Usings globais compartilhados por todos os arquivos Razor
├── afya-admin.csproj         # Arquivo de projeto .NET Blazor WebAssembly
├── App.razor                 # Componente raiz com roteador Blazor
└── Program.cs                # Ponto de entrada, configuração do HttpClient e AddMudServices
```

---

## 🧩 Tabela de Componentes

| Componente | Responsabilidade Principal | Parâmetros / Slots |
| :--- | :--- | :--- |
| `CabecalhoPagina` | Exibe o título principal h4 da página, subtítulo de apoio e área flexível alinhada à direita para botões de ação rápidos. | • `Titulo` (`string`, EditorRequired)<br>• `Subtitulo` (`string?`)<br>• `Acoes` (`RenderFragment?`) |
| `SeletorPeriodo` | Dropdown em formato de botão com ícone de calendário que permite selecionar intervalos temporais com suporte a `@bind-Valor`. | • `Opcoes` (`IReadOnlyList<string>`, EditorRequired)<br>• `Valor` (`string`)<br>• `ValorChanged` (`EventCallback<string>`) |
| `DashboardCard` | Contêiner base padronizado com elevação 1, cabeçalho de título, subtítulo, slot de ações, menu contextual "⋮" e preenchimento vertical flexível. | • `Titulo` (`string`, EditorRequired)<br>• `Subtitulo` (`string?`)<br>• `Acoes` (`RenderFragment?`)<br>• `Menu` (`RenderFragment?`)<br>• `ChildContent` (`RenderFragment?`) |
| `KpiCard` | Card de métrica individual contendo avatar em cor suave com ícone da categoria, valor de destaque, variação percentual com indicador de tendência e gráfico sparkline. | • `Kpi` (`Kpi`, EditorRequired) |
| `GraficoReceita` | Gráfico de linha/área (`MudChart<double>`) comparando a evolução temporal da Receita Realizada versus Meta estabelecida, com escala e legenda. | • `Meses` (`string[]`, EditorRequired)<br>• `Receita` (`double[]`, EditorRequired)<br>• `Meta` (`double[]`, EditorRequired) |
| `GraficoDistribuicaoClientes` | Gráfico de rosca (`Donut`) com legenda customizada com percentuais e total absoluto de clientes desenhado no centro via `<CustomGraphics>` SVG. | • `Total` (`int`, EditorRequired)<br>• `Segmentos` (`IReadOnlyList<SegmentoCliente>`, EditorRequired) |
| `PerformanceProjetos` | Lista vertical alinhada de projetos estratégicos com barras lineares de progresso (`MudProgressLinear`), percentual e relação de tarefas concluídas. | • `Projetos` (`IReadOnlyList<ProjetoPerformance>`, EditorRequired) |
| `AtividadesRecentes` | Linha do tempo de atividades recentes da equipe com avatares por iniciais (`Ui.Iniciais`), ícones temáticos de ação e tempo decorrido. | • `Atividades` (`IReadOnlyList<Atividade>`, EditorRequired) |
| `ProjetosRecentes` | Tabela interativa (`MudTable`) contendo status com chips coloridos, progresso, responsável, data de entrega e menu de ações, convertendo-se em cards no mobile. | • `Projetos` (`IReadOnlyList<ProjetoRecente>`, EditorRequired) |

---

## 📸 Telas do Projeto

### Tema Claro
![Tema Claro](docs/prints/tema-claro.png)

### Tema Escuro
![Tema Escuro](docs/prints/tema-escuro.png)

### Responsividade (Mobile)
![Mobile](docs/prints/mobile.png)

### Inspeção e DevTools (Sem erros no console / Network)
![DevTools](docs/prints/devtools.png)

---

## 🧠 O que aprendi

1. **Qual a diferença entre Blazor Web App (SSR/Server) e Blazor WebAssembly autônomo (standalone)?**
[PREENCHER PELO ALUNO]

2. **Como funciona o ciclo de inicialização do Blazor WebAssembly dentro do navegador através do `index.html` e `Program.cs`?**
[PREENCHER PELO ALUNO]

3. **Por que evitamos escrever CSS próprio ao utilizar MudBlazor e como o sistema de utilitários e temas substitui o CSS tradicional?**
[PREENCHER PELO ALUNO]

4. **Como o `MudTheme` centraliza as paletas (clara e escura), tipografias e propriedades de layout sem espalhar regras no código?**
[PREENCHER PELO ALUNO]

5. **Qual a importância e finalidade dos providers registrados no topo do layout (`MudThemeProvider`, `MudPopoverProvider`, `MudDialogProvider`, `MudSnackbarProvider`)?**
[PREENCHER PELO ALUNO]

6. **Como funciona o padrão de two-way data binding no Blazor através da convenção `@bind-Valor` e `ValorChanged`?**
[PREENCHER PELO ALUNO]

7. **Qual o papel dos parâmetros de ciclo de vida como `OnParametersSet` e dos modificadores de parâmetros como `[Parameter, EditorRequired]` e `RenderFragment`?**
[PREENCHER PELO ALUNO]

8. **Como a combinação do grid de 12 colunas (`MudGrid` / `MudItem`) com os breakpoints e utilitários de display garante uma experiência fluida entre celular, tablet e desktop?**
[PREENCHER PELO ALUNO]

---

## ⚠️ Dificuldades e Soluções
[PREENCHER PELO ALUNO]

---

## 🔮 Melhorias Futuras
[PREENCHER PELO ALUNO]

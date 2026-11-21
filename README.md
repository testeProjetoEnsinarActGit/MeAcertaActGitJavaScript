# MeAcerte

Projeto de jogo 2D desenvolvido na engine Unity e versionado em Git. O repositório contém o projeto Unity (cenas, sprites, animações, scripts e configurações) e uma pasta `Gerenciamento/` com documentação, história e material de design.

## Visão geral

MeAcerte é um projeto Unity com versão indicada em `ProjectSettings/ProjectVersion.txt` (`5.1.1f1`). A estrutura indica um jogo 2D: há configuração de Physics2D (`ProjectSettings/Physics2DSettings.asset`), sprites com animações e controllers (`Assets/Images/*.anim`, `*.controller`) e uma cena de fase (`Assets/Scenes/fase1.unity`).

A lógica de jogo não está implementada no repositório: o único script em `Assets/Scripts/` é um template vazio. O gênero e as regras do jogo não estão descritos nos arquivos.

## Objetivo

Não identificado. Os arquivos `Gerenciamento/Documentacao/Documento.txt` e `Gerenciamento/Historia/Historia.txt` contêm apenas os textos "Repositório para documentação" e "Repositório para História".

Inferência pelo nome do repositório (não confirmada em nenhum arquivo): trata-se de projeto de estudo ou exercício de Git. O repositório também não possui workflows de GitHub Actions.

## Funcionalidades

Nenhuma funcionalidade de jogo está comprovada pelo código. O que existe nos arquivos:

- Uma cena de fase: `Assets/Scenes/fase1.unity`.
- Sprites 2D com animações e controllers em `Assets/Images/`.
- Integração com Visual Studio pelo plugin UnityVS (`Assets/UnityVS/Editor/`).
- Material de apoio em `Gerenciamento/`: um desenho à mão de um personagem (`Design/Desenho.png`), um logo de equipe (`Design/logoEquipe/`) e um arquivo de áudio (`Music/`).

## Arquitetura

### Tecnologias

| Item | Versão / detalhe | Onde está comprovado |
| --- | --- | --- |
| Engine | Unity 5.1.1f1 | `ProjectSettings/ProjectVersion.txt` |
| Linguagens de script | UnityScript (`.js`, com `#pragma strict`) e C# (referenciado pelos `.csproj`) | `Assets/Scripts/`, `Assembly-CSharp.csproj` |
| Target .NET | v3.5 | `Assembly-CSharp.csproj` (linha 13) |
| IDE | Visual Studio (versão não identificada), com plugin UnityVS | `MeAcerte.sln`, `Assets/UnityVS/` |
| Física | Unity Physics2D (configuração presente) | `ProjectSettings/Physics2DSettings.asset` |

### Organização do repositório

```
MeAcertaActGitJavaScript/
├── Assets/              # Recursos do jogo Unity
│   ├── Images/          # Sprites, animações (.anim) e controllers (.controller)
│   ├── Scenes/          # fase1.unity
│   ├── Scripts/         # NewBehaviourScript.js (template vazio)
│   └── UnityVS/         # Plugin de integração com Visual Studio (DLLs do Editor)
├── ProjectSettings/     # Configurações do projeto (Physics2D, Input, Tags, Qualidade etc.)
├── Library/             # Cache gerado pelo Unity (versionado, ver Observações)
├── Temp/                # Arquivos temporários do Unity (versionado)
├── Gerenciamento/       # Documentação, história, design e música (textos e mídia)
├── *.sln, *.csproj, *.unityproj   # Solutions e projetos gerados pelo Unity/Visual Studio
└── .gitignore, .graphifyignore
```

### Padrões e camadas

- O projeto segue o modelo de componentes do Unity (GameObjects com scripts anexados). O único script versionado usa o ciclo padrão `Start()` / `Update()`.
- Não foram identificadas camadas de aplicação (domínio, serviços, repositórios) nem separação de responsabilidades no código, porque o código existente é um template.

### Fluxo principal

Não identificado: os scripts não contêm lógica de jogo. O fluxo esperado de um projeto Unity é a engine carregar a cena `fase1` e chamar `Start()` / `Update()` dos componentes. Isso é comportamento padrão da engine, não código do projeto.

### Persistência e integrações

Nenhuma comprovada. Não há acesso a banco de dados, HTTP ou serviços externos no código. `ProjectSettings/NetworkManager.asset` é um arquivo de configuração de rede do Unity, sem código que o utilize.

### Testes e CI

- Testes: nenhum arquivo de teste encontrado.
- CI: nenhum pipeline encontrado (não existe `.github/workflows`).

## Como executar e testar

Não executado/validado nesta análise.

1. Abrir a pasta do repositório como projeto Unity. O projeto foi salvo na versão 5.1.1f1 (`ProjectSettings/ProjectVersion.txt`); outras versões podem converter o projeto, o que não foi testado.
2. Abrir `Assets/Scenes/fase1.unity` e executar pelo botão Play do editor.
3. Para editar o código, abrir `MeAcerte.sln` no Visual Studio com o plugin UnityVS.
4. Testes: não há comando de teste nem suíte automatizada.

## Observações

Limitações e dívidas técnicas visíveis nos arquivos:

- `Library/` (cerca de 114 arquivos, aproximadamente 15 MB) e `Temp/` estão versionados. O `.gitignore` não tem regras para Unity. Convenção comum: ignorar `Library/`, `Temp/` e `Logs/`.
- Arquivos `.suo` e `*.userprefs` estão versionados (`.vs/`, `MeAcerte-csharp.v12.suo`, `MeAcerte.userprefs`), embora o `.gitignore` liste `*.suo` e `*.userprefs`. Arquivos já rastreados continuam sendo versionados mesmo quando ignorados.
- `sh.exe.stackdump` (dump de erro do Git Bash) está versionado.
- `Assembly-CSharp.csproj` e `UnityVS.MeAcerte.CSharp.csproj` referenciam `Assets/Scripts/NewBehaviourScript.cs`, que não existe. Existe apenas o `NewBehaviourScript.js`. Há referência quebrada e mistura de C# com UnityScript.
- Os scripts são templates vazios, e os textos em `Gerenciamento/` são placeholders.
- Nomes de arquivo indicam material de terceiros: `Binding of Isaac Rebirth - Monstro.png`, `chao_sprites_by_slytheoverlord.png` e `los-numero_1352001032145.jpg`. Origem e licença não foram verificadas. Confirmar os direitos antes de qualquer distribuição.
- Unity 5.1.1f1 e .NET 3.5 são versões antigas. Os nomes de commits com prefixo `150830` sugerem data de 2015 (inferido).
- Os textos em `Gerenciamento/Documentacao/` e `Gerenciamento/Historia/` estão em ISO-8859-1, não em UTF-8.

Não havia README anterior no repositório; este arquivo foi escrito a partir da análise dos arquivos versionados.

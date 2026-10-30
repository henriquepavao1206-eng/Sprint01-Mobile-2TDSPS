# Expedição Átomo: especificação das 8 telas (Figma)

Documento para desenhar o protótipo no Figma. Cobre os 4 blocos de nota da rubrica de Mobile: navegação (25), protótipo visual (30), gerenciamento de estado (20) e formulário com validação (15).

---

## 1. Setup do arquivo no Figma

- Nome do arquivo: `Expedição Átomo - Mobile Sprint 1`
- Páginas: `Capa`, `Design System`, `Telas`, `Fluxo`
- Frame de cada tela: **Android Compact 412 x 917** (preset "Android" do Figma). Nomear `01 Boas-vindas`, `02 Login`, ..., `08 Perfil`
- Grid de 8 pt. Margem lateral de 16 px. Raio dos cards 16, dos botões 12, dos chips 999
- Ícones: Material Icons (plugin "Material Symbols"), porque no Flutter viram `Icon(Icons.xxx)`
- Fonte: Poppins (Google Fonts). Títulos Bold, corpo Regular

## 2. Design system (página "Design System")

### Cores (criar como Color Styles ou Variables)

| Token | Hex | Uso |
|---|---|---|
| bg | #0B1F33 | fundo das telas |
| surface | #132F4C | cards, campos |
| primary | #00C2A8 | botões, destaques |
| accent | #FFB400 | XP, alertas do Doseômetro |
| text | #F2F7FB | texto principal |
| text-muted | #9FB3C8 | texto secundário |
| success | #2ECC71 | resposta certa |
| error | #FF5C5C | resposta errada, erro de campo |

Cores dos pinos por área: Saúde #FF6B8B, Indústria #FFB400, Agricultura #7ED957, Pesquisa Científica #5AB0FF, Energia #B38CFF.

### Tipografia

| Estilo | Tamanho / peso |
|---|---|
| Título | 24 Bold |
| Subtítulo | 18 SemiBold |
| Corpo | 14 Regular |
| Legenda | 12 Regular |

### Componentes (criar como Components com Variants)

- **BotaoPrimario** (default, pressed, disabled) e **BotaoSecundario** (contorno)
- **CampoTexto** (default, focado, erro com mensagem vermelha abaixo)
- **ChipArea** (selecionado, não selecionado)
- **PinMapa** (uma variante por área)
- **CardPonto** (imagem/ícone, título, cidade/UF, chip da área)
- **OpcaoMissao** (neutra, certa, errada)
- **BarraSuperior** (com e sem botão voltar)
- **BarraInferior** com 3 itens: Mapa, Doseômetro, Perfil

## 3. As 8 telas

### 01 Boas-vindas
- **Objetivo:** apresentar o app e levar ao login
- **Layout (Scaffold + Column):** logo/átomo no topo (Image), título "Expedição Átomo", subtítulo "Explore onde a tecnologia nuclear aparece no Brasil", 3 linhas curtas com ícone (Row + Icon + Text: saúde, agricultura, energia), `BotaoPrimario` "Começar" e link "Já tenho conta"
- **Parceiro:** rodapé "Desafio CTMSP, Marinha do Brasil"
- **Navegação:** "Começar" leva a 03 Cadastro; "Já tenho conta" leva a 02 Login

### 02 Login
- **Layout:** AppBar com voltar, Column com 2 CampoTexto (e-mail, senha com ícone de olho para mostrar/ocultar) e `BotaoPrimario` "Entrar"
- **Estado:** olho alterna senha visível/oculta (setState)
- **Navegação:** "Entrar" leva a 04 Mapa; "Criar conta" leva a 03 Cadastro

### 03 Cadastro (formulário principal)
- **Campos (Form + TextFormField):** nome, e-mail, data de nascimento (DatePicker), perfil (DropdownButton: Estudante, Professor, Visitante), aceite dos termos (Checkbox)
- **Validações e mensagens:**
  - Nome: obrigatório, mínimo 3 caracteres. "Informe seu nome completo"
  - E-mail: formato válido. "Digite um e-mail válido"
  - Data de nascimento: obrigatória e anterior a hoje. "Informe uma data válida"
  - Perfil: obrigatório. "Escolha um perfil"
  - Aceite: precisa estar marcado. "Aceite os termos para continuar"
- **Resposta ao usuário:** SnackBar verde "Cadastro realizado! Bem-vindo(a), {nome}" e vai para 04 Mapa. Com erro: campos em vermelho com a mensagem
- **Desenhar 2 frames:** `03a Cadastro com erros` e `03b Cadastro com SnackBar de sucesso`

### 04 Mapa Nuclear
- **Layout (Scaffold + Stack):**
  - Topo: título "Mapa Nuclear do Brasil" e chips de área em linha rolável (ListView horizontal): Todos, Saúde, Indústria, Agricultura, Pesquisa Científica, Energia
  - Centro: imagem do mapa do Brasil com os 11 pinos posicionados (Stack + Positioned) pela latitude/longitude do JSON
  - Rodapé: BarraInferior (Mapa selecionado)
- **Estado (setState):** o chip selecionado filtra os pinos. Desenhar 3 frames: `04a Todos`, `04b Saúde` (só 3 pinos: IPEN, RMB, Goiânia) e `04c Energia` (Aramar e Angra)
- **Navegação:** tocar num pino leva a 05 Detalhe, **passando o ponto como parâmetro**

### 05 Detalhe do ponto
- **Recebe por parâmetro:** o ponto escolhido (título, cidade/UF, área, resumo, curiosidade, fonte)
- **Layout (Column + Card):** AppBar com voltar e ícone de favorito (coração), Card com chip da área, título, "cidade/UF", resumo, bloco "Você sabia?" com a curiosidade, link "Fonte oficial" e `BotaoPrimario` "Fazer missão deste ponto"
- **Estado (setState):** coração alterna vazio/preenchido e um texto "Favoritos: N"
- **Navegação:** voltar retorna ao Mapa; "Fazer missão" leva a 06, passando o ponto

### 06 Missão Mito ou Verdade
- **Layout:** AppBar com voltar e "XP: N" no canto, cartão grande com a afirmação, dois botões grandes "Verdade" e "Mito", placar "Acertos: X de Y"
- **Estado (setState):** ao responder, os botões travam, o certo fica verde e o errado vermelho, o XP sobe (dificuldade x 10), o placar atualiza e aparece o bloco de explicação + fonte e o botão "Próxima missão"
- **Desenhar 3 frames:** `06a Pergunta`, `06b Acertou (+20 XP)`, `06c Errou (explicação)`
- **Fim da rodada:** tela de resumo "Você fez N XP" com botões "Voltar ao mapa" e "Ver perfil"

### 07 Doseômetro
- **Campos (Form):** voos de ida e volta no ano (número, 0 a 100), raios X de tórax no ano (número, 0 a 20), tomografias no ano (número, 0 a 10), bananas por semana (número, 0 a 100)
- **Validações:** campo vazio "Informe um valor (pode ser 0)"; fora da faixa "Valor entre 0 e N"
- **Resultado em Dialog:** dose anual estimada em mSv, comparação com a radiação natural média (2,4 mSv/ano), equivalente em bananas e em dias de radiação natural, e o aviso obrigatório:
  > "O limite de 1 mSv por ano para o público não inclui radiação natural nem exames médicos. Exames são pedidos quando o benefício do diagnóstico supera o risco. Não deixe de fazer um exame por causa deste número."
- **Exemplo para o frame de resultado:** 2 voos (0,06 mSv) + 1 raio X de tórax (0,10 mSv) + 7 bananas por semana (0,0364 mSv) = **0,196 mSv**, cerca de **8% da radiação natural anual**, equivalente a cerca de **1.964 bananas** e **30 dias** de radiação natural
- **Fórmulas (para a explicação no vídeo):** dose em µSv dividida por 0,1 dá bananas; dose em µSv dividida por 6,6 dá dias de radiação natural

### 08 Perfil
- **Layout:** avatar, nome e perfil, Card com XP total e nível, barra de progresso até o próximo nível, GridView de insígnias (conquistada e bloqueada), lista "Pontos favoritos" (ListView)
- **Insígnias de exemplo:** Primeiro Átomo (conquistada), Explorador da Saúde (conquistada), Detetive da Radiação (bloqueada, "vem com as Estações Átomo"), Navegante da Amazônia Azul (bloqueada)
- **Navegação:** BarraInferior (Perfil selecionado); item da lista de favoritos leva a 05 Detalhe

## 4. Fluxo de navegação (página "Fluxo")

```
01 Boas-vindas ──► 03 Cadastro ──► 04 Mapa ──► 05 Detalhe(ponto) ──► 06 Missão(ponto) ──► Resumo ──► 04 Mapa / 08 Perfil
       │                                │  ▲                │ voltar
       └──► 02 Login ───────────────────┘  └────────────────┘
BarraInferior (a partir da 04): Mapa ◄► 07 Doseômetro ◄► 08 Perfil
```

No Figma: ligar os frames com setas de protótipo (On tap, Navigate to, Push) e usar **Navigate back** nos botões voltar. Gerar a imagem do fluxo na página "Fluxo" (ou FigJam) para usar no README e no vídeo.

## 5. Como simular o gerenciamento de estado no Figma

Usar **Variables** do Figma com ações "Set variable" e condicionais, que reproduzem o `setState()`:

| Variável | Tipo | Onde muda |
|---|---|---|
| `filtroArea` | String | chips da tela 04 |
| `favorito` | Boolean | coração da tela 05 |
| `qtdFavoritos` | Number | soma 1 ou subtrai 1 ao favoritar |
| `xp` | Number | tela 06, soma 10, 20 ou 30 por acerto |
| `acertos` / `respondidas` | Number | tela 06 |
| `senhaVisivel` | Boolean | olho da tela 02 |

Mostrar `xp` e `acertos` nos textos usando a variável. Assim o protótipo clicável realmente muda na tela, que é o que a rubrica quer ver ("a interface é atualizada dinamicamente").

## 6. Mapeamento Figma para Flutter (para a Sprint 2)

| Elemento no Figma | Widget Flutter |
|---|---|
| Frame da tela | `Scaffold` |
| Barra superior | `AppBar` |
| Auto layout vertical / horizontal | `Column` / `Row` |
| Retângulo com fundo | `Container` |
| Espaçamento interno / entre itens | `Padding` / `SizedBox` |
| Card de ponto, de missão | `Card` |
| Mapa e logo | `Image` |
| Ícones | `Icon` |
| Lista de pontos favoritos, chips | `ListView` |
| Insígnias | `GridView` |
| Pinos sobre o mapa | `Stack` + `Positioned` |
| Campos | `Form` + `TextFormField` |
| Resultado do Doseômetro | `showDialog` / `AlertDialog` |
| Sucesso do cadastro | `SnackBar` |

## 7. Entrega do Figma

1. Prototype > Present: testar o fluxo inteiro
2. Share > "Anyone with the link can **view**" e copiar o link para o README
3. Exportar as 8 telas em PDF (File > Export frames to PDF) como backup e colocar na pasta `docs/` do repositório
4. Exportar também as imagens PNG das telas para a pasta `docs/telas/`

## 8. Checklist da rubrica de Mobile

- [ ] 5 ou mais telas com função real (são 8)
- [ ] Fluxo avança e retorna, com parâmetro entre telas (04 para 05 para 06)
- [ ] Estrutura visual definida e consistente em todas as telas (design system)
- [ ] Widgets pedidos representados: Scaffold, AppBar, Column, Row, Container, Padding, SizedBox, Card, Image, Icon, ListView, GridView
- [ ] Pelo menos uma funcionalidade de estado (chips, favorito, XP)
- [ ] Formulário com validação e resposta (Cadastro com SnackBar, Doseômetro com Dialog)
- [ ] Dados mockados coerentes com o modelo comum (arquivo `dados_mockados.json`)
- [ ] Vídeo narrado de até 5 min, publicado como "Não listado" no YouTube
- [ ] README.md com todos os itens e link do vídeo

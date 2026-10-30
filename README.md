# Expedição Átomo

Aplicativo mobile gamificado que leva o estudante a explorar, num mapa do Brasil, os lugares reais onde a tecnologia nuclear aparece (saúde, indústria, agricultura, pesquisa científica e energia) e a cumprir missões de **Mito ou Verdade** em cada um.

> **Challenge FIAP 2026, 2º ano de Análise e Desenvolvimento de Sistemas (turmas de agosto), Sprint 1**
> Disciplina: Mobile Application Development

## Empresa parceira

**CTMSP, Centro Tecnológico da Marinha em São Paulo**, que conduz o Programa Nuclear da Marinha (PNM), desenvolvido desde 1979. O desafio proposto: desenvolver uma solução digital inovadora e interativa que aproxime a sociedade da tecnologia nuclear, mostrando suas aplicações e benefícios de forma acessível, educativa e envolvente.

## Integrantes

| Nome | RM |
|---|---|
| Henrique Spoltore Moreno Pavão dos Santos | 568130 |
| Raphael Oliveira Sinelli Mendonça | 568346 |
| Arthur Lins Belarmino | 566845 |
| Lucas Martinez Lopes | 553816 |

Turma: Expedição Átomo

## Descrição da solução

O brasileiro desconfia de uma tecnologia que já usa: o tema nuclear costuma ser associado só a usinas, radiação e bomba, e pouco ao hospital, à lavoura e à pesquisa. A Expedição Átomo transforma esse conteúdo em uma jornada curta e jogável para estudantes do Ensino Médio, com fonte oficial em toda afirmação e benefícios e riscos lado a lado (Goiânia, 1987, está no mapa junto com o IPEN).

Principais funcionalidades:

- **Mapa Nuclear do Brasil:** 11 pontos reais filtráveis pelas 5 áreas do enunciado
- **Missões Mito ou Verdade:** XP de 10, 20 ou 30 conforme a dificuldade, com explicação e fonte depois de cada resposta
- **Doseômetro:** estima a dose anual de radiação (voos, exames, bananas) e compara com a média natural, com aviso para não desestimular exames
- **Perfil:** XP, nível e insígnias

## O que foi desenvolvido nesta Sprint

Esta primeira entrega é o **escopo e o protótipo visual** do aplicativo, desenhado no **Figma**, com as 8 telas, o fluxo de navegação e as interações principais já clicáveis. O aplicativo ainda não é funcional: o código Flutter vem nas próximas sprints, a partir deste protótipo.

| # | Tela | O que demonstra |
|---|---|---|
| 1 | Boas-vindas | Apresentação do app e do parceiro |
| 2 | Login | Campos e alternância de senha visível |
| 3 | Cadastro | Formulário com validação e SnackBar |
| 4 | Mapa Nuclear | Pinos por área e filtro por chips (estado) |
| 5 | Detalhe do ponto | Recebe o ponto por parâmetro, com favoritar (estado) |
| 6 | Missão Mito ou Verdade | Placar e XP que mudam a cada resposta (estado) |
| 7 | Doseômetro | Formulário com validação e resultado em Dialog |
| 8 | Perfil | XP, nível e insígnias |

Requisitos da disciplina e onde aparecem no protótipo:

- **Navegação entre telas:** 8 telas conectadas, avançando e voltando, com passagem de parâmetro (Mapa, Detalhe e Missão)
- **Protótipo visual funcional:** design system único (cores, tipografia, espaçamento e componentes), com os widgets previstos: Scaffold, AppBar, Column, Row, Container, Padding, SizedBox, Card, Image, Icon, ListView e GridView
- **Gerenciamento de estado:** filtro do mapa, favoritar, XP e placar, previstos com `StatefulWidget` e `setState()`
- **Formulário e validação:** Cadastro e Doseômetro, com mensagens de erro e resposta por SnackBar e Dialog
- **Dados mockados:** [`dados_mockados.json`](dados_mockados.json), com os mesmos pontos, áreas e missões do modelo de dados do grupo

## Protótipo e documentos

- **Protótipo no Figma (clicável):** https://www.figma.com/design/a9qZqGB5UyeR4gaE0JOH0n
- **Vídeo de demonstração (YouTube, não listado):** [(https://www.youtube.com/watch?v=RQblJ_mJoHE)]
- **Especificação das telas:** [`ESPECIFICACAO_FIGMA.md`](ESPECIFICACAO_FIGMA.md)
- **Telas exportadas:** pasta [`docs/`](docs/)

## Como visualizar o protótipo

1. Abra o link do Figma acima (acesso por link, somente visualização)
2. Clique em **Present** (ícone de play) no canto superior direito
3. Comece pela tela **01 Boas-vindas** e navegue tocando nos botões
4. Para testar o estado: na tela de Mapa, toque nos chips de área; na tela de Detalhe, toque no coração; na tela de Missão, responda para ver o XP e o placar subirem

## Tecnologias

- **Figma:** protótipo, design system e variáveis de protótipo (simulam o estado)
- **Flutter e Dart:** tecnologia prevista para a implementação do aplicativo nas próximas sprints
- **GitHub e Markdown:** versionamento e documentação

## Integração com as outras disciplinas

O app consome os mesmos nomes de campos do modelo de dados comum do grupo (`AREA_APLICACAO`, `PONTO_MAPA`, `MISSAO`, `USUARIO`, `RESPOSTA_MISSAO`): a API Java servirá o mapa, o motor .NET cuidará das missões, o banco Oracle guardará os dados e as Estações Átomo (IoT) alimentarão o mapa com radiação medida ao vivo.

## Fontes

Conteúdo baseado em fontes oficiais: CNEN, IPEN, Marinha do Brasil, INB, USP, IAEA e UNSCEAR. Referências completas no documento de ideação do grupo.

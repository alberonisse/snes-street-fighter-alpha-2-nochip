# CARTA ABERTA A GUSTAVO FRANCO

[Português](README.md) / [English](README.en.md) / [Español](README.es.md) / [Italiano](README.it.md) / [Deutsch](README.de.md) / [简体中文](README.zh-CN.md) / [日本語](README.ja.md) / [繁體中文（香港）](README.zh-HK.md)

Pedido de esclarecimento, correção de atribuição e retratação
11 de novembro de 2026

Gustavo,

Criei este fork depois que você arquivou o repositório porque foi a única forma rápida e direta que encontrei de tentar fazer esta carta chegar até você o quanto antes.

Escrevo para contestar a atribuição publicada em seu repositório, que identifica os cartuchos mencionados na página como uma comercialização da sua implementação de Street Fighter Alpha 2 sem S-DD1.

Minha declaração sobre a origem da edição é expressa: não aproveitei material do seu projeto na edição USA de 8 MiB com Shin Akuma e carregamento acelerado que forneci por meio da minha descompactação e dos patches preparados para memória 29LV640. Declaro que os cartuchos a que me refiro utilizam essa edição. Contesto a atribuição desses cartuchos ao seu projeto sem uma identificação técnica do conteúdo efetivamente utilizado.

Meu objetivo com esta carta é esclarecer a origem da edição em questão, explicar a trajetória do meu trabalho e solicitar que a atribuição pública seja sustentada por evidências verificáveis.

## 1. A TRAJETÓRIA DO MEU PROJETO

Meu trabalho não começou com a disponibilização dos patches de 8 MiB. Houve um processo anterior de estudo do S-DD1, desenvolvimento de ferramentas, análise do mapeamento, montagem de placas, correções e testes em SNES real.

O plano original envolvia uma PCB com CPLD, destinada a controlar o acesso aos dados e preservar os detalhes da implementação. Não pretendia disponibilizar abertamente toda essa estrutura de descompactação, organização dos dados e reconstrução.

Quando tomei conhecimento da publicação do seu projeto, fiquei profundamente desmotivado. Passei a considerar comprometido o diferencial do trabalho no qual vinha investindo tempo e esforço. Essa foi a minha percepção sobre o futuro do meu projeto.

Foi nesse contexto que decidi mudar de direção e disponibilizar privadamente a descompactação e os patches da edição de 8 MiB, para dar continuidade ao trabalho já realizado. Essa decisão não autoriza identificar automaticamente a edição que forneci como uma versão do seu repositório.

## 2. COMO FUNCIONA MINHA ABORDAGEM DE DESCOMPACTAÇÃO

No núcleo original do sdd1_unpacker, estudei e isolei a implementação do S-DD1 existente no bsnes. Os créditos do código foram preservados: Andreas Naive pelo algoritmo/implementação original e byuu pelo port do bsnes. Não reivindico a invenção do algoritmo S-DD1.

Esse código foi adaptado para uma ferramenta C++ independente da interface gráfica e do funcionamento completo do emulador, com leitura validada dos dados da ROM e tratamento dos bancos de memória do S-DD1.

O jogo não trata a ROM inteira como um único arquivo compactado. Ele solicita fluxos específicos, normalmente durante transferências DMA. Por isso, o trabalho envolveu analisar descritores e tabelas da ROM original, registrar solicitações realizadas durante a execução e consolidar origem, tamanho e configuração dos bancos de memória.

O trace canônico da reconstrução histórica possui 3.155 identidades de requests em 3.160 linhas. As cinco linhas adicionais registram evidências de outros pontos de chamada para pedidos já catalogados. Requests observados e entradas inferidas estaticamente são classificados separadamente; essa contagem não significa 3.155 fluxos comprimidos distintos nem prova, por si só, cobertura de todas as situações do jogo.

A cadeia do núcleo original foi estruturada como: ROM original USA, análise e traces, catálogo de requests, descompactação dos dados, organização em um novo layout, patches de DMA e verificações da reconstrução sem S-DD1.

Essa reconstrução exigiu distinguir endereço da CPU de offset no arquivo, respeitar as regiões de ROM do SNES e redirecionar as rotinas tratadas para dados já descompactados. Não se resume a aumentar o arquivo ou mudar seu cabeçalho.

## 3. A ADAPTAÇÃO DE 8 MiB E A PLACA SIMPLES

A linha de 8 MiB deve ser distinguida do núcleo anterior de reconstrução de 16 MiB. Ela passou por outro processo de organização e alocação, utilizando um inventário extraído da base 16mb que realizei os testes e postei no youtube, além de correções e verificações posteriores. Não a apresento como um simples recorte do arquivo de 16 MiB.

A edição foi preparada para uma placa simples, com as ligações adequadas e uma única memória Flash TSOP48 de 8 MiB, a 29LV640 em modo x8. Essa edição não exige S-DD1 ou CPLD para funcionar nessa configuração e foi testada em SNES real. Também houve preparação da variante para placa LoROM modificada.

Existe uma diferença objetiva em relação à conversão histórica de 12 MiB documentada no seu projeto. Essa imagem de 12 MiB não pode ser simplesmente gravada na 29LV640 de 8 MiB e utilizada na configuração que demonstrei. Seu próprio relato técnico descreve um mapeamento específico, incluindo uma janela nos bancos C0-FF:

https://github.com/snes9xgit/snes9x/issues/1081

Não estou afirmando que sua implementação jamais possa ser adaptada para um cartucho físico, nem negando os testes em hardware que você documentou. Estou distinguindo uma imagem de 12 MiB e seu mapeamento da edição de 8 MiB preparada para a minha configuração de placa.

Se a proposta é ampliar o acesso ao jogo, considero importante reconhecer também esse caminho: permitir que pessoas utilizem uma placa simples e componentes acessíveis, sem precisar adquirir um flashcart específico. Já havia registrado uma placa de testes utilizada nesse trabalho; o vídeo consta na relação ao final desta carta.

## 4. CRÉDITOS E PRECISÃO

A presente contestação se refere especificamente à edição USA de 8 MiB utilizada nos cartuchos mencionados. A origem dessa edição deve ser examinada a partir dos arquivos efetivamente utilizados, de seus patches e de sua proveniência. Não deve ser presumida a partir de inventários de outra região ou de revisões de pesquisa separadas, nem da simples semelhança entre os recursos anunciados.

Não reivindico autoria exclusiva do algoritmo público, de rotinas de terceiros ou dos dados do jogo original. Reivindico o reconhecimento correto do trabalho de integração, adaptação, correção e validação realizado na edição que forneci.

## 5. REGISTROS PÚBLICOS PARA CONFERÊNCIA DA CRONOLOGIA

Apresento os registros abaixo para que conteúdo e datas de publicação possam ser confrontados com o histórico das versões. Eles documentam a trajetória que estou relatando; não substituem a comparação dos arquivos efetivamente usados no cartucho.

Placa simples de testes:
https://www.youtube.com/shorts/EVQoQB8mD1A

Registro complementar 1:
https://www.youtube.com/shorts/uhzHfQFPbVw

Registro complementar 2:
https://www.youtube.com/shorts/23gS_IEGDqc

Transmissão relacionada ao projeto:
https://www.youtube.com/live/zakojPNeGc0

Registro complementar 3:
https://www.youtube.com/shorts/PXVAKPfAO1E

Registro complementar 4:
https://www.youtube.com/shorts/y8PAzIzPz1I

Registro complementar 5:
https://www.youtube.com/shorts/bStb8AW_QzQ

Registro complementar 6:
https://www.youtube.com/shorts/if26BECUllI

Etapa com PCB e CPLD:
https://www.youtube.com/shorts/X-Hby6Vw-m4

Vídeo que publiquei antes da preparação e do compartilhamento privado dos patches de 8 MiB:
https://www.youtube.com/shorts/YZbpycbEW0w

Demonstração posterior do jogo em placa simples com a 29LV640:
https://www.youtube.com/shorts/GKl1eOMFks0

Meu esclarecimento dirigido a você:
https://youtu.be/8X8jRSXFb5I

## 6. O QUE SOLICITO

A publicação à qual me refiro está em:
https://github.com/gufranco/snes-street-fighter-alpha-2-nochip

Solicito que esclareça qual arquivo foi examinado, qual seu hash, de qual cartucho ele foi obtido e quais elementos técnicos sustentaram a atribuição à sua implementação.

Também solicito que a comparação considere o mapeamento físico, as rotinas, os patches e a revisão concreta, em vez de tomar como prova apenas a descrição comercial ou a presença de recursos como Shin Akuma e carregamento acelerado.

Enquanto essa identificação permanecer contestada e sem demonstração técnica apresentada, peço que a publicação deixe essa condição explícita e retire a atribuição categórica. Confirmado o equívoco, solicito a correção das publicações e uma retratação com visibilidade equivalente à exposição original.

Respeito o seu trabalho e solicito que você respeite o meu também. Não pretendo promover ataques pessoais ou diminuir sua dedicação.

A questão que apresento é objetiva: a origem de uma implementação precisa ser demonstrada. Um resultado semelhante, um nome de anúncio ou uma embalagem não substituem a análise do conteúdo efetivamente utilizado.

Atenciosamente,

Responsável pelo projeto ALBER MULTI HOUSE

# Roteiro de Exercícios — Padrões de Projeto em C#

> Documento-semente. Cada exercício mira **um padrão**, mas a regra é a mesma de sempre:
> primeiro você escreve o código feio que funciona, **sente a dor**, e só então refatora
> aplicando o padrão. O padrão é a resposta — mas você precisa ter vivido a pergunta.

---

## Propósito

Você já *entende* os padrões de cabeça. O que falta é o reflexo: olhar para um trecho de
código, reconhecer o cheiro, e saber qual ferramenta pegar — sem aplicar a ferramenta onde
ela não cabe.

São três músculos diferentes:

1. **Reconhecimento** — ver um `switch` gigante e sentir "isso é Strategy", ver flags
   booleanas se multiplicando e sentir "isso é Decorator".
2. **Aplicação idiomática** — implementar o padrão no jeito que o C# moderno espera, não na
   tradução literal do livro de 1994.
3. **Julgamento** — saber quando **não** usar o padrão, porque um `if` ou um `Func<>` já
   resolvia.

A maioria dos tutoriais só treina o (2), e mal. Este roteiro treina os três — e o terceiro é
o que separa quem aplica padrões de quem é escravo deles.

---

## Como este roteiro difere do de OOP

No roteiro de OOP, a IA escondia o padrão de propósito: o objetivo era **você descobrir**
onde a abstração precisava nascer. Aqui é prática dirigida — você já sabe que hoje está
treinando Decorator. Mas a sequência continua sendo concreto → dor → refatoração, por um
motivo: se você já pulasse pro padrão, estaria copiando UML. Escrevendo a versão ingênua
primeiro, você sente *por que* o padrão existe — e da próxima vez, no código de verdade, vai
reconhecer o cheiro mesmo sem ninguém te avisar o nome.

---

## Princípios que valem para todos os exercícios

- **Faça doer primeiro.** Escreva a versão mais ingênua que funciona — o `switch`, a flag, o
  `new` no meio da regra de negócio. Não é gambiarra: é o estado inicial do experimento.
- **A dor justifica o padrão, não o contrário.** Se você refatorou e não aliviou nenhuma dor
  concreta, o padrão estava sobrando. Anote isso — é um acerto, não um fracasso.
- **O C# moderno às vezes já é o padrão.** `event`, DI, `Func<>`/delegates, `IEnumerable`/
  `yield`, object initializers, records — vários padrões do GoF estão embutidos na linguagem
  ou no framework. Saber o idioma é parte do exercício. Cada exercício aponta o equivalente.
- **Regra de três continua valendo.** Não extraia o padrão na primeira variação. Espere a
  segunda ou terceira aparecer pra sentir o atrito de verdade.
- **IA como revisora, não arquiteta.** A IA gera o cenário e, no fim, critica a *sua*
  refatoração — se aplicou bem, se aplicou cedo demais, se a forma clássica fazia sentido ali
  ou se o idioma moderno era melhor.
- **Disciplina de escopo.** Um padrão por exercício. Console, em memória, sem banco, sem UI,
  sem rede. O ganho está no design, não no volume.

---

## Como usar este roteiro

1. Escolha um exercício (comece pelo Fácil 1 e suba em ordem).
2. Copie o **Prompt-base** abaixo, preencha o nome do padrão e cole a **Descrição do
   sistema** do exercício no lugar indicado.
3. A IA te devolve um cenário em **rodadas**: a primeira é a coisa mais simples que funciona;
   as seguintes jogam requisitos novos que vão fazer a versão ingênua ranger. Sem código, sem
   solução.
4. Implemente a Rodada 1 do jeito mais direto e burro possível. Funcionou? Vá pra Rodada 2 e
   **estenda a versão ingênua** — não refatore ainda. Deixe a dor crescer.
5. Quando o atrito ficar óbvio (geralmente na Rodada 2 ou 3), **pare e refatore** aplicando o
   padrão alvo.
6. Mande sua versão final pra IA no **modo revisor**. Peça as três avaliações: apliquei o
   padrão corretamente? Apliquei cedo demais (a dor era real)? A forma clássica era a certa,
   ou o idioma moderno do C# era melhor aqui?
7. Anote no seu `DUVIDAS.md`: qual era o cheiro, o que doía antes, o que o padrão aliviou, e
   onde você teria pulado o padrão se fosse código de produção.

---

## Prompt-base

> Preencha `[PADRÃO ALVO]` e cole a descrição do exercício no final.

```
Você é um tech lead me passando um exercício para eu treinar um padrão de projeto
específico. O padrão alvo é: [PADRÃO ALVO].

Vou te dar a descrição de um sistema. Sua tarefa é transformá-la num exercício em RODADAS,
projetado para eu primeiro escrever uma versão ingênua e só depois refatorar para o padrão.

Produza, nesta ordem:
1. Contexto de negócio — o cenário real, quem usa, qual problema resolve.
2. Rodada 1 (o concreto burro) — a versão mais simples que funciona de ponta a ponta,
   pequena o bastante para eu resolver com um if/switch/new direto, SEM o padrão. Descreva
   só o requisito; não me diga como estruturar.
3. Rodadas de evolução (2 a 4) — cada uma adiciona um requisito novo e plausível que faz a
   abordagem ingênua ranger cada vez mais. Pelo menos uma rodada deve deixar a dor que o
   padrão [PADRÃO ALVO] alivia bem visível. Inclua, se couber, uma variação que seja
   TENTADORA mas onde aplicar o padrão seria exagero — quero treinar o julgamento.
4. Critérios de "pronto" — checklist objetivo.
5. Checklist de reflexão pós-refatoração — perguntas focadas em: a dor era real? apliquei o
   padrão cedo demais? a forma clássica ou o idioma moderno do C# era melhor aqui?

Restrições obrigatórias (não quebre nenhuma):
- NÃO escreva código de nenhum tipo.
- NÃO mostre como implementar o padrão, nem diagrama de classes, nem nomes de interfaces ou
  métodos. Eu descubro a forma. Você descreve o PROBLEMA, não a solução.
- NÃO refatore por mim, nem antecipe onde a abstração entra.
- Escopo enxuto: console/biblioteca C# .NET, em memória ou hardcoded. Sem banco, UI ou rede.
- Respeite o escopo da descrição — não adicione funcionalidade além do necessário para
  exercitar o padrão.

Quando eu te enviar minha refatoração final, troque para o MODO REVISOR e me dê três
avaliações honestas:
- Corretude: apliquei o padrão [PADRÃO ALVO] corretamente e de forma idiomática em C#?
- Julgamento: a dor que motivou o padrão era real, ou eu apliquei cedo demais / sem
  necessidade?
- Idioma: a forma clássica do padrão fazia sentido aqui, ou o C# moderno (event, DI,
  delegate, IEnumerable, object initializer, etc.) teria sido mais simples? Por quê?
Não reescreva por mim; aponte e explique.

Descrição do sistema:
[COLE AQUI A DESCRIÇÃO DO EXERCÍCIO]
```

---

# Os Exercícios

## Nível Fácil

### Exercício 1 — Strategy · Calculadora de Frete

**O smell que ele ataca:** um `switch` (ou cadeia de `if`) que escolhe *qual cálculo rodar*
com base em um tipo. Cada variação nova obriga a editar o mesmo método central, que vira um
monstro.

**Descrição do sistema:** um módulo que calcula o custo de frete de um pedido (peso, dimensões,
CEP de origem e destino, valor da mercadoria). Cada transportadora tem sua própria fórmula —
uma cobra por peso, outra por volume cúbico, outra tem tabela fixa por região, outra dá frete
grátis acima de um valor. O sistema recebe o pedido e a transportadora escolhida e devolve o
custo. Começa com uma transportadora; a evolução adiciona outras, cada uma com regra diferente,
e por fim a necessidade de "cotar em todas e devolver a mais barata".

**A dor que deve aparecer:** o método de cálculo vira um `switch (transportadora)` que cresce a
cada parceiro novo, e a regra "cote em todas" te obriga a varrer esse switch.

**Escopo:** console, valores hardcoded. Foco em como o cálculo absorve transportadoras novas sem
tocar no que já funciona.

**Idioma C# moderno:** a forma clássica é uma interface com várias implementações injetadas. Mas
repare onde um `Dictionary<TipoTransportadora, IFreteStrategy>` ou até um `Func<Pedido, decimal>`
deixa tudo mais enxuto. *Onde você reencontra:* regras de negócio variáveis no FinTrack; é o
padrão mais comum que existe em backend.

---

### Exercício 2 — Factory · Spawner de Inimigos

**O smell que ele ataca:** lógica de *criação* de objetos (com `new` e ramificações) espalhada
no meio da regra de negócio. O código que *usa* o objeto fica acoplado aos tipos concretos e
sabe demais sobre como montá-los.

**Descrição do sistema:** um módulo de um RPG de console que, dado um tipo de encontro (caverna,
floresta, chefe) e um nível de dificuldade, monta o inimigo apropriado — com vida, ataque, loot
e comportamento iniciais coerentes. A montagem de cada inimigo tem suas regras (um goblin de
nível 5 não é só "goblin com número maior"; um chefe tem regras próprias de loot). Começa com um
tipo; a evolução adiciona famílias de inimigos e a regra de que o mesmo encontro pode gerar
inimigos diferentes conforme o nível.

**A dor que deve aparecer:** o `new` com `switch` aparece em vários lugares que precisam criar
inimigos, e cada tipo novo te faz caçar todos esses pontos. A lógica de montagem se duplica.

**Escopo:** console, dados hardcoded. Foco em separar *quem cria* de *quem usa*.

**Idioma C# moderno:** cuidado com a confusão entre Simple Factory (uma classe com switch),
Factory Method (método virtual sobrescrito) e Abstract Factory (família de produtos) — na
revisão, peça pra IA te dizer qual você de fato implementou e se era o certo. *Onde você
reencontra:* o próprio container de DI do .NET é uma fábrica gigante; e a criação de handlers/
parsers por tipo é pão com manteiga.

---

### Exercício 3 — Adapter · Unificando Fontes de Sensores

**O smell que ele ataca:** seu código se contorcendo para falar com APIs externas incompatíveis,
com tradução e `if` espalhados toda vez que você integra uma fonte nova.

**Descrição do sistema:** um módulo que coleta leituras de sensores de diferentes "fornecedores"
(simulados). Um devolve os dados num formato (digamos, um objeto com Celsius e timestamp Unix),
outro num formato totalmente diferente (XML legado com Fahrenheit e data ISO), outro via um
método com assinatura esquisita. Seu sistema precisa de **uma** visão uniforme de "leitura"
para processar tudo igual. Começa com uma fonte; a evolução adiciona as outras, cada uma com seu
formato e suas manhas, sem que o processador central precise saber dessas diferenças.

**A dor que deve aparecer:** o processador central começa a encher de `if (fornecedor == X)` e
conversões inline, e cada fornecedor novo o suja mais.

**Escopo:** console, fornecedores simulados como classes com assinaturas propositalmente
diferentes. Foco em isolar o "tradutor" de cada fonte do código que consome.

**Idioma C# moderno:** quase sempre é só uma interface comum + uma classe-invólucro por fonte
(às vezes um extension method resolve casos pequenos). *Onde você reencontra:* literalmente o
SensorWatch — múltiplos protocolos de sensor caindo num modelo interno único. E qualquer
integração com SDK de terceiro.

---

## Nível Médio

### Exercício 4 — Builder · Construtor de Ficha de Personagem

**O smell que ele ataca:** o construtor telescópico (`new Personagem(nome, classe, força,
destreza, ..., null, null, true)`) ou o objeto que fica mutável e *inválido no meio da
montagem*. Difícil de ler, fácil de montar errado.

**Descrição do sistema:** um módulo que monta a ficha de um personagem de RPG. A ficha tem
muitos atributos: alguns obrigatórios (nome, classe), muitos opcionais (perícias, equipamentos,
traços, história), e regras de consistência (um mago não pode iniciar com armadura pesada; a
soma dos pontos de atributo tem um teto). A montagem deve ser legível e impedir que um
personagem inválido exista. Começa com poucos campos; a evolução adiciona opcionais e regras de
validação que precisam rodar no momento da finalização.

**A dor que deve aparecer:** o construtor explode em parâmetros/overloads, ou você cria o objeto
e vai "preenchendo" — e aí ele existe em estados inválidos no meio do caminho.

**Escopo:** biblioteca/console, em memória. Foco em uma construção legível, validada e que só
entrega um objeto válido no final.

**Idioma C# moderno:** aqui mora um julgamento importante — object initializers e `records` com
`init` muitas vezes já bastam, e um Builder completo só se paga quando há validação no fim,
ordem obrigatória de passos, ou imutabilidade. Na revisão, pergunte: *o Builder se pagou, ou um
initializer resolvia?* *Onde você reencontra:* a Fluent API do EF Core e o FluentValidation são
builders; configuração via `WebApplicationBuilder` também.

---

### Exercício 5 — Decorator · Camadas de um Serviço de Dados

**O smell que ele ataca:** uma classe que acumula responsabilidades transversais (log, cache,
retry) via flags booleanas — `new Servico(comCache: true, comLog: true, comRetry: false)` — ou
via explosão de subclasses. Com N comportamentos opcionais e combináveis, você cai em 2^N
combinações.

**Descrição do sistema:** um serviço que busca dados de uma fonte (simule com um delay e falhas
ocasionais). Você quer poder, opcionalmente e em qualquer combinação, **adicionar**: cache (não
buscar de novo o que já buscou), log (registrar cada chamada e quanto demorou), e retry (tentar
de novo em caso de falha). O núcleo do serviço não deve saber nada disso. Começa só com a busca;
a evolução pede cada comportamento, e por fim a combinação livre deles, em ordem que importa
(faz sentido logar por fora do cache? retry por dentro ou por fora?).

**A dor que deve aparecer:** as flags/condicionais se multiplicam e a ordem dos comportamentos
fica impossível de controlar dentro de uma classe só.

**Escopo:** console, fonte simulada. Foco em empilhar comportamentos sem tocar no núcleo.

**Idioma C# moderno:** este padrão é onipresente no .NET e vale internalizar — o pipeline de
middleware do ASP.NET é Decorator, o Polly (retry, circuit breaker) é Decorator, e decorar
repositórios com cache é exatamente o que você fará com o Redis no SensorWatch. O Scrutor
automatiza isso na DI. *Onde você reencontra:* em todo lugar. Talvez o padrão de maior ROI desta
lista pro seu roadmap.

---

### Exercício 6 — Composite · Explorador de Sistema de Arquivos

**O smell que ele ataca:** código que trata "item único" e "grupo de itens" por caminhos
separados, com recursão cheia de checagem de tipo (`if (é pasta) ... else ...`).

**Descrição do sistema:** um módulo que modela um sistema de arquivos em memória: pastas contêm
arquivos **ou outras pastas**, em qualquer profundidade. Você precisa responder, de forma
uniforme para qualquer nó: tamanho total, contagem de arquivos, e uma busca por nome. Começa com
arquivos soltos; a evolução introduz pastas aninhadas e a exigência de que toda operação funcione
igual num arquivo, numa pasta, ou na raiz inteira.

**A dor que deve aparecer:** sem o padrão, cada operação precisa distinguir arquivo de pasta e a
recursão fica salpicada de `cast` e `if`.

**Escopo:** console, árvore em memória. Foco em tratar folha e composto pela mesma interface.

**Idioma C# moderno:** este é quase a forma clássica mesmo — uma interface comum e recursão; o
C# não tem açúcar especial aqui. *Onde você reencontra:* árvores de categorias, estruturas de
comentários aninhados, qualquer hierarquia.

---

### Exercício 7 — Observer · Reações a uma Anomalia

**O smell que ele ataca:** um objeto que, ao fazer algo, **chama diretamente** cada interessado.
Cada novo interessado obriga a editar esse objeto, que passa a conhecer o mundo todo. Acoplamento
que cresce sem parar.

**Descrição do sistema:** um processador de leituras que, ao detectar uma anomalia (valor fora de
um limite), precisa disparar várias reações: registrar no log, criar um alerta, atualizar um
painel resumido, e notificar um operador. O processador **não deve** conhecer cada um desses
reatores. Começa com uma reação; a evolução adiciona as outras, e por fim a exigência de que dê
pra ligar/desligar reatores sem mexer no processador.

**A dor que deve aparecer:** o método que detecta a anomalia vira uma lista hardcoded de chamadas
diretas que cresce a cada reação nova.

**Escopo:** console, reatores simulados (imprimem o que fariam). Foco em desacoplar quem dispara
de quem reage.

**Idioma C# moderno:** a forma clássica (interface `IObserver` + `Subject`) raramente é a melhor
em C#. Prefira `event`/`EventHandler` para in-process, ou domain events despachados. Na revisão,
compare as duas formas. *Onde você reencontra:* **direto no coração do SensorWatch** — o
`TemperatureExceededThreshold` do seu roadmap é exatamente isto. Domain events e notificações do
MediatR são Observer.

---

## Nível Difícil

### Exercício 8 — Chain of Responsibility · Cadeia de Aprovação

**O smell que ele ataca:** um `if/else if` aninhado decidindo *quem* trata uma requisição,
geralmente por faixas. Mudar um limite ou inserir um nível no meio obriga a remexer todo o bloco.

**Descrição do sistema:** um módulo que processa solicitações de compra. Cada solicitação tem um
valor e precisa ser aprovada pelo nível certo: até um teto, o gerente aprova; acima, vai pro
diretor; acima de outro teto, pro VP; acima disso, exige o conselho. Alguns níveis podem
**rejeitar direto** (fora de orçamento) ou **passar adiante**. Começa com dois níveis; a evolução
adiciona níveis, insere um nível no meio, e por fim regras extras (algumas categorias pulam o
gerente e vão direto pro diretor).

**A dor que deve aparecer:** a cadeia de `if` vira um emaranhado, e inserir um nível no meio ou
mudar a ordem é cirurgia de risco.

**Escopo:** console, em memória. Foco em montar a cadeia de aprovadores de forma que ordem e
níveis sejam fáceis de rearranjar.

**Idioma C# moderno:** o pipeline de middleware do ASP.NET é Chain of Responsibility — cada
middleware decide tratar ou chamar `next`. Compare a forma clássica (handlers encadeados) com uma
lista de delegates. *Onde você reencontra:* middleware, validações encadeadas, pipelines de
processamento.

---

### Exercício 9 — State · Estados de Combate

**O smell que ele ataca:** todo método do objeto começa com um `switch (estado)`, e a validação
de quais transições são legais fica espalhada e furada — dá pra cair num estado impossível.

**Descrição do sistema:** um personagem de combate de console que tem estados: normal, defendendo,
atordoado, enfurecido. As ações (atacar, defender, receber dano, passar o turno) se comportam
diferente em cada estado — atordoado não pode atacar; enfurecido causa mais dano mas não pode
defender; receber dano pesado pode atordoar. E há transições válidas e inválidas entre estados.
Começa com dois estados e uma ação; a evolução adiciona estados, ações, e regras de transição que
não podem ser violadas.

**A dor que deve aparecer:** cada ação vira um `switch (estado)`, e garantir que só transições
legais aconteçam fica impossível de manter conforme estados e ações crescem.

**Escopo:** console, em memória. Foco em encapsular o comportamento e as transições legais de cada
estado.

**Idioma C# moderno:** julgamento importante aqui — para máquinas pequenas, um `enum` + uma tabela
de transições é mais simples que o padrão State completo; o padrão se paga quando *o comportamento*
(não só a transição) muda muito por estado. Na revisão, pergunte se valeu o padrão ou se a tabela
bastava. *Onde você reencontra:* o ciclo de vida de Pedido (era o Exercício 5 difícil do seu
roteiro de OOP!), o `acknowledged` dos alertas do SensorWatch, e qualquer workflow. É o mesmo
movimento que você treina no simulador de Pokémon — estados que mudam o que um Pokémon pode fazer.

---

### Exercício 10 — Command · Editor com Undo/Redo

**O smell que ele ataca:** a lógica de cada ação inline no lugar que a dispara, sem jeito uniforme
de desfazer, refazer, enfileirar ou logar. Cada ação nova precisa do seu próprio `undo` improvisado.

**Descrição do sistema:** um editor de texto (ou de grade) de console com operações: inserir,
apagar, mover o cursor, talvez substituir. O requisito que muda tudo: **undo e redo ilimitados**.
O usuário faz uma sequência de operações e pode desfazê-las uma a uma, e refazê-las. Começa com
inserir/apagar e undo simples; a evolução pede redo, depois operações novas (cada uma precisando
saber se desfazer), e por fim um histórico que registra tudo que aconteceu.

**A dor que deve aparecer:** sem encapsular cada ação, o undo vira um pesadelo de casos especiais,
e cada operação nova exige mexer na lógica de histórico.

**Escopo:** console, documento em memória. Foco em tratar cada ação como algo que sabe se executar
**e** se desfazer, com um histórico uniforme.

**Idioma C# moderno:** para casos simples, `Action`/delegates já encapsulam comportamento; o padrão
completo (objeto com `Execute`/`Undo`) brilha quando você precisa de undo, fila ou log uniforme.
*Onde você reencontra:* os Commands do CQRS/MediatR no SensorWatch são este padrão (sem o undo,
em geral) — uma requisição vira um objeto que um handler executa. Entender Command aqui deixa o
MediatR óbvio depois.

---

## Padrões para explorar depois (e alguns com ceticismo)

Disciplina de escopo: estes ficam de fora dos exercícios de propósito, mas vale saber onde se
encaixam.

- **Mediator** — não precisa exercitar isolado; você vai aprendê-lo na marra com o MediatR no
  SensorWatch. Faça o Command e o Observer primeiro; o Mediator vai cair sozinho.
- **Template Method** — útil, mas em C# moderno muitas vezes vira composição com `Func<>`/
  Strategy. Bom de conhecer, raro de precisar na forma clássica.
- **Facade / Proxy** — Facade é quase só "uma classe que simplifica um subsistema chato"; Proxy
  você já vai tocar de leve ao decorar com cache (Exercício 5) e com lazy loading do EF.
- **Iterator** — **já está embutido** no C#: `IEnumerable` + `yield return`. Não reimplemente.
- **Abstract Factory** — extensão do Factory (Exercício 2) para *famílias* de produtos. Suba pra
  ele só quando sentir a necessidade real de manter famílias coerentes.
- **Singleton** — cuidado. É o padrão mais mal usado do GoF. Em .NET, quase sempre o que você quer
  é registrar o serviço com lifetime Singleton no container de DI, **não** um `static Instance`
  acoplado. Conheça a armadilha mais do que o padrão.
- **Visitor** — poderoso e raro; deixe pra quando topar uma estrutura estável que precisa de
  operações sempre novas. Fácil de aplicar errado.

---

## Como progredir

- Faça **em ordem**. Os fáceis treinam o reflexo de separar o que varia; os difíceis assumem esse
  reflexo pronto.
- **Uma rodada por vez.** Nunca refatore na Rodada 1 — a dor precisa existir antes do remédio.
- Depois de cada exercício, releia a reflexão do anterior. O padrão dos *seus* erros (abstrair
  cedo, escolher a forma clássica quando o idioma moderno era melhor) é o mapa mais útil que você
  tem.
- Quando terminar os 10, faça uma rodada **às cegas**: pegue um exercício antigo, mude o domínio,
  e implemente sem decidir o padrão de antemão. Se o cheiro te levar à ferramenta certa sozinho,
  está enraizado.

---

## Checklist de reflexão (use em todos)

- Escrevi a versão concreta e ingênua **antes** de pensar no padrão?
- A dor que motivou o padrão **realmente apareceu**, ou eu forcei o padrão por dever de casa?
- O padrão **se pagou** — código mais fácil de estender — ou um `if`/`Func<>`/initializer simples
  teria bastado?
- Qual o **idioma C# moderno** equivalente (event, DI, delegate, `IEnumerable`, record)? Usei ele
  ou a forma clássica do livro? Por que essa escolha?
- Se um requisito novo plausível aparecesse amanhã, eu mexeria em **um** lugar ou em vários?
- Eu teria **reconhecido o cheiro** e chegado a este padrão se ninguém tivesse me dito o nome?

---

*Referência complementar: este roteiro acompanha o roteiro-exercicios-design-oop.md, o
roadmap-backend-csharp-azure.md e os projetos práticos. A prática conduz, a teoria acompanha.*

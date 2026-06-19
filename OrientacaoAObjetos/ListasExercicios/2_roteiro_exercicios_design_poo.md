# Roteiro de Exercícios — Prática de Design e Aplicação de OOP

> Documento-semente. Cada exercício é a **descrição de um sistema**, não a solução.
> Você alimenta a descrição (junto com o prompt-base abaixo) numa IA, ela transforma em um enunciado completo, e **você implementa**. A IA descreve o problema; o design é seu.

---

## Propósito

Fechar a distância entre *entender* composição/interfaces/polimorfismo e *aplicar* isso em código que parece de produção. O objetivo não é decorar padrões — é treinar o movimento que constrói julgamento: **escrever o concreto primeiro, deixar a abstração emergir, extrair no momento certo**.

Os cinco exercícios sobem de dificuldade de propósito, pra você atravessar a transição em degraus em vez de num salto.

---

## Princípios que valem para todos os exercícios

- **Concreto primeiro.** Faça a versão mais simples que funciona de ponta a ponta, mesmo feia. Só depois refatore.
- **Não arquitete tudo de cara.** Você ainda não entende o problema o suficiente pra projetá-lo — o entendimento vem de construir. Deixe o design emergir.
- **Regra de três / YAGNI.** Não crie abstração pra um caso só. Espere a variação aparecer de fato antes de extrair.
- **Extraia, não preveja.** A interface nasce de dentro do código que já funciona, não chutada no vácuo.
- **IA como revisora, não como arquiteta.** Use a IA pra gerar o enunciado e, no fim, criticar o *seu* design — nunca pra decidir a arquitetura por você.
- **Disciplina de escopo.** Cada exercício tem um limite explícito. Respeite-o. O ganho está no design, não no volume de funcionalidades.

---

## Como usar este roteiro

1. Escolha um exercício (comece pelo Fácil 1 e suba em ordem).
2. Copie o **Prompt-base** abaixo e cole a **Descrição do sistema** do exercício escolhido no lugar indicado.
3. Envie pra IA. Ela vai te devolver um enunciado completo: contexto, requisitos, regras de negócio, fatias de entrega e critérios de "pronto" — **sem código e sem arquitetura**.
4. Implemente sozinho, em C# console/biblioteca. Comece pela fatia mais simples e vá crescendo.
5. Quando terminar, mande sua implementação de volta pra IA e peça o **modo revisor**: onde você abstraiu cedo demais, onde duplicou sem perceber, onde herança deveria ter sido composição.
6. Anote o que aprendeu (seu `DUVIDAS.md`): que decisão de design você tomou, o que rejeitou e por quê.

---

## Prompt-base

> Copie tudo abaixo e cole a descrição do exercício no final, onde está indicado.

```
Você é um tech lead me passando a especificação de um módulo para eu implementar sozinho.
Vou te dar a descrição de um sistema. Sua tarefa é transformá-la em um enunciado de
exercício completo e realista.

Produza, nesta ordem:
1. Contexto de negócio — o cenário real, quem usa, qual problema resolve.
2. Requisitos funcionais — o que o módulo precisa fazer, em linguagem de produto.
3. Regras de negócio e casos de borda — inclusive os chatos, os que costumam passar batido.
4. Fatias de entrega sugeridas — uma sequência de fatias verticais pequenas, da mais
   simples à mais completa, para eu construir de forma incremental. A primeira deve ser a
   coisa mais simples que funciona de ponta a ponta.
5. Critérios de "pronto" — checklist objetivo de quando o exercício está concluído.
6. Checklist de reflexão pós-implementação — perguntas para eu me avaliar depois (onde
   abstraí cedo demais? onde faltou uma costura? onde herança/composição doeu?).

Restrições obrigatórias (não quebre nenhuma):
- NÃO escreva código de nenhum tipo.
- NÃO proponha arquitetura, diagrama de classes, interfaces, nem nomes de padrões de
  projeto. As decisões de design são MINHAS — o objetivo do exercício é eu descobrir
  onde as abstrações precisam aparecer.
- NÃO diga "use Strategy aqui" ou "extraia uma interface ali". Descreva o problema, não
  a solução.
- Mantenha o escopo enxuto: console/biblioteca em C# .NET, sem banco, sem UI, sem rede.
  Dados em memória ou hardcoded bastam.
- Respeite o escopo definido na descrição — não adicione funcionalidades além do
  necessário para exercitar o aprendizado.

Quando eu terminar e te enviar minha implementação, troque para o modo revisor: critique
meu design com honestidade — onde abstraí cedo demais, onde dupliquei sem perceber, onde
uma costura ficou no lugar errado, onde herança deveria ser composição. Não reescreva por
mim; aponte e explique.

Descrição do sistema:
[COLE AQUI A DESCRIÇÃO DO EXERCÍCIO]
```

---

# Os Exercícios

## Nível Fácil

### Exercício 1 — Central de Notificações (multi-canal)

**Contexto:** quase todo sistema de produção precisa avisar usuários sobre eventos — confirmação de cadastro, redefinição de senha, aviso de cobrança. No começo, manda só e-mail. Com o tempo o produto pede SMS, depois push, depois talvez um webhook pra integrar com outro sistema.

**Descrição do sistema:** um módulo que recebe uma notificação (destinatário, assunto, conteúdo, tipo de evento) e a entrega. Começa com um único canal. A evolução do exercício introduz novos canais, cada um com suas particularidades: e-mail tem assunto e corpo; SMS tem limite de caracteres; push tem título curto e um payload; cada canal entrega de um jeito diferente e pode falhar de um jeito diferente. O módulo precisa registrar o resultado de cada envio (sucesso/falha) e permitir escolher o canal conforme o tipo de evento ou a preferência do usuário.

**Escopo:** console. O "envio" pode ser apenas um log no terminal simulando a entrega — sem provedores reais, sem rede. Foco em como o módulo lida com vários canais e cresce quando um novo aparece.

---

### Exercício 2 — Calculadora de Descontos do Carrinho

**Contexto:** e-commerce. No checkout, o valor final depende de regras de desconto que o marketing inventa o tempo todo: cupom percentual, cupom de valor fixo, "leve 3 pague 2", desconto de primeira compra, frete grátis acima de um valor. As regras mudam e se acumulam.

**Descrição do sistema:** um módulo que recebe um carrinho (itens com preço e quantidade) e um conjunto de descontos aplicáveis, e calcula o valor final. Começa com um ou dois tipos simples. A evolução adiciona novos tipos, regras de combinação (alguns descontos não acumulam), ordem de aplicação (percentual antes ou depois do fixo?) e limites (desconto máximo). O resultado precisa ser auditável: saber quais descontos foram aplicados e quanto cada um abateu.

**Escopo:** biblioteca/console, tudo em memória, sem persistência. Foco em como o cálculo absorve novos tipos de desconto sem virar um emaranhado de condicionais.

---

## Nível Médio

### Exercício 3 — Pipeline de Importação de Arquivos

**Contexto:** sistemas de produção vivem importando dados de fora — planilhas de fornecedores, exportações de outros sistemas, integrações. Os arquivos chegam em formatos diferentes (CSV, JSON, às vezes um XML legado), precisam ser lidos, validados, normalizados pro modelo interno e então processados.

**Descrição do sistema:** um módulo que recebe um arquivo, identifica ou recebe o formato, extrai os registros, valida cada um (campos obrigatórios, tipos, faixas válidas, duplicatas), normaliza pro modelo interno e devolve um relatório (quantos importados, quantos rejeitados e por quê). Começa com um formato e validações simples. A evolução adiciona novos formatos, novas regras de validação que variam conforme o tipo de dado, e a necessidade de continuar processando mesmo quando alguns registros falham — não pode abortar tudo por causa de uma linha ruim.

**Escopo:** console, arquivos pequenos (strings ou arquivos locais). Sem banco — "importar" pode ser transformar numa lista em memória e imprimir o relatório. Foco em como as etapas (ler → validar → normalizar) e suas variações se organizam sem acoplar tudo.

---

### Exercício 4 — Sistema de Reservas de Recursos

**Contexto:** pense em reserva de salas de reunião, equipamentos de uma fábrica ou consultórios — qualquer recurso compartilhado com agenda. O sistema precisa evitar conflitos, respeitar regras de disponibilidade e lidar com tipos de recurso que têm regras diferentes.

**Descrição do sistema:** um módulo que gerencia recursos e suas reservas num intervalo de tempo. Precisa impedir reservas sobrepostas pro mesmo recurso, respeitar horário de funcionamento, antecedência mínima/máxima, duração máxima, e regras que variam por tipo de recurso — uma sala pode ser reservada por qualquer um; um equipamento crítico só por usuários autorizados; alguns recursos exigem intervalo de limpeza entre reservas. Precisa responder "esse horário está livre?" e "quais horários estão livres nesse dia?". Começa com um tipo de recurso e regras simples; a evolução introduz novos tipos e regras que se combinam.

**Escopo:** console, dados em memória, sem calendário externo. Foco em como as diferentes regras de disponibilidade convivem sem que cada novo tipo de recurso vire mais um `if` espalhado pelo código.

---

## Nível Difícil

### Exercício 5 — Orquestrador de Processamento de Pedidos

**Contexto:** o coração de qualquer e-commerce ou logística. Quando um pedido é confirmado, uma sequência de coisas precisa acontecer: reservar estoque, cobrar o pagamento, agendar o envio, notificar o cliente. Cada etapa pode falhar, cada etapa pode demorar, e o pedido passa por estados ao longo do caminho. Quando algo falha no meio, o que já foi feito pode precisar ser desfeito ou repetido.

**Descrição do sistema:** um módulo que recebe um pedido confirmado e o conduz por um fluxo de etapas até a conclusão (ou falha). O pedido tem um ciclo de vida com estados bem definidos e transições válidas — não dá pra "enviar" um pedido cujo pagamento falhou. Cada etapa pode ter sucesso ou falha; falhas podem ser temporárias (vale tentar de novo) ou definitivas (precisa reverter o que já foi feito e marcar o pedido como falho). Conforme o pedido avança, outras partes do sistema precisam reagir aos acontecimentos — quando o pagamento é aprovado, dispara a notificação; quando o estoque é reservado, atualiza um painel — sem que a etapa principal precise conhecer todos esses interessados. O sistema precisa registrar o histórico do que aconteceu com cada pedido.

**Por que é o mais difícil:** tem várias dimensões variando ao mesmo tempo (etapas, estados, tipos de falha, reações a eventos) e é grande o suficiente pra você **não** conseguir projetar tudo de cara. Você vai precisar construir uma fatia mínima — um pedido feliz, do início ao fim, sem nenhuma falha — e fazer o resto emergir a partir dela. É o exercício onde resistir à tentação de arquitetar tudo antes vai ser mais difícil, e mais importante.

**Escopo:** console. Estoque, pagamento e envio são simulados — podem só imprimir e retornar sucesso/falha conforme um cenário que você controla. Sem filas reais, sem banco. Mas guarda este detalhe: é exatamente o tipo de domínio que mais à frente vira mensageria + eventos de verdade no seu SensorWatch. Aqui você treina o desenho; lá você liga na infra.

---

## Como progredir

- Faça **em ordem**. Cada nível assume o reflexo que o anterior treinou.
- Faça **uma fatia por vez**. Nunca pule pra próxima sem a anterior funcionando.
- Entre um exercício e outro, releia sua reflexão do anterior. O padrão dos seus próprios erros é o mapa mais útil que você vai ter.
- Se quiser um aquecimento sem pressão antes do Fácil 1, o simulador de Pokémon serve: dois Pokémon, um golpe, código feio funcionando, depois refatorar. É o mesmo movimento em terreno divertido.

---

## Checklist de reflexão (use em todos)

- Eu escrevi a versão concreta antes de pensar em abstração?
- Onde eu criei uma interface/abstração que **não** se pagou? (abstração prematura)
- Onde eu **dupliquei** código sem perceber, e quando ficou claro que dava pra extrair?
- Alguma costura ficou no lugar errado — separei o que andava junto ou juntei o que variava separado?
- Usei herança onde composição teria sido mais simples?
- Se um requisito novo plausível aparecesse amanhã, onde eu teria que mexer? Em um lugar ou em vários?

---

*Referência complementar: este roteiro acompanha o roadmap-backend-csharp-azure.md e os projetos práticos. A prática conduz, a teoria acompanha.*

### Strategy Pattern

Consegui realizar o principal do exercicio bem, porém com algumas abstrações engessadas e utilização do padrão não tão eficaz.

Acertos: 
- Uso do Strategy, cada implementação é um contrato separado
- Implementação de casos especiais de custo tratados com sucesso (meses de maior custo em casos de calculo de frete)
- Momento da aplicação
- Separação física em pastas

Erros:
- Falha na abstração de um contrato, faltou um digito no CPF a ser considerado
- Campos obsoleto no projeto (\_ValorPedido) - ficou de resíduo devido a troca de arquitetura, em que substitui o retorno do pedido inteiro por apenas o float resultado
- uso de **float** para dinheiro
- Função **VerificaCEP()** não verifica nulos (pode quebrar)
- Violação de **Naming** - Uso de underscore ( \_ ) em propriedades públicas violando a convenção do C#. 

Melhorias potenciais no exercício
- remover o **ContextStrategyFrete** - trata de algo muito engessado do livro de padrões e sua implementação não agrega valor suficiente para ser necessária. Uma chamada simples poderia resolver o problema diretamente
- Uso de Dictionary<Transportadora, IStrategyFrete> mataria o uso de switch e ganharia em dinamicidade
- LINQ (minBy) no uso de Testar todos os fretes e escolher o menor reduziria o atrito e blocos de declarações
- Avaliar Func<Pedido, decimal> no lugar de classe-por-formula.
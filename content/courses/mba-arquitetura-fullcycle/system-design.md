## Requisitos não funcionais

Não dizem respeito a funcionalidades, mas sim a atributos do sistema: Disponibilidade, aguentar uma quantidade X de usuários simultaneamente, etc.

Teorema CAP - Balanceamento entre Consistency/Availability/Partition tolerance. Basicamente, você escolhe dois desses e abre mão do terceiro. Tolerância de partição é a capacidade de um sistema distribuído tolerar uma falha na rede que o separe em duas ou mais partições isoladas

Você precisa ter dados sobre a solução. Exemplo:
- Quantos DAU (Daily Active Users) são esperados?
- Destes, quantos vão parar na home e quantos vão até o checkout?
- Qual a taxa de conversão?
- Quantos requests vão ocorrer por usuário?
- Quanto de dados será trafegado? 

Estes dados podem vir de um sistema anterior, um caso de uso semelhante, ou serem estimativas. No fim das contas sempre vai haver algum nível de estimativa, mas ter dados proximos da realidade é importante para ajudar a dimensionar o hardware necessario para rodar a solução, qual a latencia esse hardware vai alcançar, custos, etc.

## Planos de capacidade

Mostra qual banda o sistema irá consumir diariamente, ao longo de um ano, cinco anos, etc. Idem para storage. Quanto de processamento será necessário, etc.

Sugestão, trabalhar com notação cientifica para facilitar a leitura e cálculos de cabeça. Exemplo: Ao invés de dizer que tenho 1.000.000 requisições, eu tenho 10^6.

### Requests por segundo

Se eu tenho o DAU e a quantidade de requests por usuário, é fácil calcular o total de requests, mas e por segundo?

rps = req-por-dia / segundos-por-dia

A rigor você dividiria por 24*60*60 = 86.400 segundos por dia, mas numa conversa com cliente ou numa entrevista é mais importante velocidade de cálculo que precisão, então é melhor considerar por exemplo 100.000 segundos/dia, ou 10^5

Assim, se eu tenho digamos 10^6 requisições por segundo, é fácil calcular que eu tenho 10^6/10^5 ou 10^1 = 10 requisições por segundo

### Compras por segundo

De forma semelhante, sabendo a taxa de conversão e o DAU, eu consigo calcular compras por dia e dividindo por 10^5 chego em compras/segundo

### Bandwidth

Tendo os requests/segundo e o tamanho dos requests (em kb) eu consigo estimar o consumo de banda por segundo

### Storage

Demanda de storage por segundo = requests-por-segundo (para escrita) * request size

Se trabalhar com replicação, multiplicar por um fator de replicação

À partir daí eu consigo calcular por dia, por mês, por ano, etc.

Para converter um valor de "por segundo" para "por ano", multiplicar por (10⁵ * 365) ou (10⁵ * 3,65*10²) ou 3,65 * 10⁷

Para "por 5 anos", multiplicar por (5 * 3,65 * 10⁷) ou 18,25 * 10⁷, ou 1,8 * 10⁸, ou arredondando novamente 2 * 10⁸

Lembre-se, estamos arredondando para facilitar os cáclulos. É só uma estimativa, e está tudo bem.

## Premissas

Pressupostos que guiarão o design.

Exemplo:
- Só aceita cartão de crédito
- A compra precisa ser confirmada imediatamente
- O que vale mais: Consistencia, disponibilidade..? Lembrar teorema CAP
- 
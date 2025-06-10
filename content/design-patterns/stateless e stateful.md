Aplicação stateful armazena estado (logs, sessões, etc) localmente, problemas:
- quando a aplicação escala para cima, novas instancias não possuem estes dados
- quando a aplicação é escalada para baixo, estes dados são perdidos
- diferentes instancias não possuem acesso ao mesmo estado

Por conta disso é preferivel que aplicação não armazene localmente nenhum estado que precise ser mantido.
Entretnato, tudo bem armazenar estado efêmero, como um cache, coisas que podem ser descartadas sem impacto.
---
title: "Intensivo Domain Driven Design (DDD): Os 3 pilares que você precisa saber"
externalLink: "https://www.youtube.com/watch?v=vFZkOyaPK4E&t=864s"
---
- Não é sobre código

# A idéia principal

Atacar a complexidade no coração do software. O coração do software é o domínio

Para aplicações mais simples isso não é nada, pois não há complexidade. Já em sistemas maiores, você tem você tem pessoas diferentes, linguas diferentes, sistemas diferentes interagindo e isso traz complexidade.

# Primeiro pilar: Linguagem universal

Diferentes setores da organização tem diferentes formas de falar, pensar e agir. Cada setor pode ter sua própria linguagem inclusive utilizando as mesmas palavras para falar de coisas diferentes. O sistema não pode interferir nisso e forçar uma outra linguagem.

Ele deu exemplo do seu pai que era bancário e tinha um relatório de pagamentos chamado "francesinha". Se o sistema passar a chamar isso de "relatório de pagamentos" ou algo assim provocaria rejeição e dificuldades de uso por parte dos usuários. 

Também deu exemplo de uma escola onde para o setor de vendas o "cliente" é um aluno enquanto para o setor de B2B o "cliente" é uma empresa.

Essa linguagem é a linguagem universal e deve ser respeitada

# Segundo pilar: Visão estratégica

A razão de existir de uma empresa é o seu domínio. Para a netflix, seu domínio é fornecer vídeos. Para uma escola, são cursos.

Além deste core domain, compõem o domínio áreas auxiliares como por exemplo financeiro, rh, etc. Para facilitar o design e análise, dividimos o dominio em subdomínios, que originam os "bounded contexts", ou "contextos delimitados". Estes subdomínios podem ter cada um uma linguagem diferente, que deve ser respeitada.

Existem conceitos que claramente pertencem a um subdomínio, e outros que se comunicam com mais de um, esta é a chamada zone cinzenta

![Exemplo de zona cinzenta](https://martinfowler.com/bliki/images/boundedContext/sketch.png)
[(Fonte)](https://martinfowler.com/bliki/BoundedContext.html)

No exemplo acima temos Customer e Product transitando entre o contexto de vendas e o de suporte.

Alguns subdominios são chamados "genéricos": São como commodities que podem ser delegados para sistemas de terceiros e que podem ser trocados por qualquer implementação sem impactos no negócio, mas para abstrair detalhes do fornecedor ou impedir que a implementação do core domain seja poluída com particularidades de sistemas externos, ou para adequar estes sistemas à sua linguagem universal, você pode utilizar uma ACL: Anti Corruption Layer

# Terceiro pilar: Visão tática

Aqui sim lidamos com detalhes mais técnicos. Como efetivamente implementar cada contexto.

- Complexidade do negócio: Fórmulas de cálculo de juros, fórmulas de cálculo de preços, regras de negócio
- Complexidade ocasional/técnica: É o lado do dev; Qual linguagem/framework/banco de dados/api/etc

Estas complexidades não devem se misturar, de forma que podemos alterar uma coisa ou outra sem que interfira na outra.


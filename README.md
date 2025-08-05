## Contextualização do Problema e Definição dos Objetivos

O projeto simula uma situação real em que uma empresa de serviços financeiros utiliza Inteligência Artificial (IA) para avaliar o risco de crédito de seus clientes. Apesar de o modelo atingir bons índices de acurácia, surgem dúvidas por parte de gerentes, clientes e órgãos reguladores:

Como explicar de forma clara por que um cliente teve crédito aprovado ou negado?

Neste trabalho, a missão foi utilizar um modelo preditivo para classificar clientes em bom ou mau risco de crédito e aplicar a técnica de IA Explicável (XAI) com a biblioteca LIME, a fim de tornar as decisões do modelo compreensíveis para todos os envolvidos.

## Modelo Preditivo Utilizado 

Para resolver o desafio, utilizei o conjunto de dados Statlog (German Credit Data), amplamente utilizado em pesquisas relacionadas a risco de crédito. Ele contém 1.000 registros e 20 atributos numéricos, incluindo:
 - Duração do crédito
 - Valor solicitado
 - Histórico de crédito
 - Saldo bancário
 - Tempo de residência
 - Idade, entre outros.

O modelo escolhido foi o Random Forest Classifier, uma técnica de aprendizado supervisionado robusta e bastante utilizada para problemas de classificação. Após separar os dados em treino e teste (80% / 20%), o modelo obteve uma acurácia de 69,5%, o que já indica um desempenho razoável.

## Discussão Interpretativa com LIME 

Após treinar o modelo, utilizei a biblioteca LIME para explicar previsões individuais.
Na explicação de uma das amostras (cliente nº 10 do conjunto de teste), o modelo previu que o cliente era bom pagador com 70% de probabilidade.
O LIME apontou as principais variáveis que influenciaram a decisão:

Variáveis que influenciaram positivamente a aprovação do crédito: 
- checking_status <= 1.00 - Idicando que o cliente tem saldo bancário 
- duration > 3 meses - Tempo razoável para crédito
- residence_since <= 1.00 - Tempo de residência curto, mas aceitável
- purpose <= 3.00 - Propósito do empréstimo mais conservador
- job <= 0.00 - Categoria de trabalho de menor risco

Variáveis neutras ou com influência:
- credit_amount = 1.00
- property = 0.00
- number_credits = 0.00
- age = 0.00

Essas explicações tornaram a decisão do modelo mais transparente, interpretável e confiável. 

Reflexão sobre Limitações e Importância da Interpretabilidade:

O LIME mostrou ser uma ferramenta poderosa para: 
- Justificar por que um cliente teve crédito aprovado ou negado
- Reduzir desconfianças sobre a IA
- Apoiar decisões mais transparentes com foco em ética e compliance
- Aumentar a confiança do cliente final na tecnologia

Entretanto, o LIME é uma técnica local, ou seja, ele explica apenas uma decisão por vez. Isso significa que pequenas mudanças nos dados podem gerar variações nas explicações. Além disso, ele não revela a lógica geral do modelo, apenas a influência pontual de variáveis.
Mesmo assim, é uma ferramenta extremamente útil e acessível, especialmente em contextos em que a transparência da IA é essencial, como no setor financeiro.

## Conclusão 

Este trabalho demonstrou na prática como é possível construir um modelo de machine learning funcional e, ao mesmo tempo, explicável.
A aplicação do LIME permitiu interpretar decisões que, até então, eram vistas como uma “caixa preta”, oferecendo mais confiança, ética e transparência nas previsões.

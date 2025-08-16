Crédito Explicável com LIME (XAI) — German Credit Data

Contextualização do Problema e Definição dos Objetivos

Em cenários reais de serviços financeiros, modelos de IA ajudam a avaliar risco de crédito e decidir aprovar ou negar propostas. Porém, mesmo com boa performance, surgem dúvidas legítimas de gerentes, clientes e reguladores:

Por que este cliente foi aprovado e aquele não?

Quais fatores mais pesaram na decisão?

A decisão está alinhada a critérios de ética, transparência e compliance?

Objetivo deste trabalho: construir um pipeline que classifique clientes quanto ao risco de crédito e, sobretudo, explique cada decisão de forma clara com XAI (LIME) — tornando as previsões auditáveis e compreensíveis para todas as partes.

Dados e Preparação

O dataset utilizado foi o Statlog (German Credit Data - UCI), amplamente reconhecido em pesquisas de risco de crédito.
Para facilitar a interpretabilidade e alinhar com o vocabulário de negócios, os atributos foram padronizados e transformados em 6 variáveis-chave:

Renda_Mensal → aproxima a capacidade de pagamento.

Score_Credito (0–1000) → proxy construída a partir de diferentes sinais (status, poupança, histórico, tempo de emprego).

Endividamento_% → grau de comprometimento mensal estimado.

Tempo_Emprego (meses) → estabilidade de renda e vínculo profissional.

Historico_Inadimplencia (0/1) → registro de inadimplência anterior.

Valor_vs_Renda → esforço do valor solicitado em relação à renda mensal.

A variável-alvo foi Aprovado (1/0), indicando o risco de crédito.
Essa engenharia de atributos permitiu que o modelo trabalhasse com variáveis autoexplicativas, aproximando a saída técnica do modelo às políticas usuais de crédito.

Modelo Preditivo Utilizado

O modelo escolhido foi o Random Forest Classifier, implementado dentro de um Pipeline (StandardScaler → RandomForest).

Motivos da escolha:

Robusto para dados tabulares e relações não-lineares.

Estável diante de outliers.

Capaz de fornecer probabilidades, úteis para análise de risco.

A base foi dividida em treino/teste via train_test_split (hold-out).
O desempenho foi avaliado por:

- Acurácia

- Precisão

- Recall

- Score

Matriz de Confusão (salva em outputs/confusion_matrix.png)

Essas métricas permitiram analisar os erros por classe (falsos positivos e falsos negativos), fundamentais para calibrar políticas de aprovação.

Discussão Interpretativa com LIME (XAI)

Após o treino do modelo, aplicamos o LIME Tabular para gerar explicações individuais.
O objetivo foi identificar, cliente a cliente, quais variáveis puxaram a decisão para aprovação ou negação.

🔹 Variáveis associadas à aprovação:

Score_Credito alto

Endividamento_% baixo

Tempo_Emprego elevado

Historico_Inadimplencia = 0

Valor_vs_Renda menor

🔸 Variáveis associadas à negação:

- Score_Credito baixo

- Endividamento_% alto

- Tempo_Emprego curto

- Historico_Inadimplencia = 1

- Valor_vs_Renda elevado

Os gráficos do LIME, salvos em outputs/lime_*.png, evidenciam visualmente a influência de cada variável.
Isso tornou o processo transparente e auditável, permitindo explicar decisões para clientes e reguladores de forma clara.

Simulações de Prazos (Sensibilidade Risco × Parcela)

Para aproximar ainda mais da realidade do mercado, implementamos simulações de prazos (6, 12, 18, 24, 36, 48 e 60 meses).

O fluxo foi:

Calcular a parcela estimada para cada prazo.

Atualizar o Endividamento_% do cliente.

Recalcular a probabilidade de aprovação pelo modelo.

➡️ Essa abordagem revelou casos borderline, em que o risco muda conforme o prazo:

prazos maiores → parcelas menores → endividamento reduzido → maior chance de aprovação.

Isso permite justificar contrapropostas (ex.: negar no prazo curto, mas aprovar no longo), agregando valor prático e estratégico ao modelo.

Reflexões sobre Limitações e Importância da Interpretabilidade

Embora o projeto tenha atingido bons resultados, algumas limitações devem ser destacadas:

O LIME fornece explicações locais (por cliente), mas não substitui análises globais.

As explicações são aproximações: dependem de perturbações sintéticas no espaço de dados.

Modelos complexos como Random Forest podem ter relações ocultas que o LIME simplifica.

##Importância da interpretabilidade:

Atende às demandas de compliance e órgãos reguladores.

Gera confiança para gestores de risco e clientes finais.

Evita que o modelo seja visto como “caixa-preta”.

Neste projeto, o uso do LIME mostrou-se fundamental para validar se as variáveis utilizadas eram coerentes com práticas de crédito e para garantir transparência nas decisões.

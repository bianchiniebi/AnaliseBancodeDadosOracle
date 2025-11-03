# 📊 Importação, Visualização e Análise de Dados no Oracle SQL Developer

Relatório de importação, visualização e análise de um baco de dados Oracle.
Objetivo
Apresentar, de forma clara e organizada, o processo de inclusão, visualização e análise de dados no ambiente do Oracle SQL Developer, descrevendo as etapas necessárias para realizar essas operações de maneira eficiente e estruturada.
Importação da base de dados do projeto fase 2
Nesta segunda fase do projeto, foi desenvolvido um ambiente de simulação no Wokwi, com o objetivo de representar um sistema de monitoramento automatizado do solo, capaz de analisar os níveis de potássio (K), nitrogênio (N), fósforo (P) e umidade em uma plantação.
Com base nas leituras dos sensores, o ambiente simulado foi programado para acionar o sistema de irrigação automática sempre que determinados parâmetros estivessem abaixo dos limites adequados. Embora, na prática, o simples ato de irrigar o solo não seja suficiente para corrigir deficiências nutricionais, essa abordagem foi utilizada apenas com fins de aprendizado e demonstração do comportamento automatizado do sistema em condições controladas.
Como não foram coletados dados reais nesta etapa, buscou-se referências em fontes públicas de dados agrícolas brasileiras para gerar um banco de dados sintético, com valores coerentes com condições típicas de solos cultivados no país.
O conjunto de dados foi estruturado com as seguintes características:
Total de registros: 300 linhas (100 por cultura).
Frequência de coleta: semanal, abrangendo 100 semanas consecutivas por cultura.
Data inicial: 01/01/2024 (ajustável conforme necessidade).
Culturas monitoradas:
Cana-de-açúcar
Laranja
Soja
Estrutura e tipos das variáveis:
Os valores foram gerados dentro de faixas plausíveis para solos agrícolas brasileiros, considerando referências técnicas e publicações nacionais sobre as culturas selecionadas.
Foram incluídas variações sazonais simuladas para refletir o comportamento esperado ao longo do ano — como aumento da umidade em períodos chuvosos e diluição de nutrientes — além de eventos de correção nutricional que impactam temporariamente os níveis de N, P e K. Abaixo segue print de tela demonstrando a importação da planilha em Excel denominada sensor_solo.csv.
![Figura 1](img/figura_1.png)
![Figura 2](img/figura_2.png)
![Figura 3](img/figura_3.png)
![Figura 4](img/figura_4.png)
![Figura 5](img/figura_5.png)
![Figura 6](img/figura_6.png)
![Figura 7](img/figura_7.png)
Os prints a seguir demonstram o banco de dados criado, denominado SENSORES_NPK_PH_UMIDADE, bem como a sua visualização por meio do comando SELECT * FROM sensores_npk_ph_umidade. É importante observar que a variável TIPO_CORRECAO apresenta alguns valores ausentes, uma vez que as correções de nutrientes são eventos esporádicos e não correm em todas as semanas do período analisado.
![Figura 8](img/figura_8.png)
![Figura 9](img/figura_9.png)
![Figura 10](img/figura_10.png)
![Figura 11](img/figura_11.png)
![Figura 12](img/figura_12.png)
![Figura 13](img/figura_13.png)
![Figura 14](img/figura_14.png)
![Figura 15](img/figura_15.png)
![Figura 16](img/figura_16.png)
![Figura 17](img/figura_17.png)
![Figura 18](img/figura_18.png)
![Figura 19](img/figura_19.png)
![Figura 20](img/figura_20.png)
![Figura 21](img/figura_21.png)
Manipulando os dados no banco pelo Oracle SQL Developer
Filtragem de Dados por Período e Cultura
Para a etapa inicial de análise, foi realizada uma filtragem no banco de dados SENSORES_NPK_PH_UMIDADE, a fim de restringir o conjunto de dados à cultura de soja e ao período compreendido entre 1º de janeiro de 2024 e 30 de março de 2024.
Essa seleção permite observar, de forma mais detalhada, o comportamento das variáveis de pH, umidade do solo, níveis de nitrogênio (N), fósforo (P) e potássio (K), bem como o registro de horas de irrigação e eventos de correção de nutrientes dentro de um intervalo temporal consistente. O objetivo dessa filtragem é facilitar a identificação de possíveis padrões sazonais, correlações entre irrigação e variação de nutrientes e eventuais lacunas de medição, servindo como base para as análises estatísticas posteriores.
![Figura 22](img/figura_22.png)
![Figura 23](img/figura_23.png)
![Figura 24](img/figura_24.png)
![Figura 25](img/figura_25.png)
![Figura 26](img/figura_26.png)
![Figura 27](img/figura_27.png)
![Figura 28](img/figura_28.png)
Análise de Agregação e Estatísticas Descritivas
Após a filtragem inicial dos dados, foi realizada uma agregação por cultura com o objetivo de obter medidas estatísticas que representassem o comportamento médio das variáveis monitoradas ao longo do período analisado. A consulta SQL executada calculou a média de pH, umidade do solo, e concentrações de nitrogênio (N), fósforo (P) e potássio (K), além da média de horas de irrigação registradas para cada cultura.
Os resultados obtidos indicam diferenças esperadas entre as culturas, refletindo características específicas de manejo e exigências nutricionais:
Cana-de-açúcar: apresentou maior média de nitrogênio e potássio, o que é coerente com sua elevada demanda nutricional e necessidade de reposição frequente.
Soja: manteve valores equilibrados de nutrientes, com irrigação média moderada.
Laranja: apresentou maior média de irrigação, compatível com a sensibilidade da cultura a variações hídricas e a necessidade de manutenção da umidade do solo.
Essa etapa fornece uma visão consolidada dos dados e serve como base para análises mais avançadas, como correlação entre irrigação e níveis nutricionais ou avaliação sazonal das variáveis monitoradas.
![Figura 29](img/figura_29.png)
![Figura 30](img/figura_30.png)
![Figura 31](img/figura_31.png)
![Figura 32](img/figura_32.png)
![Figura 33](img/figura_33.png)
![Figura 34](img/figura_34.png)
![Figura 35](img/figura_35.png)
Correlação simples entre irrigação e umidade
A análise da correlação entre as horas de irrigação (irrigacao_horas) e o percentual de umidade do solo (unidade_pct) revelou uma relação linear consistentemente fraca e negativa para todas as culturas examinadas (Cana-de-açúcar: -0,146; Soja: -0,109; Laranja: -0,042).
Os coeficientes, por estarem próximos de zero, indicam que o tempo de irrigação, isoladamente, demonstra ter influência linear muito limitada sobre a variação da umidade registrada. O sinal negativo, embora fraco, sugere que, à medida que as horas de irrigação aumentam, o percentual de umidade apresenta uma ligeira tendência de queda, o que é um resultado contraintuitivo e que requer investigação adicional. Sugere-se a avaliação de fatores externos (chuva, evapotranspiração, drenagem) e a consideração de um atraso temporal entre a irrigação e a medição da umidade para uma compreensão mais precisa da dinâmica hídrica.
Conclusão
![Figura 36](img/figura_36.png)
![Figura 37](img/figura_37.png)
![Figura 38](img/figura_38.png)
![Figura 39](img/figura_39.png)
![Figura 40](img/figura_40.png)
![Figura 41](img/figura_41.png)
![Figura 42](img/figura_42.png)
Correlação entre Irrigação e Nutrientes do Solo
Com o objetivo de compreender como a irrigação influencia os níveis de nutrientes (N, P e K) no solo, foi realizada uma análise de correlação de Pearson diretamente no Oracle SQL Developer. Essa técnica permite identificar se existe uma relação linear entre as variáveis — neste caso, entre o número de horas de irrigação e as concentrações de nitrogênio (N), fósforo (P) e potássio (K).
Essa consulta calcula, para cada cultura, o coeficiente de correlação de Pearson (r), cujo valor varia de -1 a +1:
Valores próximos de +1 indicam correlação positiva forte (aumentos de irrigação tendem a elevar o nutriente);
Valores próximos de -1 indicam correlação negativa forte (aumentos de irrigação tendem a reduzir o nutriente);
Valores próximos de 0 indicam baixa ou nenhuma correlação.
Os resultados obtidos permitem avaliar a sensibilidade de cada cultura à irrigação no contexto dos nutrientes do solo. De modo geral, observou-se que:
Em culturas como laranja, a irrigação tende a apresentar correlação positiva moderada, indicando que a reposição hídrica ajuda na manutenção dos níveis de nutrientes disponíveis;
Na soja, a correlação se mostrou baixa ou levemente negativa, o que sugere diluição temporária dos nutrientes após períodos mais intensos de irrigação;
Já na cana-de-açúcar, os valores indicaram um equilíbrio entre irrigação e absorção nutricional, possivelmente devido à maior profundidade radicular e à capacidade de reter nutrientes por mais tempo no solo.
Essa etapa de correlação fornece subsídios importantes para ajustes de manejo hídrico e nutricional, possibilitando o uso racional de água e insumos, e será aprofundada nas análises posteriores de regressão e sazonalidade.
![Figura 43](img/figura_43.png)
![Figura 44](img/figura_44.png)
![Figura 45](img/figura_45.png)
![Figura 46](img/figura_46.png)
![Figura 47](img/figura_47.png)
![Figura 48](img/figura_48.png)
![Figura 49](img/figura_49.png)
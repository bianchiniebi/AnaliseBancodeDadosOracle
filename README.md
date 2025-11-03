# 📊 Importação, Visualização e Análise de Dados no Oracle SQL Developer

## 🧭 Objetivo

Apresentar, de forma clara e organizada, o processo de inclusão, visualização e análise de dados no ambiente do **Oracle SQL Developer**, descrevendo as etapas necessárias para realizar essas operações de maneira eficiente e estruturada.

---

## 🌱 Contexto do Projeto

Na **fase 2** do projeto, foi desenvolvido um ambiente de simulação no **Wokwi**, representando um sistema de **monitoramento automatizado do solo**.
Esse sistema analisa os níveis de **potássio (K)**, **nitrogênio (N)**, **fósforo (P)** e **umidade** em uma plantação.

Com base nas leituras dos sensores, o sistema foi programado para acionar automaticamente a irrigação sempre que determinados parâmetros estivessem abaixo dos limites adequados.
Embora simplificado, o modelo serve como demonstração do comportamento automatizado em condições controladas.

---

## 🗂️ Estrutura do Banco de Dados

| Coluna              | Tipo         | Descrição                                         |
| ------------------- | ------------ | ------------------------------------------------- |
| `id`                | INTEGER      | Identificador único autoincremental               |
| `cultura`           | VARCHAR      | Tipo de cultura agrícola                          |
| `data`              | DATE         | Data da leitura semanal                           |
| `ph`                | NUMERIC(3,2) | pH do solo                                        |
| `umidade_pct`       | NUMERIC(5,2) | Umidade do solo (%)                               |
| `n_mgkg`            | NUMERIC(7,2) | Nitrogênio (mg/kg)                                |
| `p_mgkg`            | NUMERIC(7,2) | Fósforo (mg/kg)                                   |
| `k_mgkg`            | NUMERIC(7,2) | Potássio (mg/kg)                                  |
| `correcao_aplicada` | VARCHAR(1)   | Indica se houve correção nutricional (“S” ou “N”) |
| `irrigacao_horas`   | NUMERIC(5,2) | Total de horas de irrigação na semana             |

**Resumo do dataset:**

* 300 registros (100 por cultura)
* Período: 100 semanas consecutivas, iniciando em 01/01/2024
* Culturas monitoradas: **Cana-de-açúcar**, **Laranja**, **Soja**

Os valores foram gerados dentro de faixas plausíveis para solos agrícolas brasileiros, com **variações sazonais simuladas** (umidade, nutrientes, correções nutricionais, etc.).

---

## 🧮 Manipulação e Análise de Dados

### 🔍 Filtragem de Dados

Foram aplicados filtros para selecionar a cultura **Soja** no período de **01/01/2024 a 30/03/2024**, permitindo uma observação detalhada do comportamento de pH, umidade e nutrientes.

### 📈 Agregação e Estatísticas Descritivas

Foi realizada uma agregação por cultura para calcular as médias de pH, umidade, nutrientes e irrigação.

**Resultados:**

* **Cana-de-açúcar:** maiores médias de N e K (alta demanda nutricional)
* **Soja:** valores equilibrados e irrigação moderada
* **Laranja:** maior média de irrigação, devido à sensibilidade hídrica

---

## 🔗 Correlações

### 💧 Irrigação x Umidade

Correlação linear fraca e negativa entre horas de irrigação e umidade:

* Cana-de-açúcar: -0,146
* Soja: -0,109
* Laranja: -0,042

Esses resultados sugerem a influência de fatores externos (chuvas, evapotranspiração, drenagem).

### 🌾 Irrigação x Nutrientes

Análise de correlação de **Pearson** entre irrigação e nutrientes (N, P, K):

| Cultura        | Tendência                     | Interpretação                       |
| -------------- | ----------------------------- | ----------------------------------- |
| Laranja        | Correlação positiva moderada  | Irrigação ajuda a manter nutrientes |
| Soja           | Correlação levemente negativa | Diluição temporária dos nutrientes  |
| Cana-de-açúcar | Correlação equilibrada        | Retenção prolongada de nutrientes   |

---

## 🧩 Conclusão

A análise evidencia a importância de compreender a interação entre irrigação e nutrição do solo.
Os resultados obtidos podem subsidiar **ajustes de manejo hídrico e nutricional**, promovendo uso racional de água e insumos.

---

## 💻 Tecnologias Utilizadas

* **Oracle SQL Developer**
* **Wokwi (simulação de sensores)**
* **CSV Dataset (sensor_solo.csv)**


# 🟢 LGC Invest
### Simulador de investimentos em Excel

Planilha de planejamento financeiro para simular o crescimento do patrimônio com aportes mensais, estimar dividendos e explorar a distribuição de investimentos entre categorias de fundos imobiliários.

**Excel • Juros compostos • Análise de cenários • Visualização de dados**

---

## 🎯 Objetivo

Transformar parâmetros financeiros em projeções claras, permitindo analisar como o aporte, o prazo e a rentabilidade influenciam a formação de patrimônio.

O projeto aplica conceitos de matemática financeira, organização de dados e visualização em uma interface de simulação no Excel.

## ✨ Funcionalidades

- Sugestão de aporte equivalente a 30% do salário informado.
- Cálculo de patrimônio futuro com aportes mensais.
- Estimativa de dividendos sobre o patrimônio projetado.
- Projeções para 2, 5, 10, 20 e 30 anos.
- Seleção entre os perfis conservador, moderado e agressivo.
- Distribuição ilustrativa do aporte entre seis categorias de FIIs.
- Gráficos de patrimônio por prazo e de distribuição do aporte.

## 🚀 Como utilizar

1. Baixe a planilha deste repositório e abra no Excel.
2. Acesse a aba **Investimento**.
3. Informe salário, aporte mensal, prazo e taxas.
4. Selecione o perfil desejado.
5. Consulte os resultados e os gráficos.
6. Altere os parâmetros para explorar outras simulações.

> Digite as taxas com o símbolo de porcentagem: `1,08%`, por exemplo. Preserve as células que contêm fórmulas.

### Parâmetros de entrada

| Parâmetro | Célula | Exemplo |
| --- | --- | --- |
| Salário | D13 | R$ 9.500,00 |
| Taxa mensal de dividendos | D14 | 0,75% |
| Aporte mensal | D19 | R$ 500,00 |
| Prazo em anos | D20 | 5 |
| Rentabilidade mensal da projeção | D21 | 1,08% |
| Perfil | D34 | Conservador |

A sugestão de 30% do salário funciona como referência. O aporte utilizado nos cálculos é o valor preenchido em **D19**, independentemente dessa sugestão.

## 📊 Exemplo de resultado

Considerando:

- **Aporte:** R$ 500,00 por mês.
- **Prazo:** 5 anos.
- **Rentabilidade da projeção:** 1,08% ao mês.
- **Taxa de dividendos:** 0,75% ao mês.

| Indicador | Resultado |
| --- | --- |
| Patrimônio projetado | R$ 41.902,01 |
| Dividendos mensais estimados ao final do prazo | R$ 314,27 |

### Comparação por prazo

Mantendo o mesmo aporte e as mesmas taxas:

| Prazo | Patrimônio projetado | Dividendos mensais estimados |
| --- | --- | --- |
| 2 anos | R$ 13.615,43 | R$ 102,12 |
| 5 anos | R$ 41.902,01 | R$ 314,27 |
| 10 anos | R$ 121.728,83 | R$ 912,97 |
| 20 anos | R$ 563.524,50 | R$ 4.226,43 |
| 30 anos | R$ 2.166.952,41 | R$ 16.252,14 |

Esses valores representam uma simulação com taxas constantes.

## 🔎 Diferença entre as duas taxas

| Taxa | Aplicação |
| --- | --- |
| **Rentabilidade mensal da projeção** | Calcula o crescimento composto do patrimônio com os aportes |
| **Taxa mensal de dividendos** | Estima a renda mensal sobre o patrimônio projetado |

A taxa de dividendos não altera o patrimônio calculado. Ela é aplicada ao resultado final para estimar a renda mensal.

**As duas taxas não são somadas.** Se a rentabilidade da projeção já considerar dividendos reinvestidos, acrescentá-los novamente ao patrimônio causaria dupla contagem.

## 🗂️ Estrutura do arquivo

| Aba | Conteúdo |
| --- | --- |
| **Investimento** | Entradas, projeções, indicadores, distribuição do aporte e gráficos |
| **Tipo_FIL** | Tabela auxiliar com perfis, categorias de FIIs, chaves de busca e percentuais |

### Organização dos cálculos

- **Salário** → sugestão de investimento.
- **Aporte + prazo + rentabilidade** → patrimônio projetado.
- **Patrimônio + taxa de dividendos** → dividendos mensais estimados.
- **Perfil + categoria de FII** → percentual e valor de alocação.

## ⚙️ Documentação técnica

### Fórmulas principais

As fórmulas abaixo estão na sintaxe do Excel em português.

| Cálculo | Célula | Fórmula |
| --- | --- | --- |
| Sugestão de investimento | D15 | `=salario*30%` |
| Patrimônio acumulado | D22 | `=VF(taxa_mensal;qtd_anos*12;aporte*-1)` |
| Dividendos mensais | D23 | `=Patrimonio*rendimento_carteira` |
| Patrimônio por prazo | C27 | `=VF($D$21;$A27*12;aporte*-1)` |
| Dividendos por prazo | D27 | `=C27*rendimento_carteira` |
| Percentual por categoria | C39 | `=PROCV($D$34&"-"&B39;Chave;4;FALSO)` |
| Valor por categoria | D39 | `=C39*aporte` |

As fórmulas de projeção são replicadas até a linha 31. As fórmulas de alocação são replicadas até a linha 44.

### Função VF

A função **VF**, equivalente a `FV` em inglês, calcula o valor futuro considerando:

- Taxa mensal constante.
- Prazo convertido de anos para meses.
- Aportes de mesmo valor ao final de cada mês.
- Patrimônio inicial igual a zero.

O aporte é informado com sinal negativo na fórmula para representar a saída de caixa e apresentar o patrimônio futuro como valor positivo.

### Busca de percentuais

A função **PROCV** utiliza uma chave formada pela combinação de perfil e categoria, como `Conservador-PAPEL`.

Essa chave é localizada na tabela auxiliar, retornando o percentual correspondente por meio de uma busca exata.

### Intervalos nomeados

| Nome | Referência | Finalidade |
| --- | --- | --- |
| `salario` | `Investimento!$D$13` | Salário informado |
| `rendimento_carteira` | `Investimento!$D$14` | Taxa mensal de dividendos |
| `aporte` | `Investimento!$D$19` | Investimento mensal |
| `qtd_anos` | `Investimento!$D$20` | Prazo da simulação |
| `taxa_mensal` | `Investimento!$D$21` | Rentabilidade da projeção |
| `Patrimonio` | `Investimento!$D$22` | Patrimônio calculado |
| `Chave` | `Tipo_FIL!$B$3:$E$21` | Tabela de referência para busca |

## 🧩 Distribuição por perfil

| Categoria | Conservador | Moderado | Agressivo |
| --- | --- | --- | --- |
| Papel | 30% | 32% | 50% |
| Tijolo | 50% | 40% | 10% |
| Híbridos | 10% | 8% | 5% |
| FOFs | 10% | 5% | 5% |
| Desenvolvimento | 0% | 10% | 20% |
| Hotelaria | 0% | 5% | 10% |
| **Total** | **100%** | **100%** | **100%** |

**A seleção de perfil altera a distribuição do aporte, mas não a rentabilidade projetada.**

Os percentuais são ilustrativos e utilizados para demonstrar a lógica de alocação. Não representam recomendação de carteira ou classificação universal de risco.

## 📈 Visualizações

| Gráfico | Informação apresentada |
| --- | --- |
| Patrimônio por prazo | Comparação do patrimônio projetado em cinco horizontes |
| Aporte por categoria de FII | Distribuição mensal do valor investido conforme o perfil |

Os dois gráficos são de colunas e utilizam os resultados calculados na aba **Investimento**.

## ✅ Conferências realizadas

- Conferência das projeções com a fórmula de valor futuro.
- Verificação de que os percentuais de cada perfil totalizam 100%.
- Conferência da aplicação da taxa de dividendos sobre o patrimônio.
- Verificação da correspondência entre a projeção de cinco anos e o indicador principal no exemplo.
- Inspeção dos intervalos nomeados e das referências dos gráficos.

A análise considerou as fórmulas e os valores salvos no arquivo. A compatibilidade com outros aplicativos de planilhas não foi validada.

## 💡 Competências aplicadas

- Modelagem financeira em Excel.
- Aplicação de juros compostos.
- Funções financeiras e de busca.
- Uso de intervalos nomeados.
- Validação de dados por lista.
- Organização de tabelas auxiliares.
- Visualização de resultados.
- Documentação de regras e premissas.

  ## 🚀 Futuras evoluções

- [ ] Adicionar patrimônio inicial à simulação.
- [ ] Permitir aportes extraordinários e reajustes no aporte mensal.
- [ ] Simular períodos sem aportes.
- [ ] Incluir projeções ajustadas pela inflação.
- [ ] Considerar tributação e custos nos resultados.
- [ ] Comparar diferentes cenários de rentabilidade e variação de mercado.
- [ ] Detalhar o recebimento e o reinvestimento de dividendos.
- [ ] Exibir total aportado e rendimentos acumulados separadamente.
- [ ] Criar gráfico de evolução mensal do patrimônio.
- [ ] Integrar cotações e dados de uma carteira real.
- [ ] Calcular a quantidade de cotas por categoria de investimento.
- [ ] Validar valores de entrada com mensagens de orientação.
- [ ] Proteger células com fórmulas contra alterações acidentais.
- [ ] Adicionar verificações automáticas dos percentuais de alocação.
- [ ] Padronizar a tabela auxiliar e tratar inconsistências nas chaves de busca.
- [ ] Validar a compatibilidade com Google Sheets e LibreOffice.

## 👩‍💻 Autora

**Letícia Guimarães Coelho**

Analista de Dados | Power BI • SQL • Python • Excel

---

> Projeto educacional. As projeções dependem das premissas informadas e não representam garantia de retorno ou recomendação de investimento.

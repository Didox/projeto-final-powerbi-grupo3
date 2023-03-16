# projeto-final-powerbi

# Accenture - Gama Academy - Mulheres em Tech - Data Engineer/Azure - Power BI

Este é o repositório da versão do projeto final em Power BI

Para retornar ao repositório geral, clique [aqui](https://github.com/SheAnalyzes/readme-repository)!

## Índice

- [Apresentação do problema](#apresentação-do-problema)
- [Tecnologias utilizadas](#tecnologias-utilizadas-nesta-etapa-do-projeto)
- [Estrutura do projeto](#estrutura-do-projeto)
- [Download necessário](#download-necessário)
- [Conexão com o Banco de dados](#conexão-com-o-banco-de-dados)
- [Transformações com Power Query](#etl-com-power-query)
- [Tratamento analítico com DAX](#tratamento-analítico-com-dax)
- [Visualizações](#visualizações)
- [Grupo - SheAnalyses](#grupo---sheanalyses)

## Apresentação do problema

Desenvolver uma aplicação em Python para carga de arquivos em um banco de dados SQL e gerar relatórios estatísticos visando a descoberta de fraudes em conta correntede cartão de crédito. Levantar insights de dados a partir de visualizações e transformações. 

Você pode encontrar o link do desafio [aqui](https://docs.google.com/document/d/10fBZm7Sxm60FEIyNk4rqUE-pJLhXRxDi1grAATF7hVw/edit)!

## Tecnologias utilizadas nesta etapa do Projeto

* Power BI - Visualização;
* Power BI - Power Query;
* Power BI - DAX.

## Estrutura do projeto

```
├── README.md
├── pbi_projeto_final.pbix

```

## Download necessário

[Instalação do Software Microsoft Power BI](https://www.microsoft.com/en-us/download/details.aspx?id=58494)! 
O relatório foi desenvolvido na versão: 2.114.864.0 

## Conexão com o banco de dados
Para uso do Power Query é necessária a conexão do Power BI com o banco de dados e liberações de Firewall.
Servidor: projetosfinalserver.database.windows.net
Porta: 1433

## ETL com Power Query


## Tratamento analítico com DAX
Data Analysis Expressions ou DAX, são fórmulas que contribuem para tratamento analítico dos dados, a fim de trazer melhorias e insights mais personalizados para as visualizações.
<p>Tratamento de Dados com DAX</p>
<table>
  <colgroup>
    <col class="column1">
    <col class="columns2plus3" span="2">
  </colgroup>
  <tr>
    <th>Nome Medida</th>
    <th>Códigos</th>
    <th>Definição</th>
  </tr>
  <tr>
    <td>Clientes_cadastrados
</td>
    <td>DISTINCTCOUNT(clientes[id])</td>
    <td>Contagem de clientes distintos cadastrados na tabela cliente</td>
  </tr>
   <tr>
    <td>Clientes_fraudes_in </td>
    <td>CALCULATE(DISTINCTCOUNT(clientes_fraudes[Id_nome_cliente]), clientes_fraudes[n_fraudes_entrada] >0 && clientes_fraudes[n_fraudes_saida] = 0)

</td>
    <td>Contagem de clientes distintos cujas fraudes detectadas envolveram exclusivamente transações de entrada. e</td>
  </tr>
   <tr>
    <td>Clientes_fraudes_out </td>
    <td>CALCULATE(DISTINCTCOUNT(clientes_fraudes[Id_nome_cliente]), clientes_fraudes[n_fraudes_entrada] = 0 && clientes_fraudes[n_fraudes_saida] > 0)
</td>
    <td>Contagem de clientes distintos cujas fraudes detectadas envolveram exclusivamente transações de saída. 

</td>
  </tr>
  <td>Clientes_fraudes_in_e_out </td>
    <td>CALCULATE(DISTINCTCOUNT(CALCULATE(DISTINCTCOUNT(clientes_fraudes[Id_nome_cliente]), clientes_fraudes[n_fraudes_entrada] >0 && clientes_fraudes[n_fraudes_saida] > 0)
</td>
    <td>Contagem de clientes distintos cujas fraudes detectadas envolveram  transações de entrada e saída. 

</td>
  </tr>
  <td>n_clientes_movimentaram  </td>
    <td>DISTINCTCOUNT(movimentacao[cliente_id])
</td>
    <td>Contagem de clientes distintos, cadastrados ou não, que realizaram movimentações de qualquer tipo. 

</td>
  </tr>
  <td>n_total_transacoes</td>
    <td>DISTINCTCOUNT(movimentacao[id])
</td>
    <td>Quantidade total de transações/movimentações </td>
  </tr>
  <td>n_transacoes_entrada</td>
    <td>CALCULATE(DISTINCTCOUNT(movimentacao[id]), movimentacao[tipo_transacao] = "Entrada")
</td>
    <td> Quantidade total de transações/movimentações de Entrada </td>
  </tr>
  <td>n_transacoes_saida</td>
    <td>CALCULATE(DISTINCTCOUNT(movimentacao[id]), movimentacao[tipo_transacao] = "Saída")
</td>
    <td>Quantidade total de transações/movimentações de Saída.</td>
  </tr><td>Total_clientes_fraudes</td>
    <td>CALCULATE(DISTINCTCOUNT(movimentacao[cliente_id]), movimentacao[classificacao_transacao] = "Fraude")
</td>
    <td> Quantidade total de clientes envolvidos em fraudes </td>
  </tr>
  <td>Total_fraudes</td>
    <td>CALCULATE(DISTINCTCOUNT(movimentacao[id]), movimentacao[classificacao_transacao] = "Fraude")
</td>
    <td>Quantidade total de transações fraudulentas.</td>
  </tr>
  <td>Total_legitimas</td>
    <td>CALCULATE(DISTINCTCOUNT(movimentacao[id]), movimentacao[classificacao_transacao] = "Legítima")
</td>
    <td>Quantidade total de transações Legítimas.</td>
  </tr>
  <td>valor_total</td>
    <td>SUM(movimentacao[valor_absoluto])
</td>
    <td>Valor total absoluto movimentado.</td>
  </tr>
  <td>Valor_total_fraudes</td>
    <td>CALCULATE(SUM(movimentacao[valor_absoluto]), movimentacao[classificacao_transacao] = "Fraude")
</td>
    <td>Valor absoluto movimentado em transações fraudulentas.</td>
  </tr>
  <td>Valor_total_legitimas </td>
    <td>CALCULATE(SUM(movimentacao[valor_absoluto]), movimentacao[classificacao_transacao] = "Legítima")
</td>
    <td>Valor absoluto movimentado em transações legítimas.</td>
  </tr>
</table>


## Visualizações
Foi criado um menu inicial com links para cada aba do Dashboard.

1 - Dados: Aba cujo foco principal é a análise dos dados iniciais, conta com gráficos de barras e números a respeito das movimentações de forma geral. Contém filtro de data, com ano e mês, além de filtro para transações de entrada e saída

2 - Insights Fraudes: Aba cujo foco é a análise das fraudes, conta com gráficos de linhas, colunas clusterizadas e uma tabela, além de números sobre as operações fraudulentas. Contém filtro de data, com ano e mês;

3 -  Insights Clientes: Objetivo é analisar características dos clientes envolvidos em fraudes, seja de entrada ou de saída. Conta com gráficos de colunas empilhadas e tabelas. Por avaliar características fixas de clientes, a aba não conta com filtros.



## Grupo - SheAnalyses

![1678919788585](image/README/1678919788585.png)![1678922005355](image/README/1678922005355.png)

| Ana Paula Santos de Queiroz<br /><br />Linkedin: [/ana-paula-santos-de-queiroz-086807166](https://www.linkedin.com/in/ana-paula-santos-de-queiroz-086807166/)<br />Github: [/Queirozaps](https://github.com/Queirozaps) | ![1678913762981](image/README/1678913762981.png) |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------: |
|  **Arianna Silveira Santos**<br />  <br />Linkedin: [/arianna-silveira-aa474514b](https://www.linkedin.com/in/arianna-silveira-aa474514b/)<br />Github: [/AriannaSilveira](https://github.com/AriannaSilveira)  | ![1678880182631](image/README/1678880182631.png) |
|                            **Carolina Gois**<br /><br />Linkedin: [/carolina-gois](https://www.linkedin.com/in/carolina-gois/)<br />Github: [/carolgois](https://github.com/carolgois)                            | ![1678915457372](image/README/1678915457372.png) |
|                   **Emilly Correa Santiago**<br /><br />Linkedin: [/emillysantiago23](https://www.linkedin.com/in/emillysantiago23/)<br />Github: [/emillysant](https://github.com/emillysant)                   | ![1678881122291](image/README/1678881122291.png) |
|                              **Mariana Freire**<br /><br />Linkedin: [/maricf](https://www.linkedin.com/in/maricf/)<br />Github: [/marianafreire](https://github.com/marianafreire)                              | ![1678915794465](image/README/1678915794465.png) |
|             **Priscila Assumpção Fernandes**<br /><br />Linkedin: [/priscila-af](https://www.linkedin.com/in/priscila-af/)<br />Github: [/priscilaassumpcao](https://github.com/priscilaassumpcao)             | ![1678916901964](image/README/1678916901964.png) |
|                    **Vivian Medina**<br /><br />Linkedin: [/vivian-medina-b7250961](https://www.linkedin.com/in/vivian-medina-b7250961/)<br />Github: [/medinavi](https://github.com/medinavi)                    | ![1678885040168](image/README/1678885040168.png) |

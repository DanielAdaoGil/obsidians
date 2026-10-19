Vamos trabalhar no menu da Tesouraria, que tbm deve ser colocado na sidebar;

Movimentos Financeiros
Relatórios
Estatisticas

Movimentos Financeiros: 
	## 1. Dados essenciais de cada movimento

Estes são os campos que recomendo que não faltem.

1. Tipo de movimento

Obrigatório

Entrada ou saída. Determina se o valor será acrescentado ou subtraído do saldo.

2. Valor

Obrigatório

Montante da operação, por exemplo, 25.000 Kz. Deve ser superior a zero.

3. Data do movimento

Obrigatório

Data em que o dinheiro efetivamente entrou ou saiu, que pode ser diferente da data de registo.

4. Categoria

Obrigatório

Classifica a operação, como doações, pagamento de cota, taxa de aniverário, taxa de inscrição, taxa para dia Mundial, taxa de actividade, inscrição para medalha. 

5. Descrição

Obrigatório

Explica o motivo do movimento. Ex.: Compra de material de escritório.

6. Conta financeira

Obrigatório

Identifica de onde saiu ou para onde entrou o dinheiro: caixa físico, conta bancária ou carteira digital.


	## 2. Dados importantes para um sistema mais completo

Além dos campos essenciais, recomendo acrescentares os seguintes:

| Campo                          | Finalidade                                                                                        |
| ------------------------------ | ------------------------------------------------------------------------------------------------- |
| Número de referência           | Identificar cada movimento de forma única.MV-XXX(onde xxx é o nº do movimento começando por zero) |
| Pessoa ou entidade relacionada | Identificar quem pagou ou recebeu o dinheiro.                                                     |
| Método de pagamento            | Dinheiro, transferência bancária, Multicaixa Express, cartão, etc.                                |
| Comprovativo                   | Anexar recibo, fatura ou documento que justifique a operação.(opcional)                           |
| Estado do movimento            | Distinguir operações pendentes, concluídas ou anuladas.                                           |
| Observações                    | Adicionar informações complementares.                                                             |
| Registado por                  | Identificar o utilizador que criou o registo.                                                     |
| Data de registo                | Saber quando a informação foi introduzida no sistema.                                             |
 em movimentos financeiros, permita tbm que possam ser apresentados, e filtrados pela data(dia, mes, trimestre, ano), tipo de movimento(entrada ou saida), quantidade de valor (maior ou igual a, menor ou igual a, igual a );
relatórios trimestrais são gerados de forma automatica quando o trimestre acaba com base nos dados do movimento financeiro disponiveis para baixar o excel ou pdf.


em estatisticas apresentes o total do saldo e  quanto determinada categoria arrecadou ou gastou
gerar relatórios que podem ser diarios, semanais, mensais, quinzenais, trimestrais, semestrais, anuais
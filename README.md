# ProvaAPI
Requisitos Funcionais
•	Dado um valor do débito e um número de parcelas informados pelo usuário, a aplicação deverá calcular e retornar: 
o	a) dados resumo:
	Valor do débito original (decimal, informado pelo usuário);
	Número de parcelas (inteiro, informado pelo usuário);
	Valor total da correção (decimal, somatório das correções das parcelas);
	Valor total do parcelamento (decimal, somatório das parcelas).
o	b) uma lista de parcelas com os seguintes dados em cada parcela:
	Número da parcela (inteiro e sequencial);
	Data do vencimento (data);
	Valor do saldo atualizado (decimal);
	Valor da parcela (decimal);
	Valor do saldo remanescente (decimal);
	Valor da correção da parcela (decimal);
•	As parcelas devem ter como data de vencimento todo dia 15 de cada mês, a partir do mês seguinte ao de realização da simulação. 
o	Por exemplo, se a simulação é feita no dia 10/04, a primeira parcela deve ter como vencimento dia 15/05, a segunda 15/06, a terceira 15/07, etc.
•	O valor de cada parcela será apurado mediante a divisão do saldo devedor do débito atualizado, pelo número total de parcelas remanescentes.
•	A atualização do montante remanescente do saldo devedor é feita por meio do acréscimo de juros de mora, à taxa de um por cento (1%) ao mês.

Requisitos Não-Funcionais
•	A aplicação deverá usar o padrão REST/RESTFul para comunicação.
•	A aplicação deverá permitir o envio dos dados para simulação usando os verbos HTTP GET e POST (em duas rotas distintas).
•	A aplicação deverá usar JSON para troca de dados.
•	Não é necessário nenhum tipo de persistência de dados.
Observações
•	Não arredondar os valores. Tanto para realização dos cálculos quanto para apresentação (retorno dos dados) truncar os valores em duas casas decimais após a vírgula.
•	O número de parcelas mínimo é 2 parcelas e o número máximo é 60 parcelas.
•	O valor de cada parcela:
o	Não pode ser inferior a 200,00 para crédito tributário superior a 2.000,00.
o	Não pode ser inferior a 50,00 para crédito tributário inferior ou igual a 2.000,00
•	O valor de cada parcela é composto pelo somatório do principal e da correção (juros calculado sobre o saldo remanescente). O valor principal é constante, só o valor da correção que aumenta.
•	A primeira parcela não possui correção (juros).
•	Após o pagamento da última parcela, o valor do saldo remanescente é completamente zerado.


Exemplo de Cálculo do Parcelamento
Valor total do crédito: 10.000,00
Número de parcelas solicitadas: 10
Valor da primeira parcela:  10.000/10                                                                    = 1.000,00
Valor da segunda parcela:   (10.000 -1.000 = 9.000)  x 1,01 (9.090)/9             = 1.010,00
Valor da terceira parcela: (9.090 - 1.010 = 8.080) x 1,01 (8.160,80)/8             = 1.020,10


Os dados retornados pela API devem permitir a um frontend montar uma tela com a seguinte estrutura (considerando os valores do exemplo acima):


Resumo do Parcelamento
Valor do Débito	10.000,00
Número de Parcelas	10
Valor Total da Correção	XXX,XX
Valor Total do Parcelamento	XXXXX,XX


Demonstrativo de Cálculo do Parcelamento
Nº da Parcela	Data de Vencimento	Valor do Saldo Atualizado	Valor da Parcela	Valor do Saldo Remanescente	Valor da Correção
1	XX/XX/XXXX	10.000,00	1.000,00	9.000,00	0,00
2	XX/XX/XXXX	9.090,00	1.010,00	8.080,00	10,00
...	...	...	...	...	...
10	XX/XX/XXXX	XXXX,XX	XXXX,XX	0,00	XX,XX


 
Exemplo de JSON contendo a estrutura esperada

{
    "vlrDebito": XXXXX,
    "numParcelas": XX,
    "vlrTotal": XXXX.XX,
    "vlrCorrecao": XXX.XX,
    "parcelas": [
        {
            "numParcela": 1,
            "datVencimento": "XXXX-XX-XXTXX:XX:XX",
            "vlrSaldoAtualizado": XXXXX,
            "vlrParcela": XXXX,
            "vlrSaldoRemanescente": XXXX,
            "vlrCorrecao": XX
        },
        (...)
    ]
}



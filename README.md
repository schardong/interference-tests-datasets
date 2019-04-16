# Repositório de dados para testes de interferência de poços

Esse repositório serve para armazenar os dados gerados para testes de
interferência de poços. Instruções sobre o formato dos dados, bem como
localização e o que armazenar nessa pasta são dadas abaixo.

## Formato dos dados

Idealmente, os dados devem ser armazenados em formato CSV, com os dados dos
poços produtores em um arquivo separado dos injetores. Por hora, vamos
armazenar tanto a curva de pressão no fundo do poço quanto a sua derivada,
cada qual em seu arquivo. As classes de cada cenário são armazenadas no
arquivo "classes.csv" e por hora são restritas a **OPEN** e **CLOSED**. Os
parâmetros de simulação são codificados em formato JSON e armazenados em um
arquivo separado. Em resumo, a lista de arquivos por rodada de simulação é:

* producer_bhp.csv: Contém a pressão no fundo do poço para os poços *produtores* em seu domínio original;
* injector_bhp.csv: Contém a pressão no fundo do poço para os poços *injetores* em seu domínio original;
* producer_dbhp.csv: Contém a derivada da pressão no fundo do poço para os poços *produtores*;
* injector_dbhp.csv: Contém a derivada da pressão no fundo do poço para os poços *injetores*;
* classes.csv: Contém as classes de cada cenário gerado
* simulation_parameters.json: Contém os parâmetros de simulação usados para gerar cada cenário. Deve ser possível reconstruir a simulação a partir desses dados.

Todos os arquivos CSV devem ser *column-major*, ou seja, cada cenário deve ser
armazendo em uma coluna. A primeira coluna é reservada ao tempo, ou log(tempo)
no caso da derivada.

Já o arquivo `simulation_parameters.json` deve conter uma lista, ou `set` com
os dados de cada cenário. Cada cenário armazena um identificador único para
aquela rodada, um dicionário com dados de `grid`, refinamento, poços e canal.
O formato de entrada de cada cenário é o seguinte:

```
{
	"id": <integer>
	"closed": <boolean>
	"reference_file": <string>
	"refinement_info": {
		"radius_per_level": <integer>
	}
	"grid_dims": {
		"J": <integer>,
		"I": <integer>,
	}
	"well_info": {
		"well_name_1": Well dict
		"well_name_2": Well dict
		...
	}
	"channel_info": [
		Channel_1,
		Channel_2,
			...
	]
}
```

## Descrições das rodadas

Cada novo conjunto de dados gerado deve ser armazenado como uma rodada nova,
e sua descrição deve ser feita nessa Seção. Deve-se evitar armazenar os
arquivos do IMEX, ja que eles podem ocupar muito espaco. Por isso, o arquivo
`simulation_parameters.json` deve conter os dados necessarios para a
reconstrução dessas simulações, se necessário. Dessa forma, poderemos repetir
algum experimento feito anteriormente.

### Rodada 3
Mapa 2D de dimensões 101x101 com um canal horizontal reto de 11 células de
largura. Dois poços foram centrados nas células (45, 50) e (55, 50). Foram
sorteados dez conjuntos de coordenadas para cada poço em um raio de uma célula
em cada direção a partir das coordenadas mencionadas acima. Foi gerado um
conjunto de 2068 cenários classificados como **OPEN** ou **CLOSED**. A seed
usada para o gerador de números aleatórios foi 668. Os arquivos foram
armazenados em formato zip para poupar espaço e banda.

### Rodada 4
Mapa 2D de dimensões 101x101 com um canal horizontal reto de 11 células de
largura. Dois poços foram posicionados de maneira aleatória com centro nas
células (45, 50) e (55, 50), o primeiro poço é produtor de óleo, com vazão 500,
já o segundo poço é injetor de água, e possui vazão 500. Foram sorteados 100
conjuntos de coordenadas para cada poço a um raio de 4 células em qualquer
direção. Foi gerado um conjunto de 17952 cenários, sendo estes 17136
classificados como **OPEN** e 816 **CLOSED**. A seed para o gerador de números
aleatórios foi 624. Os arquivos foram armazenados em formato zip para poupar
espaço e banda.

### Rodada 5
Mada 2D de dimensões 101x101 com um canal horizontal reto de 11 células de
largura. Dois poços foram posicionados de maneira aleatória com centro nas
células (45, 50) e (55, 50). , o primeiro poço é produtor de óleo, com vazão 500,
já o segundo poço é injetor de água, e possui vazão 500. Foram sorteados 100
conjuntos de coordenadas para cada poço a um raio de 4 células em qualquer
direção. Foi gerado um conjunto de 92840 cenários, sendo estes 88620
classificados como **OPEN** e 4220 **CLOSED**. A seed para o gerador de
números aleatórios foi 1003. Os arquivos foram armazenados em formato zip para
poupar espaço e banda.

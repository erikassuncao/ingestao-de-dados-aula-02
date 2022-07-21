### Aula 02 - Ingestão de Dados - PECE/USP

O objetivo da tarefa da aula 2 era buscar todas as instituições no período mensal nos dois últimos anos através do portal do governo, extraindo arquivos .csv que foram alocados na pasta "raw".

Em seguida, através de Python, deveríamos consumir a API passando como parâmetro o CNPJ contido nos .csv do primeiro passo.

O terceiro passo, também em Python e em tarefas individuais, seria realizar as devidas tratativas e armazenar na pasta "trusted" para finalmente ser convertido para "star schema" e então, uma vez que os dados estivessem no banco, fossem exibidos na dashboard da Aula 01.
## Aprendizados

Acreditamos que o maior desafio foi gerar as chaves primárias para servir como relacionamento entre tabelas. Isso é algo simples que qualquer sistema de banco de dados consegue gerar de forma consistente, porém quando recebemos as instruções de dividir em etapas os script, perdemos também a consistência na geração de IDs. 

Como workaround, decidimos gerar uma HASH através das strings e então usar o resultado para como chaves de relacionamento. 

Como as chaves não poderiam ser grandes, descartamos algoritimos como SHA1, SHA256, MD5, e acabamos por utilizar a biblioteca ZLIB.CRC32.
## Demonstração do uso de HASH para relacionamento

Exemplo de um ambiente comum:

| CODIGO_UNIDADE | UNIDADE | 
| --- | --- | 
| 1 | por envelope | 
| 2 | por copia |
| 3 | por talao |
| 4 | por titulo |

Exemplo de com o uso de HASH:

| CODIGO_UNIDADE | UNIDADE | 
| --- | --- | 
| 55137634 | por envelope | 
| 76980960 | por copia |
| 215245658 | por talao |
| 291672851 | por titulo |

```
t = zlib.crc32('por envelope') 
  
print(t) 
```
O resultado de t é: 55137634



## Como funcionam os scripts

Primeiro, os scripts deverão ser executados na seguinte ordem:

    1 - Unifica CSVs
    2 - Consome API

Os demais scripts não precsiam de uma ordem específica, pois são para gerar os dados para importação como SQL:

    Gera DIM_INSTITUICAO
    Gera DIM_SERVICO
    Gera DIM_TEMPO
    Gera DIM_UNIDADE
    Gera FATO_RECL
    Gera FATO_TARIFAS

Pronto, agora os dados gerados estão prontos para serem importados para a estrutura usada na Aula 01.
    
## Referência

 - [Ranking de Instituições por Índice de Reclamações](https://dados.gov.br/dataset/ranking-de-instituicoes-por-indice-de-reclamacoes)
 - [ Tarifas Bancárias - por Segmento e por Instituição](https://dados.gov.br/dataset/tarifas-bancarias-por-segmento-e-por-instituicao)
## Autores

- [@erikassuncao](https://www.github.com/erikassuncao)
- Jorge Alexandre Pires de Oliveira
- Paulo Henrique de Souza Pereira Prazeres
- Willian Alves Barboza


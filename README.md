# Algoritmo de Substituição de Páginas

>Aluna:
- Júlia Mendonça Silva - 5956

Link do repositório Git: [Algoritmo de Substituição de Páginas](https://github.com/Juliams78/AlgoritmoSubstituicaoPaginas)

### Tópicos
:white_circle: [Descrição do projeto](#descrição-do-projeto) <br/>
:white_circle: [Como rodar a aplicação](#como-rodar-a-aplicação) <br/>
:white_circle: [Problemas e bugs](#problemas-e-bugs) 

### Descrição do Projeto
O projeto em questão visou em implementar um algoritmo de substituição de páginas dentre os aprendidos na matéria.
Para isso, foi disponibilizado pelo professor da disciplina um código que continha o funcionamento de um VMM e o algoritmo Random já implementados. <br/>
Este código pode ser visualizado na primeira versão do arquivo _vmm.c_ presente neste repositório. 

O algoritmo de substituição de páginas escolhido para ser implementado foi o FIFO - First in First out. <br/>
O algoritmo FIFO no contexto de gerência de memória é um dos mais simples, porém é ineficiente. Seu funcionamento se dá por retirar da memória a página mais antiga, 
ou seja, a "primeira" que entrou no mapeamento da memória. <br/>
Exemplos do funcionamento do algoritmo e da saída do código implementado podem ser verificados no relatório em .pdf também presente neste repositório, assim como uma comparação com o algoritmo Random.


### Como rodar a aplicação
Todos os testes de execução do código foram feitos em uma máquina virtual do aplicativo VirtualBox com um SO Linux Ubuntu 16.04.<br/>
Para rodar a aplicação deve primeiro compilar o código para gerar o arquivo executável com a seguinte linha de comando em um terminal Linux
``` gcc -Wall vmm.c -o vmm ```, da mesma forma que foi descrita pelo professor no arquivo de orientação do trabalho. <br/>
Depois, deve ser digitado o comando ``` ./vmm [algoritmo] 10 < anomaly.dat ```, sendo que _[algoritmo]_ se refere a qual algoritmo você gostaria de executar, 
como temos implementados apenas os algoritmos Random e FIFO, deve ser escolhido a palavra ``` random ``` ou ``` fifo ``` para solicitar o respectivo algoritmo.
Portanto teremos como opção: ``` ./vmm random 10 < anomaly.dat ``` ou ``` ./vmm fifo 10 < anomaly.dat ```.

### Problemas e bugs
Durante a confecção do projeto o principal problema foi entender o funcionamento do código disponibilizado, uma vez que o código base possuía muitas 
variáveis e poucos comentários. Com isso alguns dias foram gastos apenas "printanto" variáveis e buscando entender como o código funcionava e onde deveriam ser 
feitas as modificações para implementar o algoritmo.

Um bug que permaneceu no projeto foi que o algoritmo fifo retorna o número certo de _page faults_ presentes a partir do arquivo _anomaly.dat_ 
(também presente nesse repositório), porém, ao verificar o valor das variáveis _fifo_frm_ e _to_free_ podemos ver que elas não apontam para o mesmo endereço,
e portanto, a página retirada da memória acaba por não ser a página certa segundo o funcionamento do algoritmo fifo. Se verificar o código podemos ver _printf's_ que no momento estão comentados que podem mostrar essa diferença. Infelizmente, essa foi a única forma que encontrei de fazer com que o algoritmo "funcionasse", pois de qualquer outra forma que tentei implementar não era possível passar pela linha ``` assert(page_table [to_free][PT_MAPPED] != 0); ```, pois o vlor da variável _to_free_ nesse contexto apontava que a página em questão não estava mapeada, o que ao meu entender, deveria ser impossível com base no código.

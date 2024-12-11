# Entendendo a execução de um programa de computador nas suas várias camadas

Gostaria de entender como os caracteres escritos por mim são, ao final, executados. 

Parece sempre haver uma dúvida sobre como tudo funciona de ponta a ponta(sendo o teclado uma interface que está numa das pontas externas mais próximas do usuário e o circuito em si uma das camadas mais distantes dele)

Como um caractere que está em um arquivo com sua respectiva extensão, tendo sido anteriormente enviado a partir do teclado, acaba sendo executado? Como um arquivo de código de fato está na memória? Há vários blocos na memória cada qual com um caractere, por exemplo? Quando ele já está na memória, como o compilador vai efetivamente fazer com que o código passe a estar em um formato executável pela máquina? Quem compila o compilador?

Esse projeto busca esclarecer essas questões e muitas outras

### O processador

### A unidade lógica e aritmética

> A ALU não é mais que um sistema combinatório com capacidade de efetuar várias operações sobre os seus operandos BARR_A e BARR_B. *Arquitetura de Computadores; José Delgado, Carlos Ribeiro; 5ª edição; seção 7.2*
> 

Como ela, de fato, realiza essas operações?

*Arquitetura de Computadores; José Delgado, Carlos Ribeiro; 5ª edição; figura 7.4*. O BARR_A(barramento A) e o BARR_B(barramento B) parecem ter ambos 16 bits. Aparentemente o BARR_A está ligado a uma porta XOR(ou exclusivo). Mas, bem, a porta tem dois receptores nesse caso. Não sei ainda o que significaria esses 16 bits estarem conectados a um só dos receptores da porta. Significaria que compararia um por um com nA? Significa que estão todos em paralelo(de modo que o XOR tem 17 receptores) mas que, por conveniência, colocou como se estivessem em série 

### Supondo um arquivo de código em C, como ele estaria armazenado em memória?

Me refiro à organização dele. Suspeito que cada caractere esteja em um espaço de memória

### Se em cada registro da memória na seção pertencente a esse arquivo conter um caractere, como eles seriam trazidos à CPU e, posteriormente, executados?

Eu imagino que primeiro deve haver um compilador já previamente escrito. A esse compilador podem ser passados cada caractere do código para ser feita a análise léxico. 

### O compilador

### Como um compilador funciona?

Se eu não me engano, havia uma função em um compilador para pegar caractere por caractere. Nesse caso, creio que era para separar as palavras por tokens. Por exemplo, se estou na linguagem Pascal e começa-se a análise de um novo token que inicia com o caractere “5”, este token não pode ser um identificador, pois os identificadores em Pascal não podem começar com algarismos. Essa parte seria a do analisador léxico, o qual, se não me engano, tem como fundamento um Autômato Finito . Esse compilador poderia já estar escrito em linguagem de máquina.

### O analisador léxico

Para um analisador léxico, há um autômato que, se não me engano é finito. Ele pode ser representado por uma matriz de transição.

```bash
transition_matrix = [ #   L    D    +    -    *    =    <    >    :    .    ,    ;    (    )    {    }    "    %   EB  EOL   NL  TAB  EOF   oc
                   #   0    1    2    3    4    5    6    7    8    9   10   11   12   13   14   15   16   17   18   19   20   21   22   23
                   [   1,   2, 103, 104, 105, 106,   5,   6,   7, 113, 114, 115, 117, 118,   8, 503,   9, 120,   0,   0,   0,   0,   0, 504], # 0
                   [   1,   1, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100], # 1
                   [ 101,   2, 101, 101, 101, 101, 101, 101, 101,   3, 101, 101, 101, 101, 101, 101, 101, 101, 101, 101, 101, 101, 101 ,101], # 2
                   [ 500,   4, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500], # 3
                   [ 102,   4, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102, 102], # 4
                   [ 108, 108, 108, 108, 108, 109, 108, 107, 108, 108, 108, 108, 108, 108, 108, 108, 108, 108, 108, 108, 108, 108, 108, 108], # 5
                   [ 110, 110, 110, 110, 110, 111, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110, 110], # 6
                   [ 116, 116, 116, 116, 116, 112, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116, 116], # 7
                   [   8,   8,   8,   8,   8,   8,   8,   8,   8,   8,   8,   8,   8,   8,   8,   0,   8,   8,   8,   8,   8,   8, 501,   8], # 8
                   [   9,   9,   9,   9,   9,   9,   9,   9,   9,   9,   9,   9,   9,   9,   9,   9, 119,   9,   9, 502,   9,   9, 501,   9]  # 9
        ]
```

### Quem compila o compilador?

### Quem monta o código em Assembly?

Supondo que um código em C esteja em memória.  

Porém, como um caractere do código é analisado dentro do próprio *hardware*? Ele teria que estar dentro de um registrador. Teria de haver

### Há o endereço de memória. Como é o circuito que de fato permite trazer os dados que estão nos diferentes tipos de armazenamento.

### Memória RAM

Se eu não me engano, a CPU foi planejada de modo que em um registrador há um endereço de memória. Como esse dado seria trazido a partir dela? 

![*Referência* <[3-Line to 8-Line Decoder and Demultiplexer](https://www.elprocus.com/designing-3-line-to-8-line-decoder-demultiplexer/)>](Entendendo%20a%20execuc%CC%A7a%CC%83o%20de%20um%20programa%20de%20computad%2014b5d34d068d80c5b6b5c8f66684a33d/image.png)

*Referência* <[3-Line to 8-Line Decoder and Demultiplexer](https://www.elprocus.com/designing-3-line-to-8-line-decoder-demultiplexer/)>

> O circuito acima pode representar 8 células de memória usando três bits (A0, A1, A2). Cada bit tem dois estados 0 ou 1. Por exemplo, 101 ativará A0 e A2, e a saída correspondente será selecionada, digamos Z2 neste caso. Todas as saídas Z0, Z1 .. Z7 podem ser conectadas a uma célula de memória. Desta forma, a seleção do endereço de memória é uma operação constante. *Traduzido de* <[https://stackoverflow.com/questions/53710834/how-does-the-computer-directly-access-a-memory-location-in-the-ram](https://stackoverflow.com/questions/53710834/how-does-the-computer-directly-access-a-memory-location-in-the-ram)>, *autor: didxga, 2020*
> 

Nesse caso, como os dados, de fato, sairiam das células? Talvez poderia ser assim: cada bit da célula está ligada a um cada um dos “fios” de um barramento. Nesse caso, a célula teria um número de bits igual ao número de “fios” do barramento. Esse barramento pararia diretamente no registrador correto da CPU. Algo mais ou menos assim:

![image.png](Entendendo%20a%20execuc%CC%A7a%CC%83o%20de%20um%20programa%20de%20computad%2014b5d34d068d80c5b6b5c8f66684a33d/image%201.png)

Porém, seria necessário saber o registrador correto, pois há diferentes registradores. Talvez sempre pare no mesmo, mas depois pode ser movido para um registrador diferente.

### Momento pós-compilação

Deve haver a criação das estruturas de dados na memória(objetos, funções)

## Apendices

Também há a pergunta: como esses dados de fato são postos na RAM

# Plano

- [ ]  Entender como funciona o computador inteiro como um sistema digital completo. Com isso me refiro a entender como o processador, por exemplo, de fato se integra com uma memória RAM, ou com um SSD em termos de sistemas digitais.
    - [ ]  Como de fato o processador se integra com a memória RAM
        - [ ]  Como o processador se integra com a memória RAM e SSD simultaneamente
- [ ]  Como um processador de fato funciona
    - [ ]  Ordem de execução das coisas
- [ ]  Quem compila o compilador

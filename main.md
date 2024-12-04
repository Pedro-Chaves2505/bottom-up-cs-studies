# Entendendo a execução de um programa de computador nas suas várias camadas

### Supondo um arquivo de código em C, como ele estaria armazenado em memória?

Me refiro à organização dele. Suspeito que cada caractere esteja em um espaço de memória

### Se em cada registro da memória na seção pertencente a esse arquivo conter um caractere, como eles seriam trazidos à CPU e, posteriormente, executados?

Gostaria de entender como os caracteres escritos por mim são, ao final, executados. Como um caractere que está em um bloco de código, tendo sido anteriormente enviado a partir do teclado, acaba sendo executado? Como um arquivo de código de fato está na memória? Há vários blocos na memória cada qual com um caractere, por exemplo? Se eu não me engano, havia uma função em um compilador para pegar caractere por caractere. Nesse caso, creio que era para separar as palavras por tokens. Por exemplo, se estou na linguagem Pascal e começa-se a análise de um novo token que inicia com o caractere “5”, este token não pode ser um identificador, pois os identificadores em Pascal não podem começar com algarismos. Essa parte seria a do analisador léxico, o qual, se não me engano, tem como fundamento um Autômato Finito . Esse compilador poderia já estar escrito em linguagem de máquina.

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

Supondo que um código em C esteja em memória.  

Porém, como um caractere do código é analisado dentro do próprio *hardware*? Ele teria que estar dentro de um registrador. Teria de haver

 Há o endereço de memória. Como é o circuito que de fato permite trazer os dados que estão na memória. Se eu não me engano, a CPU foi planejada de modo que em um registrador há um endereço de memória. Nesse caso, a tarefa de de fato trazer o dado é da memória? Na verdade, suspeito ser mais provável que a CPU ciclicamente compare

Deve haver a criação das estruturas de dados na memória(objetos, funções)
# POOA <h1>
##### Autor: Guilherme Locca Salomão <h5>


[**POO**](https://pt.wikipedia.org/wiki/Orienta%C3%A7%C3%A3o_a_objetos), programação orientada a objetos, é um dos 4 principais paradigmas da programação, um dos quais a depender do caso em questão, pode ser a melhor estrutura para se usar em seu programa

Tendo em mente a vontade de aplicar POO em seu projeto, pode-se questionar sobre o “qual é o melhor caminho?” ou “qual é o caminho mais fácil?” e disso se origina a pergunta, **Qual a melhor linguagem de programação para orientação a objetos?**

A resposta é simples, e um jeito de colocar isso em perspectiva é fazendo a seguinte analogia:
É tão possível correr uma maratona com um tênis ergonômico e resistente, quanto correr ela com um chinelo de sola lisa.
O que isso quer dizer é, **qualquer linguagem serve para programação orientada a objetos**, do mesmo jeito que qualquer ferramenta serve para consertar uma máquina, a questão é que **dependendo do objetivo, há melhores ferramentas para se usar**.

POO é um grande conjunto de diretrizes e ou estruturas a se seguir para criar seu programa, e muitas delas podem ser traduzidas para outros paradigmas da computação, isso faz com que seja possível afirmar que qualquer linguagem pode ser usada com esse objetivo.

Um conjunto dessas diretrizes é representado pelo acronimo [SOLID](https://pt.wikipedia.org/wiki/SOLID) , dentro deles falaremos apenas do S, que representa [_Single-responsibility principle_](https://en.wikipedia.org/wiki/Single-responsibility_principle)(Princípio da responsabilidade única).

## Princípio da responsabilidade única <h2>

Esse princípio é resumido com a seguinte frase

**Uma classe deve ter um, e somente um, motivo para mudar**

Vamos expandir isso com um exemplo
~~~
class quadrado{

	float aresta;
	
    float printAreaQuadrado(){
        printf(“%f”, this.aresta*this.aresta);
    }
}
~~~

uma função simples e do dia-a-dia de qualquer programador, ela não está errada, porém o que devemos nos perguntar é, **quantos trabalhos ela faz?** 
Como podemos ver, além de imprimir a área, ela também calcula a área. logo deveríamos separar isso em funções diferentes.


~~~
class quadrado{

	float aresta;
	
	float calculaArea(){
		return this.aresta*this.aresta;
	}
    void printAreaQuadrado(){
        printf(“%f”,calculaArea());
    }
}
~~~

pronto, temos uma classe com responsabilidade única, certo? Errado, nesta classe ainda temos dois trabalhos distintos, o trabalho de calcular a área e o trabalho de imprimir a área, logo, seguindo o princípio em questão, devemos separá los.
~~~
class quadrado{

	float aresta;
	
	float calculaArea(){
		return this.aresta*this.aresta;
	}
}

class quadradoPrinter{

    quadrado Quad;
    void printAreaQuadrado(){
        printf(“%f”,Quad.calculaArea());
    }

}
~~~
Agora sim temos duas classes com responsabilidades únicas, uma sendo responsável por armazenar as informações e realizar cálculos intrínsecos a essas informações, e outra responsável apenas por imprimir essas informações. Seguindo esse princípio, expandir esse código, como por exemplo adicionar o volume e imprimir ele, é mais fácil e seguro, sem causar quebras na lógica do mesmo. E se quisermos adicionar mais coisas?


## Design especulativo <h2>


Tendo o mesmo exemplo de antes, já corrigido pelo Princípio da responsabilidade única, digamos que este tenha sido o requisito de um cliente: “me faça um programa que imprime a área de um quadrado”.

O código anterior atende a todos os requisitos? Sim, mas e se caso o cliente não comentou que queria também que o programa imprimisse a área tanto em metro, quanto centimetros? E se ele quisesse que fosse impresso em outra base numérica, como base binária, ou hexadecimal e etc?

Quando se repete muito essa frase **“E se”** este é um sinal que você está se afundando dentro da espiral contínua chamada **design especulativo**, onde você assume que, dentro de um requisito sem muitas especificações, coisas que não foram realmente ditas podem ser implícitas, e então o código procede a aumentar em complexidade as vezes desnecessariamente.

Para evitar isso, basta notar o quanto está se adicionando coisas “desnecessárias”, como por exemplo, poder imprimir a área do quadrado com números coloridos, algo que baseado na requisição, não aparenta ser necessário, e verificar se a complexidade do código não está tomando proporções muito grandes. Um bom norte para se manter longe disso é seguir o princípio KISS - Keep It Simple, Stupid (Mantenha tudo simples, estupido), onde sempre devemos optar pelo caminho mais simples, com menos complexidades.



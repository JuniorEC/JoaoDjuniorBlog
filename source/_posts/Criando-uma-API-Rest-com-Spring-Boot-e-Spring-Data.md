---
title: Criando uma API Rest com Spring-Boot e Spring-Data
date: 2018-11-24 13:55:31
tags:
- Spring-Boot
- Spring-Data
categories:
- Spring
cover_index: /assets/Criando-uma-API-Rest-com-Spring-Boot-e-Spring-Data-index.png
cover_detail: /assets/Criando-uma-API-Rest-com-Spring-Boot-e-Spring-Data-detail.png
---

**Definições**:
	Para introdução destas tecnologias empregadas neste artigo, vamos esclarecer algumas palavras chaves que irão guiar você daqui para frente.
* **Conceito de API**: A sigla API corresponde às palavras em inglês “Application Programming Interface“. As APIs são como uma “ponte”, servem para conectar/integrar aplicações podendo ser utilizadas para os mais variados tipos de negócios.
API’s são invisíveis aos usuários finais, pois trabalham provendo os dados aos quais serão mostrados pelas interfaces de usuário. No entanto, os profissionais de programação conhecem por dentro essa tecnologia que é resultado da evolução de diversos sistemas e ferramentas. Aplicativos e softwares de diversos tipos são apenas passíveis de construção por meio dos padrões e especificações disponibilizados pelas APIs.
* **Conceito de REST**: A Representational State Transfer (REST), é uma abstração da arquitetura da World Wide Web, mais precisamente, é um estilo arquitetural que consiste de um conjunto coordenado de restrições arquiteturais aplicadas a componentes, conectores e elementos de dados dentro de um sistema de hipermídia distribuído.
O REST ignora os detalhes da implementação de componente e a sintaxe de protocolo com o objetivo de focar nos papéis dos componentes, nas restrições sobre sua interação com outros componentes e na sua interpretação de elementos de dados significantes.
Ele foi definido oficialmente pela W3C.

* **Spring-Boot**: Spring Boot é um projeto da Spring que veio para facilitar o processo de configuração e publicação de nossas aplicações. Você escolhe os módulos que deseja através dos starters que inclui no pom.xml do seu projeto.

* **Spring-Data**: O Spring Data JPA é um framework que nasceu para facilitar a criação dos nossos repositórios.Ele (o Spring Data JPA) é, na verdade, um projeto dentro de um outro maior que é o Spring Data. O Spring Data tem por objetivo facilitar nosso trabalho com persistência de dados de uma forma geral.

**Aplicação**:
	Uma vez, com os devidos esclarecimentos, vamos criar um projeto com [Spring Initializr](https://start.spring.io):
{% asset_img 1.JPG This is an example image %}

**Detalhes**:
* **Group**: Seria uma forma de descrever o grupo dono do projeto, geralmente utilizado o domínio invertido,porém pode ser nomeado a livre escolha. Ele implicará também no roteamento dos packages do projeto conforme assinalado na figura 3.
* **Artifact**: É o nome do projeto quando for feito a Build.
Obs: Utilizaremos o Maven, porém sinta-se à vontade para usar o Gradle.

Utilizaremos o [STS](https://spring.io/tools) como IDE, ele é uma IDE baseada no [Eclipse](https://www.eclipse.org/downloads/). Contém tudo que é necessário para utilizar com Spring. Para importar seu projeto recém-criado basta abrir o menu: * Arquivo>importar *.
Logo selecione a pasta Maven e a opção Existing Maven Projects, conforme na imagem abaixo:
	{% asset_img 2.JPG This is an example image %}
O Projeto após importação ficará com a seguinte cara:
	{% asset_img 3.JPG This is an example image %}
Iremos criar as seguintes classes e interfaces(Ícone roxo com um "I"):
	{% asset_img 4.JPG This is an example image %}
Após criarmos nossas classes no package *Model* iremos mapear seguindo os seguites códigos:

{% gist 2c4f655740aace59d283a885d8570bcb Cliente.java %}

{% gist 2c4f655740aace59d283a885d8570bcb Compra.java %}

{% gist 2c4f655740aace59d283a885d8570bcb Coleta.java %}

{% gist 2c4f655740aace59d283a885d8570bcb Pastel.java %}

O Spring nos oferece classes para extensão as quais se encarregam de manipular os dados entre a base de dados e o código Java, um exemplo delas é o JpaRepository, necessitamos apenas passar a classe entidade e o lipo do ID dela, no nosso caso: Long.
Você pode utilizar o CrudRepository o qual se comporta de maneira semelhante.

{% gist 2c4f655740aace59d283a885d8570bcb ClienteRepository.java %}

{% gist 2c4f655740aace59d283a885d8570bcb CompraRepository.java %}

{% gist 2c4f655740aace59d283a885d8570bcb ColetaRepository.java %}

{% gist 2c4f655740aace59d283a885d8570bcb PastelRepository.java %}

Com os repositórios criados, iremos utilizar ser métodos e criar classes que serão onde criaremos as regras de negócios, você pode usar uma classe para criar implementações, mas neste caso usaremos apenas uma. Utilizaremos a anotação **@Service** para denominar a classe como sendo um serviço e assim utilizar os repositórios conforme necessário.

{% gist 2c4f655740aace59d283a885d8570bcb ClienteService.java %}

{% gist 2c4f655740aace59d283a885d8570bcb CompraService.java %}

{% gist 2c4f655740aace59d283a885d8570bcb ColetaService.java %}

{% gist 2c4f655740aace59d283a885d8570bcb PastelService.java %}

Com nosso CRUD montado, iremos agora, criar uma classe a qual se encarregará de receber as requisições e passar para a parte de servico, os Controllers. Para denominar uma classe de controller, basta utilizar a anotação **@RestController** e em seguida o **@RequestMapping** o qual receberá um *endpoint*.

Para cada método, será utilizado uma anotação a qual se encarregará de um verbo Http(GET, POST, PUT, DELETE).

Atenção: Foram criados dois métodos semelhantes, um busca algo através de um ID passado via endpoint(Por isso utilizamos a anotação **@PathVariable**) e o outro será passado um parâmetro http(daí a necessidade da anotação **@RequestParam**), mostrarei a diferença mais à diante, você pode escolher o qual achar melhor para sua aplicação.

{% gist 2c4f655740aace59d283a885d8570bcb ClienteController.java %}

{% gist 2c4f655740aace59d283a885d8570bcb CompraController.java %}

{% gist 2c4f655740aace59d283a885d8570bcb ColetaController.java %}

{% gist 2c4f655740aace59d283a885d8570bcb PastelController.java %}

A fim de haver dados para teste, foi criado uma classe para efetuar a carga de dados:

{% gist 2c4f655740aace59d283a885d8570bcb Carga.java %}

Após o término das classes, rode o projeto através do botão "Play" verde ou através do comando:

{% codeblock %}
mvnw spring-boot:run
{% endcodeblock %}

Após a mensagem de started, poderá executar o [Postman](https://www.getpostman.com) (Ferramenta para teste de endpoints e para efetuar requisições):
	{% asset_img 5.JPG This is an example image %}

Vamos testar inserir a seguinte url com o verbo "GET":
{% codeblock %}
http://localhost:8080/cliente/listar
{% endcodeblock %}
Iremos obter o seguinte resultado:
	{% asset_img 6.JPG This is an example image %}

Após, testaremos os dois métodos GET. No primeiro caso passaremos o ID através da url
{% codeblock %}
http://localhost:8080/cliente/buscar/1
{% endcodeblock %}
Obteremos o seguinte resultado:
	{% asset_img 7.JPG This is an example image %}

Agora removeremos o ID e iremos na aba params do Postman e escreveremos "clienteId" e "1" em key e value conforme demonstrado na imagem:
	{% asset_img 8.JPG This is an example image %}
Obteremos o seguinte resultado:
	{% asset_img 9.JPG This is an example image %}

Para passarmos um objeto, utilizaremos o verbo POST e escreveremos o "body" do objeto:
{% codeblock %}
{
    "nome": "Felipe",
    "coletas": [],
    "compras": []
}
{% endcodeblock %}
Assim, seu postman ficará semelhante a imagem:
	{% asset_img 10.JPG This is an example image %}
Após, eviaremos para a seguinte url:
{% codeblock %}
http://localhost:8080/pastel/inserir
{% endcodeblock %}
Receberemos o mesmo como retorno com o ID criado:
	{% asset_img 11.JPG This is an example image %}

Você poderá testar os demais endpoints, e criar outros conforme necessitar. Sua API REST está feita, assim poderá consumir por um client web ou mobile. Caso tenha ficado com alguma dúvida, digite nos comentários ou envie via email!

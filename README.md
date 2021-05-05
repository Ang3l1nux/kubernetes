# Project K8S - Start with docker concepts

<h2> 1 - Create files </h2>

package.json

```
{
    "name": "simple-node",
    "version": "1.0.0",
    "description": "A sample simple application for Kubernetes Up & Running",
    "main": "server.js",
    "scripts": {
        "start": "node server.js"
    },
    "author": "",
    "dependencies": {
        "express": "^4.17.1"
    }
}
```
server.js
```
var express = require('express');

var app = express();
app.get('/', function (req, res) {
    res.send('Hello World!');
});
app.listen(3000, function () {
    console.log('Listening on port 3000!');
    console.log(' http://localhost:3000');
});
```
<h2> 2 - Install NODE, NPM </h2>

[node-install](https://nodejs.org/en/download/)

<h2> 3 - Estabelecer dependencias com o Express</h2>

```
npm install express --save
```
<h2> 4 - Create .dockerignore para não mandar os modules para o container</h2>

Adicione no arquivo o diretorio
```
node_modules
```
<h2> 5 - Create Dockerfile</h2>

```
FROM node:10
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
CMD [ "npm", "start" ]
```

<h2> 6 - Build image</h2>

```
docker build -t simple-node .
```
<h2> 7 - Run Container</h2>

```
docker run --rm -p 3000:3000 simple-node
```
<h2> 8 - Open Browser</h2>
http://localhost:3000

<br>
<br>
<br>

<h3> Repo the project, book - Kubernetes-Up-And-Running </h3>

[github](https://github.com/kubernetes-up-and-running/kuard)


<h1> Termos </h1>

* artefacto ou objeto    
são os arquivos que dão origem ao produto final, os yamls, json, dockerfile, etc.   
Também pode ser considerado um artefato um pacote compilado da aplicação.

* container runtime   
é o software que executa os containers propriamente ditos e gerencia as imagens do mesmo em um determinado node

* libs ou bibliotecas    
é uma coleção de subprogramas utilizados no desenvolvimento de software. Bibliotecas contém código e dados auxiliares, que provém serviços a programas independentes, o que permite o compartilhamento e a alteração de código e dados de forma modular.

* framework    
Um framework possui várias funcionalidades prontas, e normalmente já possuem um fluxo de trabalho ou estrutura a serem seguidos. É algo bem mais abstrato do que uma biblioteca. Isso realmente confunde muitas pessoas. Por exemplo, o jQuery se autodenominava um framework, mas já faz um bom tempo que ele se chama de biblioteca.    
O foco dos frameworks é mais amplo que das bibliotecas. Aliás, um framework pode ser feito a partir de uma coleção de padrões, APIs e até mesmo de bibliotecas.    
Só para exemplificar, o Angular, framework JavaScript para desenvolvimento de aplicações, é feito a partir de bibliotecas de animação, requisições http, internacionalização, testes, tratamento de dados em formulários, reatividade, roteamento, etc.

* código fonte    
código fonte é um conjunto de instruções escritas em determinada linguagem que tem a função de dizer ao computador o que ele deve fazer.

* CI       
A Integração Contínua, ou apenas o CI (Continuous Integration) como é conhecida, “é uma prática de desenvolvimento de software na qual você compila e testa software toda vez que um desenvolvedor envia código para a aplicação, e isso acontece várias vezes ao dia”. [ref](https://gabriel-faraday.medium.com/o-que-%C3%A9-ci-cd-onde-eu-uso-isso-57e9b8ad8c73)

* CD        
A Entrega Contínua, ou apenas CD (Continuos Delivery), como é conhecido, “é uma abordagem de engenharia de software na qual a integração contínua, testes automatizados e recursos de implantação automatizada permitem que o software seja desenvolvido e implementado de forma rápida, confiável e repetitiva com intervenção humana mínima. Ainda assim, a implantação na produção é definida estrategicamente e acionada manualmente ”. [ref](https://gabriel-faraday.medium.com/o-que-%C3%A9-ci-cd-onde-eu-uso-isso-57e9b8ad8c73)  

* Registry    
é um repositorio onde vão ficar as imagens dos containers

* imagem  
é o template (imagine uma classe em OOP) para rodar um container.    
Você precisa baixar as imagens para rodar os containers ou pegar de algum lugar (como passar de um PC pro outro pelo Pen Drive, por exemplo) e telas em seu repositório local para que o Docker utilize para criar um container quando você roda o docker run....    
As imagens Docker ficam armazenadas no Docker Hub (registry) e, para baixar uma, funciona igualzinho utilizar o Git com Github. [ref](https://woliveiras.com.br/posts/imagem-docker-ou-um-container-docker/)

* container     
O Container é uma instância de uma Imagem em execução naquele momento. [ref](https://woliveiras.com.br/posts/imagem-docker-ou-um-container-docker/)

* sistema de arquivos overlay    
são sistemas em camadas que se sobrepõe ex. (AUFS, Overlay, Overlay1). [ref-1](https://itharley.com/a-b-c-docker-capitulo-3/) [ref-2](https://stack.desenvolvedor.expert/appendix/docker/armazenamento.html)

* efêmero    
Algo temporário, exemplo de disco efêmero numa ec2 da aws que morre junto com a ec2 caso ela seja destruída.

* persistente    
Algo que dura ficará persistido, exemplo de disco se a ec2 for destruída permanece lá.

* cluster     
Cluster é um termo em inglês que significa “aglomerar” ou “aglomeração” e pode ser aplicado em vários contextos. No caso da computação, o termo define uma arquitetura de sistema capaz combinar vários computadores para trabalharem em conjunto ou pode denominar o grupo em si de computadores combinados.

* manifesto    
Um arquivo de manifesto do Kubernetes compreende instruções em um arquivo yaml ou json que especificam como implantar um aplicativo no nó ou nos nós em um cluster do Kubernetes. As instruções incluem informações sobre a implantação do Kubernetes, o serviço Kubernetes e outros objetos do Kubernetes a serem criados no cluster. O manifesto também é conhecido como uma especificação de pod ou como um arquivo deployment.yaml (embora outros nomes de arquivos sejam permitidos). Os parâmetros a serem incluídos em um arquivo de manifesto do Kubernetes estão descritos na [documentação do Kubernetes](https://kubernetes.io/docs/home/).

* imutável    
que não está sujeito a mudar; permanente, constante, imudável.    
A “infraestrutura imutável”, combinada com o conceito de “infraestrutura como código”, possibilita, inclusive, com ferramentas como a Packer, da [HashiCorp](https://www.hashicorp.com/), que apliquemos as mesmas estratégias de CI/CD que já aplicamos com sucesso no desenvolvimento de aplicações

* encapsulamento / empacotamento    
O ato de empacotar ao mesmo tempo dados e objetos é denominado encapsulamento. O objeto esconde seus dados de outros objetos e permite que os dados sejam acessados por intermédio de seus próprios métodos. Isso é chamado de ocultação de informações (information hiding). [ref](http://www.macoratti.net/net_oocb.htm)


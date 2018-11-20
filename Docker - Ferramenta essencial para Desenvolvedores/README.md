<a href="https://www.udemy.com/curso-docker/" target="_blank">Link do Curso</a>

<a href="https://github.com/cod3rcursos/curso-docker" target="_blank">Link do Repositório do Curso</a>

----------------------------------------------------------------------
<h1>Seção 02 - Conceitos</h1>

<h2>O que é Docker?</h2>

* É uma tecnologia de virtualização, mas não é um sistema de virutalização tradicional, baseado em máquinas virtuais.

* O docker é uma engine de administração de containers.

* O container é um ambiente isolado, mas que utiliza o mesmo kernel do sistema e vários recursos são compartilhados. Os containers possuem necessidade de memória e processamento muito menor do que uma máquina virtual, além de ser inicializado rapidamente.

* Utiliza os SErviços do LXC (Linux COntainers).

* Open Source e desenvolvida na linguagem GO.

* Sistema de VIrtualização Baseado em Software (SO).

* Host e Container compartilham o Kernel, como outras bibliotecas também.

* Empacota Software com vários níveis de Isolamento. Quantidade de memória, processamento, rede, endereço e etc.

<h2>Por que não uma VM?</h2>

* Start do container é muito mais rápida que uma VM.

* Quantidade de memória e processamento muiot menor que uma VM.

* Manter mesma vantagens da VM e consumo muito menor.

<img src="imgs/01.png"/>
<img src="imgs/02.png"/>

* A tecnologia LXC para criar containers já existia a muito tempo, a dificuldade era que precisava ter um conhecimento muito profundo para conseguir gerenciar esses containers, o docker veio para facilitar essa utilização.


<h2>O que são containers?</h2>

* Segregação de processos no mesmo Kernel (Isolamento).

* Sistemas de arquivos criados a partir de uma imagem.

* Ambientes leve e portáteis no qual aplicações são executadas.

* Encapsula todos os binários e bibliotecas necessárias para execução de uma App.

* Algo entre o chroot (redefine uma pasta raiz e aprisiona o processo dentro desse diretório) e uma VM.

* Ser o mais minimalista possível. Executar um container para apenas uma aplicação. É um bom padrão.

<h2>O que são imagens Docker?</h2>

* Modelo de sistema de arquivo somente-leitura usado para criar containers.

* Imagens são criadas através de um processo chamado build. Existe também o commit, mas não é uma boa prática utilizar. O build tem um descritor.

* São armazenados em repositórios no Registry. DockerHub, repositórios oficiais do Docker.

* São compostas por uma ou mais camadas (layers).

* Uma camada repsenta uma ou mais mudanças no sistema de arquivo.

* A junção dessas camadas formam a imagem.

* Apenas a última cmada pode ser alterada quando o container for iniciado.

* AUFS (Advanced multi-layered unification filesystem) é muito usado.

* O grande objetivo dessa estratégia de dividir uma imagem em camadas é o reuso.

* É possível compor imagens a partir de camdas de outras imagens.


<h2>Imagem vs Container</h2>

* Orientação Objeto:
	* Classe = Imagem - Modelo.
	* Objeto = Container - Processo usada na memória.

<h2>Arquitetura</h2>

<img src="imgs/03.png"/>

---------------------------------------------------------------------------
<h1>Seção 03 - Instalação</h1>

<h2>Visão Geral</h2>

<img src="imgs/04.png"/>

* Verificar instalação pela documentação do Docker.

* Docker CE - Community Edition.


---------------------------------------------------------------------------

<h1>Seção 04 - Uso Básico do Docker</h1>

<h2>Hello World</h2>

* Comando: docker --help

* Comando: docker container run hello-world

<h2>Comando run</h2>

* Versão nova dos comandos.

* A partir do comando run a gente baixou uma imagem, executamos o container e o container foi mostrado.

* Foi feito o cache da imagem.

* Executar o container de forma interativa.

* Comando run é a concatenação de 4 comandos:
	* docker image pull - baixar a imagem do registry para a máquina local.
	* docker container create - Criação do container.
	* docker container start - Inicialização do container.
	* docker container exec - Execução do container em modo interativo.

<h2>Ferramentas diferentes</h2>

* Modo interativo - Para experimentos - Não é o modo prioritário. O modo prioritário é o modo daemon.

* Comando: bash --version

* docker container run debian bash --version

* docker container ps - Mostra os containers em execução

* docker container ps -a - Mostra os todos os containers independente dos status.

* Ele executa o comando e depois fecha o container.

* docker container run --rm debian - Quando terminar o processo removera da lista de containers.

<h2>Run cria sempre novos containers</h2>

* O comando run sempre cria novos containers.

* docker container run -it debian bash (modo interativo e acesso ao terminal)

* Dentro do terminal do container
	* touch curso-docker.txt
	* ls curso-docker.txt
	* exit

* Executa o docker container run it debian bash (de novo) e da um ls curso-docker.txt. Não existirá

<h2>Containers devem ter nomes únicos</h2>

* docker container run --help

* docker container run --name mydev -it debian bash

* Saia do container (exit)

* Execute novamente o comando docker container run --name mydev -it debian bash

* Vai ocorrer um erro, pois já existe o mesmo nome.

* containers precisam ter nomes únicos e o método run sempre cria um novo container.

<h2>Reutilizar containers</h2>

* docker container ls //lista os containers que foram criados

* docker container ls -a //mostra todos independentemente dos status

* docker container start -ai mydeb //apache e modo interativo

* touch curso-docker.txt //CRIA ARQUIVO NO CONTAINER

* Sair e entrar novamente e verificar que o arquivo ainda existe. O arquivo ainda continuara lá.

<h2>Cedo, surdo e mudo, só que não</h2>

* Não faz sentido ter um container completamente isolado.

* Capaz de expor uma porta dentro do container.

* Compartilhar uma pasta do container para a máquina host.

* Compartilha arquivos do container para a máquina host e vice-versa.

* Comunicação entre os próprios containers e todos conversando entre si.

* Um container que não tem um minimo de comunicação não tem sentido.

* Isolamento controlado. Minimalista.

<h2>Mapear portas dos containers</h2>

* docker container run -p 8080:80 nginx //De fora do container irá acessar a 8080 e o serviço dentro está na porta 80.

* É possível acessar o localhost:8080 e acessará o nginx que está na porta 80.

<h2>Mapear diretórios para o container</h2>

* Criar um diretório na máquina host

* mkdir curso-docker

* cd curso-docker

* mkdir ex-volume

* cd ..

* code .

* docker container run -p 8080:80 -v $(pwd)/not-found:/usr/share/nginx/html //-v mapeia o volume passa a pasta do host que você quer mapear : a pasta que você quer dentro do container


<h2>Rodar um servidor web em background</h2>

* Modo daemon //MODO BACKGROUND

* Modo princípal para o Docker.

* docker container run -d --name ex-daemon-basic -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx //-d daemon

* Retornará o ID do container que estará executando

* docker container ps

* docker container stop ex-daemon-basic //PARA O CONTAINER

<h2>Gerenciar o container em background</h2>

* docker container stop ex-daemon-basic

* docker container start ex-daemon-basic

* docker container restart ex-daemon-basic

* É possível que ao inves de pegar o nome do container, é possível pegar o id do container.

<h2>Manipulação de containers em modo daemon</h2>

* Comandos alias.

* docker container ls //SINTAXE NOVA

* docker container list //SINTAXE NOVA

* docker container ps //SINTAXE NOVA

* docker ps //SINTAXE ANTIGA

* docker container ls -a //TODOS CONTAINERS

* docker container list -a //MESMO DE CIMA

* docker container ps -a //MESMA COISA

* docker ps -a //ANTIGO

* docker container start NOME_CONTAINER

* docker container inspect NOME_CONTAINER // FORMATO JSON VARIAS CARACTERÍSTCAS QUE SE BASEIA O CONTAINER

* docker container exec NOME_CONTAINER uname -or //TIPO QUE ESTÁ SENDO EXECUTADO NO CONTAINER

<h2>Nova sintaxe do Docker Client</h2>

* Comando semelhantes que fazem as mesmas coisas. Fizeram isso para deixar mais claro.

* docker image ls //LISTA AS IMAGENS

* docker container ls //LISTA CONTAINERS

* docker rmi ID_IMAGEM //SINTAXE ANTIGA //REMOVE IMAGEM

* docker image rm ID_IMAGEM //SINTAXE NOVA

------------------------------------------------------------------------
<h1>Seção 05 - Deixando de ser apenas um usuário</h1>

























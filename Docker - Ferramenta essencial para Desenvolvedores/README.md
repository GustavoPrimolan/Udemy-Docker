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











# Modelo de previsão

Segui o exemplo da professora no curso e esse passo passo.

Modelo de previsão com seus devidos pontos de extremidade configurados

Eu aprendi a realizar as seguintes tarefas:

Criar e carregar um conjunto de dados.
Configurar e executar um experimento de ML automatizado.
Especificar configurações de previsão.
Explorar os resultados do experimento.
Implantar o melhor modelo.

Baixei o arquivo de dados bike-no.csv

Entrei no Estúdio do Azure Machine Learning.

Selecionei a assinatura e o workspace criado.

Selecionei Introdução.

No painel esquerdo, selecionei ML Automatizado na seção Criar.

Selecionei +Novo trabalho de ML automatizado.

Criei e carreguei um conjunto de dados
Antes de configurar meu experimento, carreguei o arquivo de dados no workspace na forma de um conjunto de dados do Azure Machine Learning. Essa ação permite que eu garanta que os dados estejam formatados corretamente para o experimento.

No formulário Selecionei conjunto de dados, selecionei De arquivos locais na lista suspensa +Criei conjunto de dados.

No formulário Informações básicas, dei um nome ao conjunto de dados e forneci uma descrição (opcional). O tipo de conjunto de dados deverá usar Tabela como padrão, pois o ML automatizado no Azure Machine Learning Studio atualmente só dá suporte a conjuntos de dados de tabela.

Selecionei Avançar na parte inferior esquerda

No formulário Seleção de armazenamento de dados e de arquivo, selecionei o armazenamento de dados padrão que foi configurado automaticamente durante a criação do workspace, workspaceblobstore (Armazenamento de Blobs do Azure) . Esse é o local de armazenamento onde eu carreguei o arquivo de dados.

Selecionei Carregar arquivos no menu suspenso Carregar.

Escolhi o arquivo bike-no.csv no computador local. Esse é o arquivo que eu baixei como pré-requisito.

Selecionei Avançar

Após a conclusão do upload, o formulário Configurações e visualização foi pré-populado com base no tipo de arquivo.

Verifiquei se o formulário Configurações e visualização é populado conforme mostrado a seguir e selecionei Avançar.

Campo	Descrição	Valor para o tutorial
Formato de arquivo	Define o layout e o tipo de dados armazenados em um arquivo.	(Delimitado)
Delimitador	Um ou mais caracteres para especificar o limite entre regiões separadas e independentes em texto sem formatação ou outros fluxos de dados.	Vírgula
Codificação	Identifica qual tabela de esquema de bit para caractere usar para ler meu conjunto de dados.	UTF-8
Cabeçalhos da coluna	Indica como os cabeçalhos do conjunto de dados, se houver, serão tratados.	Somente o primeiro arquivo tem cabeçalhos
Ignorar linhas	Indica quantas linhas, se houver, serão ignoradas no conjunto de registros.	(Nenhum)
O formulário Esquema permite configurar ainda mais os dados do experimento.

Para este exemplo, optei por ignorar as colunas casual e registrada. Essas colunas são um detalhamento da coluna cnt e, portanto, não as incluímos.

Além disso, para este exemplo, mantive os padrões das Propriedades e do Tipo.

Selecionei Avançar.

No formulário Confirmar detalhes, verifiquei se as informações correspondem ao que foi previamente preenchido nos formulários Informações básicas e Configurações e visualização.

Selecionei Criar para concluir a criação do conjunto de dados.

Selecionei seu conjunto de dados quando ele aparecer na lista.

Selecionei Avançar.

Configurar trabalho
Depois de carregar e configurar meus dados, configurei o destino de computação remota e selecionei qual coluna nos dados eu quero prever.

Preenchi o formulário Configurei trabalho da seguinte maneira:
Inseri um nome de experimento: automl-bikeshare

Selecionei cnt como a coluna de destino, o que eu queira prever. Essa coluna indica o número total de aluguéis de compartilhamento de bicicletas, no meu caso moto.

Selecionei cluster de computação como meu tipo de computação.

Selecionei +Novo para configurar o destino de computação. O ML automatizado só dá suporte à Computação do Azure Machine Learning.

Preenchi o formulário Selecionei máquina virtual para configurar a computação.

Campo	Descrição	Valor para o tutorial
Tipo de máquina virtual	Selecionei a prioridade que o experimento deve ter	Dedicado
Tipo de máquina virtual	Selecionei o tipo da máquina virtual da computação.	CPU (Unidade de Processamento Central)
Tamanho da máquina virtual	Selecionei o tamanho da máquina virtual da computação. É fornecida uma lista de tamanhos recomendados com base em meus dados e no tipo de experimento.	Standard_DS12_V2
Selecionei Avançar para preencher o Formulário Definir configurações.

Campo	Descrição	Valor para o tutorial
Nome da computação	Um nome exclusivo que identifiquei o contexto de computação.	bike-compute
Mín./máx. de nós	Para criar um perfil de dados, eu especifiquei um ou mais nós.	(Número mín. de nós: 1
Número máx. de nós: 6)
Segundos de espera antes de reduzir verticalmente	Tempo de espera antes que o cluster seja reduzido verticalmente automaticamente para a contagem mínima de nós.	120 (padrão)
Configurações avançadas	Definições para configurar e autorizar uma rede virtual para meu experimento.	(Nenhum)
Selecionei Criar para obter o destino de computação.

Isso levou alguns minutos para ser concluído.

Após a criação, selecionei o novo destino de computação na lista suspensa.

Selecionei Avançar.

Selecionei configurações de previsão
Conclui a configuração do experimento de ML automatizado especificando o tipo de tarefa de aprendizado de máquina e as definições de configuração.

No formulário Tipo de tarefa e configurações, selecionei Previsão de série temporal como o tipo de tarefa de aprendizado de máquina.

Selecionei data como a Coluna de tempo e deixei os Identificadores de série temporal em branco.

A Frequência na qual os dados históricos são coletados. Mantive a Detecção automática selecionada.

O horizonte de previsão é o período de tempo no futuro que eu deseja prever. Desmarquei a Detecção Automática e digitei 14 no campo.

Selecionei Exibir definições de configuração adicionais e preenchi os campos da seguinte maneira. Essas configurações são destinadas a controlar melhor o trabalho de treinamento e especificar configurações para sua previsão. Caso contrário, os padrões são aplicados com base na seleção e nos dados de experimento.

Configurações adicionais	Descrição	Valor para o tutorial
Métrica principal	Métrica de avaliação pela qual o algoritmo de aprendizado de máquina foi medido.	Raiz do erro quadrático médio normalizado
Expliquei o melhor modelo	Mostrei automaticamente a explicabilidade no melhor modelo criado pelo ML automatizado.	(Habilitei)
Algoritmos bloqueados	Algoritmos que eu deseja excluir do trabalho de treinamento	Árvores aleatórias extremas
Configurações adicionais de previsão	Essas configurações ajudam a aprimorar a precisão do modelo.

Retardos de destino de previsão: até que ponto no passado eu deseja construir os retardos da variável de destino
Janela de rolagem de destino: especifica o tamanho da janela de rolagem na qual recursos, como máx., mín. e soma, são gerados.	

Retardos do destino de previsão: (nenhum)
Tamanho da janela de rolagem de destino: (nenhum)
Critério de saída	Se um critério for atendido, o trabalho de treinamento será interrompido.	Tempo do trabalho de treinamento (horas): 3
Limite de pontuação da métrica: (nenhum)
Simultaneidade	O número máximo de iterações paralelas executadas por iteração	Máximo de iterações simultâneas: 6
Selecionei Salvar.

Selecionei Avançar.

No formulário [Opcional] Validei e testei,

Selecionei a validação cruzada k-fold como seu Tipo de validação.
Selecionei 5 como Número de validações cruzadas.
Executei o experimento
Para executar o experimento, selecionei Concluir. A tela Detalhes do trabalho foi aberta com o Status do trabalho na parte superior ao lado do número do trabalho. Esse status é atualizado conforme o progresso do experimento. Também aparecem notificações no canto superior direito do estúdio para informar eu sobre o status do experimento.

 Importante

A preparação do trabalho de experimento leva de 10 a 15 minutos. Durante a execução, são necessários mais 2 a 3 minutos para cada iteração.

Em produção, provavelmente, eu terei tempo para outras tarefas, pois esse processo é demorado. Enquanto eu aguardei, comecei a explorar os algoritmos testados na guia Modelos conforme eles são concluídos.

Explorar modelos
Naveguei até a guia Modelos para ver os algoritmos (modelos) testados. Por padrão, os modelos são ordenados pela pontuação da métrica à medida que são concluídos. Para este tutorial, o modelo com a pontuação mais alta com base na métrica Raiz do erro quadrático médio normalizado escolhida é exibido no início da lista.

Enquanto eu aguardei a conclusão de todos os modelos de experimento, selecionei o Nome do algoritmo de um modelo concluído para explorar meus detalhes de desempenho.

O seguinte exemplo naveguei até selecionar um modelo na lista de modelos que o trabalho criou. Em seguida, selecionei as guias Visão Geral e Métricas para exibir as propriedades, as métricas e os gráficos de desempenho do modelo selecionado.

Run Overview

Implantar o modelo
O machine learning automatizado no estúdio do Azure Machine Learning permite que eu implante o melhor modelo como um serviço Web em algumas etapas. A implantação é a integração do modelo para que ele possa prever novos dados e identificar possíveis áreas de oportunidade.

Para este experimento, a implantação em um serviço Web significa que a empresa de compartilhamento de bicicletas, no caso moto, agora tem uma solução da Web iterativa e escalonável para prever a demanda de aluguel de compartilhamento de moto.

Quando a execução teve concluída, voltei para a página de execução pai selecionando Trabalho 1 na parte superior da minha tela.

Na seção Resumo do melhor modelo, foi selecionado o melhor modelo no contexto desse experimento com base na Métrica da raiz do erro quadrático médio.

Implantei esse modelo, mas saiba que a implantação demora cerca de 20 minutos para ser concluída. O processo de implantação envolve várias etapas, incluindo o registro do modelo, a geração de recursos e a configuração deles para o serviço Web.

Selecionei o melhor modelo para abrir a página específica do modelo.

Selecionei o botão Implantar localizado na área superior esquerda da tela.

Preenchi o painel Implantar um Modelo da seguinte maneira:

Campo	Valor
Nome da implantação	bikeshare-deploy
Descrição da implantação	implantação da demanda de compartilhamento de bicicletas/moto
Tipo de computação	Selecionei ACI (Instância de Computação do Azure)
Habilitei autenticação	(Desabilite).
Usei ativos da implantação personalizada	(Desabilite). A desabilitação permite que o arquivo de driver padrão (script de pontuação) e o arquivo de ambiente sejam gerados automaticamente.
Para este exemplo, usei os padrões fornecidos no menu Avançado.

Selecionei Implantar.

Uma mensagem de êxito verde foi exibida na parte superior da tela Trabalho indicando que a implantação foi iniciada com êxito. O progresso da implantação pode ser encontrado no painel de Resumo do modelo em Status da implantação.

Após o êxito da implantação, eu terei um serviço Web operacional para gerar previsões.




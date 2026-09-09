To-Do List Android
Descrição do projeto

Este projeto consiste em um aplicativo Android de gerenciamento de tarefas desenvolvido em Kotlin utilizando Jetpack Compose.

O objetivo da aplicação é permitir que o usuário organize suas tarefas de forma simples, podendo visualizar as tarefas cadastradas, criar novas tarefas, editar informações, marcar tarefas como concluídas ou pendentes e excluir registros.

O projeto utiliza uma arquitetura dividida em camadas para separar a interface, a lógica da aplicação e o acesso aos dados.

Tecnologias utilizadas

O projeto utiliza as seguintes tecnologias:

Kotlin: linguagem utilizada no desenvolvimento da aplicação Android.
Jetpack Compose: utilizado para construção das telas e componentes da interface.
Room: responsável pela persistência local das tarefas.
Coroutines e Flow: utilizados para trabalhar com operações assíncronas e atualização dos dados.
ViewModel: responsável por manter e disponibilizar o estado da aplicação para a interface.
Navigation Compose: utilizado para controlar a navegação entre a tela de listagem e o formulário de tarefas.
Repository: utilizado como camada intermediária entre a ViewModel e o acesso ao banco de dados.
TarefaRepository

A classe TarefaRepository é responsável por centralizar o acesso aos dados das tarefas.

Ela utiliza o DAO da aplicação para executar as operações relacionadas ao banco de dados, evitando que a ViewModel acesse diretamente a camada de persistência.

Entre suas responsabilidades estão:

obter a lista de tarefas;
inserir uma nova tarefa;
atualizar uma tarefa existente;
excluir uma tarefa.

Dessa maneira, a aplicação mantém uma separação entre a lógica da interface e a camada responsável pelos dados.

TarefaViewModel

A TarefaViewModel é responsável por fazer a comunicação entre a interface da aplicação e o TarefaRepository.

Ela disponibiliza para as telas a lista de tarefas como um estado observável e também fornece as operações necessárias para manipular esses dados.

Por meio da ViewModel, a interface consegue:

observar as tarefas cadastradas;
cadastrar novas tarefas;
editar tarefas existentes;
alterar o estado de conclusão de uma tarefa;
excluir tarefas.

A ViewModel também ajuda a preservar o estado da interface durante mudanças no ciclo de vida da aplicação.

Na MainActivity, a TarefaViewModel é criada utilizando sua Factory, que recebe o contexto da aplicação e fornece as dependências necessárias para funcionamento da ViewModel.

ListaTarefasScreen

A ListaTarefasScreen é responsável por exibir as tarefas cadastradas.

As tarefas são apresentadas utilizando uma LazyColumn, permitindo exibir os registros de maneira eficiente.

A tela observa o estado disponibilizado pela TarefaViewModel e atualiza automaticamente a interface quando ocorre alguma alteração nos dados.

A partir dessa tela, o usuário pode:

visualizar as tarefas;
marcar ou desmarcar uma tarefa como concluída;
abrir uma tarefa para edição;
excluir uma tarefa;
acessar o formulário para cadastrar uma nova tarefa.

As ações realizadas pelo usuário são enviadas para a ViewModel, que executa as operações necessárias através do Repository.

FormularioTarefaScreen

A FormularioTarefaScreen é utilizada tanto para cadastrar uma nova tarefa quanto para editar uma tarefa existente.

A diferença entre os dois modos é determinada pelo identificador da tarefa recebido pela tela.

Quando não existe uma tarefa selecionada, o formulário funciona no modo de cadastro.

Nesse caso, o usuário informa os dados da nova tarefa e, ao salvar, uma nova tarefa é inserida no banco de dados.

Quando um ID de tarefa existente é recebido, a tela funciona no modo de edição. Os dados da tarefa são carregados para o formulário e podem ser alterados pelo usuário.

Após salvar as alterações, a tarefa é atualizada através da TarefaViewModel.

AppNavigation

A navegação da aplicação é controlada pelo AppNavigation utilizando Navigation Compose.

A aplicação possui duas rotas principais:

lista: responsável por apresentar a ListaTarefasScreen;
formulario: responsável por apresentar a FormularioTarefaScreen.

A navegação permite abrir o formulário tanto para criar uma nova tarefa quanto para editar uma tarefa existente.

No caso de edição, o ID da tarefa é enviado como parâmetro da rota. Dessa forma, a tela de formulário consegue identificar qual tarefa deve ser carregada e editada.

Depois de salvar ou cancelar uma operação, o usuário pode retornar para a tela de listagem.

MainActivity

A MainActivity é o ponto inicial da aplicação.

Dentro do método onCreate, o conteúdo da interface é configurado utilizando Jetpack Compose.

A TarefaViewModel é criada utilizando a Factory da própria ViewModel:

val viewModel: TarefaViewModel = viewModel(
    factory = TarefaViewModel.factory(applicationContext)
)

Em seguida, a aplicação inicia sua estrutura de navegação:

AppNavigation(viewModel = viewModel)

Dessa forma, a MainActivity não apresenta mais o conteúdo padrão criado pelo template do Android Studio. Ela passa a iniciar diretamente o fluxo principal do aplicativo To-Do List.

Funcionamento da aplicação

O fluxo principal da aplicação funciona da seguinte maneira:

Ao abrir o aplicativo, o usuário visualiza a lista de tarefas.
O usuário pode acessar o formulário para cadastrar uma nova tarefa.
Após salvar, a nova tarefa aparece na lista.
Uma tarefa existente pode ser selecionada para edição.
O usuário pode marcar ou desmarcar uma tarefa como concluída.
Uma tarefa também pode ser excluída.
A navegação permite alternar entre a lista e o formulário sem encerrar a aplicação.
Os dados permanecem armazenados localmente utilizando Room.
Como executar o projeto

Para executar o projeto:

Abra o projeto no Android Studio.
Aguarde a sincronização do Gradle.
Caso necessário, utilize File > Sync Project with Gradle Files.
Abra o Device Manager.
Inicie um dispositivo virtual Android.
Aguarde o emulador terminar de inicializar.
Selecione o módulo app.
Clique em Run.
Aguarde a instalação e inicialização do aplicativo no emulador.


Evidências: 
Contidas na pasta evidências dentro de app

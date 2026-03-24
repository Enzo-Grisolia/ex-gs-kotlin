Descrição do Projeto

Este projeto consiste no desenvolvimento de um aplicativo Android utilizando a linguagem Kotlin, com foco na navegação entre múltiplas telas por meio do Jetpack Compose e do Navigation Compose.

A aplicação simula um fluxo básico, iniciando em uma tela de login e permitindo ao usuário acessar um menu principal. A partir desse menu, é possível navegar para outras funcionalidades, como visualização de perfil e consulta de pedidos.

As principais telas implementadas são:

Login: responsável pela entrada do usuário no sistema
Menu: centraliza as opções de navegação
Perfil: exibe dados do usuário recebidos via parâmetros de rota
Pedidos: apresenta informações baseadas em parâmetros enviados via query string

A navegação entre as telas é gerenciada pelo NavController, definido na atividade principal, garantindo um controle centralizado e organizado das rotas.

Além disso, o projeto utiliza Jetpack Compose para construção de interfaces modernas e responsivas, proporcionando uma experiência mais dinâmica.

Outro ponto importante é a passagem de dados entre telas, utilizando:

Parâmetros de rota (dados obrigatórios)
Query string (dados opcionais)

Dessa forma, o projeto demonstra na prática conceitos fundamentais do desenvolvimento Android moderno, como composição de interfaces, navegação estruturada e organização de código.

Objetivo da Prova

O objetivo desta prova é avaliar a capacidade de aplicar conceitos de programação em Kotlin, incluindo:

Lógica de programação
Organização de código
Boas práticas de desenvolvimento

Além disso, busca validar o uso de versionamento com Git, evidenciando a evolução incremental do projeto ao longo das etapas.

Evolução do Projeto
 Etapa 1 – Parâmetro na rota (Perfil)
composable(route = "perfil/{nome}") {
val nome: String? = it.arguments?.getString("nome", "Usuário Genérico")
PerfilScreen(modifier = Modifier.padding(innerPadding), navController, nome!!)
onClick = { navController.navigate("perfil/Fulano de Tal") },

Nesta etapa, a navegação para a tela de perfil foi aprimorada com o uso de parâmetros.

A rota "perfil" foi substituída por "perfil/{nome}", permitindo enviar o nome do usuário durante a navegação. Esse valor é recuperado com um valor padrão e exibido na PerfilScreen.

 Etapa 2 – Uso do parâmetro na tela
fun PerfilScreen(
modifier: Modifier = Modifier,
navController: NavController,
nome: String
) {
text = "PERFIL - $nome",

A PerfilScreen passou a receber o nome como parâmetro, permitindo personalizar o conteúdo exibido.

O texto da tela foi atualizado para incluir o nome do usuário, tornando a interface mais dinâmica.

 Etapa 3 – Query string (Pedidos)
composable(
route = "pedidos?cliente={cliente}",
arguments = listOf(navArgument("cliente") {
defaultValue = "Cliente Genérico"
})
) {
PedidosScreen(modifier = Modifier.padding(innerPadding), navController, it.arguments?.getString("cliente"))
PerfilScreen(
modifier = Modifier.padding(innerPadding),
navController,
nome!!
)

Nesta etapa, foi implementada a navegação utilizando query string.

A rota "pedidos?cliente={cliente}" permite enviar um parâmetro opcional. Foi definido um valor padrão ("Cliente Genérico"), garantindo funcionamento mesmo sem envio explícito.

O valor é recuperado e repassado para a PedidosScreen.

 Etapa 4 – Uso do parâmetro na tela de pedidos
fun PedidosScreen(modifier: Modifier = Modifier, navController: NavController, cliente: String?) {
text = "PEDIDOS - $cliente",

A PedidosScreen foi modificada para receber o parâmetro cliente.

O texto exibido foi atualizado para incluir o nome recebido, tornando a tela mais informativa.

 Etapa 5 – Envio de parâmetro na navegação
onClick = { navController.navigate("pedidos?cliente=Cliente XPTO") },

O botão passou a enviar o nome do cliente na navegação.

Isso permite que a tela de pedidos exiba informações personalizadas com base no valor recebido.

 Etapa 6 – Múltiplos parâmetros (Perfil)
PedidosScreen(
modifier = Modifier.padding(innerPadding),
navController,
it.arguments?.getString("cliente")
)
composable(
route = "perfil/{nome}/{idade}",
arguments = listOf(
navArgument("nome") { type = NavType.StringType },
navArgument("idade") { type = NavType.IntType }
)
) {
val idade: Int? = it.arguments?.getInt("idade", 0)
idade!!

Nesta etapa, a rota foi expandida para aceitar dois parâmetros: nome e idade.

Os argumentos foram tipados corretamente (String e Int) e recuperados com valores padrão.

 Etapa 7 – Envio e uso da idade
onClick = { navController.navigate("perfil/Fulano de Tal/27") },
idade: Int
text = "PERFIL - $nome tem $idade anos",

A navegação foi atualizada para enviar dois valores (nome e idade).

A PerfilScreen passou a receber esse novo parâmetro e exibi-lo na interface, deixando a informação mais completa.

Conclusão

O projeto demonstra de forma prática a implementação de navegação entre telas no Android utilizando Jetpack Compose.

Foram aplicadas diferentes estratégias de passagem de dados, como parâmetros de rota e query string, evidenciando suas diferenças:

Parâmetros de rota: utilizados para dados obrigatórios
Query string: utilizada para dados opcionais

Além disso, o uso do NavController permitiu um fluxo de navegação organizado, enquanto o Jetpack Compose proporcionou uma interface moderna e eficiente.

O desenvolvimento incremental do projeto, aliado ao uso de Git, evidencia a evolução das funcionalidades e o domínio dos conceitos propostos.

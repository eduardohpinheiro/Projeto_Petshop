# Projeto Petshop

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_CLIENTES 100
#define MAX_PRODUTOS 100

//Código parte clientes
typedef struct {
    char nome[50];
    char email[100];
    char senha[20];
} Cliente;

typedef struct {
    char nome[50];
    float preco;
} Produto;

typedef struct {
    Produto produto;
    int quantidade;
} ItemCarrinho;

Cliente clientes[MAX_CLIENTES];
int numClientes = 0;

Produto produtos[MAX_PRODUTOS];
int numProdutos = 0;

ItemCarrinho carrinho[MAX_PRODUTOS];
int numItensCarrinho = 0;

void criarConta() {
    Cliente novoCliente;
    printf("==== Criacao de Conta ====\n");
    printf("Nome: ");
    scanf("%s", novoCliente.nome);
    printf("Email: ");
    scanf("%s", novoCliente.email);
    printf("Senha: ");
    scanf("%s", novoCliente.senha);

    if (numClientes < MAX_CLIENTES) {
        clientes[numClientes++] = novoCliente;
        printf("Conta criada com sucesso!\n");
    } else {
        printf("Limite maximo de clientes alcancado.\n");
    }
}

void fazerLogin() {
    char nome[50];
    char senha[20];
    printf("==== Area de Login ====\n");
    printf("Nome: ");
    scanf("%s", nome);
    printf("Senha: ");
    scanf("%s", senha);

    int i;
    for (i = 0; i < numClientes; i++) {
        if (strcmp(clientes[i].nome, nome) == 0 && strcmp(clientes[i].senha, senha) == 0) {
            printf("Login bem-sucedido! Bem-vindo, %s!\n", clientes[i].nome);
            return;
        }
    }

    printf("Dados de login invalidos.\n");
}

void buscarProduto() {
    char nome[50];
    printf("==== Buscar Produto ====\n");
    printf("Nome do produto: ");
    scanf("%s", nome);

    int i;
    for (i = 0; i < numProdutos; i++) {
        if (strcmp(produtos[i].nome, nome) == 0) {
            printf("Produto encontrado: %s (Preco: R$ %.2f)\n", produtos[i].nome, produtos[i].preco);
            return;
        }
    }

    printf("Produto nao encontrado.\n");
}

void exibirCatalogo() {
    int i;
    printf("==== Catalogo de Produtos ====\n");
    for (i = 0; i < numProdutos; i++) {
        printf("%d. %s (Preco: R$ %.2f)\n", i + 1, produtos[i].nome, produtos[i].preco);
    }
}

void adicionarProduto() {
    Produto novoProduto;
    printf("==== Adicionar Produto ====\n");
    printf("Nome: ");
    scanf("%s", novoProduto.nome);
    printf("Preco: ");
    scanf("%f", &novoProduto.preco);

    if (numProdutos < MAX_PRODUTOS) {
        produtos[numProdutos++] = novoProduto;
        printf("Produto adicionado com sucesso!\n");
    } else {
        printf("Limite maximo de produtos alcancado.\n");
    }
}

void realizarPagamento() {
    char email[100];
    char senha[20];

    printf("==== Pagamento Online ====\n");
    printf("Email: ");
    scanf("%s", email);
    printf("Senha: ");
    scanf("%s", senha);

    int i;
    for (i = 0; i < numClientes; i++) {
        if (strcmp(clientes[i].email, email) == 0 && strcmp(clientes[i].senha, senha) == 0) {
            printf("Autenticacao bem-sucedida! Pagamento realizado.\n");
            printf("Itens do carrinho:\n");
            float total = 0;
            for (int j = 0; j < numItensCarrinho; j++) {
                ItemCarrinho item = carrinho[j];
                printf("- Produto: %s (Quantidade: %d, Preco: R$ %.2f)\n", item.produto.nome, item.quantidade, item.produto.preco);
                total += item.quantidade * item.produto.preco;
            }
            printf("Total a pagar: R$ %.2f\n", total);
            printf("Obrigado pela compra!\n");
            numItensCarrinho = 0; // Esvaziar o carrinho após a compra
            return;
        }
    }

    printf("Autenticacao falhou. Pagamento nao realizado.\n");
}

void adicionarAoCarrinho() {
    int indiceProduto;
    int quantidade;
    printf("==== Adicionar ao Carrinho ====\n");
    exibirCatalogo();
    printf("Escolha o numero do produto: ");
    scanf("%d", &indiceProduto);

    if (indiceProduto >= 1 && indiceProduto <= numProdutos) {
        printf("Quantidade: ");
        scanf("%d", &quantidade);

        if (numItensCarrinho < MAX_PRODUTOS) {
            ItemCarrinho novoItem;
            novoItem.produto = produtos[indiceProduto - 1];
            novoItem.quantidade = quantidade;
            carrinho[numItensCarrinho++] = novoItem;
            printf("Produto adicionado ao carrinho com sucesso!\n");
        } else {
            printf("Limite maximo de itens no carrinho alcancado.\n");
        }
    } else {
        printf("Numero de produto invalido.\n");
    }
}

int main() {
    int opcao;

    // Adicionando produtos iniciais
    Produto racao = {"Racao", 50.0};
    produtos[numProdutos++] = racao;

    Produto racaoPremium = {"Racao Premium", 80.0};
    produtos[numProdutos++] = racaoPremium;

    Produto brinquedos = {"Brinquedos", 30.0};
    produtos[numProdutos++] = brinquedos;

    Produto guias = {"Guias", 40.0};
    produtos[numProdutos++] = guias;

    Produto petiscos = {"Petiscos", 20.0};
    produtos[numProdutos++] = petiscos;

    Produto roupas = {"Roupas", 60.0};
    produtos[numProdutos++] = roupas;

    Produto shampo = {"Shampo", 25.0};
    produtos[numProdutos++] = shampo;

    Produto coleiras = {"Coleiras", 35.0};
    produtos[numProdutos++] = coleiras;
    
    Produto produto3 = {"Brinquedo de Corda", 10.0};
    produtos[numProdutos++] = produto3;
    
       Produto produto2 = {"Areia Higienica", 15.0};
    produtos[numProdutos++] = produto2;
    
     Produto produto1 = {"Transportadora", 100.0};
    produtos[numProdutos++] = produto1;
    
     Produto produto4 = {"Coleira com identificação", 40.0};
    produtos[numProdutos++] = produto4;
    
    Produto produto5 = {"Pá higiênica", 40.0};
    produtos[numProdutos++] = produto5;
    
    Produto produto6 = {"Bebedouro automático", 30.0};
    produtos[numProdutos++] = produto6;
    
    Produto produto7 = {"Comedouro automático", 40.0};
    produtos[numProdutos++] = produto7;
    
    Produto produto8 = {"Caminha para cães", 10.0};
    produtos[numProdutos++] = produto8;
    
    Produto produto9 = {"Caminha para gatos", 100.0};
    produtos[numProdutos++] = produto9;
    
    Produto produto10 = {"Brinquedo interativo para cães (disco voador)", 300.0};
    produtos[numProdutos++] = produto10;
    
    Produto produto11 = {"Gaiola para hamsters", 230.0};
    produtos[numProdutos++] = produto11;
    
    Produto produto12 = {"Gaiola para pássaros", 60.0};
    produtos[numProdutos++] = produto12;
    
    Produto produto13 = {"Alpiste", 60.0};
    produtos[numProdutos++] = produto13;
    
    Produto produto14 = {"Mistura de sementes para pássaros", 5.0};
    produtos[numProdutos++] = produto14;
    
    Produto produto15 = {"Papel para forrar a gaiola", 50.0};
    produtos[numProdutos++] = produto15;
    
    Produto produto16 = {"Banheira para pássaros", 70.0};
    produtos[numProdutos++] = produto16;
    
    Produto produto17 = {"Roda de exercícios para hamsters", 40.0};
    produtos[numProdutos++] = produto17;
    
    Produto produto18 = {"Bebedouro para hamsters", 340.0};
    produtos[numProdutos++] = produto18;
    
    Produto produto19 = {"Brinquedo para hamsters (túnel de tubos)", 490.0};
    produtos[numProdutos++] = produto19;
    
    Produto produto20 = {"Ração específica para hamsters", 180.0};
    produtos[numProdutos++] = produto20;
    
    Produto produto21 = {"Cama de maravalha", 100.0};
    produtos[numProdutos++] = produto21;
    
    Produto produto22 = {"Brinquedo para pássaros (espelho com sino)", 60.0};
    produtos[numProdutos++] = produto22;
    
    Produto produto23 = {"Comedouro para hamsters", 30.0};
    produtos[numProdutos++] = produto23;
    
    Produto produto24 = {"Aquário", 40.0};
    produtos[numProdutos++] = produto24;
    
    Produto produto25 = {"Filtro de aquário", 600.0};
    produtos[numProdutos++] = produto25;
    
    Produto produto26 = {"Aquecedor de aquário", 400.0};
    produtos[numProdutos++] = produto26;
    
    Produto produto27 = {"Substrato ou cascalho para aquário", 50.0};
    produtos[numProdutos++] = produto27;
    
    Produto produto28 = {"Alimento em flocos ou pellets para peixes", 60.0};
    produtos[numProdutos++] = produto28;
    
    Produto produto29 = {"Sifão ou limpador de cascalho para aquári", 12.0};
    produtos[numProdutos++] = produto29;
    
    Produto produto30 = {"Ferramentas de manutenção de aquário", 25.0};
    produtos[numProdutos++] = produto30;
    
    Produto produto31 = {"Sistema de iluminação para aquário",77.0};
    produtos[numProdutos++] = produto31;

	Produto produto32 = {"Rede para peixes", 40.0};
    produtos[numProdutos++] = produto32;
    
    Produto produto33 = {"Bomba de ar para aquário", 70.0};
    produtos[numProdutos++] = produto33;
    
    Produto produto34 = {"Medicamentos para peixes (para doenças comuns)", 140.0};
    produtos[numProdutos++] = produto34;
    
    Produto produto35 = {"Selas (de montaria ou de trabalho)", 80.0};
    produtos[numProdutos++] = produto35;
    
    Produto produto36 = {"Rédeas", 35.0};
    produtos[numProdutos++] = produto36;
    
    Produto produto37 = {"Cabeçadas (de couro ou nylon)", 130.0};
    produtos[numProdutos++] = produto37;
    
    Produto produto38 = {"Peitorais e antolhos", 90.0};
    produtos[numProdutos++] = produto38;
    
    Produto produto39 = {"Manta de sela", 50.0};
    produtos[numProdutos++] = produto39;
    
    Produto produto40 = {"Bridões e embocaduras", 40.0};
    produtos[numProdutos++] = produto40;
    
    Produto produto41 = {"Manto do Mengao", 1000.0};
    produtos[numProdutos++] = produto41;
    
    Produto produto42 = {"Suplementos alimentares para cavalos(Bomba)", 50.0};
    produtos[numProdutos++] = produto42;
    
    Produto produto43 = {"Equipamentos de treinamento", 222.0};
    produtos[numProdutos++] = produto43;
    
    do {
        printf("\n==== Petshop Online ====\n");
        printf("1. Criar conta\n");
        printf("2. Fazer login\n");
        printf("3. Buscar produto\n");
        printf("4. Exibir catalogo de produtos\n");
        printf("5. Adicionar produto\n");
        printf("6. Adicionar ao carrinho\n");
        printf("7. Realizar pagamento\n");
        printf("0. Sair\n");
        printf("Escolha uma opcao: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1:
                criarConta();
                break;
            case 2:
                fazerLogin();
                break;
            case 3:
                buscarProduto();
                break;
            case 4:
                exibirCatalogo();
                break;
            case 5:
                adicionarProduto();
                break;
            case 6:
                adicionarAoCarrinho();
                break;
            case 7:
                realizarPagamento();
                break;
            case 0:
                printf("Obrigado por usar o Petshop Online. Ate mais!\n");
                break;
            default:
                printf("Opcao invalida. Tente novamente.\n");
                break;
        }
    } while (opcao != 0);

    return 0;
}

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_PRODUTOS 100

//Código parte funcionários

typedef struct {
char nome[50];
float preco;
int quantidade;
} Produto;

Produto produtos[MAX_PRODUTOS];
int numProdutos = 0;

void fazerLoginFuncionario() {
char nome[50];
char email[100];
printf("==== Area de Login do Funcionario ====\n");
printf("Nome: ");
scanf("%s", nome);
printf("Email: ");
scanf("%s", email);
printf("Login bem-sucedido! Bem-vindo, %s!\n", nome);
}

void confirmarVenda() {
int indiceProduto;
int quantidade;
printf("==== Confirmacao de Vendas ====\n");
printf("Escolha o numero do produto vendido: ");
scanf("%d", &indiceProduto);
if (indiceProduto >= 1 && indiceProduto <= numProdutos) {
    printf("Quantidade vendida: ");
    scanf("%d", &quantidade);

    if (quantidade <= produtos[indiceProduto - 1].quantidade) {
        produtos[indiceProduto - 1].quantidade -= quantidade;
        printf("Venda confirmada! Estoque atualizado.\n");
    } else {
        printf("Quantidade solicitada superior ao estoque disponivel.\n");
    }
} else {
    printf("Numero de produto invalido.\n");
}
}

void exibirEstoque() {
int i;
printf("==== Estoque de Produtos ====\n");
for (i = 0; i < numProdutos; i++) {
printf("%d. %s (Quantidade: %d)\n", i + 1, produtos[i].nome, produtos[i].quantidade);
}
}

void cadastrarProduto() {
if (numProdutos < MAX_PRODUTOS) {
printf("==== Cadastro de Produto ====\n");
printf("Nome do produto: ");
scanf("%s", produtos[numProdutos].nome);
printf("Preco: ");
scanf("%f", &produtos[numProdutos].preco);
printf("Quantidade: ");
scanf("%d", &produtos[numProdutos].quantidade);
    numProdutos++;
    printf("Produto cadastrado com sucesso!\n");
} else {
    printf("Limite maximo de produtos atingido.\n");
}
}

int main() {
int opcao;
// Adicionando produtos iniciais
Produto racao = {"Racao", 50.0, 100};
produtos[numProdutos++] = racao;

Produto racaoPremium = {"Racao Premium", 80.0, 50};
produtos[numProdutos++] = racaoPremium;

Produto brinquedos = {"Brinquedos", 30.0, 200};
produtos[numProdutos++] = brinquedos;

Produto guias = {"Guias", 40.0, 150};
produtos[numProdutos++] = guias;

Produto petiscos = {"Petiscos", 20.0, 300};
produtos[numProdutos++] = petiscos;

Produto roupas = {"Roupas", 60.0, 100};
produtos[numProdutos++] = roupas;

Produto shampo = {"Shampo", 25.0, 80};
produtos[numProdutos++] = shampo;

Produto coleiras = {"Coleiras", 35.0, 120};
produtos[numProdutos++] = coleiras;

fazerLoginFuncionario();

do {
    printf("\n==== Controle de Vendas e Estoque ====\n");
    printf("1. Confirmar Venda\n");
    printf("2. Exibir Estoque\n");
    printf("3. Cadastrar Produto\n");
    printf("0. Sair\n");
    printf("Escolha uma opcao: ");
    scanf("%d", &opcao);

    switch (opcao) {
        case 1:
            confirmarVenda();
            break;
        case 2:
            exibirEstoque();
            break;
        case 3:
            cadastrarProduto();
            break;
        case 0:
            printf("Obrigado por usar o Controle de Vendas e Estoque. Ate mais!\n");
            break;
        default:
            printf("Opcao invalida. Tente novamente.\n");
            break;
    }
} while (opcao != 0);

return 0;
}





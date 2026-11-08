#include <stdio.h>

#define MAX_PROBLEMAS 50
#define ARQUIVO_DADOS "problemas.txt"


typedef struct {
    int bairro;
    int categoria;
    int prioridade;
    int pessoasAfetadas;
} Problema;


void mostrarNomeBairro(int bairro) {

    switch(bairro) {

        case 1:
            printf("Centro");
            break;

        case 2:
            printf("Jardim Aurora");
            break;

        case 3:
            printf("Vila Esperanca");
            break;

        case 4:
            printf("Parque das Aguas");
            break;

        case 5:
            printf("Nova Harmonia");
            break;

        default:
            printf("Bairro desconhecido");
    }
}

void mostrarNomeCategoria(int categoria) {

    switch(categoria) {

        case 1:
            printf("Infraestrutura");
            break;

        case 2:
            printf("Seguranca");
            break;

        case 3:
            printf("Limpeza Urbana");
            break;

        case 4:
            printf("Saneamento");
            break;

        case 5:
            printf("Transporte");
            break;

        default:
            printf("Categoria desconhecida");
    }
}

int salvarProblemas(Problema problemas[], int quantidadeProblemas) {

    FILE *arquivo;
    int i;

    arquivo = fopen(ARQUIVO_DADOS, "w");

    if (arquivo == NULL) {
        printf("\nErro ao salvar os dados no arquivo.\n");
        return 0;
    }

    fprintf(arquivo, "%d\n", quantidadeProblemas);

    for (i = 0; i < quantidadeProblemas; i++) {

        fprintf(arquivo, "%d %d %d %d\n",
                problemas[i].bairro,
                problemas[i].categoria,
                problemas[i].prioridade,
                problemas[i].pessoasAfetadas);
    }

    fclose(arquivo);

    return 1;
}


int carregarProblemas(Problema problemas[]) {

    FILE *arquivo;
    int quantidade = 0;
    int i;

    arquivo = fopen(ARQUIVO_DADOS, "r");

    if (arquivo == NULL) {
        return 0;
    }

    if (fscanf(arquivo, "%d", &quantidade) != 1) {
        fclose(arquivo);
        return 0;
    }

    if (quantidade < 0 || quantidade > MAX_PROBLEMAS) {
        fclose(arquivo);
        return 0;
    }

    for (i = 0; i < quantidade; i++) {

        if (fscanf(arquivo, "%d %d %d %d",
                   &problemas[i].bairro,
                   &problemas[i].categoria,
                   &problemas[i].prioridade,
                   &problemas[i].pessoasAfetadas) != 4) {

            quantidade = i;
            break;
        }
    }

    fclose(arquivo);

    return quantidade;
}

void buscarPorBairro(Problema problemas[], int quantidadeProblemas) {

    int bairroBusca;
    int encontrou = 0;
    int i;

    printf("       BUSCA DE PROBLEMAS POR BAIRRO\n");

    if (quantidadeProblemas == 0) {
        printf("\nNao existem problemas cadastrados.\n");
        return;
    }

    printf("\nBairros disponiveis:\n");
    printf("1 - Centro\n");
    printf("2 - Jardim Aurora\n");
    printf("3 - Vila Esperanca\n");
    printf("4 - Parque das Aguas\n");
    printf("5 - Nova Harmonia\n");

    printf("\nDigite o bairro que deseja buscar: ");
    scanf("%d", &bairroBusca);

    if (bairroBusca < 1 || bairroBusca > 5) {
        printf("\nBairro invalido.\n");
        return;
    }

    printf("\n RESULTADOS DA BUSCA \n");

    for (i = 0; i < quantidadeProblemas; i++) {

        if (problemas[i].bairro == bairroBusca) {

            encontrou = 1;

            printf("\nProblema %d:\n", i + 1);

            printf("Bairro: ");
            mostrarNomeBairro(problemas[i].bairro);
            printf("\n");

            printf("Categoria: ");
            mostrarNomeCategoria(problemas[i].categoria);
            printf("\n");

            printf("Prioridade: %d\n", problemas[i].prioridade);

            printf("Pessoas afetadas: %d\n",
                   problemas[i].pessoasAfetadas);
        }
    }

    if (encontrou == 0) {
        printf("\nNenhum problema encontrado nesse bairro.\n");
    }
}

void mostrarMaiorPrioridade(Problema problemas[],
                            int quantidadeProblemas) {

    int maiorPrioridade;
    int posicaoMaior;
    int i;

    if (quantidadeProblemas == 0) {
        printf("\nNao existem problemas cadastrados.\n");
        return;
    }

    maiorPrioridade = problemas[0].prioridade;
    posicaoMaior = 0;

    for (i = 1; i < quantidadeProblemas; i++) {

        if (problemas[i].prioridade > maiorPrioridade) {

            maiorPrioridade = problemas[i].prioridade;
            posicaoMaior = i;
        }
    }

    printf("       PROBLEMA MAIS PRIORITARIO\n");

    printf("\nProblema %d\n", posicaoMaior + 1);

    printf("Bairro: ");
    mostrarNomeBairro(problemas[posicaoMaior].bairro);
    printf("\n");

    printf("Categoria: ");
    mostrarNomeCategoria(problemas[posicaoMaior].categoria);
    printf("\n");

    printf("Prioridade: %d\n",
           problemas[posicaoMaior].prioridade);

    printf("Pessoas afetadas: %d\n",
           problemas[posicaoMaior].pessoasAfetadas);
}

void mostrarEstatisticas(Problema problemas[],
                         int quantidadeProblemas) {

    int somaPrioridades = 0;
    int totalPessoas = 0;
    int maiorPrioridade;
    int contadorCategorias[6] = {0};
    int maiorCategoria = 1;
    int i;

    float mediaPrioridades;

    if (quantidadeProblemas == 0) {
        printf("\nNao existem problemas cadastrados.\n");
        return;
    }

    maiorPrioridade = problemas[0].prioridade;

    for (i = 0; i < quantidadeProblemas; i++) {

        somaPrioridades += problemas[i].prioridade;

        totalPessoas += problemas[i].pessoasAfetadas;

        if (problemas[i].prioridade > maiorPrioridade) {
            maiorPrioridade = problemas[i].prioridade;
        }

        if (problemas[i].categoria >= 1 &&
            problemas[i].categoria <= 5) {

            contadorCategorias[problemas[i].categoria]++;
        }
    }

    mediaPrioridades =
        (float)somaPrioridades / quantidadeProblemas;

    for (i = 2; i <= 5; i++) {

        if (contadorCategorias[i] >
            contadorCategorias[maiorCategoria]) {

            maiorCategoria = i;
        }
    }

    printf("        ESTATISTICAS DA CIDADE\n");

    printf("\nQuantidade total de problemas: %d\n",
           quantidadeProblemas);

    printf("Media das prioridades: %.2f\n",
           mediaPrioridades);

    printf("Total de pessoas afetadas: %d\n",
           totalPessoas);

    printf("Maior prioridade: %d\n",
           maiorPrioridade);

    printf("Categoria com maior numero de ocorrencias: ");

    mostrarNomeCategoria(maiorCategoria);

    printf("\n");

    printf("\nQuantidade por categoria:\n");

    printf("Infraestrutura: %d\n",
           contadorCategorias[1]);

    printf("Seguranca: %d\n",
           contadorCategorias[2]);

    printf("Limpeza Urbana: %d\n",
           contadorCategorias[3]);

    printf("Saneamento: %d\n",
           contadorCategorias[4]);

    printf("Transporte: %d\n",
           contadorCategorias[5]);
}


int main() {

    Problema problemas[MAX_PROBLEMAS];

    // Variaveis de controle
    int quantidadeProblemas = 0;
    int opcao;
    int i;

    quantidadeProblemas = carregarProblemas(problemas);

    if (quantidadeProblemas > 0) {
        printf("%d problema(s) carregado(s) do arquivo.\n\n",
               quantidadeProblemas);
    }

    do {

        printf("   SISTEMA DE PLANEJAMENTO URBANO\n");
        printf("          CIDADE ATLANTIDA\n");

        printf("1 - Cadastrar problema\n");
        printf("2 - Consultar todos os problemas\n");
        printf("3 - Buscar problemas por bairro\n");
        printf("4 - Mostrar problema mais prioritario\n");
        printf("5 - Mostrar estatisticas da cidade\n");
        printf("0 - Encerrar programa\n");

        printf("\nEscolha uma opcao: ");
        scanf("%d", &opcao);

        switch(opcao) {


            case 1:

                if (quantidadeProblemas < MAX_PROBLEMAS) {

                    printf("\n CADASTRO DE PROBLEMA \n");


                    printf("\nBairros disponiveis:\n");
                    printf("1 - Centro\n");
                    printf("2 - Jardim Aurora\n");
                    printf("3 - Vila Esperanca\n");
                    printf("4 - Parque das Aguas\n");
                    printf("5 - Nova Harmonia\n");

                    printf("\nDigite o bairro: ");

                    scanf("%d",
                           &problemas[quantidadeProblemas].bairro);


                    if (problemas[quantidadeProblemas].bairro < 1 ||
                        problemas[quantidadeProblemas].bairro > 5) {

                        printf("Bairro invalido\n");
                        printf("O problema nao foi cadastrado.\n");

                        break;
                    }


                    printf("\nCategorias disponiveis:\n");
                    printf("1 - Infraestrutura\n");
                    printf("2 - Seguranca\n");
                    printf("3 - Limpeza Urbana\n");
                    printf("4 - Saneamento\n");
                    printf("5 - Transporte\n");

                    printf("\nDigite a categoria: ");

                    scanf("%d",
                           &problemas[quantidadeProblemas].categoria);


                    if (problemas[quantidadeProblemas].categoria < 1 ||
                        problemas[quantidadeProblemas].categoria > 5) {

                        printf("Categoria invalida!\n");
                        printf("O problema nao foi cadastrado.\n");

                        break;
                    }


                    printf("Digite o nivel de prioridade (1 a 10): ");

                    scanf("%d",
                           &problemas[quantidadeProblemas].prioridade);


                    if (problemas[quantidadeProblemas].prioridade < 1 ||
                        problemas[quantidadeProblemas].prioridade > 10) {

                        printf("Prioridade invalida!\n");
                        printf("O problema nao foi cadastrado.\n");

                        break;
                    }

                    printf("Digite a quantidade de pessoas afetadas: ");

                    scanf("%d",
                           &problemas[quantidadeProblemas].pessoasAfetadas);


                    if (problemas[quantidadeProblemas].pessoasAfetadas < 0) {

                        printf("Quantidade invalida!\n");
                        printf("O problema nao foi cadastrado.\n");

                        break;
                    }

                    quantidadeProblemas++;

                    if (salvarProblemas(problemas, quantidadeProblemas)) {
                        printf("\nProblema cadastrado com sucesso!\n");
                    }

                } else {

                    printf("\nLimite maximo de problemas atingido!\n");

                }

                break;

            case 2:

                printf("       TODOS OS PROBLEMAS CADASTRADOS\n");

                if (quantidadeProblemas == 0) {

                    printf("\nNenhum problema foi cadastrado ainda.\n");

                } else {

                    for (i = 0;
                         i < quantidadeProblemas;
                         i++) {

                        printf("\n--- Problema %d ---\n",
                               i + 1);

                        printf("Bairro: ");
                        mostrarNomeBairro(problemas[i].bairro);
                        printf("\n");

                        printf("Categoria: ");
                        mostrarNomeCategoria(problemas[i].categoria);
                        printf("\n");

                        printf("Prioridade: %d\n",
                               problemas[i].prioridade);

                        printf("Pessoas afetadas: %d\n",
                               problemas[i].pessoasAfetadas);
                    }
                }

                break;

            case 3:

                buscarPorBairro(problemas, quantidadeProblemas);

                break;

            case 4:

                mostrarMaiorPrioridade(problemas, quantidadeProblemas);

                break;

            case 5:

                mostrarEstatisticas(problemas, quantidadeProblemas);

                break;

            case 0:

                salvarProblemas(problemas, quantidadeProblemas);

                printf("\nEncerrando o Sistema de Planejamento ");
                printf("Urbano de Atlantida...\n");

                break;

            default:

                printf("\nOpcao invalida! Tente novamente.\n");
        }

    } while (opcao != 0);


    return 0;
}

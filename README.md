MAPA – Estrutura de Dados 2: Implementação de Pilha para Inversão de Palavras em C
Autor: Michael Ewerton Oliveira Disciplina: Estrutura de Dados I Instituição: UniCesumar

Contextualização do Projeto
Este projeto tem como objetivo aplicar os conceitos fundamentais de estruturas de dados por meio da implementação prática de uma pilha em linguagem C. A proposta consiste em desenvolver um programa interativo que utiliza uma pilha para armazenar caracteres e inverter a ordem das letras de uma palavra fornecida pelo usuário. A atividade reforça o entendimento sobre operações básicas de pilha, como empilhar (push), desempilhar (pop), visualizar o topo (topo) e limpar a estrutura (limpar).

Funcionalidades Implementadas
Push: Adiciona caracteres ao topo da pilha, respeitando o limite máximo de armazenamento.

Pop: Remove e retorna o caractere do topo da pilha, permitindo a inversão da palavra.

Topo: Exibe o caractere atual no topo da pilha sem removê-lo.

Limpar: Reinicializa a pilha, tornando os dados inacessíveis sem liberar memória (já que os dados são estáticos).

Menu Interativo: Permite ao usuário escolher entre adicionar palavras, inverter, limpar ou visualizar o topo da pilha.

Aplicabilidade
A pilha é uma estrutura de dados do tipo LIFO (Last In, First Out), ideal para situações em que o último elemento inserido deve ser o primeiro a ser removido. Neste projeto, ela é utilizada para inverter palavras, demonstrando uma aplicação clássica e intuitiva do conceito.

Tecnologias Utilizadas
Linguagem C

Biblioteca padrão stdio.h e string.h

Ambiente de desenvolvimento: Code::Blocks / VS Code / Dev-C++

Resultado e Reconhecimento
A implementação cumpre com clareza os requisitos da atividade prática, demonstrando domínio sobre estruturas de dados estáticas e manipulação de memória. O projeto também reforça a importância da lógica de programação e da organização funcional em sistemas interativos.

Pronto para ser integrado ao portfólio acadêmico e demonstrar habilidades técnicas em estruturas de dados.

#include <stdio.h>
#include <string.h>

#define MAX_SIZE 100

struct Pilha {
    char itens[MAX_SIZE];
    int topo;
};

void inicializar(struct Pilha *p) {
    p->topo = -1;
}

int vazia(struct Pilha *p) {
    return p->topo == -1;
}

int cheia(struct Pilha *p) {
    return p->topo == MAX_SIZE - 1;
}

void push(struct Pilha *p, char item) {
    if (cheia(p)) {
        printf("\nErro: Pilha cheia. Não é possível adicionar mais elementos.\n");
    } else {
        p->itens[++(p->topo)] = item;
    }
}

char pop(struct Pilha *p) {
    if (vazia(p)) {
        printf("\nErro: Pilha vazia. Nenhum elemento para remover.\n");
        return '\0';
    } else {
        return p->itens[(p->topo)--];
    }
}

char topo(struct Pilha *p) {
    if (vazia(p)) {
        printf("\nErro: Pilha vazia. Nenhum elemento no topo.\n");
        return '\0';
    } else {
        return p->itens[p->topo];
    }
}

void limpar(struct Pilha *p) {
    p->topo = -1;
}

int main() {
    struct Pilha p;
    inicializar(&p);

    while (1) {
        printf("\nDigite 1 para adicionar uma palavra à pilha\n");
        printf("Digite 2 para desempilhar a palavra\n");
        printf("Digite 3 para limpar a pilha\n");
        printf("Digite 4 para exibir o topo da pilha\n");
        printf("Digite 0 para sair\n");

        int opcao;
        printf("\nEscolha uma opção: ");
        scanf("%d", &opcao);

        switch (opcao) {
            case 1: {
                char palavra[MAX_SIZE];
                printf("\nDigite a palavra a ser adicionada: ");
                scanf("%s", palavra);
                for (int i = 0; i < strlen(palavra); i++) {
                    push(&p, palavra[i]);
                }
                printf("\nPalavra '%s' adicionada à pilha.\n", palavra);
                break;
            }
            case 2: {
                char palavra[MAX_SIZE];
                int indice = 0;
                while (!vazia(&p)) {
                    palavra[indice++] = pop(&p);
                }
                palavra[indice] = '\0';
                if (indice > 0) {
                    printf("\nPalavra desempilhada (invertida): '%s'\n", palavra);
                } else {
                    printf("\nPilha vazia. Nenhum elemento para mostrar.\n");
                }
                break;
            }
            case 3: {
                limpar(&p);
                printf("\nPilha limpa.\n");
                break;
            }
            case 4: {
                char top = topo(&p);
                if (top != '\0') {
                    printf("\nElemento no topo da pilha: %c\n", top);
                }
                break;
            }
            case 0: {
                printf("\nEncerrando o programa...\n");
                return 0;
            }
            default: {
                printf("\nOpção inválida. Digite 1, 2, 3, 4 ou 0.\n");
            }
        }
    }

    return 0;
}


# Atividade-41

#include <stdio.h>
#include <ctype.h>
#include <string.h>  // Para a função strchr

void codificar_cesar(char *texto, int deslocamento) {
    char ch;
    while ((ch = *texto) != '\0') {
        if (isalpha(ch)) {
            char base = isupper(ch) ? 'A' : 'a';
            *texto = (ch - base + deslocamento) % 26;
            if (*texto < 0) *texto += 26;
            *texto += base;
        }
        texto++;
    }
}

void decodificar_cesar(char *texto, int deslocamento) {
    // Decodificar é equivalente a codificar com deslocamento negativo
    codificar_cesar(texto, -deslocamento);
}

int main() {
    char texto[256];
    int deslocamento;
    char operacao;

    printf("Cifra de César\n");
    printf("Digite o texto (máximo 255 caracteres): ");
    fgets(texto, sizeof(texto), stdin);

    // Remove o caractere de nova linha do final da string, se presente
    size_t len = strlen(texto);
    if (len > 0 && texto[len - 1] == '\n') {
        texto[len - 1] = '\0';
    }

    printf("Digite o deslocamento: ");
    scanf("%d", &deslocamento);

    // Limpa o buffer de entrada para evitar problemas com fgets
    while (getchar() != '\n');

    printf("Digite 'c' para codificar ou 'd' para decodificar: ");
    scanf("%c", &operacao);

    switch (operacao) {
        case 'c':
            codificar_cesar(texto, deslocamento);
            printf("Texto codificado: %s\n", texto);
            break;
        case 'd':
            decodificar_cesar(texto, deslocamento);
            printf("Texto decodificado: %s\n", texto);
            break;
        default:
            printf("Operação inválida.\n");
            break;
    }

    return 0;
}

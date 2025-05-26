#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

int main() {
    int sock = 0;
    struct sockaddr_in serv_addr;
    char buffer[BUFFER_SIZE] = { 0 };
    const char* student_info = "Рожков Александр Сергеевич, Группа ККСО-26-24, Курс 1";

    // Создание сокета
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        perror("Ошибка создания сокета");
        exit(EXIT_FAILURE);
    }

    serv_addr.sin_family = AF_INET;
    serv_addr.sin_port = htons(PORT);

    // Преобразование IP-адреса из текстового в бинарный формат
    if (inet_pton(AF_INET, "127.0.0.1", &serv_addr.sin_addr) <= 0) {
        perror("не правильный адресс");
        exit(EXIT_FAILURE);
    }

    // Подключение к серверу
    if (connect(sock, (struct sockaddr*)&serv_addr, sizeof(serv_addr)) < 0) {
        perror("ошибка соединения");
        exit(EXIT_FAILURE);
    }

    // Отправка данных серверу
    send(sock, student_info, strlen(student_info), 0);
    printf("Информация о студенте отпралена на сервер: %s\n", student_info);

    // Чтение ответа от сервера
    read(sock, buffer, BUFFER_SIZE);
    printf("ответ сервера: %s\n", buffer);

    close(sock);
    return 0;
}

# .-
#include <stdio.h>
#include <locale.h>

int check(double x, double y, double r_big, double r_small) {
    if (y >= 0 && (x * x + y * y <= r_big * r_big) && !(x >= 0 && (x * x + y * y <= r_small * r_small))) {
        return 1;
    }
    return 0;
}

void draw_area(double x_min, double x_max, double y_min, double y_max,
               double step, double r_big, double r_small) {
    for (double y = y_max; y >= y_min; y -= step) {
        for (double x = x_min; x <= x_max; x += step) {
            if (check(x, y, r_big, r_small)) {
                printf("* ");
            }
            else {
                printf("  ");
            }
        }
        printf("\n");
    }
}

double task1(double x) {
    if (x <= 13) {
        return -x * x * x + 9.0;
    }
    else {
        return -3.0 / (x + 1.0);
    }
}

int main() {
    setlocale(LC_CTYPE, "RUS");
    int choice;
    int cont;
    do {
        printf("\nменю\n");
        printf("1. Проверить принадлежность точки\n");
        printf("2. Нарисовать область\n");
        printf("3. Вычислить функцию (task1)\n");
        printf("Выберите пункт: ");
        scanf("%d", &choice);

        switch (choice) {
        case 1: {
            double x, y;
            printf("Введите координаты x и y: ");
            scanf("%lf %lf", &x, &y);
            if (check(x, y, 6.0, 3.0) == 1) {
                printf("Точка принадлежит области.\n");
            }
            else {
                printf("Точка НЕ принадлежит области.\n");
            }
            break;
        }
        case 2: {
            printf("\nРисуем фигуру:\n\n");
            draw_area(-6.0, 6.0, 0.0, 6.0, 0.5, 6.0, 3.0);
            break;
        }
        case 3: {
            double x;
            printf("Введите значение x: ");
            scanf("%lf", &x);
            printf("Результат: %.4f\n", task1(x));
            break;
        }
        default: {
            printf("Неверный пункт!\n");
            break;
        }
        }
        printf("\nПродолжить ? (Да - введите любое число, Нет - введите 0): ");
        scanf("%d", &cont);
    } while (cont != 0);
    printf("\nПрограмма завершена.\n");
    return 0;
}

# base
Эта программа(C++) является простой базой данных, в которой можно добавлять/удалять спортсменов, искать нужного спортсмена по его собранной сумме, также можно сохранить то, что ввели, и позже открыть.

#include<stdio.h>
#include<locale.h>
                    
struct competion
{
  int summa;
  char name[30];
  char surname[30];
  float weight;
};

struct competion sportsman[20];
int vvod()
{
    int n;
    printf("Введите количество спортсменов\n");
    scanf_s("%d", &n);
    for (int i = 1; i < n+1; i++)
    {
        printf("Введите имя спортсмена\n");
        scanf_s("%s", &sportsman[i].name,30);

        printf("Введите фамилию спортсмена\n");
        scanf_s("%s", &sportsman[i].surname,30);

        printf("Введите вес спортсмена\n");
        scanf_s("%f", &sportsman[i].weight);

        printf("Введите сумму спортсмена\n");
        scanf_s("%d", &sportsman[i].summa);

    }
    return n;
}

void vivod(int N,int k)
{
    if (k == 1) {
        printf("%-4s %-20s %-20s %-20s %-20s\n", "N", "name", "surname", "weight", "summa");
        for (int i = 1; i < N+1 ; i++) {
            printf("%-4d %-20s %-20s %-20.1f %-20d\n", i, sportsman[i].name, sportsman[i].surname, sportsman[i].weight, sportsman[i].summa);

        }
    }
    else printf("Ошибка! Для начала введите базу данных!\n");
}
int add(int N, int k)
{
    int i;
    if (k == 1) {
        i = N + 1;
        printf("Введите имя спортсмена\n");
        scanf_s("%s", &sportsman[i].name,30);

        printf("Введите фамилию спортсмена\n");
        scanf_s("%s", &sportsman[i].surname,30);

        printf("Введите вес спортсмена\n");
        scanf_s("%f", &sportsman[i].weight);

        printf("Введите сумму спортсмена\n");
        scanf_s("%d", &sportsman[i].summa);


        return N + 1;
    }
    else printf("Ошибка! Для начала введите базу данных!\n");
    return N;
}

void search(int N, int k)
{
    if (k == 1)
    {
        int st;
        printf("Введите сумму: ");
        scanf_s("%d", &st);
        printf("N\tname\tsurname\tweight\tsumma\n");
        for (int i = 1; i < N + 1; i++) 
        {
            if (st == sportsman[i].summa) 
            {
                printf("%d\t%s\t%s\t%f\t%d\n", i, sportsman[i].name,sportsman[i].surname, sportsman[i].weight, sportsman[i].summa);
            }
        }
    }
    else printf("Ошибка! Для начала введите базу данных!\n");
}


void deleti(struct competion* sportsman, int *N, int k)
{
    if (k == 1)
    {
        int num;
        printf("Введите номер спорстмена,чтобы удалить его\n");
        scanf_s("%d", &num);
        if (num<1 || num>*N)
        {
            printf("Нет спортсмена под таким номером\n");
        }
        else
        {
            for (int i = num; i < *N; i++)
            {
               sportsman[i] = sportsman[i + 1];
            }
        }
        (*N)--;
        printf("Спорстмен был удален\n");
    }
    else printf("Ошибка! Для начала введите базу данных!");
}

int load(competion *sportsman)



int main(void)
{
  setlocale(LC_ALL, "RU");
  int k = 0, n, N = 0;
  while (1)
  {
    printf("1-добавление таблицы\n2-вывод таблицы\n3-добавление строки\n4-поиск по сумме спорстменов\n5-удалить строку\n6-сохранить данные в файл\n7-загрузить данные из файла\n8-выход\n");
    printf("Выберите действие: ");
    scanf_s("%d", &n);
    switch (n)
    {
        case 1:
            N = vvod(); k = 1;
            break;
        case 2:
            vivod(N, k);
            break;
        case 3:
            N = add(N, k);
            break;
        case 4:
            search(N, k);
            break;
        case 5:
            deleti(sportsman, &N, k);
            break;
        case 6:
             save(sportsman, N, k);
            break;
        case 7:
            N = load(sportsman);
            if (N > 0) 
            {
                k = 1;
            }
            break;

        case 8:
            return 0;
        default:
            printf("Невверный ввод\n");
            break;

    }
  }
}

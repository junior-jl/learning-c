```c
#include<stdio.h>
#include<stdlib.h>
#include<locale.h>

void main(){

    setlocale(LC_ALL, "");

    //Crie um algoritmo que leia três valores na mesma linha e multiplique-os
    float n1,n2,n3, mult;

    printf("Insira três números. \n");
    scanf("%f %f %f", &n1,&n2,&n3);
    mult = n1*n2*n3;
    printf("O produto %f x %f x %f é igual a %f", n1,n2,n3,mult);

}
```

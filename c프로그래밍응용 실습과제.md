#include <stdio.h>

int main() {
    int num;
    int store[100];
    int sale[100];
    int id;

    printf("상품 개수 입력 : ");
    if (scanf("%d", &num) != 1) {
        return 1;
    }
    int list[num];

    if (num <= 0 || num > 100) {
        printf("상품 개수는 1에서 100 사이여야 합니다.\n");
        return 1;
    }

    printf("상품 별 입고 수량 입력 : ");
    int total_store = 0;  
    for (int i = 0; i < num; i++) {
        if (scanf("%d", &store[i]) != 1) {
            return 1;
        }
        total_store += store[i]; 
    }

    printf("상품 별 판매 수량 입력 : ");
    int total_sale = 0;
    for (int i = 0; i < num; i++) {
        if (scanf("%d", &sale[i]) != 1) {
            return 1;
        }
        total_sale += sale[i]; 
    }

    for (int i = 0; i < num; i++) {
        list[i] = store[i] - sale[i];  
    }

    printf("id 입력 : ");
    if (scanf("%d", &id) != 1) {
        return 1;
    }

    if (id < 1 || id > num) {
        printf("유효한 ID는 1에서 %d 사이여야 합니다.\n", num);
        return 1;
    }

    printf("%d번 상품의 남은 재고: %d\n", id, list[id - 1]);

    printf("재고수량: ");
    for (int i = 0; i < num; i++) {
        printf("%d ", list[i]);
    }
    printf("\n");

    if (total_store > 0) { 
        float sale_percentage = ((float)total_sale / total_store) * 100;
        printf("총 판매 비율: %.2f%%\n", sale_percentage);
    } else {
        printf("총 입고 수량이 0입니다. 판매 비율을 계산할 수 없습니다.\n");
    }

    printf("총 판매 수량: %d\n", total_sale);

    return 0;
}

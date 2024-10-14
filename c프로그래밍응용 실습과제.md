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

    // 남은 재고 계산 및 출력
    printf("재고수량: ");
    for (int i = 0; i < num; i++) {
        list[i] = store[i] - sale[i];  
        printf("%d ", list[i]);  // 재고 수량 출력
    }
    printf("\n");

    // 가장 많이 판매된 상품과 적게 판매된 상품 찾기
    int max_sale = sale[0];
    int min_sale = sale[0];
    int max_id = 1;
    int min_id = 1;

    for (int i = 1; i < num; i++) {
        if (sale[i] > max_sale) {ㅁ
            max_sale = sale[i];
            max_id = i + 1; // ID는 1부터 시작하므로
        }
        if (sale[i] < min_sale) {
            min_sale = sale[i];
            min_id = i + 1;
        }
    }

    // 판매 비율 및 총 판매 수량 출력
    if (total_store > 0) { 
        float sale_percentage = ((float)total_sale / total_store) * 100;
        printf("총 판매량: %d (%.2f%%)\n", total_sale, sale_percentage); // 수량(판매율) 형식으로 출력
    } else {
        printf("총 입고 수량이 0입니다. 판매 비율을 계산할 수 없습니다.\n");
    }

    // 결과 출력
    printf("가장 많이 판매된 상품: id = %d, 판매량 = %d\n", max_id, max_sale);
    printf("가장 적게 판매된 상품: id = %d, 판매량 = %d\n", min_id, min_sale);

    // 재고 부족 상품 출력 (가장 적게 판매된 상품 아래로 이동)
    for (int i = 0; i < num; i++) {
        if (list[i] <= 2) { // 재고 수량이 2 이하인 경우
            printf("상품 id: %d, 재고 부족(%d)\n", i + 1, list[i]);
        }
    }

    return 0;
}

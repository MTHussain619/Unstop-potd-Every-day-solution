#include <stdio.h>
#include <stdlib.h>

// Comparator function to sort in descending order safely
int compare_desc(const void *a, const void *b) {
    int valA = *(int*)a;
    int valB = *(int*)b;
    
    if (valA < valB) return 1;
    if (valA > valB) return -1;
    return 0;
}

void dispatch_order(int n, int k, int* priorities, int* result) {
    // 1. Sort the entire priorities array in descending order
    qsort(priorities, n, sizeof(int), compare_desc);
    
    // 2. Copy the top K elements into the result array
    for (int i = 0; i < k; ++i) {
        result[i] = priorities[i];
    }
}

int main() {
    int n, k;
    scanf("%d %d", &n, &k);
    int* priorities = (int*)malloc(n * sizeof(int));
    for (int i = 0; i < n; ++i) {
        scanf("%d", &priorities[i]);
    }
    
    int* result = (int*)malloc(k * sizeof(int));
    dispatch_order(n, k, priorities, result);
    
    for (int i = 0; i < k; ++i) {
        printf("%d ", result[i]);
    }
    printf("\n");
    
    free(priorities);
    free(result);
    return 0;
}

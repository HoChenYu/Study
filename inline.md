# inline
````C
#include <stdio.h>

// 使用 inline 關鍵字聲明內聯函數
inline int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3);
    printf("The result is %d\n", result);
    return 0;
}
````
在這個例子中，add函數被聲明為內聯函數。當編譯器遇到add函數的調用時，它可能會將add函數的代碼直接插入到調用位置，而不是進行傳統的函數調用。
## 優點

- 減少函數調用的開銷。
- 提高性能，特別是對於小而頻繁調用的函數。

## 缺點

- 代碼膨脹，可能增加可執行文件的大小。
- 編譯器可能不會內聯所有標記為 `inline` 的函數，特別是對於複雜函數或大量使用的情況。

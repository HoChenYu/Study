### What's the content of array a?
````C
int a[] = {6, 7, 8, 9, 10};
int *p=a;
*(p++)+=123;
*(++p)+=123;
````
- a[] = {129, 7, 131, 9, 10} 

### 設定一個絕對位址為0x67a9的整數型變數的值為0xaa55
````C
int *ptr;
ptr = (int *)0x67a9; // 設定指標變數的值
*ptr = 0xaa55; //設定指標變數指向的值
````
### 下列程式碼輸出什麼
````C
int a[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
int *p = &(a + 1)[3];
printf("%d\n", *p);
````
- 輸出 5  
- 因為a+1指向a的第二個元素，[3]表示再向後移動3個元素  
- a+1是跳一個int的大小(a想成指標)  
- &a+1是跳一整個array的大小  

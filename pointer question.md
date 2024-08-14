### What's the content of array a?
````C
int a[] = {6, 7, 8, 9, 10};
int *p=a;
*(p++)+=123;
*(++p)+=123;
````
### 答案
a[] = {129, 7, 131, 9, 10} 

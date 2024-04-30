# Big Endian & Little Endian  

## CPU對於資料存放進記憶體的位元組順序有兩種
- **Big-Endian:**
  - 最高位元組(MSB)會放在最低的記憶體位置上
  - 例如:某一32bits資料為0x12345678，透過Big-Endian存放的順序為|0x12|0x34|0x56|0x78|
- **Little-Endian**
  - 最低位元組(LSB)會放在最低的記憶體位置上
  - 例如:某一32bits資料為0x12345678，透過Little-Endian存放的順序為|0x78|0x56|0x34|0x12|

## 例題:
![image](https://github.com/HoChenYu/Study/assets/63805851/269baef9-240a-41d0-854c-c25eb0d5d12a)  
以little endian的順序輸出以下
````C++
int *ptr = 0x1000;
printf("%x",*ptr + 1);
printf("%x",*(ptr + 1));
````
## 解題思路:
在0x1000地址，整數由低地址到高地址的位元組為 0x01 0x23 0x45 0x67，Little-Endian順序是最低位元組(LSB)會放在最低的記憶體位置上，這裡是0x01最低位元組放在最低記憶體位置0x1000，因此組成的整數是 0x67452301。  
在0x1004地址，整數由位元組 0x89 0xAB 0xCD 0xEF 組成，整數是 0xEFCDAB89。
- 第一個printf的%x顯示*ptr + 1：
  - *ptr為 0x67452301，所以 *ptr + 1 就是 0x67452302。  
- 第二個printf的%x顯示*(ptr + 1)：
  - ptr + 1會將指針移動到下一個整數地址，即0x1004，因此 *(ptr + 1) 是 0xEFCDAB89。  

輸出結果：  
第一個printf輸出：67452302  
第二個printf輸出：efcdab89  
### Reference:[2022 研發替代役面試心得 — 群聯篇](https://leisurecodog.medium.com/%E9%9D%A2%E8%A9%A6-2022-%E7%A0%94%E7%99%BC%E6%9B%BF%E4%BB%A3%E5%BD%B9%E9%9D%A2%E8%A9%A6%E5%BF%83%E5%BE%97-%E7%BE%A4%E8%81%AF%E7%AF%87-7458b4fab85b)

### N is power of 2 or not?
````C
bool ispowerof2(int N){
  return (N>0) && (N&(N-1))==0
}
````
### find LSB value
````C
int findLSBvlue{
  return x&(-x) \\same as return x & (~x+1)
}
````
### find MSB value
````C
int findMSBvalue(int a) {
    if (a == 0) return 0;

    a |= (a >> 1);
    a |= (a >> 2);
    a |= (a >> 4);
    a |= (a >> 8);
    a |= (a >> 16);

    return (a + 1) >> 1;
}
````
會將最高位元(MSB)右邊的bit都變成1，所以之後再加上1造成進位後右移1個bit

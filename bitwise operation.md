### N is power of 2 or not?
````C
bool ispowerof2(int N){
  return (N>0) && (N&(N-1))==0
}
````

# strcpy
````c
void strcpy(char *dest, const char *src)
{
    if (dest == NULL || src == NULL) return;
    
    while (*src != '\0') {
        *dest = *src;
        dest++;
        src++;
    }
````
# strcat
````C
void strcat(char *dest, const char *src)
{
    char *p = dest;
    int loc = 0;

    if (dest == NULL || src == NULL) return;

    while(*(p++) != '\0') loc++;
    
    while(*src != '\0') {
        dest[loc] = *src;
        src++;
        loc++;
    }
}
````
# strlen
````C
int strlen(const char *str)
{
    int len = 0;
    while (*str++ != '\0') len++;
    
    return len;
}
````
# strcmp
````C
int strcmp(const char *s1, const char *s2)
{
    char *ptr = s1 + strlen(s1);
 
    while (*s2 != '\0') {
        *ptr++ = *s2++;
    }

    *ptr = '\0';

    return s1;
}
````
# binary search
````c
void binary_search(int *arr, int len, int target)
{
    int right = len - 1, left = 0, mid = 0;
    
    while (right >= left) {
        mid = (right + left) / 2;
        if (arr[mid] < target) {
            left = mid + 1;
        } else if (arr[mid] > target) {
            right = mid - 1;
        } else if (arr[mid] == target) {
            printf("Found it\n");
            return;
        }
    }
    
    printf("Not found\n");
}
````
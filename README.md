隨著使用者的輸入數值調整陣列大小
====
如何讓陣列隨著使用者的需求而改變大小，使其不至於浪費記憶體。
<br>
<br>
## 方法:
藉由指標設定陣列的第一個元素位址，當換了一個新的大小陣列時，將指標重新指定至新的陣列，再將原本的舊陣列移除，以達到該目的，而重新分配一個新的空間給指標可以用以下的函式:
```
#include <stdio.h>
#include <stdlib.h>

int main() {

  int *numbers = 0; //即為指標, = 0的意思是當它一開始還沒有指定任何陣列時，令他是空指標(NULL)
  
  int length = 0; //為陣列當前的元素個數
  
  numbers = realloc(numbers, sizeof(int) * (length + 1)); //配置一個大小為(sizeof(int) * (length + 1))的記憶體的陣列空間，並將該陣列空間的第1個元素位址指定給更新後的舊指標: numbers
  
  return 0;
  
}
```
上面的一大串函式也可以寫成:
```
#include <stdio.h>
#include <stdlib.h>

int main() {
  int *numbers = 0; //即為指標, = 0的意思是當它一開始還沒有指定任何陣列時，令他是空指標(NULL)
  
  int length = 0; //為陣列當前的元素個數
  
  int *larger = malloc(sizeof(int) * (length　+ 1)); //配置一個大小為(sizeof(int) * (length + 1))的記憶體的陣列空間，並將該陣列空間的第1個元素位址指定給新的指標: larger
  
  for (int i = 0; i < length; i++) {
    larger[i] = numbers[i];
  } //將舊陣列指標numbers的元素一個一個複製貼到新陣列指標larger內
  
  free(numbers); //釋放numbers指定的舊陣列記憶體空間
  
  numbers = larger; //將新指標larger替代掉之前的舊指標numbers，成為新的指標numbers
  
  return 0;
  
}
```

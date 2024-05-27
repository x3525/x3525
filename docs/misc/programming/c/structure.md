---
glightbox: true
---

# Structure

## Documentation Section

```c
// Author: Serhat Çelik
// Date: 21 March 2024
/* Program for addition
 * of two numbers.
 */
```

## Link Section

```c
#include <stdio.h>
#include <conio.h>
```

## Definition Section

```c
#define PI 3.14
#define MIN 0
#define MAX 9
```

## Global Declaration Section

```c
int a;
int b;

void sum();
void sub();
```

## Main Section

```c
void main() {
    // Declaration
    int x;
    // Execution
    func();

    /* Declaration kısmı, Execution kısmından sonra gelirse
     * eski derleyiciler hata verir.
     */
}
```

## Subprogram Section

```c
void hello() {
    printf("Hello world!");
}
```

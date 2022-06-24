# Memory Allocation

## Usage

### Execute

```bash
# allocation <max> <size> <interval>
allocation 100 25 1000
```

### Arguments:

Description:
 - <max> max of iterations e.g.: 100
 - <size> size in MB e.g.: 25 = 25MB" << std::endl;
 - <interval>interval in milliseconds, e.g. 1000 = 1 Second

## Source
```cpp
#include <iostream>
#include <chrono>
#include <thread>

#define Megabyte (1024 * 1024)
#define RequiredArgc 4

int main(int argc, char *argv[]) {
    if (argc != RequiredArgc) {
        std::cout << "Usage: <max> <size> <interval>" << std::endl;
        std::cout << std::endl;
        std::cout << "\t<max>\t\tmax of iterations e.g.: 100" << std::endl;
        std::cout << "\t<size>\t\tsize in MB e.g.: 25 = 25MB" << std::endl;
        std::cout << "\t<interval>\tinterval in milliseconds, e.g. 1000 = 1 Second" << std::endl;
        return 1;
    }

    int max = std::stoi(argv[1]);
    int size = std::stoi(argv[2]);
    int interval = std::stoi(argv[3]);
    int malloc_size = Megabyte * size / 1024 / 1024;
    char *data;

    for (int j = 0; j < max; j++) {
        printf("[%i] Allocating %iMB..\n", j, malloc_size);
        char *data = (char *) malloc(Megabyte * malloc_size);
        printf("[%i] Sleep for %i..\n", j, interval);
        std::this_thread::sleep_for(std::chrono::milliseconds(interval));
    }

    while (true) {
        std::this_thread::sleep_for(std::chrono::milliseconds(20));
    }
}

```

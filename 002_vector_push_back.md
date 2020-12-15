### 1. pass in vectors
```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    //std::cout << "Hello, world!";
    vector<int> test1(3, -100);
    vector<int> test2(2, 9);
    vector<vector<int>> test;
    test.push_back(test1);
    test.push_back(test2);
    test1.at(0) = 1000000;
    for (auto element : test)
    {   
        for (auto num: element)
        {
            cout << num << " ";
        }
        cout << endl;
    }
    for (auto num: test1)
    {
        cout << num << " ";
    }
    return 0;
}
```

Output:
```
-100 -100 -100 
9 9 
1000000 -100 -100
```
Apparently the vector1 pushed back into vector is a copy, not a reference.

### 2. pass in pointers
```
#include <iostream>
#include <vector>
using namespace std;
int main() {
    //std::cout << "Hello, world!";
    vector<int> test1(3, -100);
    vector<int> test2(2, 9);
    vector<vector<int>*> test;
    test.push_back(&test1);
    test.push_back(&test2);
    test1.at(0) = 1000000;
    for (auto element : test)
    {   
        for (auto num: *element)
        {
            cout << num << " ";
        }
        cout << endl;
    }
    for (auto num: test1)
    {
        cout << num << " ";
    }
    return 0;
}
```

Output:
```
1000000 -100 -100 
9 9 
1000000 -100 -100
```
We can see that the element is indeed passed in as reference.

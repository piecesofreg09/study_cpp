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
We can see that the element is indeed passed in as pointers.


### 3. set vectors of references
```cpp
#include <iostream>
#include <vector>
using namespace std;
int main() {
    //std::cout << "Hello, world!";
    vector<int> test1(3, -100);
    vector<int> test2(2, 9);
    vector<vector<int>&> test;
    return 0;
}
```
This program will return error, as vector of references are not allowed.

[Explanation1 on stackoverflow](https://stackoverflow.com/questions/922360/why-cant-i-make-a-vector-of-references)
> The component type of containers like vectors must be assignable. References are not assignable (you can only initialize them once when they are declared, and you cannot make them reference something else later). Other non-assignable types are also not allowed as components of containers, e.g. vector<const int> is not allowed.
[Explanation2 on stackoverflow](https://stackoverflow.com/questions/1164266/why-are-arrays-of-references-illegal)
> Answering to your question about standard I can cite the C++ Standard §8.3.2/4:
> There shall be no references to references, no arrays of references, and no pointers to references.

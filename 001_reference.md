```#include <iostream>
#include <vector>
using namespace std;
int main() {
    //std::cout << "Hello, world!";
    vector<int> test1(3, -100);
    vector<int> test2(2, 9);
    vector<vector<int>> test;
    test.push_back(test1);
    test.push_back(test2);
    for (auto element : test)
    {   
        cout << &element << endl;
        for (auto &num: element)
        {
            num += 10000;
        }
        for (auto num: element)
        {
            cout << num << " ";
        }
        cout << endl;
    }
    for (auto element : test)
    {   
        for (auto num: element)
        {
            cout << num << " ";
        }
        cout << endl;
    }
    return 0;
}
```
Output:
0x7ffe97313b70
9900 9900 9900 
0x7ffe97313b70
10009 10009 
-100 -100 -100 
9 9
it can be seen that the elements in the test vector are not altered at all, even though the
temporary variable element that was created has been altered.
*/

```
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
    for (auto &element : test)
    {   
        cout << &element << endl;
        for (auto &num: element)
        {
            num += 10000;
        }
        for (auto num: element)
        {
            cout << num << " ";
        }
        cout << endl;
    }
    for (auto element : test)
    {   
        for (auto num: element)
        {
            cout << num << " ";
        }
        cout << endl;
    }
    return 0;
}
```

Output:
0x22faef0
9900 9900 9900 
0x22faf08
10009 10009 
9900 9900 9900 
10009 10009
It can be seen that the two vectors inside the test vector has changed.
So you have to use reference type if you want to change things.

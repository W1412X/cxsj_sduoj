# STL标准模板库学习
## Vector
- 定义
```cpp
vector<int>array;
vector<vector<int>>array;
vector<struct SelfDef>array;
```
- 访问
  1) 下标访问
    ```cpp
    vector<int>array;
    array.push_back(0);
    array[0];
    ```
  2) 迭代器访问
    ```cpp
    vector<int>array;
    array.push_back(0);
    for(vector<int>::iterator it=array.begin();it!=array.end();it++){
        cout<<*it<<endl;
    }
    ```
- 一些函数
  - push_back()
  $$
  O(1)
  $$
  - pop_back()
  $$
  O(1)
  $$
  -  size()
  $$
  O(1)
  $$
  - clear()
  $$
  O(n)
  $$
  - insert()
  $$
  O(n)\ or\ O(1)
  $$
  ```cpp
    vector<int>array;
    array.push_back(0);
    array.insert(array.begin(),1);
  ```
  - erase()
    - 删除指定位置元素
      ```cpp
      array.erase(array.begin());
      ```
    - 删除一个区间内元素
        ```cpp
        array.erase(array.begin(),array.begin()+array.size());
        ```
##  Set
- 定义
  ```cpp
  set<int>s;
  ```
  > 定义的变量可以时普通类型，可以是vector,set,queue
- 访问  
**仅可以通过迭代器访问**
  ```cpp
  set<int>s;
  for(set<int>::iterator it=s.begin();it!=s.end();it++){
    cout<<*it<<' ';
  }
  ```
- 常用函数
  - insert(element)  
  **insert会自动对插入的元素进行排序（自动递增）**
    $$
    O(\log(n))
    $$
  - find(element)
    $$
    O(log(n))
    $$
    - 返回一个set中的迭代器
    ```cpp
    //判断是否含有此元素
    if(set.find(element)!=set.end()){
      ...
    }else{
      ...
    }
    ```
  - erase
    - 删除单个
      - 通过迭代器
      $$
      O(1)
      $$
      ```cpp
      set<int>iterator it;
      set.erase(it)
      ```
      - 通过元素
      $$
      O(\log(n))
      $$
      ```cpp
      set.erase(100)
      ```
    - 删除区间
    ```cpp
    set.erase(set.begin(),set.end())
    ```
## Unordered_set
- 定义
  ```cpp
  unordered_set<int>ust;
  ```
  > **可以是任何类型的键，与set类似**
- **其余使用与 *set* 类似**  
## Unordered_map
- 定义
  ```cpp
  unordered_map<key_type,value_type>um;
  ```
  > **支持所有的类型，但是对于一些自定义或者预定义类型（如vector）需要完善哈希函数以及对应的相等性的判断**
- 常用函数
  - 时间复杂度均为
  $$
  O(1)->O(n)
  $$
  - at(key)
    > 返回key对应值的引用
    ```cpp
    unordered_map<string,int>um;
    um["wx"]=0621;
    um.at("wx")=1412;
    cout<<um["wx"];
    ``` 
    > 将输出1412
  - begin()/end()
    - 返回迭代器
  - erase()
    ```cpp
    um["wx1"]=1412;
    um.erase("wx1");
    if(um.find("wx1")==um.end()){
        cout<<"delete wx1"<<endl;
    }
    ```
    - 其中也可以仿照set利用迭代器删除元素
  - find()
  - empty()
    - 返回一个bool值
  
## Queue
- 定义
  ```cpp
  queue<type>q
  ```
- 常见函数
1. **push()**：将元素压入队列尾部
   - 时间复杂度：均摊 O(1)

2. **pop()**：将队首元素从队列中移除
   - 时间复杂度：O(1)

3. **front()**：访问队首元素
   - 时间复杂度：O(1)

4. **back()**：访问队尾元素
   - 时间复杂度：O(1)

5. **empty()**：检查队列是否为空
   - 时间复杂度：O(1)

6. **size()**：返回队列中元素的个数
   - 时间复杂度：O(1)
## Stack
- 定义
  ```cpp
  stack<type>sk;
  ```
- 常见函数
1. **push()**：将元素压入栈顶
   - 时间复杂度：均摊 O(1)

2. **pop()**：将栈顶元素弹出栈
   - 时间复杂度：O(1)

3. **top()**：访问栈顶元素
   - 时间复杂度：O(1)

4. **empty()**：检查栈是否为空
   - 时间复杂度：O(1)

5. **size()**：返回栈中元素的个数
   - 时间复杂度：O(1)

## priority_queue
### 包含头文件
```cpp
#include <queue>
```

### 创建优先队列
```cpp
std::priority_queue<int> pq; // 创建一个存储整数的默认最大优先队列
```

### 插入元素
```cpp
pq.push(10); // 向优先队列中插入元素 10
pq.push(20); // 向优先队列中插入元素 20
```

### 访问顶部元素
```cpp
int topElement = pq.top(); // 获取优先队列中的顶部元素（具有最高优先级）
```

### 删除顶部元素
```cpp
pq.pop(); // 从优先队列中删除顶部元素
```

### 自定义比较函数
如果需要自定义元素的比较方式，可以传入自定义的比较函数作为模板参数，或者重载元素类型的 `<` 操作符。

例如，创建一个最小堆（最小值优先）的优先队列：
```cpp
std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
```

或者自定义结构体并重载 `<` 操作符：
```cpp
struct Node {
    int val;
    int priority;
    bool operator<(const Node& other) const {
        return priority > other.priority; // 自定义比较规则
    }
};

std::priority_queue<Node> customQueue;
```

### 注意事项
- `std::priority_queue` 默认情况下是最大堆（最大值优先），如果需要最小堆，可以传入第三个模板参数为 `std::greater<T>`。
- 优先队列的元素没有随机访问的能力，只能操作顶部元素和插入/删除操作。
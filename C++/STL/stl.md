## vector

向量，变长数组（长度根据需要而自动改变的数组）



### 使用前

添加

```c++
#include <vector>
using namespace std;
```



### 定义

####一维

```c++
vector <typename> name;

vector<int> name;
vector<double> name;
vector<char> name;
vector<node> name;//node是结构体类型

vector <vector <int> > name; //>>之间要加空格
```

####二维

```c ++
vector<typename> Arrayname[arraySize];

vector<int> vi[100];
```

`vector<vector<int> > name`和`vector<int> name[Size]`不同，后者的一维长度固定为Size



### 访问

#### 通过下标访问

```c++
vi[index]
```



#### 通过迭代器进行访问

```c++
vector<typename>::iterator it;

vector<int>::iterator it;
vector<double>::iterator it;
```

使用`*it`访问vector里面的元素



### 常用函数

```markdown
* push_back()		在vector后面添加一个元素
* pop_back()		删除vector的尾元素
* size()			获得vector()中元素的个数
* clear()			清空vector中的所有元素
* insert()			用来向vector的任意迭代器it处插入一个元素x
* erase()
	erase(it)		删除迭代器为it处的元素
	erase(first, last)		删除[first, last)内的所有元素
```







## set

集合，内部自动有序且不含重复元素的容器

###使用前添加

```c++
#include <set>
using namespace std;
```



### 访问

只能通过迭代器访问

```cpp
set<typename>::iterator it;

set<int>::iterator it;
```



由于除开vector和string之外的STL容器都不支持*(it+i)的访问方式，因此只能按如下方式枚举

```cpp
#include <stdio.h>
#include <set>
using namespace std;

int main(void)
{
	set<int> st;
	st.insert(3);
	st.insert(5);
	st.insert(2);
	st.insert(3);

	for (set<int>::iterator it = st.begin(); it != st.end(); it++)
		printf("%d ", *it);

	return 0;
}
```



**set内的元素自动递增排序，且自动去除了重复元素**



### 常用函数

```markdown
* insert(x)		将x插入set容器中，并自动递增排序和去重

* find(value)	返回set中对应值为value的迭代器，如果没找到则返回s.end(),末尾迭代器的后一个迭代器

* erase()
	* st.erase(it)		it为所需要删除元素的迭代器（删除单个元素）
	* st.erase(value)	value为所需要删除元素的值（删除单个元素）
	* st.erase(first, second)	first为所需要删除区间的起始迭代器，second为所需要删除区间的末尾迭代器的下一个地址

* size()	获得set内元素的个数

* clear()	清空set中的所有元素
* count(u)	查询u在set中出现的次数（0或1）
```





## string

### 使用前添加

```cpp
#include <string>
using namespace std;
```



### 定义

```cpp
string str;

string str = "abcd";  //可以在定义时直接初始化
```

### 访问

####通过下标

```cpp
str[index]
```

如果要读入和输出整个字符串，则只能用cin和cout

```cpp
#include <iostream> //cin和cout在iostream头文件中
#include <string>
using namespace std;

int main(void)
{
	string str;
	cin >> str;
	cout << str;
	return 0;
}
```



用`c_str()`将string类型转换为字符数组，用printf进行输出

```cpp
#include <iostream> //cin和cout在iostream头文件中
#include <string>
using namespace std;

int main(void)
{
	string str = "abcd";
	printf("%s", str.c_str());
	return 0;
}
```



#### 通过迭代器

##### 定义

```cpp
string::iterator it;
```

通过*it来访问string里的每一位

```cpp
#include <iostream>
#include <string>
using namespace std;

int main(void)
{
	string str = "abcd";

	for (string::iterator it = str.begin(); it != str.end(); it++)
		printf("%c", *it);
	return 0;
}
```

**string和vector一样，支持直接对迭代器进行加减某个数字**，如str.begin() + 3的写法是可行的



### 常用函数

* operator+=		将两个string直接拼接起来

  ```cpp
  #include <iostream>
  #include <string>
  using namespace std;
  
  int main(void)
  {
  	string str1 = "abc", str2 = "xyz", str3;
  	str3 = str1 + str2;  //将str1和str2拼接起来，赋值给str3
  	str1 += str2;  //将str2直接拼接到str1上
  	cout << str1 << endl;
  	cout << str3 << endl;
  	//abcxyz
  	return 0;
  }
  ```

* compare operator

  两个string类型可以直接使用==、!=、<、<=、>、>=比较大小，比较规则是字典序

  ```cpp
  #include <iostream>
  #include <string>
  using namespace std;
  
  int main(void)
  {
  	string str1 = "aa", str2 = "aaa", str3 = "abc", str4 = "xyz";
  	if (str1 < str2)
  		cout << "ok1" << endl;
  	if (str1 != str3)
  		cout << "ok2" << endl;
  	if (str4 > str3)
  		cout << "ok3" << endl;
  
  	return 0;
  }
  
  ```

* length()/size()

  ```cpp
  str.size();
  ```

* insert()

  * insert(pos, string)		在pos号位置插入字符串string

    ```cpp
    string str1 = "abcxyz", str2 = "opa";
    str1.insert(3, str2);  //往str2[3]处插入opq，这里str2直接写成"opq"也是可以的
    
    //abcopqxyz
    ```

  * insert(it, it2, it3)    it为原字符串的欲插入位置，it2和it3为待插入字符串的首尾迭代器，用来表示串[it2, it3)将被插在it的位置上

    ```cpp
    #include <iostream>
    #include <string>
    using namespace std;
    
    int main(void)
    {
    	string str = "abcxyz", str2 = "opq";
    	str.insert(str.begin() + 3, str2.begin(), str2.end());
    	return 0;
    }
    ```

    

* erase()
  * str.erase(it)用于删除单个元素，it为需要删除的元素的迭代器
  * str.erase(first, last)   first为需要删除区间的起始迭代器，last为需要删除区间的末尾迭代器的下一个地址
  * str.erase(pos, length)，pos为需要开始删除的起始位置（整数），length为删除的字符个数



* clear()  清空string中的数据

* substr(pos, len)   返回从pos位开始、长度为len的子串

* string::npos

  string::npos是一个常数，其本身的值为-1，但由于是unsigned_int类型，因此实际上也可以认为是unsigned_int类型的最大值。string_npos用以作为find函数失配时的返回值。

  ```cpp
  #include <iostream>
  #include <string>
  using namespace std;
  
  int main(void)
  {
  	if (string::npos == -1)
  		cout << "-1 is true." << endl;
  	if (string::npos == 4294967295)
  		cout << "4294967295 is also true." << endl;
  
  	return 0;
  }
  ```

* find()
  * str.find(str2)  当str2是str的子串（str也可以是一个字符）时，返回其在str中第一次出现的位置（字符串中字符的位置编号从0开始）；如果str2不是str的子串，那么返回string::npos
  * str.find(str2, pos)  从str的pos号位开始匹配str2，返回值与上相同

* replace()
  * str.replace(pos, len, str2)  把str从pos号位开始、长度为len的子串替换为str2
  * str.replace(it1, it2, str2)  把str的迭代器[it1, it2)范围的子串替换为str2



### 注：

可以直接将字符和string类型的字符串通过`+`拼接起来

```cpp
string str;
str = '0' + str;
```

但是，不能加上一个整数，以下两种都是错误的

```cpp
str = '0' + 2 + str;
str = ('0' + 2) + str;
```

应改为

```cpp
str = char('0' + 2) + str;
```





## map

map可以将任何基本类型（包括STL容器）映射到任何基本类型（包括STL容器）

### 使用前添加

```c++
#include <map>
using namespace std;
```

### 定义

```c++
map<typename1, typename2> mp;

map<int, int> mp;
map<string, int> mp;
map<set<int>, string> mp;
```

### 访问

#### 通过下标

```c++
map<char, int> mp;
mp['a'] = 20;
printf("%d", mp['a']);
```

#### 通过迭代器

##### 定义

```c++
map<typename1, typename2>::iterator it;
```

通过`it->first`访问键，`it->second`访问值

#####代码

```cpp
#include <stdio.h>
#include <map>
#include <iostream>
using namespace std;
int main(void)
{
	set<int> st;
	for (int i = 0; i < 3; i++)
		st.insert(i);

	map<char, int> mp;
	mp['a'] = 1;
	mp['b'] = 2;
	mp['c'] = 3;
	for (map<char, int>::iterator it = mp.begin(); it != mp.end(); it++)
		cout << it->first << it->second << endl;
}
```

**map会以键从小到大的顺序自动排序**





### 插入

```cpp
#include <iostream>
#include <map>
#include <string>
using namespace std;

int main(void)
{
	map<int, string> mp;
	mp.insert(make_pair(0, "zero"));
	mp.insert(pair<int, string>(1, "one"));

	mp[2] = "two";

	for (map<int, string>::iterator it = mp.begin(); it != mp.end(); it++)
	{
		cout << it->first << " " << it->second << endl;
	}

}
```



以上三种用法，虽然都可以实现数据的插入，但是它们是有区别的，当然了第一种和第二种在效果上是完成一样的，用insert函数插入数据，在数据的 插入上涉及到集合的唯一性这个概念，即当map中有这个关键字时，insert操作是不能在插入数据的，但是用数组方式就不同了，它可以覆盖以前该关键字对 应的值

### 常用函数

```cpp
* find(key)		返回键为key的映射的迭代器
    
* erase()
    mp.erase(it)	it为需要删除元素的迭代器
    mp.erase(key)	key为欲删除的映射的键
    mp.erase(first, last)	first为需要删除区间的起始迭代器，last为需要删除区间的末尾迭代器的下一个地址
    
* size()	获得map中映射的对数
    
* clear()	清空map中的所有元素
    
* count(x)	x为数对中的first，返回个数，即：有则返回1，没有则返回0
```



```cpp
#include <iostream>
#include <map>
using namespace std;

map<int, int> mp;

int main()
{
	mp[1] = 0;
	cout << mp.count(1) << endl;  //1
	cout << mp.count(2) << endl;  //0
	cout << mp.count(2) << endl;  //0
}
```





### 注

如果有`map<int, int> mp`，但实现并没有存储`mp[0]`而直接输出时，`mp[0]`为0

如果有`map<string, string> mp`，但并没有存储`mp["s"]`而直接输出时，`mp["s"]`为空字符串`""`。

```cpp
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main(void)
{
	map<string, int> m;
	cout << m["jjj"] << endl;
}

//输出0
```



## queue

### 使用前添加

```cpp
#include <queue>
using namespace std;
```

### 定义

```cpp
queue<typename> name;
```



### 常用函数

```cpp
* push()	入队
* front()	获得队首元素
* back()	获得队尾元素
* pop()		队首元素出队
```



## priority_queue

### 使用前添加

```cpp
#include <queue>
using namespace std;
```

### 定义

```cpp
priority_queue<typename> name;
```

### 访问

只能通过`top()`函数访问队首元素（也可以称为堆顶元素），即优先级最高的元素。

``` cpp
#include <iostream>
#include <queue>
using namespace std;

int main(void)
{
	priority_queue<int> q;
	q.push(3);
	q.push(4);
	q.push(1);
	cout << q.top() << endl;

	return 0;
}
```

### 常用函数

```markdown
* push()  q.push(x)将x入队

* top()   q.top()获得队首元素

* pop()   q.pop()令队首元素（即堆顶元素）出队

* empty()  检测优先队列是否为空，返回true则空，返回false则非空

* size()  返回优先队列内元素的个数
```



### 元素优先级的设置

#### 基本数据类型

（int、double、char等），优先队列对它们的优先级设置一般是数字大的优先级越高（如果是char型，则是字典序最大的）。对基本数据类型来说，下面两种优先队列的定义时等价的（以int型为例，注意最后两个>之间有一个空格）

```cpp
priority_queue<int> q;
priority_queue<int, vector<int>, less<int> > q;
```

第二种定义方式的尖括号内多出了两个参数：一个是vector<int>，另一个是less<int>。其中vector<int>填写的是来承载底层数据结构堆（heap）的容器，如果第一个参数是double或char型，则此处填写的是vector<double>或vector<char>；而第三个参数less<int>则是对第一个参数的比较类，less<int>表示数字大的优先级大，而greater<int>表示数字小的优先级越大。

如果想让优先队列总是把最小的元素放在队首，只需进行如下定义：

```cpp
priority_queue<int, vector<int>, greater<int> > q;
```



#### 结构体

**小于号的作用不变（return中还是小于号），则数字大的优先级高**

对水果的名称和价格建立一个结构体

```cpp
struct fruit{
    string name;
    int price;
}
```

现在希望按水果的价格高的为优先级高，就需要重载（overload）小于号“<”。重载是指对已有的运算符进行重新定义，也就是说，可以改变小于号的功能（例如把它重载为大于号的功能）。

```cpp
struct fruit{
    string name;
    int price;
    friend bool operator < (fruit f1, fruit f2)
    {
        return f1.price < f2.price;
    }
}
```

可以看到，fruit结构体中增加了一个函数，其中“friend”为友元。后面的`bool operator < (fruit f1, fruit f2)`对fruit类型的操作符`<`进行了重载（重载大于号会编译错误，因为从数字上来说只需要重载号，即f1 > f2等价于判断f2 < f1，而f1 == f2则等价于判断!(f1 < f2) && !(f2 < f1)，函数内部为`return f1.price < f2.price`，因此重载后小于号还是小于号的作用。此时就可以直接定义fruit类型的优先队列，其内部就是以价格高的水果为优先级高。

```cpp
priority_queue<fruit> q;
```

同理，如果想要以价格低的水果为优先级高，那么只需要把return中的小于号改为大于号即可。

```cpp
#include <iostream>
#include <string>
#include <queue>
using namespace std;

struct fruit {
	string name;
	int price;
	friend bool operator < (fruit f1, fruit f2)
	{
		return f1.price > f2.price;
	}
}f1, f2, f3;

int main(void)
{
	priority_queue<fruit> q;

	f1.name = "桃子";
	f1.price = 3;

	f2.name = "梨子";
	f2.price = 4;

	f3.name = "苹果";
	f3.price = 1;

	q.push(f1);
	q.push(f2);
	q.push(f3);

	cout << q.top().name << " " << q.top().price << endl;

	return 0;
}
```

此处对小于号的重载与排序函数sort中的cmp函数有些相似，它们的参数都是两个变量，函数内部都是return了true或者false。事实上，这两者的作用确实是类似的，只不过效果看上去似乎是“相反的”。在排序中，如果是`return f1.price > f2.price`，那么则是按价格从高到低排序，但是在优先队列中却是把价格低的放到队首。原因在于，优先队列本身默认的规则就是优先级高的放在队首，因此把小于号重载为大于号的功能时只是把这个规则反向了一下。



跟sort中的cmp函数那样写在结构体外面：只需要把friend去掉，把小于号改成一对小括号，然后把重载的函数写在结构体外面，然后把重载的函数写在结构体外面，同时将其用struct包装起来，如下

```cpp
struct cmp {
	bool operator () (fruit f1, fruit f2)
	{
		return f1.price > f2.price;
	}
};
```

在这种情况下，需要用之前讲解的第二种定义方式来定义优先队列：

```cpp
priority_queue<fruit, vector<fruit> cmp> q;
```

可以看到，此处只是把greater<>部分换成了cmp

```cpp
#include <iostream>
#include <string>
#include <queue>
using namespace std;

struct fruit {
	string name;
	int price;
}f1, f2, f3;

struct cmp {
	bool operator () (fruit f1, fruit f2)
	{
		return f1.price > f2.price;
	}
};

int main(void)
{
	priority_queue<fruit, vector<fruit>, cmp> q;

	f1.name = "桃子";
	f1.price = 3;

	f2.name = "梨子";
	f2.price = 4;

	f3.name = "苹果";
	f3.price = 1;

	q.push(f1);
	q.push(f2);
	q.push(f3);

	cout << q.top().name << " " << q.top().price << endl;

	return 0;
}
```

最后指出，如果结构体内的数据较为庞大（例如出现了字符串或者数组），建议使用引用来提高效率，此时比较类的参数中需要加上`const`和`&`，如下所示：

```cpp
friend bool operator < (const fruit & f1, const fruit & f2)
    return f1.price < f2.price;


bool operator () (const fruit& f1, const fruit & f2)
    return f1.price < f2.price;

```



### 应用

* 可以采用从小到大的优先队列实现哈夫曼树的计数



## deque

### 使用前添加

```cpp
#include <deque>
using namespace std;
```



### 定义

```cpp
deque<typename> name;

deque<int> d;
```



### 常用函数

```markdown
* begin()		返回指向容器中第一个元素的迭代器
* end()			返回指向容器中最后一个元素所在位置后一个位置的迭代器
* rbegin()		返回指向最后一个元素的迭代器
* rend()		返回指向第一个元素所在位置的前一个位置的迭代器
* size()		返回实际元素个数
* empty()		判断容器中是否有元素，若无元素，则返回true，否则返回false
* front()		返回第一个元素的引用
* back()		返回最后一个元素的引用
* push_back()	在序列的尾部添加一个元素
* push_front()	在序列的头部添加一个元素
* pop_back()	移除容器尾部的元素
* pop_front()	移除容器头部的元素
```







## stack

### 使用前添加

```cpp
#include <stack>
using namespace std;
```

### 定义

```cpp
stack<typename> name;
```

### 访问

只能通过`top()`访问栈顶元素

```cpp
st.top()
```

### 常用函数

```markdown
* push()  st.push(x)将x入栈

* top()	  st.top()获得栈顶元素

* pop()	  st.pop()弹出栈顶元素

* empty()  st.empty()检测stack内是否为空，返回true为空，返回false为非空

* size()  st.size()返回st内的元素个数
```



## pair

### 使用前添加

```cpp
#include <utility>
using namespace std;
```

注：由于map的内部实现中设计pair，因此添加map头文件时会自动添加utility头文件，此时如果需要使用pair，就不需要额外再去添加utility头文件了。因此，记不住“utility”拼写的读者可以偷懒的用map头文件来代替utility头文件。

### 定义

pair有两个参数，分别对应first和second的数据类型，它们可以是任意的基本数据类型或容器

```cpp
pair<typename1, typename2> name;
```

```cpp
pair<string, int> p;

pair<string, int> p("haha", 5);//后面跟上填写有想要初始化的元素的小括号进行初始化
```



如果想要在代码中临时构建一个pair，有如下两种方法

* `pair<string, int>("haha", 5)`
* `make_pair("haha", 5)`



### 访问

按结构体的方式去访问

```cpp
#include <iostream>
#include <utility>
#include <string>
using namespace std;

int main(void)
{
	pair<string, int> p;
	p.first = "haha";
	p.second = 5;

	cout << p.first << " " << p.second << endl;

	p = make_pair("xixi", 55);
	cout << p.first << " " << p.second << endl;

	p = pair<string, int>("heihei", 555);
	cout << p.first << " " << p.second << endl;

	return 0;
}
```



### 常用函数

* 比较操作数  	两个pair类型数据可以直接使用==、!=、<、<=、>、>=比较大小，比较规则是先以first的大小作为标准，只有当first相等时才去判别second的大小

```cpp
pair<int, int> p1(5, 10);
pair<int, int> p2(2, 5);

if(p1 < p2) printf("y");
```

### 用途

1. 用来代替二元结构体及其构造函数
2. 作为map的键值对来进行插入

```cpp
#include <iostream>
#include <string>
#include <map>
using namespace std;

int main(void)
{
	map<string, int> mp;
	mp.insert(make_pair("haha", 5));
	mp.insert(pair<string, int>("heihei", 10));

	for (map<string, int>::iterator it = mp.begin(); it != mp.end(); it++)
		cout << it->first << " " << it->second << endl;
	return 0;
}
```



## algorithm头文件下的常用函数

需要在头问下加一行`using namespace std;`才能正常使用

### max()、min()和abs()

max(x, y)和min(x, y)分别返回x和y中的最大值和最小值，且参数必须是两个（可以是浮点数）。如果想返回三个数x、y和z的最大值，可以使用max(x, max(y, z))的写法。

abs(x)返回x的绝对值。注意：x必须是整数，浮点型的绝对值请用math头文件下的fabs。



### swap()

swap(x, y)用来交换x和y的值



### reverse()

reverse(it, it2)可以将数组指针在[it, it2)之间的元素或容器的迭代器在[it, it2)范围内的元素进行反转。



### fill()

fill()可以把数组或容器中的某一段区间赋为相同的值。和memset不同，这里的赋值可以是数组类型对应范围中的任意值。

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
int main(void)
{
    int a[5] = {1, 2, 3, 4, 5};
    fill(a, a + 5, 233);  //将a[0]~a[4]均赋值为233
    for(int i = 0; i < 5, i++)
        cout << a[i] << " ";
}

/*
a为起始元素的地址，5为元素
*/
```





### sort()

####使用方式

```markdown
sort(首元素地址（必填）, 尾元素地址的下一个地址（必填）, 比较函数（非必填）);
```

如果不写比较函数，则默认对前面给出的区间进行递增排序。



#### 实现基本比较函数cmp

##### 基本数据类型数组的排序

若比较函数不填，则默认从小到大的顺序排序。

如果想要从大到小来排序，则要使用比较函数cmp来“告诉”sort何时要交换元素（让元素的大小比较关系反过来）。

```cpp
#include <stdio.h>
#include <iostream>
#include <algorithm>
using namespace std;

bool cmp(int a, int b)
{
	return a > b;  //可以理解为当a > b时把a放在b前面
}

int main(void)
{
	int a[] = { 3, 1, 4, 2 };
	sort(a, a + 4, cmp);

	for (int i = 0; i < 4; i++)
		cout << a[i] << " ";

	return 0;
}
```

对double和char型的数组排序只需要把上面的int改成double或者char即可。

记忆方法：如果要把数据从小到大排序，那么就用”<“，因为”a < b“就是左小右大；如果要把数据从大到小排列，那么就用”>“，因为”a > b“就是左大右小。

##### 结构体数组的排序

如果想将ssd数组按照x从大到小排序（即进行一级排序），则代码如下：

```cpp
#include <stdio.h>
#include <iostream>
#include <algorithm>
using namespace std;

struct node {
	int x, y;
}ssd[10];

bool cmp(node a, node b)
{
	return a.x > b.x;  //按x值从大到小对结构体数组排序
}

int main(void)
{
	ssd[0].x = 2;
	ssd[0].y = 2;

	ssd[1].x = 1;
	ssd[1].y = 3;

	ssd[2].x = 3;
	ssd[2].y = 1;

	sort(ssd, ssd + 3, cmp);

	for (int i = 0; i < 3; i++)
		cout << ssd[i].x << " " << ssd[i].y << endl;
}
```



而如果想先按x从大到小排序，但当x相等的情况下，按照y的大小从小到大来排序（即进行二级排序），那么cmp的写法是：

```cpp
bool cmp(node a, node b)
{
    if(a.x != b.x)	
        return a.x > b.x;
    else
        return a.y < b.y;
}
```



##### 容器的排序

在STL标准容器中，只有vector、string、deque是可以使用sort的。这是因为像set、map这种容器是用红黑树实现的，元素本身有序，故不允许使用sort排序。

以vector为例：

```cpp
#include <stdio.h>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

bool cmp(int a, int b)  //因为vector中的元素为int型，因此仍然是int的比较
{
	return a > b;
}

int main(void)
{
	vector<int> v;
	v.push_back(3);
	v.push_back(1);
	v.push_back(2);

	sort(v.begin(), v.end(), cmp);

	for (int i = 0; i < 3; i++)
		cout << v[i] << " ";
}
```



string的排序

```cpp
#include <stdio.h>
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;


int main(void)
{
	string str[3] = { "bbbb", "cc", "aaa" };
	sort(str, str + 3);  //将string型数组按字典序从小到大输出

	for (int i = 0; i < 3; i++)
		cout << str[i] << endl;

	return 0;

}
```



如果上面这个例子中，需要按字符串长度从小到大排序，可以这样写：

```cpp
#include <stdio.h>
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

bool cmp(string str1, string str2)
{
	return str1.length() < str2.length();
}

int main(void)
{
	string str[3] = { "bbbb", "cc", "aaa" };
	sort(str, str + 3, cmp);  //将string型数组按字典序从小到大输出

	for (int i = 0; i < 3; i++)
		cout << str[i] << endl;

	return 0;

}
```



## lower_bound()和upper_bound()

lower_bound()和upper_bound()需要用在一个有序数组或容器中。

lower_bound(first, last, val)用来寻找在数组或容器的[first, last)范围内第一个值大于等于val元素的位置，如果是数组，则返回该位置的指针；如果是容器，则返回该位置的迭代器。

upper_bound(first, last, val)用来寻找在数组或容器的[first, last)范围内第一个值大于val元素的位置，如果是数组，则返回该位置的指针；如果是容器，则返回该位置的迭代器。

显然，如果数组或容器中没有需要寻找的元素，则lower_bound()和upper_bound()均返回可以插入该元素的位置的指针或迭代器（即假设存在该元素时，该元素应当在的位置）。

```cpp
#include <stdio.h>
#include <algorithm>
using namespace std;
int main(void)
{
	int a[10] = { 1, 2, 2, 3, 3, 3, 5, 5, 5, 5 };

	//寻找-1
	int* lowerPos = lower_bound(a, a + 10, -1);
	int* upperPos = upper_bound(a, a + 10, -1);
	printf("%d, %d\n", lowerPos - a, upperPos - a);

	//寻找1
	lowerPos = lower_bound(a, a + 10, 1);
	upperPos = upper_bound(a, a + 10, 1);
	printf("%d, %d\n", lowerPos - a, upperPos - a);

	//寻找3
	lowerPos = lower_bound(a, a + 10, 3);
	upperPos = upper_bound(a, a + 10, 3);
	printf("%d, %d\n", lowerPos - a, upperPos - a);

	//寻找6
	lowerPos = lower_bound(a, a + 10, 6);
	upperPos = upper_bound(a, a + 10, 6);
	printf("%d, %d\n", lowerPos - a, upperPos - a);

	return 0;
}
```

显然，如果只是想获得欲查元素的下标，就可以不使用临时指针，而直接令返回值减去数组首地址即可：


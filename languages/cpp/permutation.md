# Permutation in C++

C++ algorithm standard library에서는 `next_permutation()`이라는 순열을 구하는 함수를 제공한다.

숫자 배열 또는 문자열을 받아 가능한 순열을 만들어준다.
예를 들어 `1, 2, 3`이라는 숫자들로 순열을 만든다면, 가능한 순열은 `(1, 2, 3), (1, 3, 2), (2, 1, 3), (2, 3, 1), (3, 1, 2), (3, 2, 1)`로 총 6가지 이다.

모든 순열을 만들고 나면 `false`를 return 한다. 그리고 vector를 permutation으로 iterate하기 전에는 반드시 sort하도록 하자. 그렇지 않으면 예상했던 개수만큼의 순열을 얻지 못하는 비극이 찾아온다.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    vector<int> num = {1, 2, 3};
    do {
        for (auto i: num) {
            cout << i << " ";
        }
        cout << "\n";
    } while(next_permutation(num.begin(), num.end()));

    return 0;
}
```

```
1 2 3 
1 3 2 
2 1 3 
2 3 1 
3 1 2 
3 2 1 
```

# Combination in C++

이 `next_permutation()`을 이용하면 조합(Combination)을 만들 수 있다!

재미있는 트릭을 이용하는데, n Combination r을 만드는 것을 가정해보자.
`n = 3, r = 2` 즉 주어진 3개 중 2개를 뽑는 경우를 생각해보자.

먼저 주어진 숫자 3개를 먼저 벡터에 저장해 두자.
새로운 벡터를 만들어 숫자를 뽑을지 말지 정보를 저장하자.
이 벡터에는 0(안 뽑음), 1(뽑음) 두가지 element만 store 한다.

이 binary 정보를 가진 벡터를 `next_permutation`을 이용해 iterate 하자.
iterate 할 때 element의 값이 1이면, 그 index로 주어진 숫자를 저장해둔 벡터에 access하자.
당연히 0이면 안 가져오면 된다.

말로 표현하자니 모호한 부분이 많은 것 같다. 코드를 통해 살펴보자.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int n = 3, r = 2;
    vector<int> num = {1, 2, 3};

    vector<int> isIncluded;
    for (int i = 0; i < r; i++) {
        isIncluded.push_back(1);
    }

    for (int i=0; i < n-r; i++) {
        isIncluded.push_back(0);
    }

    sort(isIncluded.begin(), isIncluded.end());

    do {
        for (int i = 0; i < n; i++) {
            if (isIncluded[i] == 1) {
                cout << num[i] << " ";
            }
        }
        cout << "\n";
    } while (next_permutation(isIncluded.begin(), isIncluded.end()));

    return 0;
}
```

```
2 3 
1 3 
1 2
```

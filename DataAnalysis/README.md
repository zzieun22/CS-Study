- **	작성자** : 박지은
- **최초 작성일** : 21. 03 .28
- **마지막 수정일** : 21. 03. 28
- 이것이 데이터 분석이다 책 따라하기 

## 목차

[1.개발환경 구축](#개발환경_구축)

[2. 라이브러리](#라이브러리)

[3. 데이터 분석](#데이터분석)

[4.텍스트마이닝](텍스트마이닝 )

# 개발환경_구축

### 아나콘다 설치 

1. https://www.anaconda.com/products/individual/download-success 에서 다운 

2. 설치 완료 후 아나콘다 프롬포트 실행 
3. 가상환경 생성 
   1. "conda --version" 버전확인 후
   
   2. "conda create -n pybook python=3.7" pybook이라는 파이썬3.7 버전의 새로운 가상환경 생성
   
   3. 주피터 노트북 설치 "pip install jupyter"
   
   4. 주피터 노트북 실행 "jupyter notebook"
   
   5. 주피터 노트북 접속 : 출력된 url복사해서  웹브라우저에서 실행 
   
      ![url](https://user-images.githubusercontent.com/36434665/112743441-4f396e00-8fd2-11eb-83f6-8484ba7af508.png)
   
      ![2  page](https://user-images.githubusercontent.com/36434665/112743443-519bc800-8fd2-11eb-9741-b69360fbca9a.png)
   
   6. New - python 3 버튼눌러서 새 파일 생성 

#### 라이브러리 설치 

1. pip isntall pandas numpy matplotlib

> 판다스 , 넘파이 , matplotlib설치 





## 라이브러리

#### 판다스 

판다스는 데이터 분석 라이브러리로 데이터 프레임 이라는 자료구조를 사용한다. 

엑셀 스프레드시트 형태 > 파이썬을 쉽게 처리한다. 





##### 따라해보기

2개의 열데이터를 입력후, list()와 zip() 함수로 데이터 셋 생성해보기 

head()함수로 생성된 데이터 프레임 

```python
import pandas as pd

names = ['Bob','Jessica' ,'Mary' , 'John', 'Mel']
births = [968,155,77,578,973]
custom = [1,5,25,13,23232]

BabyDataSet = list(zip(names,births))
df = pd.DataFrame(data = BabyDataSet, columns=['Names','Births'])
df.head()
```

<u>결과</u> 



![캡처](https://user-images.githubusercontent.com/36434665/112743445-53658b80-8fd2-11eb-834c-ee556a9d7c7b.PNG)



**데이터 프레임 기본정보 출력**

```python
df.dtypes
df.index
df.columns
```

dtypes, index, columns 로 데이터 프레임의 행 렬 정보를 출력할 수 있다. 

dtypes : 열타입의 정보

index : 행의 형태 정보

columns : 데이터 프레임의 열 정보 



**행열 각각 출력**

하나의 열 'Name'을 선택해서 모두 출력

```
df['Names']
```

0~3번째 인덱스를 출력 

```
df[0:3]
```



**필터링 기능** 

Briths열에 해당하는 데이터가 100보다 큰 경우만 반환

```
df[df['Births']>100]
```



**평균값 계산**

'Names'는 계산을 못하니, Births 만 평균값으로 계산된다. 

mean() 은 각각 테이터 타입을 체크 한 뒤 연산이 간으한 열으리 평균값만을 반환함

```
df.mean()
```





#### 넘파이 설치, 활용

넘파이는 수치계산을 위해 만들어진 파이썬 라이브러리.

넘파이에서 배열의 개념으로 변수를 사용하며, 벡터,행렬 등의 연산을 쉽고 빠르게 수행하도록 지원한다. 



**실행해보기** 

3*5 배열 15개 생성하기

```python
import numpy as np

arr1 = np.arange(15).reshape(3,5)
arr1
```

<u>결과</u>

```
array([[ 0,  1,  2,  3,  4],
       [ 5,  6,  7,  8,  9],
       [10, 11, 12, 13, 14]])
```





1. 넘파이 배열의 데이터 차원을 호출하는 방법은 **shape**

2. 데이터 타입을 호출하는 방법은 **dtype**

3. 데이터를 생성하는 방법 **zeros( )** 함수 이용 

```python
arr1.shape
#결과 (3, 5)

arr1.dtype
#결과 dtype('int32')

arr3 = np.zeros((3,4))
arr3
# 결과 
array([[0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.]])
```



**데이터 연산**

사칙연산 수행 

```python
arr4 = np.array([
    [1,2,3],
    [4,5,6]
], dtype = np.float64)

arr5 = np.array([
    [7,8,9],
    [10,11,12]
], dtype = np.float64)


# 사칙연산 수행 
print("arr4 + arr5 = ")
print(arr4 + arr5, "\n")
print("arr4 - arr5 = ")
print(arr4 - arr5, "\n")
print("arr4 * arr5 = ")
print(arr4 * arr5, "\n")
print("arr4 / arr5 = ")
print(arr4 / arr5, "\n")

```

```
## 결과
arr4 + arr5 = 
[[ 8. 10. 12.]
 [14. 16. 18.]] 

arr4 - arr5 = 
[[-6. -6. -6.]
 [-6. -6. -6.]] 

arr4 * arr5 = 
[[ 7. 16. 27.]
 [40. 55. 72.]] 

arr4 / arr5 = 
[[0.14285714 0.25       0.33333333]
 [0.4        0.45454545 0.5       ]] 
```

이외에도 다양한 함수를 사용할 수 있다.



#### Matplotlib

matplotlib라이브러리는 데이터를 시각화해주는 가장 기본적인 라이브러리이다. 

```python
%matplotlib inline
#현재 실행중인 주피터 노트북에서 그래프를 출력 가능하도록 선언하는 명령어
import matplotlib.pyplot as plt
```



**그래프 만들기**

1. **막대그래프**

   Matplotlib라이브러리를 사용할때는 그래프 객체라는 것을 생성해주어야 한다. 

   `plt.bar(x,y)`를 실행하면 막대그래프 객체가 생성된다. 그 객체에 다른 요소를 추가해 줄 수 있음 

   `plt.xlabel`, `plt.ylabel`, `plt.title` 은 그래프 객체에 각각 x축 제목, y축 제목, 그래프 전체 제목을 달아주는 코드.

   마지막으로 `plt.show()`를 호출하면 그래프를 출력 할 수 있음 

   

   예시 코드 

   ```
   y = df['Births']
   x = df['Names']
   
   plt.bar(x,y)
   plt.xlabel('Names')
   plt.ylabel('Births')
   plt.title('Bar plot')
   plt.show
   ```

    <u>결과</u> 

![sdfs](https://user-images.githubusercontent.com/36434665/112743928-a2adbb00-8fd6-11eb-852c-3ce5b70b0e9a.PNG)

2. **산점도 그래프** 

   `random.seed()` 함수는 랜덤 추출 시드를 고정한 것이고, 이를 토대로 `random.rand()`함수가 넘파이 배열 타입의 난수를 생성.

   그리고 arrange() 함수는 5의 간격으로 0부터 100까지의 숫자를 생성한 것. 지금까지 데이터를 plt.scatter()함수로 출력한 결과 

   ```python
   #랜덤 추출시드를 고정
   np.random.seed(19920613)
   
   # 산점도 데이터 생성 
   x = np.arange(0.0,100.0,5.0)
   y = (x * 1.5) + np.random.rand(20) * 50
   
   #산점도 데이터 출력
   plt.scatter(x,y,c="b", alpha = 0.5 , label ="scatter point")
   plt.xlabel("X")
   plt.ylabel("Y")
   plt.legend(loc='upper left')
   plt.title('Scatter plog')
   plt.show()
   ```

    <u>결과</u>

![gra2](https://user-images.githubusercontent.com/36434665/112744079-b60d5600-8fd7-11eb-9468-cba546f1f61b.PNG)



## 데이터분석

#### raw data

정제되지 않은 데이터 

> 샘플링 이란 ? 어떤 자료로 부터 일부의 값을 추출하는 행위.



#### 피처 

데이터를 구성하는 요소

ex> 학급의 신체검사 결과 기록한 데이터 --> 키,몸무게,시력 등등이 **피처**이다. 



#### 피처의 속성, 상관관계 탐색, 시각화

- 속성탐색 : 학급 데이터에서 학급 평균키 등등 , "표준편차, 중앙값, 데이터등등 통계값"을 구할 수 있다. 

- 상관관계 탐색 :  ex> 몸무게, 키 와의 상관관계 / 이를 통계적으로 알아 볼 수 있다.
- 데이터 시각화 : 수치적 자료만 가지고는 파악하기 힘든 패턴이나 인사이트를 발견하는데 유용하다. 



**practice**

### 멕시코풍 프렌차이즈 주문 데이터 분석하기



#### 데이터 기초정보 

```python
# -*- coding: utf-8 -*-

import pandas as pd

# read_csv 함수로 데이터를 Dataframe 형태로 불러옵니다.
file_path = '../data/chipotle.tsv'
chipo = pd.read_csv(file_path, sep = '\t')

print(chipo.shape)
print("------------------------------------")
print(chipo.info())
```

**result** 

```
(4622, 5)
------------------------------------
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 4622 entries, 0 to 4621
Data columns (total 5 columns):
 #   Column              Non-Null Count  Dtype 
---  ------              --------------  ----- 
 0   order_id            4622 non-null   int64 
 1   quantity            4622 non-null   int64 
 2   item_name           4622 non-null   object
 3   choice_description  3376 non-null   object
 4   item_price          4622 non-null   object
dtypes: int64(2), object(3)
memory usage: 180.7+ KB
None
```

1. 데이터를 불러오기 위해 read_csv() 함수를 사용해야 한다. 데이터 파일경로 입력 (file_path)
2. shape()와 info()함수를 호출하면 result 와 같은 결과가 나온다.
   1. shpe() 데이터 행과 열 크기를 반환
   2. info() 행의 구성정보와 열의 구성정보를 나타낸다. 
   3. item_name 는 object type 으로 알 수 있는데 이는 "문자열 "을 의미
   4.  null의 뜻은 데이터가 비어있다 "결측값"이다 라는 의미 / not null 은 데이터가 비어있지 않다.



#### 다양한 함수

```
# chipo 라는 Dataframe에서 순서대로 10개의 row 데이터를 보여준다.
chipo.head(10)
print(chipo.columns) # 열정보 출력 
print("------------------------------------")
print(chipo.index) # 행정보 출력
```



**연속형 피처**

quantity, item_price 두 피처는 연속형 피처(어떤 값도 가질 수 있는 연속적인 숫자 형태)

```python
chipo['order_id'] = chipo['order_id'].astype(str) # order_id는 숫자의 의미를 가지지 않기 때문에 str으로 변환

print(chipo.describe()) # chipo dataframe에서 수치형 피처들의 요약 통계량을 확인.

#result 
          quantity
count  4622.000000
mean      1.075725 # 아이템 평균 주문 수량 
std       0.410186
min       1.000000
25%       1.000000
50%       1.000000
75%       1.000000
max      15.000000
```

item_price 같은 경우는 object 타입이기 때문에 **데이터 전처리** 과정을 거쳐야 한다. 



```python
print(len(chipo['order_id'].unique())) # order_id의 개수
print(len(chipo['item_name'].unique())) # item_name의 개수
1834
50
```

unique() 개수 출력 



#### 탐색과 시각화

**가장 많이 주문한 아이템10**

DataFrame['column']의 형태에 value_counts() 함수를 적용한다. 

DataFrame['column'] 은 시리즈라는 객체를 반환하는데 value_counts()는 오직 시리즈 객체에서만 적용된다.

```python
# 가장 많이 주문한 item : top 10을 출력
item_count = chipo['item_name'].value_counts()[:10]
for idx, (val, cnt) in enumerate(item_count.iteritems(), 1):
```



**아이템별 주문 개수와 총량**

groupby() : 데이터 프레임에서 특정 피처를 기준으로 그룹을 생성하여, 이를 통해 그럽별 연산을 적용할 수 있음

​	ex> "학급" 그룹 만들어서 학급별 키,몸무게를 구할 수 있음 

```python
#아이템별 주문개수 출력 
order_count = chipo.groupby('item_name')['order_id'].count()
order_count[:10] ##아이템별 주문 개수 출력

# item당 주문 총량을 출력.
item_quantity = chipo.groupby('item_name')['quantity'].sum()
item_quantity[:10] # item당 주문 총량을 출력.
```



**시각화**

그래프로 시각화 

tolist() 와 넘파이의 arrange() 함수를 이용해 x_pos를 선언하고 0~50 까지 숫자를 x축 이름으로 사용한다.

y값에는 주문 총량인 item_quantity.value.tolist()를 넣어줌 

```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt

item_name_list = item_quantity.index.tolist() # x축에 넣을 값들 리스트 
x_pos = np.arange(len(item_name_list)) # x축에 넣을 값리스트 총 개수
order_cnt = item_quantity.values.tolist() # item_quantity의 개수 리스트 
plt.bar(x_pos, order_cnt, align='center') 
plt.ylabel('ordered_item_count')
plt.title('Distribution of all orderd item')
 
plt.show()
```



##### value_counts()와 unique()의 차이점 ***

```
print((chipo['item_name'].unique())) # order_id의 개수를 출력합니다.
print("------------------------")
print((chipo['item_name'].value_counts())) # order_id의 개수를 출력합니다.
```

```
['Chips and Fresh Tomato Salsa' 'Izze' 'Nantucket Nectar'
 'Chips and Tomatillo-Green Chili Salsa' 'Chicken Bowl' 'Side of Chips'
 'Steak Burrito' 'Steak Soft Tacos' 'Chips and Guacamole'
 'Chicken Crispy Tacos' 'Chicken Soft Tacos' 'Chicken Burrito'
 'Canned Soda' 'Barbacoa Burrito' 'Carnitas Burrito' 'Carnitas Bowl'
.......
-------------------------------
Chicken Bowl                             726
Chicken Burrito                          553
Chips and Guacamole                      479
Steak Burrito                            368
Canned Soft Drink                        301
Chips                                    211
Steak Bowl                               211
Bottled Water                            162
Chicken Soft Tacos                       115
Chips and Fresh Tomato Salsa             110
Chicken Salad Bowl                       110
Canned Soda                              104
Side of Chips                            101
Veggie Burrito                            95
.......
```

unique() : 배열 형태로 출력되며, 개수를 출력안되고 순서없이 유일한 값으로 1개씩 출력됨

```
<class 'numpy.ndarray'> #데이터 형태
```

value_counts() : 테이블 형태로 출력, count된 개수대로 내림차순으로 출력된다.

```
<class 'pandas.core.series.Series'> #데이터 형태
```



#### 데이터 전처리 함수 사용 

item_price 는 object 이기 때문에 피처의 요약 통계를 구할 수 없었다. 



**데이터 전처리 방법**

item_price 는 앞에 $표시가 있었기 때문에 기호 삭제해주는 전처리 작업이 필요함 

chipo['item_price']에 apply()함수를 적용함으로써 가능하다. 

apply()는 lambda라는 함수 명령어를 추가해준다. 

```python
# column 단위 데이터에 apply 함수로 전처리를 적용합니다.
chipo['item_price'] = chipo['item_price'].apply(lambda x: float(x[1:]))
chipo.describe()

#result
 		quantity	item_price
count	4622.000000	4622.000000
mean	1.075725	7.464336
std		0.410186	4.245557
min		1.000000	1.090000
25%		1.000000	3.390000
50%		1.000000	8.750000
75%		1.000000	9.250000
max		15.000000	44.250000
```

**apply()**함수는 시리즈 단위의 연산을 처리하는 기능을 수행 , sum()이나 mean()같이 연산이 정의된 함수를 파라미터로 받는다. 우리가 정의할 새로운함수 문자열 데이터에서 첫번째 문자열을 제거하고 나머지 문자열을 수치로 바꿔주는 함수를 파라미터로 입력할 수 있다. 



#### 탐색적 분석

- sum() : 합계
- info() : 기초적인 정보

- mean() : 평균값 구하기

- sort_values() : 데이터 정렬함수
- drop_duplicates() : 해당 컬럼 중복제거 

> 활용해보기

```python
chipo_one_item = chipo[chipo.quantity == 1] // quantity 가 1인 데이터를 골라서
price_per_item = chipo_one_item.groupby('item_name').min() // item_name이 최솟값인 애들을 골라서
price_per_item.sort_values(by = "item_price", ascending = False)[:10] // item_price기준으로 내림차순 10개를 보여줘라
```



**practice2**

### 국가별 음주데이터 분석

#### 탐색과 시각화

**피처관 상관관계 탐색하는 방법**

1. 피처가 2개일때 상관계수를 계산하는 단순 상관 분석방법
2. 피처가 여러개일때 상호간의 연관성을 분석하는 다중 상관 분석



**실습**

맥주와 와인 소비량의 상관관계

```python
corr = drinks[['beer_servings', 'wine_servings']].corr(method = 'pearson')
print(corr)
# result
               beer_servings  wine_servings
beer_servings       1.000000       0.527172
wine_servings       0.527172       1.000000
```

**pearson** : 상관계수를 구하는 계산 방법 중 하나를 의미하며, 가장 널리 쓰이는 방법

두 피처를 선택 후 corr()함수에 적용. 이를통해 matrix 형태로 출력할 수 있음 



**heatmap, pairplot** 

파이썬의 <u>**seaborn**</u>이라는 시각화 라이브러리를이용해 2의 기법을 사용할 수 있음 

```python
!pip install seaborn
```

아나콘다 프롬포트에서 가상환경을 실행한 상태로 아래 명령어를 입력

heatmap의 경우 corr.values를 

pairplot의 경우 데이터 프레임을 파라미터로 넣어줌 



```python
#heatmap이용 
import seaborn as sns
cols_view = ['beer', 'spirit', 'wine', 'alcohol'] 
sns.set(font_scale=1.5)
hm = sns.heatmap(corr.values,
            cbar=True,
            annot=True, 
            square=True,
            fmt='.2f',
            annot_kws={'size': 15},
            yticklabels=cols_view,
            xticklabels=cols_view)

plt.tight_layout()
plt.show()
```

![img](data:image/png;base64,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)



```python
#pairplot이용 
sns.set(style='whitegrid', context='notebook')
sns.pairplot(drinks[['beer_servings', 'spirit_servings', 
                     'wine_servings', 'total_litres_of_pure_alcohol']], height=2.5)
plt.show()
```

기존의 corr를 이용해서 상관관계를 한눈에 확인 가능함 



#### 탐색적 분석 

**fillna()**

결측 값을 해당하는 데이터로 처리하는 함수

> continent 피처에 존재하는 결측데이터 처리

```python
drinks['continent'] = drinks['continent'].fillna('OT')
```

**plt.pie()**

파이차트로 시각화

> OT 차지하는 비중 찾기

```python
labels = drinks['continent'].value_counts().index.tolist() #continent에 해당하는 list 다 따옴 ['AF', 'EU', 'AS', 'OT', 'OC', 'SA']
fracs1 = drinks['continent'].value_counts().values.tolist() # continent에 해당하는 각각 군집의 개수  53, 45, 44, 23, 16, 12]
explode = (0, 0, 0, 0.25, 0, 0) ## 파이차트중 어떤것에 해당하는걸 조금더 뒤로 뺄지 .. OT 3번째 배열을 조금 더 뒤로 뺀다 

plt.pie(fracs1, explode=explode, labels=labels, autopct='%.0f%%', shadow=True)
plt.title('null data to \'OT\'')
plt.show()
```

![img](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAOcAAAD+CAYAAADBLRJzAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjMuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8vihELAAAACXBIWXMAAAsTAAALEwEAmpwYAABLiElEQVR4nO2dd3hT5/XHP1dbsmV5T7wNBmP2JmGTMMIIkFASQnbTpEk60iQdv7RN0jRpM0pW27QZbZOmDdmEhBCG2XuEYaYBG+8pWZItybqS7u8PgwvBBgO2JJv7eR4/4Kt773tk6Xvfcc57jiBJkoSMjEzQoQi0ATIyMq0ji1NGJkiRxSkjE6TI4pSRCVJkccrIBCmyOGVkghRVoA3o7kycOJFXXnkFh8PB7373O7788ssLnr9ixQref/993nvvvQue9/rrr9O7d28mT57cblv279/Pxx9/zNNPP93ua1577TV27NjRYs+hQ4d45ZVXOHnyJAaDAYPBwD333NNix4IFC3A6nYiiSGFhIb169QIgKyuLtLS0c+4lc2FkcXZRtm/fTlZW1iVdc/z4caqqqi7pGp1Oh16vB5rF/dBDD/H0008zfvx4AE6cOMGPf/xjamtrWbBgAR988AEApaWlzJw5k6VLl7bc680332y5l8zFkcXZTrZv387ixYtJTk6moKAAj8fDU089xZAhQ/jFL35Bz549ueeeewDO+/1ivPLKKyxbtozw8HBSU1NbjhcWFvL000/T2NhITU0NvXv35uWXX+bjjz8mPz+f559/HqVSSVZWVqvnabXalntVVFTw6quvYrfb+eUvf8lzzz3HkiVLeO+991AoFERHR/PrX/+a9PT0c2zLzc3lTJzKK6+8wv33398iTIDMzEyef/557rzzTubOnYtGo2nzfZ59L5mLI885L4H9+/dz99138/nnnzN37lwWL158xfdcvXo1K1eu5PPPP+eDDz6goaGh5bUPP/yQG2+8kQ8//JCVK1dSWlrKunXrWLhwIbm5uTz++ONcd911bZ53NgkJCfzoRz9i6NChPPfcc2zdupW33nqLd999ly+++IIZM2bw4IMPnieeUaNGcd999wGwZ88ehg0bdt57yMnJQRAEjh8/fsH3eva9ZC6OLM5LIDExkT59+gDNX0ir1XrF99y6dSvXXXcdoaGhqFQq5s2b1/LaY489RmRkJG++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)

explode 를 0.25 대신 0.9를 줬을때 

![img](data:image/png;base64,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)



**agg()**

> ##### apply, agg 함수를 이용한 대륙별 분석

agg()는 apply()와 거의 동일한 기능이지만 apply에 들어가는 함수 파라미터를 병렬로 설정하여 **그룹에 해단 연산결과를 동시에 얻을 수 있는 함수**

```python
# 대륙별 spirit_servings의 평균, 최소, 최대, 합계를 계산.
result = drinks.groupby('continent').spirit_servings.agg(['mean', 'min', 'max', 'sum'])
result.head()
```

**idxmax()**

mean()함수를 이용한 탐색 + idxmax()함수를 적용하면 평균 "beer_serving"이 가장 높은 "대륙"이 어딘지 찾을 수 있음.

```python
beer_continent = drinks.groupby('continent').beer_servings.mean().idxmax()
print(beer_continent)
```



#### 통계적 분석

분석 결과에 타당성을 부여하기 위해 통계적으로 차이를 검정하는 과정 

t-test를 통해 분석 대상 간에 통계적 차이를 검정하는 방법

**scipy**를 활용하여 두 집단간의 t-test를 검정 할 수 있음 

```python
!pip install scipy #설치 
```

```python
# 아프리카와 유럽간의 맥주 소비량 차이를 검정
africa = drinks.loc[drinks['continent']=='AF']
europe = drinks.loc[drinks['continent']=='EU']

from scipy import stats
tTestResult = stats.ttest_ind(africa['beer_servings'], europe['beer_servings'])
tTestResultDiffVar = stats.ttest_ind(africa['beer_servings'], europe['beer_servings'], equal_var=False)

print("The t-statistic and p-value assuming equal variances is %.3f and %.3f." % tTestResult)
print("The t-statistic and p-value not assuming equal variances is %.3f and %.3f" % tTestResultDiffVar)

# result 
The t-statistic and p-value assuming equal variances is -7.268 and 0.000.
The t-statistic and p-value not assuming equal variances is -7.144 and 0.000
```

**p-value**

가설이 얼마나 믿을만 한 것인지 나타내는 지표 (ex:  -7.268)

테이터를 새로 샘플링 했을 때 가설이 맞다는 전데하에 현재 나온 통계값 이상이 나올 확률 이라고 정의할 수 있음 

p-value가 너무 낮으면 가설이 일어날 확률이 낮기 때문에 가설을 기각하게 된다. 

이 p-value를 **유의확률** 이라고 한다. 





## 텍스트마이닝 

### 웹크롤링으로 데이터 수집

1. 리스트의 url정보 수집 

### 웹 크롤링 라이브러리 사용

**BeautifulSoup**과 **requset** 라는 라이브러리로 웹 크롤러를 만든다.

**requtests**

특정 URL로부터 HTML문서를 가져오는 작업을 수행 

**BeautifulSoup**

HTML문서에 데이터를 추출하는 작업을 수행



아나콘다 프롬포트에 > 설치 

```
pip install lxml beautifulsoup4 requests
```



requests.get()함수로 URL의 HTML문서를 가져온 뒤, 이를BeautifulSoup()클래스의 soup객체로 변환한다.

find(), find_all() 함수를 사용하여 특정 HTML태그 혹은 특정 HTML클래스를 가진 데이터를 가져온다.

```python
import requests
from bs4 import BeautifulSoup
import re

# 크롤링할 사이트 주소를 정의.
source_url = "https://finance.naver.com/sise/lastsearch2.nhn"

# 사이트의 html 구조에 기반하여 크롤링을 수행.
req = requests.get(source_url)
html = req.content
soup = BeautifulSoup(html, 'lxml')
contents_div = soup.find(name="div" , attrs={"class":"box_type_l"})
contents_table = contents_div.find(name="table")
table_rows = contents_table.find_all(name="tr")

content_list = []
for lists in table_rows: 
    content_list.append(lists.text)

content_list

#result 
['\n순위\n종목명\n검색비율\n현재가\n전일비\n등락률\n거래량\n시가\n고가\n저가\nPER\nROE\n',
 '',
 '\n1\nSK이노베이션\n4.05%\n238,000\n\n\n\t\t\t\t5,500\n\t\t\t\t\n\n\n\n\t\t\t\t-2.26%\n\t\t\t\t\n\n839,964\n241,000\n243,500\n235,000\n-10.27\n-13.58\n',

```


















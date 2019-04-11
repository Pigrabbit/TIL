# Pandas Dataframe

Machine Learning 공부를 시작하게 되면서 pandas python 패키지를 접하게 되었다. 데이터 분석을 할 때 유용하며 Table을 다루기 위해 필요한 Series 및 Dataframe 클래스를 제공한다.

데이터는 직접 table을 만들거나 .csv파일을 읽어올 수도 있다. 물론 excel, json, sql 등 형식의 파일도 read할 수 있다.

``` python
df = pd.readcsv('path')
```

## Dataframe 클래스

Dataframe object 에서 column 접근은 다음과 같이 한다.

``` python
x = df[['Column1', 'Column2', 'Column3']]
y = df[['Column5']]
```


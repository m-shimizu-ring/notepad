# 実践的なSQL

## 様々な関数

1.SUM関数

SQLで数値の合計を計算する場合は、SUMを用います。
「 SUM(カラム名) 」のようにすることで、指定したカラムに保存されたデータの合計を計算することが可能です。
```
SUM(カラム名)
```
SUM関数はSELECTで取得するカラムに用いることで、purchasesテーブルの集計結果を取得することができます。
WHEREを使うことで、太郎が今まで使ったお金の合計金額を取得しています。
```
SELECT SUM(price)
FROM purchases;
WHERE character_name ='太郎'
```

2.AVG関数
SQLで数値の平均を計算する場合は、AVGを用います。
「AVG(カラム名)」のようにすることで、指定したカラムに保存されたデータの平均を計算することが可能です。
```
AVG(カラム名)
```
AVG関数はSELECTで取得するカラムに使用することで、計算結果を取得することができます。
WHEREを使うことで、太郎が買った商品の平均金額を取得しています。
```
SELECT AVG(price)
FROM purchases;
WHERE character_name ='太郎'
```

3.COUNT関数
COUNT関数は、指定したカラムのデータの合計数を計算してくれる関数です。

＊COUNT関数でカラム名を指定した場合、nullになっているデータの数は計算されません。
```
COUNT(カラム名)
```
nullの数も含めてデータの数を計算したい場合は、COUNT関数で * (全てのカラム)を指定します。* を使った場合、特定のカラムのデータの数ではなく、レコードの数を計算します。この方法で、nullの数を含めてデータの数を数えられます。
WHEREによって、太郎がいくつ商品を買ったかを取得しています
```
SELECT COUNT(*)
FROM purchases;
WHERE character_name ='太郎'
```

4.MAX/MIN関数
SQLでMAXという関数を用いると、指定したカラムのデータの中から最大のデータを取得することができます。同じく、MINと言う関数を用いることで、最小のデータを取得することができます。
```
MAX(カラム名)
MIN(カラム名)
```
MAX,MINも他の集計関数と同様にSELECTで取得したカラムに使用することができます。
priceカラムを指定することでもっとも値段が高かった商品のデータを取得することができます。
太郎が使った1番高い金額を取得しています。
```
SELECT MAX(price)
FROM purchases;
WHERE character_name ='太郎'
```

## データのグループ化
GROUP BYを用いると、データをグループ化することができます。「GROUP BY カラム名」とすることで、指定したカラムで、完全に同一のデータを持つレコードどうしが同じグループとなります。

```
GROUP BY カラム名
```
グループ化するには、今までの集計関数を取得するFROMの後ろに「GROUP BY カラム名」を追加します。集計関数により、各グループごとにデータが集計されます。
```
SELECT SUM(price),purchased_at
FROM purchases
GROUP BY purchased_at;
```
＊GROUP BYを用いる場合、SELECTで使えるのは、GROUP BYに指定しているカラム名と、集計関数のみです。
図ではSELECTで集計関数を使っていないため、日付ごとに集計された値が取得できません。
```
 ❌   SELECT price,purchased_at　集計関数を使っていない
      FROM purchases
      GROUP BY purchased_at;
```















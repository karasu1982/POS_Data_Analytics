# 購買データ分析

## 目的

購買データ（POSデータ、ID-POSデータ）というのは、昔から注目されているビッグデータの１つです。

図は10年近く前の情報通信白書ですが、当時時点のさらに約10年前からデータ流通量の１つとしてPOSデータが挙げられます。

2005年時点で、POSデータの流通量は、防犯・遠隔監視カメラ、センサーログに次いで3番目に多い。カメラは画像データ、センサーはログデータだとすると、テーブルデータとしては最も多いことになります。

2013年時点でも全体に占める割合は減少しましたが、順位は変動していません。

![「平成26年版　情報通信白書」図表3-1-2-6　データ流通量の推移（メディア別）](https://www.soumu.go.jp/johotsusintokei/whitepaper/ja/h26/image/n3102060.png)

「平成26年版　情報通信白書」図表3-1-2-6　データ流通量の推移（メディア別）

現時点（2023年）では、その順位も変動してきていそうですが、購買データの量が多いことは間違いなく、テーブルデータを扱う基本の１つとなっています。

そして、そんな歴史のある購買データなので、「購買データ分析」と検索すると、多くのサービスがヒットします。

そのように、かなり一般化されている購買データ分析ですが、ここで改めてナレッジの体系化をしていきます。

## 分析メニュー

上述の通り、「購買データ分析」で検索してみると、次のようなサイトが上位でヒットします。

[購買データとは？分析するメリットや導入しやすい代表的な購買データを紹介 | LISKUL](https://liskul.com/purchasing-data-109069)

[マーケティングコラム | IDレシートBIツール | FeliCa Networks](https://receiptreward.jp/solution/column/purchasing-analysis.html)

それらも参考にしながら、次の分析メニューを解説・実装していきます。（メニューは順次充実化・追加予定）

ここでは、基本的に四則演算のみで実装可能なメニューにしぼって紹介します。機械学習が必要なメニューは別途切り出して解説・実装します。

| 種別 | 分析メニュー | 分析内容 | 集計・分析プログラム |
| --- | --- | --- | --- |
| 全般 | 売上分解分析 |企業や店舗全体の売上がどの様な構成になっていて、何が要因で上昇・下降しているのかを把握するための第一歩となる分析です。  |[売上分解分析](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/%E5%A3%B2%E4%B8%8A%E5%88%86%E8%A7%A3%E3%83%84%E3%83%AA%E3%83%BC.ipynb)  |
|  | 時系列分析 |データを時系列での推移をみていく分析です。売上や株価など、時間軸で変わっていくものの変化を確認するために用いられます。  |[時系列分析](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/%E6%99%82%E7%B3%BB%E5%88%97%E5%88%86%E6%9E%90.ipynb) |
| 顧客観点 | デシル分析 |顧客の一定期間の購買金額に基づいてグループ分けする手法の１つで、購買金額が最も多いグループから最も少ないグループまで、人数が（ほぼ）同じになるように10個に分ける。  |[デシル分析](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/%E3%83%87%E3%82%B7%E3%83%AB%E5%88%86%E6%9E%90.ipynb) |
|  | RFM分析 |顧客の最新購入日(R)、購入頻度(F)、購入金額(M)の3つの軸でグループ分けする  |[RFM分析](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/RFM%E5%88%86%E6%9E%90.ipynb)  |
| 商品観点 | ABC分析 |商品別の売り上げを比較し、売り上げ上位からA, B, Cの3つのグループに分ける。品揃えや商品の入れ替え・在庫管理などに利用される | [ABC分析](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/ABC%E5%88%86%E6%9E%90.ipynb) |
|  | リピート率 |商品別のリピート率（特定の期間内に同じ人に複数回購入される確率）を比較する  |[リピート率](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/%E3%83%AA%E3%83%94%E3%83%BC%E3%83%88%E7%8E%87.ipynb) |
|  | バスケット分析 |商品同士が同時購入される確率から、ある商品の購入者にお勧めする商品を検討する  |[バスケット分析](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/%E3%83%90%E3%82%B9%E3%82%B1%E3%83%83%E3%83%88%E5%88%86%E6%9E%90.ipynb)  |
|  | 購買順分析 |、バスケット分析の応用で、商品Aを買う前に何を買っていたか、買った後に何を買ったかを分析する  |[購買順分析](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/%E8%B3%BC%E8%B2%B7%E9%A0%86%E5%88%86%E6%9E%90.ipynb)  |

※ 集計・分析プログラムについての注意点

データ集計は、Pythonで行うパターンとSQLで行うパターンを、自分なりに最適と思う基準で分けています。

実践を考えたときに、多くのビジネスシーンで、元データ（今回はPOSデータ）がDWH（BigQueryやSnowflakeなどのクラウドも含めたSQLサーバ）に格納されている。それを、集計をするためにわざわざPythonでデータを取得し、Pandasに入れて集計するといったことが適さないケースが多いためです。

ただし、SQLのみで書いてしまうと自身でサーバを用意しないと、実行することができなくなってしまうため、[DuckDB](https://zenn.dev/paxdare_labo/articles/99c4e373a9fb58)を用いてSQLライクな実行を行っていきたいと思います。

## 利用するデータ

購買データでいいサンプルがなかったのですが、[こちら](https://www.kyoritsu-pub.co.jp/book/b10003634.html)の本のデータがよさそうだったので、使ってみましょう。

データ確認については、[こちら](https://github.com/karasu1982/POS_Data_Analytics/blob/main/notebook/%E3%83%87%E3%83%BC%E3%82%BF%E5%8F%AF%E8%A6%96%E5%8C%96.ipynb)にコードを載せていますので、併せてご確認ください。

まずは、データを読み込ませて、そのまま見てみましょう。

|  | Time | CustID | Age | Area | ProductSubClass | ProductID | Amount | Asset | SalesPrice |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 2000-11-01 00:00:00 | 46855 | D | E | 110411 | 4710085120468 | 3 | 51 | 57 |
| 1 | 2000-11-01 00:00:00 | 539166 | E | E | 130315 | 4714981010038 | 2 | 56 | 48 |
| 2 | 2000-11-01 00:00:00 | 663373 | F | E | 110217 | 4710265847666 | 1 | 180 | 135 |
- Time : これは購買日時でしょうね。時間がすべて、00:00:00なので日付のみの項目かもしれません。
- CustID：これは顧客ID。数値で入っていますが、数の大小に意味がないので、STRING型にしておきましょう。（以降のID系も同様）
- Age：年齢という項目ですが、なぜかA, B, C・・・。10代・20代・・・を置き換えているのかもしれませんね。
- Area：エリアという項目ですが、こちらもA, B, C・・・。北海道・東北・・・を置き換えているのかな。店舗のエリアを設定しているのかもしれませんね。
- ProductSubClass：商品のカテゴリのような項目でしょうか。コードなので何を指しているかはわかりませんが、飲料とかパンとか、そういう項目だと想定しておきましょう。
- ProductID****：****商品コードですね。通常の購買データであれば、49/45で始まるJANコードや、それ以外のインストアコードと呼ばれるものが入ります。データでは47はじまりなので、ダミーデータだと考えておきましょう。
- Amount：購入個数ですね。これはINT型でOKですね。（以降の数値系も同様）
- Asset：資産という項目ですが何でしょうか。POSデータの定番といえば、原価か在庫数ということになりますが、ちょっと資産とは違うような。項目値からの推測としては、原価でしょうか。
- SalesPrice：購入単価ですね。Assetを原価とすると、Sales Price - Asset で利益になります。Sales Price < Assetのものは、特売価格なのでしょうか。

### 基準統計量

数値系の項目については、基準統計値を見てみましょう。

| index | Amount | Asset | SalesPrice |
| --- | --- | --- | --- |
| count | 817741\.0 | 817741\.0 | 817741\.0 |
| mean | 1\.3817810284674488 | 112\.10984773907632 | 131\.87558897010177 |
| std | 2\.8974732938939023 | 603\.6617756382111 | 631\.0576333829703 |
| min | 1\.0 | 0\.0 | 1\.0 |
| 25% | 1\.0 | 35\.0 | 42\.0 |
| 50% | 1\.0 | 62\.0 | 76\.0 |
| 75% | 1\.0 | 112\.0 | 132\.0 |
| max | 1200\.0 | 432000\.0 | 444000\.0 |

Amountが75%点でも1個なのに、maxだと1200個。極端な外れ値ですね。（Asset, SalesPriceも同様ですが）

テストではない実際の購買データでの外れ値だとすると、業者による購入か・爆買いか・店舗間の在庫移動か。。。と妄想してしまいますね。

### グラフによる見える化

グラフの練習も兼ねて、色々なグラフをつくりつつ、データを見ていきましょう。

【ヒストグラム】

Amount別の件数を見てみましょう。ただし、上述のようにAmountは外れ値があるため、10個までの範囲でグラフ化しています。

圧倒的に、1個か2個購入するケースが多いことが、グラフからもわかりますね。

![image](https://github.com/karasu1982/POS_Data_Analytics/assets/22285502/78b1918a-a17e-4601-8853-229eff986743)

【棒グラフ】

横にエリア・縦にSalesPriceの平均値でグラフ化しています。

エリアG（どこか知りませんが）の平均単価が頭一つ高いですね。高級品を買ってくれやすいエリアなのでしょうか。

![image](https://github.com/karasu1982/POS_Data_Analytics/assets/22285502/994e2041-8780-4e50-960a-31c8bcaceb6b)


【散布図】

SalesPriceとAmountで散布図をつくっています。かつ、ポイントの色をエリアで分けています。

ちょっとこれだけだと、わかりづらいですね。AmountとSalesPriceは、基本相関が高いわけではないので、こんなもんでしょうか。

![image](https://github.com/karasu1982/POS_Data_Analytics/assets/22285502/2ae034c5-8927-46bc-b4cb-09e8bea4580f)


【箱ひげ図】

Amountについての箱ひげ図を、Age別に作成しています。

![image](https://github.com/karasu1982/POS_Data_Analytics/assets/22285502/599921e5-a68b-4418-a934-f3288b7de150)


ただ、これだと、ちょっと外れ値が多すぎるので、Amountが200以下に絞ってみましょう。

すると、平均値はほぼ同程度のようですが、A, G, H, I ,Kが上に突き抜けているケースが少ないですね。

![image](https://github.com/karasu1982/POS_Data_Analytics/assets/22285502/8bfe759e-0bf0-44eb-99d4-9e58601c61dc)


ただ、これでも数件の外れ値なので、実際には25以下とかに絞るといいかもしれませんね。

【ヒートマップ】

数値同士の相関係数を可視化するヒートマップです。

数値項目がすくないため、SalesPriceとAssetがほぼ1.0で、SalesPriceとAmountが0.44というくらいで、情報量は少ないですが、項目が多くなると重要な見える化になります。

![image](https://github.com/karasu1982/POS_Data_Analytics/assets/22285502/22fed27f-517c-46b0-9d21-7320d96e6fcc)


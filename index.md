# 湘南医療大学　統計学

<div style="text-align: center;">このサイトのURLはhttps://akrgt.github.io/2021statistics/です．</div>

<div align="center">
<img src="qr.png" title="講義サイトqrコード">
</div>



## 第1講(11/16)

* [講義資料（スライド）](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/1st.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_1st.html)



## 第2講/第3講(11/30)

* [講義資料](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/2nd3rd.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_2nd3rd.html)
* [dataの説明](https://akrgt.github.io/2021statistics/page/data_table.html)
* [data](https://raw.githubusercontent.com/akrgt/2021statistics/gh-pages/data/exdataset.csv)
  * 画面を表示してから，csvファイルとして保存します．



## 第4講/第5講(12/07)

* [講義資料](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/4th5th.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_4th5th.html)
* [dataの説明](https://akrgt.github.io/2021statistics/page/data_table.html)
* [data](https://raw.githubusercontent.com/akrgt/2021statistics/gh-pages/data/exdataset.csv)
  * 画面を表示してから，csvファイルとして保存します．

  

## 第6講/第7講(12/14)

* [講義資料](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/6th7th.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_6th7th.html)

  

## 第8講/第9講(12/21)

* [講義資料](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/8th9th.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_8th9th.html)
* [講義資料（code）](https://github.com/akrgt/2021statistics/blob/gh-pages/code/8th9th.md)


  

## 第10講/第11講(01/11)

* [講義資料](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/10th11th.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_10th11th.html)
  
```
## Reordering exdataset$MAR
exdataset$MAR <- factor(exdataset$MAR,
  levels = c("NotMarried", "Married")
)

## Recoding exdataset$MAR into exdataset$MAR01
exdataset$MAR01 <- fct_recode(exdataset$MAR,
  "0" = "NotMarried",
  "1" = "Married"
)
exdataset$MAR01 <- as.numeric(as.character(exdataset$MAR01))
```

## 第12講/第13講(01/18)

* [講義資料](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/12th13th.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_12th13th.html)


```
## Reordering exdataset$ARE
exdataset$ARE <- factor(exdataset$ARE, levels=c("Kanto", "Hokkaido", "Tohoku", "Chubu", "Kinki", "Chugoku", "Shikoku", "Kyushu"))

## Reordering exdataset$MAR
exdataset$MAR <- factor(exdataset$MAR, levels=c("NotMarried", "Married"))

## Reordering exdataset$CHI
exdataset$CHI <- factor(exdataset$CHI, levels=c("NoChild", "Child"))
```


## 第14講/第15講(01/25)
* [講義資料](https://github.com/akrgt/2021statistics/raw/gh-pages/slide/14th15th.pdf)
* [講義資料（html）](https://akrgt.github.io/2021statistics/page/html_14th15th.html)
* 演習問題は別途配布します．



## リアクションペーパー：毎回必ずお答えください．

[https://forms.gle/oxrNRW1HW9mwGeoHA](https://forms.gle/oxrNRW1HW9mwGeoHA)



## 担当

- 湘南医療大学　保健医療学部　非常勤講師
- 明治大学　情報コミュニケーション学部　専任講師
  - 後藤　晶
  - akrgt0713[at]gmail.com
  - [at]をあっとまーくに変えてください．

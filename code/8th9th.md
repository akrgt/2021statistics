## サンプリング

```{r}
die <- 1:6
dice <- sample(x = die, size = 2 , replace = TRUE)
sum(dice)
```


## サンプリング
```{r}
roll <- function(){
　　die <- 1:6
　　dice <- sample(x = die, size = 2 , replace = TRUE)
　　sum(dice)
}
roll()
```
* die：サイコロの目の数を定義している．
* size：サイコロの個数を意味している

## サンプリング
```{r}
rolls <- replicate(10000, roll())
```
* rollのあとに()を付けるのを忘れてはいけない．
  - 関数には必ず()が必要．

## サンプリング
```{r, echo=TRUE, fig.height=3.8, fig.width=6}
library(ggplot2)
qplot(rolls, binwidth = 1)
```
* “binwidth = 1”は幅の指定のために必要

## 地域の並べ替え
```{r echo=TRUE}
head(factor(exdataset$ARE))
```


## 地域の並べ替え

```{r echo=TRUE}
## Reordering exdataset$ARE
exdataset$ARE <- factor(exdataset$ARE, 
                 levels=c("Kanto", "Hokkaido", 
                 "Tohoku", "Chubu", "Kinki", 
                  "Chugoku", "Shikoku", "Kyushu"))
head(factor(exdataset$ARE))
```

## 結婚と子どもの有無についても並べ替えよう．

```{r echo=TRUE}
head(factor(exdataset$MAR))
```

* NotMarried(未婚)を最初として，次にMarried(既婚)として並べ替えよう．

```{r echo=TRUE}
head(factor(exdataset$CHI))
```
* NoChild(子どもなし)を最初として，次にChild(子どもあり)として並べ替えよう．


* 並べ替えを手抜きするために"Addin"を使えば，クリックだけでいろいろできる．



## データのフィルタリング

```{r include=FALSE}
exdataset <- read_csv("../data/exdataset.csv")
library(ggplot2)

## Reordering exdataset$ARE
exdataset$ARE <- factor(exdataset$ARE, levels=c("Kanto", "Hokkaido", "Tohoku", "Chubu", "Kinki", "Chugoku", "Shikoku", "Kyushu"))

## Reordering exdataset$MAR
exdataset$MAR <- factor(exdataset$MAR, levels=c("NotMarried", "Married"))

## Reordering exdataset$CHI
exdataset$CHI <- factor(exdataset$CHI, levels=c("NoChild", "Child"))
```


## 男性だけのデータの平均値
```{r echo=TRUE}
mean(exdataset$SUB_HAP)
```

## 男性だけのデータの平均値

```{r echo=TRUE, message=FALSE}
# install.packages('dplyr', dependencies = T)
library(dplyr)
```
* dplyrという関数を用いる．


## filter()：指定した条件に合うデータを抽出
* 男性のみを取り出す
```{r}
exdataset %>%
  filter(F_SEX == "male")
```

* 関東地方以外の人を取り出す
```{r}
exdataset %>%
  filter(ARE != "Kanto")
```


## select()：列を抽出
* 主観的幸福度(SUB_HAP)と睡眠満足度(SUB_SLP)のみを抽出
```{r}
exdataset %>%
  select(SUB_HAP, SUB_SLP)
```

* 主観的幸福度(SUB_HAP)と睡眠満足度(SUB_SLP)以外を抽出
```{r}
exdataset %>%
  select(-SUB_HAP, -SUB_SLP)
```


## mutate()：列を追加
* 主観的幸福度(SUB_HAP)と生活満足度(SUB_SAT)を足してHAPSATという変数を作成する
```{r}
exdataset %>%
  mutate(HAPSAT = SUB_HAP + SUB_SAT)
```

* 主観的幸福度(SUB_HAP)と生活満足度(SUB_SAT)を引いてdifHAPSATという変数を作成する
```{r}
exdataset %>%
  mutate(difHAPSAT = SUB_HAP - SUB_SAT)
```


## arrange()：並び替え
* 地域順で並び替え
```{r}
exdataset %>%
  arrange(ARE)

```

## summarise()：集約する
* 主観的幸福度の平均値・分散・標準偏差を取り出す．
```{r}
exdataset %>%
  summarise(heikin=mean(SUB_HAP), 
            bunsan=var(SUB_HAP), 
            hyohen=sd(SUB_HAP))
```


## group_by：グループごとに算出する
* 地域ごとにまとめて，平均値を算出する．
  * 他の関数と組み合わせて強みがわかる
```{r}
exdataset %>%
  group_by(ARE)%>%
  summarise(heikin=mean(SUB_HAP), 
            bunsan=var(SUB_HAP), 
            hyohen=sd(SUB_HAP))
```


## 組み合わせの数をカウントする．

* 使用するパッケージ
```{r, echo=T}
# install.packages("dplyr") # 最初のみ
library(dplyr)

# install.packages("tidyr") # 最初のみ
library(tidyr)
```

## dplyrのgroup_by関数を使う方法
```{r, echo=T}
tablea<-exdataset %>% 
  group_by(ARE, CHI) %>% 
  tally() %>% 
  spread(ARE, n) 
tablea
```



## dplyrのcount関数を使う方法
```{r, echo=T}
tableb<-exdataset %>%
  count(ARE, CHI) %>%
  spread(ARE, n)
tableb
```



## 参考：ggplot2で可視化する方法

```{r}
library(ggplot2)
exdataset%>%
  ggplot(aes(x=ARE, fill=CHI),stat="count")+geom_bar()
```



## xtabs 関数を使う方法


```{r, echo=T}
tablec<-xtabs(~ CHI, exdataset)
tablec
```

```{r, echo=T}
tabled<- xtabs(~ ARE, exdataset)
tabled
```

## table 関数を使う方法

```{r, echo=T}
tablee<-xtabs(~ ARE + CHI, exdataset)
tablee
```
---

* 行のパーセント表示
```{r, echo=T}
tableg<-prop.table(tablee, 1)
tableg
```

---

* 列のパーセント表示
```{r, echo=T}
tableh<-prop.table(tablee, 2)
tableh
```


## もっと細かいクロス集計表を出してみよう
```{r echo=T}
xtabs(~ CHI + ARE +F_SEX, exdataset)
```


## 連関係数を出力しよう


```{r echo=TRUE}
#install.packages('vcd', dependencies = T)：初回のみ
library(vcd)
```

---

```{r echo=TRUE}
assocstats(tablee)
```


## 適合度検定



```{r echo=T}
psy <- c(40, 21, 40, 90, 50, 70)
```

```{r echo=T}
the_psy <- c(1/6, 1/6, 1/6, 1/6, 1/6, 1/6)
```

## 適合度検定の実施

```{r echo=T}
chisq.test(psy, p = the_psy)
```



## 適合度検定の実施その2

```{r}
roll <- function(){
　　die <- 1:6
　　a_die <- sample(x = die, size = 1 , replace = TRUE)
}
```
* size=1に注意

## 適合度検定の実施その2

```{r}
rolls <- replicate(10000, roll())
```
* サイコロを10000回振ります．

## 適合度検定の実施その2
```{r}
rolls_table<-table(rolls)
rolls_table
```


## 適合度検定の実施その2
```{r}
chisq.test(rolls_table, p = the_psy)
```


## 独立性検定

```{r echo=T}
ryoko_seibetsu <- matrix(c(70, 50, 60, 40, 30, 20),
                         nrow = 2, byrow = T)
```

## 独立性検定
```{r echo=T}
chisq.test(ryoko_seibetsu)
```


```{r echo=T}
chitest.tablee<-chisq.test(tablee)
chitest.tablee
```


```{r echo=T}
chitest.tablee$stdres
```



* もしくは，以下の計算でp値を算出しても良い．

```{r}
pnorm(abs(chitest.tablee$stdres), lower.tail = FALSE) * 2
```



```{r dataを読み込む, message=FALSE, warning=FALSE, include=FALSE}
library(readr)
exdataset <- read_csv("../data/exdataset.csv")
```



```{r fig.height=4, fig.width=7, message=FALSE, warning=FALSE}
library(ggplot2)

ggplot(exdataset) +
 aes(x = SUB_HAP, y = SUB_SAT) + geom_point(size = 1L, colour = "#0c4c8a") +
 geom_smooth(span = 1L) + theme_minimal()
```


```{r}
hapsat_model<-lm(SUB_HAP~SUB_SAT, data = exdataset)
summary(hapsat_model)
```

## 結果をきれいに表記しよう．

* パッケージpanderの中にある関数panderを使うと，結果がわかりやすく表示されます．
```
library(pander)
pander(hapsat_model)
```

* 私のはCSSをいじっているので少し色が変わっています．


* 他にもパッケージhuxtableの中にhuxregという関数があります．
```
library(huxtable)
huxreg(hapsat_model)
```


* パッケージstargazerの中にあるstargazerという関数を使うとxls形式で出力できます．

```
library(stargazer)
stargazer(hapsat_model, type = "html", align=TRUE, 
          title = "分析結果", out = "hapsatmodel.xls")
```

# 使用 gensim 訓練中文詞向量

## [原作者網站](http://zake7749.github.io/2016/08/28/word2vec-with-gensim/)

## 套件需求

* jieba
```
pip3 install jieba
```
* gensim
```
pip3 install -U gensim
```
* [OpenCC](https://github.com/BYVoid/OpenCC) (可更換為任何繁簡轉換套件)

## 訓練流程

1.取得[簡體中文維基數據](https://dumps.wikimedia.org/zhwiki/latest/)，本次實驗是採用最新的資料。

*目前 8 月 20 號的備份已經被汰換掉囉，請前往[繁體中文維基數據](https://dumps.wikimedia.org/twwiki/latest/)可跳過2.3步驟。( 請挑選以`pages-articles.xml.bz2`為結尾的檔案 )*

2.將下載後的維基數據置於與專案同個目錄，再使用`wiki_to_txt.py`從 xml 中提取出維基文章

```
python3 wiki_to_txt.py zhwiki-20160820-pages-articles.xml.bz2
```
*若您採用的不是 8 月 20 號的備份，請更換 `zhwiki-20160820-pages-articles.xml.bz2` 為您採用的備份的檔名。*

3.使用 OpenCC 將維基文章統一轉換為繁體中文
```
opencc -i wiki_texts.txt -o wiki_zh_tw.txt -c s2tw.json
```
4.使用`jieba` 對文本斷詞，並去除停用詞
```
python3 segment.py
```
5.使用`gensim` 的 word2vec 模型進行訓練
```
python3 train.py
```
6.測試我們訓練出的模型
```
python3 demo.py
```
資料來源2，以台灣的PTT為例，資料下載自
[PTT:](https://tw.pyladies.com/~marsw/dmworkshop.slides.html#/2)
下載 PTT_Gossiping_201611.csv 後以筆記本開啟，轉存為 wiki_zh_tw.txt
即可開始練習
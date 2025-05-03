# char-similar-z
 汉字字形/拼音/语义相似度(单字, 可用于数据增强, CSC错别字检测识别任务(构建混淆集))

- 备注: 完全基于[https://github.com/yongzhuo/char-similar](https://github.com/yongzhuo/char-similar) 项目, 仅修改了部分代码(删除了多线程和多进程，只保留了基础的功能), 使其支持python3.10+版本, 其他功能和使用方式保持一致.



# 一、安装
```bash
pip install char_similar_z
```

# 二、使用方式

## 2.1 详细使用
```python3
import time
from char_similar_z import CharSimilarity

# "shape"-字形; "all"-汇总字形/词义/拼音; "w2v"-词义优先+字形; "pinyin"-拼音优先+字形
# kind = "shape"  # "all"  # "w2v"  # "pinyin"  # "shape"
# 对于字符而言， 使用 w2v 和all 无意义， 推荐使用 pinyin
sim = CharSimilarity()
char1 = "我"
char2 = "他"
for kind in ["shape", "pinyin", "w2v", "all"]:
    t0 = time.time()
    score = sim.std_cal_sim(char1, char2, kind=kind)
    t1 = time.time()
    print(f"相似度({char1}, {char2})[{kind}]: {score}, 用时: {round(t1 - t0, 4)}s")


```





# 三、技术原理
```
char-similar最初的使用场景是计算两个汉字的字形相似度(构建csc混淆集), 后加入拼音相似度,字义相似度,字频相似度...详见源码.

# 四角码(code=4, 共5位), 统计四个数字中的相同数/4
# 偏旁部首, 相同为1
# 词频log10, 统计大规模语料macropodus中词频log10的 1-(差的绝对值/两数中的最大值)
# 笔画数, 1-(差的绝对值/两数中的最大值)
# 拆字, 集合的与 / 集合的并
# 构造结构, 相同为1
# 笔顺(实际为最小的集合), 集合的与 / 集合的并
# 拼音(code=4, 共4位), 统计四个数字中的相同数(拼音/声母/韵母/声调)/4
# 词向量, char-word2vec, cosine
```


# 四、参考(部分字典来源以下项目)
 - [https://github.com/contr4l/SimilarCharacter](https://github.com/contr4l/SimilarCharacter)
 - [https://github.com/houbb/nlp-hanzi-similar](https://github.com/houbb/nlp-hanzi-similar)
 - [https://github.com/mozillazg/python-pinyin](https://github.com/mozillazg/python-pinyin)
 - [https://github.com/CNMan/UnicodeCJK-WuBi](https://github.com/CNMan/UnicodeCJK-WuBi)
 - [https://github.com/yongzhuo/Macropodus](https://github.com/yongzhuo/Macropodus)
 - [https://github.com/kfcd/chaizi](https://github.com/kfcd/chaizi)
 


# Reference
For citing this work, you can refer to the present GitHub project. For example, with BibTeX:
```
@misc{Macropodus,
    howpublished = {https://github.com/yongzhuo/char-similar},
    title = {char-similar},
    author = {Yongzhuo Mo},
    publisher = {GitHub},
    year = {2024}
}
```


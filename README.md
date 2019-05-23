# BERT-BiLSMT-CRF-NER

fork from https://github.com/macanv/BERT-BiLSTM-CRF-NER



### 原程序弊端(Motivation)

原程序作为服务时可提供API被其他程序调用。但是在做NER时，返回的只是标签序列，我们并不知道NER程序对于输入文本是如何分词（tokenlize）的。

原程序例：

input:

```json
{"id": 123,"texts": ["1992/6，小明在Stanford University攻读CS专业"]}
```

output:

```json
{
    "id": 123,
    "result": [
        [
            "B-TIME",
            "I-TIME",
            "I-TIME",
            "O",
            "B-PEOPLE",
            "I-PEOPLE",
            "O",
            "B-ORGANIZATION",
            "I-ORGANIZATION",
            "I-ORGANIZATION",
            "I-ORGANIZATION",
            "B-VERB",
            "I-VERB",
            "B-POSITION",
            "I-POSITION",
            "I-POSITION"
        ]

    ],
    "status": 200
}
```



### 修改(Modify)

参考原作者对分类型任务的输出处理，增加了对分词结果(tokens)的输出，方便客户端使用

修改后输出：

```json
{
    "id": 123,
    "result": [
        {
            "tags": [
                [
                    "B-TIME",
                    "I-TIME",
                    "I-TIME",
                    "O",
                    "B-PEOPLE",
                    "I-PEOPLE",
                    "O",
                    "B-ORGANIZATION",
                    "I-ORGANIZATION",
                    "I-ORGANIZATION",
                    "I-ORGANIZATION",
                    "B-VERB",
                    "I-VERB",
                    "B-POSITION",
                    "I-POSITION",
                    "I-POSITION"
                ]
            ],
            "tokens": [
                [
                    "1992",
                    "/",
                    "6",
                    "，",
                    "小",
                    "明",
                    "在",
                    "st",
                    "##an",
                    "##ford",
                    "university",
                    "攻",
                    "读",
                    "cs",
                    "专",
                    "业"
                ]
            ]
        }
    ],
    "status": 200
}
```


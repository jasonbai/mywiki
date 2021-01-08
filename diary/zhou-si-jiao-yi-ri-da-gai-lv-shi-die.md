---
description: '2020-09-24'
---

# 周四交易日大概率是跌？



> 今天周四，大盘暴跌，都说周四总是要跌的，近期尝试学了一些量化交易的东西，写几段代码看看是不是真的。

* 每逢周四必跌是真的吗？
* 数据样本：2010-01-01 到 2020-09-23 （上证指数）
* 工作平台：宽聚 https://www.joinquant.com
* 代码语言：python

```text
import pandas as pdimport  time,datetimebegin = datetime.date(2010,1,1)end = datetime.date(2020,9,23)
df = get_price('000001.XSHG', start_date = begin, end_date= end, frequency='daily', fields=None, skip_paused=False, fq='pre', panel=True)
df['涨跌']= df['close']-df['open']
#判断星期几def  get_week_day(date):    idx = pd.date_range(start=date, freq='D', periods=1)    return  idx.day_name()
```

```text
# 判断市场周四跌的次数
Thursday_lose = 0Thursday = 0for i in range(0,len(df)):    if get_week_day(df.index.values[i]) == 'Thursday':        Thursday +=1        if df.iloc[i,6]<0 :            Thursday_lose  += 1
print("近10年来，周四交易日上证指数为亏的比例：" + str(Thursday_lose/Thursday))
```

```text
近10年来，周四交易日上证指数为亏的比例： 0.526615969581749
```

```text
# 判断市场周一跌的次数Monday_lose = 0Monday = 0for i in range(0,len(df)):    if get_week_day(df.index.values[i]) == 'Monday':        Monday +=1        if df.iloc[i,6]<0 :            Monday_lose  += 1
print("近10年来，周一交易日上证指数为亏的比例：" + str(Monday_lose/Monday))
```

```text
近10年来，周一交易日上证指数为亏的比例： 0.421259842519685
```

```text
# 判断市场周二跌的次数Tuesday_lose = 0Tuesday = 0for i in range(0,len(df)):    if get_week_day(df.index.values[i]) == 'Tuesday':        Tuesday +=1        if df.iloc[i,6]<0 :            Tuesday_lose  += 1
print("近10年来，周二交易日上证指数为亏的比例：" + str(Tuesday_lose/Tuesday))
```

```text
近10年来，周二交易日上证指数为亏的比例： 0.4049429657794677
```

```text
# 判断市场周三跌的次数Wednesday_lose = 0Wednesday = 0for i in range(0,len(df)):    if get_week_day(df.index.values[i]) == 'Wednesday':        Wednesday +=1        if df.iloc[i,6]<0 :            Wednesday_lose  += 1
print("近10年来，周三交易日上证指数为亏的比例：" + str(Wednesday_lose/Wednesday))
```

```text
近10年来，周三交易日上证指数为亏的比例： 0.4641509433962264
```

```text
# 判断市场周五跌的次数Friday_lose = 0Friday = 0for i in range(0,len(df)):    if get_week_day(df.index.values[i]) == 'Friday':        Friday +=1        if df.iloc[i,6]<0 :            Friday_lose  += 1
print("近10年来，周五交易日上证指数为亏的比例：" + str(Friday_lose/Friday))
```

```text
近10年来，周五交易日上证指数为亏的比例： 0.4007707129094412
```

```text
print('近10年来，周一交易日，上证指数为亏的比例: {:.2f}%'.format(Monday_lose/Monday*100))print('近10年来，周二交易日，上证指数为亏的比例: {:.2f}%'.format(Tuesday_lose/Tuesday*100))print('近10年来，周三交易日，上证指数为亏的比例: {:.2f}%'.format(Wednesday_lose/Wednesday*100))print('近10年来，周四交易日，上证指数为亏的比例: {:.2f}%'.format(Thursday_lose/Thursday*100))print('近10年来，周五交易日，上证指数为亏的比例: {:.2f}%'.format(Friday_lose/Friday*100))
```

```text
近10年来，周一交易日，上证指数为亏的比例: 42.13%近10年来，周二交易日，上证指数为亏的比例: 40.49%近10年来，周三交易日，上证指数为亏的比例: 46.42%近10年来，周四交易日，上证指数为亏的比例: 52.66%近10年来，周五交易日，上证指数为亏的比例: 40.08%
```

从数据来看，周四确实是跌幅最大的一天，老股民的感觉还是准的，周四果然不吉利。


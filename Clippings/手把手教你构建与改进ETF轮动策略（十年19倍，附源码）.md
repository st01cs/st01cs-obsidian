---
title: "手把手教你构建与改进ETF轮动策略（十年19倍，附源码）"
source: "https://mp.weixin.qq.com/s/tzKIAiKiA_Lo7VCgu-fcZg"
author:
  - "[[量化君]]"
published:
created: 2025-10-23
description: "从十年3倍到19倍~"
tags:
  - "clippings"
---
原创 量化君 *2025年08月28日 23:26*

![图片](https://mmbiz.qpic.cn/mmbiz_png/icBZQJaAUTJiac8IbeKmzNQ1RicdXbOzLzy9jfu3JK3sCf2tQ5Ku5yzT1Xqibt21ahx3ibmF3lrBOSFZEVOBibl4dMxg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=0)

  

**一、说在前面的话**  

众所周知，股票、债券、商品等投资市场存在着各种各样明显的轮动效应，最常见的有3种。

  

**第一种是资产轮动** ，也就是大类资产间的轮动，在不同的市场/宏观环境下，配置不同的类别的资产，可以获得更显著的投资收益，比如资产配置中最经典的美林时钟，按照经济增长与通胀将经济周期划分为4个阶段，每个阶段都有最适合的投资品种：衰退期买债券，复苏期炒股票，过热期投大宗商品，滞涨期持现金。对了，常见的股债轮动策略也是属于这个类别。

  

**第二种是行业轮动** ，也可以称之为板块轮动，说的就是各行业/板块在相同时期会表现出差异性，各自支棱的时间不同步，因此可以通过不同时期配置不同行业/板块，从而博取高于市场基准的投资收益。

  

**第三种就是风格轮动** ，跟行业轮动和板块轮动原理类似，只不是走强的不是轮动/板块，而是某类投资风格，比方我们常见的大小盘轮动、成长价值轮动就属于这种，晨星的投资风格箱就是按此划分的。

  

![图片](https://mmbiz.qpic.cn/mmbiz_png/icBZQJaAUTJhqibo0e8NQu5z0yeCeTA3CGSt6NXCnLlSsyjPFb9icGOFN2IBnuOEicCUvnbOqWpt9SFp6cYkicibic2Dg/640?wx_fmt=png&from=appmsg&watermark=1&tp=webp&wxfrom=5&wx_lazy=1#imgIndex=1)

  

第一种是各类资产之间的轮动，后两种更多的是某类资产(如股票)内的轮动，不过抽象出来，它们都是具有价格走势的证券/品种，只要它们有价格走势，就可以非常容易地构建出轮动策略，核心因素有两个。

  

**第一个是候选池，也就是在哪个“池子”里面进行轮动** ，是在股票、债券、商品、现金里面进行轮动呢，还是在大小盘风格里面进行轮动，这需要咱一开始就进行框定。

  

**第二个就是强弱排序，也就是采用什么方法规则对池子里面的品种进行排序** ，每期买入最强的那个或前几个品种，就跟和联胜社团每两年要选举一次那样，是靠叔父辈发话，还是靠才智拳头，拿到龙头棍，当上坐馆。

  

这些问题，咱都会在本篇文章内解决，就不扯闲篇儿了，赶紧一起出发，let's go~哦，对了，记得戴上头盔~~

  

**二、轮动策略构建**  

**1.候选池确定**  

**第一步咱先要确定轮动策略的 候选 池，后面的所有步骤都是围绕着这个 候选 池展开的** ，为了讲解方便，最开始先构建A股里面常见的风格轮动，后续要换成别的轮动形式，只要更换里面证券代码列表就可以了。

  

在大小盘风格轮动中，常用沪深300指数代表大盘风格，中证500指数代表小盘风格，为了体现可交易性，这里用的是ETF（ Exchange Traded Fund， 交易型开放式指数基金），沪深300ETF代码是510300，中证500ETF代码是510500。

  

其实现在代表小盘风格，感觉中证1000指数/中证2000指数更为合适，但是最早上市的中证1000ETF从2016年底才开始，数据不够10年，不方便长期回测，于是还是用中证500，这些细节不用太在意，理解整个轮动策略的框架和回测思路就可以了。

  

在价值成长风格轮动中，个人喜欢用红利ETF（代码：510880）代表价值风格，创业板ETF（代码：159915）代表成长风格，这里没有太死板的规定，根据个人的理解和喜好来决定就可以了。

  

**至此，咱有了风格轮动策略的 候选 池： 沪深300ETF（ 510300 ）， 中证500ETF（ 510500 ）， 红利ETF（510880）， 创业板ETF（159915）。** 再啰唆一句， 候选 池的确定没有什么条条框框，全凭自己的对交易的理解和喜好，例如你就放余额宝和银华日利都可以，只要能取到序列数据。

  

**2.数据获取**  

在获取数据之前，咱要先把编程环境搭上，本次策略开发用的编程语言是Python 3.13，代码编辑和执行软件是Jupyter Notebook，你使用别的Python版本和集成开发环境IDE都是可以的，只要安装的库大体对应就行，磨刀不误砍柴工，咱先把接下来要用的库导入进来。

  

`   `

```bash
# 510300：沪深300ETF，代表大盘# 510500：中证500ETF，代表小盘# 510880：红利ETF，代表价值# 159915：创业板ETF，代表成长code_list = ['510300', '510500', '510880', '159915']start_date = '20150101'end_date = '20250828'
df_list = []for code in code_list:    print(f'正在获取[{code}]行情数据...')    # adjust：""-不复权、qfq-（前复权）、hfq-后复权    df = ak.fund_etf_hist_em(symbol=code, period='daily',         start_date=start_date, end_date=end_date, adjust='hfq')    df.insert(0, 'code', code)    df_list.append(df)    time.sleep(3)print('数据获取完毕！')
all_df = pd.concat(df_list, ignore_index=True)data = all_df.pivot(index='日期', columns='code', values='收盘')[code_list]data.index = pd.to_datetime(data.index)data = data.sort_index()data.head(10)
```

`   `

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

`   `

**3.数据计算**  

**轮动策略的第二个核心就是强弱排序，这里采用的是动量策略的规则，每天买入前N个交易日涨幅最大的那一个ETF** ，因此需要计算出每个ETF在每一天的前N个交易日的涨幅。  

  

为了方便后面的回测，还需要顺带计算出每个ETF的日涨幅，计算代码和运行结果如下。

  

```powershell
# 动量长度N = 10# 计算每日涨跌幅和N日涨跌幅for code in code_list:    data['日收益率_'+code] = data[code] / data[code].shift(1) - 1.0    data['涨幅_'+code] = data[code] / data[code].shift(N+1) - 1.0# 去掉缺失值data = data.dropna()data[['涨幅_'+v for v in code_list]].head(10)
```

`   ` ![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

**4.信号生成与回测**  

经过上一步的计算， **咱就知道了每一天所有ETF的区间涨幅，就可以筛选出涨幅最大的那个ETF，根据这个信号买入这个最强的ETF，作为轮动策略的持仓。**

  

知道了策略每一天的持仓，就知道策略每一天的收益率，采用连乘的方式进而计算出策略的净值曲线，有了这条净值曲线，就可以统计出回测的各项绩效指标。  

  

```powershell
# 取出每日涨幅最大的证券data['信号'] = data[['涨幅_'+v for v in code_list]].idxmax(axis=1).str.replace('涨幅_', '')# 今日的涨幅由昨日的持仓产生data['信号'] = data['信号'].shift(1)data = data.dropna()data['轮动策略日收益率'] = data.apply(lambda x: x['日收益率_'+x['信号']], axis=1) # 第一天尾盘交易，当日涨幅不纳入data.loc[data.index[0],'轮动策略日收益率'] = 0.0data['轮动策略净值'] = (1.0 + data['轮动策略日收益率']).cumprod()data[['涨幅_'+v for v in code_list]+['信号','轮动策略日收益率','轮动策略净值']].head(10)
```

`   `

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

这里需要特别说明两点，第一点是交易信号列要前移1格（对应第4行代码当中的shift），因为策略今日的涨跌幅/收益率是由昨日的持仓产生的，这里其实也暗含着一个回测设定，就是当日收盘价计算交易信号当日收盘价成交，如果前移2格就是当日收盘价计算交易信号明日收盘价成交。

  

第二点就是 回测第一个 交易日 收益率为0，这跟 第一点暗含的设定有关 ， 当日收盘价才 成交产生持仓 ，故第一个交易日 收盘前没有持仓 ，不纳入信号证券的涨跌幅，收益率为 0。

  

**5.结果统计和画图**  

经过上一步，终于回测计算出轮动策略的净值曲线了，咱先把这4个ETF和策略净值都画出来，直观对比一下。  

  

```powershell
# 显示中文设置plt.rcParams['font.sans-serif']=['SimHei']plt.rcParams['axes.unicode_minus']=False
# 获取ETF名称etf_df = ak.fund_etf_spot_em()code_to_name_dict = etf_df.set_index('代码')['名称'].to_dict()
# 绘制净值曲线图fig, ax = plt.subplots(figsize=(15, 6))ax.set_xlabel('日期')ax.set_ylabel('净值')name_list = []for code in code_list:    if code not in code_to_name_dict.keys():        continue    name = code_to_name_dict[code]    name_list.append(name)    data[name+'净值'] = data[code] / data[code].iloc[0]    ax.plot(data.index, data[name+'净值'].values, linestyle='--')ax.plot(data.index, data['轮动策略净值'].values, linestyle='-', color='#FF8124')name_list.append('轮动策略')
# 显示图例和标题ax.legend(name_list)ax.set_title('轮动策略净值曲线对比 by 公众号【量化君也】')
plt.show()
```

`   `

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

图中那条黄色实线就是轮动策略的净值曲线，它最终跑赢了这4个ETF中的任何一个，实现了通过轮动配置增强了策略收益。  

  

**光看净值曲线还不够，还需要获得收益率、夏普率等回测统计指标信息，在这里，咱可以通过量化工具库quantstats快速实现** ，导入该库后，可以通过reports.html函数生成html格式的完整回测报告，回测报告会存储在与策略代码同级的文件夹下，也可以通过reports.basic函数输出基本的回测报告信息，也还有很多类似的函数，有空可以逐一去探索。

  

```powershell
#将完整回测报告存为HTML文件title = '轮动策略回测报告_原始版 by 公众号【量化君也】'output_file = os.path.join(os.getcwd(), f'{title}_{datetime.now().strftime('%Y%m%d_%H%M%S')}.html')qs.reports.html(data['轮动策略净值'], benchmark=data['沪深300ETF净值'],                title=title, output=output_file) print(f'已将回测报告保存到文件: {output_file}')#输出基本回测报告信息qs.reports.basic(data['轮动策略净值'], benchmark=data['沪深300ETF净值'])
```

`   `

  

输出的部分结果截图：  

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

第一幅图显示的是回测当中的各种统计指标，其中关键的是，策略累计收益率(Cumulative Return)是333.09%，年化收益率(CAGR)是10.01%，比基准沪深300ETF的年化收益2.47%高出了7个百分点，策略的夏普率(Sharpe)为0.66，也高于基准的0.28，不过最大回撤(Max Drawdown)达到了47.68%，超过了基准，不是大心脏真扛不下来。

  

第二幅图是轮动策略和基准的累计收益率曲线，第三幅图是策略相对基准每个月的超额收益，这个就很直观了，就不用过多解释了。

  

**三、改进1：修改侯选池**  

初版的轮动策略咱已经完成了，虽然能跑赢基准，但是各项回测统计指标看上去还有很大的提升空间，革命尚未成功，同志仍需努力~  

  

还记得轮动策略的两个核心吗？一是 候选 池，二是强弱排序，要改进，可以先从 候选 池下手。  

  

侯选池的重要性不言而喻，因为后续所有的动作都是围绕着侯选池展开的，就跟从中国足球队 随机 挑选球员，还是从巴西 足球 队随机挑选球员去点球一样，底子好的自然胜率高。

  

比如说，咱除了A股之外，还考虑国外市场，选入代表漂亮国的纳指ETF（代码：513100），还考虑大宗商品市场，于是选入黄金ETF（代码：518880），同时剔除原来候选池当中的沪深300ETF和中证500ETF， **于是整个 候选 池就变为： 红利ETF（510880），创业板ETF（159915）， 纳指ETF（513100）， 黄金ETF（518880） 。** 于是乎，获取数据部分的代码做出对应的调整。

  

```bash
# 510880：红利ETF，代表价值# 159915：创业板ETF，代表成长# 513100：纳指ETF，代表外盘# 518880：黄金ETF，代表商品code_list = ['510880', '159915', '513100', '518880']start_date = '20150101'end_date = '20250828'
df_list = []for code in code_list:    print(f'正在获取[{code}]行情数据...')    # adjust：""-不复权、qfq-（前复权）、hfq-后复权    df = ak.fund_etf_hist_em(symbol=code, period='daily',         start_date=start_date, end_date=end_date, adjust='hfq')    df.insert(0, 'code', code)    df_list.append(df)    time.sleep(3)print('数据获取完毕！')
all_df = pd.concat(df_list, ignore_index=True)data = all_df.pivot(index='日期', columns='code', values='收盘')[code_list]data.index = pd.to_datetime(data.index)data = data.sort_index()data.head(10)
```

`   `

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

咱按照原始策略的流程重新回测一遍，注意在回测结果统计的部分要将原来的沪深300ETF修改成纳指ETF。  

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

从结果图中可以看出，修改 候选 池后的轮动策略的回测绩效取得了明显的提升， **年化收益率从原来的10.01%提升到了14.74%，夏普率也从原来的0.66提高到了0.94，最大回撤也从原来的47.68%降低到了39.65%。**

  

**四 、改进2：修改强弱排序方式**

**候选池改过了，咱接下来就是改强弱排序，还是保存动量规则不变，原来采用的是区间涨跌幅，这次改进则打算采用区间走势** ， 候选 池依旧是上一步改进策略的 候选 池： 红利ETF（510880），创业板ETF（159915），纳指ETF（513100），黄金ETF（518880）。  

  

区间走势用什么指标来衡量呢？这里借鉴RSRS指标的构建思路，用收盘价序列的斜率来表征，斜率越大，走势越猛越强。  

  

同时也引入决定系数R2的概念，它是对线性拟合效果好坏的判断指标，取值范围一般在0~1之间，数值越大，表示线性拟合的效果就越好，当直线能完美拟合所有数据点时，取值为1，更详细的说明可以见之前的文章 [《(续)复现网红阻力支撑指标RSRS，手把手教你构建大盘择时策略》](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485225&idx=1&sn=dba12368183359f98f7b0f60ea6a38a4&chksm=c21ba4a6f56c2db0684151422eb24311f06902d656ce3654bfd4954aceeb4571cdbdd26712dd&scene=21#wechat_redirect) 。

  

**于是强弱规则就修改为“斜率和决定系数的乘积”，乘积作为ETF动量强弱的趋势得分，得分数值越高，就表示动量越强，每日都选入强弱得分最高的ETF** ，数据计算部分的代码也做出相应的调整。  

  

```apache
# 计算强弱得分def calculate_score(srs, N=25):    if srs.shape[0] < N:        return np.nan    x = np.arange(1, N+1)    y = srs.values / srs.values[0]    lr = LinearRegression().fit(x.reshape(-1, 1), y)    # 斜率    slope = lr.coef_[0]    # 决定系数R2    r_squared = lr.score(x.reshape(-1, 1), y)    # 得分    score = 10000 * slope * r_squared    return score
# 斜率计算长度N = 25# 计算每日涨跌幅和得分for code in code_list:    data['日收益率_'+code] = data[code] / data[code].shift(1) - 1.0    data['得分_'+code] = data[code].rolling(N).apply(lambda x: calculate_score(x, N))# 去掉缺失值data = data.dropna()data[['得分_'+v for v in code_list]].head(10)
```

`   `

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

在趋势得分计算当中，有两点要补充说明， **一是在斜率计算时，要每次都对收盘价序列“归一化”** ，因为ETF的数值范围不一样，会导致即使相同走势，斜率也不一样，比如说，序列y1=\[1,2,3,4\]和y2=\[2,4,6,8\]分别都对x= \[1,2,3,4\]求斜率，前者的斜率值是1，后者是2，其实它们的走势都是一样的，涨幅也是一样的。

  

二是计算强弱得分求乘积时，乘以了系数10000，那个只是为了让数值“ 好看 ”一些，更像是得分的范畴，横截面比较，同时都乘以一个任意正实数，都不影响排序。  

  

之前是按照区间涨幅排序，现在是改为强弱得分排序，重新回测一遍，记得第4步信号生成与回测中的“涨幅”要改为“得分”。  

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

从结果图中看出，改进策略2在改进策略1的基础上又取得了进一步的提升， **累计收益率从十年7倍提升到了十年19倍，年化收益率从 14.74% 提升到了 21.67% ，夏普率从0.94提升到了1.33，最大回撤也从 39.65% 下降到了 30.31% 。**

  

为了更直观地对比改进结果，咱把原始策略、改进策略1和改进策略2都放在一张图里面进行展示，绩效对比一目了然。  

  

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

  

**五、总结和补充说明**  

咱戴上头盔撸起袖子终于吭哧吭哧干完了，走通了从零开始构建轮动策略的全流程，并且进行了两番改进，从十年3倍提升到了十年19倍， 虽然效果看起来很不错 ，但仍然存在 一些不足 。

  

一是为了方便回测，是按照当日收盘价计算信号并且按收盘价交易的，虽然这在实际当中可以在尾盘近似实现，但依然会存在差距。

  

二是在回测 当中 并没有 考虑 滑点和费率，这也是为了方便回测当中的计算。  

  

三是候选池的选取，这也是所有轮动策略中最大玄学部分的存在，像改进策略1一样， 候选 池选对了，年化收益直接爆升，你可以将本文当中所有候选池的选取都当做是我的主观臆断，有后视镜的存在，后面存在失效的可能。

  

**本文主要还是让大伙儿快速感受和上手轮动策略的构建过程，有好的idea了，可以快速地进行回测，验证思路，如果有惊艳的结果产生，仍需细细验证，有什么到不到的地方，望大伙儿 多多包涵。**

---

★

往期回顾

  

★

  

\------量化社群------

  

[量化达摩院](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486732&idx=1&sn=982268f4b3e9bbf2dfcebe9221759dc0&scene=21#wechat_redirect)

[量化藏经阁Max](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486489&idx=1&sn=7d7d3bed4d6f78c5e9477a7601a49864&scene=21#wechat_redirect)

[量化藏经阁2025](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486497&idx=1&sn=17a679999c0b3aeaf1c0d421f0533a8b&scene=21#wechat_redirect)

\------量化策略------

[桥水全天候策略](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485885&idx=1&sn=d687f4296450cae754bd1b801ce7bd34&chksm=c21baa32f56c2324b137bf77796ce740cf9ca6b2c66f4ea4f9c60f1658b170cae66ae45ec5e3&scene=21#wechat_redirect) [风险平价策略](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485904&idx=1&sn=7f9a873f81ea6dcbc6e5b9af2d659fa5&chksm=c21baa5ff56c23495174192875c6ea4a6cdfa52d9db3646fa52765acc68bdfdd7334859b1377&scene=21#wechat_redirect)

[聪明钱](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483685&idx=1&sn=e1c02c587859ffce1e0497fe6c7b2651&scene=21#wechat_redirect) [TrendModelSys](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484039&idx=1&sn=defcd9c0c03653ed1078ba98392af315&scene=21#wechat_redirect) [张坤策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483753&idx=1&sn=ecbe89280d78f897b394a97e06ffd6b5&scene=21#wechat_redirect)

[RSRS](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483898&idx=1&sn=d792431094001b4e64360a901b92e6bf&scene=21#wechat_redirect) [北向资金](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483921&idx=1&sn=242f6a721077eaf46b7340c4ddedb76a&scene=21#wechat_redirect) [F-Score](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483724&idx=1&sn=16645331a226874c8110ecfee3875e96&scene=21#wechat_redirect) [鱼身策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484311&idx=1&sn=8a064c83e9412d0cc5a05698f4c7aa54&scene=21#wechat_redirect)

[TrendPattern](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484545&idx=1&sn=20905b287eee64d65843ba4687ad8621&scene=21#wechat_redirect) [波动率收敛](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483852&idx=1&sn=00e3211e3ad821606e6d10b9bdc09b5a&scene=21#wechat_redirect) [RSJ策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484191&idx=1&sn=191cbea3fc1bcdfb0f90c2956e49c65c&scene=21#wechat_redirect)

[期货Alpha](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484095&idx=1&sn=56d3df957c23f8043667b9fa190d1a36&scene=21#wechat_redirect) [跨品种套利](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484021&idx=1&sn=de75d6fb7b8e30c4e6a6b465ed608791&scene=21#wechat_redirect) [GARP策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484628&idx=1&sn=91adbe6e039e86324b2136f733fb4e72&scene=21#wechat_redirect)

[MACD形态](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483870&idx=1&sn=8936877f7f597a2bbb9ef8e2ec9887cb&scene=21#wechat_redirect) [导数策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484119&idx=1&sn=40636937af309698dd56a24a129dad8e&scene=21#wechat_redirect) [Trendflex](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484458&idx=1&sn=c8f01ddeadd954f432b91bcfe00afc3b&scene=21#wechat_redirect)

[绩优小市值](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484219&idx=1&sn=b4b6b583d379ec5920807d580559578a&scene=21#wechat_redirect) [漂亮50](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483810&idx=1&sn=cbf7c998e8b95f029bd98d16b75a89ce&scene=21#wechat_redirect) [操盘手](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484010&idx=1&sn=8f425ffec08b044aff03cf8a1f51b16b&scene=21#wechat_redirect) [Rumi](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484064&idx=1&sn=cfd99a47728f889692845ccb7b0a099d&scene=21#wechat_redirect)

[AI择时](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484565&idx=1&sn=9fedbb0b8904fac5e4cb6df582e94bf8&scene=21#wechat_redirect) [K线面积法](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484161&idx=1&sn=85b980eb19f4d016b7f1a42ffa9bf7a5&scene=21#wechat_redirect) [零代码策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484518&idx=1&sn=24270a92ae7e4aada59981a479adf38e&scene=21#wechat_redirect)

[贴水策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484405&idx=1&sn=664567f274c737278867402e0b2277c2&scene=21#wechat_redirect) [概率密度策略](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484675&idx=1&sn=e8a5e701e58ddb2e34db793f0ec59d9c&chksm=c21ba68cf56c2f9ab4d37d956e70250dfd59af25b636681f8fae8d9557e4c639e45c1633429d&scene=21#wechat_redirect) [一致预期](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484960&idx=1&sn=bacb21875c2a4b377a7d35c47d03b21b&chksm=c21ba5aff56c2cb97a55bab6a7630d20e5cf19fb9f6743d9e8c49f186f19d6a5e3ff666c43d7&scene=21#wechat_redirect)

[RSRS复现1](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485087&idx=1&sn=f42bcb657ce82654a537194992787157&chksm=c21ba510f56c2c06459d13f193613df9d633679b2fc5089054de9953d652f94b46a836690790&scene=21#wechat_redirect) [RSRS复现2](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485225&idx=1&sn=dba12368183359f98f7b0f60ea6a38a4&chksm=c21ba4a6f56c2db0684151422eb24311f06902d656ce3654bfd4954aceeb4571cdbdd26712dd&scene=21#wechat_redirect) [ICU均线](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485797&idx=1&sn=cb4c3026e855879e1fa57e4f7d1e8ee3&chksm=c21baaeaf56c23fcb81d4a01669c3c743ba1dc101053a8b0f0a0339effac391938fce0a4fea2&scene=21#wechat_redirect)

[野路子策略](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485305&idx=1&sn=eb63adecb80b44b8ee57d050495da51c&chksm=c21ba4f6f56c2de037a52ab7b5c74ae31ace34863ed6d9bad20486e583e09d2643e2150d7a3d&scene=21#wechat_redirect) [ETF轮动](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485362&idx=1&sn=28d5dc92d07758cdc922cf81e5cc5e26&chksm=c21ba43df56c2d2b2a2185c28297745c1108163ab6ae2274676f3605eed9bf10f80ad681db31&scene=21#wechat_redirect) [ETF轮动2](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485425&idx=1&sn=d25d93f195a38d64976f6cd0f78bd21d&chksm=c21ba47ef56c2d68436195945c4d1a85887736a36366cf207f19aa9f5cea36ceb936f107a491&scene=21#wechat_redirect)

[菜场大妈&马科维茨](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485558&idx=1&sn=a376f48a64e624ca543f4ad6d947f8f2&chksm=c21babf9f56c22effd22cff1aefd7c02835f96a840b08d65772af4d584320066e89571dbf5b7&scene=21#wechat_redirect) [多赚200%](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485503&idx=1&sn=436532c5379f99d18307c2841b150020&chksm=c21babb0f56c22a6eb876387adf688580acd97e2e4a49b1f2352833f45e22fcbde11509293ad&scene=21#wechat_redirect)

[美债&A股择时](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485683&idx=1&sn=470100d1c72e65d5f9ae4116e480617c&chksm=c21bab7cf56c226a9b8d699c6504d982240a1b65da0b832df2e6723cd266c31d302a3eb5b6a8&scene=21#wechat_redirect) [价比斜率套利](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485960&idx=1&sn=3ac032c71b7aafeb15d9bbb0b84f9faf&chksm=c21ba987f56c20914d85503f959c7b0912b1189b30af329e408375c6b7ed203c706a55e30d54&scene=21#wechat_redirect)

[黄金价格预测](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486032&idx=1&sn=7b0a0f10b252eabec76bfef256db9d8e&chksm=c21ba9dff56c20c92e3a08ee170b20dc411112fa12a8f89f55ae70450000e25614174a7a22bf&scene=21#wechat_redirect) [量化兵器库](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483659&idx=1&sn=4c44a69d92bf5fdcb57ae64f3f7bab01&chksm=c21ba284f56c2b92aadecee7a9b50d507198c87b64c7355d23c178756b1ef4348105d58a2ac8&scene=21#wechat_redirect)

[十年零回撤](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485946&idx=1&sn=0247059aebc4e851e330dcfef8a71e06&scene=21#wechat_redirect) [红利策略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486120&idx=1&sn=b3810b54ef12d899cd8cacdf3f7ea594&scene=21#wechat_redirect) [数字信号](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486368&idx=1&sn=9a8e7b22717192a59072ef40c5b1ea43&scene=21#wechat_redirect)

\------心得杂谈------

[打开黑箱](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484482&idx=1&sn=7b98097f0a0a48728aeec452a834f1fc&scene=21#wechat_redirect) [量化手册](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486076&idx=1&sn=7265e59cd5b9a9716a83b1a4cfb416b4&scene=21#wechat_redirect) [量化攻略](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486384&idx=1&sn=a1d00fcf058755df0f2b51cda5a2ab5a&scene=21#wechat_redirect)

[个人量化](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484469&idx=1&sn=ecfdb2b3f3e723fd417c0bddbd957b6b&scene=21#wechat_redirect) [量化误解](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485473&idx=1&sn=4c71320bde8a62db39ee807dc4a206a8&chksm=c21babaef56c22b8846e2a4b1c499cd1ffae011276bd06c8cad172453b9d4d905578da0c71cf&scene=21#wechat_redirect) [高收入背后](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484426&idx=1&sn=e0d282978280a65b4d3270c050fe71bf&scene=21#wechat_redirect)

[西蒙斯](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483840&idx=1&sn=8cce9b5875f11d57945a1666f0e03591&scene=21#wechat_redirect) [雪球爆仓](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485815&idx=1&sn=6378f7c65c16da331af9598b08d53679&scene=21#wechat_redirect) [量化交易邪术](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486330&idx=1&sn=10e5309bc821819950e43bf7df0cac21&scene=21#wechat_redirect)

[量化网站1](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485841&idx=1&sn=e94800a827ce4f38c833dcd144ea1806&scene=21#wechat_redirect) [量化网站2](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485869&idx=1&sn=951f15090c856e7fcda3b660dccc6b8f&scene=21#wechat_redirect) [量化狠人](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485924&idx=1&sn=9447f05fbba78524455878c999adabd1&scene=21#wechat_redirect)

[年化577倍](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484340&idx=1&sn=b415703a642e2b3c1a04481af017108f&scene=21#wechat_redirect) [抄底&摸顶](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484287&idx=1&sn=5de0c792a1d7a56bf8867656d919c07e&scene=21#wechat_redirect) [策略开发](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483999&idx=1&sn=1c77888217e83b4dab4961bc2b3b8ce5&scene=21#wechat_redirect)

[未来函数](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484081&idx=1&sn=6076ced2c2418de2d8e5d77f2162ea07&scene=21#wechat_redirect) [回测&过拟合](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484577&idx=1&sn=6492bc8164649e3d85d015410c9db8a6&scene=21#wechat_redirect) [回测&实盘](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484586&idx=1&sn=545202b3c6a10f87e5f03be0f00a2cb2&scene=21#wechat_redirect)

[Alpha&风险因子](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484663&idx=1&sn=b92ae7684ce15f839cdcdbe7ae8c0a37&scene=21#wechat_redirect) [MACD参数](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484259&idx=1&sn=fdcb626ce9c07fca5c9362978d81a2a3&scene=21#wechat_redirect)

[资金流](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484049&idx=1&sn=78b94c8055e6822e949180d942b00058&scene=21#wechat_redirect) [吃贴水](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484388&idx=1&sn=f165f6ca0ab5c0e36fc320e4dbf0e8e0&scene=21#wechat_redirect) [回测提速](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483736&idx=1&sn=334f2395a881328014c2f2bc1568e89b&scene=21#wechat_redirect) [量价背离](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247483796&idx=1&sn=0f783208f9dd1994a21964b715bdf63e&scene=21#wechat_redirect)

[自学路径](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484712&idx=1&sn=9fdf003c783b4bc053b90736ebbb8435&chksm=c21ba6a7f56c2fb1e87cf876cba0c2620244840c339666072447a0c14516dbeb686ca2e65702&scene=21#wechat_redirect) [文章合辑](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485751&idx=1&sn=c97da5635ce842634d1c2f68397f21c1&scene=21#wechat_redirect) [151个策略](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484775&idx=1&sn=90a7e0d3786f9dd2d97a7ba95ec69318&chksm=c21ba6e8f56c2ffe64eb9fe0d2f30ba8460d53997401f00b79a91e5981a9ba2ab21a000e4d2b&scene=21#wechat_redirect)  

[chatGPT选股](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484803&idx=1&sn=a96365d1b1f719a0e83a60ef1c4b0165&chksm=c21ba60cf56c2f1a467ba8d5728fcbbc1319ab4817812c6dde43346dc1ea892a19539d558592&scene=21#wechat_redirect) [量化注册制](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247484876&idx=1&sn=cf7d6c875d2163bcce200946e09e4e82&chksm=c21ba643f56c2f5514f04bec3fcc62b4028b3aa67fbc81487106336cf4dec8543f1c58d30a1f&scene=21#wechat_redirect)  

[5年131倍](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485243&idx=1&sn=2c2903bce6d0de4f7480ab30c4139124&chksm=c21ba4b4f56c2da23deaa897576c6617653a7dd1d9186fdec53ba42d813a628eaf7132eddaf3&scene=21#wechat_redirect) [量化编程神器](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485006&idx=1&sn=ec989b1a9f2d74f669509dc7ce561710&chksm=c21ba5c1f56c2cd7e02fba70dab2e8236ddbc6aa05d6cf7ad7fc9205c6fe1f4f7f29461d6f6b&scene=21#wechat_redirect)

[4000因子](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485037&idx=1&sn=dad40d6cdb8482fdf1e6f94690f2494e&chksm=c21ba5e2f56c2cf48767632408133f74e3e23dbd0aac285e1f169d2d7f912516d178b04da22d&scene=21#wechat_redirect) [因子库](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486429&idx=1&sn=5f2101cfde264f0370b99b4f8b8e7ada&scene=21#wechat_redirect) [量化神集](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485464&idx=1&sn=782255a6c21ac469dc7fb85bde8699a4&chksm=c21bab97f56c2281ce0d25b95fbc689322fecd47952f24ce8e29e35da0f24891bce15dda51fb&scene=21#wechat_redirect)

[量化深坑](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485449&idx=1&sn=e228c79ce83db37b1c4360347439ddf8&chksm=c21bab86f56c22909465f838d3eb66009058cdfbe63f8a64f272d6517328d6ff4f4f4e216b93&scene=21#wechat_redirect) [老胡炒股](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485272&idx=1&sn=11e9d986e865585aa6b82ebdf28ffde0&chksm=c21ba4d7f56c2dc10545527e2fa965adde6559c1ffca60f5c1acff0413cf5616b72e1d56f661&scene=21#wechat_redirect) [私募上班](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485250&idx=1&sn=294038b08fe03a700052aa6e94aea1f2&chksm=c21ba4cdf56c2ddb2831a4da44609bc7c323d03c0897a57022fa937501bf2c18f83ac417490c&scene=21#wechat_redirect)

[机器学习算法Top10](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485534&idx=1&sn=e24e01705f49ae8e145b748705170931&chksm=c21babd1f56c22c7b99f7c78c5d0fda3f3788028f02be161a7c036c5cecc78f62a88ef92dca4&scene=21#wechat_redirect) [微盘股](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485638&idx=1&sn=855a89c9abdb037020c750b5d50bc550&chksm=c21bab49f56c225f2288b263efa6ce51046f70819165febeefb85ec3970ae0130ce54e81dfed&scene=21#wechat_redirect)

[量化的一天](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485598&idx=1&sn=0beb5d40d9ccde36e688a1c273de74ca&chksm=c21bab11f56c2207dcd2fbe6a2fc593e40bc559f1d38665eec3747fea0c04ffc6932797ef8aa&scene=21#wechat_redirect) [失败的Quant](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485604&idx=1&sn=411b3d6d6dc89743b8585739c52ccbaa&chksm=c21bab2bf56c223d1dcd11327a3b53d2e1c3b5007e5c758a7be792f2407d864608a8ce7ac15d&scene=21#wechat_redirect)  

[十年8万倍](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485624&idx=1&sn=893ca25217be05fca79e7f43ae3410cd&chksm=c21bab37f56c2221c2cc186175080622c2421cc7c1704862e482a60f282900e4c1ff02708855&scene=21#wechat_redirect) [五穷六绝](http://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247486105&idx=1&sn=87db4aa95cd30cf1e2b2b4a0205a2234&chksm=c21ba916f56c200088c4aceda6e62511469cff0d18af97fa48b659fc6ac3862d494f02fd38a6&scene=21#wechat_redirect) [一月之殇](https://mp.weixin.qq.com/s?__biz=MzkyODI5ODcyMA==&mid=2247485826&idx=1&sn=cfeb2dd29ef21c48ab2e96b568b42559&scene=21#wechat_redirect)

  

  

*Tip：点击关键字可以直接查看对应文章。*

END

如果对本文有疑惑，或是想聊聊

亦或是围观朋友圈当点赞之交

戳我，让我们一路同行

吃瓜吐槽写代码

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

添加好友后，私信『 **666** 』

送你一些量化小福利

人工回复慢请见谅~

![图片](https://mp.weixin.qq.com/s/www.w3.org/2000/svg'%20xmlns:xlink='http://www.w3.org/1999/xlink'%3E%3Ctitle%3E%3C/title%3E%3Cg%20stroke='none'%20stroke-width='1'%20fill='none'%20fill-rule='evenodd'%20fill-opacity='0'%3E%3Cg%20transform='translate(-249.000000,%20-126.000000)'%20fill='%23FFFFFF'%3E%3Crect%20x='249'%20y='126'%20width='1'%20height='1'%3E%3C/rect%3E%3C/g%3E%3C/g%3E%3C/svg%3E)

继续滑动看下一个

量化君也

向上滑动看下一个
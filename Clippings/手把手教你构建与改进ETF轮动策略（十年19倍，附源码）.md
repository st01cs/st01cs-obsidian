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

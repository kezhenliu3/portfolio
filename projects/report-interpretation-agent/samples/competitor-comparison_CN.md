# 同题对比：锚定报告的个性化解读 vs. 泛化健康建议

**方法说明。** 同一个问题分别向微信小程序「九上阿」（左）与一款第三方消费级 App（右）各提问一次：

> "我是一个素食主义者，而且身体比较差，帮我重新生成一份健康建议。"

这是**单次同题观察（anecdotal），不是基准评测**。第三方 App 刻意不点名，其品牌标识与界面中出现的用户姓名已打码。截图仅用于展示一种行为差异：**锚定用户报告数据与文献的回答 vs. 泛化的健康建议**。

## 四组截图对比

| # | 我方 — 小程序「九上阿」 | 第三方 App（品牌已打码） |
|---|---|---|
| 1 | [<img src="media/our-personalized-advice-1.jpg" width="300" alt="我方智能体结合用户血液时钟报告（心血管、肝脏、炎症偏弱）定制素食方案">](media/our-personalized-advice-1.jpg) 回答开篇即**锚定用户的血液时钟报告**：心血管、肝脏、炎症状态偏弱——素食方案围绕这些具体发现展开。 | [<img src="media/competitor-generic-1.jpg" width="300" alt="第三方 App 对同一问题的回答：泛化素食营养建议，品牌与用户名已打码">](media/competitor-generic-1.jpg) 结构完整但**泛化**的素食营养建议；界面声称使用了"个性化数据"，但建议未引用任何具体报告发现。 |
| 2 | [<img src="media/our-personalized-advice-2.jpg" width="300" alt="后续建议延续报告依据：补充剂、运动、睡眠与报告弱项对应">](media/our-personalized-advice-2.jpg) 补充剂、运动、睡眠建议持续对应报告弱项——每条建议都挂着一个具体发现。 | [<img src="media/competitor-generic-2.jpg" width="300" alt="泛化的营养素补充清单，品牌已打码">](media/competitor-generic-2.jpg) 泛化的营养素补充清单（B12、铁、Omega-3、钙、锌）。 |
| 3 | [<img src="media/our-source-tracing.jpg" width="300" alt="溯源参考面板：JAMA/BMJ/NEJM 文献标题与链接 + 报告章节'健康管理-健康饮食'">](media/our-source-tracing.jpg) 回答末尾附**溯源参考面板**：文献标题+链接（*JAMA* 2015、*BMJ* 2019、*NEJM* 2007、国家临床指南）+ 建议所依据的报告章节。 | [<img src="media/competitor-generic-3.jpg" width="300" alt="泛化的饮食结构建议，品牌已打码">](media/competitor-generic-3.jpg) 泛化的饮食结构建议（早/午/晚餐模板）。 |
| 4 | — | [<img src="media/competitor-generic-4.jpg" width="300" alt="第三方 App 结尾的主动追问，品牌已打码">](media/competitor-generic-4.jpg) 第三方 App 结尾**主动追问**（哪种素食、哪些症状）。公平起见：主动澄清是双方都具备的能力——我方在槽位缺失时会在回答前澄清；这张截图仅展示同一次会话中的差异。 |

## 实机演示（视频）

<a href="media/report-interpretation-demo.mp4"><img src="../assets/video-poster.png" width="360" alt="27 秒演示视频 — 点击图片播放"></a>

27 秒小程序录屏：前半段为**访客模式**——未绑定报告的访客得到产品介绍（回答范围限定为通用科普）；后半段为**报告模式**——绑定血液时钟报告后，系统输出生物学年龄结果、器官系统百分位与个性化流式建议。

## 看什么

1. **报告锚定**——一方点名用户实际偏弱的系统并据此定制；另一方的建议对任何用户都成立。"读了报告"与"没读报告"是全部差异所在。
2. **可验证来源**——溯源面板让每一条结论都有据可查：期刊链接与报告章节，而非空口断言。
3. **模式边界**——访客模式讲产品，报告模式讲报告；回答范围在生成之前就已决定，而不是靠 Prompt 里的一句话。

*脱敏说明：第三方品牌与用户姓名已打码；我方截图展示公开小程序及作者本人测试数据。详见[脱敏声明](README_CN.md)。*

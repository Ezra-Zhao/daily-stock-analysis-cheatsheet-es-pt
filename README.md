# daily_stock_analysis 速查表 | Daily Stock Analysis Cheatsheet | Guía rápida de daily_stock_analysis

**收盘后，它自动把自选股的结论、风险和检查清单推到你手机上——但先看合规卡：评分是 AI 算的，可以错，不是买卖指令**

> 一页看懂 ZhuLinsen/daily_stock_analysis：一个由大模型驱动的多市场自选股每日分析系统。它覆盖 A 股、港股、美股、日股、韩股、台股与 ETF，把行情、K 线、技术指标、新闻与公告聚到一起，每天自动生成一份决策仪表盘——核心结论、评分、趋势、买卖点位、风险警报、催化因素和操作检查清单都在里面——再推送到 Telegram、Discord、Slack 和邮箱，还带 Web 工作台、回测与 15 种内置策略，并能用 agent 直接问股。它不是一个模型，也不是一个交易框架，而是普通投资者每天真在用的成品系统。

- 上游项目：[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)（2026-11-11 实测 69,982 ★ / 56,797 forks；38 个 release、1,070 个 commit；2026-01-10 建仓）
- 运行方式：GitHub Actions、本地 Python 或 Docker；原仓 README 只有简体中文、英文与繁体中文三版，没有西语、葡语版
- 本页结构：中文主文 → English → Español → Português

---

Apoyo y más: [GitHub Sponsors](https://github.com/sponsors/Ezra-Zhao) · [Gumroad — plantillas y cuadernos que uso](https://ezraflow28.gumroad.com) · [Ko-fi](https://ko-fi.com/ezra777zhao)

## 合规卡（第一屏，先于一切装法）

| 记住 | 为什么 |
|---|---|
| 仅供学习研究 | 这是原仓自己写在最前面的免责声明，不是本页另外加的 |
| 不构成任何投资建议 | 仪表盘里的结论、评分与买卖点位都是 AI 生成的内容 |
| 评分可以错 | AI 评分不是荐股，更不是买卖指令；下不下单、担多大风险，是你自己的判断 |
| 本页不写收益承诺 | 全页守这条线：只讲它怎么工作、怎么装、边界在哪，不承诺任何回报 |

## 三条起步路，先选哪条

| 路 | 怎么跑 | 适合谁 |
|---|---|---|
| GitHub Actions（零成本首选） | fork 本仓 → 配好 Secrets → 启用 Actions；默认工作日 18:00（北京时间）自动跑，不需要服务器 | 大多数人：零成本、不用管机器 |
| 本地跑 | 拉下代码直接 `python main.py` | 先试一把、调配置的时候 |
| Docker 部署 | 容器化跑在自己的服务器上 | 有服务器、想长期自托管的人 |

## Secrets 别配漏卡

- 三样缺一不可：**至少一个模型 key + 至少一个通知渠道 + STOCK_LIST 自选股清单**。少配一样，要么跑不起来，要么跑完了没人收到。
- 自选股代码照这个格式写：`600519`（A 股）、`hk00700`（港股）、`AAPL`（美股）、`7203.T`（日股）。
- **API key 只放 GitHub Secrets，绝不写进代码仓**——这是原仓口径。fork 出去的仓默认公开，key 写进代码等于公开送人。

## 免费源边界卡

- 默认用 AkShare、Baostock、YFinance 等免费数据源，零配置就能跑起来。
- 但原仓自己写明：免费源受上游限流与接口变动影响，**稳定性不保证**。哪天某个源抽风、报告缺一块数据，不奇怪。
- 想要稳定，再配 Tushare、Longbridge 这类带 token 的数据源。

## 拉美与巴西本地化一行版

- 自选清单可以直接填美股代码——拉美与巴西散户大量只买美股，这一页就是按这个用法写的。
- 报告推送走 Telegram 与 Discord，正是当地最常用的两个渠道，不用另学工具。
- 行情源以 YFinance 为主。
- 本地市场（巴西 B3、墨西哥 BMV 等）的代码支持到什么程度，以原仓的市场支持边界文档为准，本页不夸大。

## 诚实标注区

- **体量**：69,982 ★ / 56,797 forks、38 个 release（2026-11-11 原仓页实测，证据 A）。
- **势头**：今日日榜第 2、约 +960 星/天（第三方榜单口径，证据 B）。
- **fork 率约 81%，在 GitHub 上很罕见**：它的主流用法就是 fork 一份到自己账号、用 Actions 每天跑——这里的 fork 数大体可以读成装机量（这是本页的读法，属于推断，不是官方统计）。
- **再说一遍合规**：AI 评分与点位可错，本页不构成投资建议。

---

## English (summary)

daily_stock_analysis (69,982 stars / 56,797 forks as of 2026-11-11; 38 releases) is an LLM-driven daily analysis system for multi-market watchlists: A-shares, Hong Kong, US, Japanese, Korean and Taiwanese stocks plus ETFs. It pulls together quotes, candlesticks, technical indicators, news and filings, and every day generates a decision dashboard — core conclusion, score, trend, buy/sell levels, risk alerts, catalysts and an action checklist — then pushes it to Telegram, Discord, Slack and email. It also ships a web workspace, backtesting, 15 built-in strategies and an agent you can ask about a ticker. Compliance first, taken from the upstream repo's own disclaimer: for study and research only, not investment advice; the scores and levels in the report are AI-generated, can be wrong, and are not stock recommendations; this page makes no return promises. Three ways to start: GitHub Actions is the zero-cost default (fork, configure Secrets, enable Actions; it runs automatically at 18:00 Beijing time on weekdays, no server needed); run it locally with `python main.py`; or deploy with Docker. Secrets checklist: at least one model key, at least one notification channel, and your STOCK_LIST — tickers are written like `600519` (A-share), `hk00700` (Hong Kong), `AAPL` (US), `7203.T` (Japan). Keys belong only in GitHub Secrets, never in the repo. Free data sources (AkShare, Baostock, YFinance) work with zero configuration, but upstream itself warns they are subject to rate limits and interface changes and do not guarantee stability; for stability, add token-based sources such as Tushare or Longbridge. For Latin America and Brazil: the watchlist takes US tickers directly, reports go out over Telegram and Discord, and YFinance is the main data source; how far local-market ticker support goes is defined by upstream's market-support documentation — this page does not overstate it.

---

## Español (guía rápida — traducción de estudio, pendiente de revisión por un hablante nativo)

**Después del cierre, te llegan al teléfono las conclusiones, los riesgos y la lista de verificación de tus acciones. Pero mira primero la tarjeta de cumplimiento: las puntuaciones las calcula una IA, pueden estar equivocadas y no son una orden de compra.**

Tarjeta de cumplimiento (lo primero, antes de cualquier instalación): es solo para estudio e investigación — es el aviso que el propio repositorio original pone al frente —; no constituye asesoramiento de inversión; las puntuaciones, las conclusiones y los niveles de compra y venta del informe los genera una IA y pueden fallar, no son recomendaciones de compra; y esta página no promete rendimientos.

daily_stock_analysis (69.982 estrellas / 56.797 forks a 11 de noviembre de 2026; 38 releases) es un sistema de análisis diario de acciones impulsado por un modelo de lenguaje. Cubre acciones A de China, Hong Kong, EE. UU., Japón, Corea, Taiwán y ETF; reúne cotizaciones, velas, indicadores técnicos, noticias y anuncios oficiales, y cada día genera un panel de decisión — conclusión principal, puntuación, tendencia, niveles de compra y venta, alertas de riesgo, catalizadores y lista de verificación — que envía a Telegram, Discord, Slack y correo electrónico. Incluye además panel web, backtesting, 15 estrategias integradas y un agente al que puedes preguntarle por una acción.

Tres caminos para empezar. El recomendado, sin costo: GitHub Actions — haz fork del repositorio, configura los Secrets y activa Actions; corre solo los días laborables a las 18:00, hora de Pekín, sin necesidad de servidor —. En local: `python main.py`. O con Docker, si ya tienes tu propio servidor. En los Secrets no puede faltar nada: al menos una clave de modelo, al menos un canal de notificación y tu lista STOCK_LIST. Los códigos se escriben así: `600519` (China A), `hk00700` (Hong Kong), `AAPL` (EE. UU.), `7203.T` (Japón). Las claves van solo en GitHub Secrets, nunca dentro del código: un fork es público.

Fuentes de datos: por defecto usa fuentes gratuitas como AkShare, Baostock e YFinance, sin configurar nada; pero el propio repositorio advierte que dependen de los límites y cambios de interfaz de terceros, y no garantizan estabilidad. Si necesitas estabilidad, añade fuentes con token como Tushare o Longbridge. Para América Latina y Brasil: la lista acepta directamente códigos de EE. UU. — que es lo que compra buena parte de la región —, los informes llegan por Telegram y Discord, y la fuente principal es YFinance; hasta dónde llega el soporte de códigos de mercados locales (B3, BMV) lo define la documentación de mercados del repositorio original, y esta página no lo exagera.

---

## Português (guia rápido — tradução de estudo, aguardando revisão de um falante nativo)

**Depois do fechamento, chegam ao seu telefone as conclusões, os riscos e a lista de verificação das suas ações. Mas olhe primeiro o cartão de conformidade: as pontuações são calculadas por uma IA, podem estar erradas e não são uma ordem de compra.**

Cartão de conformidade (o primeiro, antes de qualquer instalação): é só para estudo e pesquisa — é o aviso que o próprio repositório original coloca na frente —; não constitui recomendação de investimento; as pontuações, as conclusões e os níveis de compra e venda do relatório são gerados por uma IA e podem falhar, não são recomendação de compra; e esta página não promete rendimentos.

O daily_stock_analysis (69.982 estrelas / 56.797 forks em 11 de novembro de 2026; 38 releases) é um sistema de análise diária de ações movido por um modelo de linguagem. Cobre ações A da China, Hong Kong, EUA, Japão, Coreia, Taiwan e ETFs; reúne cotações, candles, indicadores técnicos, notícias e anúncios oficiais, e todo dia gera um painel de decisão — conclusão principal, pontuação, tendência, níveis de compra e venda, alertas de risco, catalisadores e lista de verificação — enviado para Telegram, Discord, Slack e e-mail. Traz ainda painel web, backtesting, 15 estratégias embutidas e um agente a quem você pode perguntar sobre uma ação.

Três caminhos para começar. O recomendado, sem custo: GitHub Actions — faça fork do repositório, configure os Secrets e ative o Actions; roda sozinho nos dias úteis às 18:00, horário de Pequim, sem precisar de servidor —. Local: `python main.py`. Ou com Docker, se você já tem servidor próprio. Nos Secrets não pode faltar nada: pelo menos uma chave de modelo, pelo menos um canal de notificação e a sua lista STOCK_LIST. Os códigos são escritos assim: `600519` (China A), `hk00700` (Hong Kong), `AAPL` (EUA), `7203.T` (Japão). As chaves ficam só nos GitHub Secrets, nunca dentro do código: um fork é público.

Fontes de dados: por padrão usa fontes gratuitas como AkShare, Baostock e YFinance, sem configurar nada; mas o próprio repositório avisa que elas dependem de limites e mudanças de interface de terceiros, e não garantem estabilidade. Se você precisa de estabilidade, adicione fontes com token como Tushare ou Longbridge. Para o Brasil e a América Latina: a lista aceita diretamente códigos dos EUA — que é o que boa parte da região compra —, os relatórios chegam por Telegram e Discord, e a fonte principal é o YFinance; até onde vai o suporte a códigos de mercados locais (B3, BMV) é definido pela documentação de mercados do repositório original, e esta página não exagera isso.

---

## 来源与声明

- 灵感来源 / Source / Fuente / Fonte: [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)（2026-11-11 实测 69,982 ★ / 56,797 forks，38 个 release）
- 本仓是个人学习整理：内容用我自己的话总结自上游公开文档，不搬运原文；装法、Secrets 与数据源口径以 2026-11-11 的上游 README 为准，星数以同日 GitHub 实测为准，上游迭代后请以官方文档为最终依据。本仓内容仅供学习研究，不构成任何投资建议。
- 西语、葡语部分为学习译稿，待母语校对。Las secciones en español y portugués son traducciones de estudio pendientes de revisión nativa.
- License: MIT © 2026 Guangyi Zhao

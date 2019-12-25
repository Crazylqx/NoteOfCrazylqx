# A/D和D/A变换器

- [A/D和D/A变换器](#ad%e5%92%8cda%e5%8f%98%e6%8d%a2%e5%99%a8)
  - [ADC结构和分类](#adc%e7%bb%93%e6%9e%84%e5%92%8c%e5%88%86%e7%b1%bb)
    - [Direct-Conversion ADC](#direct-conversion-adc)
    - [Successive-approximation ADC](#successive-approximation-adc)
    - [Integrating ADC](#integrating-adc)
    - [Pipeline ADC](#pipeline-adc)
    - [Σ-Δ ADC](#%ce%a3-%ce%94-adc)
  - [ADC之间的比较](#adc%e4%b9%8b%e9%97%b4%e7%9a%84%e6%af%94%e8%be%83)

## ADC结构和分类

### Direct-Conversion ADC

快闪型（Flash）ADC

- 最快的ADC，但需要大量的比较器和参考电压
- $2^N-1$个并行比较器
- 分辨率受可用Die尺寸和输入电容限制
- 各比较器性能要精确匹配
- 输出为Thermometer code，但由于亚稳态可能出现Sparkle codes
- 同分辨率die尺寸更大，比pipeline大7倍，输入电容是6倍，功耗2倍

### Successive-approximation ADC

逐次比较型ADC

只用一个比较器，将输入信号和一个N比特DAC的输出称重。

组成：

- 一个比较器
- 一个DAC
- 一个SAR
- 一个逻辑控制单元

工作频率1msps，功耗小，成本低

要求：模拟设计强，输入带宽低、采样率低

### Integrating ADC

积分型ADC

组成：

- 一个积分器
- 一个选择开关（用来选在被测电压和参考电压）
- 一个定时器（用来决定对被测电压的积分时间长度和测量参考电压积- 分消耗时间）
- 一个比较器（用来进行过零检测）
- 一个控制器
- 一个放电开关（可无）

步骤：

- 上升阶段：积分器输入为被测电压，进行固定时间的积分
- 下降阶段：积分器输入为参考电压，反向积分，测量归零时间

特点：

- 速率非常慢
- 可以去除高频噪声

### Pipeline ADC

流水线ADC

- 折中die尺寸、速度、功耗和模拟设计难度
- 广泛使用
- 每级有多余bit用于修正错误
- 级间有独立的T/H放大器，允许多级同时采样变换
- 可避免sparkle code和温度计bubble code
- 电路复杂
- 流水线延迟
- 锁存时钟定时严格

### Σ-Δ ADC

又称Oversampling convertors,结构简单，包括Σ-Δ调制器，后跟数字 抽取滤波器（Decimation Filter）。Σ-Δ调制器内部的1bitDAC作用像 一个开关，有比较器输出控制，目的使反馈信号逐渐接近输入信号Vn 。输入信号频率低，但采样频率高，输出1bit采样码，经滤波器后变 为Nbit分辨率的输出码。

特点：

- 低成本
- 高分辨率
- 有数字滤波器介入，DSP兼容
- 有利于系统集成
- 不知道精确采样时刻
- 很难多路复用
- 主要用于音频

## ADC之间的比较

采样率：
快闪型 > 流水线型 > Σ-Δ型 > 逐次比较型 > 积分型

分辨率：
Σ-Δ型 > 逐次比较型 > 流水线型 > 积分型 > 快闪型


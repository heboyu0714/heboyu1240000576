# reorder_4 四线程补充实验复核

批次 `42384122902` 的六次运行全部完成。按原始日志重数并复算，阶段报告表 3 至表 5 中与本次补充实验有关的数值一致。[阶段报告](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/report/EXPANDED_REPORT.md)

| 轮次 | 方法与原始日志 | 探索调度数 | 首次失败序号 | 触发断言的调度数 | 整次驱动耗时（秒） |
| --- | --- | ---: | ---: | ---: | ---: |
| 1 | [PERIOD](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/period_r01.txt) | 100 | 9 | 12 | 21.278865 |
| 1 | [author_serialized_abi16](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/author_serialized_abi16_r01.txt) | 384 | 47 | 87 | 135.595131 |
| 2 | [author_serialized_abi16](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/author_serialized_abi16_r02.txt) | 384 | 47 | 87 | 135.451399 |
| 2 | [PERIOD](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/period_r02.txt) | 100 | 9 | 12 | 22.225299 |
| 3 | [PERIOD](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/period_r03.txt) | 100 | 9 | 12 | 22.025956 |
| 3 | [author_serialized_abi16](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/author_serialized_abi16_r03.txt) | 384 | 47 | 85 | 130.840428 |

两种驱动在同一台主机上运行同一个四线程程序，探索深度为 3，预算为 10,000 个调度，外层时限为 240 秒。表格按启动顺序排列。调度总数来自连续的 `test` 编号，每条 `[Error Found]` 归到当前调度。耗时取日志末行的 `elapsed_seconds`，计算使用运行记录保存的原始精度。[实验方案](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/experiments/2026-11-07/REORDER4_TIMEOUT_FOLLOWUP.md) · [运行记录](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/records.json)

每种方法各三次，均值取算术平均，样本标准差的分母为 2。PERIOD 每轮比兼容串行驱动少探索 284 个调度，降幅为 284/384 = 73.96%。两种方法的整次驱动耗时分别为 21.843 ± 0.499 秒和 133.962 ± 2.705 秒。逐轮用串行耗时减去 PERIOD 耗时，得到的配对差为 **112.119 ± 2.913 秒**。

表 2 的 PERIOD 失败调度数 11.800 ± 0.632 取自上一批十次运行；本次三轮均为 12。兼容串行驱动三轮依次为 87、87、85，均值和样本标准差为 86.333 ± 1.155。三对完整数据支持本主机及配置下的调度数量和耗时比较。计时包括驱动的校准、执行和报告，比较对象为 ABI 适配后的串行驱动。本记录是归档日志复核，未重新运行实验。

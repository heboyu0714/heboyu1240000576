# Review of the `reorder_4` four-thread experiment

All six runs in follow-up batch `42384122902` completed and triggered the target assertion. Recounting the schedules and recalculating the timing statistics from the archived logs confirmed the `reorder_4` results in Tables 3–5 of the stage report. [Full review (Word)](./reorder_4_Four_Thread_Review.docx) · [Stage report](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/report/EXPANDED_REPORT.md)

## Results by run

Both methods ran the same four-thread binary on the same host, with depth 3, a budget of 10,000 schedules and a 240-second outer time limit. The table follows the recorded run order.

| Pair | Method and raw log | Schedules explored | First failing schedule | Failing schedules | Whole-driver time (s) |
| --- | --- | ---: | ---: | ---: | ---: |
| 1 | [PERIOD](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/period_r01.txt) | 100 | 9 | 12 | 21.278865 |
| 1 | [author_serialized_abi16](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/author_serialized_abi16_r01.txt) | 384 | 47 | 87 | 135.595131 |
| 2 | [author_serialized_abi16](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/author_serialized_abi16_r02.txt) | 384 | 47 | 87 | 135.451399 |
| 2 | [PERIOD](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/period_r02.txt) | 100 | 9 | 12 | 22.225299 |
| 3 | [PERIOD](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/period_r03.txt) | 100 | 9 | 12 | 22.025956 |
| 3 | [author_serialized_abi16](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/author_serialized_abi16_r03.txt) | 384 | 47 | 85 | 130.840428 |

Each numbered `test` counts as one explored schedule. Each `[Error Found]` entry belongs to the current schedule ID, and the first failing ID is one-based. The runner footer records whole-driver time in `elapsed_seconds`. The table shows six decimal places, and the calculations use the full precision in `records.json`. [Follow-up protocol](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/experiments/2026-11-07/REORDER4_TIMEOUT_FOLLOWUP.md) · [Run records](https://github.com/Sasuke-666/CS340-Research-Paper-Replication/blob/7affd301486741b5db729d746ac36facafd1935d/results/2026-11-07/comparison-42384122902/reorder_4/records.json)

## Recalculated statistics

Each value is the arithmetic mean ± sample standard deviation over three runs. The sample variance uses a denominator of two.

| Measure | PERIOD | author_serialized_abi16 |
| --- | ---: | ---: |
| Schedules explored | 100 ± 0 | 384 ± 0 |
| First failing schedule | 9 ± 0 | 47 ± 0 |
| Schedules triggering the assertion | 12 ± 0 | 86.333 ± 1.155 |
| Whole-driver time (s) | 21.843 ± 0.499 | 133.962 ± 2.705 |

PERIOD explored 284 fewer schedules in each pair, a **73.96% reduction** relative to 384. Subtracting PERIOD time from serialized time within each pair gives 114.316266, 113.226100 and 108.814472 seconds. The paired difference was **112.119 ± 2.913 seconds**.

## Scope of the comparison

Table 2 reports 11.800 ± 0.632 failing schedules for PERIOD across ten earlier runs. Each of the three follow-up runs recorded 12. The earlier batch used a different host and a 120-second outer limit, which all ten earlier serialized runs reached. The timing comparison uses only the three complete follow-up pairs. It measures the entire driver invocation, including calibration, execution and reporting, for PERIOD and the ABI-adapted serialized driver on this host. The review used archived logs.

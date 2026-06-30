# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-30T07:22:34Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 9V74 80-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 60.40K | ± 814.18 | ops/s | **fastest** |
| prometheusNoLabelsInc | 52.36K | ± 395.58 | ops/s | 1.2x slower |
| prometheusAdd | 48.41K | ± 1.18K | ops/s | 1.2x slower |
| codahaleIncNoLabels | 44.49K | ± 731.26 | ops/s | 1.4x slower |
| simpleclientInc | 6.22K | ± 110.30 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.12K | ± 176.19 | ops/s | 9.9x slower |
| simpleclientAdd | 5.94K | ± 193.38 | ops/s | 10x slower |
| openTelemetryInc | 1.37K | ± 129.93 | ops/s | 44x slower |
| openTelemetryIncNoLabels | 1.33K | ± 93.89 | ops/s | 46x slower |
| openTelemetryAdd | 1.30K | ± 39.72 | ops/s | 46x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.49K | ± 1.63K | ops/s | **fastest** |
| simpleclient | 4.34K | ± 90.25 | ops/s | 1.3x slower |
| prometheusNative | 3.14K | ± 114.59 | ops/s | 1.8x slower |
| openTelemetryClassic | 595.22 | ± 13.40 | ops/s | 9.2x slower |
| openTelemetryExponential | 514.40 | ± 29.70 | ops/s | 11x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 530.07K | ± 3.35K | ops/s | **fastest** |
| prometheusWriteToByteArray | 525.46K | ± 1.39K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 519.40K | ± 7.07K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 509.43K | ± 4.76K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      44489.049    ± 731.259  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1301.983     ± 39.721  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1367.712    ± 129.930  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1325.720     ± 93.892  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      48406.221   ± 1176.462  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      60399.121    ± 814.184  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      52361.234    ± 395.580  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       5940.389    ± 193.379  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6220.342    ± 110.297  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6123.968    ± 176.195  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        595.225     ± 13.398  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        514.396     ± 29.704  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5489.001   ± 1630.637  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3135.062    ± 114.588  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4339.871     ± 90.252  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     509425.737   ± 4755.948  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     519403.793   ± 7071.613  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     525463.605   ± 1388.702  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     530066.157   ± 3348.987  ops/s
```

## Notes

- **Score** = Throughput in operations per second (higher is better)
- **Error** = 99.9% confidence interval

## Benchmark Descriptions

| Benchmark | Description |
|:----------|:------------|
| **CounterBenchmark** | Counter increment performance: Prometheus, OpenTelemetry, simpleclient, Codahale |
| **HistogramBenchmark** | Histogram observation performance (classic vs native/exponential) |
| **TextFormatUtilBenchmark** | Metric exposition format writing speed |

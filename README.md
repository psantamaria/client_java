# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-05-19T07:19:05Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1013-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.80K | ± 557.72 | ops/s | **fastest** |
| prometheusNoLabelsInc | 57.12K | ± 187.69 | ops/s | 1.2x slower |
| prometheusAdd | 51.08K | ± 517.78 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 45.01K | ± 8.48K | ops/s | 1.5x slower |
| simpleclientNoLabelsInc | 6.52K | ± 148.41 | ops/s | 10x slower |
| simpleclientInc | 6.48K | ± 187.46 | ops/s | 10x slower |
| simpleclientAdd | 6.19K | ± 232.70 | ops/s | 11x slower |
| openTelemetryInc | 1.34K | ± 118.18 | ops/s | 49x slower |
| openTelemetryIncNoLabels | 1.25K | ± 74.37 | ops/s | 53x slower |
| openTelemetryAdd | 1.25K | ± 18.66 | ops/s | 53x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 5.32K | ± 1.76K | ops/s | **fastest** |
| simpleclient | 4.49K | ± 26.16 | ops/s | 1.2x slower |
| prometheusNative | 2.72K | ± 105.99 | ops/s | 2.0x slower |
| openTelemetryClassic | 695.37 | ± 46.01 | ops/s | 7.7x slower |
| openTelemetryExponential | 537.73 | ± 48.25 | ops/s | 9.9x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 488.43K | ± 2.76K | ops/s | **fastest** |
| prometheusWriteToByteArray | 487.63K | ± 4.18K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 476.65K | ± 5.61K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 471.21K | ± 7.07K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      45007.465   ± 8477.694  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1249.888     ± 18.663  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1342.197    ± 118.175  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1250.216     ± 74.368  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51076.778    ± 517.780  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65795.246    ± 557.718  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      57124.647    ± 187.689  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6186.776    ± 232.698  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6484.594    ± 187.455  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6517.300    ± 148.409  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        695.372     ± 46.014  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        537.733     ± 48.248  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       5320.035   ± 1757.481  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2715.312    ± 105.995  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4490.207     ± 26.163  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     471213.357   ± 7066.231  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     476650.491   ± 5610.833  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     487628.670   ± 4184.993  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     488431.062   ± 2756.817  ops/s
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

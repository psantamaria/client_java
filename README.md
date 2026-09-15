# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-09-15T08:20:40Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** INTEL(R) XEON(R) PLATINUM 8573C, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1022-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusNoLabelsInc | 29.27K | ± 1.22K | ops/s | **fastest** |
| codahaleIncNoLabels | 29.03K | ± 1.20K | ops/s | 1.0x slower |
| prometheusInc | 28.33K | ± 1.41K | ops/s | 1.0x slower |
| prometheusAdd | 27.78K | ± 1.08K | ops/s | 1.1x slower |
| simpleclientNoLabelsInc | 7.46K | ± 78.19 | ops/s | 3.9x slower |
| simpleclientInc | 7.23K | ± 75.77 | ops/s | 4.0x slower |
| simpleclientAdd | 6.98K | ± 150.95 | ops/s | 4.2x slower |
| openTelemetryInc | 1.17K | ± 11.44 | ops/s | 25x slower |
| openTelemetryAdd | 1.11K | ± 65.22 | ops/s | 26x slower |
| openTelemetryIncNoLabels | 1.05K | ± 40.30 | ops/s | 28x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| simpleclient | 4.80K | ± 129.46 | ops/s | **fastest** |
| prometheusClassic | 2.88K | ± 572.42 | ops/s | 1.7x slower |
| prometheusNative | 2.22K | ± 152.14 | ops/s | 2.2x slower |
| openTelemetryClassic | 402.04 | ± 18.96 | ops/s | 12x slower |
| openTelemetryExponential | 318.23 | ± 6.84 | ops/s | 15x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToByteArray | 300.38K | ± 4.65K | ops/s | **fastest** |
| prometheusWriteToNull | 297.75K | ± 4.66K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 283.03K | ± 1.73K | ops/s | 1.1x slower |
| openMetricsWriteToByteArray | 282.95K | ± 3.71K | ops/s | 1.1x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      29032.782   ± 1197.905  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1112.109     ± 65.219  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1170.386     ± 11.440  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1050.666     ± 40.299  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      27776.417   ± 1078.265  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      28325.410   ± 1408.221  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      29268.092   ± 1216.575  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6984.017    ± 150.955  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       7229.299     ± 75.768  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       7460.057     ± 78.190  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        402.038     ± 18.965  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        318.231      ± 6.837  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       2880.574    ± 572.419  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       2222.660    ± 152.145  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4798.836    ± 129.458  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     282948.090   ± 3713.360  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     283026.005   ± 1728.792  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     300382.492   ± 4645.936  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     297749.655   ± 4662.422  ops/s
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

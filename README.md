# Prometheus Java Client Benchmarks

## Run Information

- **Date:** 2026-06-24T07:18:57Z
- **Commit:** [`4b69f40`](https://github.com/psantamaria/client_java/commit/4b69f40bd4e616d69468ce99dc4323162287a577)
- **JDK:** 25.0.2 (OpenJDK 64-Bit Server VM)
- **Benchmark config:** 3 fork(s), 3 warmup, 5 measurement, 4 threads
- **Hardware:** AMD EPYC 7763 64-Core Processor, 4 cores, 16 GB RAM
- **OS:** Linux 6.17.0-1018-azure

## Results

### CounterBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusInc | 65.06K | ± 1.26K | ops/s | **fastest** |
| prometheusNoLabelsInc | 55.27K | ± 1.22K | ops/s | 1.2x slower |
| prometheusAdd | 51.21K | ± 533.48 | ops/s | 1.3x slower |
| codahaleIncNoLabels | 48.58K | ± 2.30K | ops/s | 1.3x slower |
| simpleclientInc | 6.71K | ± 11.77 | ops/s | 9.7x slower |
| simpleclientNoLabelsInc | 6.36K | ± 186.54 | ops/s | 10x slower |
| simpleclientAdd | 6.29K | ± 281.26 | ops/s | 10x slower |
| openTelemetryInc | 1.38K | ± 208.46 | ops/s | 47x slower |
| openTelemetryAdd | 1.25K | ± 49.02 | ops/s | 52x slower |
| openTelemetryIncNoLabels | 1.15K | ± 74.56 | ops/s | 57x slower |

### HistogramBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusClassic | 6.56K | ± 1.20K | ops/s | **fastest** |
| simpleclient | 4.46K | ± 80.96 | ops/s | 1.5x slower |
| prometheusNative | 3.08K | ± 259.44 | ops/s | 2.1x slower |
| openTelemetryClassic | 684.50 | ± 7.36 | ops/s | 9.6x slower |
| openTelemetryExponential | 567.17 | ± 11.86 | ops/s | 12x slower |

### TextFormatUtilBenchmark

| Benchmark | Score | Error | Units | |
|:----------|------:|------:|:------|:---|
| prometheusWriteToNull | 484.80K | ± 3.88K | ops/s | **fastest** |
| prometheusWriteToByteArray | 481.38K | ± 4.99K | ops/s | 1.0x slower |
| openMetricsWriteToNull | 480.43K | ± 5.93K | ops/s | 1.0x slower |
| openMetricsWriteToByteArray | 470.17K | ± 4.87K | ops/s | 1.0x slower |

### Raw Results

```
Benchmark                                            Mode  Cnt          Score        Error  Units
CounterBenchmark.codahaleIncNoLabels                thrpt   15      48575.881   ± 2299.826  ops/s
CounterBenchmark.openTelemetryAdd                   thrpt   15       1250.309     ± 49.022  ops/s
CounterBenchmark.openTelemetryInc                   thrpt   15       1379.286    ± 208.461  ops/s
CounterBenchmark.openTelemetryIncNoLabels           thrpt   15       1145.726     ± 74.559  ops/s
CounterBenchmark.prometheusAdd                      thrpt   15      51213.819    ± 533.483  ops/s
CounterBenchmark.prometheusInc                      thrpt   15      65058.241   ± 1257.390  ops/s
CounterBenchmark.prometheusNoLabelsInc              thrpt   15      55266.226   ± 1223.473  ops/s
CounterBenchmark.simpleclientAdd                    thrpt   15       6289.467    ± 281.258  ops/s
CounterBenchmark.simpleclientInc                    thrpt   15       6710.118     ± 11.768  ops/s
CounterBenchmark.simpleclientNoLabelsInc            thrpt   15       6361.164    ± 186.541  ops/s
HistogramBenchmark.openTelemetryClassic             thrpt   15        684.504      ± 7.356  ops/s
HistogramBenchmark.openTelemetryExponential         thrpt   15        567.167     ± 11.864  ops/s
HistogramBenchmark.prometheusClassic                thrpt   15       6560.440   ± 1198.921  ops/s
HistogramBenchmark.prometheusNative                 thrpt   15       3078.958    ± 259.441  ops/s
HistogramBenchmark.simpleclient                     thrpt   15       4462.858     ± 80.960  ops/s
TextFormatUtilBenchmark.openMetricsWriteToByteArray  thrpt   15     470168.376   ± 4870.164  ops/s
TextFormatUtilBenchmark.openMetricsWriteToNull      thrpt   15     480428.998   ± 5929.263  ops/s
TextFormatUtilBenchmark.prometheusWriteToByteArray  thrpt   15     481382.979   ± 4989.592  ops/s
TextFormatUtilBenchmark.prometheusWriteToNull       thrpt   15     484803.236   ± 3884.475  ops/s
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

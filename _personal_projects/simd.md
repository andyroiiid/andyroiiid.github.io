---
title:  "SIMD Experiments"
excerpt: "Some experiments with SIMD instrinsics. The goal is to write a new SIMD math library for Haru-V engine."
header:
  teaser: /assets/images/simd/cover.png
  overlay_image: /assets/images/simd/cover.png
  overlay_filter: 0.5
  caption: "Screenshot of benchmarking"
  actions:
    - label: "GitHub"
      url: https://github.com/andyroiiid/SimdExperiments/
sidebar:
    - title: "Type"
      text: "Math Library"
    - title: "Programming Lanauges"
      text: "C++"
    - title: "Highlighted Features"
      text: "SIMD Intrinsics, Vector/Matrix/Quaternion Support"
    - title: "Team"
      text: "Solo"
    - title: "Work Period"
      text: "03/14/2022 - Present"
    - title: "GitHub Repository"
      text: "https://github.com/andyroiiid/SimdExperiments/"

toc: true
---

This project is still in early stage so there's not much to share, but here are some benchmarks I did.

The benchmarks are done on a Terrans Force AMD 27X7SH1 laptop. Here's the environment:
- CPU: AMD Ryzen 7 3700X 8-Core Processor 3.59 GHz
- RAM: 16GB DDR4 3200MHz
- Windows Version: Windows 10 Pro Version	22H2 OS build	19045.2728

There was [a great talk on quaternions at GDC 2023 by Hamish Todd](https://schedule.gdconf.com/session/math-in-game-development-summit-a-visual-guide-to-quaternions-and-dual-quaternions/894472). I stayed in Room 2001 all day with [Prof. Squirrel](http://www.eiserloh.net/bio/) and those talks were amazing. You should definitely check the GDC Vault if you missed them!
{: .notice--success}

## Normalization Benchmarks (3.25ns -> 3.01ns -> 1.25ns)
```
benchmark name                       samples       iterations    estimated
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
Plain Normalize                                100          6859     2.7436 ms
                                        3.25485 ns    3.07785 ns    3.66395 ns
                                        1.30459 ns   0.668945 ns    2.31069 ns

SIMD Normalize                                 100          9750      2.925 ms
                                        3.01292 ns    2.44769 ns    5.71959 ns
                                        5.39945 ns  0.0793706 ns    12.8712 ns

SIMD Fast Normalize                            100         23303     2.3303 ms
                                        1.25147 ns    1.21847 ns    1.39355 ns
                                       0.298176 ns  0.0517975 ns   0.699776 ns
```

## Cross Product Benchmarks (6.09ns -> 0.85ns)
```
benchmark name                       samples       iterations    estimated
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
Plain Cross Product                            100          4693     2.8158 ms
                                        6.09269 ns    6.08225 ns    6.11144 ns
                                      0.0694439 ns  0.0424052 ns   0.109927 ns

SIMD Cross Product                             100         32996          0 ns
                                       0.852285 ns   0.849558 ns   0.857104 ns
                                      0.0181609 ns  0.0115653 ns  0.0274572 ns
```

## Matrix Multiplication Benchmarks (35.87ns -> 5.29ns)
```
benchmark name                       samples       iterations    estimated
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
Plain Matrix Multiplication                    100          1453      2.906 ms
                                        35.8727 ns    35.5726 ns    36.1142 ns
                                        1.36282 ns    1.05278 ns    2.15015 ns

SIMD Matrix Multiplication                     100          5800        2.9 ms
                                        5.29724 ns    5.17569 ns    5.55534 ns
                                       0.862319 ns   0.480469 ns    1.41255 ns
```

## LookAt Matrix Benchmarks (35.71ns -> 23.42ns)
```
benchmark name                       samples       iterations    estimated
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
Plain LookAt                                   100           840       2.94 ms
                                        35.7131 ns    34.9714 ns    37.1821 ns
                                         5.1074 ns    3.03591 ns    7.97927 ns

SIMD LookAt                                    100          1298     2.9854 ms
                                        23.4299 ns    23.2419 ns     23.641 ns
                                        1.02251 ns   0.917863 ns    1.10795 ns
```

## Perspective Matrix Benchmarks (11.03ns -> 6.76ns)
```
benchmark name                       samples       iterations    estimated
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
Plain Perspective                              100          2726      2.726 ms
                                        11.0279 ns    10.9215 ns    11.4079 ns
                                       0.917814 ns   0.238381 ns    2.10322 ns

SIMD Perspective                               100          4388     2.6328 ms
                                        6.75501 ns    6.74111 ns    6.80378 ns
                                       0.119221 ns  0.0315541 ns   0.272402 ns
```

## Quaternion Hamilton Product Benchmarks (7.13ns -> 1.29ns)
```
benchmark name                       samples       iterations    estimated
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
Plain Quat Hamilton Product                    100          4266     2.5596 ms
                                         7.1369 ns    7.01711 ns    7.45499 ns
                                       0.893766 ns   0.189609 ns    1.80165 ns

SIMD Quat Hamilton Product                     100         23125     2.3125 ms
                                        1.29937 ns    1.28549 ns    1.36216 ns
                                       0.127958 ns  0.0149846 ns   0.302725 ns
```

## Quaternion To Matrix Benchmarks (5.61ns -> 3.60ns)
```
benchmark name                       samples       iterations    estimated
                                     mean          low mean      high mean
                                     std dev       low std dev   high std dev
-------------------------------------------------------------------------------
Plain Quat To Matrix                           100          4949     2.9694 ms
                                        5.60598 ns    5.55223 ns    5.87189 ns
                                       0.530724 ns 0.00201048 ns    1.16256 ns

SIMD Quat To Matrix                            100          8518     2.5554 ms
                                        3.60284 ns    3.53287 ns    3.73034 ns
                                       0.468055 ns   0.315483 ns   0.814731 ns
```

# COVID-19 SIR mathematical model for Madrid

SIR mathematical model for infectious diseases optimized for COVID-19 using Spanish Ministry of Health public available data for Madrid.

-----

![sir-cases](https://github.com/agastalver/sir-covid-19-madrid/raw/master/images/generated-sir-cases.png "SIR Model Cases")

![sir](https://github.com/agastalver/sir-covid-19-madrid/raw/master/images/generated-sir.png "SIR Model")

**Note**: 

* `susceptible`, `infected`, and `recovered`, stand for the observable population; thus, the ones that can be detected. The actual values could be higher.
* `susceptible` is an estimated value calculated from `N` with respect to the `infected` and `recovered`, the actual value is not provided by the government.
* `recovered` stands for people who has recovered from the virus or has died; as considered in the SIR model.

-----

## Last optimization

### Case forecasting table

| Date           | Infected  | Cases     |
|:--------------:|:---------:|:---------:|
| 2020-04-15     | 14116     | 49575     |
| 2020-04-16     | 13591     | 50336     |
| 2020-04-17     | 13050     | 51032     |
| 2020-04-18     | 12500     | 51668     |
| 2020-04-19     | 11945     | 52248     |
| 2020-04-20     | 11392     | 52778     |
| 2020-04-21     | 10844     | 53262     |
| 2020-04-22     | 10305     | 53704     |
| 2020-04-23     | 9776      | 54108     |
| 2020-04-24     | 9262      | 54478     |
| 2020-04-25     | 8763      | 54815     |
| 2020-04-26     | 8281      | 55125     |
| 2020-04-27     | 8069      | 55671     |

### Optimized SIR parameters

```
N = 64712.04793187371
beta = 0.4604897386293976
gamma = 0.09199941219277888
delta = 0.5186519863016679
delay = 1
```

* `delta` stands for a factor of reduction of `beta` during the lockdown.
* All results are available in the folders `images` and `data`.

-----

## Last data information

### Madrid total cases

![total](https://github.com/agastalver/sir-covid-19-madrid/raw/master/images/generated-total.png "Total cases")

-----

## Methodology

### Data sources

Main data source:

* Spanish government: https://www.mscbs.gob.es/profesionales/saludPublica/ccayes/alertasActual/nCov-China/situacionActual.htm
  * https://covid19.isciii.es/
  * https://covid19.isciii.es/resources/serie_historica_acumulados.csv

* Github: https://github.com/datadista/datasets
  * https://raw.githubusercontent.com/datadista/datasets/master/COVID%2019/ccaa_covid19_casos_long.csv
  * https://raw.githubusercontent.com/datadista/datasets/master/COVID%2019/ccaa_covid19_altas_long.csv
  * https://raw.githubusercontent.com/datadista/datasets/master/COVID%2019/ccaa_covid19_fallecidos_long.csv

### Epidemiology model

This is based on the SIR epidemiology model proposed by W. O. Kermack and A. G. McKendrick in:

```
Kermack, W. O.; McKendrick, A. G. (1927). "A Contribution to the Mathematical Theory of Epidemics". Proceedings of the Royal Society A: Mathematical, Physical and Engineering Sciences. 115 (772): 700. Bibcode:1927RSPSA.115..700K. doi:10.1098/rspa.1927.0118. JSTOR 94815.
```

You can find the description on wikipedia: https://en.wikipedia.org/wiki/Mathematical_modelling_of_infectious_disease#The_SIR_model

### Optimization

The parameters `N`, `beta`, and `gamma`, are unknown. Additionally, a `delay` parameter is considered; defined as a time synchronization parameter in case the available data is not adjusted to day 0.

The optimization method is Nendel-Mead, adjusting mean squares on `I(t)` and `R(t)` to the available data. `S(t)` and `N` are calculated backwards.

```
Nelder, John A.; R. Mead (1965). "A simplex method for function minimization". Computer Journal. 7 (4): 308–313. doi:10.1093/comjnl/7.4.308.
```

## Usage

Execute:

```
$ python main.py
```

## Important note

The mathematical model could not adjust to the real behaviour of the virus. Furthermore, the data can have errors, delays, or be incomplete, so the adjustment can vary in the future.

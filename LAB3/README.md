# LAB3
Лякин Даниил

Информационно-аналитические технологии поиска угроз инорфмационной
безопасности

# Основы обработки данных с помощью R и Dplyr

## Цель работы

1.  Развить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания базовых типов данных языка R
3.  Развить практические навыки использования функций обработки данных
    пакета dplyr – функции `select()`, `filter()`,`mutate()`,
    `arrange()`, `group_by()`

## Исходные данные

1.  Операционная система Windows 10
2.  Rstudio Desktop
3.  Интерпретатор языка R версии 4.4.2
4.  Github
5.  Программный пакет dplyr, nycflights13

## План выполнения работы

1.  Установить программный пакет dplyr
2.  Проанализировать датафреймы в рамках пакета nycflights13
3.  Выполнить аналитические задания

## Содержание Работы

### Шаг 1. Установка пакета dplyr

``` r
install.packages('nycflights13')
```

WARNING: Rtools is required to build R packages but is not currently
installed. Please download and install the appropriate version of Rtools
before proceeding:

https://cran.rstudio.com/bin/windows/Rtools/ Устанавливаю пакет в
‘C:/Users/qq/AppData/Local/R/win-library/4.4’ (потому что ‘lib’ не
определено) пробую URL
‘https://cran.rstudio.com/bin/windows/contrib/4.4/nycflights13_1.0.2.zip’
Content type ‘application/zip’ length 4511507 bytes (4.3 MB) downloaded
4.3 MB

пакет ‘nycflights13’ успешно распакован, MD5-суммы проверены

Скачанные бинарные пакеты находятся в C:7o\_packages

### Шаг 2. Подгрузка пакет

``` r
library(nycflights13)
```

### Шаг 3. Количество датафреймов

``` r
data(package = "nycflights13")
```

Data sets in package ‘nycflights13’:

airlines Airline names. airports Airport metadata flights Flights data
planes Plane metadata. weather Hourly weather data

``` r
length(data(package = "nycflights13"))
```

\[1\] 4

### Шаг 4. Количество строк в каждком пакете

``` r
data_list <- data(package = "nycflights13")$results[, "Item"]
```

``` r
rows_in_datasets <- sapply(data_list, function(x) nrow(get(x)))
```

``` r
rows_in_datasets
```

airlines airports flights planes weather 16 1458 336776 3322 26115

``` r
rows_in_datasets
```

airlines airports flights planes weather 16 1458 336776 3322 26115

### Шаг 5. Количество столбцов в каждом датафрейме

``` r
cols_in_datasets <- sapply(data_list, function(x) ncol(get(x)))
```

``` r
cols_in_datasets
```

airlines airports flights planes weather 2 8 19 9 15

### Шаг 6. Примерный вид датафреймов

``` r
lapply(data_list, function(x) head(get(x)))
```

\[\[1\]\] A tibble: 6 × 2 carrier name <chr> <chr> 1 9E Endeavor Air
Inc. 2 AA American Airlines Inc. 3 AS Alaska Airlines Inc. 4 B6 JetBlue
Airways 5 DL Delta Air Lines Inc. 6 EV ExpressJet Airlines Inc.

\[\[2\]\] A tibble: 6 × 8 faa name lat lon alt tz dst tzone <chr> <chr>
<dbl> <dbl> <dbl> <dbl> <chr> <chr> 1 04G Lansdowne Airport 41.1 -80.6
1044 -5 A America/New_Yo… 2 06A Moton Field Municipal Airport 32.5 -85.7
264 -6 A America/Chicago 3 06C Schaumburg Regional 42.0 -88.1 801 -6 A
America/Chicago 4 06N Randall Airport 41.4 -74.4 523 -5 A
America/New_Yo… 5 09J Jekyll Island Airport 31.1 -81.4 11 -5 A
America/New_Yo… 6 0A9 Elizabethton Municipal Airport 36.4 -82.2 1593 -5
A America/New_Yo…

\[\[3\]\] A tibble: 6 × 19 year month day dep_time sched_dep_time
dep_delay arr_time sched_arr_time <int> <int> <int> <int> <int> <dbl>
<int> <int> 1 2013 1 1 517 515 2 830 819 2 2013 1 1 533 529 4 850 830 3
2013 1 1 542 540 2 923 850 4 2013 1 1 544 545 -1 1004 1022 5 2013 1 1
554 600 -6 812 837 6 2013 1 1 554 558 -4 740 728 ℹ 11 more variables:
arr_delay <dbl>, carrier <chr>, flight <int>, tailnum <chr>, origin
<chr>, dest <chr>, air_time <dbl>, distance <dbl>, hour <dbl>, minute
<dbl>, time_hour <dttm>

\[\[4\]\] A tibble: 6 × 9 tailnum year type manufacturer model engines
seats speed engine <chr> <int> <chr> <chr> <chr> <int> <int> <int> <chr>
1 N10156 2004 Fixed wing multi engi… EMBRAER EMB-… 2 55 NA Turbo… 2
N102UW 1998 Fixed wing multi engi… AIRBUS INDU… A320… 2 182 NA Turbo… 3
N103US 1999 Fixed wing multi engi… AIRBUS INDU… A320… 2 182 NA Turbo… 4
N104UW 1999 Fixed wing multi engi… AIRBUS INDU… A320… 2 182 NA Turbo… 5
N10575 2002 Fixed wing multi engi… EMBRAER EMB-… 2 55 NA Turbo… 6 N105UW
1999 Fixed wing multi engi… AIRBUS INDU… A320… 2 182 NA Turbo…

\[\[5\]\] A tibble: 6 × 15 origin year month day hour temp dewp humid
wind_dir wind_speed wind_gust <chr> <int> <int> <int> <int> <dbl> <dbl>
<dbl> <dbl> <dbl> <dbl> 1 EWR 2013 1 1 1 39.0 26.1 59.4 270 10.4 NA 2
EWR 2013 1 1 2 39.0 27.0 61.6 250 8.06 NA 3 EWR 2013 1 1 3 39.0 28.0
64.4 240 11.5 NA 4 EWR 2013 1 1 4 39.9 28.0 62.2 250 12.7 NA 5 EWR 2013
1 1 5 39.0 28.0 64.4 260 12.7 NA 6 EWR 2013 1 1 6 37.9 28.0 67.2 240
11.5 NA ℹ 4 more variables: precip <dbl>, pressure <dbl>, visib <dbl>,
time_hour <dttm>

### Шаг 7. Подсчет количество компаний-перевозчиков

``` r
num_carriers <- length(unique(flights$carrier))
```

``` r
num_carriers
```

\[1\] 16

### Шаг 8. Подсчет количества рейсов John f Kennedy в мае

``` r
jfk_may_flights <- flights %>% filter(month == 5, origin == "JFK") %>% summarise(num_flights = n())
```

``` r
jfk_may_flights
```

A tibble: 1 × 1 num_flights <int> 1 9397

### Шаг 9. Поиск самого северного аэропорта

``` r
northern_airport <- airports %>% arrange(desc(lat)) %>% slice(1)
```

``` r
northern_airport
```

A tibble: 1 × 8 faa name lat lon alt tz dst tzone <chr> <chr> <dbl>
<dbl> <dbl> <dbl> <chr> <chr> 1 EEN Dillant Hopkins Airport 72.3 42.9
149 -5 A NA

### Шаг 10. Поиск самого высокогорного аэропорта

``` r
highest_airport <- airports %>% arrange(desc(alt)) %>% slice(1)
```

``` r
highest_airport
```

A tibble: 1 × 8 faa name lat lon alt tz dst tzone <chr> <chr> <dbl>
<dbl> <dbl> <dbl> <chr> <chr> 1 TEX Telluride 38.0 -108. 9078 -7 A
America/Denver

### Шаг 11. Поиск самых старых самолетов

``` r
oldest_planes <- planes %>% arrange(year) %>% slice(1:5)
```

``` r
oldest_planes
```

A tibble: 5 × 9 tailnum year type manufacturer model engines seats speed
engine <chr> <int> <chr> <chr> <chr> <int> <int> <int> <chr> 1 N381AA
1956 Fixed wing multi engine DOUGLAS DC-7BF 4 102 232 Recipr… 2 N201AA
1959 Fixed wing single engine CESSNA 150 1 2 90 Recipr… 3 N567AA 1959
Fixed wing single engine DEHAVILLAND OTTER DHC-3 1 16 95 Recipr… 4
N378AA 1963 Fixed wing single engine CESSNA 172E 1 4 105 Recipr… 5
N575AA 1963 Fixed wing single engine CESSNA 210-5(205) 1 6 NA Recipr…

### Шаг 12. Поиск средней температуры воздуха в сентябре в аэропорту JFK

``` r
average_temp_jfk_september <- weather %>% filter(month == 9, origin == "JFK") %>% summarise(average_temp = mean(temp, na.rm = TRUE))
```

``` r
average_temp_jfk_september
```

A tibble: 1 × 1 average_temp <dbl> 1 66.9

### Шаг 13. Поиск авиакомпании с самым большим количеством рейсов в июне

``` r
top_carrier_june <- flights %>% filter(month == 6) %>% group_by(carrier) %>% summarise(num_flights = n()) %>% arrange(desc(num_flights)) %>% slice(1)
```

``` r
top_carrier_june
```

A tibble: 1 × 2 carrier num_flights <chr> <int> 1 UA 4975 \### Шаг 14.
Поиск компании с самым большим количеством задержек рейсов

``` r
top_delayed_carrier <- flights %>% filter(dep_delay > 0) %>% group_by(carrier) %>% summarise(delayed_flights = n()) %>% arrange(desc(delayed_flights)) %>% slice(1)
```

``` r
top_delayed_carrier
```

A tibble: 1 × 2 carrier delayed_flights <chr> <int> 1 UA 27261

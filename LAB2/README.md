# LAB2
Лякин Даниил

Информационно-аналитические технологии поиска угроз инорфмационной
безопасности

# Введение в R

## Цель работы

Развить навыки работы с языком программирования R и закрепить знания
базовых типов данных и операций с ними

## Исходные данные

1.  Операционная система Windows 10
2.  Rstudio Desktop
3.  Интерпретатор языка R версии 4.4.2
4.  Github
5.  Программный пакет swirl

## План выполнения работы

1.  Установить программный пакет swirl
2.  Выполнить курсы, указанные в задание

## Содержание Работы

### Шаг 1. Установка программного пакет swirl.

На данном шаге необходимо установить программный пакет swirl.

![](./Images/1.png)

### Шаг 2. Запуск swirl и выбор обучения

![](./Images/2.png)

![](./Images/3.png)

### Выполнение практики по 5 подкурсам в рамках обучения “R Programming: The basics of programming in R”

``` r
install.packages("dplyr")
```WARNING: Rtools is required to build R packages but is not currently installed. Please download and install the appropriate version of Rtools before proceeding:

https://cran.rstudio.com/bin/windows/Rtools/
Устанавливаю пакет в ‘C:/Users/qq/AppData/Local/R/win-library/4.4’
(потому что ‘lib’ не определено)
устанавливаю также зависимости ‘fansi’, ‘utf8’, ‘pkgconfig’, ‘generics’, ‘pillar’, ‘tibble’, ‘tidyselect’

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/fansi_1.0.6.zip'
Content type 'application/zip' length 324751 bytes (317 KB)
downloaded 317 KB

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/utf8_1.2.4.zip'
Content type 'application/zip' length 151200 bytes (147 KB)
downloaded 147 KB

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/pkgconfig_2.0.3.zip'
Content type 'application/zip' length 23168 bytes (22 KB)
downloaded 22 KB

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/generics_0.1.3.zip'
Content type 'application/zip' length 84636 bytes (82 KB)
downloaded 82 KB

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/pillar_1.9.0.zip'
Content type 'application/zip' length 665218 bytes (649 KB)
downloaded 649 KB

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/tibble_3.2.1.zip'
Content type 'application/zip' length 696560 bytes (680 KB)
downloaded 680 KB

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/tidyselect_1.2.1.zip'
Content type 'application/zip' length 229256 bytes (223 KB)
downloaded 223 KB

пробую URL 'https://cran.rstudio.com/bin/windows/contrib/4.4/dplyr_1.1.4.zip'
Content type 'application/zip' length 1588818 bytes (1.5 MB)
downloaded 1.5 MB

пакет ‘fansi’ успешно распакован, MD5-суммы проверены
пакет ‘utf8’ успешно распакован, MD5-суммы проверены
пакет ‘pkgconfig’ успешно распакован, MD5-суммы проверены
пакет ‘generics’ успешно распакован, MD5-суммы проверены
пакет ‘pillar’ успешно распакован, MD5-суммы проверены
пакет ‘tibble’ успешно распакован, MD5-суммы проверены
пакет ‘tidyselect’ успешно распакован, MD5-суммы проверены
пакет ‘dplyr’ успешно распакован, MD5-суммы проверены

Скачанные бинарные пакеты находятся в
    C:\Users\qq\AppData\Local\Temp\RtmpUbMz7o\downloaded_packages
```r
library(dplyr)
```

Присоединяю пакет: ‘dplyr’

Следующие объекты скрыты от ‘package:stats’:

    filter, lag

Следующие объекты скрыты от ‘package:base’:

    intersect, setdiff, setequal, union

`r starwars %>% nrow()`\[1\] 87 `r starwars %>% ncol()`\[1\] 14 \`\`\`r

\`\`\``r starwars %>% glimpse()`Rows: 87 Columns: 14 $ name <chr> “Luke
Skywalker”, “C-3PO”, “R2-D2”, … $ height <int> 172, 167, 96, 202, 150,
178, 165, 97… $ mass <dbl> 77, 75, 32, 136, 49, 120, 75, 32, 84… $
hair_color <chr> “blond”, NA, NA, “none”, “brown”, “b… $ skin_color
<chr>”fair”, “gold”, “white, blue”, “whit… $ eye_color <chr>”blue”,
“yellow”, “red”, “yellow”, “… $ birth_year <dbl> 19.0, 112.0, 33.0,
41.9, 19.0, 52.0,… $ sex <chr>”male”, “none”, “none”, “male”, “fem… $
gender <chr>”masculine”, “masculine”, “masculine… $ homeworld
<chr>”Tatooine”, “Tatooine”, “Naboo”, “Ta… $ species <chr>”Human”,
“Droid”, “Droid”, “Human”, … $ films <list> \<“A New Hope”, “The Empire
Strikes … $ vehicles <list> \<”Snowspeeder”, “Imperial Speeder B… $
starships <list> \<”X-wing”, “Imperial shuttle”\>, \<\>,…
`r num_species <- starwars %>%`+ filter(!is.na(species)) %\>% +
summarise(unique_species = n_distinct(species)) %\>% +
pull(unique_species) \`\`\`r

```` r num_species ```[1] 37 ```r tallest_character <- starwars %>% filter(!is.na(height)) %>% arrange(desc(height)) %>% slice(1) ````r
tallest_character
`# A tibble: 1 × 14   name       height  mass hair_color skin_color eye_color   <chr>       <int> <dbl> <chr>      <chr>      <chr> 1 Yarael Po…    264    NA none       white      yellow # ℹ 8 more variables: birth_year <dbl>, sex <chr>, #   gender <chr>, homeworld <chr>, species <chr>, #   films <list>, vehicles <list>, starships <list>`r
tallest_character$name
\`\`\`\[1\] "Yarael Poof"
\`\`\`r
short_characters \<- starwars %\>% filter(!is.na(height) & height \< 170) %\>% select(name)
\`\`\`\`\`\`r
short_characters$name
`[1] "C-3PO"                 "R2-D2"  [3] "Leia Organa"           "Beru Whitesun Lars"  [5] "R5-D4"                 "Yoda"  [7] "Mon Mothma"            "Wicket Systri Warrick"  [9] "Nien Nunb"             "Watto" [11] "Sebulba"               "Shmi Skywalker" [13] "Ratts Tyerel"          "Dud Bolt" [15] "Gasgano"               "Ben Quadinaros" [17] "Cordé"                 "Barriss Offee" [19] "Dormé"                 "Zam Wesell" [21] "Jocasta Nu"            "R4-P17"`r
starwars_bmi \<- starwars %\>% filter(!is.na(mass) & !is.na(height))
%\>% mutate(BMI = mass / (height / 100)^2) %\>% select(name, BMI)
```` r starwars_bmi ```# A tibble: 59 × 2    name                 BMI    <chr>              <dbl>  1 Luke Skywalker      26.0  2 C-3PO               26.9  3 R2-D2               34.7  4 Darth Vader         33.3  5 Leia Organa         21.8  6 Owen Lars           37.9  7 Beru Whitesun Lars  27.5  8 R5-D4               34.0  9 Biggs Darklighter   25.1 10 Obi-Wan Kenobi      23.2 # ℹ 49 more rows # ℹ Use `print(n = ...)` to see more rows ```r elongated_characters <- starwars %>% filter(!is.na(mass) & !is.na(height)) %>% mutate(Elongation = mass / height) %>% arrange(desc(Elongation)) %>% slice(1:10) %>% select(name, Elongation) ````r
elongated_characters
`# A tibble: 10 × 2    name                  Elongation    <chr>                      <dbl>  1 Jabba Desilijic Tiure      7.76  2 Grievous                   0.736  3 IG-88                      0.7  4 Owen Lars                  0.674  5 Darth Vader                0.673  6 Jek Tono Porkins           0.611  7 Bossk                      0.595  8 Tarfful                    0.581  9 Dexter Jettster            0.515 10 Chewbacca                  0.491`r
average_age_per_species \<- starwars %\>% filter(!is.na(age) &
!is.na(species)) %\>% group_by(species) %\>% summarise(average_age =
mean(age, na.rm = TRUE)) %\>% arrange(desc(average_age))
`` Error in `filter()`: ℹ In argument: `!is.na(age) & !is.na(species)`. Caused by error: ! объект 'age' не найден Run `rlang::last_trace()` to see where the error occurred. ``r
average_age_per_species \<- starwars %\>% filter(!is.na(birth_year) &
!is.na(species)) %\>% group_by(species) %\>% summarise(average_age =
mean(birth_year, na.rm = TRUE)) %\>% arrange(desc(average_age))
\`\`\``r average_age_per_species`\# A tibble: 15 × 2 species average_age
<chr> <dbl> 1 Yoda’s species 896 2 Hutt 600 3 Wookiee 200 4 Cerean 92 5
Zabrak 54 6 Human 53.7 7 Droid 53.3 8 Trandoshan 53 9 Gungan 52 10
Mirialan 49 11 Twi’lek 48 12 Rodian 44 13 Mon Calamari 41 14 Kel Dor 22
15 Ewok 8 \`\`\`r

`r most_common_eye_color <- starwars %>% filter(!is.na(eye_color)) %>% count(eye_color) %>% arrange(desc(n)) %>% slice(1)`r
most_common_eye_color
`# A tibble: 1 × 2   eye_color     n   <chr>     <int> 1 brown        21`r

`r average_name_length_per_species <- starwars %>% filter(!is.na(name) & !is.na(species)) %>% mutate(name_length = nchar(name)) %>% group_by(species) %>% summarise(average_name_length = mean(name_length, na.rm = TRUE)) %>% arrange(desc(average_name_length))`r
average_name_length_per_species
\`\``# A tibble: 37 × 2    species   average_name_length    <chr>                   <dbl>  1 Ewok                     21  2 Hutt                     21  3 Geonosian                17  4 Besalisk                 15  5 Mirialan                 14  6 Toong                    14  7 Aleena                   12  8 Cerean                   12  9 Gungan                   11.7 10 Human                    11.3 # ℹ 27 more rows # ℹ Use`print(n
= …)\` to see more rows

## Оценка результата

В результате работы была установлена библиотека swirl, а также были
пройдены 5 подкурсов в рамках обучения “R Programming: The basics of
programming in R”

## Вывод

Были изучены базовые команды и функции языка R - работа с переменными,
векторами, файлами, циклами и NA.

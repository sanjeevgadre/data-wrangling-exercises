This is the solution to the problem set found at
<https://www.r-exercises.com/2017/06/22/data-wrangling-reshaping/>.

### 3.1

    data = airquality[4:6]
    str(data)

    ## 'data.frame':    153 obs. of  3 variables:
    ##  $ Temp : int  67 72 74 62 56 66 65 59 61 69 ...
    ##  $ Month: int  5 5 5 5 5 5 5 5 5 5 ...
    ##  $ Day  : int  1 2 3 4 5 6 7 8 9 10 ...

### 3.2

    data %>% spread(Month,Temp) %>% head()

    ##   Day  5  6  7  8  9
    ## 1   1 67 78 84 81 91
    ## 2   2 72 74 85 81 92
    ## 3   3 74 67 81 82 93
    ## 4   4 62 84 84 86 93
    ## 5   5 56 85 83 85 87
    ## 6   6 66 79 83 87 84

### 3.3

    data %>% spread(Month,Temp) %>% gather(Month,Temp, 2:6) %>% head()

    ##   Day Month Temp
    ## 1   1     5   67
    ## 2   2     5   72
    ## 3   3     5   74
    ## 4   4     5   62
    ## 5   5     5   56
    ## 6   6     5   66

### 3.4

    data %>% spread(Month,Temp) %>% gather(Month, Temp, "5","6","7","8","9") %>% head()

    ##   Day Month Temp
    ## 1   1     5   67
    ## 2   2     5   72
    ## 3   3     5   74
    ## 4   4     5   62
    ## 5   5     5   56
    ## 6   6     5   66

### 3.5

    new.data = data %>% spread(Month,Temp) %>% gather(Month, Temp, -Day)

### 3.6

    new.data %>% unite(Date, Day, Month, sep="-") %>% head()

    ##   Date Temp
    ## 1  1-5   67
    ## 2  2-5   72
    ## 3  3-5   74
    ## 4  4-5   62
    ## 5  5-5   56
    ## 6  6-5   66

### 3.7

    new.data = new.data %>% unite(Date, Day, Month, sep="-") %>% 
      separate(Date, c("Day","Month"), sep="-")

### 3.8

    new.data %>% replace_na(list(Temp = "Unknown")) %>% tail()

    ##     Day Month    Temp
    ## 150  26     9      70
    ## 151  27     9      77
    ## 152  28     9      75
    ## 153  29     9      76
    ## 154  30     9      68
    ## 155  31     9 Unknown

### 3.9

    new.data$year = rep(NA, nrow(new.data))
    new.data$year[1] = '2015'
    new.data$year[as.integer(nrow(new.data)/3)] = '2016'
    new.data$year[as.integer(2*nrow(new.data)/3)] = '2017'

    new.data = new.data %>% fill(year, .direction="down")

### 3.10

    parse_number(new.data$Temp, na="NA")

    ##   [1] 67 72 74 62 56 66 65 59 61 69 74 69 66 68 58 64 66 57 68 62 59 73 61
    ##  [24] 61 57 58 57 67 81 79 76 78 74 67 84 85 79 82 87 90 87 93 92 82 80 79
    ##  [47] 77 72 65 73 76 77 76 76 76 75 78 73 80 77 83 NA 84 85 81 84 83 83 88
    ##  [70] 92 92 89 82 73 81 91 80 81 82 84 87 85 74 81 82 86 85 82 86 88 86 83
    ##  [93] 81 81 81 82 86 85 87 89 90 90 92 86 86 82 80 79 77 79 76 78 78 77 72
    ## [116] 75 79 81 86 88 97 94 96 94 91 92 93 93 87 84 80 78 75 73 81 76 77 71
    ## [139] 71 78 67 76 68 82 64 71 81 69 63 70 77 75 76 68 NA

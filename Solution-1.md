This is the solution to the problem set found at
<https://www.r-exercises.com/2017/05/24/data-wrangling-part-1-io/>.

### 1.1

    csv_file = read_csv("./Problem-Set-1-Data/data.csv", col_names=TRUE)

    ## Warning: Missing column names filled in: 'X1' [1]

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_integer(),
    ##   preg = col_integer(),
    ##   plas = col_integer(),
    ##   pres = col_integer(),
    ##   skin = col_integer(),
    ##   test = col_integer(),
    ##   mass = col_double(),
    ##   pedi = col_double(),
    ##   age = col_integer(),
    ##   class = col_integer()
    ## )

### 1.2

    txt_file = read.table("./Problem-Set-1-Data/data.txt", header=TRUE)

### 1.3

    xls_file = read_xls("./Problem-Set-1-Data/data.xls", sheet=1, col_names=TRUE)

### 1.4

    xlsx_file = read_xlsx("./Problem-Set-1-Data/data.xlsx", sheet=1, col_names=TRUE)

### 1.5

    json_file = fromJSON(file="./Problem-Set-1-Data/data.json")
    json_file = as.data.frame(json_file)

### 1.6

    xml_file = xmlToDataFrame("./Problem-Set-1-Data/data.xml")

### 1.7

    write_csv(csv_file, "./Problem-Set-1-Data/data01.csv", append=FALSE)

    write.table(txt_file, "./Problem-Set-1-Data/data01.txt", append=FALSE)

### 1.8

    write.xlsx(xls_file, "./Problem-Set-1-Data/data01.xls")

    write.xlsx(xlsx_file, "./Problem-Set-1-Data/data01.xlsx")

### 1.9

    json_file = toJSON(json_file)
    write(json_file, "./Problem-Set-1-Data/data01.json")

### 1.10

    write.xml(xml_file, "./Problem-Set-1-Data/data01.xml")

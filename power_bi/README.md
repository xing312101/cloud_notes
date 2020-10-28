# Power BI
> https://powerbi.microsoft.com

## Download Oracle Client from Power BI dependence
https://docs.microsoft.com/zh-tw/power-bi/connect-data/desktop-connect-oracle-database

#### 32-bit:
https://www.oracle.com/database/technologies/dotnet-utilsoft-downloads.html

#### 64-bit
https://www.oracle.com/database/technologies/odac-downloads.html



## Comparing Power BI Report Server and the Power BI service
> https://docs.microsoft.com/en-us/power-bi/report-server/compare-report-server-service

## Embed
> https://docs.microsoft.com/zh-tw/power-bi/report-server/quickstart-embed

URL帶入參數: rs:embed=true
```
https://myserver/reports/powerbi/Sales?rs:embed=true

// with password
https://username:Password@myserver/reports/powerbi/Sales?rs:embed=true

<iframe width="800" height="600" src="https://myserver/reports/powerbi/Sales?rs:embed=true" frameborder="0" allowFullScreen="true"></iframe>
```

#### Tags
```
<iframe>

<object data="https://myserver/reports/powerbi/Sales?rs:embed=true"></object>

<embed src="http://win-hauseq7hanj:82/Reports/powerbi/bb?rs:embed=true" />

```


## Download for using Microsoft Cloud service
** Power BI Desktop **
> https://powerbi.microsoft.com/zh-tw/desktop/

## Downloads for Power BI Report Server
1, POWER BI Report Server

2, POWER BI Desktop for report Server
> https://www.microsoft.com/en-us/download/details.aspx?id=56722

3, SQL server 2019，developer version
> https://www.microsoft.com/zh-tw/sql-server/sql-server-downloads

4, SSMS - DB management Tool (option)
> https://docs.microsoft.com/zh-tw/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver15


## Switch Import-data to directQuery
> https://xxlbi.com/blog/switching-from-imported-data-to-directquery-or-live-connection-in-power-bi/

## Go to detail when click a bar in chart
> https://docs.microsoft.com/en-us/power-bi/create-reports/desktop-see-data-see-records

## DAX
> https://medium.com/mastertalks-tw/%E4%BD%BF%E7%94%A8-power-bi-%E4%B8%80%E5%AE%9A%E8%A6%81%E6%87%82%E5%BE%97-dax-%E5%87%BD%E6%95%B8-%E7%9C%8B%E5%AE%8C%E9%80%99%E7%AF%87%E7%AB%8B%E5%8D%B3%E4%B8%8A%E6%89%8B-1206283eed6f


## Like VLOOKUP in power bi
### 1, RELATED
> https://community.powerbi.com/t5/Community-Blog/Good-Ol-VLOOKUP-The-Ultimate-Guide-to-Lookups-in-Power-BI/ba-p/35912

### 2, LOOKUPVALUE
> https://docs.microsoft.com/en-us/dax/lookupvalue-function-dax

> https://exceltown.com/en/tutorials/power-bi/powerbi-com-and-power-bi-desktop/dax-query-language-for-power-bi-and-power-pivot/lookupvalue-assigning-of-values-from-other-table-dax-power-pivot-power-bi/

```
LOOKUPVALUE(
    <result_columnName>,
    <search_columnName>,
    <search_value>
    [, <search2_columnName>, <search2_value>]…
    [, <alternateResult>]
)
```

```
[Region] = LOOKUPVALUE(Employee[Region], Employee[Email], USERNAME(), BLANK())

Product = LOOKUPVALUE('Product'[Product], Sales[ProductKey], 'Product'[ProductKey])

Product = RELATED('Product'[Product])
```


## 3, ROLLING 12 MONTH
> DEFAULT VALUE ALSO USING CALCULATE

```
VALUE_1 =
CALCULATE (
    SUMX (
        TableName,
        TableName[Column Name]
    )
)

ROLLING_12_MONTH =
CALCULATE(
    [VALUE_1],
    FILTER (
        ALL(Dates),
        AND (
            Dates[Date] <= MAX( Dates[Date] ),
            DATEADD (
                Dates[Date],
                1,
                YEAR
            )  > MAX ( Dates[Date] )
        )
    )
)
```

## 4, CONVERT IMPORT MODE TO DIRECT QUERY
> https://datacaffee.com/convert-import-mode-to-direct-query-in-power-bi/


## 5, Dynamic Top N











In this project, I aim to extract historical stock price data from the internet, specifically focusing on the S&P 500 (Standard & Poor's 500) using Python. The methodology employed for this task involves leveraging the yfinance library, a powerful tool for fetching financial data. The S&P 500, a renowned stock market index, serves as the primary source, monitoring and reflecting the performance of 500 major publicly traded companies in the United States. Recognized globally, it holds a prominent status as one of the most extensively observed and closely monitored equity indices. Due to its comprehensive representation of diverse sectors, the S&P 500 is considered a reliable gauge, offering insights into the overall health and dynamics of the American economy. Throughout this project, the objective is to effectively retrieve and analyze S&P historic stock price data, contributing to a comprehensive understanding of market trends and economic indicators.The main objective of this project is to extract the Adjusted Closing price, denoted as "Adj Close," for all the companies listed here using with their respective ticker symbol and exporting the data in to  Csv file for further analysis.

```python
# Install the yfinance library 
! pip install yfinance

```

    Requirement already satisfied: yfinance in c:\users\user\anaconda3\lib\site-packages (0.2.36)
    Requirement already satisfied: pandas>=1.3.0 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (2.0.3)
    Requirement already satisfied: numpy>=1.16.5 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (1.24.3)
    Requirement already satisfied: requests>=2.31 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (2.31.0)
    Requirement already satisfied: multitasking>=0.0.7 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (0.0.11)
    Requirement already satisfied: lxml>=4.9.1 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (4.9.3)
    Requirement already satisfied: appdirs>=1.4.4 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (1.4.4)
    Requirement already satisfied: pytz>=2022.5 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (2023.3.post1)
    Requirement already satisfied: frozendict>=2.3.4 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (2.4.0)
    Requirement already satisfied: peewee>=3.16.2 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (3.17.1)
    Requirement already satisfied: beautifulsoup4>=4.11.1 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (4.12.2)
    Requirement already satisfied: html5lib>=1.1 in c:\users\user\anaconda3\lib\site-packages (from yfinance) (1.1)
    Requirement already satisfied: soupsieve>1.2 in c:\users\user\anaconda3\lib\site-packages (from beautifulsoup4>=4.11.1->yfinance) (2.4)
    Requirement already satisfied: six>=1.9 in c:\users\user\anaconda3\lib\site-packages (from html5lib>=1.1->yfinance) (1.16.0)
    Requirement already satisfied: webencodings in c:\users\user\anaconda3\lib\site-packages (from html5lib>=1.1->yfinance) (0.5.1)
    Requirement already satisfied: python-dateutil>=2.8.2 in c:\users\user\anaconda3\lib\site-packages (from pandas>=1.3.0->yfinance) (2.8.2)
    Requirement already satisfied: tzdata>=2022.1 in c:\users\user\anaconda3\lib\site-packages (from pandas>=1.3.0->yfinance) (2023.3)
    Requirement already satisfied: charset-normalizer<4,>=2 in c:\users\user\anaconda3\lib\site-packages (from requests>=2.31->yfinance) (2.0.4)
    Requirement already satisfied: idna<4,>=2.5 in c:\users\user\anaconda3\lib\site-packages (from requests>=2.31->yfinance) (3.4)
    Requirement already satisfied: urllib3<3,>=1.21.1 in c:\users\user\anaconda3\lib\site-packages (from requests>=2.31->yfinance) (1.26.16)
    Requirement already satisfied: certifi>=2017.4.17 in c:\users\user\anaconda3\lib\site-packages (from requests>=2.31->yfinance) (2023.11.17)
    


```python
# Importing the Libraries required for the project
import pandas as pd
import yfinance as yf
```
Retrieve the initial S&P table from Wikipedia, which serves as an excellent source for data scraping. The Wikipedia project's open-source nature eliminates many restrictions present on other websites, making it an ideal platform for extracting information. my goal is to acquire the most up-to-date roster of companies in the S&P, including their respective tickers, by leveraging the wealth of data available on Wikipedia.

```python
# Geting the page from wikipedia and assign it to the ulr 
url = 'https://en.wikipedia.org/wiki/List_of_S%26P_500_companies'

# read url to pandas dataframe  "data"
data = pd.read_html(url)
```


```python
data
```




    [    Symbol              Security             GICS Sector  \
     0      MMM                    3M             Industrials   
     1      AOS           A. O. Smith             Industrials   
     2      ABT                Abbott             Health Care   
     3     ABBV                AbbVie             Health Care   
     4      ACN             Accenture  Information Technology   
     ..     ...                   ...                     ...   
     498    YUM           Yum! Brands  Consumer Discretionary   
     499   ZBRA    Zebra Technologies  Information Technology   
     500    ZBH         Zimmer Biomet             Health Care   
     501   ZION  Zions Bancorporation              Financials   
     502    ZTS                Zoetis             Health Care   
     
                           GICS Sub-Industry    Headquarters Location  Date added  \
     0              Industrial Conglomerates    Saint Paul, Minnesota  1957-03-04   
     1                     Building Products     Milwaukee, Wisconsin  2017-07-26   
     2                 Health Care Equipment  North Chicago, Illinois  1957-03-04   
     3                         Biotechnology  North Chicago, Illinois  2012-12-31   
     4        IT Consulting & Other Services          Dublin, Ireland  2011-07-06   
     ..                                  ...                      ...         ...   
     498                         Restaurants     Louisville, Kentucky  1997-10-06   
     499  Electronic Equipment & Instruments   Lincolnshire, Illinois  2019-12-23   
     500               Health Care Equipment          Warsaw, Indiana  2001-08-07   
     501                      Regional Banks     Salt Lake City, Utah  2001-06-22   
     502                     Pharmaceuticals   Parsippany, New Jersey  2013-06-21   
     
              CIK      Founded  
     0      66740         1902  
     1      91142         1916  
     2       1800         1888  
     3    1551152  2013 (1888)  
     4    1467373         1989  
     ..       ...          ...  
     498  1041061         1997  
     499   877212         1969  
     500  1136869         1927  
     501   109380         1873  
     502  1555280         1952  
     
     [503 rows x 8 columns],
                       Date  Added                                Removed  \
                       Date Ticker                       Security  Ticker   
     0    December 18, 2023   UBER                           Uber     SEE   
     1    December 18, 2023    JBL                          Jabil     ALK   
     2    December 18, 2023   BLDR           Builders FirstSource    SEDG   
     3     October 18, 2023   HUBB                        Hubbell     OGN   
     4     October 18, 2023   LULU            Lululemon Athletica    ATVI   
     ..                 ...    ...                            ...     ...   
     333       June 9, 1999    WLP                      Wellpoint     HPH   
     334  December 11, 1998    FSR                        Firstar     LDW   
     335  December 11, 1998    CCL                 Carnival Corp.     GRN   
     336  December 11, 1998   CPWR                      Compuware     SUN   
     337      June 17, 1997    CCI  Countrywide Credit Industries     USL   
     
                                    \
                          Security   
     0                  Sealed Air   
     1            Alaska Air Group   
     2                   SolarEdge   
     3               Organon & Co.   
     4         Activision Blizzard   
     ..                        ...   
     333  Harnischfeger Industries   
     334                     Amoco   
     335                General Re   
     336                SunAmerica   
     337                    USLife   
     
                                                     Reason  
                                                     Reason  
     0                     Market capitalization change.[4]  
     1                     Market capitalization change.[4]  
     2                     Market capitalization change.[4]  
     3                     Market capitalization change.[5]  
     4    S&P 500 and S&P 100 constituent Microsoft acqu...  
     ..                                                 ...  
     333           Harnischfeger filed for bankruptcy.[252]  
     334                           BP purchased Amoco.[253]  
     335      Berkshire Hathaway purchased General Re.[253]  
     336                     AIG purchased SunAmerica.[253]  
     337                          AIG acquired USLife.[254]  
     
     [338 rows x 6 columns]]




```python
# Checking the number of tables that are returned
len(data)
```




    2




```python
# Usng the index "0" to filter the 1st table.
data[0]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>Security</th>
      <th>GICS Sector</th>
      <th>GICS Sub-Industry</th>
      <th>Headquarters Location</th>
      <th>Date added</th>
      <th>CIK</th>
      <th>Founded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MMM</td>
      <td>3M</td>
      <td>Industrials</td>
      <td>Industrial Conglomerates</td>
      <td>Saint Paul, Minnesota</td>
      <td>1957-03-04</td>
      <td>66740</td>
      <td>1902</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AOS</td>
      <td>A. O. Smith</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>Milwaukee, Wisconsin</td>
      <td>2017-07-26</td>
      <td>91142</td>
      <td>1916</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABT</td>
      <td>Abbott</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>North Chicago, Illinois</td>
      <td>1957-03-04</td>
      <td>1800</td>
      <td>1888</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABBV</td>
      <td>AbbVie</td>
      <td>Health Care</td>
      <td>Biotechnology</td>
      <td>North Chicago, Illinois</td>
      <td>2012-12-31</td>
      <td>1551152</td>
      <td>2013 (1888)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ACN</td>
      <td>Accenture</td>
      <td>Information Technology</td>
      <td>IT Consulting &amp; Other Services</td>
      <td>Dublin, Ireland</td>
      <td>2011-07-06</td>
      <td>1467373</td>
      <td>1989</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>498</th>
      <td>YUM</td>
      <td>Yum! Brands</td>
      <td>Consumer Discretionary</td>
      <td>Restaurants</td>
      <td>Louisville, Kentucky</td>
      <td>1997-10-06</td>
      <td>1041061</td>
      <td>1997</td>
    </tr>
    <tr>
      <th>499</th>
      <td>ZBRA</td>
      <td>Zebra Technologies</td>
      <td>Information Technology</td>
      <td>Electronic Equipment &amp; Instruments</td>
      <td>Lincolnshire, Illinois</td>
      <td>2019-12-23</td>
      <td>877212</td>
      <td>1969</td>
    </tr>
    <tr>
      <th>500</th>
      <td>ZBH</td>
      <td>Zimmer Biomet</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Warsaw, Indiana</td>
      <td>2001-08-07</td>
      <td>1136869</td>
      <td>1927</td>
    </tr>
    <tr>
      <th>501</th>
      <td>ZION</td>
      <td>Zions Bancorporation</td>
      <td>Financials</td>
      <td>Regional Banks</td>
      <td>Salt Lake City, Utah</td>
      <td>2001-06-22</td>
      <td>109380</td>
      <td>1873</td>
    </tr>
    <tr>
      <th>502</th>
      <td>ZTS</td>
      <td>Zoetis</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>Parsippany, New Jersey</td>
      <td>2013-06-21</td>
      <td>1555280</td>
      <td>1952</td>
    </tr>
  </tbody>
</table>
<p>503 rows × 8 columns</p>
</div>




```python
# Usng the index "1" to filter the 2nd table.
data[1]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>Date</th>
      <th colspan="2" halign="left">Added</th>
      <th colspan="2" halign="left">Removed</th>
      <th>Reason</th>
    </tr>
    <tr>
      <th></th>
      <th>Date</th>
      <th>Ticker</th>
      <th>Security</th>
      <th>Ticker</th>
      <th>Security</th>
      <th>Reason</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>December 18, 2023</td>
      <td>UBER</td>
      <td>Uber</td>
      <td>SEE</td>
      <td>Sealed Air</td>
      <td>Market capitalization change.[4]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>December 18, 2023</td>
      <td>JBL</td>
      <td>Jabil</td>
      <td>ALK</td>
      <td>Alaska Air Group</td>
      <td>Market capitalization change.[4]</td>
    </tr>
    <tr>
      <th>2</th>
      <td>December 18, 2023</td>
      <td>BLDR</td>
      <td>Builders FirstSource</td>
      <td>SEDG</td>
      <td>SolarEdge</td>
      <td>Market capitalization change.[4]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>October 18, 2023</td>
      <td>HUBB</td>
      <td>Hubbell</td>
      <td>OGN</td>
      <td>Organon &amp; Co.</td>
      <td>Market capitalization change.[5]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>October 18, 2023</td>
      <td>LULU</td>
      <td>Lululemon Athletica</td>
      <td>ATVI</td>
      <td>Activision Blizzard</td>
      <td>S&amp;P 500 and S&amp;P 100 constituent Microsoft acqu...</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>333</th>
      <td>June 9, 1999</td>
      <td>WLP</td>
      <td>Wellpoint</td>
      <td>HPH</td>
      <td>Harnischfeger Industries</td>
      <td>Harnischfeger filed for bankruptcy.[252]</td>
    </tr>
    <tr>
      <th>334</th>
      <td>December 11, 1998</td>
      <td>FSR</td>
      <td>Firstar</td>
      <td>LDW</td>
      <td>Amoco</td>
      <td>BP purchased Amoco.[253]</td>
    </tr>
    <tr>
      <th>335</th>
      <td>December 11, 1998</td>
      <td>CCL</td>
      <td>Carnival Corp.</td>
      <td>GRN</td>
      <td>General Re</td>
      <td>Berkshire Hathaway purchased General Re.[253]</td>
    </tr>
    <tr>
      <th>336</th>
      <td>December 11, 1998</td>
      <td>CPWR</td>
      <td>Compuware</td>
      <td>SUN</td>
      <td>SunAmerica</td>
      <td>AIG purchased SunAmerica.[253]</td>
    </tr>
    <tr>
      <th>337</th>
      <td>June 17, 1997</td>
      <td>CCI</td>
      <td>Countrywide Credit Industries</td>
      <td>USL</td>
      <td>USLife</td>
      <td>AIG acquired USLife.[254]</td>
    </tr>
  </tbody>
</table>
<p>338 rows × 6 columns</p>
</div>


Retrieve Ticker Symbols
Ticker symbols serve as distinct identifiers for individual stocks. These symbols play a crucial role in pinpointing the specific stocks included in the S&P index, particularly when my goal is to obtain historical price data from Yahoo Finance. To accomplish this, I will compile a comprehensive list of ticker objects, allowing me to efficiently extract the relevant information. This process involves organizing the tickers in a manner that facilitates seamless retrieval of historical stock prices from the specified financial platform. The extraction will only be based on the first table

```python
# Creating a list fronm the data  that contains all the ticker symbols in the S&P 500
tickers = data[0]["Symbol"].tolist()
tickers
```




    ['MMM',
     'AOS',
     'ABT',
     'ABBV',
     'ACN',
     'ADBE',
     'AMD',
     'AES',
     'AFL',
     'A',
     'APD',
     'ABNB',
     'AKAM',
     'ALB',
     'ARE',
     'ALGN',
     'ALLE',
     'LNT',
     'ALL',
     'GOOGL',
     'GOOG',
     'MO',
     'AMZN',
     'AMCR',
     'AEE',
     'AAL',
     'AEP',
     'AXP',
     'AIG',
     'AMT',
     'AWK',
     'AMP',
     'AME',
     'AMGN',
     'APH',
     'ADI',
     'ANSS',
     'AON',
     'APA',
     'AAPL',
     'AMAT',
     'APTV',
     'ACGL',
     'ADM',
     'ANET',
     'AJG',
     'AIZ',
     'T',
     'ATO',
     'ADSK',
     'ADP',
     'AZO',
     'AVB',
     'AVY',
     'AXON',
     'BKR',
     'BALL',
     'BAC',
     'BK',
     'BBWI',
     'BAX',
     'BDX',
     'BRK.B',
     'BBY',
     'BIO',
     'TECH',
     'BIIB',
     'BLK',
     'BX',
     'BA',
     'BKNG',
     'BWA',
     'BXP',
     'BSX',
     'BMY',
     'AVGO',
     'BR',
     'BRO',
     'BF.B',
     'BLDR',
     'BG',
     'CDNS',
     'CZR',
     'CPT',
     'CPB',
     'COF',
     'CAH',
     'KMX',
     'CCL',
     'CARR',
     'CTLT',
     'CAT',
     'CBOE',
     'CBRE',
     'CDW',
     'CE',
     'COR',
     'CNC',
     'CNP',
     'CF',
     'CHRW',
     'CRL',
     'SCHW',
     'CHTR',
     'CVX',
     'CMG',
     'CB',
     'CHD',
     'CI',
     'CINF',
     'CTAS',
     'CSCO',
     'C',
     'CFG',
     'CLX',
     'CME',
     'CMS',
     'KO',
     'CTSH',
     'CL',
     'CMCSA',
     'CMA',
     'CAG',
     'COP',
     'ED',
     'STZ',
     'CEG',
     'COO',
     'CPRT',
     'GLW',
     'CTVA',
     'CSGP',
     'COST',
     'CTRA',
     'CCI',
     'CSX',
     'CMI',
     'CVS',
     'DHR',
     'DRI',
     'DVA',
     'DAY',
     'DE',
     'DAL',
     'XRAY',
     'DVN',
     'DXCM',
     'FANG',
     'DLR',
     'DFS',
     'DG',
     'DLTR',
     'D',
     'DPZ',
     'DOV',
     'DOW',
     'DHI',
     'DTE',
     'DUK',
     'DD',
     'EMN',
     'ETN',
     'EBAY',
     'ECL',
     'EIX',
     'EW',
     'EA',
     'ELV',
     'LLY',
     'EMR',
     'ENPH',
     'ETR',
     'EOG',
     'EPAM',
     'EQT',
     'EFX',
     'EQIX',
     'EQR',
     'ESS',
     'EL',
     'ETSY',
     'EG',
     'EVRG',
     'ES',
     'EXC',
     'EXPE',
     'EXPD',
     'EXR',
     'XOM',
     'FFIV',
     'FDS',
     'FICO',
     'FAST',
     'FRT',
     'FDX',
     'FIS',
     'FITB',
     'FSLR',
     'FE',
     'FI',
     'FLT',
     'FMC',
     'F',
     'FTNT',
     'FTV',
     'FOXA',
     'FOX',
     'BEN',
     'FCX',
     'GRMN',
     'IT',
     'GEHC',
     'GEN',
     'GNRC',
     'GD',
     'GE',
     'GIS',
     'GM',
     'GPC',
     'GILD',
     'GPN',
     'GL',
     'GS',
     'HAL',
     'HIG',
     'HAS',
     'HCA',
     'PEAK',
     'HSIC',
     'HSY',
     'HES',
     'HPE',
     'HLT',
     'HOLX',
     'HD',
     'HON',
     'HRL',
     'HST',
     'HWM',
     'HPQ',
     'HUBB',
     'HUM',
     'HBAN',
     'HII',
     'IBM',
     'IEX',
     'IDXX',
     'ITW',
     'ILMN',
     'INCY',
     'IR',
     'PODD',
     'INTC',
     'ICE',
     'IFF',
     'IP',
     'IPG',
     'INTU',
     'ISRG',
     'IVZ',
     'INVH',
     'IQV',
     'IRM',
     'JBHT',
     'JBL',
     'JKHY',
     'J',
     'JNJ',
     'JCI',
     'JPM',
     'JNPR',
     'K',
     'KVUE',
     'KDP',
     'KEY',
     'KEYS',
     'KMB',
     'KIM',
     'KMI',
     'KLAC',
     'KHC',
     'KR',
     'LHX',
     'LH',
     'LRCX',
     'LW',
     'LVS',
     'LDOS',
     'LEN',
     'LIN',
     'LYV',
     'LKQ',
     'LMT',
     'L',
     'LOW',
     'LULU',
     'LYB',
     'MTB',
     'MRO',
     'MPC',
     'MKTX',
     'MAR',
     'MMC',
     'MLM',
     'MAS',
     'MA',
     'MTCH',
     'MKC',
     'MCD',
     'MCK',
     'MDT',
     'MRK',
     'META',
     'MET',
     'MTD',
     'MGM',
     'MCHP',
     'MU',
     'MSFT',
     'MAA',
     'MRNA',
     'MHK',
     'MOH',
     'TAP',
     'MDLZ',
     'MPWR',
     'MNST',
     'MCO',
     'MS',
     'MOS',
     'MSI',
     'MSCI',
     'NDAQ',
     'NTAP',
     'NFLX',
     'NEM',
     'NWSA',
     'NWS',
     'NEE',
     'NKE',
     'NI',
     'NDSN',
     'NSC',
     'NTRS',
     'NOC',
     'NCLH',
     'NRG',
     'NUE',
     'NVDA',
     'NVR',
     'NXPI',
     'ORLY',
     'OXY',
     'ODFL',
     'OMC',
     'ON',
     'OKE',
     'ORCL',
     'OTIS',
     'PCAR',
     'PKG',
     'PANW',
     'PARA',
     'PH',
     'PAYX',
     'PAYC',
     'PYPL',
     'PNR',
     'PEP',
     'PFE',
     'PCG',
     'PM',
     'PSX',
     'PNW',
     'PXD',
     'PNC',
     'POOL',
     'PPG',
     'PPL',
     'PFG',
     'PG',
     'PGR',
     'PLD',
     'PRU',
     'PEG',
     'PTC',
     'PSA',
     'PHM',
     'QRVO',
     'PWR',
     'QCOM',
     'DGX',
     'RL',
     'RJF',
     'RTX',
     'O',
     'REG',
     'REGN',
     'RF',
     'RSG',
     'RMD',
     'RVTY',
     'RHI',
     'ROK',
     'ROL',
     'ROP',
     'ROST',
     'RCL',
     'SPGI',
     'CRM',
     'SBAC',
     'SLB',
     'STX',
     'SRE',
     'NOW',
     'SHW',
     'SPG',
     'SWKS',
     'SJM',
     'SNA',
     'SO',
     'LUV',
     'SWK',
     'SBUX',
     'STT',
     'STLD',
     'STE',
     'SYK',
     'SYF',
     'SNPS',
     'SYY',
     'TMUS',
     'TROW',
     'TTWO',
     'TPR',
     'TRGP',
     'TGT',
     'TEL',
     'TDY',
     'TFX',
     'TER',
     'TSLA',
     'TXN',
     'TXT',
     'TMO',
     'TJX',
     'TSCO',
     'TT',
     'TDG',
     'TRV',
     'TRMB',
     'TFC',
     'TYL',
     'TSN',
     'USB',
     'UBER',
     'UDR',
     'ULTA',
     'UNP',
     'UAL',
     'UPS',
     'URI',
     'UNH',
     'UHS',
     'VLO',
     'VTR',
     'VLTO',
     'VRSN',
     'VRSK',
     'VZ',
     'VRTX',
     'VFC',
     'VTRS',
     'VICI',
     'V',
     'VMC',
     'WRB',
     'WAB',
     'WBA',
     'WMT',
     'DIS',
     'WBD',
     'WM',
     'WAT',
     'WEC',
     'WFC',
     'WELL',
     'WST',
     'WDC',
     'WRK',
     'WY',
     'WHR',
     'WMB',
     'WTW',
     'GWW',
     'WYNN',
     'XEL',
     'XYL',
     'YUM',
     'ZBRA',
     'ZBH',
     'ZION',
     'ZTS']




```python
# Checking the len of the ticker list to confirm that it is at least 500 objects long
len(tickers)
```




    503


## Downloading Data Using the Yfinance Library.

To retrieve data from Yahoo Finance using the yfinance library, I will initiate the download process by invoking the library and specifying the required parameters that define the dataset i intend to fetch. For this excercise, I will focus on obtaining data related to Tesla identified by its ticker symbol TSLA. In this particular instance, the data retrieval period will be set to commence from June 14, 2022, and conclude on June 18, 2022. 



```python

```


```python
# Download data from yahoo finance using the yf library
yf.download ("TSLA", start = "2022-6-14", end = "2022-6-18" )
```

    [*********************100%%**********************]  1 of 1 completed
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Adj Close</th>
      <th>Volume</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2022-06-14</th>
      <td>218.286667</td>
      <td>226.330002</td>
      <td>211.736664</td>
      <td>220.889999</td>
      <td>220.889999</td>
      <td>97988700</td>
    </tr>
    <tr>
      <th>2022-06-15</th>
      <td>220.916672</td>
      <td>235.663330</td>
      <td>218.149994</td>
      <td>233.000000</td>
      <td>233.000000</td>
      <td>119131800</td>
    </tr>
    <tr>
      <th>2022-06-16</th>
      <td>222.736664</td>
      <td>225.166672</td>
      <td>208.693329</td>
      <td>213.100006</td>
      <td>213.100006</td>
      <td>107390700</td>
    </tr>
    <tr>
      <th>2022-06-17</th>
      <td>213.433334</td>
      <td>220.970001</td>
      <td>213.196671</td>
      <td>216.759995</td>
      <td>216.759995</td>
      <td>92641800</td>
    </tr>
  </tbody>
</table>
</div>




The extracted data pertains to comprehensive stock information for TSLA, encompassing various parameters such as the opening price, highest price, lowest price, closing price, and Adjusted Closing price, all organized in a table. However, given the specific focus of this project, I find that the wealth of information provided exceeds my current needs. My primary interest lies in tracking the Adjusted Closing price, as it serves as a key metric for understanding the longitudinal movement of stock prices over an extended period. Therefore, for the broader dataset required, I will exclusively extract the Adjusted Closing price, denoted as "Adj Close," for all the companies listed here using with their respective ticker symbol streamlining my data collection to align with the project's objectives.






```python
# pulling the adjusted closing price data for all of the stocks, using the ticker list for 2 days and assign the it to adj_prices
adj_prices = yf.download (tickers, start = "2022-6-14", end = "2022-6-18" )["Adj Close"]
```

    [*********************100%%**********************]  503 of 503 completed
    
    5 Failed downloads:
    ['VLTO', 'GEHC', 'KVUE']: Exception("%ticker%: Data doesn't exist for startDate = 1655179200, endDate = 1655524800")
    ['BF.B']: Exception('%ticker%: No price data found, symbol may be delisted (1d 2022-6-14 -> 2022-6-18)')
    ['BRK.B']: Exception('%ticker%: No timezone found, symbol may be delisted')
    
FAILED DOWNLOAD

5 Failed downloads:
['VLTO', 'GEHC', 'KVUE']: Exception("%ticker%: Data doesn't exist for startDate = 1655179200, endDate = 1655524800")
['BF.B']: Exception('%ticker%: No price data found, symbol may be delisted (1d 2022-6-14 -> 2022-6-18)')
['BRK.B']: Exception('%ticker%: No timezone found, symbol may be delisted')

```python
adj_prices
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Ticker</th>
      <th>A</th>
      <th>AAL</th>
      <th>AAPL</th>
      <th>ABBV</th>
      <th>ABNB</th>
      <th>ABT</th>
      <th>ACGL</th>
      <th>ACN</th>
      <th>ADBE</th>
      <th>ADI</th>
      <th>...</th>
      <th>WYNN</th>
      <th>XEL</th>
      <th>XOM</th>
      <th>XRAY</th>
      <th>XYL</th>
      <th>YUM</th>
      <th>ZBH</th>
      <th>ZBRA</th>
      <th>ZION</th>
      <th>ZTS</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2022-06-14</th>
      <td>114.599976</td>
      <td>12.95</td>
      <td>131.452835</td>
      <td>128.502655</td>
      <td>98.870003</td>
      <td>99.521851</td>
      <td>44.549999</td>
      <td>267.685211</td>
      <td>370.820007</td>
      <td>143.091003</td>
      <td>...</td>
      <td>57.422058</td>
      <td>62.855083</td>
      <td>90.457390</td>
      <td>34.638973</td>
      <td>74.851028</td>
      <td>106.641464</td>
      <td>103.794312</td>
      <td>300.739990</td>
      <td>48.103584</td>
      <td>155.403702</td>
    </tr>
    <tr>
      <th>2022-06-15</th>
      <td>115.054390</td>
      <td>13.31</td>
      <td>134.096573</td>
      <td>128.941513</td>
      <td>101.470001</td>
      <td>101.320091</td>
      <td>43.990002</td>
      <td>273.591187</td>
      <td>376.920013</td>
      <td>145.920334</td>
      <td>...</td>
      <td>58.738579</td>
      <td>62.826458</td>
      <td>89.318451</td>
      <td>34.415112</td>
      <td>74.802109</td>
      <td>108.257095</td>
      <td>105.470497</td>
      <td>308.359985</td>
      <td>49.310356</td>
      <td>155.669601</td>
    </tr>
    <tr>
      <th>2022-06-16</th>
      <td>113.562752</td>
      <td>12.16</td>
      <td>128.779434</td>
      <td>129.931290</td>
      <td>93.260002</td>
      <td>98.680733</td>
      <td>42.230000</td>
      <td>263.579224</td>
      <td>365.079987</td>
      <td>139.483841</td>
      <td>...</td>
      <td>53.937733</td>
      <td>61.967777</td>
      <td>86.023949</td>
      <td>33.811684</td>
      <td>71.494949</td>
      <td>105.586945</td>
      <td>101.792778</td>
      <td>292.119995</td>
      <td>47.982918</td>
      <td>154.999924</td>
    </tr>
    <tr>
      <th>2022-06-17</th>
      <td>111.340073</td>
      <td>12.94</td>
      <td>130.264664</td>
      <td>129.118927</td>
      <td>99.489998</td>
      <td>99.125458</td>
      <td>43.400002</td>
      <td>267.938171</td>
      <td>360.790009</td>
      <td>140.621399</td>
      <td>...</td>
      <td>54.402973</td>
      <td>60.975533</td>
      <td>81.063393</td>
      <td>34.385921</td>
      <td>71.338402</td>
      <td>105.935226</td>
      <td>101.211052</td>
      <td>288.459991</td>
      <td>48.512035</td>
      <td>156.418076</td>
    </tr>
  </tbody>
</table>
<p>4 rows × 503 columns</p>
</div>




```python
# Using the isna method to confirm that the failed stocks are indeed without data
adj_prices.isna().any()
```




    Ticker
    A       False
    AAL     False
    AAPL    False
    ABBV    False
    ABNB    False
            ...  
    YUM     False
    ZBH     False
    ZBRA    False
    ZION    False
    ZTS     False
    Length: 503, dtype: bool




```python
# Filtering for the stocks that have null values
adj_prices.loc[:, adj_prices.isna().any()]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Ticker</th>
      <th>BF.B</th>
      <th>BRK.B</th>
      <th>GEHC</th>
      <th>KVUE</th>
      <th>VLTO</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2022-06-14</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2022-06-15</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2022-06-16</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2022-06-17</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>


Downloading information may be unsuccessful for various reasons. In this case, the attempt to retrieve data for the first stock, represented by the ticker GEHC, failed because there was no available information for the specified time. Additionally, the second and third stocks, represented by the tickers BRK.B and BF.B, were unable to be downloaded due to discrepancies in the ticker symbols.

Upon investigation, I discovered that the stocks had different ticker symbols in Wikipedia compared to the symbols recorded for the same stocks on Yahoo Finance. The disparity arose from the use of a full stop instead of a hyphen in the Wikipedia ticker symbols. This inconsistency prevented the proper mapping of the tickers on the list to their corresponding stocks.

To address this issue, I need to update the ticker list with the information from Yahoo Finance.

```python
# Testing to confirm that  the ticker from yahoo finance works as it should
yf.download("BF-B")["Adj Close"]
```

    [*********************100%%**********************]  1 of 1 completed
    




    Date
    1980-03-17     0.196182
    1980-03-18     0.196182
    1980-03-19     0.198807
    1980-03-20     0.199463
    1980-03-21     0.196838
                    ...    
    2024-02-16    57.869999
    2024-02-20    58.509998
    2024-02-21    58.570000
    2024-02-22    57.820000
    2024-02-23    57.490002
    Name: Adj Close, Length: 11078, dtype: float64




```python
yf.download("BRK-B")["Adj Close"]
```

    [*********************100%%**********************]  1 of 1 completed
    




    Date
    1996-05-09     23.200001
    1996-05-10     24.000000
    1996-05-13     23.900000
    1996-05-14     23.600000
    1996-05-15     23.200001
                     ...    
    2024-02-16    405.989990
    2024-02-20    407.149994
    2024-02-21    409.250000
    2024-02-22    415.160004
    2024-02-23    417.220001
    Name: Adj Close, Length: 6995, dtype: float64




```python
yf.download("GEHC")["Adj Close"]
```

    [*********************100%%**********************]  1 of 1 completed
    




    Date
    2022-12-15    59.904152
    2022-12-16    56.649361
    2022-12-19    56.409740
    2022-12-20    57.118603
    2022-12-21    56.869003
                    ...    
    2024-02-16    86.019997
    2024-02-20    86.389999
    2024-02-21    84.980003
    2024-02-22    87.639999
    2024-02-23    89.070000
    Name: Adj Close, Length: 298, dtype: float64


It can be noted that the pricing data for GEHC is available only from December 15, 2022. However, my initial request encompasses a date range preceding this. As the required data is not present, I will be compelled to exclude that specific stock. Nevertheless, I will rectify any incorrect tickers in the list with the accurate ones to ensure the retrieval of data.

```python
#This loop iterates through the tickers list and updates the tickers with the correct symbol
ticker_mapping = {'BRK.B': 'BRK-B', 'BF.B': 'BF-B'}

for i in range(len(tickers)):
    tickers[i] = ticker_mapping.get(tickers[i], tickers[i])

```


```python
#Confirming to see that the correct tickers are in the tickers list
'BF-B' in tickers
```




    True




```python
'BRK-B' in tickers
```




    True




```python
#Confirming to see that the wrong tickers are off the tickers list
'BF.B' in tickers
```




    False




```python
'BRK.B' in tickers
```




    False




```python
# removing the GEHC stock from the list
tickers.remove("GEHC")
```


```python
#Downloading the final stock data
adj_prices_new = yf.download (tickers, start = "2017-1-1", end = "2023-1-1" )["Adj Close"]
```

    [*********************100%%**********************]  502 of 502 completed
    
    2 Failed downloads:
    ['VLTO', 'KVUE']: Exception("%ticker%: Data doesn't exist for startDate = 1483246800, endDate = 1672549200")
    


```python
adj_prices_new
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Ticker</th>
      <th>A</th>
      <th>AAL</th>
      <th>AAPL</th>
      <th>ABBV</th>
      <th>ABNB</th>
      <th>ABT</th>
      <th>ACGL</th>
      <th>ACN</th>
      <th>ADBE</th>
      <th>ADI</th>
      <th>...</th>
      <th>WYNN</th>
      <th>XEL</th>
      <th>XOM</th>
      <th>XRAY</th>
      <th>XYL</th>
      <th>YUM</th>
      <th>ZBH</th>
      <th>ZBRA</th>
      <th>ZION</th>
      <th>ZTS</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2017-01-03</th>
      <td>44.047394</td>
      <td>44.741226</td>
      <td>26.989264</td>
      <td>45.449177</td>
      <td>NaN</td>
      <td>34.296661</td>
      <td>28.629999</td>
      <td>104.167412</td>
      <td>103.480003</td>
      <td>63.237148</td>
      <td>...</td>
      <td>80.211411</td>
      <td>33.062614</td>
      <td>64.500008</td>
      <td>54.809013</td>
      <td>45.438725</td>
      <td>55.535847</td>
      <td>95.016678</td>
      <td>86.250000</td>
      <td>35.140808</td>
      <td>51.009773</td>
    </tr>
    <tr>
      <th>2017-01-04</th>
      <td>44.625340</td>
      <td>45.127758</td>
      <td>26.959059</td>
      <td>46.090031</td>
      <td>NaN</td>
      <td>34.568928</td>
      <td>28.833332</td>
      <td>104.417885</td>
      <td>104.139999</td>
      <td>63.106316</td>
      <td>...</td>
      <td>82.797691</td>
      <td>33.209106</td>
      <td>63.790375</td>
      <td>55.257797</td>
      <td>46.115955</td>
      <td>55.737926</td>
      <td>95.890266</td>
      <td>87.029999</td>
      <td>35.645378</td>
      <td>51.504742</td>
    </tr>
    <tr>
      <th>2017-01-05</th>
      <td>44.094769</td>
      <td>44.345036</td>
      <td>27.096159</td>
      <td>46.439575</td>
      <td>NaN</td>
      <td>34.867538</td>
      <td>28.540001</td>
      <td>102.852585</td>
      <td>105.910004</td>
      <td>62.199318</td>
      <td>...</td>
      <td>83.861557</td>
      <td>33.209106</td>
      <td>62.839428</td>
      <td>54.537868</td>
      <td>45.694988</td>
      <td>55.922428</td>
      <td>96.506355</td>
      <td>84.750000</td>
      <td>35.067558</td>
      <td>51.333424</td>
    </tr>
    <tr>
      <th>2017-01-06</th>
      <td>45.468594</td>
      <td>44.654259</td>
      <td>27.398228</td>
      <td>46.454140</td>
      <td>NaN</td>
      <td>35.816082</td>
      <td>28.823334</td>
      <td>104.024323</td>
      <td>108.300003</td>
      <td>62.443527</td>
      <td>...</td>
      <td>84.769508</td>
      <td>33.306793</td>
      <td>62.803951</td>
      <td>54.500465</td>
      <td>45.374668</td>
      <td>56.598938</td>
      <td>96.515533</td>
      <td>85.959999</td>
      <td>35.295441</td>
      <td>51.495228</td>
    </tr>
    <tr>
      <th>2017-01-09</th>
      <td>45.610699</td>
      <td>45.494972</td>
      <td>27.649181</td>
      <td>46.759995</td>
      <td>NaN</td>
      <td>35.780952</td>
      <td>28.406668</td>
      <td>102.861542</td>
      <td>108.570000</td>
      <td>62.740040</td>
      <td>...</td>
      <td>85.062996</td>
      <td>32.802139</td>
      <td>61.767868</td>
      <td>54.668758</td>
      <td>45.182476</td>
      <td>56.757088</td>
      <td>98.391411</td>
      <td>85.970001</td>
      <td>34.912933</td>
      <td>51.352451</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2022-12-23</th>
      <td>147.932892</td>
      <td>12.710000</td>
      <td>130.959961</td>
      <td>155.283295</td>
      <td>85.250000</td>
      <td>105.548424</td>
      <td>63.380001</td>
      <td>260.975555</td>
      <td>338.450012</td>
      <td>160.778214</td>
      <td>...</td>
      <td>79.901894</td>
      <td>68.115944</td>
      <td>104.124252</td>
      <td>31.219862</td>
      <td>108.006187</td>
      <td>125.889435</td>
      <td>125.714478</td>
      <td>248.220001</td>
      <td>45.659222</td>
      <td>144.115570</td>
    </tr>
    <tr>
      <th>2022-12-27</th>
      <td>148.250107</td>
      <td>12.530000</td>
      <td>129.142456</td>
      <td>155.178558</td>
      <td>83.489998</td>
      <td>105.928925</td>
      <td>63.619999</td>
      <td>260.210541</td>
      <td>335.089996</td>
      <td>159.168869</td>
      <td>...</td>
      <td>83.475304</td>
      <td>68.730553</td>
      <td>105.570953</td>
      <td>31.455259</td>
      <td>108.980629</td>
      <td>126.866066</td>
      <td>126.299927</td>
      <td>251.000000</td>
      <td>46.026760</td>
      <td>143.660736</td>
    </tr>
    <tr>
      <th>2022-12-28</th>
      <td>146.802811</td>
      <td>12.320000</td>
      <td>125.179680</td>
      <td>154.454987</td>
      <td>82.489998</td>
      <td>105.206924</td>
      <td>62.599998</td>
      <td>258.062653</td>
      <td>328.329987</td>
      <td>157.284744</td>
      <td>...</td>
      <td>79.278267</td>
      <td>68.235481</td>
      <td>103.836815</td>
      <td>30.386158</td>
      <td>107.228592</td>
      <td>126.289864</td>
      <td>125.019859</td>
      <td>246.839996</td>
      <td>45.206875</td>
      <td>142.207321</td>
    </tr>
    <tr>
      <th>2022-12-29</th>
      <td>149.776733</td>
      <td>12.700000</td>
      <td>128.725311</td>
      <td>154.769165</td>
      <td>85.230003</td>
      <td>107.626602</td>
      <td>63.110001</td>
      <td>263.221527</td>
      <td>337.579987</td>
      <td>160.915604</td>
      <td>...</td>
      <td>80.436417</td>
      <td>68.718948</td>
      <td>104.622452</td>
      <td>31.789503</td>
      <td>109.886169</td>
      <td>126.953972</td>
      <td>126.845695</td>
      <td>257.529999</td>
      <td>46.252934</td>
      <td>146.478577</td>
    </tr>
    <tr>
      <th>2022-12-30</th>
      <td>148.570496</td>
      <td>12.720000</td>
      <td>129.043121</td>
      <td>153.864700</td>
      <td>85.500000</td>
      <td>107.119247</td>
      <td>62.779999</td>
      <td>261.711151</td>
      <td>336.529999</td>
      <td>160.964676</td>
      <td>...</td>
      <td>81.634155</td>
      <td>67.790703</td>
      <td>105.676338</td>
      <td>31.356190</td>
      <td>108.832985</td>
      <td>125.088600</td>
      <td>126.518242</td>
      <td>256.410004</td>
      <td>46.328323</td>
      <td>144.896637</td>
    </tr>
  </tbody>
</table>
<p>1510 rows × 502 columns</p>
</div>


I now have a compiled dataset containing the adjusted closing prices of S&P 500 stocks from January 1, 2017, to January 1, 2023. The last step i will carry out involves exporting this data to a convenient .csv file for analysis, a task easily accomplished with the to_csv method.






```python
adj_prices_new.to_csv('S&P_500_Historical_Price.csv', index=True)
```


```python

```

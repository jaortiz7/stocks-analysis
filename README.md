# Stock Analysis With Excel VBA
Click here to view the Excel file: https://github.com/jaortiz7/stocks-analysis/commit/29f566e2ad364b08e8c415bd82bae6650b1f76f8

## Overview of Project
### Purpose
The purpose of this project was to refactor a Microsoft Excel VBA code to collect certain stock information in the year 2017 and 2018 and determine whether or not the stocks are worth investing.

### The Data
The data that is presented includes two charts with stock information on 12 different stocks. The stock information contains a ticker value, the date the stock was issued, the opening, closing and adjusted closing price, the highest and lowest price, and the volume of the stock. The goal is to retrieve the ticker, the total daily volume, and the return on each stock.

## Results
### Analysis
Before refactoring the code, I copy the code that was needed to create the input box, chart headers, ticker array, and to activate the appropriate worksheet. The steps were then listed out in order to set the structure for the refactoring. Below is the instruction and code as written in the file. 

    '1a) Create a ticker Index
    tickerIndex = 0

    '1b) Create three output arrays
    Dim tickerVolumes(12) As Long
    Dim tickerStartingPrices(12) As Single
    Dim tickerEndingPrices(12) As Single
    
    ''2a) Create a for loop to initialize the tickerVolumes to zero.
    ' If the next row’s ticker doesn’t match, increase the tickerIndex.
    For i = 0 To 11
        tickerVolumes(i) = 0
        tickerStartingPrices(i) = 0
        tickerEndingPrices(i) = 0
    Next i
   
    ''2b) Loop over all the rows in the spreadsheet.
    For i = 2 To RowCount
    
        '3a) Increase volume for current ticker
        tickerVolumes(tickerIndex) = tickerVolumes(tickerIndex) + Cells(i, 8).Value
        
        '3b) Check if the current row is the first row with the selected tickerIndex.
        'If  Then
        If Cells(i, 1).Value = tickers(tickerIndex) And Cells(i - 1, 1).Value <> tickers(tickerIndex) Then
            tickerStartingPrices(tickerIndex) = Cells(i, 6).Value
        End If
        
        '3c) check if the current row is the last row with the selected ticker
        'If  Then
         If Cells(i, 1).Value = tickers(tickerIndex) And Cells(i + 1, 1).Value <> tickers(tickerIndex) Then
            tickerEndingPrices(tickerIndex) = Cells(i, 6).Value
         End If

         '3d) Increase the tickerIndex.
             If Cells(i, 1).Value = tickers(tickerIndex) And Cells(i + 1, 1).Value <> tickers(tickerIndex) Then
                tickerIndex = tickerIndex + 1
            End If
    
    Next i
    
    '4) Loop through your arrays to output the Ticker, Total Daily Volume, and Return.
    For i = 0 To 11
        
        Worksheets("All Stocks Analysis").Activate
        Cells(4 + i, 1).Value = tickers(i)
        Cells(4 + i, 2).Value = tickerVolumes(i)
        Cells(4 + i, 3).Value = tickerEndingPrices(i) / tickerStartingPrices(i) - 1
        
    Next i

## Summary
### Pros of Refactoring Code
Refactoring helps make our code cleaner and more organized. A few advantages of a cleaner code include design and software improvement, debugging, and faster programming. It may also benefit other users who view our projects because it becomes easier to read, as it is more concise and straightforward. However, 

### The Advantages of Refactoring Stock Analysis
The biggest benefit that occurred as a result of the refactoring was an decrease in macro run time. 

### Working Code
![VBA_Challenge_2017](https://user-images.githubusercontent.com/114612708/203655070-91638372-4f69-4d66-b9f6-9deb38e0b31d.png)
![VBA_Challenge_2018](https://user-images.githubusercontent.com/114612708/203655083-1b0ccde0-5ada-49c0-ab5f-27fe9803dc0c.png)


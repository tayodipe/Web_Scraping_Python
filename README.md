# Web Scraping with Python

## List of largest companies in the United States by revenue in 2023
Data Source: Wiki
Url: https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue

![](Front.png)

## Problem Statement
The objective of this portfolio project is to perform web scraping using Python to extract and document the list of the largest companies in the United States by revenue for the year 2023. This project aims to demonstrate proficiency in web scraping techniques, data extraction, and data handling, ultimately resulting in a well-structured and organized dataset that showcases the top companies and their respective revenues, contributing to a comprehensive understanding of the economic landscape in the United States in 2023.

## Solution

- The first thing I did was to inspect the webpage as shown below

![](Inspect.png)

- Next I Import the python libraries (Beautiful Soup) needed as shown
  
        from bs4 import BeautifulSoup
        import requests

- I sent an HTTP request, so I can get the webpage I want to scrap

        url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
        
        page = requests.get(url)
        soup = BeautifulSoup(page.text, ‘html')

  ![](Soup.png)

- Next I go through the Soup, then I extracted all the tables in it.

        soup.find_all(‘table')


- After seeing all the tables, I located the table I need and to get it

        soup.find_all(‘table’)[1] 

  ![](Table1.png)

- The next thing I did was give the table a name so I can reference it. I call it **table**.

        table = soup.find_all('table')[1]
        print(table)

![](MainTable.png)

- Now I want to get the columns sorted out. I see the columns are tagged ‘th’. So I call the columns world_titles

        world_titles = table.find_all(‘th')
        print(world_titles)

![](ColumnA.png)

- Next I strip the so it can look like a real column, I name it world_table_titles

        world_table_titles =[title.text.strip() for title in world_titles]
        print(world_table_titles)

![](ColumnStrip.png)


- Next I imported panda libraries. This help with the dataframe, makes it look like a real table column

        import pandas as pd
        df = pd.DataFrame(columns = world_table_titles)
        df
![](PandaColumn.png)

- I want to find the data in each column(rows). I already know the rows are tagged ‘tr’. So I call it Column_data.

        column_data = table.find_all(‘tr')
- I want each individual row for each column, I call it row_data.

        for row in column_data:
            row_data = row.find_all('td')
            individual_row_data = [data.text.strip() for data in row_data]
            print(individual_row_data)

  ![](IndividualRow.png)

- I did a little cleaning so I can remove the [] at the top

        for row in column_data[1:]:
            row_data = row.find_all('td')
            individual_row_data = [data.text.strip() for data in row_data]
            print(individual_row_data)

![](IndividualRowCleaned.png)

- I now need to make it like a real table, here, I used some panda features too

        for row in column_data[1:]:
            row_data = row.find_all('td')
            individual_row_data = [data.text.strip() for data in row_data]
            
            lenght = len(df)
            df.loc[lenght] = individual_row_data


![](FinalTable.png)


- The last thing I did was to safe the table as an excel file

        df.to_csv(r'/Users/olatayodipe/Desktop/For python/companies.csv', index = False)

  ![](Excel.png)

  ## Summary

  This project involves web scraping with Python to extract a list of the largest companies in the United States by revenue for the year 2023. The aim is to demonstrate proficiency in web scraping techniques, data extraction, and data organization. By successfully scraping and documenting this information, the project contributes to a comprehensive understanding of the economic landscape in the United States for 2023, showcasing the top companies and their respective revenues.

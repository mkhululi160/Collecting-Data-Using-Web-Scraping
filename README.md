# Collecting-Data-Using-Web-Scraping

Import the required libraries:
import requests
from bs4 import BeautifulSoup
import pandas as np

Download the webpage at the url:
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DA0321EN-SkillsNetwork/labs/datasets/Programming_Languages.html"
response = requests.get(url)

if response.status_code == 200:
    print("Webpage downloaded successfully")

Create a soup object:
soup = BeautifulSoup(response.content, 'html.parser')

Scrape the Language name and annual average salary.:
table = soup.find('table')

languages = []
salaries = []

for row in table.find_all('tr')[1:]:
    cols = row.find_all('td')
    if len(cols) > 0:
        language_name = cols[0].get_text(strip=True)
        average_salary = cols[2].get_text(strip=True)
        
        languages.append(language_name)
        salaries.append(average_salary)

Save the scrapped data into a file named popular-languages.csv:
import pandas as pd

df = pd.DataFrame({'Programming Language': languages, 'Average Annual Salary': salaries})

csv_filename = 'scraped_programming_languages.csv'
df.to_csv(csv_filename, index=False)
print(f"Data successfully written to {csv_filename}")
        salaries.append(average_salary)

      

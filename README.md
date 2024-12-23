<h2 align="center"><u>**QuotesScrapper**</u></h2>

<h4 align="center"> practice task </h4>

<p align="center">
<br>
</p>

### [+] Description
This Python project scrapes quotes, authors' information, and associated tags from a website (https://quotes.toscrape.com). The scrapper gathers data, stores it in an SQL database, and also exports the data into a CSV file.
Features

    Scrapes quotes, authors, tags, and categories from the website.
    Retrieves detailed author information including title, date of birth, location, and biography.
    Stores scraped data in a MySQL database.
    Optionally exports scraped data to a CSV file.
    Handles pagination to ensure all data is retrieved from multi-page sections.
    Extracts top tags and categories from the website’s main page.

Requirements

    Python 3.x
    Dependencies:
        requests
        beautifulsoup4
        pandas
        sqlalchemy
        mysql-connector-python (for SQL operations)
        json
        csv

To install all the dependencies, run the following command:

pip install -r requirements.txt

Setup
Database Setup

    Ensure you have MySQL installed and running on your local machine or a server.
    Create a database called quotes (or change the database connection in the code to match your configuration).
    The QuoteScrapper class will automatically create the table scraped_quotes in the database.

Usage

    Clone or download this repository.
    Run:
    python scrap_task.py

The script will:

    Fetch quotes and other information from the website.
    Store the data in a MySQL database (scraped_quotes table).
    Optionally, you can modify the script to output the data to a 
    CSV file by using the csv_maker() method.

Functions

    top_ten()
    This function fetches the top 10 tags from the main page of 
    the website. These tags will be used to categorize the quotes 
    when fetched in later steps.

    fetch_data(url_path, category)
    Scrapes quotes, authors, tags, and associated categories from the provided URL. It handles pagination, meaning it will scrape all available pages for the category.

    fetch_author_info(url)
    Fetches detailed information about each author, including title, date of birth, location, and biography.

    write_sql()
    Writes the scraped data into a MySQL database using SQLAlchemy. The data is stored in the scraped_quotes table with columns: quotes, author, authorinfo, tags, category.

    csv_maker()
    Writes the scraped data into a CSV file (my_quotes.csv). Each row contains the quote, author, author info (in JSON format), tags, and category.

Example Output

    Data will be saved in a MySQL table with the following structure:
    id	quotes	author	authorinfo	tags	category
    1	"Quote text"	Author 1	{"title": "Author Title", "dob": "Jan 1, 1970", "location": "Location", "bio": "Bio"}	"tag1, tag2"	"Category 1"

    CSV File (my_quotes.csv):

    quote,author,author_info,tags,category
    "Quote text","Author 1","{\"title\": \"Author Title\", \"dob\": \"Jan 1, 1970\", \"location\": \"Location\", \"bio\": \"Bio\"}","tag1, tag2","Category 1"

Code Refactor Goals

    Class-based architecture: A single class QuoteScrapper to manage the entire scraping process.
    Reuse URL: The URL https://quotes.toscrape.com is stored as a class variable, ensuring that it's only referenced once throughout the code.
    Efficient string handling: Using substrings where applicable instead of relying on large f-strings, optimizing readability and performance.

Troubleshooting

    Timeout errors: If the server is unreachable, the script will retry fetching the data.
    Empty categories: If a category has no quotes, the script will stop scraping for that category.

License

This project is licensed under the MIT License - see the LICENSE file for details.


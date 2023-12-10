# Web Scraping Project README

## Objective

Create a web scraping project to extract information about organizations from ProPublica.

## Tools and Libraries

- Python
- BeautifulSoup/Selenium

## Given

You are provided with a file containing 10,000 entries detailing nonprofit ID, the name of the nonprofit, and its location. An example entry is as follows:

```plaintext
000004101|South Lafourche Quarterback Club|Lockport|LA|United States|PF
```

## Set Up Your Project:

1. Create a new Python script for your project.
- Install the necessary libraries (requests and beautifulsoup4) using a virtual environment.

2. Write a Function to Extract Information:
- Create a function that takes the URL of an organization's page as input and returns a list containing the extracted information.
- Use Beautiful Soup to parse the HTML and extract relevant data.

3. Handle Different Cases:
- Account for situations where the information may not be available or is not structured as expected.
- Implement error handling to gracefully handle exceptions.

4. Scrape Multiple Pages:
- Write a loop to scrape information from multiple organization pages.
- Consider adding a delay between requests to avoid overwhelming the server.

5. Store the Data:
- Choose a storage format for your data (e.g., CSV).
- Write the extracted information to a file for further analysis.

6. Testing and Refinement:
- Test your scraper on a small subset of pages to ensure it works as expected.
- Refine your code as needed and handle edge cases.

7. Documentation:
- Add comments to explain your code.
- Write a brief documentation or readme file that describes how to use your scraper.

Resources:
https://www.youtube.com/watch?v=bargNl2WeN4&pp=ygUNYmVhdXRpZnVsc291cA%3D%3D&ab_channel=AlexTheAnalyst

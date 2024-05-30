%%sql postgresql:///oldestbusinesses
 
1.Select the oldest and newest founding years from the businesses table
SELECT MIN(year_founded),MAX(year_founded)
FROM businesses;


2. Get the count of rows in businesses where the founding year was before 1000

SELECT COUNT(*) 
FROM businesses
WHERE year_founded < 1000;

3. Select all columns from businesses where the founding year was before 1000
Arrange the results from oldest to newest

SELECT *
FROM businesses
WHERE year_founded < 1000
ORDER BY year_founded;

4.Select business name, founding year, and country code from businesses; and category from categories
where the founding year was before 1000, arranged from oldest to newest

SELECT businesses.business, businesses.year_founded, businesses.country_code, categories.category
FROM businesses
INNER JOIN categories ON businesses.category_code = categories.category_code
WHERE businesses.year_founded < 1000
ORDER BY businesses.year_founded ASC;

5.Select the category and count of category (as "n")
arranged by descending count, limited to 10 most common categories

SELECT categories.category, COUNT(categories.category) AS n
FROM categories
INNER JOIN businesses ON categories.category_code = businesses.category_code
GROUP BY categories.category
ORDER BY n DESC
LIMIT 10;

 6.Select the oldest founding year (as "oldest") from businesses, 
and continent from countries
for each continent, ordered from oldest to newest 

SELECT countries.continent, MIN(businesses.year_founded) AS oldest
FROM businesses
INNER JOIN countries ON businesses.country_code = countries.country_code
GROUP BY countries.continent
ORDER BY oldest ASC;

7.Select the business, founding year, categories.category, country, and continent

SELECT businesses.business, businesses.year_founded, categories.category, countries.country, countries.continent
FROM businesses
INNER JOIN categories ON businesses.category_code = categories.category_code
INNER JOIN countries ON businesses.country_code = countries.country_code;

8.Count the number of businesses in each continent and category

SELECT countries.continent, categories.category, COUNT(businesses.business) AS n
FROM businesses
INNER JOIN categories ON businesses.category_code = categories.category_code
INNER JOIN countries ON businesses.country_code = countries.country_code
GROUP BY countries.continent, categories.category;


9.Repeat that previous query, filtering for results having a count greater than 5

SELECT countries.continent, categories.category, COUNT(businesses.business) AS n
FROM businesses
INNER JOIN categories ON businesses.category_code = categories.category_code
INNER JOIN countries ON businesses.country_code = countries.country_code
GROUP BY countries.continent, categories.category
HAVING COUNT(businesses.business) > 5
ORDER BY n DESC;

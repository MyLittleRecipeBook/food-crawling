# Recipe Data Crawler and Processor for 10000recipe.com

A comprehensive Python-based web scraping and data processing solution that extracts, processes, and analyzes recipe data from 10000recipe.com. The system features asynchronous crawling, robust data parsing, and efficient categorization of Korean recipes with their ingredients, instructions, and metadata.

This project provides a complete pipeline for gathering recipe information, including recipe details, ingredients, cooking instructions, tags, and categories. It employs modern asynchronous programming techniques to efficiently collect data while respecting the website's resources. The processed data is structured and normalized for easy integration into recipe recommendation systems, food analysis applications, or culinary research projects.

## Repository Structure
```
.
├── 10000test_crawling.py          # Main crawler implementation with Selenium
├── done/                          # Completed and stable implementations
│   ├── 10000recipe_log.txt       # Logging output for crawling operations
│   ├── 10000trimRecipe.py        # Recipe trimming and filtering functionality
│   ├── compare_data.py           # Data comparison and merging utilities
│   ├── fast_version.py           # Optimized async crawler implementation
│   ├── ingredients.js            # JavaScript module for ingredient processing
│   ├── preprocessing_recipes.py   # Data cleaning and normalization
│   ├── recent_crawling.py        # Latest version of the crawler
│   └── search_category.py        # Category extraction and classification
└── V1/                           # Initial version of the implementation
    └── 10000recipe_crawling.py   # Original crawler implementation
```

## Usage Instructions
### Prerequisites
- Python 3.7+
- Chrome browser installed (for Selenium-based crawling)
- Node.js (for ingredients.js processing)

Required Python packages:
```
selenium>=4.0.0
beautifulsoup4>=4.9.3
aiohttp>=3.8.0
pandas>=1.3.0
fake-useragent>=0.1.11
webdriver-manager>=3.5.0
```

### Installation
```bash
# Clone the repository
git clone <repository-url>
cd recipe-crawler

# Install Python dependencies
pip install -r requirements.txt

# Install Node.js dependencies (if using ingredients.js)
npm install
```

### Quick Start
1. Basic recipe crawling:
```python
from done.recent_crawling import main

# Crawl 1000 recipes starting from a specific ID
main("Recipe_data.csv", 1000, "output.csv")
```

2. Category-based crawling:
```python
from done.search_category import crawl_recipes

# Crawl recipes within ID range
recipe_ids = crawl_recipes(7018267, 7028266)
```

### More Detailed Examples
1. Preprocessing crawled data:
```python
from done.preprocessing_recipes import preprocess_recipe_data

# Process raw recipe data
preprocess_recipe_data(
    input_file="./recipes.csv",
    output_file="./processed_recipes.csv",
    rows_to_process=10000
)
```

### Troubleshooting
Common Issues:
1. Selenium WebDriver errors
   - Error: `WebDriver not found`
   - Solution: Ensure Chrome and ChromeDriver versions match
   ```python
   from webdriver_manager.chrome import ChromeDriverManager
   driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
   ```

2. Rate limiting
   - Error: HTTP 429 Too Many Requests
   - Solution: Adjust request delays
   ```python
   import random
   time.sleep(random.uniform(1, 3))
   ```

## Data Flow
The system processes recipe data through multiple stages: crawling, parsing, preprocessing, and categorization.

```ascii
[Web Source] -> [Crawler] -> [Parser] -> [Preprocessor] -> [Category Classifier]
     |             |            |              |                    |
     v             v            v              v                    v
 HTML Pages    Raw Data    JSON Data    Cleaned Data    Categorized Data
```

Key component interactions:
1. Crawler fetches HTML content using async requests or Selenium
2. Parser extracts structured data using BeautifulSoup
3. Preprocessor normalizes and validates extracted data
4. Category classifier organizes recipes by type and situation
5. Data storage handles both raw and processed formats
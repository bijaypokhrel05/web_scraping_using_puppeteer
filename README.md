# Web Scraping Tutorial - Books to Scrape

A web scraping practice project that extracts book data from [books.toscrape.com](https://books.toscrape.com), a website specifically designed for practicing web scraping techniques. This project uses **Puppeteer** to dynamically scrape book information from multiple pages.

## 📚 About the Project

This project demonstrates dynamic web scraping techniques using Puppeteer, a headless browser automation library. The scraper navigates through multiple pages of the books.toscrape.com website and extracts detailed information about each book.

### Target Website
**books.toscrape.com** is a practice website created for learning web scraping. It simulates a real e-commerce bookstore with:
- Multiple paginated pages of books
- Dynamic content loaded via JavaScript
- Various book attributes (title, price, availability, ratings)
- A realistic HTML structure for scraping practice

## 🛠️ Technologies Used

- **Node.js** - Runtime environment
- **Puppeteer** (v24.27.0) - Headless Chrome browser automation for dynamic content scraping
- **fs** (File System) - Native Node.js module for writing JSON files

## 📋 Features

- ✅ **Multi-page Scraping**: Automatically navigates through multiple pages (configurable)
- ✅ **Dynamic Content Handling**: Uses Puppeteer to handle JavaScript-rendered content
- ✅ **Data Extraction**: Extracts comprehensive book information including:
  - Book title
  - Price
  - Stock availability
  - Star rating
  - Book detail page link
- ✅ **JSON Output**: Saves all scraped data in a structured JSON format

## 🚀 Installation

### Prerequisites
- Node.js (v12 or higher recommended)
- npm (Node Package Manager)

### Setup Steps

1. **Clone or download the project**
   ```bash
   cd web_scraping_using_puppeteer
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```
   
   This will install Puppeteer and its dependencies (including Chromium).

## 📖 Usage

### Running the Scraper

Simply run the main script:

```bash
node index.js
```

The scraper will:
1. Launch a headless browser instance
2. Navigate through pages 1-10 (configurable in code)
3. Extract book data from each page
4. Save all data to `books.json`
5. Close the browser and display a completion message

### Configuration

You can modify the scraping behavior by editing `index.js`:

```javascript
let maxPages = 10;  // Change this to scrape more or fewer pages
```

The website has 50 pages total, so you can set `maxPages` to any value between 1 and 50.

## 📊 Output Format

The scraped data is saved to `books.json` with the following structure:

```json
[
  {
    "title": "A Light in the Attic",
    "price": "£51.77",
    "stock": "In Stock",
    "rating": "Three",
    "link": "a-light-in-the-attic_1000/index.html"
  },
  {
    "title": "Tipping the Velvet",
    "price": "£53.74",
    "stock": "In Stock",
    "rating": "One",
    "link": "tipping-the-velvet_999/index.html"
  }
]
```

### Data Fields Explained

- **title**: The full title of the book
- **price**: Book price in British Pounds (£)
- **stock**: Availability status ("In Stock" or "Out of Stock")
- **rating**: Star rating (One, Two, Three, Four, or Five)
- **link**: Relative URL path to the book's detail page

## 🔍 How It Works

### Code Explanation

1. **Browser Launch**: Puppeteer launches a headless Chrome browser instance
   ```javascript
   const browser = await puppeteer.launch();
   const page = await browser.newPage();
   ```

2. **Page Navigation**: The script loops through pages, constructing URLs dynamically
   ```javascript
   const url = `https://books.toscrape.com/catalogue/page-${currentPage}.html`;
   await page.goto(url);
   ```

3. **Data Extraction**: Uses `page.evaluate()` to run JavaScript in the browser context
   - Queries DOM elements using CSS selectors (`.product_pod`, `.price_color`, etc.)
   - Extracts data from each book element
   - Returns an array of book objects

4. **Data Aggregation**: Combines data from all pages into a single array
   ```javascript
   allBooks.push(...books);
   ```

5. **File Writing**: Saves the complete dataset to JSON format
   ```javascript
   fs.writeFileSync('books.json', JSON.stringify(allBooks, null, 2));
   ```

### Why Puppeteer?

Puppeteer is used here because:
- The website may have JavaScript-rendered content
- It provides reliable DOM access after page load
- It handles dynamic content better than static HTTP requests
- It can execute JavaScript in the browser context

## 📁 Project Structure

```
web_scraping_using_puppeteer/
├── index.js          # Main scraping script
├── package.json      # Node.js dependencies and project metadata
├── books.json        # Output file with scraped book data
├── node_modules/     # Installed dependencies
└── README.md         # Project documentation
```

## ⚠️ Important Notes

- **Rate Limiting**: The scraper includes a simple loop without delays. For production use, consider adding delays between page requests to be respectful to the server.

- **Error Handling**: The current implementation is basic. For production scraping, add error handling for:
  - Network failures
  - Missing DOM elements
  - Page load timeouts
  - Invalid page numbers

- **Respect robots.txt**: Always check and respect the website's robots.txt file and terms of service when scraping.

## 🎯 Learning Objectives

This project demonstrates:
- ✅ Setting up Puppeteer for web scraping
- ✅ Navigating paginated websites
- ✅ Extracting data using CSS selectors
- ✅ Handling dynamic JavaScript content
- ✅ Saving scraped data to JSON files
- ✅ Working with async/await in Node.js

## 📝 Future Enhancements

Possible improvements you could add:
- Add error handling and retry logic
- Implement rate limiting/delays between requests
- Add progress logging
- Support for scraping individual book detail pages
- Export to CSV or other formats
- Add command-line arguments for configuration
- Implement data validation and cleaning

## 📄 License

ISC

## 👤 Author

Web scraping practice project by [bijaypokhrel05](https://github.com/bijaypokhrel05)

---

**Note**: This project is for educational purposes only. Always respect website terms of service and scraping policies when working with real websites.


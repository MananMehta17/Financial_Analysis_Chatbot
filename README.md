# Financial Analysis Chatbot

**Author:** Manan Mehta ([GitHub](https://github.com/MananMehta17) | [LinkedIn](https://www.linkedin.com/in/mananmehta08))

A two stage Python project: first build a company and year wise dataset of core financial metrics for Microsoft, Apple and Tesla, then query it through a rule based chatbot.

## Project structure

```
Financial_Data_Extraction_and_Initial_analysis.ipynb   # builds dataset, growth rates, ratios, charts
Financial_Analysis_Chatbot.ipynb                       # rule based chatbot over the dataset
combined_financial_analysis.csv                        # dataset used by the chatbot
data/<filing folders>/                                 # place 10-K XBRL/HTML files here
requirements.txt
```

## Stage 1: Data and analysis
* Five core metrics per company and year (USD millions): Total Revenue, Net Income, Total Assets, Total Liabilities, Cash Flow from Operating Activities
* Year over year growth for each metric, calculated within each company
* Ratios: Net Profit Margin, Return on Assets, Debt to Assets
* Line charts comparing metrics, growth rates and ratios across companies
* An HTML table parser (BeautifulSoup) for 10-K filings is included in `FinancialDataAnalyzer.extract_from_html`

## Stage 2: Chatbot
* Keyword based intent matching for the five metrics
* Detects company names in the question (e.g. "Apple net income") and answers only for those
* Shows the latest year value with year over year change
* Comparison queries ("compare revenue Microsoft vs Tesla") also report the highest value
* Timestamped responses

Example:
```
Q: Microsoft total revenue
Total Revenue (latest year):
  Microsoft (2024): $211,915M | YoY change: 6.9%
```

## How to run
1. `pip install -r requirements.txt`
2. Run `Financial_Data_Extraction_and_Initial_analysis.ipynb` (writes the CSV)
3. Run `Financial_Analysis_Chatbot.ipynb`. For typing your own questions, set `INTERACTIVE = True` in the last cell.

## Limitations
* The current dataset comes from `create_sample_data()`; values are placeholders and should be replaced with figures verified from the companies' 10-K filings
* Rule based matching only, no NLP or LLM
* Answers cover the latest year per company

# Day 4 – Fresh Basket Order Agent with Google Sheets

Fresh Basket is a vegetable-shop assistant built in Google Colab with Python, LangChain, and Groq. It estimates prices, looks up opening hours, and records customer-approved pickup requests in Google Sheets.

## Notebook

[DAY-4.ipynb](./DAY-4.ipynb)

## Agent tools

| Tool | What it does |
| --- | --- |
| `get_price` | Calculates an estimate from a vegetable's price per kilogram and the requested weight. |
| `is_open` | Looks up the shop's hours for a day of the week. |
| `log_order` | Validates a pickup request with Pydantic and adds it to Google Sheets. |

The agent converts grams to kilograms, asks for missing order details, and requests confirmation before saving. It keeps conversation history in memory during the notebook session and replies in English or Telugu to match the customer.

## Run in Google Colab

1. Open `DAY-4.ipynb` in Google Colab. The first cell installs `langchain`, `langchain-groq`, and `gspread`.
2. Open **Secrets**, add a Groq API key, and enable **Notebook access**. The current notebook reads the secret named **`GROK_API_KEY`**. If you prefer **`GROQ_API_KEY`**, update the name inside `userdata.get(...)` to match. The agent uses `openai/gpt-oss-20b`.
3. Run the first cell and complete the Google sign-in prompt. It creates a spreadsheet named **Fresh Basket Orders** and prints its URL.
4. Run the cells defining the menu, order model, tools, and agent. The first examples check pricing and hours, then ask for confirmation of Jenny's pickup request.
5. Run the final confirmation cell when you're ready to write an example row to your spreadsheet.

Keep API keys in Colab Secrets. Before publishing the notebook, clear any outputs that contain your private spreadsheet URL or customer details.

## Reuse an existing spreadsheet

The setup cell creates a new spreadsheet each time it runs. To reuse one, replace the spreadsheet creation and header-writing lines with:

```python
sh = gc.open_by_url("YOUR_GOOGLE_SHEET_URL")
ws = sh.sheet1
```

Use a sheet with these headers in the first row:

```csv
name,item,quantity_kg,date,total
```

## Example from the notebook

| Customer request | Result |
| --- | --- |
| Are you open on Sunday? How much do 2 kg of tomatoes cost? | Sunday hours are 10 AM to 6 PM. The estimate is ₹80.00. |
| I'm Jenny. I'd like to pick up 500 g of carrots on 24 Dec. | The agent summarizes the 0.5 kg request, estimates ₹30.00, and asks for confirmation. |
| Yes, save that pickup request. | The agent reports that the request was saved and that the shop will confirm stock and pickup details. |

The notebook uses sample prices and hours, and each pickup request records one vegetable. The sheet stores the requested pickup date and an estimated total. The shop confirms actual stock and pickup details.

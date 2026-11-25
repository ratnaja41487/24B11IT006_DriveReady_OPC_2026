# Day 2 – Interactive Fresh Basket Vegetable Shop Chatbot

## Objective

Build an interactive chatbot that estimates vegetable prices, suggests options within a budget, and answers questions about in-store pickup.

## Implementation

- Uses the Groq Python SDK with `openai/gpt-oss-20b`. The system prompt includes a sample price list in rupees per kilogram and asks the model to reply in English or Telugu based on the customer’s language.
- Keeps up to eight recent exchanges so the chatbot can use details from earlier messages. It also handles rate-limit and connection errors.
- Demonstrates `get_price()` separately at startup. The function looks up the vegetable, validates the quantity, calculates the price, and logs the result. Chat replies use the price list supplied in the system prompt.

## How to Run

1. Open `DAY-2.ipynb` in Google Colab.
2. Add your Groq API key to Colab Secrets under `GROK_API_KEY` and grant the notebook access.
3. Run the cells from top to bottom, starting with the `groq` installation cell.
4. Enter a question at the `You:` prompt. Type `exit` to stop.

## Example

**Customer:** I need 1 kg of tomatoes and 500 g of carrots. How much will it cost?

**Result:** The chatbot estimates ₹70 total (₹40 for tomatoes and ₹30 for carrots) and tells the customer that the shop will confirm the final price and availability.

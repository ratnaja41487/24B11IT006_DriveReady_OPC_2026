# Day 1 – Fresh Basket Vegetable Shop Chatbot

## Task

Build a Python chatbot that answers customer questions about vegetable prices and calculates the cost for a requested quantity.

## Implementation

The chatbot uses the Groq API to respond to customer questions. When a customer asks for a price, the chatbot can call the Python `get_price()` function, which multiplies the price per kilogram by the requested quantity in kilograms. The chatbot displays the result in rupees and accepts more questions until the customer types `exit`.

## How to Run

1. Open `DAY-1.ipynb` in Google Colab.
2. Set up your Groq API key privately in Colab.
3. Run the notebook cells in order.
4. Enter a question when the `You:` prompt appears.
5. Type `exit` to stop the chatbot.

## Example

**Customer:** How much do 500 grams of carrots cost?

**Chatbot:** Price for 500 g of carrots: Rs. 30.00

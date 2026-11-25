# Day 2 – Fresh Basket Vegetable Shop Chatbot

**Drive Ready – AI Agents | One Person Company (OPC) Initiative**

## Objective

Build a Python chatbot that answers customer questions about vegetable prices and calculates the total cost for the quantity they request.

## How It Works

The chatbot uses the Groq API to understand customer questions. When a customer asks for a price, it can call the Python function `get_price(vegetable, quantity_kg)`. The function looks up the price per kilogram and multiplies it by the requested quantity in kilograms. The chatbot then displays the total in rupees.

For example, if a customer asks for 500 g of carrots, the chatbot passes `0.5` kg to the pricing function.

## How to Run

1. Open [DAY-2.ipynb](./DAY-2.ipynb) in Google Colab.
2. Configure your `GROQ_API_KEY` privately. Keep the key out of the notebook and the public repository.
3. Run the notebook cells from top to bottom.
4. At the `You:` prompt, ask for the price of a vegetable and specify a quantity.
5. Type `exit` to end the conversation.

## Example

**Customer:** How much do 500 grams of carrots cost?

**Output:** `Price for 500 g of carrots: Rs. 30.00`

## What I Learned

I learned how to connect an AI chatbot to a Python function so it can use the shop’s price list and calculate a total from a customer’s request.

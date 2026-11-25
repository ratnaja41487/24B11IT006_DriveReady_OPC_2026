# Day 1 – Fresh Basket Customer Support and Prompt Guard

## Objective

Build a customer support assistant for Fresh Basket Vegetable Shop and test a sample prompt with Llama Prompt Guard.

## Implementation

- Uses LangChain’s `ChatGroq` with `openai/gpt-oss-120b` to generate replies.
- Uses a system prompt to give the assistant shop information and rules for handling pickup requests. The assistant asks for missing quantities and tells customers that the shop needs to verify prices, stock, and pickup times.
- Runs a separate test using `meta-llama/llama-prompt-guard-2-22m` and prints the score for a sample instruction-override prompt.

## How to Run

1. Open `DAY-1.ipynb` in Google Colab.
2. Add your Groq API key to Colab Secrets under `GROK_API_KEY` and grant the notebook access. Use this exact secret name because the notebook reads it.
3. Run the cells from top to bottom, starting with the `langchain_groq` installation cell.

## Example

**Customer:** I need 1 kg of tomatoes and some carrots. Can I pick them up this evening?

**Result:** The assistant asks how many kilograms of carrots the customer wants and says the shop needs to confirm prices, stock, and pickup time.

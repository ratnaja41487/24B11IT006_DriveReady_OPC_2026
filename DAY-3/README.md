# Fresh Basket Vegetable Shop Chatbot

Fresh Basket is a customer-support chatbot built with Python and LangChain in Google Colab. It answers vegetable price questions, estimates order totals, explains in-store pickup, and replies in English or Telugu.

## What the notebook demonstrates

- **Price estimates** for vegetables sold by weight, including gram-to-kilogram conversion.
- **Conversation memory** using LangChain message history.
- **Two model integrations** using Groq (`openai/gpt-oss-20b`) and Gemini (`gemini-3.1-flash-lite`).
- **CSV-based testing** with individual results and a pass-rate summary.
- **A LangChain agent demo** that handles an off-topic request for a flower bouquet. The demo uses no external tools.

## Run in Google Colab

1. Open `DAY-3.ipynb` in Google Colab.
2. Run this installation cell to set up the dependencies for both model examples and the agent demo:

   ```python
   %pip install -q langchain langchain-groq langchain-google-genai
   ```

3. In Colab’s **Secrets** panel, add `GROQ_API_KEY` for Groq and `GEMINI_API_KEY` for Gemini if you plan to run both examples. Enable **Notebook access** for each key you use.
4. Before running the notebook, update all Groq setup and verification cells to read `userdata.get("GROQ_API_KEY")`. The current notebook uses `GEMINI_API_KEY` in one Groq setup cell and `GROK_API_KEY` in two others. Keep `GEMINI_API_KEY` in the Gemini setup cell.
5. Run the model setup, prompt, and chain cells in order. The main test cell creates its own CSV with 18 questions. To run the separate five-question test cell, upload its CSV to `/content/test.csv` or pass its actual path to `run_tests()`.

## Example conversation

**Customer:** Hi, I'm Jenny. How much for 1 kg of tomatoes and 500 g of carrots?

**Chatbot:** The estimated total is ₹70. Tomatoes cost ₹40 and 500 g of carrots cost ₹30.

**Customer:** What's my name?

**Chatbot:** Your name is Jenny.

## Saved test results

| Test run | Passed | Failed | Errors |
|---|---:|---:|---:|
| Groq price tests | 18 | 0 | 0 |
| Gemini CSV tests | 5 | 0 | 0 |

The notebook records these results from previous runs. Each CSV test starts with empty conversation history. To check memory, send two consecutive questions through `ask()`.

## Order estimates

The notebook uses sample prices. The shop confirms actual prices, stock, and pickup times.

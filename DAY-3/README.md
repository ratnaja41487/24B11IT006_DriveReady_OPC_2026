# Day 3 – Fresh Basket AI Chatbot with LangChain

Fresh Basket is a customer-support chatbot for a vegetable shop. It estimates prices in Indian rupees, answers in-store pickup questions, and remembers details from earlier messages in the same Colab session. The notebook demonstrates the same shop prompt with Groq and Google Gemini.

## Features

- Estimates order totals from sample per-kilogram prices, including quantities entered in grams.
- Answers in English or Telugu and recommends vegetables based on a recipe or budget.
- Uses conversation history to recall a customer's name and order details.
- Evaluates model replies using CSV test cases and reports passes, failures, and API errors.
- Includes a LangChain agent demo that redirects an off-topic flower request back to vegetable shopping. The demo runs without external tools.

## Run in Google Colab

1. Open [DAY-3.ipynb](./DAY-3.ipynb) in Google Colab.
2. Replace the first installation cell with the following, then run it:

   ```python
   %pip install -q langchain langchain-groq langchain-google-genai
   ```

3. Open **Secrets** in the Colab sidebar and add the keys for the providers you plan to run. Enable **Notebook access** for each secret.

   | Provider | Colab secret | Model used in the notebook |
   | --- | --- | --- |
   | Groq | `GROQ_API_KEY` | `openai/gpt-oss-20b` |
   | Google Gemini | `GEMINI_API_KEY` | `gemini-3.1-flash-lite` |

4. In the current notebook, update each Groq setup or key-check cell to read `userdata.get("GROQ_API_KEY")`. Those cells currently use a mix of `GEMINI_API_KEY` and `GROK_API_KEY`. The Gemini setup cell continues to read `GEMINI_API_KEY`.
5. Run the Groq setup, prompt, and chain cells in order. Run the Groq CSV tests before the Gemini cells, which rebuild `fresh_basket_chain` with the Gemini model. The optional agent demo uses the Gemini model defined as `llm`.

Store API keys in Colab Secrets and keep them out of the notebook code and outputs.

## Example conversation

```text
Customer: Hi, I'm Jenny. How much for 1 kg of tomatoes and 500 g of carrots?
Assistant: The estimated total is ₹70. Tomatoes cost ₹40 and 500 g of carrots cost ₹30.

Customer: What's my name?
Assistant: Your name is Jenny.
```

Try these two messages in one Colab cell after building the chain:

```python
history.clear()
print(ask("Hi, I'm Jenny. How much for 1 kg of tomatoes and 500 g of carrots?"))
print(ask("What's my name?"))
```

## Test results

| Saved notebook run | Passed | Failed | API errors | Pass rate |
| --- | ---: | ---: | ---: | ---: |
| Groq price tests | 18 | 0 | 0 | 100% |
| Gemini CSV tests | 5 | 0 | 0 | 100% |

The Groq test cell creates `/content/fresh_basket_tests.csv` automatically and checks whether each full reply contains the expected rupee amount.

The Gemini test cell reads `/content/test.csv`. To reproduce that run, create a CSV with the following content and upload it to Colab as `test.csv` before running the Gemini test cell:

```csv
question,must_include
What is the price of 1 kg of onions?,35
Can I collect my vegetables from the shop?,pickup
Can I pick up 2 kg of potatoes this evening?,confirm
How much does 250 g of green beans cost?,20
What is the total for 2 kg of tomatoes and 1 kg of onions?,115
```

Each CSV question starts with empty conversation history. The two-message example checks memory separately. The table shows results saved in the notebook. New runs can vary with model responses, API availability, and quota.

## Project scope

Prices are sample estimates. The shop confirms actual prices, stock, and pickup times.

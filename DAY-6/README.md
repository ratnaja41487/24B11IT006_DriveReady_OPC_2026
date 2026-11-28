# Day 6 – LangGraph Intent Routing and Tool-Calling Chatbots

This exercise uses **LangGraph**, **LangChain**, and **Groq** in Google Colab to build two chatbots. Fresh Basket routes customer messages by intent. The second chatbot lets the model decide when to look up information on Wikipedia.

## Notebooks

| Notebook | What it demonstrates |
| --- | --- |
| [DAY-6.ipynb](./DAY-6.ipynb) | Fresh Basket classifies messages as orders, FAQs, or greetings and unrelated requests. |
| [Copy_of_Langgraph_Chatbot_With_Tools.ipynb](./Copy_of_Langgraph_Chatbot_With_Tools.ipynb) | A chatbot calls Wikipedia when needed, then uses the result to answer. |

## How to Run in Colab

1. In Colab **Secrets**, store your Groq API key under `GROK_API_KEY` and enable **Notebook access**. Both notebooks use this exact secret name and call `openai/gpt-oss-120b`.
2. For **Fresh Basket**, run both installation cells before the first graph import. Run the later Groq setup and plain-text classifier cells before compiling the final routing graph. If the earlier structured-output demo returns a tool-call error, continue with the later classifier, which asks for one intent label and validates it.
3. Before the Fresh Basket agent setup cell, run the Day 4 definitions for `get_price`, `is_open`, and `log_order`, including their menu, hours, and any order-schema dependencies. Set up the Google Sheets worksheet as `ws` if you intend to save an order. These tools are referenced but are defined outside the Day 6 notebook.
4. Run the Fresh Basket agent setup, conditional graph, and streaming examples in order.
5. For the **Wikipedia chatbot**, open the second notebook and run its installation, tool setup, Groq setup, and graph cells in order. Run the sample questions after compiling the graph.

## Fresh Basket intent routing

The initial graph sends every classified message to the FAQ node. The final graph uses the intent to select one of three paths:

| Intent | Example | Expected behavior |
| --- | --- | --- |
| `faq` | How much does 1 kg of tomatoes cost? | The FAQ agent uses the price tool. With the Day 4 sample menu, the estimate is ₹40. |
| `order` | I'd like to pick up 500 g of carrots on 24 Dec. | The order agent collects missing details and asks for confirmation before saving a pickup request. |
| `other` | Good morning! | The graph returns a greeting and explains what Fresh Basket can help with. |

The notebook renders the graph as a Mermaid diagram and streams updates so you can see the classifier and the selected node. Each sample message starts a separate run. To complete an order across multiple turns, pass the earlier order-agent messages along with the customer's confirmation.

## Wikipedia chatbot

The model can answer directly or request a Wikipedia lookup. A LangGraph `ToolNode` executes the lookup and returns the result to the chatbot, which can then answer the user. Try the notebook's example, **“What is UNESCO?”**, and inspect the streamed messages to see whether the model calls the tool.

The notebook defines an ArXiv tool as well, while the compiled graph uses only Wikipedia through `tools = [wiki_tool]`.

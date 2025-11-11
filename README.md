# tripcraftAI
Here is a comprehensive README file for your `tripcraftAI` repository, generated based on the structure and content of the files you provided.

-----

# 🌍 TripCraftAI

TripCraftAI is an intelligent, agentic application designed to act as a personal AI Travel Agent and Expense Planner. It leverages a multi-agent workflow (using LangGraph) and a suite of external tools to build comprehensive, real-time travel itineraries, including detailed cost breakdowns, based on simple user prompts.

## 📸 Screenshots

Here is the application in action, planning a 5-day trip to Udaipur:

| Main Interface | Generated Itinerary | Cost & Weather |
| :---: | :---: | :---: |
|  |  |  |

## ✨ Features

  * **Agentic Planning:** Utilizes a core agent built with LangGraph to dynamically research, plan, and structure travel itineraries.
  * **Real-time Data:** Fetches live data for crucial planning aspects:
      * **Places:** Attractions, restaurants, activities, and transport modes via Google Places API (with Tavily as a fallback).
      * **Weather:** Current weather and multi-day forecasts from OpenWeatherMap.
  * **Expense Management:** Automatically calculates:
      * Total estimated trip costs.
      * Daily budget estimates.
      * Live currency conversions.
  * **Dual Interface:**
      * **Streamlit UI:** A user-friendly web interface for easy interaction.
      * **FastAPI Backend:** A robust API endpoint for programmatic access.
  * **Persistent Memory:** Uses SQLite to maintain conversation history and context for follow-up questions.
  * **Dockerized:** Comes with a `Dockerfile` for easy and consistent deployment.

## 🛠️ Tech Stack & Architecture

  * **Backend:** FastAPI
  * **Frontend:** Streamlit
  * **AI/Agent Framework:** LangGraph, LangChain
  * **LLM Provider:** Groq (default, configured in `config.yaml`), OpenAI
  * **Tools & APIs:**
      * Google Places API
      * OpenWeatherMap API
      * ExchangeRate-API
      * Tavily Search API
  * **Database:** SQLite (for agent checkpointing)
  * **Containerization:** Docker

The application works by passing a user query to a LangGraph agent. This agent, defined by a system prompt, breaks down the request and uses the available tools (weather, places, calculator, currency) to gather all necessary information before compiling the final travel plan.

## 🚀 Getting Started

Follow these instructions to get the project up and running on your local machine.

### Prerequisites

  * Python 3.11+
  * API Keys for the following services:
      * Groq
      * Google Places
      * OpenWeatherMap
      * ExchangeRate-API
      * Tavily Search (optional, for fallback)

### Installation

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/adithya95978/tripcraftai.git
    cd tripcraftai
    ```

2.  **Install dependencies:**

    ```bash
    pip install -r requirements.txt
    ```

    This will install all necessary packages, including `langgraph`, `fastapi`, `streamlit`, and more.

3.  **Set up Environment Variables:**
    Create a `.env` file in the root of the project and add your API keys. The application uses `python-dotenv` to load these keys.

    ```ini
    GROQ_API_KEY=your_groq_api_key
    GPLACES_API_KEY=your_google_places_api_key
    OPENWEATHERMAP_API_KEY=your_openweathermap_api_key
    EXCHANGE_RATE_API_KEY=your_exchangerate_api_key
    TAVILY_API_KEY=your_tavily_search_api_key
    ```

### Usage

You need to run both the backend server and the frontend application.

1.  **Run the FastAPI Backend:**
    The backend server handles the agent logic and API requests.

    ```bash
    uvicorn main:app --host 0.0.0.0 --port 8000
    ```

    The server will be running on `http://localhost:8000`.

2.  **Run the Streamlit Frontend:**
    In a **new terminal**, run the Streamlit app:

    ```bash
    streamlit run streamlit_app.py
    ```

    The application will open in your browser, typically at `http://localhost:8501`.

### 🐳 Running with Docker

You can also build and run the application using Docker.

1.  **Build the image:**

    ```bash
    docker build -t tripcraftai .
    ```

2.  **Run the container:**
    (Make sure your `.env` file is present in the root directory to be copied, or pass the environment variables using the `-e` flag)

    ```bash
    docker run -p 8000:8000 --env-file .env tripcraftai
    ```

    This will start the FastAPI server on port 8000. You will still need to run the Streamlit app locally to interact with it.

## 📁 File Structure

```
tripcraftAI/
├── agent/
│   ├── agentic_wf.py     # Defines the core LangGraph agent workflow
│   └── .gitkeep
├── config/
│   ├── config.yaml       # Configuration for LLM providers (e.g., Groq model)
│   └── .gitkeep
├── library/
│   ├── prompt.py         # System prompt defining the AI agent's role
│   └── .gitkeep
├── tools/
│   ├── calci_tool.py     # Tool for calculations (total cost, daily budget)
│   ├── cc_tool.py        # Tool for currency conversion
│   ├── place_info_tool.py # Tool for Google Places & Tavily search
│   ├── weather_info.py   # Tool for OpenWeatherMap API
│   └── .gitkeep
├── uploads/              # Sample images for README
│   ├── image1.png
│   ├── image2.png
│   ├── image3.png
│   └── image4.png
├── utils/
│   ├── calculator.py     # Utility functions for calculations
│   ├── config_loader.py  # Loads the config.yaml
│   ├── curr_converter.py # Utility for currency conversion logic
│   ├── model_loader.py   # Loads the LLM (Groq, OpenAI)
│   ├── place_info_search.py # Utility for Google Places & Tavily logic
│   ├── save_to_doc.py    # Utility to save plans as .md files
│   ├── weather_info.py   # Utility for OpenWeatherMap logic
│   └── .gitkeep
├── Dockerfile            # Container definition for deployment
├── LICENSE               # Apache 2.0 License
├── main.py               # FastAPI backend server
├── README.md             # This file
├── requirements.txt      # Python dependencies
└── streamlit_app.py      # Streamlit frontend application
```

## 📜 License

This project is licensed under the Apache License 2.0. See the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.

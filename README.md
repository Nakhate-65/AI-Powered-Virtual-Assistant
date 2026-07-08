import requests
import json

OLLAMA_URL = "http://localhost:11434/api/generate"
MODEL_NAME = "gpt-oss:120b-cloud"

def get_ollama_response(prompt):
    payload = {
        "model": MODEL_NAME,
        "prompt": prompt,
        "stream": False
    }

    response = requests.post(OLLAMA_URL, json=payload)

    if response.status_code == 200:
        return response.json()["response"]
    else:
        return "Error connecting to Ollama."

def main():
    print("Academic Virtual Assistant (Ollama Backend)")
    print("Type 'exit' to quit.\n")

    while True:
        user_input = input("You: ")

        if user_input.lower() == "exit":
            print("Assistant: Goodbye!")
            break

        reply = get_ollama_response(user_input)
        print("Assistant:", reply)

if __name__ == "__main__":
    main()

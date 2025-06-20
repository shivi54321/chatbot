# chatbot
# ChatBot
import requests

GROQ_API_KEY = "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"  
def chat_with_groq(prompt):
    url = "https://api.groq.com/openai/v1/chat/completions"
    headers = {
        "Authorization": f"Bearer {GROQ_API_KEY}",
        "Content-Type": "application/json"
    }
    data = {
        "model": "llama3-70b-8192", 
        "messages": [{"role": "user", "content": prompt}],
        "temperature": 0.7
    }

    response = requests.post(url, headers=headers, json=data)

    try:
        result = response.json()
        return result['choices'][0]['message']['content']
    except Exception as e:
        print("❌ Error occurred:", response.text)
        return "Something went wrong. Please check the API key or model."

# Run chatbot loop
print("Welcome to Groq Chat! Type 'exit' to quit.")
while True:
    user_input = input("You: ")
    if user_input.lower() == 'exit':
        break
    response = chat_with_groq(user_input)
    print("Bot:", response)

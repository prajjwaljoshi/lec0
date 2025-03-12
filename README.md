import os
import openai

# Set Azure OpenAI credentials
openai.api_type = "azure"
openai.api_key = os.getenv("AZURE_OPENAI_API_KEY")  # Fetch API key from env variables
openai.api_base = "https://your-resource-name.openai.azure.com/"  # Your Azure OpenAI endpoint
openai.api_version = "2023-12-01-preview"  # API version (check Azure portal for updates)

# Set your deployment name (not model name)
deployment_id = "your-deployment-name"

try:
    response = openai.ChatCompletion.create(
        deployment_id=deployment_id,  # Correct parameter for Azure
        messages=[
            {"role": "system", "content": "You are an AI assistant."},
            {"role": "user", "content": "Hello, how are you?"}
        ],
        max_tokens=5,
        temperature=0.7
    )

    print(response)  # Prints full API response
    print(response['choices'][0]['message']['content'])  # Extracts AI response
    
    print("Azure OpenAI API is working correctly!")

except Exception as e:
    print(f"An error occurred: {e}")
    print("Check your API key, endpoint, deployment name, and internet connection.")

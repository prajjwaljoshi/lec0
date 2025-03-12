import os
import openai

# Replace with your actual Azure OpenAI credentials
openai.api_key = os.environ.get("AZURE_OPENAI_API_KEY")  # Use environment variable
openai.api_base = "https://your-resource-name.openai.azure.com/"  # Your Azure OpenAI endpoint
openai.api_version = "2023-12-01-preview"  # API version (check Azure for latest)
deployment_name = "your-deployment-name"  # The name of the model deployment

try:
    response = openai.ChatCompletion.create(
        engine=deployment_name,  # Azure requires the deployment name
        messages=[{"role": "system", "content": "You are an AI assistant."},
                  {"role": "user", "content": "Hello, how are you?"}],
        max_tokens=5,  # Limit the generated text
        temperature=0.7
    )
    
    print(response)  # Prints the raw API response
    print(response['choices'][0]['message']['content'])  # Extracts the generated response
    
    print("Azure OpenAI API Key is working, and the model is accessible!")

except Exception as e:
    print(f"An error occurred: {e}")
    print("Check your API key, deployment name, and endpoint.")

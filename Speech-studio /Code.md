# chatbot_azure.py
from azure.core.credentials import AzureKeyCredential
from azure.ai.language.conversations import ConversationAnalysisClient

# Configurações do seu recurso no Azure
ENDPOINT = "https://<seu-recurso>.cognitiveservices.azure.com/"
KEY = "sua-chave-de-api"
PROJECT_NAME = "seu-projeto-clu"
DEPLOYMENT_NAME = "producao"

def chatbot_azure():
    # Inicializa o cliente
    client = ConversationAnalysisClient(ENDPOINT, AzureKeyCredential(KEY))
    
    print("Chatbot Azure (Digite 'sair' para encerrar)")
    print("-------------------------------------------")
    
    while True:
        # Recebe input do usuário
        user_input = input("Você: ")
        
        if user_input.lower() == 'sair':
            break
            
        # Envia a consulta para o modelo
        result = client.analyze_conversation(
            task={
                "kind": "Conversation",
                "analysisInput": {
                    "conversationItem": {
                        "participantId": "user1",
                        "text": user_input,
                        "id": "1",
                        "language": "pt-br"
                    }
                },
                "parameters": {
                    "projectName": PROJECT_NAME,
                    "deploymentName": DEPLOYMENT_NAME,
                    "verbose": True
                }
            }
        )
        
        # Exibe a resposta do chatbot
        if result['result']['prediction']['topIntent'] == "None":
            print("Bot: Desculpe, não entendi. Poderia reformular?")
        else:
            print(f"Bot: {result['result']['prediction']['entities'][0]['text']}")

if __name__ == "__main__":
    chatbot_azure()

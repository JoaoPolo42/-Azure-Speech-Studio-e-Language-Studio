Speech-to-Text (STT) no Azure Speech Studio
O Speech-to-Text (STT), ou reconhecimento de fala, é uma tecnologia que converte áudio em texto usando modelos de IA. No Azure Speech Studio, essa funcionalidade permite desde transcrições em tempo real até processamento de arquivos de áudio em lote, com suporte para diversos idiomas, sotaques e cenários específicos.

Principais Recursos
1. Tipos de Transcrição
Tipo	Descrição	Aplicações
Em Tempo Real	Conversão instantânea (ex: legendas ao vivo).	Call centers, reuniões, assistentes de voz.
Em Lote (Batch)	Processamento assíncrono de arquivos de áudio.	Análise de gravações, podcasts, entrevistas.
2. Idiomas e Modelos
Suporte a 100+ idiomas e variantes (ex.: pt-BR, en-US, es-ES).

Modelos pré-treinados e customizáveis (para vocabulário técnico).

3. Recursos Avançados
✔ Identificação de falantes (diarização).
✔ Filtro de conteúdo sensível (palavrões, PII).
✔ Pontuação automática (vírgulas, pontos).

Como Usar o Speech-to-Text
Opção 1: Portal do Azure Speech Studio
Acesse o Speech Studio.

Selecione "Speech-to-Text" > "Real-time Transcription" ou "Batch Transcription".

Faça upload do áudio ou teste com o microfone.

Opção 2: Programação (Python SDK)
python
from azure.cognitiveservices.speech import SpeechConfig, AudioConfig, SpeechRecognizer

# Configuração
speech_key = "SUA_CHAVE_AZURE"
region = "eastus"
speech_config = SpeechConfig(subscription=speech_key, region=region)

# Reconhecer fala do microfone
audio_config = AudioConfig(use_default_microphone=True)
recognizer = SpeechRecognizer(speech_config, audio_config)

print("Fale algo...")
result = recognizer.recognize_once()

print(f"Texto reconhecido: {result.text}")
Opção 3: API REST (Para Processamento em Lote)
bash
POST https://{region}.api.cognitive.microsoft.com/speechtotext/v3.1/transcriptions
Headers: {
  "Ocp-Apim-Subscription-Key": "SUA_CHAVE",
  "Content-Type": "application/json"
}
Body: {
  "contentUrls": ["https://exemplo.com/audio.wav"],
  "locale": "pt-BR"
}

Casos de Uso
Cenário	Benefício
Atendimento Automatizado	Transcrição de chamadas para análise de qualidade.
Acessibilidade	Legendas automáticas para surdos e deficientes auditivos.
Reuniões	Conversão de gravações em atas de reunião.

Limitações e Boas Práticas
Ruído Ambiente: Áudios com muito ruído podem reduzir a precisão.

Customização: Para termos técnicos (ex.: jargões médicos), treine um modelo Custom Speech.

Custo: Cobrança por minutos processados (ver preços).

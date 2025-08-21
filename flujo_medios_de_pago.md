kind: AdaptiveDialog
beginDialog:
  kind: OnRecognizedIntent
  id: main
  intent:
    triggerQueries:
      - monto mínimo para hacer una compra
      - cuanto es lo mínimo que puedo comprar
      - cuanto es lo mínimo que puedo pedir

  actions:
    - kind: SearchAndSummarizeContent
      id: 6psQvs
      autoSend: false
      variable: Topic.Respuesta
      userInput: consulta sobre monto mínimo
      fileSearchDataSource:
        searchFilesMode:
          kind: SearchSpecificFiles
          files:
            - cr7fa_agent.file.02_Politicas_Comerciales.docx_A30

      knowledgeSources:
        kind: SearchSpecificKnowledgeSources

      responseCaptureType: FullResponse

    - kind: SendActivity
      id: sendActivity_k5ORNJ
      activity: "{Topic.Respuesta.Text.Content}"
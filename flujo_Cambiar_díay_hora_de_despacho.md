kind: AdaptiveDialog
beginDialog:
  kind: OnRecognizedIntent
  id: main
  intent:
    triggerQueries:
      - No alcanzo a recibir mi pedido
      - no podré recibir mi pedido a la hora que lo programé
      - necesito que mi pedido se retrase
      - Quiero reprogramar mi pedido
      - Quiero postergar mi pedido
      - Necesito cambiar la hora de mi pedido
      - no alcanzaré a recibir mi pedido

  actions:
    - kind: Question
      id: question_38EHLp
      interruptionPolicy:
        allowInterruption: true

      variable: init:Topic.Var1
      prompt: La reprogramación de su pedido se podrá generar solamente para un horario posterior al agendado actualmente. ¿En qué estado se encuentra el pedido?
      entity:
        kind: EmbeddedEntity
        definition:
          kind: ClosedListEntity
          items:
            - id: Ingresado
              displayName: Ingresado

            - id: En preparación
              displayName: En preparación

            - id: En camino
              displayName: En camino

            - id: Otro
              displayName: Otro

    - kind: ConditionGroup
      id: conditionGroup_dbp0vc
      conditions:
        - id: conditionItem_awChTl
          condition: =Topic.Var1 = 'crcc6_jumbito.topic.Cambiardayhoradedespacho.main.question_38EHLp'.Ingresado
          actions:
            - kind: Question
              id: question_QNnmKv
              interruptionPolicy:
                allowInterruption: true

              variable: init:Topic.Var2
              prompt: ¿Qué plataforma está utilizando?
              entity:
                kind: EmbeddedEntity
                definition:
                  kind: ClosedListEntity
                  items:
                    - id: Web
                      displayName: Web

                    - id: Aplicación
                      displayName: Aplicación

            - kind: ConditionGroup
              id: conditionGroup_uPFPF5
              conditions:
                - id: conditionItem_dukD4S
                  condition: =Topic.Var2 = 'crcc6_jumbito.topic.Cambiardayhoradedespacho.main.question_QNnmKv'.Web
                  actions:
                    - kind: SendActivity
                      id: sendActivity_FdnMuD
                      activity: Debe ingresar a su cuenta y dar click en el menú, donde indica "Hola, ...". Una vez desplegado el menú, ingresar a la sección "Mis compras". Allí, deberá dar click a "Revisar pedido" seleccionando el pedido en cuestión. Luego, a la derecha, dar click a "Reprogramar pedido"

                    - kind: SendActivity
                      id: sendActivity_mcnaYJ
                      activity: Por último, deberá elegir el horario según lo necesite⏰🛒. En caso de que no haya sido posible esta gestión, será necesario que tome contacto con uno de nuestros agentes. 👨‍💻

                - id: conditionItem_Bb3mAS
                  condition: =Topic.Var2 = 'crcc6_jumbito.topic.Cambiardayhoradedespacho.main.question_QNnmKv'.Aplicación
                  actions:
                    - kind: SendActivity
                      id: sendActivity_FLjrbC
                      activity: Debe ingresar a su cuenta y dar click en la esquina inferior derecha, donde diga "Cuenta". Una vez desplegado el menú, ingresar a la sección "Mis compras". Allí, deberá dar click en "Ingresado" seleccionando el pedido en cuestión. Luego, a la derecha, dar click a "Reprogramar".

                    - kind: SendActivity
                      id: sendActivity_o5imhv
                      activity: Por último, deberá elegir el horario adecuado según lo necesite⏰🛒. En caso de que no haya sido posible esta gestión, será necesario que tome contacto con uno de nuestros agentes. 👨‍💻

      elseActions:
        - kind: SendActivity
          id: sendActivity_Kbml56
          activity: Le comentamos que, por el estado en el que se encuentra su  pedido, no será posible que este sea reprogramado.

        - kind: SendActivity
          id: sendActivity_u5Imtv
          activity: En caso de que el pedido llegue a su destino y no haya podido ser recepcionado, por favor tome contacto con uno de nuestros agentes. Si desea, transferiré la conversación con un ejecutivo de atención al cliente. ¡Estamos aquí para ayudarle! 👨‍💻

    - kind: Question
      id: question_e88uKa
      interruptionPolicy:
        allowInterruption: true

      variable: init:Topic.Var3
      prompt: ¿Hay algo más en lo que le pueda ayudar?
      entity: BooleanPrebuiltEntity

    - kind: ConditionGroup
      id: conditionGroup_kxZJfT
      conditions:
        - id: conditionItem_4obgLF
          condition: =Topic.Var3 = false
          actions:
            - kind: BeginDialog
              id: fGZBT7
              dialog: crcc6_jumbito.topic.EndofConversation

      elseActions:
        - kind: SendActivity
          id: sendActivity_mdutut
          activity: Cuénteme, ¿en qué le puedo ayudar?

    - kind: CancelAllDialogs
      id: KDWXPp
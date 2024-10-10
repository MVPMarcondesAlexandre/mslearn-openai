# Laboratório 02: Usar os SDKs do Azure OpenAI na sua aplicação

### Duração Estimada: 40 minutos

## Cenário do laboratório
Com o Serviço Azure OpenAI, os desenvolvedores podem criar chatbots, modelos de linguagem e outras aplicações que se destacam na compreensão da linguagem natural humana. O Azure OpenAI fornece acesso a modelos de IA pré-treinados, bem como um conjunto de APIs e ferramentas para personalizar e ajustar esses modelos para atender aos requisitos específicos de sua aplicação. Neste exercício, você aprenderá como implantar um modelo no Azure OpenAI e usá-lo em sua própria aplicação.

No cenário deste exercício, você desempenhará o papel de um desenvolvedor de software encarregado de implementar uma aplicação que possa utilizar inteligência artificial generativa para fornecer recomendações de trilhas. As técnicas usadas no exercício podem ser aplicadas a qualquer aplicação que queira usar as APIs do Azure OpenAI.

## Objetivos do laboratório
Neste laboratório, você concluirá as seguintes tarefas:

- Tarefa 1: Provisionar um recurso Azure OpenAI
- Tarefa 2: Implantar um modelo
- Tarefa 3: Configurar uma aplicação no Cloud Shell
- Tarefa 4: Configurar a sua aplicação
- Tarefa 5: Testar a sua aplicação

## Tarefa 1: Provisionar um recurso Azure OpenAI

Antes de poder usar os modelos Azure OpenAI, você deve provisionar um recurso Azure OpenAI em sua assinatura do Azure.

1. No **portal do Azure**, pesquise por **Azure OpenAI (1)** e selecione **OpenAI (2)**.

   ![](../media/8-10-24(10).png)

2. Na tela **Azure AI services | OpenAI**, clique em **+ Criar**.

   ![](../media/8-10-24(11).png)

3. Crie um recurso **Azure OpenAI** com as seguintes configurações 

    - **Assinatura (1)**: Default - Assinatura pré-atribuída.
    - **Grupo de recursos (2)**: openai-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Região (3)**: Selecione <inject key="Region" enableCopy="false" />
    - **Nome (4)**: OpenAI-Lab02-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Tipo de preço (5)**: Standard S0
    - Clique em **Próxima (6)**
  
       ![](../media/8-10-24(36).png)

4. Clique em **Próxima** duas vezes e subsequentemente clique em **Criar**.

    ![](../media/8-10-24(13).png)

5. Aguarde o término da implantação. Em seguida, acesse o recurso do Azure OpenAI implantado no portal do Azure.

    ![](../media/8-10-24(14).png)

6. Para capturar os valores de Chaves e Endpoints, na lâmina **openai-<inject key="DeploymentID" enableCopy="false"></inject>**:
      - Selecione **Chaves e Ponto de extremidade (1)** sob **Gerenciamento de Recursos**.
      - Clique em **Mostrar as Chaves (2)**.
      - Copie a **CHAVE 1 (3)** e certifique-se de colá-la em um editor de texto como o Bloco de Notas para referência futura.
      - Finalmente, copie a URL da API do **Ponto de extremidade (4)** clicando em copiar para a área de transferência. Cole-a em um editor de texto como o Bloco de Notas para uso posterior.

        ![](../media/8-10-24(38).png)

#### Validação

> **Parabéns** por completar a tarefa! Agora, é hora de validá-la. Aqui estão os passos:
> - Clique no botão Validar para a tarefa correspondente. Se você receber uma mensagem de sucesso, pode prosseguir para a próxima tarefa. 
> - Caso contrário, leia atentamente a mensagem de erro e tente novamente o passo, seguindo as instruções no guia do laboratório.
> - Se precisar de alguma assistência, por favor, entre em contato conosco em cloudlabs-support@spektrasystems.com. Estamos disponíveis 24/7 para ajudá-lo.

   <validation step="8d0ea9cb-8ab4-4fa7-81a6-3642e4534d68" />

## Tarefa 2: Implantar um modelo

Para usar a API do Azure OpenAI, você deve primeiro implantar um modelo para usar através do **Azure OpenAI Studio**. Uma vez implantado, faremos referência a esse modelo em nosso aplicativo.

1. No **portal do Azure**, pesquise por **Azure OpenAI (1)** e selecione **OpenAI (2)**.

   ![](../media/8-10-24(10).png)

2. Na lâmina **Azure AI Services | OpenAI**, selecione **OpenAI-Lab02-<inject key="DeploymentID" enableCopy="false"></inject>**

   ![](../media/8-10-24(39).png)

3. No painel de recursos do Azure OpenAI, clique em **Go to Azure OpenAI Studio** e ele navegará para o **Azure AI Studio**.

   ![](../media/8-10-24(40).png)
   
5. Clique em **Implantações (1)** no painel de navegação à esquerda, clique em **+ Implante o modelo (2)**, selecione **Implantar o modelo básico (3)**.  

   ![](../media/8-10-24(41).png)

6. Na janela **Selecionar um modelo**, selecione **gpt-35-turbo-16k (1)** e clique em **Confirmar (3)**.

   ![](../media/8-10-24(42).png)

7. Na interface pop-up **Implantar o modelo**, insira os seguintes detalhes:
    
    - **Nome da implantação (1)**: text-turbo
    - **Versão do modelo (2)**: 0613 (Predefinição)
    - **Tipo de implantação (3)**: Standard
    - **Limite de Velocidade de Tokens por Minuto (milhares) (4)**: 10K
    - Habilitar cota dinâmica: **Habilitado (5)**
    - Clique em **Implantar (6)**
  
      ![](../media/8-10-24(43).png)

8. Isso implantará um modelo com o qual você brincará à medida que avançar.

   > **Nota**: Você pode ignorar a notificação "Falha ao buscar informações de cota de implantações".
   
   > **Nota**: Cada modelo Azure OpenAI é otimizado para um equilíbrio diferente de capacidades e desempenho. Usaremos a série de modelos **3.5 Turbo** na família de modelos **GPT-3** neste exercício, que é altamente capaz de compreensão de linguagem. Este exercício usa apenas um único modelo, no entanto, a implantação e o uso de outros modelos que você pode implantar funcionarão da mesma maneira.

#### Validação

> **Parabéns** por completar a tarefa! Agora, é hora de validá-la. Aqui estão os passos:
> - Clique no botão Validar para a tarefa correspondente. Se você receber uma mensagem de sucesso, pode prosseguir para a próxima tarefa. 
> - Caso contrário, leia atentamente a mensagem de erro e tente novamente o passo, seguindo as instruções no guia do laboratório.
> - Se precisar de alguma assistência, por favor, entre em contato conosco em cloudlabs-support@spektrasystems.com. Estamos disponíveis 24/7 para ajudá-lo.

   <validation step="d1610911-47ae-44ef-a286-4f4961a4b36d" />

## Tarefa 3: Configurar uma aplicação no Cloud Shell

Para mostrar como integrar com um modelo Azure OpenAI, usaremos uma aplicação de linha de comandos que é executada no Cloud Shell no Azure. Abra uma nova guia do navegador para trabalhar com o Cloud Shell.

1. No [portal do Azure](https://portal.azure.com?azure-portal=true), selecione o botão **[>_]** (*Cloud Shell*) na parte superior da página à direita da caixa de pesquisa. Um painel do Cloud Shell será aberto na parte inferior do portal.

    ![](../media/8-10-24(44).png)

2. Na primeira vez que você abrir o Cloud Shell, você pode ser solicitado a escolher o tipo de shell que deseja usar (*Bash* ou *PowerShell*). Selecione **Bash**. Se você não vir esta opção, pule o passo.

   ![](../media/8-10-24(45).png)

3. Dentro do painel Começando, selecione **Montar conta de armazenamento (1)**, selecione sua **Assinatura da conta de armazenamento (2)** no menu suspenso e clique em **Aplicar (3)**.

   ![](../media/8-10-24(46).png)

4. Dentro do painel **Montar conta de armazenamento**, selecione **Eu quero criar uma conta de armazenamento (1)** e clique em **Avancar (2)**.

   ![](../media/8-10-24(47).png)

5. Dentro do painel **Configurações avançadas**, insira os seguintes detalhes:

    - **Assinatura (1)**: Default- Escolha a única assinatura existente atribuída para este laboratório.
    - **Grupo de recursos (2)**: Selecione **Usar existente**
      - openai-<inject key="DeploymentID" enableCopy="false"></inject>
    - **Região (3)**: <inject key="Region" enableCopy="false" />
    - **Nome da Conta de armazenamento (4)**: Selecione **Criar nova**
      - storage<inject key="DeploymentID" enableCopy="false"></inject>
    - **Comp. de arquivos (5)**: Crie um novo compartilhamento de arquivo chamado **none**
    - Clique em **Criar (6)**

        ![](../media/8-10-24(48).png)

6. Note que você pode redimensionar o cloud shell arrastando a barra separadora na parte superior da página, ou usando os ícones **&#8212;**, **&#9723;**, e **X** no canto superior direito da página para minimizar, maximizar e fechar o painel. Para mais informações sobre como usar o Azure Cloud Shell, consulte a [documentação do Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview). 

7. Assim que o terminal iniciar, insira o seguinte comando para baixar a aplicação de exemplo e salvá-lo em uma pasta chamada `azure-openai`.
   
    ```bash
   rm -r azure-openai -f
   git clone https://github.com/MicrosoftLearning/mslearn-openai azure-openai
    ```
    
8. Os arquivos são baixados para uma pasta chamada **azure-openai**. Navegue até os arquivos do laboratório para este exercício usando o seguinte comando.

    ```bash
   cd azure-openai/Labfiles/02-azure-openai-api
    ```
    
    Foram fornecidos aplicativos tanto para C# quanto para Python, bem como um arquivo de texto de exemplo que você usará para testar o resumo. Ambos os aplicativos possuem a mesma funcionalidade.

9. Abra o editor de código integrado e observe o arquivo de texto que você estará resumindo com seu modelo localizado em `text-files/sample-text.txt`. Use o seguinte comando para abrir os arquivos do laboratório no editor de código.

    ```bash
    code .
    ```

    > **Nota:** Se você for solicitado a **Alternar para o Cloud Shell Clássico** após executar o comando **code .**, clique em **Confirmar** e execute os passos 8 e 9 novamente.

    ![](../media/8-10-24(49).png)
   
#### Validação

> **Parabéns** por completar a tarefa! Agora, é hora de validá-la. Aqui estão os passos:
> - Clique no botão Validar para a tarefa correspondente. Se você receber uma mensagem de sucesso, pode prosseguir para a próxima tarefa. 
> - Caso contrário, leia atentamente a mensagem de erro e tente novamente o passo, seguindo as instruções no guia do laboratório.
> - Se precisar de alguma assistência, por favor, entre em contato conosco em cloudlabs-support@spektrasystems.com. Estamos disponíveis 24/7 para ajudá-lo.

   <validation step="bd2f25c6-d67e-4553-a8ed-32e9f0162e26" />

## Tarefa 4: Configurar a sua aplicação

Para este exercício, você concluirá algumas partes importantes do aplicativo para permitir o uso do seu recurso Azure OpenAI.

1. No editor de código, expanda a pasta **CSharp** ou **Python**, dependendo da sua preferência de linguagem.

2. Abra o arquivo de configuração para sua linguagem

    - C#: `appsettings.json`
    
    - Python: `.env`
    
3. Atualize os valores de configuração para incluir o **Ponto de extremidade** e a **chave** do recurso Azure OpenAI que você criou, bem como o nome do modelo que você implantou, `text-turbo`. Em seguida, salve o arquivo clicando com o botão direito no arquivo no painel esquerdo e clicando em **Salvar**

4. Navegue até a pasta da sua linguagem preferida e instale os pacotes necessários

    **C#** : 

    ```bash
    cd CSharp
    dotnet add package Azure.AI.OpenAI --version 1.0.0-beta.14
    ```

    **Python** : 

    ```bash
    cd Python
    pip install python-dotenv
    pip install openai==1.13.3
    ```

5. Navegue até a pasta da sua linguagem preferida, selecione o arquivo de código e adicione as bibliotecas necessárias.

    **C#**: Program.cs

    ```csharp
    // Add Azure OpenAI package
    using Azure.AI.OpenAI;
    ```

    **Python**: test-openai-model.py

    ```python
    # Add Azure OpenAI package
    from openai import AzureOpenAI
    ```

6. No código do aplicativo para sua linguagem, substitua o comentário ***Inicializar o cliente Azure OpenAI...*** com o seguinte código para inicializar o cliente e definir nossa mensagem do sistema.

    **C#**: Program.cs

    ```csharp
    // Initialize the Azure OpenAI client
    OpenAIClient client = new OpenAIClient(new Uri(oaiEndpoint), new AzureKeyCredential(oaiKey));
    
    // System message to provide context to the model
    string systemMessage = "I am a hiking enthusiast named Forest who helps people discover hikes in their area. If no area is specified, I will default to near Rainier National Park. I will then provide three suggestions for nearby hikes that vary in length. I will also share an interesting fact about the local nature on the hikes when making a recommendation.";
    ```

    **Python**: test-openai-model.py

    ```python
    # Initialize the Azure OpenAI client
    client = AzureOpenAI(
            azure_endpoint = azure_oai_endpoint, 
            api_key=azure_oai_key,  
            api_version="2024-02-15-preview"
            )
    
    # Create a system message
    system_message = """I am a hiking enthusiast named Forest who helps people discover hikes in their area. 
        If no area is specified, I will default to near Rainier National Park. 
        I will then provide three suggestions for nearby hikes that vary in length. 
        I will also share an interesting fact about the local nature on the hikes when making a recommendation.
        """
    ```

      >**Nota**: Certifique-se de indentar o código eliminando quaisquer espaços em branco extras após colá-lo no editor de código.

7. Substitua o comentário ***Adicionar código para enviar solicitação...*** com o código necessário para construir a solicitação; especificando os vários parâmetros para o seu modelo, como `messages` e `temperature`.

    **C#**: Program.cs

    ```csharp
    // Add code to send request...
    // Build completion options object
    ChatCompletionsOptions chatCompletionsOptions = new ChatCompletionsOptions()
    {
        Messages =
        {
            new ChatRequestSystemMessage(systemMessage),
            new ChatRequestUserMessage(inputText),
        },
        MaxTokens = 400,
        Temperature = 0.7f,
        DeploymentName = oaiDeploymentName
    };

    // Send request to Azure OpenAI model
    ChatCompletions response = client.GetChatCompletions(chatCompletionsOptions);

    // Print the response
    string completion = response.Choices[0].Message.Content;
    Console.WriteLine("Response: " + completion + "\n");
    ```

    **Python**: test-openai-model.py

    ```python
    # Add code to send request...
    # Send request to Azure OpenAI model
    response = client.chat.completions.create(
        model=azure_oai_deployment,
        temperature=0.7,
        max_tokens=400,
        messages=[
            {"role": "system", "content": system_message},
            {"role": "user", "content": input_text}
        ]
    )
    generated_text = response.choices[0].message.content

    # Print the response
    print("Response: " + generated_text + "\n")
    ```

8. Antes de salvar o arquivo, certifique-se de que seu código se pareça com o código fornecido abaixo.

    **C#**: Program.cs
      
      ```CSharp
      // Implicit using statements are included
      using System.Text;
      using System.Text.Json;
      using Microsoft.Extensions.Configuration;
      using Microsoft.Extensions.Configuration.Json;
      using Azure;
      
      // Add Azure OpenAI package
      using Azure.AI.OpenAI;
      
      // Build a config object and retrieve user settings.
      IConfiguration config = new ConfigurationBuilder()
          .AddJsonFile("appsettings.json")
          .Build();
      string? oaiEndpoint = config["AzureOAIEndpoint"];
      string? oaiKey = config["AzureOAIKey"];
      string? oaiDeploymentName = config["AzureOAIDeploymentName"];
      
      if(string.IsNullOrEmpty(oaiEndpoint) || string.IsNullOrEmpty(oaiKey) || string.IsNullOrEmpty(oaiDeploymentName) )
      {
          Console.WriteLine("Please check your appsettings.json file for missing or incorrect values.");
          return;
      }
      
      // Initialize the Azure OpenAI client...
      OpenAIClient client = new OpenAIClient(new Uri(oaiEndpoint), new AzureKeyCredential(oaiKey));
      
      // System message to provide context to the model
      string systemMessage = "I am a hiking enthusiast named Forest who helps people discover hikes in their area. If no area is specified, I will default to near Rainier National Park. I will then provide three suggestions for nearby hikes that vary in length. I will also share an interesting fact about the local nature on the hikes when making a recommendation.";
      
      do {
          Console.WriteLine("Enter your prompt text (or type 'quit' to exit): ");
          string? inputText = Console.ReadLine();
          if (inputText == "quit") break;
      
          // Generate summary from Azure OpenAI
          if (inputText == null) {
              Console.WriteLine("Please enter a prompt.");
              continue;
          }
          
          Console.WriteLine("\nSending request for summary to Azure OpenAI endpoint...\n\n");
      
          // Add code to send request...
          // Build completion options object
          ChatCompletionsOptions chatCompletionsOptions = new ChatCompletionsOptions()
          {
              Messages =
              {
                  new ChatRequestSystemMessage(systemMessage),
                  new ChatRequestUserMessage(inputText),
              },
              MaxTokens = 400,
              Temperature = 0.7f,
              DeploymentName = oaiDeploymentName
          };
      
          // Send request to Azure OpenAI model
          ChatCompletions response = client.GetChatCompletions(chatCompletionsOptions);
      
          // Print the response
          string completion = response.Choices[0].Message.Content;
          Console.WriteLine("Response: " + completion + "\n");
      
      } while (true);
      ```
    
   **Python**: test-openai-model.py

      ```Python
      import os
      from dotenv import load_dotenv
      
      # Add Azure OpenAI package
      from openai import AzureOpenAI
      
      def main(): 
              
          try: 
          
              # Get configuration settings 
              load_dotenv()
              azure_oai_endpoint = os.getenv("AZURE_OAI_ENDPOINT")
              azure_oai_key = os.getenv("AZURE_OAI_KEY")
              azure_oai_deployment = os.getenv("AZURE_OAI_DEPLOYMENT")
              
              # Initialize the Azure OpenAI client...
              client = AzureOpenAI(
                      azure_endpoint = azure_oai_endpoint, 
                      api_key=azure_oai_key,  
                      api_version="2024-02-15-preview"
                      )
              
              # Create a system message
              system_message = """I am a hiking enthusiast named Forest who helps people discover hikes in their area. 
                  If no area is specified, I will default to near Rainier National Park. 
                  I will then provide three suggestions for nearby hikes that vary in length. 
                  I will also share an interesting fact about the local nature on the hikes when making a recommendation.
                  """
                    
              while True:
                  # Get input text
                  input_text = input("Enter the prompt (or type 'quit' to exit): ")
                  if input_text.lower() == "quit":
                      break
                  if len(input_text) == 0:
                      print("Please enter a prompt.")
                      continue
      
                  print("\nSending request for summary to Azure OpenAI endpoint...\n\n")
                                    
                  # Add code to send request...
                  # Send request to Azure OpenAI model
                  response = client.chat.completions.create(
                      model=azure_oai_deployment,
                      temperature=0.7,
                      max_tokens=400,
                      messages=[
                          {"role": "system", "content": system_message},
                          {"role": "user", "content": input_text}
                      ]
                  )
                  generated_text = response.choices[0].message.content
      
                  # Print the response
                  print("Response: " + generated_text + "\n")
                        
          except Exception as ex:
              print(ex)
      
      if __name__ == '__main__': 
          main()
      ```

9. Para salvar as alterações feitas no arquivo, clique com o botão direito no arquivo no painel esquerdo na janela de código e clique em **Salvar**.

   >**Nota:** Certifique-se de indentar o código eliminando quaisquer espaços em branco extras após colá-lo no editor de código.

## Tarefa 5: Testar a sua aplicação

Agora que seu aplicativo foi configurado, execute-o para enviar sua solicitação ao seu modelo e observe a resposta.

1. Caso esteja utilizando a linguagem **C#**, abra o arquivo **CSharp.csproj** do projeto e substitua o conteúdo por este código. Em seguida, salve o arquivo.
   ```
   <Project Sdk="Microsoft.NET.Sdk">
         
   <PropertyGroup>
      <OutputType>Exe</OutputType>
      <TargetFramework>net8.0</TargetFramework>
      <ImplicitUsings>enable</ImplicitUsings>
      <Nullable>enable</Nullable>
   </PropertyGroup>
         
   <ItemGroup>
      <PackageReference Include="Azure.AI.OpenAI" Version="1.0.0-beta.14" />
      <PackageReference Include="Microsoft.Extensions.Configuration" Version="8.0.*" />
      <PackageReference Include="Microsoft.Extensions.Configuration.Json" Version="8.0.*" />
   </ItemGroup>
         
   <ItemGroup>
      <None Update="appsettings.json">
         <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
      </None>
   </ItemGroup>
         
   </Project>
   ```  

2. Agora, no painel do terminal interativo, certifique-se de que o contexto da pasta seja a pasta da sua linguagem preferida. Em seguida, digite o seguinte comando para executar a aplicação.

    - **C#**: `dotnet run`
    
    - **Python**: `python test-openai-model.py`

      > **Dica**: Você pode usar o ícone **Maximizar tamanho do painel** (**^**) na barra de ferramentas do terminal para ver mais texto no console.

2. Quando solicitado, digite o texto `What hike should I do near Rainier?`.

3. Observe o resultado, notando que a resposta segue as diretrizes fornecidas na mensagem do sistema que você adicionou ao array *messages*.

4. Forneça o prompt `Where should I hike near Boise? I'm looking for something of easy difficulty, between 2 to 3 miles, with moderate elevation gain.` e observe o resultado.

5. No arquivo de código da sua linguagem preferida, altere o valor do parâmetro *temperature* em sua solicitação para **1.0** e salve o arquivo.

6. Execute o aplicativo novamente usando os prompts acima e observe o resultado.

Aumentar a temperatura geralmente faz com que a resposta varie, mesmo quando fornecido o mesmo texto, devido ao aumento da aleatoriedade. Você pode executá-lo várias vezes para ver como o resultado pode mudar. Tente usar valores diferentes para sua temperatura com a mesma entrada.

## Revisão

Neste laboratório, você realizou o seguinte:
- Provisionou um recurso Azure OpenAI
- Implantou um modelo OpenAI dentro do Azure OpenAI Studio
- Integrou modelos Azure OpenAI em suas aplicações

### Você completou com sucesso o laboratório.

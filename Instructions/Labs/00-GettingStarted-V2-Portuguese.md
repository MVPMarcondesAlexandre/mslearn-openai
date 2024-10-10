# Comece com o OpenAI e Desenvolva Soluções de Processamento de Linguagem Natural

### Duração Estimada Total: 4 Horas

## Visão Geral

O serviço do Azure OpenAI traz os modelos de IA generativa desenvolvidos pela OpenAI para a plataforma Azure, possibilitando o desenvolvimento de soluções de IA capazes de gerar texto, traduzir idiomas, escrever diferentes tipos de conteúdo criativo e responder a suas perguntas complexas e muito mais. A segurança, escalabilidade e integração com outros serviços da nuvem Azure facilitam o desenvolvimento e a implantação dessas soluções. Neste laboratório, você aprenderá a provisionar o serviço do Azure OpenAI como um recurso e usar o Azure OpenAI Studio para implementar e explorar os modelos da OpenAI. Com o Azure OpenAI, os desenvolvedores podem criar aplicações como chatbots e modelos de linguagem que se destacam na compreensão da linguagem humana natural. O serviço oferece acesso a modelos de IA pré-treinados e um conjunto de APIs e ferramentas para personalizar e ajustar esses modelos para atender aos requisitos específicos da aplicação. Neste cenário, você assumirá o papel de um desenvolvedor de software responsável de implementar um aplicativo que forneça recomendações de trilhas para caminhadas utilizando inteligência artificial generativa, demonstrando técnicas aplicáveis a qualquer aplicativo que utilize as APIs do Azure OpenAI.

## Objetivo

No final deste laboratório, você será capaz de:

- **Começar a usar o Serviço do Azure OpenAI**: Este exercício prático visa provisionar um recurso do Azure OpenAI e implementar um modelo. Explore as capacidades do modelo no playground de Completions, em seguida, interaja com ele usando o playground de Chat. Aprimore as respostas ajustando os prompts e parâmetros, e aproveite a geração de código para automatizar tarefas.
- **Usar os SDKs do Azure OpenAI na sua aplicação**: Este exercício prático tem como objetivo provisionar um recurso do Azure OpenAI, implementar um modelo, configurar um aplicativo no Cloud Shell e, em seguida, executar o aplicativo, demonstrando o ciclo de vida completo, desde a criação do recurso até a implantação e execução do aplicativo.
  
## Pré-requisitos

- Familiaridade com o serviço do Azure OpenAI, Azure CLI e APIs REST
- Compreensão básica de conceitos de IA e Machine Learning

## Arquitetura

O fluxo de arquitetura para esta tarefa começa com o provisionamento de um recurso Azure OpenAI em sua assinatura do Azure e a implantação de um modelo pré-treinado usando o Azure OpenAI Studio. Em seguida, você explorará as capacidades do modelo no playground de Completions e testará suas habilidades conversacionais no playground de Chat, experimentando diferentes prompts e parâmetros para personalizar as respostas. Você também investigará as capacidades de geração de código do modelo. Na fase de desenvolvimento da aplicação, você configurará seu ambiente no Azure Cloud Shell, configurará a aplicação para integrar com o modelo OpenAI implantado e, finalmente, executará a aplicação para fornecer recomendações de caminhadas usando IA generativa.

## Diagrama de Arquitetura

![Acesse sua VM e Guia do Laboratório](../media/arch20.png)

## Descrição dos Componentes

1. **Azure OpenAI**: O serviço Azure OpenAI fornece acesso via API REST aos poderosos modelos de linguagem da OpenAI. Esses modelos podem ser integrados aos seus dados, permitindo interações personalizadas e seguras.
2. **Modelos do Azure OpenAI**: Oferece modelos de linguagem pré-treinados e personalizáveis para diversas aplicações de IA. Esses modelos permitem soluções poderosas baseadas em IA, gerando conteúdo adaptado e contextualmente relevante com base em prompts bem elaborados.
3. **Azure CloudShell**: O Azure CloudShell oferece uma experiência de shell integrada e baseada em navegador para gerenciar recursos do Azure. Ele fornece um ambiente pronto para uso com ferramentas pré-instaladas e acesso tanto ao Bash quanto ao PowerShell.

## Começando o Laboratório

### Ingressando no seu Ambiente de Laboratório

Uma vez pronto para começar, sua máquina virtual e o guia do laboratório estarão ao seu alcance diretamente no seu navegador web.

![Acesse sua VM e Guia do Laboratório](../media/8-10-24(1).png)

### Máquina Virtual & Guia do Laboratório

Sua máquina virtual é seu principal recurso durante o workshop. O guia do laboratório é seu roteiro para o sucesso.

### Explorando Seus Recursos de Laboratório

Para entender melhor seus recursos e credenciais de laboratório, navegue até a guia **Ambiente**.

![Acesse sua VM e Guia do Laboratório](../media/8-10-24(2).png)

### Utilizando o Recurso de Janela Dividida

Para sua comodidade, você pode abrir o guia do laboratório em uma janela separada selecionando o botão 'Dividir Janela' no canto superior direito.

![Acesse sua VM e Guia do Laboratório](../media/8-10-24(3).png)

### Gerenciando Sua Máquina Virtual

Sinta-se à vontade para iniciar, parar ou reiniciar sua máquina virtual conforme necessário na guia **Recursos**. Sua experiência está em suas mãos!

![Acesse sua VM e Guia do Laboratório](../media/8-10-24(4).png)

## Vamos Começar com o Portal do Azure

1. Na sua máquina virtual, clique no ícone do Portal do Azure conforme mostrado abaixo:

   ![Acesse sua VM e Guia do Laboratório](../media/8-10-24(5).png)

2. Você verá a guia **Entrar no Microsoft Azure**. Aqui, insira suas credenciais:

   - **Email/Usuário:** <inject key="AzureAdUserEmail"></inject>

       ![Acesse sua VM e Guia do Laboratório](../media/8-10-24(6).png)

3. Em seguida, forneça sua senha:

   - **Senha:** <inject key="AzureAdUserPassword"></inject>

       ![Acesse sua VM e Guia do Laboratório](../media/8-10-24(7).png)

4. Se for solicitado para permanecer conectado, você pode clicar em **Não**.

    ![Acesse sua VM e Guia do Laboratório](../media/8-10-24(8).png)

5. Se uma janela pop-up **Bem-vindo ao Microsoft Azure** aparecer, simplesmente clique em **Cancelar** para pular o tour.

6. Clique em **Próximo** no canto inferior direito para começar sua jornada no laboratório!

    ![Acesse sua VM e Guia do Laboratório](../media/8-10-24(9).png)

Este laboratório lhe proporcionará as habilidades para implantar e personalizar modelos do Azure OpenAI, permitindo que você crie aplicações avançadas de IA, como chatbots e sistemas de recomendação.

## Contato de Suporte

A equipe de suporte da CloudLabs está disponível 24/7, 365 dias por ano, via e-mail e chat para garantir assistência contínua a qualquer momento. Oferecemos canais de suporte dedicados especificamente para alunos e instrutores, garantindo que todas as suas necessidades sejam prontamente e eficientemente atendidas.

Contatos de Suporte para Alunos:

- Suporte por E-mail: cloudlabs-support@spektrasystems.com
- Suporte por Chat ao Vivo: https://cloudlabs.ai/labs-support

Agora, clique em Próximo no canto inferior direito para passar para a próxima página.

## Votos de bom treinamento!

# DevOps

## Pipeline de CI/CD com Compilação, Qualidade de Código, Testes Automatizados, Envio de Imagem Docker e Deploy no Azure

Esse projeto serviu para criar um script YAML que define uma série de etapas para um fluxo de trabalho de integração contínua (CI) e implantação contínua (CD) no Azure. O fluxo de trabalho é acionado quando há um push no branch "main" do repositório.

 - Compilação: Essa etapa compila o projeto Java usando o Maven, executando o comando mvn clean install -DskipTests. Ela é executada em um ambiente Ubuntu e utiliza o JDK 11 como versão do Java.

 - Qualidade de Código: Essa etapa realiza análises de qualidade de código usando o SonarCloud. Primeiro, é feito o checkout do repositório. Em seguida, é adicionada permissão de execução ao arquivo "mvnw" (script do Maven Wrapper). Por fim, é executado o comando ./mvnw verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar para realizar a análise e envio dos resultados para o SonarCloud. É necessário fornecer a chave do projeto SonarCloud como variável de ambiente "SONAR_TOKEN".

 - Testes Automatizados: Essa etapa executa os testes automatizados do projeto. Primeiro, é feito o checkout do repositório. Em seguida, é configurado o JDK 11 e é executado o comando mvn -B test --file pom.xml para rodar os testes utilizando o Maven.

 - Enviando imagem para o DockerHub: Essa etapa envia uma imagem Docker para o DockerHub. Ela utiliza o Docker para fazer o login na conta do DockerHub com as credenciais fornecidas em "DOCKERHUB_USERNAME" e "DOCKERHUB_TOKEN". Em seguida, utiliza o Docker Build and Push Action para criar e enviar a imagem Docker com base no arquivo "Dockerfile". A imagem é marcada com a tag "henriquezanetti/javacrescer:latest".

 - Publica app ACI: Essa etapa faz o deploy do aplicativo em um Azure Container Instance (ACI). Primeiro, é feito o login na conta do Azure através da Azure CLI com as credenciais fornecidas em "AZURE_CREDENTIALS". Em seguida, é utilizado o Azure Container Instances Deploy Action para realizar o deploy do contêiner com base na imagem Docker enviada anteriormente. São fornecidos detalhes como grupo de recursos, nome do contêiner, localização, configurações de CPU e memória, além das informações de login do registro Docker (DockerHub).

Essas etapas compõem um pipeline de CI/CD que compila o projeto, realiza análises de qualidade de código, executa testes automatizados, envia uma imagem Docker para o DockerHub e faz o deploy do aplicativo em um Azure Container Instance. Cada etapa é executada em sequência, dependendo do sucesso da etapa anterior.

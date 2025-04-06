1. Pré-requisitos
Antes de executar o sistema, certifique-se de ter os seguintes componentes instalados em sua máquina:

Java JDK 17 ou superior

Verifique a instalação com: java -version

Maven (gerenciador de dependências)

Verifique a instalação com: mvn -version

MySQL Server (versão 8.0 ou superior)

Verifique a instalação com: mysql --version

Git (opcional, apenas se for clonar o repositório)

Visual Studio Code (ou outra IDE de sua preferência)

Extensões recomendadas para VSCode:

Java Extension Pack

Spring Boot Extension Pack

MySQL

2. Configuração Inicial
2.1. Banco de Dados MySQL
Inicie o servidor MySQL

Acesse o console do MySQL:

bash
Copy
mysql -u root -p
Crie o banco de dados e um usuário (opcional):

sql
Copy
CREATE DATABASE biblioteca_db;
CREATE USER 'biblioteca_user'@'localhost' IDENTIFIED BY 'senha123';
GRANT ALL PRIVILEGES ON biblioteca_db.* TO 'biblioteca_user'@'localhost';
FLUSH PRIVILEGES;
2.2. Configuração da Aplicação
Edite o arquivo src/main/resources/application.properties com as credenciais do seu banco de dados:

properties
Copy
spring.datasource.url=jdbc:mysql://localhost:3306/biblioteca_db
spring.datasource.username=root  # ou 'biblioteca_user' se criou um usuário específico
spring.datasource.password=senha123
3. Executando a Aplicação
Opção 1: Executando com Maven (terminal)
Navegue até a raiz do projeto (onde está o arquivo pom.xml)

Execute o seguinte comando:

bash
Copy
mvn spring-boot:run
Opção 2: Executando na IDE (VSCode)
Abra o projeto no VSCode

Localize a classe principal BibliotecaApplication.java

Clique no botão "Run" acima do método main ou use o atalho F5

4. Acessando a Aplicação
Após a inicialização, o sistema estará disponível em:

Front-end: http://localhost:8080

API REST: http://localhost:8080/api/livros

5. Testando o Sistema
Via Interface Web
Acesse http://localhost:8080 no navegador

Utilize a interface para:

Adicionar novos livros

Editar livros existentes

Buscar livros por título

Remover livros

Via API (usando cURL ou Postman)
Listar todos os livros:

bash
Copy
curl http://localhost:8080/api/livros
Adicionar um novo livro:

bash
Copy
curl -X POST -H "Content-Type: application/json" -d '{
  "titulo": "Dom Casmurro",
  "autor": "Machado de Assis",
  "isbn": "9788544001823"
}' http://localhost:8080/api/livros
Atualizar um livro (substitua {id} pelo ID real):

bash
Copy
curl -X PUT -H "Content-Type: application/json" -d '{
  "titulo": "Dom Casmurro",
  "autor": "Machado de Assis",
  "isbn": "9788544001823",
  "disponivel": true
}' http://localhost:8080/api/livros/{id}
Deletar um livro:

bash
Copy
curl -X DELETE http://localhost:8080/api/livros/{id}

7. Solução de Problemas Comuns
Erro de conexão com o banco de dados
Verifique se o MySQL está rodando

Confira as credenciais no application.properties

Verifique se o usuário tem permissões no banco

Porta 8080 já em uso
Altere a porta no application.properties:

properties
Copy
server.port=8081
Dependências não encontradas
Execute:

bash
Copy
mvn clean install
8. Finalizando a Aplicação
Para parar a aplicação, no terminal onde ela está rodando, pressione:
Ctrl + C

9. Contato
Em caso de dúvidas ou problemas, entre em contato com o desenvolvedor ou consulte a documentação oficial do Spring Boot: https://spring.io/projects/spring-boot

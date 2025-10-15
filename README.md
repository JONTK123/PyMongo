# Sistema de Mensagens Criptografadas com PyMongo

Um sistema de mensagens seguro e criptografado desenvolvido em Python, utilizando MongoDB para armazenamento de dados e criptografia AES para proteção das mensagens.

## 📋 Descrição

Este projeto implementa um sistema de mensagens peer-to-peer com criptografia AES-CBC, onde os usuários podem enviar e receber mensagens criptografadas. Cada mensagem é protegida por uma chave de criptografia definida pelo remetente, garantindo privacidade e segurança na comunicação.

## ✨ Funcionalidades

- **Autenticação de Usuários**: Sistema de login seguro com email e senha
- **Envio de Mensagens Criptografadas**: Envie mensagens para outros usuários com criptografia AES-CBC
- **Recebimento e Descriptografia**: Receba e descriptografe mensagens usando a chave correta
- **Interface de Terminal Interativa**: Menu intuitivo para navegação entre funcionalidades
- **Armazenamento em MongoDB**: Dados persistentes e escaláveis
- **Timestamp de Mensagens**: Registro de data e hora de cada mensagem enviada

## 🛠️ Tecnologias Utilizadas

- **Python 3.x**: Linguagem de programação principal
- **PyMongo 4.10.1**: Driver MongoDB para Python
- **MongoDB Atlas**: Banco de dados NoSQL em nuvem
- **AES-PKCS5 1.0.3**: Biblioteca de criptografia AES com padding PKCS5
- **Cryptography 43.0.1**: Funções criptográficas adicionais
- **CFFI 1.17.1**: Interface de funções estrangeiras para Python
- **dnspython 2.7.0**: Toolkit DNS para Python (necessário para MongoDB Atlas)

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- Python 3.7 ou superior
- pip (gerenciador de pacotes Python)
- Conta no MongoDB Atlas (ou instância local do MongoDB)
- Conexão com a internet

## 🚀 Instalação

1. **Clone o repositório**
   ```bash
   git clone https://github.com/JONTK123/PyMongo.git
   cd PyMongo
   ```

2. **Navegue até o diretório src**
   ```bash
   cd src
   ```

3. **Crie um ambiente virtual (recomendado)**
   ```bash
   python -m venv env
   
   # No Windows
   env\Scripts\activate
   
   # No Linux/Mac
   source env/bin/activate
   ```

4. **Instale as dependências**
   ```bash
   pip install -r requirements.txt
   ```

## ⚙️ Configuração

### Configuração do Banco de Dados

1. **Variável de Ambiente (Recomendado)**
   
   Crie um arquivo `.env` no diretório `src` com sua string de conexão MongoDB:
   ```
   MONGODB_URI=mongodb+srv://seu_usuario:sua_senha@cluster.mongodb.net/
   ```

2. **Configuração Padrão**
   
   Se não configurar a variável de ambiente, o sistema utilizará a conexão padrão definida em `mongohandler.py`

### Estrutura do Banco de Dados

O sistema utiliza um banco de dados chamado `pymongo` com duas coleções:

- **users**: Armazena informações dos usuários
  ```json
  {
    "nome": "Nome do Usuário",
    "nickname": "email@exemplo.com",
    "password": "senha123"
  }
  ```

- **messages**: Armazena as mensagens criptografadas
  ```json
  {
    "to": "destinatario@exemplo.com",
    "nickname": "remetente@exemplo.com",
    "content": "mensagem_criptografada_base64",
    "datetime": "2024-01-01T12:00:00"
  }
  ```

## 💻 Uso

1. **Inicie o programa**
   ```bash
   python main.py
   ```

2. **Faça login**
   - Digite seu email (nickname)
   - Digite sua senha
   - Se as credenciais estiverem corretas, você será autenticado

3. **Menu Principal**
   
   Após o login, você terá acesso a três opções:

   **Opção 1 - Enviar Mensagem**
   - Selecione o destinatário da lista
   - Digite a mensagem
   - Defina uma chave de criptografia (lembre-se dela para descriptografar)
   - A mensagem será criptografada e enviada

   **Opção 2 - Ler Mensagens**
   - Visualize suas mensagens recebidas
   - Selecione uma mensagem para ler
   - Digite a chave de criptografia para descriptografar
   - Se a chave estiver correta, a mensagem será exibida

   **Opção 3 - Desligar**
   - Encerra o programa

## 📁 Estrutura do Projeto

```
PyMongo/
│
├── README.md                 # Documentação do projeto
│
└── src/                      # Código fonte
    ├── main.py              # Ponto de entrada da aplicação
    ├── mongohandler.py      # Manipulador do banco de dados MongoDB
    ├── models.py            # Modelos de dados (Users, Messages)
    ├── requirements.txt     # Dependências do projeto
    ├── .gitignore          # Arquivos ignorados pelo git
    └── env/                # Ambiente virtual (não versionado)
```

## 🔐 Segurança

### Criptografia
- O sistema utiliza **AES-CBC** (Advanced Encryption Standard - Cipher Block Chaining)
- Padding PKCS5 para blocos de dados
- Chaves são ajustadas para 16 bytes (128 bits)
- IV (Initialization Vector) fixo: `0011223344556677`
- Mensagens codificadas em Base64 para armazenamento

### Recomendações de Segurança
⚠️ **IMPORTANTE**: Este projeto é educacional. Para uso em produção, considere:
- Implementar hash de senhas (bcrypt, argon2)
- Usar HTTPS para comunicação
- Gerar IVs aleatórios para cada mensagem
- Implementar gerenciamento seguro de chaves
- Adicionar autenticação de dois fatores
- Validar e sanitizar todas as entradas de usuário

## 🧪 Testes

Atualmente, o projeto não possui testes automatizados. Para testar manualmente:

1. Certifique-se de ter usuários cadastrados no MongoDB
2. Execute o programa e tente fazer login
3. Teste o envio de mensagens entre usuários
4. Verifique se a criptografia/descriptografia funciona corretamente

## 📝 Como Contribuir

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

## 🐛 Problemas Conhecidos

- O IV (Initialization Vector) é fixo, o que reduz a segurança
- Senhas são armazenadas em texto plano no banco de dados
- Não há validação de formato de email
- Não há limite de tentativas de login

## 🔮 Melhorias Futuras

- [ ] Implementar hash de senhas
- [ ] Adicionar testes unitários e de integração
- [ ] Criar interface gráfica (GUI)
- [ ] Implementar sistema de grupos
- [ ] Adicionar notificações de novas mensagens
- [ ] Permitir anexos de arquivos
- [ ] Implementar sistema de backup
- [ ] Adicionar logs de auditoria

## 📚 Recursos Adicionais

- [Documentação PyMongo](https://pymongo.readthedocs.io/)
- [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
- [Python Cryptography](https://cryptography.io/en/latest/)
- [AES Encryption](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)

## 👥 Autores

- **Filipe Daniel M. T. Mota**
- **Thiago Luiz Fossa**
- **Alex Insel**

## 📄 Licença

Este projeto é de código aberto e está disponível para fins educacionais.

---

**Nota**: Este projeto foi desenvolvido como parte de um trabalho acadêmico e serve como exemplo de implementação de sistema de mensagens com criptografia básica. Não é recomendado para uso em produção sem melhorias significativas de segurança.

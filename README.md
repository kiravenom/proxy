### VETOR DA FALHA
Falha crítica permitindo a criação de um fluxo controlado de comunicação entre cliente e servidor. 
A vulnerabilidade ocorre porque a chave de decrypt AES é estática e permite a alteração da requisição POST

### ⚡ Fluxo de Ataque

1️⃣ **Proxy Intercept** – tráfego redirecionado para um proxy sob controle do atacante.  

2️⃣ **Decrypt com AES Key** – mensagens descriptografadas com chave AES **estática** armazenada no cliente.  

3️⃣ **Edição dos Dados** – payload pode ser manipulado (ex.: parâmetros de autenticação, UID, etc).  

4️⃣ **Reencrypt** – conteúdo modificado é recriptografado com a mesma chave.  

5️⃣ **Envio para URL Original** – requisição adulterada é enviada ao servidor como legítima. 

### 🔑 Chaves AES expostas no cliente
```csharp
private static readonly byte[] AES_KEY = Encoding.UTF8.GetBytes("Yg&tc%DEuh6%Zc^8");
private static readonly byte[] AES_IV  = Encoding.UTF8.GetBytes("6oyZDr22E3ychjM%");
```

### ⚡ Fluxo de Ataque

| Etapa              | Descrição                                                                 |
|--------------------|---------------------------------------------------------------------------|
| **Proxy Intercept** | Tráfego redirecionado para proxy do atacante.                            |
| **Decrypt**         | Descriptografado com chave AES estática no cliente.                      |
| **Edição**          | Payload alterado (UID, parâmetros, etc).                                 |
| **Reencrypt**       | Recriptografado com a mesma chave.                                       |
| **Envio**           | Requisição adulterada enviada ao servidor como legítima.                 |





## COM TUDO EM MÃOS, VAMOS FAZER O SETUP DA APLICAÇÃO PARA RECEBER OS REQUESTS

> ⚠️ **O MITMPROXY É NESCESSÁRIO PARA REALIZAR A INTERCEPTAÇÃO E MANIPULAÇÃO DO TRÁFEGO HTTP.**


### 1️⃣ Download dos Arquivos
- Faça o download deste repositório clicando em **Code > Download ZIP** ou usando `git clone`.
- Recomendo utilizar **Windows** para maior compatibilidade.

### 2️⃣ Instalar Python
- Baixe e instale a versão mais recente do [Python](https://www.python.org/downloads/) (>= 3.9).
- Durante a instalação, marque a opção **"Add Python to PATH"**.

### 3️⃣ Instalar Dependências
- Abra o **Prompt de Comando** ou **PowerShell** dentro da pasta do projeto.
- Instale os módulos necessários executando:

```bash
pip install -r requirements.txt
```

### 4️⃣ Configurar bypass.py

- Edite o arquivo bypass.py e atualize os endereços e informações.

- Altere a variável de configuração para que o fluxo do tráfego seja redirecionado para o seu IP local (máquina onde o proxy irá rodar).

### 5️⃣ Configurar o Emulador

- Instale o certificado gerado/fornecido dentro do emulador (necessário para o proxy conseguir interceptar HTTP).

- Execute no shell do emulador o comando para definir o proxy:

```bash
settings put global http_proxy <SEU_IP>:8080
```
### 6️⃣ Iniciar o Servidor

No terminal, inicie a aplicação de bypass:

```bash
python bypass.py
```

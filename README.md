# Projeto Node-RED: Consulta de CEP

Este projeto Node-RED implementa um serviço de consulta de CEP que permite aos usuários inserir um CEP em um formulário web e receber informações detalhadas sobre o endereço, como estado, cidade, bairro, rua, latitude e longitude. A consulta é realizada através da API BrasilAPI.

## Funcionalidades

- Formulário web para entrada de CEP.
- Validação básica do formato do CEP (8 dígitos, com ou sem hífen).
- Integração com a API BrasilAPI para consulta de dados de CEP.
- Exibição das informações do CEP de forma clara e organizada.

## Pré-requisitos

- Node.js e npm instalados.
- Node-RED instalado e em execução.

## Instalação 
primeiro é necessário instalar o nodejs através do site:

[Nodejs.org](https://nodejs.org/en)

Após a instalação é possivel checar se está devidamente instalado através do prompt de comando:

```bash
node --version
```
Com o Nodejs devidamente instalado, ainda com o terminal aberto, para instalar o node red é necessário digitar o seguinte comando:

```bash
npm install -g --unsafe-perm node-red
```

## Execução
1. Importe o arquivo `flows.json` para o seu ambiente Node-RED.
   - Abra o Node-RED em seu navegador (geralmente `http://localhost:1880`).
   - Clique no menu superior direito (três linhas horizontais) e selecione `Importar` > `Área de Transferência`.
   - Cole o conteúdo do arquivo `flows.json` e clique em `Importar`.
2. Implante o fluxo clicando no botão `Deploy` no canto superior direito do Node-RED.
3. Acesse o formulário web através do seguinte URL:
   `http://localhost:1880/formulario1`

## Uso

1. No formulário, digite um CEP válido (apenas números, o formato `00000-000` será ajustado automaticamente).
2. Clique em `Buscar`.
3. As informações do CEP serão exibidas na tela.

## Detalhes Técnicos

O fluxo Node-RED é composto pelos seguintes nós principais:

- **HTTP In (`/formulario1`):** Responsável por servir o formulário HTML inicial para a entrada do CEP.
- **Template (Formulário CEP):** Contém o código HTML e CSS para renderizar o formulário de consulta de CEP. Inclui um script JavaScript para formatar o CEP enquanto o usuário digita.
- **HTTP In (`/consulta1`):** Recebe a requisição GET do formulário com o CEP inserido pelo usuário.
- **Function (Monta URL):** Extrai o CEP da requisição (`msg.req.query.formcep`) e constrói a URL completa para a API BrasilAPI (ex: `https://brasilapi.com.br/api/cep/v2/32450000`).
- **HTTP Request:** Realiza a requisição GET para a API BrasilAPI com a URL do CEP.
- **Template (Retorno HTML):** Processa a resposta da API BrasilAPI e gera o HTML para exibir as informações detalhadas do CEP. Inclui um botão para retornar ao formulário de consulta.
- **HTTP Response:** Envia a resposta HTML de volta para o navegador do usuário.
- **Nós de Debug:** Existem nós de debug configurados para auxiliar no monitoramento do `msg.url`, `msg.numCep` e o `payload` de retorno da requisição da API.

## API Utilizada

- [BrasilAPI - Consulta de CEP](https://brasilapi.com.br/docs#tag/CEP)

## Autor

- Victor Jorge



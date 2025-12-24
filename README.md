# 📘 Resumo de Estudos – Alura

## 📌 Sobre o Repositório

Este repositório reúne resumos das aulas assistidas na plataforma **Alura** sobre **HTTP, APIs, arquitetura web, segurança (HTTPS/TLS)** e uso prático de ferramentas (DevTools, Postman, Telnet, Wireshark). O objetivo é oferecer um material de **revisão rápida, consulta técnica e apoio aos estudos**.
Todas as informações contidas neste README foram extraídas exclusivamente dos resumos das aulas assistidas e organizadas para leitura clara e objetiva.

---

## 📋 Índice

* [📌 Sobre o Repositório](#-sobre-o-repositório)
* [📚 Conteúdos Estudados](#-conteúdos-estudados)
  * [🛠️ Ambiente de Desenvolvimento](#️-ambiente-de-desenvolvimento)
  * [🌐 HTTP, URLs e Camadas da Internet](#-http-urls-e-camadas-da-internet)
  * [🔌 Portas, Servidores e DNS](#-portas-servidores-e-dns)
  * [🧾 Formato de Mensagens HTTP (linha inicial, headers, body)](#-formato-de-mensagens-http-linha-inicial-headers-body)
  * [🛠 Telnet, Postman e DevTools — Ferramentas práticas](#-telnet-postman-e-devtools—ferramentas-práticas)
  * [🛡️ Segurança: HTTP vs HTTPS / TLS / Certificados](#️-segurança-http-vs-https--tls--certificados)
  * [📦 APIs e Projeto AluraBooks (exemplos práticos)](#-apis-e-projeto-alurabooks-exemplos-práticos)
* [📌 Observações Importantes](#-observações-importantes)
* [🚀 Próximos Estudos](#-próximos-estudos)
* [📎 Referências](#-referências)

---

## 📚 Conteúdos Estudados


### 🛠️ Ambiente de Desenvolvimento

Conteúdo extraído das aulas práticas (AluraBooks / Node.js / DevTools):

* **Execução local (exemplos observados)**:

  ```bash
  # Iniciar back-end (ex.: projeto AluraBooks)
  npm run start-auth
  # Resultado observado:
  # API disponível em http://localhost:8000

  # Iniciar front-end
  npm start
  # Front-end em http://localhost:3000


* **Boas práticas**:
* Inspecionar requisições com DevTools → aba **Network**.
* Usar **Postman** para testes repetíveis (configurar `Body` → `raw` → `JSON`).
* Evitar colocar chaves privadas em repositórios; usar cofres de segredo para produção.
* Forçar reload (`Ctrl` + `Shift` + `R`) se houver cache ao testar rotas de documentação.



---

### 🌐 HTTP, URLs e Camadas da Internet

**HTTP (Hypertext Transfer Protocol)**

* Protocolo da **camada de aplicação** que define regras de troca de mensagens entre **cliente** (navegador/apps) e **servidor**.
* **Regra básica:** a comunicação é iniciada pelo **cliente**; o servidor responde.
* **HTTP trafega sobre TCP** (entrega confiável); versões mais novas (HTTP/3) usam QUIC sobre UDP (ver observações).

**Composição de uma URL (exemplo):**

```text
http://localhost:3000/
│   │          └─ caminho
│   └─ host
└─ protocolo (scheme)

```

**Camadas da Internet (resumo):**

* **Física** — meios físicos (cabos, Wi-Fi, 5G).
* **Enlace** — tráfego local no meio físico.
* **Rede** — endereçamento IP.
* **Transporte** — TCP / UDP.
* **Aplicação** — HTTP/HTTPS, navegadores e apps.

**O que memorizar**

* HTTP = camada de aplicação; depende de transporte (TCP/UDP conforme versão).
* Cliente inicia requisição; servidor responde com códigos de status.

---

### 🔌 Portas, Servidores e DNS

* **Porta:** identifica ponto de acesso de uma aplicação no servidor.
* Portas padrão: `80` (HTTP), `443` (HTTPS).
* Faixas: `0–1023` (reservadas), `1024–65535` (ephemeral / dev).
* Uso comum em dev: front-end → porta `3000`; back-end → porta `8000`.


* **DNS:** resolve nomes de domínio para endereços IP (ex.: `google.com` → `142.251.128.14`).
* Estrutura hierárquica: Raiz → TLDs (.com, .br) → domínios → subdomínios.



---

### 🧾 Formato de Mensagens HTTP (linha inicial, headers, body)

* Mensagens HTTP são **textuais** e seguem o padrão:
```text
<linha inicial>
<Header: Value>
<Header: Value>

<body opcional>

```


* **Exemplo de requisição POST (cru):**
```http
POST /public/login HTTP/1.1
Host: localhost
Content-Type: application/json
Content-Length: 45

{"email": "geo@alura.com.br", "senha": "123"}

```


* **Headers importantes**:
* `Content-Type`: formato do corpo (ex.: `application/json;charset=utf-8`, `text/html`).
* `Accept`: formatos aceitos pelo cliente.
* `Authorization`: esquema de autenticação (ex.: `Authorization: Bearer <token>`).


* **Códigos de status (classes)**:
* `1xx` — Informativos
* `2xx` — Sucesso (ex.: `200 OK`, `201 Created`)
* `3xx` — Redirecionamento
* `4xx` — Erro do cliente (ex.: `400 Bad Request`, `401 Unauthorized`)
* `5xx` — Erro do servidor (ex.: `500 Internal Server Error`)



---

### 🛠 Telnet, Postman e DevTools — Ferramentas práticas

**Telnet (requisições manuais):**

* Permite abrir conexão TCP e enviar requisições HTTP “cruas”:
```bash
telnet localhost 8000
GET / HTTP/1.1

```


* Útil para visualizar a **linha inicial**, headers e body sem abstrações.

**Postman:**

* Interface para criar requisições **GET/POST/PUT/DELETE**, configurar Body (`raw` → `JSON`) e visualizar respostas.
* Usar `Body` → `raw` → `JSON` para enviar payloads JSON.
* Exemplo de uso (POST):
* URL: `http://localhost:8000/public/login`
* Body:
```json
{"email": "geo@alura.com.br", "senha": "123"}

```





**DevTools (Network):**

* Inspecionar `Request URL`, `Request Method`, `Status Code`, `Payload` (JSON), headers e tempo de resposta.
* Identificar chamadas originadas por ações do front-end (ex.: formulário de cadastro).

---

### 🛡️ Segurança: HTTP vs HTTPS / TLS / Certificados

**Problema com HTTP:**

* Requisições HTTP via **texto puro** podem ser interceptadas (ex.: e-mail e senha aparecem legíveis).

**Solução: HTTPS (TLS):**

* HTTPS cifra o tráfego via **TLS**, protegendo confidencialidade e integridade.
* Em desenvolvimento, podem ser usados **certificados autoassinados**; em produção, obter certificados de CAs confiáveis.

**Comandos e verificações (observados nas aulas):**

* **Gerar certificado autoassinado (OpenSSL):**
```bash
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 \
  -keyout server.key -out server.crt

```


* **Inspecionar certificado:**
```bash
openssl x509 -in server.crt -text

```


* **Inspecionar chave privada:**
```bash
openssl rsa -in server.key -text -noout

```



**Exemplo básico de servidor HTTPS em Node.js (trecho observado):**

```javascript
const https = require('https')
const fs = require('fs')

// `server` = instância do Express / app já configurada
https.createServer(
  {
    key: fs.readFileSync('server.key'),
    cert: fs.readFileSync('server.crt')
  },
  server
).listen(8000, () => {
  console.log("API disponível em https://localhost:8000")
})

```

**Wireshark — inspeção de tráfego:**

* Filtros usados nas aulas:
* HTTP (texto): `tcp.port == 8000 && http`
* TLS/HTTPS (cifrado): `tcp.port == 8000 && tls`


* Observação: com HTTP foi possível visualizar o `POST /public/login` e o JSON com e-mail/senha; com TLS os pacotes aparecem como `Application Data` (conteúdo não legível).

**Chaves e responsabilidades:**

* `server.crt` → certificado (contém chave pública e dados de identidade).
* `server.key` → chave privada (NUNCA deve ser divulgada/publicada).
* Vazamento da chave privada compromete a confidencialidade das comunicações.

---

### 📦 APIs e Projeto AluraBooks (exemplos práticos)

**Endpoints observados (back-end local):**

* `GET  http://localhost:8000/livros`
* `GET  http://localhost:8000/categorias`
* `POST http://localhost:8000/livros`

**Estrutura típica de um objeto `livro` (observada):**

```json
{
  "id": 1,
  "categoria": 3,
  "titulo": "Novo livro",
  "slug": "novo-livro",
  "descricao": "Livro do curso HTTP",
  "isbn": "978-65-1111-11-1",
  "numeroPaginas": 200,
  "publicacao": "2023-01-01",
  "autor": 1,
  "opcoesCompra": [{"id":1,"titulo":"E-book","preco":29.9}],
  "sobre": "Compre esse livro e aprenda tudo sobre HTTP."
}

```

**Filtragem via query params (exemplo):**

```http
GET http://localhost:8000/livros?categoria=3
# Retorna livros cuja categoria = 3

```

**Criação de recurso (POST):**

* Fazer POST com `Content-Type: application/json` e JSON no body.
* Resposta esperada: **HTTP 201 Created**.
* Verificar inclusão com `GET /livros`.

**Documentação HTML da API (observação prática):**

* Ao criar rota com HTML, definir `Content-Type: text/html` para que o navegador renderize:

```javascript
server.get('/public/docs', (req, res) => {
  const meuHtml = `
    <h1>Documentação da API</h1>
    <ul>
      <li>GET /livros</li>
      <li>POST /livros</li>
      <li>GET /categorias</li>
    </ul>
  `
  res.status(200).contentType("text/html").send(meuHtml)
})

```

* Se `Content-Type` estiver como `text/plain`, o HTML será exibido como texto cru.

**Headers e formatos:**

* `Content-Type: application/json` → resposta em JSON (máquina).
* `Content-Type: text/html` → resposta renderizável por navegador (humano).
* `Accept` (cliente) e `Content-Type` (resposta/req.body) são conceitos a memorizar.

---

## 📌 Observações Importantes

* Todo o conteúdo deste README foi compilado **apenas** a partir dos resumos das aulas assistidas (Alura) — **nenhuma informação externa foi adicionada**.
* Exemplos e comandos refletem exercícios locais com `http://localhost:8000` (projeto AluraBooks).
* Use certificados autoassinados apenas em desenvolvimento; em produção utilize CAs confiáveis.
* Nunca comitar `server.key` ou outras chaves privadas em repositórios públicos.
* Para testes repetíveis e documentação de APIs, prefira Postman e rotas de documentação em HTML (com `Content-Type: text/html`).
* Em depuração: inspecione `Request URL`, `Method`, `Status`, `Payload`, e headers na aba **Network** do DevTools.

---

## 🚀 Próximos Estudos

* Estrutura de **URLs**: esquema, host, porta, caminho, query.
* Resolução de nomes e **DNS** em produção.
* **Formatação e validação do body** (JSON, form-data) e parâmetros no HTTP.
* **Aprofundar segurança**: TLS, gestão de certificados, refresh tokens e políticas de sessão (cookies vs tokens).
* Acompanhar evolução de protocolos (**HTTP/2** e **HTTP/3/QUIC**) e sua adoção prática.

---

## 📎 Referências

* **Plataforma Alura** — cursos e aulas sobre HTTP, APIs, segurança (base dos resumos).
* **Projeto local**: AluraBooks (`http://localhost:8000`) — exemplos práticos usados nas aulas.
* **Ferramentas citadas**: DevTools (Network), Postman, Telnet, Wireshark, OpenSSL, Node.js (https).



```

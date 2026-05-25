# LangChain e Python: Criando Ferramentas com a OpenAI

Projetos desenvolvidos no primeiro módulo do Nível 1 da formação de Engenharia de Agentes de IA. O foco é entender os fundamentos do LangChain, LCEL e LangGraph para construção de cadeias e agentes com LLMs.

---

## Projetos

### 1. Chatbot com Memória (`main_chat.py`)
Chatbot de sugestões de viagens pelo Brasil com histórico de conversa por sessão.

**Conceitos abordados:**
- LCEL (LangChain Expression Language) com operador `|`
- `ChatPromptTemplate` para estruturar prompts
- `StrOutputParser` para extrair texto da resposta do modelo
- `InMemoryChatMessageHistory` para armazenar histórico
- `RunnableWithMessageHistory` para manter contexto entre perguntas

**Fluxo:**
```
Pergunta → Prompt formatado → GPT → Texto limpo → Histórico atualizado
```

---

### 2. Agente com Roteamento Condicional (`main_langgraph.py`)
Agente que decide automaticamente qual especialista responde — Sra. Praia ou Sr. Montanha — com base na pergunta do usuário.

**Conceitos abordados:**
- LangGraph com `StateGraph`
- Estado compartilhado entre nós com `TypedDict`
- Roteamento condicional com `add_conditional_edges`
- `with_structured_output` para forçar saída estruturada do modelo
- Execução assíncrona com `async/await` e `ainvoke`

**Fluxo:**
```
Pergunta → [rotear] → GPT decide: "praia" ou "montanha"
                          ↓                    ↓
                    [Sra. Praia]         [Sr. Montanha]
                          ↓                    ↓
                        [END]               [END]
```

---

### 3. RAG com PDFs de Seguros (`main_rag.py`)
Sistema de perguntas e respostas sobre documentos PDF de planos de seguro de viagem (Standard, Gold e Platinum), usando busca semântica para recuperar trechos relevantes antes de gerar a resposta.

**Conceitos abordados:**
- RAG (Retrieval-Augmented Generation)
- Carregamento de PDFs com `PyPDFLoader`
- Divisão de documentos com `RecursiveCharacterTextSplitter`
- Geração de embeddings com `OpenAIEmbeddings`
- Busca vetorial com `FAISS`
- Prompt com contexto recuperado

**Fluxo:**
```
Pergunta → vira vetor → FAISS busca os 2 trechos mais relevantes
                ↓
    Trechos + pergunta → GPT responde com base nos documentos
```

---

## Tecnologias

- Python 3.11
- LangChain 0.3.25
- LangGraph 0.4.8
- langchain-openai 0.3.22
- FAISS
- python-dotenv

## Como executar

1. Crie e ative o ambiente virtual:
```bash
py -3.11 -m venv langchain
langchain\Scripts\activate
```

2. Instale as dependências:
```bash
pip install -r requirements.txt
```

3. Configure a chave da OpenAI no arquivo `.env`:
```
OPENAI_API_KEY=sua-chave-aqui
```

4. Execute o script desejado:
```bash
python main_chat.py
python main.py
python rag.py
```

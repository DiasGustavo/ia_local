# Segundo Cérebro — Assistente de IA Local para o IFPB Sousa

> **Notebook compartilhado:** [Abrir no NotebookLM](https://notebook.google.com/notebook/cd60caf7-8ff0-4a8b-a784-de7173ee4ce1)

---

## 🎯 Objetivo

> *Reunir conhecimento sobre como implementar um assistente de IA localmente usando modelos leves de IA para ser usado por alunos e visitantes do campus de Sousa do IFPB.*

O foco deste segundo cérebro é o **fim** — montar e implantar um assistente funcional no campus —, sendo os modelos leves de IA o **meio** para viabilizar isso em hardware institucional limitado.

---

## 📋 Critérios de Curadoria de Fontes

Antes de entrar no Notebook, cada fonte foi avaliada pelos critérios abaixo, aplicados em dois níveis de prioridade:

### Nível 1 — Filtro Obrigatório (toda fonte passa por aqui)

| Critério | Definição |
|---|---|
| **Atualidade** | Publicado nos últimos 5 anos, com preferência para fontes mais recentes |
| **Credibilidade** | Autor ou organização verificável e com autoridade sobre o tema |

### Nível 2 — Filtro Contextual (aplicado conforme o propósito da fonte)

| Critério | Definição |
|---|---|
| **Aplicabilidade** | Mostra o processo funcionando na prática, não apenas em teoria |
| **Especificação técnica** | Compatível ou aplicável a hardware com processador Core i3 / AMD FX e 8 GB de RAM |

> [!NOTE]
> Fontes conceituais (ex.: o que é RAG, como funcionam modelos leves) têm exigência menor de **aplicabilidade** e **especificação técnica**, pois seu papel é construir entendimento, não guiar a instalação.

---

## 📚 Fontes Incluídas e Justificativas

### 🎬 Vídeos

| # | Link | Justificativa |
|---|---|---|
| 1 | [YouTube — vídeo 1](https://www.youtube.com/watch?v=jxejoffemHc) | Aprovado nos quatro critérios após análise do conteúdo |
| 2 | [YouTube — vídeo 2](https://www.youtube.com/watch?v=tyyIy09BlOQ) | Aprovado nos quatro critérios após análise do conteúdo |
| 3 | [YouTube — vídeo 3](https://www.youtube.com/watch?v=XIrnmCtRCEI) | Aprovado nos quatro critérios após análise do conteúdo |

### 📄 Textos

| # | Link | Justificativa |
|---|---|---|
| 1 | [Hugging Face](https://huggingface.co/) | Principal repositório global de modelos de IA — alta credibilidade, fonte primária de modelos e documentação |
| 2 | [Neurônios Artificiais — IA local sem GPU](https://neuroniosartificiais.com.br/rodar-ia-local-sem-gpu/) | Conteúdo em português, prático, voltado especificamente para execução sem GPU |
| 3 | [MobileTime — IA sem GPU poderosa](https://www.mobiletime.com.br/noticias/16/11/2023/nao-e-preciso-gpu-poderosa-em-celular-para-rodar-ia-diz-vp-da-nvidia/) | Publicado em novembro/2023, dentro do limite de 5 anos; fonte jornalística verificável com declaração de VP da NVIDIA |
| 4 | [Diário Econômico — Microsoft cria IA sem GPU](https://www.diarioeconomico.co.mz/2025/05/13/trends/ai/microsoft-cria-ia-que-funciona-sem-gpu-e-promete-revolucionar-o-sector/) | Publicado em maio/2025; trata do BitNet b1.58 da Microsoft, diretamente relevante para hardware sem GPU |

> [!IMPORTANT]
> Uma URL duplicada foi identificada e removida durante a curadoria:
> `https://neuroniosartificiais.com.br/rodar-ia-local-sem-gpu/#google_vignette` aponta para a mesma página da fonte 2 acima — o sufixo `#google_vignette` é apenas um parâmetro de rastreamento do Google.

---

## 🧭 Diretriz de Comportamento do Notebook

O assistente deve:

- Responder **apenas com base nos documentos e fontes fornecidos**
- Priorizar informações compatíveis com **hardware sem GPU dedicada** (Core i3 / AMD FX, 8 GB RAM)
- Indicar **de qual fonte ou trecho** veio a informação ao responder
- Não especular sobre configurações ou ferramentas fora do escopo das fontes
- Contextualizar as respostas para o cenário de **implantação institucional local** no campus de Sousa do IFPB

---

## 💬 Perguntas Feitas ao Notebook e Respostas Obtidas

---

## Pergunta 1
> **"Existe algum modelo que eu consiga botar para funcionar em um computador com processador core i3 de terceira geração e com 8GB de RAM? Liste os modelos e faça um tutorial de como fazer isto."**

### Resposta
Sim, é perfeitamente viável rodar modelos de Inteligência Artificial localmente em um computador equipado com um processador Intel Core i3 de 3ª geração e 8 GB de memória RAM, mesmo sem possuir uma placa de vídeo (GPU) dedicada [41, 43]. Nesses cenários, ferramentas de execução como o **Ollama** ou **LM Studio** utilizam automaticamente a CPU e a memória RAM do sistema [41, 45].

Para garantir o funcionamento em sistemas com 8 GB de RAM, a regra principal é selecionar **modelos compactos (de 2B a 3B de parâmetros)** e utilizar técnicas de **quantização (como Q4 ou Q5)**, que reduzem drasticamente o tamanho do arquivo na memória e aceleram a resposta no processador com perda mínima de qualidade [44, 45].

#### Modelos Recomendados
1. **Phi-3 (Microsoft):** Modelo pequeno (2B a 3B de parâmetros), rápido, eficiente e altamente capaz para execução via CPU [43, 46].
2. **Gemma 2B (Google):** Leve e muito eficiente para rodar com pouca memória RAM [44, 46].
3. **TinyLlama / Llama 3 Quantizado:** Versões altamente compactas desenhadas especificamente para máquinas mais modestas [44].
4. **Mistral 7B (Quantizado Q4):** Representa o limite superior confortável para um sistema sem GPU; funcionará na CPU, embora responda de forma mais lenta [44, 46, 47].
5. **BitNet b1.58 (Microsoft / `bitnet.cpp`):** Arquitetura inovadora de 1-bit criada para operar em CPUs comuns sem necessidade de GPU, substituindo números flutuantes complexos por adições simples (-1, 0, 1) [75, 102, 103].
6. **Colibri (Engine Open Source):** Motor em C puro que gerencia partes de modelos MoE (*Mixture of Experts*) entre memória e disco para rodar sem GPU dedicada [25, 26, 29].

---

#### Tutorial Passo a Passo para Configuração Local

1. **Download e Instalação da Ferramenta de Execução:**
   * Baixe e instale o **Ollama** ou o **LM Studio** [41, 45].
   * O software detecta a ausência de uma GPU dedicada e configura a CPU para o processamento automaticamente [41, 45].

2. **Preparação da Memória RAM:**
   * Com 8 GB de RAM, o limite ideal são modelos de até 3B [44]. Feche navegadores e programas pesados em segundo plano antes de iniciar o modelo [45].

3. **Baixar e Executar o Modelo:**
   * Abra o Terminal ou Prompt de Comando (CMD).
   * Execute o comando do modelo desejado:
     * Para Phi-3: `ollama run phi3` [45]
     * Para Gemma 2B: `ollama run gemma:2b` [45]
   * O sistema baixará a versão quantizada (Q4) e abrirá o chat no próprio terminal [45].

4. **Boas Práticas de Desempenho:**
   * Dê preferência sempre a modelos quantizados em Q4 ou Q5 [44, 45].
   * Utilize um armazenamento SSD para agilizar o carregamento inicial do modelo [45].
   * Se precisar treinar modelos pesados ou rodar IAs que excedam o hardware local, soluções em nuvem com GPUs remotas (como **Mimic PC** ou **Kaggle**) podem ser utilizadas complementarmente [2, 3, 8, 9].

---

## Pergunta 2
> **"É possível criar um assistente com esses modelos para treinar com a legislação, material e conteúdo sobre a instituição que eu trabalho?"**

### Resposta
Sim, é totalmente possível criar um assistente especializado na legislação e no conteúdo da sua instituição [9, 10, 41]. A metodologia mais recomendada e viável para o seu hardware (Core i3 + 8 GB RAM) é o **RAG (Retrieval-Augmented Generation / Geração Aumentada por Recuperação)**, em vez do re-treinamento total do modelo [9, 10, 41].

#### Por que o RAG é a melhor abordagem para o seu PC?
* **Consulta em Tempo Real:** O sistema busca trechos exatos dos seus documentos (PDFs, portarias, regulamentos) e os fornece como contexto para o modelo leve de IA (ex.: Phi-3 ou Gemma 2B) responder [9, 10, 41].
* **Privacidade e Segurança Total:** A execução permanece 100% local, garantindo que normas e documentos institucionais sigilosos não sejam enviados a servidores externos [8, 104].
* **Respostas Precisas sem "Alucinações":** O assistente fundamenta suas respostas diretamente nos textos fornecidos, indicando o documento e a página de origem [9, 10].
* **Sem Necessidade de Placa de Vídeo (GPU):** Ao contrário do *Fine-Tuning* (ajuste fino dos pesos da rede), que exigiria GPUs de alta capacidade com muita VRAM [8, 11, 103], o RAG consome pouca memória e roda tranquilamente na CPU [41, 45].

---

#### Passo a Passo Prático para Montar o Assistente Institucional

1. **Manter o Servidor de IA Ativo:**
   * Certifique-se de que o **Ollama** está instalado e executando um modelo leve na sua máquina (ex.: `ollama run phi3` ou `ollama run gemma:2b`) [45].

2. **Instalar a Interface Visual (ex.: AnythingLLM ou Open WebUI):**
   * Baixe e instale uma ferramenta como o **AnythingLLM**, que gerencia repositórios de documentos e se conecta diretamente ao Ollama [9, 10].

3. **Criar uma Área de Trabalho (Workspace) e Carregar Documentos:**
   * No aplicativo, crie um diretório de trabalho dedicado à sua instituição.
   * Faça o upload dos arquivos PDF, documentos Word e legislações institucionais.
   * Selecione a opção de processamento (*Save and Embed*) para criar o índice de busca vetorial local.

4. **Interagir com o Assistente:**
   * Faça perguntas diretamente no chat (ex.: *"Qual o procedimento correto segundo a Portaria X?"*). O assistente recuperará os trechos relevantes da legislação e responderá com precisão embasada [9, 10].

---

## Referências e Fontes Consultadas

1. **""Não tem Placa de Vídeo? Rode essa IA PESADA em QUALQUER PC!""** *(Vídeo do YouTube)* [Passagens 1–7]
   * Demonstração do uso de ambientes de cadernos de código na nuvem (Kaggle) para execução de modelos avançados sem depender do hardware local.
2. **"Achei a solução para você usar a IA local sem ter PLACA DE VÍDEO! @MIMICPC-td3xq"** *(Vídeo do YouTube)* [Passagens 8–24]
   * Apresentação da plataforma de GPU em nuvem Mimic PC para execução remota de modelos locais e Ollama.
3. **"Colibri: IA gigante no seu PC sem GPU? Como funciona"** *(Vídeo do YouTube)* [Passagens 25–29]
   * Explicação do motor em C puro Colibri e da distribuição inteligente de parâmetros entre RAM e disco.
4. **"IA Local sem GPU: 5 modelos que funcionam no PC fraco 2026"** *(Artigo Web)* [Passagens 41–74]
   * Detalhamento sobre requisitos de hardware, ferramentas (Ollama, LM Studio), modelos compactos (Phi-3, Gemma 2B, Mistral 7B Q4) e uso de quantização.
5. **"Microsoft Cria IA Que Funciona Sem GPU e Promete Revolucionar o Sector"** *(Diário Económico)* [Passagens 75–116]
   * Reportagem sobre o modelo BitNet b1.58 da Microsoft com arquitetura de 1-bit otimizada para CPUs convencionais.
6. **"Smartphones não precisam de GPU poderosa para rodar IA generativa"** *(Mobile Time)* [Passagens 117–124]
   * Entrevista e conceitos sobre a desalocação do processamento pesado de IA para serviços de inferência e nuvem.

---

## 🗂️ Próximos Passos Sugeridos

- [ ] Testar o Ollama com o Phi-3 ou Gemma 2B no hardware do campus
- [ ] Instalar e configurar o AnythingLLM
- [ ] Selecionar os documentos institucionais prioritários para a primeira versão do assistente
- [ ] Definir as perguntas mais frequentes que o assistente deverá responder
- [ ] Avaliar a necessidade de novas fontes conforme lacunas forem identificadas

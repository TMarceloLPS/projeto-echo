# PROJETO ECHO — ANTEPROJETO DE PESQUISA E DESENVOLVIMENTO TECNOLÓGICO

> **ECHO:** *Eletrofisiologia Cognitiva e Híbrida Operacional* (*Electrophysiological Cognitive & Hybrid Output*)  
> **Instituição:** Clube de Inovação Digital e de Tecnologia (CIDIT) — Escola de Especialistas da Aeronáutica (EEAR)

---

## 1. Identificação do Projeto

* **Título Acadêmico:** Projeto ECHO: Desenvolvimento de Interface Homem-Máquina Multimodal Vestível de Baixo Custo Baseada em Fusão Sensorial (EEG/sEMG) e Tokenização Adaptativa para Comunicação Silenciosa.
* **Área de Conhecimento:** Engenharia de Computação, Processamento Digital de Sinais Biomédicos, Sistemas Embarcados e Interação Homem-Máquina (IHM).
* **Subáreas:** Interfaces Cérebro-Computador Híbridas (*Hybrid BCI*), Ergonomia Cognitiva e Computação Vestível (*Wearables*).
* **Aplicação Alvo:** Operação computacional silenciosa (*hands-free* e *eyes-free*), ergonomia cognitiva em consoles críticos e tecnologias assistivas.

---

## 2. Problema Operacional e Justificativa

Em ambientes operacionais de alta demanda cognitiva e acústica — tais como salas de controle de tráfego aéreo, centros de operações de defesa, cabines de comando e oficinas de manutenção aeronáutica —, os operadores frequentemente enfrentam limitações severas nas interfaces tradicionais de entrada de dados:

1. **Indisponibilidade Manual (*Hands-Busy*):** A necessidade de operar consoles, ferramentas ou equipamentos impede o uso contínuo de teclados e mouses convencionais.
2. **Falha de Reconhecimento de Voz:** Comandos por áudio sofrem degradação crítica em ambientes com alto ruído ambiente (pistas, hangares, salas de fonia) e comprometem o sigilo operacional quando a comunicação precisa ser discreta.
3. **Limitações dos Sistemas BCI Convencionais:** Interfaces puramente baseadas em Eletroencefalografia (EEG) não-invasiva enfrentam baixa relação sinal-ruído ($\text{SNR}$) devido à atenuação provocada pelo crânio, além de sofrerem instabilidade causada pela não-estacionariedade do sinal cerebral diante de variações de humor, fadiga e estímulos auditivos externos (como música ou fonia de fundo).

**Justificativa da Proposta:** O **Projeto ECHO** propõe superar esses gargalos por meio de uma arquitetura vestível minimalista em formato de *headphone* circumaural que combina a **precisão neuromuscular da eletromiografia de superfície subvocal ($\text{sEMG}$)** com a **monitoração cognitiva cortical ($\text{EEG}$)**, utilizando algoritmos de **tokenização neural com auto-calibração contínua** e avaliando quantitativamente o impacto de estímulos musicais na estabilidade do sistema.

---

## 3. Objetivos

### 3.1. Objetivo Geral

Projetar, prototipar e validar uma interface homem-máquina multimodal vestível e de baixo custo, integrada a um chassi de *headphone*, capaz de decodificar comunicação silenciosa em tempo real por meio de tokenização adaptativa ($\text{EEG} + \text{sEMG}$) e mensurar o impacto de diferentes cenários auditivos na precisão do sistema.

### 3.2. Objetivos Específicos

* Desenvolver um sistema embarcado de aquisição biomédica multicanal baseado no microcontrolador ESP32-S3 com transmissão sem fio via Bluetooth Low Energy ($\text{BLE}$).
* Integrar sensores secos (*dry electrodes*) em um chassi ergonômico de *headphone* com haste occipital e haste lateral articulada, eliminando a necessidade de gel condutor ou múltiplos cabos corporais.
* Implementar um pipeline de processamento digital de sinais em Python para filtragem em tempo real, extração de matrizes de características e discretização em um dicionário (*Codebook*) de tokens neurais/musculares.
* Desenvolver um mecanismo de **auto-calibração contínua (*Online Learning*)** capaz de compensar desvios de linha de base (*baseline drift*) causados por alterações de estado emocional, fadiga ou estímulos sonoros.
* Executar um protocolo experimental controlado para quantificar a degradação e a adaptação da escrita silenciosa sob silêncio, ruído branco, música instrumental e música vocal.

---

## 4. Arquitetura do Sistema (Hardware e Software)

### 4.1. Arquitetura Física: Chassi *Headphone* Híbrido

Para maximizar o conforto operacional, a estabilidade mecânica do contato pele-eletrodo e o isolamento eletromagnético, toda a eletrônica será alojada nas conchas de um *headphone* circumaural adaptado:

| Estrutura do *Headphone* | Região Anatômica (Sistema 10-20) | Tipo de Sensor | Função Biomédica e Operacional |
| :--- | :--- | :--- | :--- |
| **Haste Lateral Articulada (*Boom*)** | Área de Broca ($F_7$) + Região Sub-mandibular / Masseter | Eletrodo Seco Plano ($\text{Ag/AgCl}$ / Ouro) | Captação de planejamento linguístico cortical ($\text{EEG}$) e impulsos neuromusculares da subvocalização silenciosa ($\text{sEMG}$). |
| **Almofadas / Conchas Auriculares** | Córtex Temporal ($T_7$) e Ossos Mastóides ($TP_9 / TP_{10}$) | Eletrodo Seco Plano + Transdutores de Áudio | Referência elétrica neutra (*Ground/Ref*), monitoramento da resposta auditiva à música e retorno sonoro discreto. |
| **Arco Superior** | Córtex Motor Primário ($C_z$) | Eletrodo Seco tipo Pente (*Spring-Loaded*) | Detecção de intenção motora (comandos binários de confirmação/envio) e índice de atenção ($\beta / \alpha$). |
| **Haste Posterior (Nuca)** | Córtex Occipital ($O_z$) | Eletrodo Seco tipo Pente (*Spring-Loaded*) | Monitoramento de ondas Alpha (fadiga/relaxamento) e suporte a gatilhos visuais ($\text{SSVEP}$) opcionais. |

**Blindagem Eletromagnética:** Os condutores dos alto-falantes internos serão fisicamente separados e isolados com malha blindada aterrada e fita de cobre no interior das conchas, evitando indução eletromagnética do áudio nos canais de microvolts ($\mu\text{V}$).

### 4.2. Pipeline de Processamento e Tokenização Neural

O fluxo de dados opera em janelas deslizantes de $\Delta t = 500\text{ ms}$ com sobreposição de $50\%$, estruturado em quatro camadas em Python:

1. **Pré-processamento e Filtragem Digital (`SciPy` / `BrainFlow`):**
   * Filtro *Notch* de $60\text{ Hz}$ (rejeição da rede elétrica).
   * Filtro Passa-Banda de $1\text{ Hz}$ a $45\text{ Hz}$ para os canais de $\text{EEG}$ (isolando bandas $\delta, \theta, \alpha, \beta, \gamma$).
   * Filtro Passa-Banda de $20\text{ Hz}$ a $250\text{ Hz}$ para o canal $\text{sEMG}$ sub-mandibular.
2. **Representação Matricial:**
   * Para cada janela temporal, o sistema constrói uma matriz de características $\mathbf{X} \in \mathbb{R}^{C \times F}$, onde $C$ representa os canais ativos e $F$ representa a densidade espectral de potência ($\text{PSD}$ via Transformada Rápida de Fourier — $\text{FFT}$) e parâmetros temporais ($\text{RMS}$ e comprimento de onda).
3. **Quantização Vetorial (*Codebook* de Tokens):**
   * A matriz $\mathbf{X}$ é projetada em um espaço latente previamente clusterizado, convertendo o sinal contínuo em um identificador discreto $T_k \in \{T_1, T_2, \dots, T_N\}$ (Token Neural/Fonético).
4. **Decodificação Contextual:**
   * A sequência de tokens $[T_{k-2}, T_{k-1}, T_k]$ alimenta um modelo de linguagem leve local, que resolve ambiguidades fonéticas pelo contexto gramatical e reconstrói palavras e frases sem necessidade de teclado virtual.

---

## 5. Auto-Calibração Adaptativa por Estado e Uso

Para mitigar a variação inter-sessão e intra-sessão causada por humor, estresse ou fadiga, o sistema implementa um ciclo duplo de adaptação:

1. **Calibração Rápida de Linha de Base (*Few-Shot Baseline* — $30\text{ s}$):**
   * No início da operação, o usuário subvocaliza 3 tokens-âncora (*"Confirmar"*, *"Apagar"*, *"Avançar"*). O algoritmo calcula o vetor de deslocamento médio $\vec{\mu}_{\text{shift}}$ entre a sessão atual e o banco histórico, recentrando os centroides do *Codebook* antes do uso.
2. **Aprendizado Contínuo Implícito (*Online Adaptation*):**
   * **Reforço Positivo:** Quando uma palavra decodificada é aceita pelo usuário (continuidade da escrita sem comando de correção), a matriz $\mathbf{X}$ correspondente atualiza suavemente o centroide do token utilizado por meio de média móvel exponencial:
     $$\mathbf{C}_{k}^{(t+1)} = (1 - \eta)\mathbf{C}_{k}^{(t)} + \eta \mathbf{X}^{(t)}$$
     onde $\eta \in (0, 1)$ representa a taxa de aprendizagem adaptativa.
   * **Reforço Negativo e Detecção de Erro ($\text{ErrP}$):** Quando o usuário aciona o comando de exclusão ou o canal frontal detecta um Potencial Relacionado ao Erro (*Error-Related Potential* — $\text{ErrP}$), a amostra é descartada e o limiar de confiança da classificação é recalibrado automaticamente.

---

## 6. Protocolo Experimental: Interferência Auditiva e Musical

Para avaliar a robustez da interface em condições realistas de trabalho e validar a capacidade de auto-calibração, será conduzido um experimento controlado em **4 condições acústicas** (reproduzidas diretamente pelos transdutores do *headphone* em volume padronizado de $60\text{ dB SPL}$):

1. **Condição 1 — Silêncio Ambiental (*Baseline*):** Referência pura de desempenho sem estímulo auditivo externo.
2. **Condição 2 — Ruído Branco / Rosa Contínuo:** Avaliação do efeito de mascaramento acústico estacionário sobre o córtex temporal.
3. **Condição 3 — Música Instrumental (Andamento constante, sem vocal):** Avaliação da sincronização rítmica e modulação das ondas $\alpha$ e $\beta$ sem disputa semântica.
4. **Condição 4 — Música Vocal no Idioma Nativo (Português):** Cenário crítico de interferência cognitiva, onde o processamento auditivo verbal compete diretamente com a Área de Broca ($F_7$) e o planejamento da subvocalização.

Em cada condição, o participante executará a transcrição silenciosa de um conjunto padronizado de 20 frases operacionais curtas, registrando-se os sinais brutos e as taxas de adaptação antes e após a ativação do algoritmo de *Online Learning*.

---

## 7. Métricas Científicas de Avaliação

Os resultados serão quantificados utilizando três métricas padrão da literatura internacional de Interfaces Cérebro-Computador:

1. **Relação Sinal-Ruído ($\text{SNR}$ — *Signal-to-Noise Ratio*):**
   $$\text{SNR}_{\text{dB}} = 10 \log_{10} \left( \frac{P_{\text{sinal}}}{P_{\text{ruído}}} \right)$$
   Mensura o quanto o estímulo musical e a movimentação degradam a potência útil nas bandas de interesse em comparação ao repouso.
2. **Taxa de Erro de Caracteres ($\text{CER}$ — *Character Error Rate*):**
   $$\text{CER} = \frac{S + D + I}{N} \times 100\%$$
   Onde $S$ é o número de substituições, $D$ de deleções, $I$ de inserções e $N$ o total de caracteres da frase-alvo.
3. **Taxa de Transferência de Informação ($\text{ITR}$ — *Information Transfer Rate*):**
   $$\text{ITR} = \frac{60}{T} \left[ \log_2 M + P \log_2 P + (1 - P) \log_2 \left( \frac{1 - P}{M - 1} \right) \right] \quad (\text{bits/min})$$
   Onde $M$ é o número de tokens selecionáveis no *Codebook*, $P$ é a acurácia de classificação ($0 < P < 1$) e $T$ é o tempo médio em segundos por seleção.

---

## 8. Orçamento Detalhado e Lista de Materiais (BOM)

O desenvolvimento está estruturado em **duas fases progressivas** para otimizar recursos e validar os algoritmos antes da integração mecânica final:

### Fase 1: Protótipo de Bancada e Validação Algorítmica

*Foco: Aquisição de 2 canais ($\text{EEG}$ temporal/Broca + $\text{sEMG}$ mandibular), filtragem digital, treinamento inicial do Codebook e testes preliminares de interferência musical.*

| Item | Especificação Técnica | Qtd. | Custo Unit. Estimado | Subtotal |
| :--- | :--- | :---: | :---: | :---: |
| Microcontrolador | Placa ESP32-S3 DevKitC N16R8 (Wi-Fi / BLE 5.0 / 8MB PSRAM) | 01 | R\$ 70,00 | R\$ 70,00 |
| Aquisição Biomédica | Módulo BioAmp EXG Pill (Amplificador de instrumentação EEG/EMG) | 02 | R\$ 115,00 | R\$ 230,00 |
| Eletrodos de Teste | Pacote com 50 eletrodos descartáveis Ag/AgCl + 2 cabos snap | 01 | R\$ 60,00 | R\$ 60,00 |
| Alimentação Isolada | Bateria LiPo 3.7V 1000mAh + Módulo carregador TP4056 + Protoboard | 01 | R\$ 65,00 | R\$ 65,00 |
| **Subtotal Fase 1** | | | | **R\$ 425,00** |

### Fase 2: Integração Vestível (Chassi *Headphone* + Canal Occipital)

*Foco: Embutimento eletrônico nas conchas do headphone, substituição por sensores secos reutilizáveis, adição do canal occipital ($O_z$) e blindagem eletromagnética.*

| Item | Especificação Técnica | Qtd. | Custo Unit. Estimado | Subtotal |
| :--- | :--- | :---: | :---: | :---: |
| Chassi Base | *Headphone* Over-Ear circumaural com conchas internas amplas | 01 | R\$ 120,00 | R\$ 120,00 |
| Expansão Biomédica | Módulo BioAmp EXG Pill extra (dedicado ao canal occipital $O_z$) | 01 | R\$ 115,00 | R\$ 115,00 |
| Eletrodos Secos Planos | Sensores secos reutilizáveis banhados a Ouro/AgCl (pele lisa) | 04 | R\$ 25,00 | R\$ 100,00 |
| Eletrodos Secos Pente | Sensores secos com pinos retráteis com mola (couro cabeludo) | 03 | R\$ 35,00 | R\$ 105,00 |
| Blindagem e Conexões | Cabo coaxial blindado fino (RG174), fita de cobre adesiva e conectores JST | 01 | R\$ 80,00 | R\$ 80,00 |
| Manufatura Aditiva | Filamento PLA/PETG para impressão 3D da haste occipital e suporte *boom* | — | Infraestrutura CIDIT | R\$ 0,00 |
| **Subtotal Fase 2** | | | | **R\$ 520,00** |

* **Investimento Total Estimado (Fases 1 + 2):** **R\$ 945,00** (com margem de variação cambial entre **R\$ 850,00 e R\$ 1.100,00**).

---

## 9. Cronograma de Execução (Ciclo Anual CIDIT)

| Etapa | Atividade Principal | Meses 1–2 | Meses 3–4 | Meses 5–6 | Meses 7–8 | Meses 9–10 |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **1** | Revisão bibliográfica e simulação em datasets públicos ($\text{PhysioNet}$) | X | | | | |
| **2** | Aquisição dos componentes da Fase 1 e montagem do protótipo de bancada | X | X | | | |
| **3** | Desenvolvimento do pipeline Python ($\text{FFT}$, matrizes e *Codebook* de tokens) | | X | X | | |
| **4** | Modelagem 3D e integração vestível no chassi *headphone* (Fase 2) | | | X | X | |
| **5** | Execução do protocolo experimental com os 4 cenários sonoros | | | | X | |
| **6** | Análise estatística ($\text{ITR, CER, SNR}$), redação do artigo e apresentação | | | | | X |

---

## 10. Plano de Publicação e Divulgação Científica

Os resultados obtidos ao longo do desenvolvimento serão estruturados para submissão em múltiplos níveis acadêmicos:

1. **Publicação Institucional (Força Aérea Brasileira):** Submissão do artigo completo para os periódicos científicos da **Academia da Força Aérea (AFA)** e da **Universidade da Força Aérea (UNIFA)**, destacando a aplicabilidade em ergonomia cognitiva e operação *hands-free* em ambientes ruidosos.
2. **Congressos Nacionais de Engenharia e Computação:** Submissão de trabalho técnico aos anais do **Congresso Brasileiro de Engenharia Biomédica (CBEB)** ou ao **Simpósio Brasileiro sobre Fatores Humanos em Sistemas Computacionais (IHC / SBC)**, utilizando dupla afiliação institucional (**EEAR / UNIVESP**).
3. **Repositório Aberto e Preprint:** Disponibilização do código-fonte dos filtros digitais, esquemas CAD das hastes impressas em 3D e conjunto de dados anonimizados no **GitHub**, acompanhado da publicação de *preprint* com registro **DOI** na plataforma **TechRxiv (IEEE)**.
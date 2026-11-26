# PROJETO ECHO — ANTEPROJETO DE PESQUISA E DESENVOLVIMENTO TECNOLÓGICO

> **ECHO:** *Eletrofisiologia Cognitiva e Híbrida Operacional* (*Electrophysiological Cognitive & Hybrid Output*)
>
> **Instituição:** Clube de Inovação Digital e de Tecnologia (CIDIT) — Escola de Especialistas da Aeronáutica (EEAR)

## 1. Identificação do Projeto

* **Título Acadêmico:** Projeto ECHO: Desenvolvimento de Interface Cérebro-Computador (BCI) Vestível de Baixo Custo Embarcada em Chassi Acústico com Tokenização Neural Adaptativa para Comunicação Silenciosa sob Interferência Auditiva.
* **Proponente:** Aluno CFS (Especialidade BCT — Controle de Tráfego Aéreo) / Membro do CIDIT.
* **Área de Conhecimento:** Engenharia de Computação, Processamento Digital de Sinais Biomédicos (DSP), Sistemas Embarcados e Interação Homem-Máquina (IHM).
* **Alvo de Submissão:** Clube de Inovação Digital e de Tecnologia (CIDIT — EEAR), com desdobramento para publicação científica (AFA, UNIFA, CBEB/SBEB e periódicos de Engenharia Biomédica).

## 2. Problema Operacional e Justificativa

Operadores em ambientes críticos de comando, controle e aviação frequentemente enfrentam cenários com alta carga auditiva (fonia intensa, alarmes sonoros e ruído ambiente) e restrição física ou tática para o uso de periféricos convencionais (teclados, telas táteis) ou comandos de voz.

Paralelamente, as Interfaces Cérebro-Computador (BCIs) não-invasivas tradicionais sofrem com três gargalos que impedem sua adoção fora de laboratórios clínicos:

1. **Desconforto e Complexidade Mecânica:** Toucas clínicas exigem gel condutor, múltiplos fios e longo tempo de preparação.
2. **Não-Estacionariedade do Sinal Cortical:** Oscilações no estado emocional, fadiga mental e humor deslocam a linha de base elétrica do cérebro ao longo do dia, degradando modelos estáticos.
3. **Vulnerabilidade a Estímulos Ambientais:** A literatura carece de métricas quantitativas sobre o quanto estímulos auditivos contínuos (como música de fundo ou comunicações de rádio) interferem na atividade cortical durante a decodificação de fala imaginada (*Imagined Speech*).

**Justificativa da Proposta:** O **Projeto ECHO** resolve esses gargalos ao integrar sensores secos de Eletroencefalografia ($\text{EEG}$) puramente corticais em um chassi ergonômico de *headphone* com haste occipital, combinando **auto-calibração contínua por estado cognitivo** e **quantização vetorial de padrões neurais (Tokens Neurais)** para comunicação 100% mental e discreta, sem depender de micro-contrações musculares.

## 3. Trabalhos Relacionados e Contribuição Original

### 3.1. Estado da Arte (Embasamento Científico)

A arquitetura do Projeto ECHO apoia-se em quatro pilares consolidados na neuroengenharia contemporânea:

* **Ear-EEG e Interfaces Vestíveis em Chassi Acústico (Looney et al., 2012; Debener et al., 2015):** Demonstraram que eletrodos secos posicionados ao redor do pavilhão auditivo e sobre os ossos mastóides captam ritmos corticais ($\alpha$, $\beta$) e potenciais evocados com relação sinal-ruído ($\text{SNR}$) viável para aplicações fora do laboratório.
* **Decodificação de Fala Imaginada via EEG (*Covert / Imagined Speech* — Cooney et al., 2019; Panachakel & Ramakrishnan, 2021):** Evidenciaram que o pensamento articulatório silencioso gera assinaturas espectrais e temporais mensuráveis nas regiões fronto-temporais esquerdas (Área de Broca e Córtex Auditivo), dispensando ativação muscular periférica.
* **Tokenização Neural e Quantização Vetorial (Défossez et al., 2023; VQ-VAE aplicado a sinais neurais):** Validaram o mapeamento de janelas contínuas de atividade cerebral em códigos discretos (*codebooks*) que alimentam modelos de linguagem contextuais para reconstrução de texto.
* **Adaptação Online via Potenciais Relacionados ao Erro (*ErrP* — Chavarriaga et al., 2014):** Estabeleceram o uso de respostas corticais automáticas à percepção de erro como sinal de reforço implícito para atualização contínua de classificadores sem interromper o usuário.

### 3.2. Contribuição Inédita do Projeto ECHO

Enquanto os estudos acima investigam cada técnica isoladamente em salas acusticamente isoladas, o **ineditismo do Projeto ECHO** reside em três contribuições integradas:

1. **Protocolo de Interferência Auditiva Controlada na Fala Imaginada:** Avaliação quantitativa inédita da degradação espectral e da resiliência de decodificadores neurais quando submetidos a diferentes cargas sonoras (silêncio, música instrumental, música vocal e fonia operacional).
2. **Arquitetura Híbrida Intra-Cortical em Headphone Único:** Fusão simultânea de três paradigmas puramente cerebrais — Fala Imaginada ($F_7/T_7$), Imaginação Motora ($C_3/C_z/C_4$) e Modulação Occipital ($O_1/O_z/O_2$) — embarcados em hardware aberto de baixo custo.
3. **Recentragem Dinâmica de Centroides sob Estresse Cognitivo:** Uso de aprendizado online leve (*Exponential Moving Average*) guiado por estado basal e $\text{ErrP}$ para impedir a perda de precisão quando o usuário alterna seu estado emocional ou insere estímulos musicais durante a operação.

## 4. Objetivos

### 4.1. Objetivo Geral

Projetar, construir e validar um protótipo de Interface Cérebro-Computador vestível de baixo custo em formato de *headphone* (**Projeto ECHO**), baseado exclusivamente em captação cortical ($\text{EEG}$), capaz de converter padrões mentais em tokens discretos para escrita silenciosa com auto-calibração contínua.

### 4.2. Objetivos Específicos

* **Hardware Vestível:** Adaptar um chassi de *headphone* circumaural com haste occipital acoplada para posicionar eletrodos secos nas regiões fronto-temporal ($F_7/T_7$), central motora ($C_3/C_z/C_4$), occipital ($O_1/O_z/O_2$) e mastóides ($TP_9/TP_{10}$), garantindo isolamento eletromagnético entre os transdutores de áudio e os canais de microvolts ($\mu\text{V}$).
* **Pipeline de Aquisição e DSP:** Implementar amostragem sincronizada em microcontrolador **ESP32-S3** ($250\text{–}500\text{ Hz}$) com transmissão via Bluetooth Low Energy ($\text{BLE}$) e filtragem digital em Python (Notch $60\text{ Hz}$, passa-banda $1\text{–}45\text{ Hz}$ e rejeição de artefatos oculares/musculares).
* **Tokenização Neural e Auto-Calibração:** Desenvolver um algoritmo de quantização vetorial com normalização basal rápida ($30\text{ s}$) e atualização contínua online modulada por estado cognitivo e detecção de $\text{ErrP}$.
* **Decodificação Contextual:** Integrar a sequência de tokens neurais a um modelo de linguagem leve para reconstrução probabilística de palavras e comandos sem necessidade de teclado virtual piscante.
* **Avaliação Experimental sob Estímulo Musical:** Mensurar e comparar o desempenho do sistema sob quatro condições auditivas controladas utilizando métricas padronizadas da literatura BCI.

## 5. Arquitetura do Sistema (Hardware e Software)

### 5.1. Topologia Sensorial no Chassi do Headphone (Sistema Internacional 10-20)

Para maximizar o conforto operacional, a estabilidade mecânica do contato pele-eletrodo e o isolamento eletromagnético, toda a eletrônica será alojada nas conchas de um *headphone* circumaural adaptado:

| Estrutura do *Headphone* | Região Anatômica (Sistema 10-20) | Tipo de Sensor | Função Biomédica e Operacional |
| :--- | :--- | :--- | :--- |
| **Conchas Auriculares** | Mastóides ($TP_9, TP_{10}$) | Eletrodo Seco Plano ($\text{Ag/AgCl}$ / Ouro) | Referência elétrica diferencial (`REF`), terra (`GND`) e entrega de áudio/feedback sonoro. |
| **Haste Lateral Esquerda** | Frontotemporal ($F_7 / T_7$) | Eletrodo Seco Plano na Têmpora | Captação da Área de Broca (fala imaginada), córtex auditivo e detecção de $\text{ErrP}$. |
| **Arco Superior** | Córtex Motor Primário ($C_3, C_z, C_4$) | Eletrodo Seco tipo Pente (*Spring-Loaded*) | Detecção de imaginação motora (comandos binários de confirmação/correção) e índice de atenção ($\beta / \alpha$). |
| **Haste Posterior (Nuca)** | Córtex Occipital ($O_1, O_z, O_2$) | Eletrodo Seco tipo Pente (*Spring-Loaded*) | Monitoramento de ondas $\alpha$ (fadiga/relaxamento) e suporte a modulações visuais auxiliares. |

**Blindagem Eletromagnética:** Os condutores dos alto-falantes internos serão fisicamente separados e isolados com malha blindada aterrada e fita de cobre no interior das conchas, evitando indução eletromagnética do áudio nos canais de microvolts ($\mu\text{V}$).

### 5.2. Pipeline de Processamento e Tokenização Neural

O fluxo de dados opera em janelas deslizantes de $\Delta t = 500\text{ ms}$ com sobreposição de $50\%$, estruturado em quatro camadas em Python:

1. **Pré-processamento e Filtragem Digital (`SciPy` / `MNE`):**
   * Filtro *Notch* IIR de $60\text{ Hz}$ (rejeição da rede elétrica).
   * Filtro Butterworth Passa-Banda de $1\text{ Hz}$ a $45\text{ Hz}$ para isolar os ritmos corticais ($\delta, \theta, \alpha, \beta, \gamma$).
   * Rejeição automática de janelas contaminadas por artefatos oculares ($\text{EOG}$) ou tensão muscular ($\text{EMG}$) com amplitude superior a $100\ \mu\text{V}$.

2. **Representação Matricial:**
   * Para cada janela temporal, o sistema constrói uma matriz de características $\mathbf{X} \in \mathbb{R}^{C \times F}$, onde $C$ representa os canais corticais ativos e $F$ representa a densidade espectral de potência ($\text{PSD}$ via Transformada Rápida de Fourier — $\text{FFT}$) nas bandas $\delta$ ($1\text{–}4\text{ Hz}$), $\theta$ ($4\text{–}8\text{ Hz}$), $\alpha$ ($8\text{–}13\text{ Hz}$), $\beta$ ($13\text{–}30\text{ Hz}$) e $\gamma$ ($30\text{–}45\text{ Hz}$).

3. **Quantização Vetorial (*Codebook* de Tokens Neurais):**
   * A matriz $\mathbf{X}$ normalizada é projetada em um espaço latente previamente clusterizado, convertendo o sinal contínuo em um identificador discreto $T_k \in \{T_1, T_2, \dots, T_N\}$:

$
\text{Token\_ID}_t = \arg\min_{k} \|\mathbf{z}_t - \mathbf{c}_k\|_2
$

4. **Decodificação Contextual:**
   * A sequência de tokens $[T_{k-2}, T_{k-1}, T_k]$ alimenta um modelo de linguagem leve local, que resolve ambiguidades pelo contexto gramatical e reconstrói palavras e frases sem necessidade de teclado virtual.

## 6. Auto-Calibração Adaptativa por Estado e Uso

Para mitigar a variação inter-sessão e intra-sessão causada por humor, estresse ou fadiga, o sistema implementa um ciclo duplo de adaptação:

1. **Calibração Rápida de Linha de Base (*Few-Shot Baseline* — $30\text{ s}$):**
   * No início da operação, o usuário realiza a imaginação mental de 3 tokens-âncora (*"Confirmar"*, *"Apagar"*, *"Avançar"*). O algoritmo calcula a média ($\mu_0$) e o desvio-padrão ($\sigma_0$) da sessão atual, aplicando normalização Z-Score dinâmica para recentrar os vetores antes do uso:

$$
\mathbf{z}_t = \frac{\mathbf{x}_t - \mu_t}{\sigma_t}
$$

2. **Aprendizado Contínuo Implícito (*Online Adaptation*):**
   * **Reforço Positivo:** Quando uma palavra decodificada é aceita pelo usuário (continuidade da escrita sem comando de correção), o vetor $\mathbf{z}_t$ correspondente atualiza suavemente o centroide do token utilizado por meio de média móvel exponencial:

$$
\mathbf{c}_{k}^{(t+1)} = (1 - \eta)\mathbf{c}_{k}^{(t)} + \eta \mathbf{z}_t
$$

   onde $\eta \in (0, 1)$ representa a taxa de aprendizagem adaptativa.

   * **Reforço Negativo e Detecção de Erro ($\text{ErrP}$):** Quando o usuário aciona o comando mental de exclusão ou o canal fronto-central detecta um Potencial Relacionado ao Erro (*Error-Related Potential* — $\text{ErrP}$), a amostra é descartada e o limiar de confiança da classificação é recalibrado automaticamente.

## 7. Protocolo Experimental: Interferência Auditiva e Musical

Para avaliar a robustez da escrita mental em condições realistas de trabalho e validar a capacidade de auto-calibração, será conduzido um experimento controlado em **4 condições acústicas** (reproduzidas diretamente pelos transdutores do *headphone* em volume padronizado de $60\text{ dB SPL}$):

1. **Condição 1 — Silêncio Ambiental (*Baseline*):** Referência pura de desempenho sem estímulo auditivo externo.
2. **Condição 2 — Ruído Branco / Rosa Contínuo:** Avaliação do efeito de mascaramento acústico estacionário sobre o córtex temporal.
3. **Condição 3 — Música Instrumental (Andamento constante, sem vocal):** Avaliação da sincronização rítmica e modulação das ondas $\alpha$ e $\beta$ sem disputa semântica.
4. **Condição 4 — Música Vocal no Idioma Nativo (Português):** Cenário crítico de interferência cognitiva, onde o processamento auditivo verbal compete diretamente com a Área de Broca ($F_7$) durante a fala imaginada.

Em cada condição, o participante executará a transcrição mental de um conjunto padronizado de 20 frases operacionais curtas, registrando-se os sinais brutos e as taxas de adaptação antes e após a ativação do algoritmo de *Online Learning*.

## 8. Métricas Científicas de Avaliação

Os resultados serão quantificados utilizando três métricas padrão da literatura internacional de Interfaces Cérebro-Computador:

1. **Relação Sinal-Ruído ($\text{SNR}_{\text{dB}}$ — *Signal-to-Noise Ratio*):**

$$
\text{SNR}_{\text{dB}} = 10 \log_{10} \left( \frac{P_{\text{sinal}}}{P_{\text{ruído}}} \right)
$$

   Mensura o quanto o estímulo musical e a movimentação degradam a potência útil nas bandas de interesse em comparação ao repouso.

2. **Taxa de Erro de Caracteres ($\text{CER}$ — *Character Error Rate*):**

$$
\text{CER} = \frac{S + D + I}{N} \times 100\%
$$

   Onde $S$ é o número de substituições, $D$ de deleções, $I$ de inserções e $N$ o total de caracteres da frase-alvo.

3. **Taxa de Transferência de Informação ($\text{ITR}$ — *Information Transfer Rate*):**

$$
\text{ITR} = \left( \log_2 M + P \log_2 P + (1 - P) \log_2 \left( \frac{1 - P}{M - 1} \right) \right) \times \frac{60}{T}
$$

   Expressa em $\text{bits/min}$, onde $M$ é o número de tokens selecionáveis no *codebook*, $P$ é a acurácia de classificação ($0 < P < 1$) e $T$ é o tempo médio em segundos por seleção.

## 9. Orçamento Detalhado e Lista de Materiais (BOM)

O desenvolvimento está estruturado em **duas fases progressivas** para otimizar recursos e validar os algoritmos antes da integração mecânica final:

### Fase 1: Protótipo de Bancada e Validação Algorítmica

*Foco: Aquisição cortical de 2 canais ($F_7/T_7$ e $C_z$), filtragem digital em Python e treino inicial dos centroides.*

| Item | Especificação Técnica | Qtd. | Custo Unit. Estimado | Subtotal |
| :--- | :--- | :---: | :---: | :---: |
| Microcontrolador | Placa ESP32-S3 DevKitC N16R8 (Wi-Fi / BLE 5.0 / 8MB PSRAM) | 01 | R\$ 70,00 | R\$ 70,00 |
| Aquisição Biomédica | Módulo BioAmp EXG Pill (configurado para ganho e banda $\text{EEG}$) | 02 | R\$ 115,00 | R\$ 230,00 |
| Eletrodos de Teste | Pacote com 50 eletrodos descartáveis $\text{Ag/AgCl}$ + 2 cabos snap | 01 | R\$ 60,00 | R\$ 60,00 |
| Alimentação Isolada | Bateria LiPo 3.7V 1000mAh + Módulo carregador TP4056 + Protoboard | 01 | R\$ 65,00 | R\$ 65,00 |
| **Subtotal Fase 1** | | | | **R\$ 425,00** |

### Fase 2: Integração Vestível (Chassi *Headphone* + Canal Occipital)

*Foco: Embutimento eletrônico nas conchas do headphone, substituição por sensores secos reutilizáveis, adição do canal occipital ($O_z$) e blindagem eletromagnética.*

| Item | Especificação Técnica | Qtd. | Custo Unit. Estimado | Subtotal |
| :--- | :--- | :---: | :---: | :---: |
| Chassi Base | *Headphone* Over-Ear circumaural com conchas internas amplas | 01 | R\$ 120,00 | R\$ 120,00 |
| Expansão Biomédica | Módulo BioAmp EXG Pill extra (dedicado ao canal occipital $O_z$) | 01 | R\$ 115,00 | R\$ 115,00 |
| Eletrodos Secos Planos | Sensores secos reutilizáveis banhados a Ouro/$\text{AgCl}$ (pele lisa) | 04 | R\$ 25,00 | R\$ 100,00 |
| Eletrodos Secos Pente | Sensores secos com pinos retráteis com mola (couro cabeludo) | 03 | R\$ 35,00 | R\$ 105,00 |
| Blindagem e Conexões | Cabo coaxial blindado fino (RG174), fita de cobre adesiva e conectores JST | 01 | R\$ 80,00 | R\$ 80,00 |
| Manufatura Aditiva | Filamento PLA/PETG para impressão 3D da haste occipital e suporte *boom* | — | Infraestrutura CIDIT | R\$ 0,00 |
| **Subtotal Fase 2** | | | | **R\$ 520,00** |

* **Investimento Total Estimado (Fases 1 + 2):** **R$ 945,00** (com margem de variação cambial entre **R$ 850,00 e R$ 1.100,00**).

## 10. Cronograma de Execução (Ciclo Anual CIDIT)

| Etapa | Atividade Principal | Meses 1–2 | Meses 3–4 | Meses 5–6 | Meses 7–8 | Meses 9–10 |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **1** | Revisão bibliográfica e simulação em datasets públicos ($\text{PhysioNet}$) | X | | | | |
| **2** | Aquisição dos componentes da Fase 1 e montagem do protótipo de bancada | X | X | | | |
| **3** | Desenvolvimento do pipeline Python ($\text{FFT}$, matrizes e *Codebook* de tokens) | | X | X | | |
| **4** | Modelagem 3D e integração vestível no chassi *headphone* (Fase 2) | | | X | X | |
| **5** | Execução do protocolo experimental com os 4 cenários sonoros | | | | X | |
| **6** | Análise estatística ($\text{ITR, CER, SNR}$), redação do artigo e apresentação | | | | | X |

## 11. Plano de Publicação e Divulgação Científica

Os resultados obtidos ao longo do desenvolvimento serão estruturados para submissão em múltiplos níveis acadêmicos:

1. **Publicação Institucional (Força Aérea Brasileira):** Submissão do artigo completo para os periódicos científicos da **Academia da Força Aérea (AFA)** e da **Universidade da Força Aérea (UNIFA)**, destacando a aplicabilidade em ergonomia cognitiva e operação *hands-free* em ambientes ruidosos.
2. **Congressos Nacionais de Engenharia e Computação:** Submissão de trabalho técnico aos anais do **Congresso Brasileiro de Engenharia Biomédica (CBEB)** ou ao **Simpósio Brasileiro sobre Fatores Humanos em Sistemas Computacionais (IHC / SBC)**, utilizando dupla afiliação institucional (**EEAR / UNIVESP**).
3. **Repositório Aberto e Preprint:** Disponibilização do código-fonte dos filtros digitais, esquemas CAD das hastes impressas em 3D e conjunto de dados anonimizados no **GitHub**, acompanhado da publicação de *preprint* com registro **DOI** na plataforma **TechRxiv (IEEE)**.

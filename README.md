# Projeto ECHO

**Eletrofisiologia Cognitiva e Híbrida Operacional** *(Electrophysiological Cognitive & Hybrid Output)*

Interface Cérebro-Computador (BCI) vestível de baixo custo embarcada em chassi acústico (headphone), baseada em captação cortical via Eletroencefalografia ($\text{EEG}$) e tokenização neural adaptativa para comunicação silenciosa sob interferência auditiva.

---

## Visão Geral

O **Projeto ECHO** investiga a viabilidade de decodificação de fala imaginada (*Imagined Speech*) e comandos motores mentais fora de ambientes laboratoriais isolados. O sistema integra sensores secos em um headphone modificado com haste occipital, utilizando processamento digital de sinais (DSP) em tempo real, auto-calibração contínua por estado cognitivo e quantização vetorial (*codebook* de tokens neurais) acoplada a um decodificador de linguagem contextual.

### Principais Diferenciais
* **Arquitetura Cortical:** Dispensa ativação muscular periférica (sEMG), operando pela fusão de Fala Imaginada ($F_7/T_7$), Imaginação Motora ($C_3/C_z/C_4$) e Modulação Occipital ($O_1/O_z/O_2$).
* **Auto-Calibração Contínua:** Normalização Z-Score dinâmica associada à detecção de Potenciais Relacionados ao Erro ($\text{ErrP}$) para atualizar centroides sem necessidade de retreino completo.
* **Protocolo de Interferência Auditiva:** Avaliação quantitativa da degradação espectral ($\text{SNR}_{\text{dB}}$), taxa de erro ($\text{CER}$) e velocidade ($\text{ITR}$) sob silêncio, música instrumental, música vocal e fonia operacional.

---

## Arquitetura do Sistema

```text
[ Eletrodos Secos (10-20) ] ──▶ [ BioAmp EXG Pill ] ──▶ [ ESP32-S3 (BLE 5.0) ]
                                                                 │
                                                                 ▼
[ Decoder Contextual (LLM) ] ◀── [ Codebook + ErrP ] ◀── [ DSP Python (Notch / FFT) ]
```

### Mapeamento Sensorial (Sistema Internacional 10-20)

| Componente | Posição 10-20 | Função Principal |
| :--- | :--- | :--- |
| **Conchas Auriculares** | $TP_9, TP_{10}$ | Referência diferencial (`REF`), terra (`GND`) e saída de áudio. |
| **Haste Lateral Esquerda** | $F_7 / T_7$ | Área de Broca (fala imaginada), córtex auditivo e detecção de $\text{ErrP}$. |
| **Arco Superior** | $C_3, C_z, C_4$ | Imaginação motora (confirmação/correção) e índice de atenção ($\beta/\alpha$). |
| **Haste Posterior** | $O_1, O_z, O_2$ | Monitoramento de ritmo $\alpha$ e fadiga cognitiva. |

---

## Estrutura do Repositório

```text
projeto-echo/
├── docs/
│   ├── anteprojeto_cidit_bci.md   # Anteprojeto técnico completo (CIDIT / Publicações)
│   └── referencias/               # Artigos base (Ear-EEG, Imagined Speech, VQ-VAE, ErrP)
├── firmware/                      # Código embarcado C++ (ESP32-S3 + ADC + BLE)
├── dsp_ia/                        # Filtros digitais, extração FFT, Z-Score e Tokenização
├── hardware_3d/                   # Modelos STL da haste occipital e suportes de eletrodos
└── README.md                      # Documentação principal do repositório
```

---

## Documentação e Referências

* **[Anteprojeto Técnico Completo](docs/anteprojeto_cidit_bci.md):** Detalhamento teórico, protocolo experimental em 4 cenários sonoros, métricas matemáticas, orçamento por fases e cronograma de 16 semanas.
* **Embasamento Científico:** Looney et al. (2012) & Debener et al. (2015) (*Ear-EEG*); Cooney et al. (2019) & Panachakel & Ramakrishnan (2021) (*Imagined Speech*); Défossez et al. (2023) (*Neural Tokenization*); Chavarriaga et al. (2014) (*ErrP*).

---

## Status do Projeto

* [x] Definição da arquitetura cortical e revisão bibliográfica
* [x] Redação do anteprojeto técnico para submissão ao CIDIT
* [ ] Implementação e validação do pipeline DSP/FFT em Python
* [ ] Montagem da Fase 1 em bancada (ESP32-S3 + BioAmp EXG Pill)
* [ ] Integração vestível no chassi acústico (Fase 2) e coleta experimental

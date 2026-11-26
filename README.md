<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,20,24&height=200&section=header&text=Projeto%20ECHO&fontSize=58&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=BCI%20Vest%C3%ADvel%20%E2%80%A2%20EEG%20%E2%80%A2%20Tokeniza%C3%A7%C3%A3o%20Neural&descSize=18&descAlignY=58" width="100%" alt="Projeto ECHO"/>

**Eletrofisiologia Cognitiva e Híbrida Operacional**
*(Electrophysiological Cognitive & Hybrid Output)*

<br/>

<img src="https://img.shields.io/badge/Status-Pesquisa%20em%20andamento-F59E0B?style=for-the-badge"/>
<img src="https://img.shields.io/badge/P%26D-CIDIT-1E293B?style=for-the-badge&logo=airplayaudio&logoColor=A78BFA"/>
<img src="https://img.shields.io/badge/ESP32--S3-E7352C?style=for-the-badge&logo=espressif&logoColor=white"/>
<img src="https://img.shields.io/badge/BLE%205.0-0082FC?style=for-the-badge&logo=bluetooth&logoColor=white"/>
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white"/>

</div>

<br/>

Interface Cérebro-Computador (BCI) vestível de baixo custo embarcada em chassi acústico (headphone), baseada em captação cortical via Eletroencefalografia ($\text{EEG}$) e tokenização neural adaptativa para comunicação silenciosa sob interferência auditiva.

---

## <img src="https://api.iconify.design/lucide/brain.svg?color=%2338bdf8" height="26" align="absmiddle"/> Visão Geral

O **Projeto ECHO** investiga a viabilidade de decodificação de fala imaginada (*Imagined Speech*) e comandos motores mentais fora de ambientes laboratoriais isolados. O sistema integra sensores secos em um headphone modificado com haste occipital, utilizando processamento digital de sinais (DSP) em tempo real, auto-calibração contínua por estado cognitivo e quantização vetorial (*codebook* de tokens neurais) acoplada a um decodificador de linguagem contextual.

### Principais Diferenciais

<img src="https://api.iconify.design/lucide/network.svg?color=%2338bdf8" height="18" align="absmiddle"/> **Arquitetura Cortical:** dispensa ativação muscular periférica (sEMG), operando pela fusão de Fala Imaginada ($F_7/T_7$), Imaginação Motora ($C_3/C_z/C_4$) e Modulação Occipital ($O_1/O_z/O_2$).

<img src="https://api.iconify.design/lucide/refresh-cw.svg?color=%2338bdf8" height="18" align="absmiddle"/> **Auto-Calibração Contínua:** normalização Z-Score dinâmica associada à detecção de Potenciais Relacionados ao Erro ($\text{ErrP}$) para atualizar centroides sem necessidade de retreino completo.

<img src="https://api.iconify.design/lucide/audio-lines.svg?color=%2338bdf8" height="18" align="absmiddle"/> **Protocolo de Interferência Auditiva:** avaliação quantitativa da degradação espectral ($\text{SNR}_{\text{dB}}$), taxa de erro ($\text{CER}$) e velocidade ($\text{ITR}$) sob silêncio, música instrumental, música vocal e fonia operacional.

---

## <img src="https://api.iconify.design/lucide/workflow.svg?color=%2338bdf8" height="26" align="absmiddle"/> Arquitetura do Sistema

```mermaid
flowchart LR
  A["Eletrodos secos (10-20)"] --> B["BioAmp EXG Pill"]
  B --> C["ESP32-S3 (BLE 5.0)"]
  C --> D["DSP Python (Notch / FFT)"]
  D --> E["Codebook + ErrP"]
  E --> F["Decoder contextual (LLM)"]
```

### Mapeamento Sensorial (Sistema Internacional 10-20)

| Componente | Posição 10-20 | Função Principal |
| :--- | :--- | :--- |
| **Conchas Auriculares** | $TP_9, TP_{10}$ | Referência diferencial (`REF`), terra (`GND`) e saída de áudio. |
| **Haste Lateral Esquerda** | $F_7 / T_7$ | Área de Broca (fala imaginada), córtex auditivo e detecção de $\text{ErrP}$. |
| **Arco Superior** | $C_3, C_z, C_4$ | Imaginação motora (confirmação/correção) e índice de atenção ($\beta/\alpha$). |
| **Haste Posterior** | $O_1, O_z, O_2$ | Monitoramento de ritmo $\alpha$ e fadiga cognitiva. |

---

## <img src="https://api.iconify.design/lucide/folder-tree.svg?color=%2338bdf8" height="26" align="absmiddle"/> Estrutura do Repositório

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

## <img src="https://api.iconify.design/lucide/book-open.svg?color=%2338bdf8" height="26" align="absmiddle"/> Documentação e Referências

- **[Anteprojeto Técnico Completo](docs/anteprojeto_cidit_bci.md):** detalhamento teórico, protocolo experimental em 4 cenários sonoros, métricas matemáticas, orçamento por fases e cronograma de 16 semanas.
- **Embasamento científico:** Looney et al. (2012) & Debener et al. (2015) (*Ear-EEG*); Cooney et al. (2019) & Panachakel & Ramakrishnan (2021) (*Imagined Speech*); Défossez et al. (2023) (*Neural Tokenization*); Chavarriaga et al. (2014) (*ErrP*).

---

## <img src="https://api.iconify.design/lucide/list-checks.svg?color=%2338bdf8" height="26" align="absmiddle"/> Status do Projeto

- [x] Definição da arquitetura cortical e revisão bibliográfica
- [x] Redação do anteprojeto técnico para submissão ao CIDIT
- [ ] Implementação e validação do pipeline DSP/FFT em Python
- [ ] Montagem da Fase 1 em bancada (ESP32-S3 + BioAmp EXG Pill)
- [ ] Integração vestível no chassi acústico (Fase 2) e coleta experimental

<br/>

<div align="center">

Desenvolvido por [**Marcelo Tadeu**](https://github.com/TMarceloLPS) · [LinkedIn](https://www.linkedin.com/in/marcelo-tadeu-lopes-13b54433b/)

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,20,24&height=100&section=footer" width="100%" alt=""/>

</div>

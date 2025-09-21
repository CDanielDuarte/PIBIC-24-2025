
# 🧬 Análise Computacional da Expressão Gênica em Modelo *in vitro* de Cromoblastomicose

## 📌 Descrição do Projeto

Este projeto analisa a expressão gênica de *Fonsecaea pedrosoi*, principal agente etiológico da cromoblastomicose (CBM), uma micose crônica negligenciada.
Foram comparados dois estados celulares: **micélio (CMC)** e **células muriformes (CMT)**, a forma patogênica mais resistente. O objetivo é identificar genes diferencialmente expressos que possam servir como potenciais alvos terapêuticos.

A análise foi realizada com dados de RNA-seq processados pela pipeline [nf-core/rnaseq](https://nf-co.re/rnaseq), executada via [Nextflow](https://www.nextflow.io/).

## 🧪 Dados

* **Organismo:** *Fonsecaea pedrosoi*
* **Condições:**

  * **CMC** → micélio (forma saprofítica)
  * **CMT** → células muriformes (forma patogênica)
* **Sequenciamento:** Illumina, paired-end 2×150 bp
* **Amostras:** 4 réplicas biológicas por condição
* **Total de dados brutos:** \~13,37 GB

---

## ⚙️ Metodologia

1. **Pré-processamento**

   * Controle de qualidade: FastQC + MultiQC
   * Trimming: TrimGalore

2. **Execução da pipeline nf-core/rnaseq**

   * Ambiente: Nextflow (v25.04.2), Mamba (v1.5.9), Docker
   * Pipeline: nf-core/rnaseq (v3.20.0)
   * Comando:

     ```bash
     nextflow run main.nf \
       --input ./data/samplesheet.csv \
       --outdir ./results \
       --gtf ./data/genome/genomic.gtf \
       --fasta ./data/genome/genomic.fna \
       -profile docker
     ```

3. **Análises diferenciais (R/Colab)**

   * Pacotes: DESeq2, ggplot2, pheatmap
   * Gráficos: PCA, Volcano Plot, Heatmap

---

## 📊 Resultados

* Dados de alta qualidade (Q30+ na maior parte das leituras).
* Perfis transcricionais de micélio e CM são **claramente distintos**.
* **Genes upregulated em CMs:** resistência a estresses, adaptação metabólica, virulência.
* **Genes downregulated em CMs:** crescimento filamentoso e processos vegetativos.
* PCA e Heatmap confirmam agrupamento consistente por condição.

---

## ✅ Conclusão

A transição morfológica de micélio para célula muriforme em *F. pedrosoi* envolve uma **reprogramação gênica em larga escala**, fundamental para sua adaptação, resistência e virulência.
Este pipeline fornece uma base reprodutível para estudos futuros em transcriptômica fúngica e abre caminho para identificar potenciais alvos terapêuticos contra a cromoblastomicose.

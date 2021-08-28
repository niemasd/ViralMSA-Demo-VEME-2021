# ViralMSA Demo (VEME 2021)
In this demo, we will run [ViralMSA](https://github.com/niemasd/ViralMSA) on an example SARS-CoV-2 dataset.

## Step 1: Install ViralMSA and Minimap2
Before analyzing any data, you must first install ViralMSA and Minimap2:

* **ViralMSA:** https://github.com/niemasd/ViralMSA#installation
* **Minimap2:** https://github.com/lh3/minimap2#install

## Step 2: Download Unaligned SARS-CoV-2 Genome Sequence Dataset
We will be using a dataset of curated SARS-CoV-2 consensus sequences from [Kristian Andersen's lab](https://andersen-lab.com/). The original data repository can be found here:

https://github.com/andersen-lab/HCoV-19-Genomics

Rather than downloading the dataset from the Andersen lab's repository, however, we have merged the consensus sequences into a single file and have provided it in this repository, so you can just download the following file:

https://github.com/niemasd/ViralMSA-Demo-VEME-2021/raw/main/andersen_consensus_2021-08-28.fasta.gz

If you're using a command line environment, you can download this file using `wget`:

```bash
wget https://github.com/niemasd/ViralMSA-Demo-VEME-2021/raw/main/andersen_consensus_2021-08-28.fasta.gz
```

## Step 3: Decompress the Sequence Dataset
As you may have noticed, the dataset we have provided is gzip-compressed (hence the `.gz` file extension). We compressed the file so that it would be small enough to fit into a GitHub Repository and so that it would be easier for you to download, but before we can use it with ViralMSA, we need to decompress it. We can do so using `gunzip`:

```bash
gunzip andersen_consensus_2021-08-28.fasta.gz
```

This will decompress our original gzip-compressed file, `andersen_consensus_2021-08-28.fasta.gz`, into a new uncompressed FASTA file, `andersen_consensus_2021-08-28.fasta`. This is the file we will align using ViralMSA.

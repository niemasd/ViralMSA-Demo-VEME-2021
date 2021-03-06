# ViralMSA Demo (VEME 2021)
In this demo, we will run [ViralMSA](https://github.com/niemasd/ViralMSA) on an example dataset containing **19,294** SARS-CoV-2 consensus genome sequences.

## Step 1: Install ViralMSA and Minimap2
Before analyzing any data, you must first install ViralMSA and Minimap2:

* **ViralMSA:** https://github.com/niemasd/ViralMSA#installation
* **BioPython:** https://biopython.org/wiki/Download
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

## Step 4: Align Using ViralMSA
We can now perform reference-guided multiple sequence alignment using ViralMSA. We will run it as follows (replace `EMAIL_ADDRESS` with your actual email address):

```bash
ViralMSA.py -e EMAIL_ADDRESS -r SARS-CoV-2 -o viralmsa_output -s andersen_consensus_2021-08-28.fasta
```

* **`-e EMAIL_ADDRESS`:** Specifies your email address (needed for BioPython to download the reference genome from GenBank)
* **`-r SARS-CoV-2`:** Specifies the virus of interest so ViralMSA can download the appropriate reference genome
  * For a full list of virus names, see the keys of this dictionary: https://github.com/niemasd/ViralMSA/blob/master/ViralMSA.py#L31-L49
  * You can alternatively specify a GenBank accession number, or you can specify the path to a local file
  * But for this demo, just use `SARS-CoV-2` for the reference genome
* **`-o viralmsa_output`:** Specifies the output folder to be the folder `viralmsa_output` (which will be created by ViralMSA)
* **`-s andersen_consensus_2021-08-28.fasta`:** Specifies the input sequences we want to align to be the file `andersen_consensus_2021-08-28.fasta`

On my 8-core laptop that has a solid-state drive (SSD), ViralMSA took just over 30 seconds to align this dataset. This may take longer on your computer depending on the number of cores as well as the speed of your storage (e.g. HDD or SSD).

Once ViralMSA finishes running, you can find the output multiple sequence alignment in a file named `andersen_consensus_2021-08-28.fasta.aln` within the `viralmsa_output` directory created by ViralMSA. In general, the ViralMSA log will tell you exactly where the output multiple sequence alignment is located, e.g. the following line (should be the last line of the log output):

```
[2021-08-28 13:12:30] Multiple sequence alignment complete: /home/niema/ViralMSA-Demo-VEME-2021/viralmsa_output/andersen_consensus_2021-08-28.fasta.aln
```

## Conclusion
Congratulations! You've just finished aligning almost 20,000 SARS-CoV-2 consensus genome sequences using ViralMSA! If you wish to view the input sequences or the output multiple sequence alignment, you can use a visualization tool such as [Jalview](https://www.jalview.org/). You may notice that ViralMSA included the reference genome as the first sequence
in the output multiple sequence alignment for convenience as well as for context. However, if you wish to omit the reference genome from ViralMSA's output, you can use the `--omit_ref` argument when you run ViralMSA.

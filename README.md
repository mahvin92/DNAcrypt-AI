<img width="200" height="200" alt="DNAcrypt-logo-3" src="https://github.com/user-attachments/assets/9c545cff-dfd2-4a4e-806c-cd12d152ee51" />

# DNAcrypt-AI
An artificial intelligence that generates, encrytps, and decrypts passwords and cryptographic keys using the human genome.

DNAcrypt-AI was built using [FAS2rDNA](https://fas2rdna.chordexbio.com) and [Covary](https://covary.chordexbio.com) through the [assemBold program](https://assembold.chordexbio.com/), with permission from [ChordexBio](https://chordexbio.com).

OBFD tag: 12/26


### Description
DNAcrypt-AI is founded on the intrinsic complexity, variation, unpredictability, and scale of the human genome. It works by generating a pseudo-genomic vocabulary, randomly sampled from more than 3 billion genomic loci across multiple chromosomes and genome assemblies (hg19 and hg38). This vocabulary consists of genomic coordinates, which are interpreted by FAS2rDNA to reconstitute DNA sequences that typically range from 1,000 to 50,000 nucleotides in length. The resulting collection of sequences forms a heterogeneous genomic corpus, containing structure and information that cannot be easily interpreted, decrypted, or recognized by visual inspection or conventional bioinformatics tools.

DNAcrypt-AI then leverages machine learning through Covary to extract latent sequence patterns from this reconstituted DNA vocabulary using a sequence-informed framework. Covary uses feature expansion to encode the genetic sequences, making the framework very suitable for pattern extraction without reducibility to frequency-based signatures. This design makes the transformation pipeline irreversibly traceable. Finally, DNAcrypt-AI maps the vector embedding into alphanumeric and symbolic encodings, generating unique strings that can serve as passwords or cryptographic keys for the users.

The pipeline stores and encrypts the password or cryptographic key in a form of genomic coordinates, which can then be decrypted through DNAcrypt-AI.


### Architecture

The architecture of DNAcrypt-AI is relatively simple, yet largely dependent on two genome intelligence frameworks: [FAS2rDNA](https://github.com/mahvin92/FAS2rDNA) (a high-throughput DNA sequence reconstruction module) and [Covary](https://github.com/mahvin92/Covary) (a machine learning-based sequence intelligence framework). The detailed designs and internal architectures of these frameworks are described separately in their respective GitHub repositories. The image below maps the internal architecture of DNAcrypt-AI. 

<img width="3780" height="1890" alt="DNAcrypt architecture" src="https://github.com/user-attachments/assets/c4d07f7c-defa-473a-aafa-5d18075c6c8d" />

DNAcrypt-AI begins by accepting a user-specified workflow and key length. The user may select to generate 
- a pure alphanumeric sequence or alphanumeric-symbols.
- a key consisting of 6 to 90 characters, default of 12 (if not specified)

This input is used to generate a pseudo-DNA sequence (or a DNA hash) that encodes feature-level encrypted information. A predefined k-mer dictionary (k = 5) is then applied to encode alphanumeric characters and symbols into a traceable but non-reversible mapping space. For enhanced security, users may generate dynamic k-mer dictionaries with customized encoding combinations, enabling variable character-to-sequence mappings (see Usage below).

DNAcrypt-AI then performs a deep genome keyring process, producing an encrypted corpus of genomic coordinates across multiple human genome assemblies (hg19 and hg38). This process randomly samples chromosome identifiers, strand orientation, and start–end genomic coordinates, ensuring cross-assembly variability, structural diversity, and high sequence entropy.

To further increase cryptographic functions, DNAcrypt-AI generates a genome-derived sequence ensemble with a maximum sequence length of 50,000 nucleotides, aggregated into 1,024 independent vocabularies. The resulting genome-derived dictionary may contain up to 51.2 million nucleotides, making it computationally difficult to synthetically reproduce, memorize, reverse-engineer, or decrypt using conventional methods.

FAS2rDNA reconstructs the DNA sequences corresponding to the generated genomic coordinates using a high-throughput, multiprocessing reconstruction pipeline. The reconstructed sequences are then passed to Covary, which deconvolves and learns relational sequence patterns from the corpus. DNAcrypt-AI consumes the vector embeddings produced by Covary and maps the angular derivatives of the embeddings onto the k-mer dictionary. This final transformation renders a unique cryptographic sequence, which then effectively decrypted using the pseudo-DNA hash to produce a unique key with specific sequence length.


## Usage
DNAcrypt-AI can be used and tested as a Jupyter Notebook hosted on Google Colab. A working local implementation is under development and you can contact us to request an early access.

DNAcrypt-AI is very intuitive to use, requiring very minimal user input, as shown in the figure below. For encryption and password generation all you need is define: 1) string length 2) type of use case. For decryptoon all you need is provide the encrypted data.

<img width="3780" height="1890" alt="DNAcrypt user step" src="https://github.com/user-attachments/assets/e54936fb-729e-4fe0-ad66-6a5b74dacf7d" />



## Generate and encrypt a key:

1. Launch DNAcrypt-AI
There are a number of ways to launch DNAcrypt-AI:
- open the shareable versions of the jupyter notebooks here and choose the latest one or use the legacy version
- download the latest version of the notebook from the ```ipynb``` folder above and import it on your workspace
- load a version of the notebook directly from an opened Colab environment:

```
from IPython.display import HTML

notebook = "DNAcrypt-AI_colab_v1_0.ipynb" # -> change the version here
repo = "mahvin92/FAS2rDNA-Colab"
folder = "ipynb"

colab_url = f"https://colab.research.google.com/github/{repo}/blob/main/{folder}/{notebook}"
HTML(f'<a href="{colab_url}" target="_blank">Open {notebook} in Google Colab</a>')
```

2. Create a user configuration
- project_name: experiment code (optional)
- char_count: string lenght (default = 12)
- Use cases: Password= alphanumeric + symbol; Encryption= alphanumeric only (default = Password)

3. Run DNAcrypt-AI
```
Runtime -> Run all
```

4. Store your encrypted data
You can print or save a digital copy of your data, ensuring you can reproduce them for decryption later.


## Decrypt a key:
1. Launch DNAcrypt-AI
Similar to steps in **'Generate and encrypt a key'** section.

2. Modify user configuration
- Use cases: select 'Decryption'

3. Run DNAcrypt-AI
```
Runtime -> Run all
```
4. Upload your encrypted data
Note that in addition to the original 'DNAcrypt_metadata.json', you are required to upload the 'kmer_dict.json' if you encrypted your data using a customized kmer dictionary. Otherwise, DNAcrypt-AI will assume you used the static vocabularies. Note that the files could be renamed.

5. Wait for the key to be decrypted
This may take some time, roughly about 15 minutes or less, depending on the genome vocabularies you have.

## Encrypting and decrypting using a custom kmer dictionary:
There is no advantage to using a custom kmer dictionary, except in a situation where
- your key has been compromised;
- you want to recycle your encrption data but gets a refreshed sequence;
- you want to create a customized library suitable for your needs.

To generate a random kmer dictionary:
1. Launch DNAcrypt-AI as usual
2. Navigate to ```User configuration```, tick the box next to ```Custom``` under Kmer dictionary.
3. Run DNAcrypt-AI as usual
4. Save or upload the necessary file
   - For encryption, save the kmer_dict.json file along with DNAcrypt_metadata.json, which are your encrypted data.
   - For decryption, just upload the kmer_dict.json and DNAcrypt_metadata.json that were originally generated by DNAcrypt-AI.

Note that when you loss your custom kmer_dict.json, DNAcrypt-AI will not be able to recover the dictionary for you. Without correctly mapping your alphanumeric and symbol encodings to your kmer vocabularies, it's unlikely to decrypt your data.


## Storing your encrypted data
The encrypted data is light and does not take too much of storage (maximum of 100kb). You can store your encryption as follows:
1. Printed copy - private and secure but requires re-encoding to a digital copy later before using
2. Digital copy - ready to use but also allows others to decrypt once they get a copy of your data


## Troubleshooting
1. Decrypted key does not match the expected alphanumeric-symbol sequence
   - Re-run the decryption again or restart your session ```Runtime -> Restart session and run all```
2. DNAcrypt-AI session crashed due to RAM exhaustion
   - Machine learning is a RAM-hungry process, ensure that you are connected to a GPU support (e.g., T4) if you are using the Colab environment
3. DNAcrypt-AI is taking so long in reconstucting my genome corpus
   - The reconstruction of DNA sequences is loaded to FAS2rDNA, which requires to download either or both the hg19 and hg38 human genome assemblies. These assemblies are quite massive (~>3 GB each) in size. Please wait for a moment for these assemblies to be fetched and indexed
4. DNAcrypt-AI is not downloading the required file (e.g., DNAcrypt_metadata.json)
   - If DNAcrypt-AI executed without an error and yet did not produce a download, it means that your browser is blocking the process. You can fetch your encryption files from ```/content``` directory through the File browser.
5. I obtained a low entropy sequence
   - DNAcrypt-AI estimates the entropy of the generated password (the random assignment and sequence of alphanumeric-symbol charcaters), not necessarily the strength of the encryption. If you are not satisfied with the entropy estimate, you can always run DNAcrypt-AI again until you arrive at a desirable entropy. If you encounter issues while running DNAcrypt-AI multiple times, restarting your session can fix most issues ```Runtime -> Restart session and run all```
  
## Reporting
Comments and suggestions to improve DNAcrypt-AI are welcome. If you find any bug or problem, please open an issue.

## Citation
To follow

## License notice
Please see updated license here
To request for a validation license, please inquire at https://dnacrypt.chordexbio.com/

## Acknowledgement
Covary is powered by [Covary](https://github.com/mahvin92/Covary), [FAS2rDNA](https://github.com/mahvin92/FAS2rDNA), [ChordexBio](https://chordexbio.com), and [CodeEnigma](https://github.com/KrishnanSG/codeenigma), made with Python, and tested using Google Colab ❤️
  

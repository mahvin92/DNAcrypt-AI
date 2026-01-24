<img width="200" height="200" alt="DNAcrypt-logo-3" src="https://github.com/mahvin92/DNAcrypt-AI/blob/main/assets/DNAcrypt%20logo/DNAcrypt-logo-3.png" />

Latest: v.1.1 (updated 26/01/24)
# DNAcrypt-AI
**Human genome-based cryptography using artificial intelligence**

DNAcrypt-AI was built using [FAS2rDNA](https://fas2rdna.chordexbio.com) and [Covary](https://covary.chordexbio.com) through the [assemBold program](https://assembold.chordexbio.com/), with permission from [ChordexBio](https://chordexbio.com).

*Protocols are now out on protocols.io*
- DNAcrypt-AI protocol for generating and encrypting a secret key (DOI: http://dx.doi.org/10.17504/protocols.io.14egn12k6v5d/v1)
- DNAcrypt-AI protocol for generating and encrypting a password (DOI: http://dx.doi.org/10.17504/protocols.io.bp2l6e951gqe/v1)
- Decryption of genome-encoded cryptographic keys using DNAcrypt-AI (DOI: https://dx.doi.org/10.17504/protocols.io.5qpvo1387g4o/v1)

OBFD tag: 12/26


### Description
DNAcrypt-AI is founded on the intrinsic complexity, variation, unpredictability, and scale of the human genome. It works by generating a genome vocabulary, randomly sampled from more than 3 billion genomic loci across multiple chromosomes and genome assemblies (hg19 and hg38). This vocabulary consists of genomic coordinates, which are interpreted by FAS2rDNA to reconstitute DNA sequences that typically range from 1,000 to 50,000 nucleotides in length. The resulting collection of sequences forms a heterogeneous genomic corpus, containing structure and information that cannot be easily interpreted, decrypted, or recognized by visual inspection or conventional bioinformatics tools.

DNAcrypt-AI then leverages machine learning through Covary to extract latent sequence patterns from this reconstructed genome vocabulary using a sequence-informed framework. Covary uses feature expansion from [TIPs-VF](https://github.com/mahvin92/TIPs-VF) (refactored to [Covary_encoder](https://github.com/mahvin92/Covary-encoder/)) to encode the genetic sequences, making the framework very suitable for pattern extraction without reducibility to frequency-based signatures. This design makes the transformation pipeline irreversibly traceable. Finally, DNAcrypt-AI maps the vector embedding into alphanumeric and symbolic encodings through a kmer strategy, generating unique strings that can serve as passwords or cryptographic keys for the users.

The pipeline stores and encrypts the password or cryptographic key in a form of genomic coordinates, which can then be decrypted through DNAcrypt-AI.


### Architecture

The architecture of DNAcrypt-AI is relatively simple, yet largely dependent on two genome intelligence frameworks: [FAS2rDNA](https://github.com/mahvin92/FAS2rDNA) (a high-throughput DNA sequence reconstruction module) and [Covary](https://github.com/mahvin92/Covary) (a machine learning-based sequence intelligence framework). The detailed designs and internal architectures of these frameworks are described separately in their respective GitHub repositories. The image below maps the internal architecture of DNAcrypt-AI. 

<img width="3780" height="1890" alt="DNAcrypt architecture" src="https://github.com/mahvin92/DNAcrypt-AI/blob/main/assets/DNAcrypt%20architecture.png" />

DNAcrypt-AI begins by accepting a user-specified workflow and key length. The user may select to generate:
- a pure alphanumeric sequence (encryption key) or alphanumeric-symbols (password)
- a key consisting of 6 to 90 characters, default of 12 (if not specified)

This input is used to generate a pseudo-DNA sequence (or a DNA hash) that encodes feature-level encrypted information. A predefined k-mer dictionary (k = 5) is then applied to encode alphanumeric characters and symbols into a traceable but non-reversible mapping space. For enhanced security, users may generate dynamic k-mer dictionaries with customized encoding combinations, enabling variable character-to-kmer mappings (see *Encrypting and decrypting using a custom kmer dictionary* below).

DNAcrypt-AI then performs a deep genome keyring process, producing an encrypted corpus of genomic coordinates across multiple human genome assemblies (hg19 and hg38). This process randomly samples chromosome identifiers, strand orientation, and start–end genomic coordinates, ensuring cross-assembly variability, structural diversity, and high sequence entropy.

To further increase cryptographic functions, DNAcrypt-AI generates a genome-derived sequence ensemble with a maximum sequence length of 50,000 nucleotides, aggregated into 1,025 independent vocabularies. The resulting genome-derived dictionary may contain up to 51 million nucleotides, making it computationally difficult to synthetically reproduce, memorize, reverse-engineer, or decrypt using conventional methods.

FAS2rDNA reconstructs the DNA sequences corresponding to the generated genomic coordinates using a high-throughput, multiprocessing reconstruction pipeline. The reconstructed sequences are then passed to Covary, which deconvolves and learns relational sequence patterns from the corpus. DNAcrypt-AI consumes the vector embeddings produced by Covary and maps the scores and/or angular derivatices of the embeddings onto the k-mer dictionary. This final transformation renders a unique cryptographic sequence, which then effectively decrypted using the DNA hash to produce a unique key or phrase with specific sequence length.


## Usage notice
- DNAcrypt-AI can be used and tested as a Jupyter notebook hosted on Google Colab. A working local implementation is in development and you can contact us to request an early access.

- DNAcrypt-AI is very intuitive to use, requiring very minimal user input, as shown in the figure below. For encryption and password generation all you need is define: 1) string length 2) type of use case. For decryption all you need is provide the encrypted data.

- DNAcryt-AI supports alphanumeric encodings ```a -> z, A -> Z, 0 -> 9``` (for both Password and Encryption) and symbolic encodings such as ```!@#$%^&*()-_+=”``` (for Password only).

- The hg19 and hg38 genome assemblies are used as reference to encrypt and decrypt your password/key. Therefore, DNAcrypt-AI uses a biological and native genome sequences to store and read your secret information. Although current works is already being undertaken to expand this support to multi-species genome assemblies to increase the genome vocabularies of DNAcrypt-AI.

<img width="3780" height="1890" alt="DNAcrypt user step" src="https://github.com/mahvin92/DNAcrypt-AI/blob/main/assets/DNAcrypt%20user%20step.png" />


## Generate and encrypt a password or key

1. Launch DNAcrypt-AI (different ways)

- open the shareable versions of the [DNAcrypt-AI notebooks here](https://dnacryptai.chordexbio.com/releases) and choose the latest one, or use the [legacy version](https://colab.research.google.com/github/mahvin92/DNAcrypt-AI/blob/main/ipynb/DNAcrypt-AI_beta(v.0.1).ipynb)
- download the latest version of the notebook from the ```ipynb``` folder above and import it to your workspace
- load a version of the notebook directly from an opened Colab environment:

```
from IPython.display import HTML

notebook = "DNAcrypt-AI_beta(v.0.1).ipynb" # -> change the notebook name here
repo = "mahvin92/DNAcrypt-AI"
folder = "ipynb"

colab_url = f"https://colab.research.google.com/github/{repo}/blob/main/{folder}/{notebook}"
HTML(f'<a href="{colab_url}" target="_blank">Open {notebook} in Google Colab</a>')
```

2. Create a user configuration
- project_name: experiment code (optional)
- char_count: string lenght (default = 12)
- Use cases: **Password** = alphanumeric + symbol; **Encryption** = alphanumeric only (default = Password)

3. Run DNAcrypt-AI
```
Runtime -> Run all
```

4. Wait for DNAcrypt-AI to finish training from the reconstructed genome sequences (see *Training DNAcrypt-AI* below)
   
5. Store your encrypted data
- You can print or save a digital copy of your data, ensuring you can reproduce them for decryption later.


## Decrypt a password or key
1. Launch DNAcrypt-AI
- Similar to steps in **'Generate and encrypt a key'** section.

2. Modify user configuration
- Use cases: select 'Decryption'

3. Run DNAcrypt-AI
```
Runtime -> Run all
```
4. Upload your encrypted data
- Note that in addition to the original '*DNAcrypt_metadata.json*', you are required to upload the '*kmer_dict.json*' if you encrypted your data using a customized kmer dictionary. Otherwise, DNAcrypt-AI will assume you used the static vocabularies. The files could be renamed.

5. Wait for the key to be decrypted
- This may take some time, roughly about 15 minutes or less, depending on the genome vocabularies you have.

## Encrypting and decrypting using a custom kmer dictionary

There is no advantage to using a custom kmer dictionary, except in a situation where
- your key has been compromised;
- you want to recycle your encrption data but gets a refreshed sequence;
- you want to create a customized library suitable for your needs.

To generate a random kmer dictionary:
1. Launch DNAcrypt-AI as usual
2. Navigate to ```User configuration```, tick the box next to ```Custom``` under Kmer dictionary.
3. Run DNAcrypt-AI as usual
4. Save or upload the necessary file
   - For encryption, save the *kmer_dict.json* file along with *DNAcrypt_metadata.json*, which are your encrypted data.
   - For decryption, just upload the *kmer_dict.json* and *DNAcrypt_metadata.json* that were originally generated by DNAcrypt-AI.

Note that when you loss your custom *kmer_dict.json*, DNAcrypt-AI will not be able to recover the dictionary for you. Without correctly mapping your alphanumeric and symbol encodings to your kmer vocabularies, it's unlikely to decrypt your data.

## Storing your encrypted data

Your encrpytion data MUST NOT be modified. Any loss, modification, or unnecessary addition will affect the stored information. Tampering with the encrypted data (both *DNAcrypt_metadata.json* and *kmer_dict.json*) will affect the recovery of your password/key. However, you can rename the files as you wish.

The encrypted data is light and does not take too much of storage (maximum of 200kb). You can store your encryption as follows:
1. Printed copy - private and secure but requires re-encoding to a digital copy later before using
2. Digital copy - ready to use but also allows others to decrypt once they get a copy of your file/s

## Training DNAcrypt-AI

DNAcrypt-AI (in Jupyter notebooks) runs entirely in your browser, and DNAcrypt-AI does not collect nor store your data in the cloud or local server. Furthermore, the cipher does not index your encrypted data, nor does it utilize a pre-packed knowledge base or vector store of genomic vocabularies (such as encoded human genome sequences or k-mer dictionaries used in alphanumeric/symbol encoding). By design through Covary, users train and run DNAcrypt-AI locally, ensuring that user data remains exclusively theirs. Please note that machine learning inference is computationally intensive, so expect a processing time of approximately 15 minutes to successfully decrypt your password or key.


## Troubleshooting

1. Decrypted key does not match the expected alphanumeric-symbol sequence
   - Re-run the decryption again or restart your session ```Runtime -> Restart session and run all```
2. DNAcrypt-AI session crashed due to RAM exhaustion
   - Machine learning is a RAM-hungry process, ensure that you are connected to a GPU support (e.g., T4) if you are using the Colab environment
3. DNAcrypt-AI is taking so long in reconstucting my genome corpus
   - The reconstruction of DNA sequences is loaded to FAS2rDNA, which requires to download either or both the hg19 and hg38 human genome assemblies. These assemblies are quite massive (~>3 GB each) in size. Please wait for a moment for these assemblies to be fetched and indexed
4. DNAcrypt-AI is not downloading the required file (e.g., *DNAcrypt_metadata.json*)
   - If DNAcrypt-AI executed without an error and yet did not produce a download, it means that your browser is blocking the process. You can fetch your encryption files from ```/content``` directory through the File browser.
5. I obtained a low entropy sequence
   - DNAcrypt-AI estimates the entropy of the generated password (the random assignment and sequence of alphanumeric-symbol charcaters), not necessarily the strength of the encryption. If you are not satisfied with the entropy estimate, you can always run DNAcrypt-AI again until you arrive at a desirable entropy. If you encounter issues while running DNAcrypt-AI multiple times, restarting your session can fix most issues ```Runtime -> Restart session and run all```
  
## Reporting

Comments and suggestions to improve DNAcrypt-AI are welcome. If you find any bug or problem, please [open an issue](https://github.com/mahvin92/DNAcrypt-AI/issues/new) or [request a support here](https://dnacryptai.chordexbio.com).


## License notice

Please see updated license here: https://github.com/mahvin92/DNAcrypt-AI/blob/main/LICENSE

If you qualify for Section III, you can always request a license by contacting us at https://dnacryptai.chordexbio.com/

## Citations
De los Santos, M. and Lynn, C. (2026). DNAcrypt-AI protocol for generating and encrypting a secret key. protocols.io. DOI: 10.17504/protocols.io.14egn12k6v5d/v1

De los Santos, M. and Lynn, C. (2026). DNAcrypt-AI protocol for generating and encrypting a password. protocols.io. DOI: 10.17504/protocols.io.bp2l6e951gqe/v1

De los Santos, M. and Lynn, C. (2026). Decryption of genome-encoded cryptographic keys using DNAcrypt-AI. protocols.io. DOI: 10.17504/protocols.io.5qpvo1387g4o/v1

## Acknowledgement
Covary is powered by [Covary](https://github.com/mahvin92/Covary), [FAS2rDNA](https://github.com/mahvin92/FAS2rDNA), [assemBold program](https://assembold.chordexbio.com), [ChordexBio](https://chordexbio.com), and [CodeEnigma](https://github.com/KrishnanSG/codeenigma); made with Python, and tested using Google Colab ❤️
  

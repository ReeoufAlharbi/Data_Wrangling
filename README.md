# Data_Wrangling
### Step 1: Transfer the .zip File from Local System to the Server

```shell
scp -r C:/Users/Reeuo/Downloads/ncbi_dataset_all.zip alharbrn@ilogin.ibex.kaust.edu.sa:/home/alharbrn/
```

### Step 2: Unzip the Dataset on the Server

```text
unzip ncbi_dataset_all.zip
```

### Step 3: Calculate Genome Sizes for Each .fna File

```shell
for file in *.fna; do echo "$file $(grep -v "^>" "$file" | wc -c)" >> genome_sizes.fna; done
```

### Step 4: Find the Smallest Genome 

```shell
sort -k2 -n genome_sizes.fna | head -1
```

```text
GCA_000008725.1_ASM872v1_genomic.fna 1055551
```

### Step 5: Find the Largest Genome

```shell
sort -k2 -n genome_sizes.fna | tail -1
```

```text
GCA_000006745.1_ASM674v1_genomic.fna 4083883
```

### Step 6: Search for Words Containing Two 'c's in All .fna Files

```shell
grep -E "\b\w*c\w*c\w*\b" *.fna | wc -l
```

```text
7
```

### Step 7: Refine the Search to Exclude the Word "coccus"

```shell
grep -E "\b\w*c\w*c\w*\b" *.fna | grep -Ev "coccus" | wc -l
```

```text
2
```

### Step 8: Find .fna Files Larger Than 3MB

```shell
find . -name "*.fna" -size +3M | wc -l
```

```text
3
```



# master-slave-paradigm


- O processo master distribui as tasks (vetor de vetores) para os slaves
    - os vetores deverão ser ordenados usando bubble sort e quick sort

- devemos plotar o gráfico de Speed-Up 
    - o fator de aceleração ideal é o mesmo para quick e bubble
    - devemos adicionar mais uma linha para o quick e para o bubble
        - comparar o fator de aceleração com mais processadores paralelamente


- página 1 -> relatório
- página 2 -> resultados do quick e bubble

&vetor[0] é a mesma coisa que vetor

MPI_Send(vetor, 8, MPI_INT, 1, 5, MPI_COMM_WORLD)
send vetor, 8 posicoes, tipo inteiro, processo um, etiqueta 5, comunicador mundo (vai para todos os processos);

MPI_Send(&vetor[4], 4, MPI_INT, 1, 5, MPI_COMM_WORLD)
send vetor na posição 4, últimas quatro posições, tipo inteiro, processo um, etiqueta 5, comunicador mundo (vai para todos os processos);

MPI_Recv(vetor, 8, MPI_INT, 0, 5, MPI_COMM_WORLD, &status)
vetor, espaço no buffer, tipo, fonte processo 0, tag 5, comunicador mundo e status (struct que diz o que chegou)

MPI_Recv(&vetor[4], 4, MPI_INT, 1, 5, MPI_ANY_SOURCE, MPI_ANY_TAG, MPI_COMM_WORLD &status)
filtro aberto: receber de qualquer fonte, qualquer tag

MPI_Get_Count(&Stat, MPI_CHAR, &count) 
count é em bytes, precisamos converter para pegar em elementos

Não fazer dois gráficos 😭


___

### Para compilar o sequencial
gcc seq.c -o seq


### Para rodar o sequencial
srun --exclusive -N <num_machines> -n <num_cores> ./seq <num_Vetores> <tam_vetores> <sort_mechanism>

### Para compilar o paralelo
ladcomp -env mpicc mpi_master_slave.c -o par

### Para rodar o paralelo
srun --exclusive -N 1 -n 8 ./par <num_Vetores> <tam_vetores> <sort_mechanism>


___
**Fazer para cada múltiplo de cores** 

- Medir o tempo do sequencial e anotar na planilha
- Medir o tempo do paralelo e anotar na planilha

> usar 2 máquinas no MÁXIMO (nós)!

### Ideia:
- uma medição com **1** máquina (1, 2, 4, 8, 16 cores)


#### BSort: 5k vetores 10k elementos
- Sequencial: 2239.40
- 2 cores: 2250.67 (2 machines)
- 4 cores: 745.01 (2 machines)
- 8 cores: 321.09 (2 machines)
- 16 cores: 158.0 (2 machines)
- 32 cores: 146.60 (2 machines)

#### QSort: 5k vetores 100k elementos
- Sequencial: 28.27 
- 2 cores: 41.91 (2 machines) 
- 4 cores: 14.40 (2 machines)
- 8 cores: 7.54 (2 machines)
- 16 cores: 6.77 (2 machines)
- 32 cores: 7.55  (2 machines) 

> colocar no gráfico somente execução com 1 máquina (exceto 32 cores)
> iremos comparar a execução com 2 máquinas no texto (execução é paralela e distribuída, por isso o tempo maior!)

### Relatório

- comparar execução bubble sort com quicksort nos diferentes cores
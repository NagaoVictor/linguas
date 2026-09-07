| Categoria | Instrução / Diretiva | Descrição Técnica | Exemplo de Uso |

| :--- | :--- | :--- | :--- |

| \*\*Movimentação\*\* | `MOV` | Copia o valor de um registrador ou imediato para o registrador de destino. | `MOV X0, X1` |

| \*\*Movimentação\*\* | `MOVK` | Insere um valor imediato de 16 bits em uma parte específica (half-word) de um registrador, preservando os demais bits. | `MOVK X0, #0x1234, LSL #16` |

| \*\*Movimentação\*\* | `MOVZ` | Move um valor imediato de 16 bits para o registrador e preenche o restante dos bits com zeros. | `MOVZ X0, #42` |

| \*\*Movimentação\*\* | `MOVN` | Move o complemento de um valor imediato de 16 bits para o registrador (negativo lógico). | `MOVN X0, #0` |

| \*\*Memória (Load/Store)\*\*| `LDR` | Carrega um valor da memória (apontada por um registrador) para o registrador de destino. | `LDR X0, \[X1]` |

| \*\*Memória (Load/Store)\*\*| `STR` | Armazena o valor de um registrador no endereço de memória especificado. | `STR X0, \[X1, #8]` |

| \*\*Memória (Load/Store)\*\*| `LDUR / STUR` | Carrega ou armazena dados da memória utilizando um deslocamento imediato não alinhado/negativo. | `LDUR X0, \[X1, #-8]` |

| \*\*Memória (Load/Store)\*\*| `LDP / STP` | Carrega (\*Load Pair\*) ou armazena (\*Store Pair\*) um par de registradores da/para a memória em uma única instrução. | `STP X29, X30, \[SP, #-16]!` |

| \*\*Aritmética\*\* | `ADD` | Adiciona o operando fonte ao registrador base e armazena o resultado no destino. | `ADD X0, X1, X2` |

| \*\*Aritmética\*\* | `ADDS` | Adiciona valores e atualiza as flags de condição (N, Z, C, V) no registrador PSTATE. | `ADDS X0, X1, #10` |

| \*\*Aritmética\*\* | `SUB` | Subtrai o operando fonte do registrador base e armazena o resultado no destino. | `SUB X0, X1, X2` |

| \*\*Aritmética\*\* | `SUBS` | Subtrai valores e atualiza as flags de condição com base no resultado. | `SUBS X0, X1, X2` |

| \*\*Aritmética\*\* | `ADC / ADCS` | Adiciona valores considerando o valor atual da flag Carry (CF). | `ADC X0, X1, X2` |

| \*\*Aritmética\*\* | `SBC / SBCS` | Subtrai valores e a flag Carry (CF) do operando base. | `SBC X0, X1, X2` |

| \*\*Aritmética\*\* | `MUL` | Multiplica dois registradores e armazena o resultado no destino. | `MUL X0, X1, X2` |

| \*\*Aritmética\*\* | `MADD` | Multiplica dois registradores e adiciona um terceiro (Multiply-Add): $Rd = Ra + (Rn \\times Rm)$. | `MADD X0, X1, X2, X3` |

| \*\*Aritmética\*\* | `MSUB` | Multiplica dois registradores e subtrai o resultado de um terceiro (Multiply-Subtract): $Rd = Ra - (Rn \\times Rm)$. | `MSUB X0, X1, X2, X3` |

| \*\*Aritmética\*\* | `SDIV / UDIV` | Realiza divisão inteira com sinal (`SDIV`) ou sem sinal (`UDIV`). | `UDIV X0, X1, X2` |

| \*\*Aritmética\*\* | `NEG / NEGS` | Inverte o sinal aritmético do operando (equivalente a subtrair de zero). | `NEG X0, X1` |

| \*\*Lógica e Bits\*\* | `AND` | Realiza a operação lógica E bit a bit entre os registradores. | `AND X0, X1, X2` |

| \*\*Lógica e Bits\*\* | `ORR` | Realiza a operação lógica OU bit a bit entre os registradores. | `ORR X0, X1, X2` |

| \*\*Lógica e Bits\*\* | `EOR` | Realiza a operação lógica OU exclusivo (XOR) bit a bit. | `EOR X0, X1, X2` |

| \*\*Lógica e Bits\*\* | `BIC` | Realiza um E bit a bit entre o primeiro operando e o complemento do segundo (Bit Clear). | `BIC X0, X1, X2` |

| \*\*Lógica e Bits\*\* | `ORN` | Realiza um OU bit a bit combinando o primeiro operando com o complemento do segundo. | `ORN X0, X1, X2` |

| \*\*Lógica e Bits\*\* | `EON` | Realiza um XOR bit a bit combinando o primeiro operando com o complemento do segundo. | `EON X0, X1, X2` |

| \*\*Lógica e Bits\*\* | `MVN` | Move o valor invertido (complemento de 1) para o registrador de destino. | `MVN X0, X1` |

| \*\*Deslocamento\*\* | `LSL` | Desloca os bits para a esquerda (Logical Shift Left), preenchendo com zeros. | `LSL X0, X1, #2` |

| \*\*Deslocamento\*\* | `LSR` | Desloca os bits para a direita sem sinal (Logical Shift Right), preenchendo com zeros. | `LSR X0, X1, #3` |

| \*\*Deslocamento\*\* | `ASR` | Desloca os bits para a direita com sinal (Arithmetic Shift Right), preservando o bit de sinal. | `ASR X0, X1, #1` |

| \*\*Deslocamento\*\* | `ROR` | Rotaciona os bits para a direita, recirculando os bits que caem para fora. | `ROR X0, X1, #4` |

| \*\*Comparação\*\* | `CMP` | Compara dois valores executando uma subtração interna (`SUBS`) e atualizando flags (descarta o resultado). | `CMP X0, X1` |

| \*\*Comparação\*\* | `CMN` | Compara valores executando uma adição interna (`ADDS`) e atualizando flags (Negative Compare). | `CMN X0, #5` |

| \*\*Comparação\*\* | `TST` | Executa um E lógico interno (`ANDS`) entre registradores para testar bits (descarta o resultado). | `TST X0, #0x1` |

| \*\*Controle de Fluxo\*\* | `B` | Salta incondicionalmente para o rótulo de destino especificado. | `B loop\_start` |

| \*\*Controle de Fluxo\*\* | `BL` | Salta para uma função salvando o endereço de retorno no registrador de link (`X30`/`LR`). | `BL printf` |

| \*\*Controle de Fluxo\*\* | `BR` | Salta incondicionalmente para o endereço contido em um registrador. | `BR X10` |

| \*\*Controle de Fluxo\*\* | `BLR` | Salta para o endereço contido em um registrador, salvando o retorno em `X30`. | `BLR X12` |

| \*\*Controle de Fluxo\*\* | `RET` | Retorna da subrotina saltando para o endereço armazenado no registrador de link (`X30`). | `RET` |

| \*\*Saltos Condicionais\*\* | `B.EQ` | Salta se o resultado anterior for igual (Equal, Z = 1). | `B.EQ label\_equal` |

| \*\*Saltos Condicionais\*\* | `B.NE` | Salta se o resultado anterior não for igual (Not Equal, Z = 0). | `B.NE label\_diff` |

| \*\*Saltos Condicionais\*\* | `B.GT` | Salta se maior com sinal (Signed Greater Than). | `B.GT label\_greater` |

| \*\*Saltos Condicionais\*\* | `B.GE` | Salta se maior ou igual com sinal (Signed Greater or Equal). | `B.GE label\_ge` |

| \*\*Saltos Condicionais\*\* | `B.LT` | Salta se menor com sinal (Signed Less Than). | `B.LT label\_lt` |

| \*\*Saltos Condicionais\*\* | `B.LE` | Salta se menor ou igual com sinal (Signed Less or Equal). | `B.LE label\_le` |

| \*\*Saltos Condicionais\*\* | `B.HI` | Salta se maior sem sinal (Higher, C = 1 e Z = 0). | `B.HI label\_higher` |

| \*\*Saltos Condicionais\*\* | `B.LS` | Salta se menor ou igual sem sinal (Lower or Same). | `B.LS label\_ls` |

| \*\*Seleção Condicional\*\*| `CSEL` | Seleciona o valor entre dois registradores com base na condição avaliada (\*Conditional Select\*). | `CSEL X0, X1, X2, EQ` |

| \*\*Seleção Condicional\*\*| `CSINC` | Seleciona entre dois registradores, incrementando o segundo se a condição for falsa. | `CSINC X0, X1, X2, NE` |

| \*\*Pilha (Stack)\*\* | `ADD / SUB SP` | Ajusta o ponteiro da pilha (`SP`) alocando ou liberando espaço local. | `SUB SP, SP, #32` |

| \*\*Sistemas e Exceções\*\*| `SVC` | Dispara uma chamada de supervisor ou interrupção de sistema para o Kernel (Supervisor Call). | `SVC #0` |

| \*\*Sistemas e Exceções\*\*| `BRK` | Gera uma interrupção de ponto de parada (\*breakpoint\*) para depuração de software. | `BRK #0xDEAD` |

| \*\*Sistemas e Exceções\*\*| `NOP` | Instrução de preenchimento que não executa nenhuma operação, consumindo um ciclo. | `NOP` |

| \*\*Barreiras e Cache\*\* | `DMB` | Garante a barreira de memória de dados (\*Data Memory Barrier\*), ordenando transações. | `DMB SY` |

| \*\*Barreiras e Cache\*\* | `DSB` | Garante a barreira de sincronização de dados (\*Data Synchronization Barrier\*). | `DSB SY` |

| \*\*Barreiras e Cache\*\* | `ISB` | Limpa o pipeline de instruções (\*Instruction Synchronization Barrier\*). | `ISB` |

| \*\*Atômicas e Concorrência\*\*| `LDREX / STREX`| Carrega e armazena exclusivos para operações de sincronização atômica em multiprocessamento. | `LDREX W0, \[X1]` |

| \*\*Atômicas e Concorrência\*\*| `CAS` | Executa comparação e troca atômica (\*Compare and Swap\*) em memória diretamente. | `CAS W0, W1, \[X2]` |


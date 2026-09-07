| Categoria | Instrução / Diretiva | Descrição Técnica | Exemplo de Uso |
| :--- | :--- | :--- | :--- |
| **Movimentação** | `MOV` | Copia o valor do operando fonte para o operando destino. | `MOV EAX, EBX` |
| **Movimentação** | `MOVSX` | Move com extensão de sinal, preenchendo os bits superiores com o bit de sinal. | `MOVSX EAX, AL` |
| **Movimentação** | `MOVZX` | Move com extensão de zero, preenchendo os bits superiores com zeros. | `MOVZX EBX, BL` |
| **Movimentação** | `LEA` | Carrega o endereço efetivo (ponteiro) calculado pela expressão de memória no registrador. | `LEA EAX, [EBX + ECX*4]` |
| **Movimentação Avançada** | `MOVSB / MOVSW / MOVSD` | Copia blocos de bytes, words ou doublewords de RSI/ESI para RDI/EDI. | `REP MOVSB` |
| **Movimentação Avançada** | `STOSB / STOSW / STOSD` | Preenche uma área de memória com o valor contido em AL/AX/EAX. | `REP STOSD` |
| **Movimentação Avançada** | `LODSB / LODSW / LODSD` | Carrega um elemento da memória apontada por RSI/ESI para AL/AX/EAX. | `LODSD` |
| **Aritmética** | `ADD` | Adiciona o valor fonte ao destino e armazena o resultado no destino. | `ADD EAX, 10` |
| **Aritmética** | `SUB` | Subtrai o valor fonte do destino e armazena o resultado no destino. | `SUB EAX, EBX` |
| **Aritmética** | `INC` | Incrementa o operando especificado em 1 unidade. | `INC EAX` |
| **Aritmética** | `DEC` | Decrementa o operando especificado em 1 unidade. | `DEC EAX` |
| **Aritmética** | `IMUL` | Executa multiplicação com sinal entre registradores ou memória. | `IMUL EAX, EBX` |
| **Aritmética** | `IDIV` | Executa divisão com sinal, utilizando pares de registradores (EDX:EAX). | `IDIV ECX` |
| **Aritmética Avançada** | `MUL` | Multiplicação sem sinal entre o acumulador e o operando. | `MUL EAX` |
| **Aritmética Avançada** | `DIV` | Divisão sem sinal, utilizando o par de registradores EDX:EAX. | `DIV ECX` |
| **Aritmética Avançada** | `NEG` | Inverte o sinal aritmético do operando (complemento de 2). | `NEG EAX` |
| **Aritmética Avançada** | `ADC` | Adiciona o operando fonte ao destino junto com o valor da flag Carry (CF). | `ADC EAX, EBX` |
| **Aritmética Avançada** | `SBB` | Subtrai a fonte e a flag Carry (CF) do destino. | `SBB EAX, EBX` |
| **Conversão e Extensão** | `CBW / CWDE / CDQE` | Converte um byte em word, word em doubleword ou doubleword em quadword com sinal. | `CWDE` |
| **Conversão e Extensão** | `CWD / CDQ / CQO` | Expande o sinal do acumulador (AX/EAX/RAX) para o registrador superior (DX/EDX/RDX). | `CDQ` |
| **Lógica e Bits** | `AND` | Realiza a operação lógica E bit a bit entre os operandos. | `AND EAX, 0x0F` |
| **Lógica e Bits** | `OR` | Realiza a operação lógica OU bit a bit entre os operandos. | `OR EAX, 0x80` |
| **Lógica e Bits** | `XOR` | Realiza a operação lógica OU exclusivo bit a bit (frequentemente usada para zerar registradores). | `XOR EAX, EAX` |
| **Lógica e Bits** | `NOT` | Inverte todos os bits do operando (complemento de 1). | `NOT EAX` |
| **Lógica e Bits** | `SHL / SAL` | Desloca os bits para a esquerda (Shift Left), preenchendo com zeros. | `SHL EAX, 2` |
| **Lógica e Bits** | `SHR` | Desloca os bits para a direita sem sinal (Shift Right), preenchendo com zeros. | `SHR EAX, 1` |
| **Lógica e Bits** | `SAR` | Desloca os bits para a direita com sinal (Arithmetic Shift Right), preservando o bit de sinal. | `SAR EAX, 1` |
| **Manipulação de Bits** | `BT` | Testa um bit específico em um operando e copia seu valor para a flag Carry (CF). | `BT EAX, 3` |
| **Manipulação de Bits** | `BTS` | Testa um bit e o define como 1 (Bit Test and Set). | `BTS EAX, 5` |
| **Manipulação de Bits** | `BTR` | Testa um bit e o define como 0 (Bit Test and Reset). | `BTR EAX, 2` |
| **Manipulação de Bits** | `BTC` | Testa um bit e inverte seu valor (Bit Test and Complement). | `BTC EAX, 4` |
| **Manipulação de Bits** | `BSF / BSR` | Procura pelo primeiro bit definido (Bit Scan Forward ou Reverse), do LSB ou MSB. | `BSF EAX, EBX` |
| **Manipulação de Bits** | `POPCNT` | Conta o número de bits definidos como 1 em um registrador (popcount). | `POPCNT EAX, EBX` |
| **Rotação e Deslocamento** | `ROL / ROR` | Rotaciona os bits para a esquerda (Left) ou direita (Right), recirculando os bits. | `ROL EAX, 1` |
| **Rotação e Deslocamento** | `RCL / RCR` | Rotaciona os bits incluindo a flag Carry (CF) no ciclo de rotação. | `RCL EAX, 1` |
| **Comparação** | `CMP` | Compara dois operandos subtraindo a fonte do destino e atualizando as flags de status (sem salvar o resultado). | `CMP EAX, 5` |
| **Comparação** | `TEST` | Executa um E lógico entre os operandos e atualiza as flags de status (sem salvar o resultado). | `TEST EAX, EAX` |
| **Controle de Fluxo** | `JMP` | Salta incondicionalmente para o rótulo de destino especificado. | `JMP loop_start` |
| **Controle de Fluxo** | `JE / JZ` | Salta condicionalmente se o resultado anterior for igual ou zero (ZF = 1). | `JE target_label` |
| **Controle de Fluxo** | `JNE / JNZ` | Salta condicionalmente se o resultado anterior não for igual ou não zero (ZF = 0). | `JNE error_handler` |
| **Controle de Fluxo** | `JG / JNLE` | Salta se o valor for maior (Signed Greater). | `JG positive_path` |
| **Controle de Fluxo** | `JL / JNGE` | Salta se o valor for menor (Signed Less). | `JL negative_path` |
| **Controle de Fluxo** | `CALL` | Empilha o endereço de retorno atual e salta para a subrotina especificada. | `CALL print_uart` |
| **Controle de Fluxo** | `RET` | Desempilha o endereço salvo no topo da pilha e retorna o fluxo de execução para ele. | `RET` |
| **Saltos Condicionais (Sinal)** | `JL / JNGE` | Salta se menor que (Signed Less). | `JL menor` |
| **Saltos Condicionais (Sinal)** | `JLE / JNG` | Salta se menor ou igual a (Signed Less or Equal). | `JLE menor_igual` |
| **Saltos Condicionais (Sinal)** | `JGE / JNL` | Salta se maior ou igual a (Signed Greater or Equal). | `JGE maior_igual` |
| **Saltos Condicionais (Sem Sinal)**| `JB / JC / JNAE` | Salta se abaixo, menor sem sinal ou se Carry estiver ativado (CF = 1). | `JB abaixo` |
| **Saltos Condicionais (Sem Sinal)**| `JBE / JNA` | Salta se abaixo ou igual (Unsigned Less or Equal). | `JBE abaixo_igual` |
| **Saltos Condicionais (Sem Sinal)**| `JA / JNBE` | Salta se acima ou maior sem sinal (Unsigned Above). | `JA acima` |
| **Saltos Condicionais (Status)** | `JO / JNO` | Salta se a flag de Overflow estiver ativada (OF = 1) ou desativada (OF = 0). | `JO overflow_err` |
| **Saltos Condicionais (Status)** | `JS / JNS` | Salta se o resultado for negativo (SF = 1) ou positivo/zero (SF = 0). | `JS negativo` |
| **Controle de Loop** | `LOOP / LOOPE / LOOPNE`| Decrementa ECX/RCX e salta condicionalmente enquanto o contador não for zero (com suporte a ZF). | `LOOP loop_label` |
| **Controle de Flags** | `CLC / STC / CMC` | Limpa (Clear), define (Set) ou inverte (Complement) a flag Carry (CF). | `CLC` |
| **Controle de Flags** | `CLI / STI` | Limpa ou define a flag de interrupção (IF), desativando ou ativando interrupções de hardware. | `CLI` |
| **Pilha (Stack)** | `PUSH` | Insere um valor no topo da pilha (decrementando o registrador RSP/ESP). | `PUSH EAX` |
| **Pilha (Stack)** | `POP` | Remove o valor do topo da pilha e o armazena no registrador (incrementando RSP/ESP). | `POP EAX` |
| **Sistemas / Outros** | `NOP` | Instrução de preenchimento que não executa nenhuma operação, consumindo apenas um ciclo. | `NOP` |
| **Sistemas / Outros** | `SYSCALL / INT` | Dispara uma interrupção de software ou chamada de sistema para o Kernel. | `SYSCALL` |
| **Sincronização e Sistema**| `CPUID` | Retorna informações sobre o fabricante, arquitetura e recursos do processador. | `CPUID` |
| **Sincronização e Sistema**| `RDTSC` | Lê o contador de ciclos de clock da CPU (Time Stamp Counter) em EDX:EAX. | `RDTSC` |
| **Sincronização e Sistema**| `UD2` | Gera uma instrução de opcode indefinido proposital para forçar uma exceção de exceção inválida. | `UD2` |
| **Sincronização e Sistema**| `CLFLUSH` | Invalida e limpa a linha de cache de dados correspondente a um endereço de memória. | `CLFLUSH [EAX]` |
| **Atômicas e Concorrência**| `LOCK` | Prefixo que torna operações de memória atômicas em sistemas multi-core. | `LOCK XADD [EAX], EBX` |
| **Atômicas e Concorrência**| `CMPXCHG` | Compara o acumulador com o operando e realiza troca atômica se forem iguais. | `CMPXCHG [EBX], ECX` |
| **Atômicas e Concorrência**| `XCHG` | Troca atomicamente os valores entre dois operandos. | `XCHG EAX, [EBX]` |
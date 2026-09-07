\# Glossário Completo e Prático de Comandos e Flags (GCC e GDB)



\## Opções de Compilação, Otimização e Arquitetura do GCC



\* \*\*-O0 / -O1 / -O2 / -O3\*\*: Níveis de otimização do compilador. `-O0` desativa otimizações para depuração limpa; `-O1` aplica otimizações básicas; `-O2` equilibra performance e tamanho sem loops agressivos; `-O3` maximiza a performance aplicando \*loop unrolling\* e vetorização avançada.

&#x20; \* \*\*Exemplo\*\*: `gcc -O3 main.c -o main\_optimized`



\* \*\*-Os\*\*: Otimização focada em reduzir ao máximo o tamanho do código binário (\*code size\*), ideal para microcontroladores com memória Flash limitada.

&#x20; \* \*\*Exemplo\*\*: `arm-none-eabi-gcc -Os firmware.c -o firmware.elf`



\* \*\*-Ofast\*\*: Ativa todas as otimizações do `-O3` juntamente com relaxamentos em regras de conformidade matemática (como desconsiderar flags de ponto flutuante IEEE).

&#x20; \* \*\*Exemplo\*\*: `gcc -Ofast simulation.c -o simulation`



\* \*\*-Og\*\*: Otimiza o código mantendo a depuração intacta e amigável para depuradores, sem reordenar excessivamente o código ou criar pontos de parada confusos.

&#x20; \* \*\*Exemplo\*\*: `gcc -Og -g main.c -o main\_debug`



\* \*\*-ffreestanding\*\*: Indica ao GCC que o ambiente de destino pode não possuir a biblioteca padrão completa do C (libc), essencial para desenvolvimento \*bare-metal\* e sistemas operacionais.

&#x20; \* \*\*Exemplo\*\*: `gcc -ffreestanding kernel.c -o kernel.elf`



\* \*\*-fno-builtin\*\*: Desativa o reconhecimento automático de funções embutidas do compilador (como `memcpy` ou `strcpy`), garantindo que o GCC invoque apenas as funções explicitamente implementadas.

&#x20; \* \*\*Exemplo\*\*: `gcc -fno-builtin custom\_mem.c -o custom`



\* \*\*-fno-stack-protector\*\*: Desativa a injeção de código de proteção contra estouro de pilha (\*canaries\*), economizando ciclos e memória em sistemas embarcados restritos.

&#x20; \* \*\*Exemplo\*\*: `gcc -fno-stack-protector target.c -o target`



\* \*\*-fomit-frame-pointer\*\*: Suprime a criação de um ponteiro de quadro (\*frame pointer\*) dedicado nas funções, liberando o registrador correspondente para uso geral e otimizando o tamanho do código.

&#x20; \* \*\*Exemplo\*\*: `gcc -fomit-frame-pointer -O2 routine.c -o routine`



\* \*\*-funroll-loops\*\*: Expande automaticamente loops de tamanho fixo para eliminar saltos e instruções de controle de fluxo, aumentando a velocidade de execução em troca de maior espaço em Flash.

&#x20; \* \*\*Exemplo\*\*: `gcc -funroll-loops -O3 matrix.c -o matrix`



\* \*\*-flto (Link-Time Optimization)\*\*: Realiza otimizações em todo o programa durante a fase de linkagem, permitindo que o GCC analise funções entre diferentes arquivos para eliminar código morto e inline avançado.

&#x20; \* \*\*Exemplo\*\*: `gcc -flto -O3 file1.c file2.c -o program`



\* \*\*-fvisibility\*\*: Controla a exportação de símbolos de funções e variáveis nas bibliotecas, permitindo ocultar símbolos internos (`-fvisibility=hidden`) para otimizar a resolução de links.

&#x20; \* \*\*Exemplo\*\*: `gcc -fvisibility=hidden library.c -shared -o lib.so`



\* \*\*-fPIC (Position Independent Code)\*\*: Gera código independente de posição, necessário para a criação de bibliotecas compartilhadas carregadas dinamicamente na memória.

&#x20; \* \*\*Exemplo\*\*: `gcc -fPIC -c shared.c -o shared.o`



\* \*\*-fPIE (Position Independent Executable)\*\*: Gera executáveis inteiros independentes de posição, permitindo proteção avançada contra ataques de sequestro de fluxo de controle (como ASLR).

&#x20; \* \*\*Exemplo\*\*: `gcc -fPIE -pie main.c -o secure\_exec`



\* \*\*-fipa-pta\*\*: Ativa a análise interprocedural de pontos de alias (\*pointer alias analysis\*), permitindo que o compilador rastreie o comportamento de ponteiros entre chamadas de funções.

&#x20; \* \*\*Exemplo\*\*: `gcc -fipa-pta -O2 pointers.c -o pointers`



\* \*\*-fivopts\*\*: Realiza otimizações de variáveis de indução em loops, substituindo cálculos complexos de ponteiros por operações aritméticas lineares mais rápidas.

&#x20; \* \*\*Exemplo\*\*: `gcc -fivopts -O2 loop\_opt.c -o loop\_opt`



\* \*\*-fverbose-asm\*\*: Insere comentários explicativos em linguagem Assembly nos arquivos de montagem gerados (`-S`), facilitando a auditoria humana do código traduzido.

&#x20; \* \*\*Exemplo\*\*: `gcc -S -fverbose-asm source.c -o source.s`



\* \*\*-ffunction-sections / -fdata-sections\*\*: Coloca cada função e variável em sua própria seção dedicada na memória, permitindo que o linker descarte blocos não utilizados.

&#x20; \* \*\*Exemplo\*\*: `gcc -ffunction-sections -fdata-sections main.c -c`



\* \*\*-rdynamic\*\*: Passa instruções ao linker para adicionar todos os símbolos globais à tabela dinâmica do executável, permitindo rastreamento de pilha e símbolos em tempo de execução.

&#x20; \* \*\*Exemplo\*\*: `gcc -rdynamic main.c -o main`



\* \*\*-fno-common\*\*: Força o GCC a alocar variáveis globais não inicializadas na seção `.bss` em vez de tratá-las como símbolos comuns (\*common symbols\*), evitando conflitos acidentais de nomes.

&#x20; \* \*\*Exemplo\*\*: `gcc -fno-common globals.c -o globals`



\* \*\*-fno-exceptions / -fno-rtti\*\*: Desativa o suporte a exceções (`try`/`catch`) e informações de tipo em tempo de execução (`dynamic\_cast`), economizando muita memória e ciclos em projetos em C/C++ embarcado.

&#x20; \* \*\*Exemplo\*\*: `g++ -fno-exceptions -fno-rtti cpp\_code.cpp -o cpp\_code`



\* \*\*-fshort-enums\*\*: Atribui ao tipo `enum` o menor tipo inteiro possível compatível com os valores declarados, compactando o espaço ocupado por enumeradores em structs.

&#x20; \* \*\*Exemplo\*\*: `gcc -fshort-enums enums.c -o enums`



\* \*\*-fpack-struct\*\*: Força o empacotamento de todas as estruturas sem preenchimento (\*padding\*), equivalente a aplicar o atributo `packed` globalmente.

&#x20; \* \*\*Exemplo\*\*: `gcc -fpack-struct packet.c -o packet`



\* \*\*-mcpu=... / -march=... / -mtune=...\*\*: Define a microarquitetura, o conjunto de instruções alvo e a otimização de pipeline específica para o processador de destino (ex: `cortex-m4`, `armv7em`).

&#x20; \* \*\*Exemplo\*\*: `arm-none-eabi-gcc -mcpu=cortex-m4 main.c -o main.elf`



\* \*\*-mfloat-abi=...\*\*: Define o ABI de ponto flutuante (`soft`, `softfp`, `hard`), determinando se a CPU usará a FPU de hardware ou rotinas de software.

&#x20; \* \*\*Exemplo\*\*: `arm-none-eabi-gcc -mfloat-abi=hard main.c -o main.elf`



\* \*\*-mfpu=...\*\*: Especifica a unidade de ponto flutuante de hardware disponível no chip (ex: `fpv4-sp-d16`).

&#x20; \* \*\*Exemplo\*\*: `arm-none-eabi-gcc -mfpu=fpv4-sp-d16 main.c -o main.elf`



\* \*\*-mthumb\*\*: Força a geração de código utilizando o conjunto de instruções Thumb de tamanho reduzido, fundamental para arquiteturas ARM Cortex-M.

&#x20; \* \*\*Exemplo\*\*: `arm-none-eabi-gcc -mthumb main.c -o main.elf`



\---



\## Flags de Alertas, Diagnóstico e Segurança Estática do GCC



\* \*\*-Wall\*\*: Ativa um conjunto abrangente de avisos comuns sobre construções de código potencialmente perigosas ou suspeitas.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wall main.c -o main`



\* \*\*-Wextra\*\*: Habilita avisos adicionais não cobertos pelo `-Wall`, como comparações redundantes ou variáveis não inicializadas sutilmente.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wall -Wextra main.c -o main`



\* \*\*-Werror\*\*: Trata todos os avisos (\*warnings\*) gerados pelo compilador como erros fatais, interrompendo imediatamente o processo de build.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wall -Werror main.c -o main`



\* \*\*-Werror=...\*\*: Converte um aviso específico (ex: `-Werror=format-security`) em erro obrigatório.

&#x20; \* \*\*Exemplo\*\*: `gcc -Werror=format-security main.c -o main`



\* \*\*-Wconversion / -Wsign-conversion\*\*: Avisa sobre conversões implícitas de tipos de dados que possam causar perda de dados ou inversão de sinal numérico.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wconversion -Wsign-conversion main.c -o main`



\* \*\*-Wformat-security\*\*: Detecta usos inseguros de funções de formatação (como `printf` sem strings de formato literais), prevenindo vulnerabilidades de exploração de memória.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wformat-security main.c -o main`



\* \*\*-Wpadded\*\*: Emite um aviso sempre que o compilador insere bytes de preenchimento (\*padding\*) invisíveis dentro de estruturas (`struct`), garantindo controle milimétrico de layout binário.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wpadded struct\_test.c -o test`



\* \*\*-Wpacked\*\*: Verifica se o uso do atributo `packed` em structs causou desalinhamentos de memória perigosos para a arquitetura do processador.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wpacked struct\_test.c -o test`



\* \*\*-Wanalyzer-...\*\*: Ativa o analisador estático integrado do GCC para detectar vazamentos de memória, desreferências de ponteiros nulos e estouros de limites em tempo de compilação.

&#x20; \* \*\*Exemplo\*\*: `gcc -fanalyzer memory\_leak.c -o leak`



\* \*\*-Wshadow\*\*: Alerta quando uma variável local redefine o escopo de uma variável de escopo superior (\*variable shadowing\*), prevenindo confusões lógicas.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wshadow main.c -o main`



\* \*\*-Wbad-function-cast\*\*: Avisa sobre conversões explícitas de tipos de retorno de funções que possam causar perda de dados.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wbad-function-cast main.c -o main`



\* \*\*-Wmissing-prototypes / -Wstrict-prototypes\*\*: Exige a declaração prévia de protótipos de funções antes de sua implementação ou uso em C estrito.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wstrict-prototypes -std=c11 file.c -o file`



\* \*\*-Wredundant-decls\*\*: Alerta sobre declarações repetidas e desnecessárias de variáveis ou funções no mesmo escopo.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wredundant-decls main.c -o main`



\* \*\*-Wunused-parameter / -Wunused-variable / -Wunused-function\*\*: Detecta parâmetros, variáveis ou funções declaradas mas nunca utilizadas no escopo.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wunused-variable main.c -o main`



\* \*\*-Wswitch-enum / -Wswitch-default\*\*: Garante que todas as opções de um `enum` sejam tratadas explicitamente em instruções `switch`, ou exige a presença de um bloco `default`.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wswitch-enum state\_machine.c -o sm`



\* \*\*-Wpointer-arith\*\*: Emite avisos sobre operações aritméticas executadas diretamente em ponteiros para tipos com tamanho desconhecido ou `void\*`.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wpointer-arith ptr.c -o ptr`



\* \*\*-Wcast-qual\*\*: Alerta sempre que um modificador de tipo qualificador (como `const` ou `volatile`) é descartado ou alterado em um \*cast\*.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wcast-qual main.c -o main`



\* \*\*-Wwrite-strings\*\*: Atribui o qualificador `const` a literais de string em C, impedindo modificações indevidas em áreas de texto somente leitura.

&#x20; \* \*\*Exemplo\*\*: `gcc -Wwrite-strings main.c -o main`



\* \*\*-fsanitize=address\*\*: Insere instrumentação no código para detectar violações de memória em tempo de execução (como acessos fora dos limites do heap/stack e \*use-after-free\*).

&#x20; \* \*\*Exemplo\*\*: `gcc -fsanitize=address -g ubsan\_test.c -o test`



\* \*\*-fsanitize=thread\*\*: Detecta condições de corrida (\*data races\*) em código multithread em tempo de execução.

&#x20; \* \*\*Exemplo\*\*: `gcc -fsanitize=thread -pthread race.c -o race`



\* \*\*-fsanitize=undefined\*\*: Identifica comportamentos indefinidos (\*Undefined Behavior\*), como estouros de inteiros assinados, divisões por zero e deslocamentos de bits inválidos.

&#x20; \* \*\*Exemplo\*\*: `gcc -fsanitize=undefined ub.c -o ub`



\* \*\*-fsanitize=leak\*\*: Ativa o detector de vazamentos de memória integrado para identificar blocos alocados dinamicamente que nunca foram liberados.

&#x20; \* \*\*Exemplo\*\*: `gcc -fsanitize=leak leak.c -o leak`



\---



\## Comandos, Inspeção e Controle Avançado do GDB



\* \*\*target remote / target extended-remote\*\*: Conecta o depurador a um servidor remoto de hardware (como OpenOCD via JTAG/SWD) ou a uma instância de simulação.

&#x20; \* \*\*Exemplo\*\*: `(gdb) target remote localhost:3333`



\* \*\*monitor ...\*\*: Envia comandos diretos de controle de baixo nível para o firmware do gravador/debugador de hardware (ex: `monitor reset halt`).

&#x20; \* \*\*Exemplo\*\*: `(gdb) monitor reset halt`



\* \*\*info registers\*\*: Exibe o conteúdo atual de todos os registradores da CPU, incluindo contadores de programa e ponteiros de pilha.

&#x20; \* \*\*Exemplo\*\*: `(gdb) info registers`



\* \*\*x (examine)\*\*: Inspeciona a memória bruta em um endereço específico com formatação customizada (ex: `x/32xw 0x20000000` para visualizar 32 palavras em hexadecimal).

&#x20; \* \*\*Exemplo\*\*: `(gdb) x/16xw 0x20000000`



\* \*\*disassemble\*\*: Traduz e exibe o código de máquina atual em instruções Assembly legíveis para a arquitetura de destino.

&#x20; \* \*\*Exemplo\*\*: `(gdb) disassemble main`



\* \*\*break / watch\*\*: Interrompe a execução quando o fluxo atinge uma linha/função específica (`break`) ou quando o valor de uma variável/endereço de memória é alterado (`watch`).

&#x20; \* \*\*Exemplo\*\*: `(gdb) watch global\_var`



\* \*\*info threads / thread apply\*\*: Gerencia o contexto de execução de múltiplas threads de sistema operacional ou tarefas em tempo real.

&#x20; \* \*\*Exemplo\*\*: `(gdb) thread apply all bt`



\* \*\*stepi / nexti\*\*: Executa o programa estritamente passo a passo em nível de instrução de máquina (\*instruction\*), ignorando ou entrando em subrotinas.

&#x20; \* \*\*Exemplo\*\*: `(gdb) stepi`



\* \*\*backtrace (bt)\*\*: Rastreia e exibe a pilha de chamadas (\*call stack\*) atual, revelando a hierarquia de funções ativas até o ponto de parada.

&#x20; \* \*\*Exemplo\*\*: `(gdb) backtrace full`



\* \*\*symbol-file\*\*: Carrega símbolos de depuração DWARF de um arquivo ELF externo para mapear endereços de memória a nomes de funções e variáveis.

&#x20; \* \*\*Exemplo\*\*: `(gdb) symbol-file firmware.elf`



\* \*\*restore\*\*: Escreve o conteúdo binário de um arquivo diretamente em uma faixa específica da memória física ou Flash do microcontrolador.

&#x20; \* \*\*Exemplo\*\*: `(gdb) restore image.bin binary 0x08000000`



\* \*\*dump\*\*: Extrai uma faixa de memória bruta do dispositivo e a salva diretamente em um arquivo binário no computador de controle.

&#x20; \* \*\*Exemplo\*\*: `(gdb) dump binary memory dump.bin 0x20000000 0x20000FFF`



\* \*\*jump\*\*: Altera forçadamente o ponteiro de instrução (`PC`) para desviar o fluxo de execução para um endereço de memória arbitrário.

&#x20; \* \*\*Exemplo\*\*: `(gdb) jump \*0x080001FA`



\* \*\*maintenance info sections\*\*: Exibe informações detalhadas sobre os limites, permissões e tamanhos de todas as seções de memória mapeadas no executável.

&#x20; \* \*\*Exemplo\*\*: `(gdb) maintenance info sections`



\* \*\*handle\*\*: Configura como o GDB deve reagir quando sinais de sistema específicos (como `SIGSEGV` ou `SIGBUS`) são disparados pela aplicação.

&#x20; \* \*\*Exemplo\*\*: `(gdb) handle SIGSEGV stop print`



\* \*\*layout asm\*\*: Alterna a interface visual do GDB para um modo de divisão de tela focado na inspeção simultânea do código Assembly e registradores.

&#x20; \* \*\*Exemplo\*\*: `(gdb) layout asm`



\* \*\*layout regs\*\*: Divide a tela do GDB exibindo os registradores da CPU atualizados em tempo real lado a lado com o código-fonte ou Assembly.

&#x20; \* \*\*Exemplo\*\*: `(gdb) layout regs`



\* \*\*layout split\*\*: Exibe simultaneamente janelas de código-fonte, código em Assembly e a interface de linha de comando do GDB.

&#x20; \* \*\*Exemplo\*\*: `(gdb) layout split`



\* \*\*tui enable / tui disable\*\*: Ativa ou desativa a interface gráfica em modo texto (Text User Interface) nativa do GDB.

&#x20; \* \*\*Exemplo\*\*: `(gdb) tui enable`



\* \*\*set variable\*\*: Modifica o valor de uma variável ou registrador dinamicamente em tempo de execução durante uma interrupção.

&#x20; \* \*\*Exemplo\*\*: `(gdb) set variable counter = 0`



\* \*\*call\*\*: Força a execução imediata de uma função contida no programa a partir da linha de comando do GDB, independentemente do fluxo atual.

&#x20; \* \*\*Exemplo\*\*: `(gdb) call reset\_hardware()`



\* \*\*print / format\*\*: Imprime o valor de expressões avaliando formatos específicos (`/x` para hexadecimal, `/t` para binário, `/u` para decimal sem sinal, `/a` para endereço).

&#x20; \* \*\*Exemplo\*\*: `(gdb) print/x status\_reg`



\* \*\*whatis / ptype\*\*: Exibe o tipo de dados exato de uma expressão ou a definição detalhada de uma estrutura (`struct`).

&#x20; \* \*\*Exemplo\*\*: `(gdb) ptype struct control\_block`



\* \*\*catchpoint (catch throw / catch syscall)\*\*: Interrompe a execução do programa quando eventos específicos do sistema ocorrem (como exceções ou chamadas de sistema).

&#x20; \* \*\*Exemplo\*\*: `(gdb) catch syscall read`



\* \*\*condition\*\*: Adiciona uma condição lógica a um ponto de parada existente para que ele só dispare quando a condição for verdadeira.

&#x20; \* \*\*Exemplo\*\*: `(gdb) condition 1 err\_count > 5`



\* \*\*commands\*\*: Associa uma lista automatizada de comandos do GDB para serem executados automaticamente sempre que um breakpoint específico for atingido.

&#x20; \* \*\*Exemplo\*\*: 

&#x20;   ```text

&#x20;   (gdb) commands 1

&#x20;   > print x

&#x20;   > continue

&#x20;   > end

&#x20;   ```



\* \*\*enable / disable / delete breakpoints\*\*: Gerencia o estado de ativação ou remoção de pontos de parada configurados na sessão de depuração.

&#x20; \* \*\*Exemplo\*\*: `(gdb) disable breakpoint 2`



\* \*\*file\*\*: Especifica o arquivo executável principal a ser depurado, carregando seus símbolos na sessão atual.

&#x20; \* \*\*Exemplo\*\*: `(gdb) file firmware.elf`



\* \*\*detach\*\*: Desconecta o GDB do processo ou servidor remoto alvo, permitindo que o sistema continue rodando de forma autônoma.

&#x20; \* \*\*Exemplo\*\*: `(gdb) detach`



\* \*\*quit\*\*: Encerra a sessão atual do depurador GDB.

&#x20; \* \*\*Exemplo\*\*: `(gdb) quit`


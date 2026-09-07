# Aplicação dos 30 Roteiros no Ecossistema GNU (GCC e GDB)

## Bloco 1: Diagnóstico de Baixo Nível, Símbolos e Arquitetura de Hardware

* **Roteiro 01: Diagnóstico de Falha de Hardware/Memória**
  * **GCC:** Compilação com injeção estrita de diagnósticos de barramento e alocação de registradores: `gcc -O2 -ffreestanding -fno-builtin -Wall -Wextra -Werror firmware.c -o firmware.elf`
  * **GDB:** Inspeção de registradores e falhas de barramento em tempo de execução: `(gdb) target remote localhost:3333`, seguido de `(gdb) info registers` e `(gdb) x/32xw 0x40021000` para auditar o mapeamento de E/S.
* **Roteiro 02: Refatoração de Rotina Crítica em C**
  * **GCC:** Forçamento de expansão de funções críticas para eliminar overhead de *stack frame*: `gcc -O3 -fno-inline-functions-called-once -finline-limit=64 -S rotina.c`
  * **GDB:** Análise do desmonte (*disassembly*) gerado pelo compilador: `(gdb) disassemble main`, validando se o GCC aplicou *tail-call optimization* corretamente.
* **Roteiro 03: Validação de Concorrência e Race Condition em C**
  * **GCC:** Detecção estrita de condições de corrida em tempo de compilação via ferramentas de instrumentação: `gcc -fsanitize=thread -pthread -g concurrency.c -o conc`
  * **GDB:** Rastreamento de múltiplas threads de execução em nível de instrução: `(gdb) info threads`, `(gdb) thread apply all bt` e inserção de *hardware watchpoints*: `(gdb) watch variable_global`.
* **Roteiro 04: Otimização de Performance (Assembly/C)**
  * **GCC:** Inserção de blocos de *Inline Assembly* com restrições explícitas de registradores: `__asm__ volatile ("dsb" : : : "memory");` compilado com `gcc -mcpu=cortex-m4 -mthumb -O3`.
  * **GDB:** Verificação de ciclos de clock e execução passo a passo em Assembly: `(gdb) stepi` e `(gdb) display /i $pc`.
* **Roteiro 05: Relatório de Exceção de Hardware (Kernel Panic / Hard Fault)**
  * **GCC:** Geração de mapas de símbolos detalhados para rastreamento de saltos inválidos: `gcc -g3 -ggdb -fno-omit-frame-pointer main.c -o main.elf`
  * **GDB:** Carregamento de símbolos de depuração e rastreamento de pilha corrompida: `(gdb) symbol-file main.elf`, `(gdb) backtrace` e inspeção do registrador de pilha `(gdb) p/x $sp`.
* **Roteiro 06: Plano de Rollback de Firmware**
  * **GCC:** Criação de seções personalizadas na memória Flash via arquivo *linker script* (`.ld`) e `gcc -T linker.ld` para endereçamento fixo do bootloader.
  * **GDB:** Manipulação direta da memória Flash e reinicialização de ponteiros de instrução: `(gdb) restore firmware_v1.bin binary 0x08000000` e `(gdb) set {unsigned int}0x20000000 = 0x08002000`.

---

## Bloco 2: Análise Crítica, Flags de Compilação e Undefined Behavior

* **Roteiro 07: Ponderação de Trade-offs (Alocação Dinâmica vs. Estática)**
  * **GCC:** Bloqueio absoluto de funções de heap (`malloc`/`free`) em nível de linker para forçar alocação estática: `gcc -Wl,--wrap=malloc -Wl,--wrap=free main.c`
  * **GDB:** Monitoramento estático dos limites de seções `.bss` e `.data`: `(gdb) maintenance info sections` para garantir zero alocação dinâmica imprevista.
* **Roteiro 08: Contestação de Comportamento Indefinido (Undefined Behavior)**
  * **GCC:** Ativação de flags rigorosas de mitigação de UB do GCC: `gcc -fsanitize=undefined -fno-sanitize-recover=all -Wall -Wextra`
  * **GDB:** Interrupção automática do fluxo quando o compilador injeta armadilhas de UB: `(gdb) catch throw` ou inspeção de sinais de falha de alinhamento `(gdb) handle SIGBUS stop print`.
* **Roteiro 09: Defesa de Padrão de Projeto de Driver (HAL)**
  * **GCC:** Isolamento de módulos com visibilidade estrita de símbolos via link-time optimization e escopo: `gcc -flto -fvisibility=hidden driver.c`
  * **GDB:** Validação de encapsulamento de ponteiros de funções na HAL: `(gdb) p *hal_struct_ptr` e rastreamento de chamadas indiretas `(gdb) info symbol 0x0800124A`.
* **Roteiro 10: Avaliação de Risco de Dívida Técnica em Firmware**
  * **GCC:** Varredura estática de estouro de limites e ponteiros nus através de flags de aviso estritas: `gcc -Wanalyzer-too-complex -Warray-bounds=2 -Wstringop-overflow=4`
  * **GDB:** Inspeção de limites de buffers estáticos diretamente na RAM: `(gdb) print sizeof(buffer_uart) / sizeof(buffer_uart[0])`.
* **Roteiro 11: Validação de Benchmark de Hardware**
  * **GCC:** Remoção de código morto e otimização agressiva de loops de contagem de ciclos: `gcc -O3 -funroll-loops -fipa-pta`
  * **GDB:** Medição precisa de intervalos entre pontos de parada (*breakpoints*): `(gdb) break start_handler`, `(gdb) continue`, zerar timer, e `(gdb) break end_handler`, `(gdb) print $timer_register`.
* **Roteiro 12: Desmistificação de Alocação de Memória**
  * **GCC:** Análise de escopo de variáveis locais via diretivas de geração de símbolos do GCC (`-g3`).
  * **GDB:** Monitoramento de variáveis locais saindo de escopo e persistindo na stack frame: `(gdb) info locals` e `(gdb) frame 1` para inspecionar o encadeamento de quadros de pilha.

---

## Bloco 3: Gestão de Projetos Embarcados, Linker e Prazos

* **Roteiro 13: Escalada de Bloqueio de Hardware (Blocker)**
  * **GCC:** Interrupção imediata do processo de linkagem por símbolos indefinidos de periféricos: `gcc -Wl,--no-undefined main.o i2c.o -o firmware.elf`
  * **GDB:** Diagnóstico de registradores de estado de barramento travados em nível de hardware via GDB Server (OpenOCD).
* **Roteiro 14: Redefinição de Escopo de Arquitetura**
  * **GCC:** Análise detalhada do tamanho de cada função e seção gerada pelo compilador: `gcc -Wl,-Map=output.map` (mapeamento completo da Flash/RAM).
  * **GDB:** Inspeção do uso real de memória estática após remoção de módulos de log: `(gdb) p &_end - &_stext`.
* **Roteiro 15: Alinhamento de Prioridades de Compilação**
  * **GCC:** Tratamento de todos os avisos do compilador como erros fatais para travar a build: `gcc -Werror -Wall -Wextra main.c`
  * **GDB:** Validação imediata de correções de ponteiros antes de prosseguir com a gravação na placa física.
* **Roteiro 16: Handoff de Código de Baixo Nível**
  * **GCC:** Inclusão de metadados de documentação e revisão de símbolos exportados via `gcc -rdynamic`.
  * **GDB:** Dump completo da tabela de símbolos para transferência de contexto: `(gdb) info functions` e `(gdb) info variables`.
* **Roteiro 17: Relatório de Status de Compilação (Sprint)**
  * **GCC:** Execução de compilação limpa com relatório detalhado de otimizações aplicadas: `gcc -fopt-info-all=build_opt.log -O2 main.c`
  * **GDB:** Execução automatizada de suítes de testes unitários em ambiente simulado QEMU via GDB batch mode: `gdb -batch -x test_script.gdb`.
* **Roteiro 18: Negociação de Prazo para Otimização de Assembly**
  * **GCC:** Geração de arquivo intermediário de montagem para inspeção cirúrgica de registradores: `gcc -S -fverbose-asm kernel_timer.c`
  * **GDB:** Comparação de contagem de instruções antes e depois da otimização manual em Assembly.

---

## Bloco 4: Negociação Técnica, Code Review e Mitigação via GCC/GDB

* **Roteiro 19: Mediação de Impasse sobre Arquitetura de Software**
  * **GCC:** Compilação condicional baseada em *macros* de arquitetura pré-definidas: `gcc -DUS_DMA_STATE_MACHINE=1 main.c`
  * **GDB:** Teste dinâmico de caminhos de código alternativos alterando flags em tempo de execução: `(gdb) set variable use_dma = 1`.
* **Roteiro 20: Correção de Rota em Code Review (C/Assembly)**
  * **GCC:** Ativação de alertas específicos contra funções vulneráveis a estouro de buffer: `gcc -Wformat-security -Werror=format-security`
  * **GDB:** Intercepção de chamadas a funções inseguras para análise de parâmetros: `(gdb) break strcpy` e `(gdb) print (char*) $rsi`.
* **Roteiro 21: Solicitação de Datasheet ou Especificação**
  * **GCC:** Verificação de alinhamento de estruturas de dados de acordo com o manual do componente: `gcc -Wpadded main.c` (avisa se o compilador inseriu *padding* indesejado).
  * **GDB:** Inspeção binária byte a byte de structs enviadas pelo barramento SPI: `(gdb) x/8tb &packet_spi`.
* **Roteiro 22: Imposição de Critério de Aceite para Deploy em Embarcados**
  * **GCC:** Otimização máxima para consumo energético e tamanho de binário: `gcc -Os -flto -ffunction-sections -Wl,--gc-sections`
  * **GDB:** Monitoramento contínuo de exceções e travamentos durante testes de estresse de 48 horas conectados via GDB Server.
* **Roteiro 23: Redirecionamento de Foco para Restrição de Hardware**
  * **GCC:** Emissão de avisos rigorosos de largura de banda de tipos de dados (`-Wconversion -Wsign-conversion`).
  * **GDB:** Inspeção de perda de precisão numérica em registradores de ponto flutuante ou inteiros de 16/32 bits.
* **Roteiro 24: Validação de Consenso de Protocolo**
  * **GCC:** Geração de código estrito conforme padrões ANSI C / ISO C11: `gcc -std=c11 -pedantic-errors`
  * **GDB:** Validação do estado mestre/escravo do barramento inspecionando diretamente os bits de controle nos registradores I2C.

---

## Bloco 5: Narrativa Temporal, Post-Mortem e Incidentes de Sistema

* **Roteiro 25: Post-Mortem de Falha de Firmware (Crash Histórico)**
  * **GCC:** Geração de arquivo de *Core Dump* para análise pós-falha em sistemas Unix-like (ou análise de imagem binária via *objdump*): `gcc -g crash_analysis.c -o crash`
  * **GDB:** Investigação do estado exato da máquina no momento do impacto: `gdb crash core`, seguido de `(gdb) bt` e `(gdb) info registers`.
* **Roteiro 26: Projeção de Carga de Processamento (Stress Test)**
  * **GCC:** Instrumentação de código para profiling de desempenho com suporte do GCC: `gcc -pg -O2 main.c -o profiled`
  * **GDB:** Coleta de amostras de endereço de instrução sob carga máxima: `(gdb) interrupt`, `(gdb) info line *($pc)` repetidas vezes para mapear gargalos de CPU.
* **Roteiro 27: Resumo Executivo de Arquitetura**
  * **GCC:** Consolidação do processo de build limpo utilizando um Makefile estruturado sob GCC puro sem dependências de IDEs propietárias.
  * **GDB:** Validação final de que todos os símbolos de depuração essenciais estão presentes para auditoria externa.
* **Roteiro 28: Histórico Evolutivo de Firmware**
  * **GCC:** Comparação de versões de binários gerados através de ferramentas GNU como `size firmware_v1.elf firmware_v2.elf`.
  * **GDB:** Auditoria de regressão de comportamento entre versões carregando símbolos antigos em paralelo.
* **Roteiro 29: Contextualização de Impacto de Atualização de Toolchain**
  * **GCC:** Identificação de mudanças de comportamento geradas por novas versões do compilador através de flags de diagnóstico de alinhamento (`-Wpacked`).
  * **GDB:** Verificação de deslocamentos (*offsets*) de campos dentro de structs que mudaram devido a alterações no *alignment* padrão do novo GCC.
* **Roteiro 30: Síntese de Aprendizado em Engenharia de Baixo Nível**
  * **GCC:** Domínio absoluto da cadeia de compilação cruzada (*cross-compiler* `arm-none-eabi-gcc`) para geração de imagens bare-metal.
  * **GDB:** Fluência na depuração remota via interface JTAG/SWD, controlando o ciclo de vida completo do silício a partir da linha de comando.

---

# Variação Profunda dos 30 Roteiros: Arquitetura, GCC, GDB e C Puro

## Bloco 1: Diagnóstico de Barramento, Endereçamento Físico e Compilação Cruzada

* **Roteiro 01: Diagnóstico de Falha de Hardware/Memória**
  * **GCC:** `arm-none-eabi-gcc -mcpu=cortex-m4 -mfloat-abi=hard -mfpu=fpv4-sp-d16 -O2 -ffreestanding -fno-builtin -Wall -Wextra -Werror bus_fault.c -o bus_fault.elf`
  * **GDB:** `(gdb) target extended-remote :4242`, `(gdb) monitor reset halt`, `(gdb) print/x *(volatile uint32_t*)0xE000ED28` (leitura direta do registrador CFSR de falhas do ARM).

* **Roteiro 02: Refatoração de Rotina Crítica em C**
  * **GCC:** `arm-none-eabi-gcc -O3 -fno-stack-protector -fomit-frame-pointer -funroll-loops -S interrupt_handler.c -o -`
  * **GDB:** `(gdb) disassemble interrupt_handler`, `(gdb) break *0x080004f2`, `(gdb) commands`, `print $r0`, `end`.

* **Roteiro 03: Validação de Concorrência e Race Condition em C**
  * **GCC:** `gcc -fsanitize=thread -O1 -g ring_buffer.c -o ring_buffer -lpthread`
  * **GDB:** `(gdb) set non-stop on`, `(gdb) watch circular_buffer_head`, `(gdb) thread apply 2 print/x *shared_ptr`.

* **Roteiro 04: Otimização de Performance (Assembly/C)**
  * **GCC:** `arm-none-eabi-gcc -mcpu=cortex-m4 -O3 -masm=intel -S dsp_filter.c`
  * **GDB:** `(gdb) layout asm`, `(gdb) stepi 10`, `(gdb) info registers r0 r1 r2 r3`.

* **Roteiro 05: Relatório de Exceção de Hardware (Kernel Panic / Hard Fault)**
  * **GCC:** `arm-none-eabi-gcc -g3 -fno-omit-frame-pointer -rdynamic hardfault.c -o hardfault.elf`
  * **GDB:** `(gdb) frame 0`, `(gdb) p/x $pc`, `(gdb) info frame`, verificando o registrador LR salvo na pilha para identificar o ponto de salto inválido.

* **Roteiro 06: Plano de Rollback de Firmware**
  * **GCC:** `arm-none-eabi-gcc -T linker_bootloader.ld -Wl,--section-start=.text=0x08000000 firmware.c -o firmware.elf`
  * **GDB:** `(gdb) restore image_v1.bin binary 0x08004000`, `(gdb) jump *0x08000000`.

---

## Bloco 2: Alocação Estática, Mitigação de UB e Verificação Estática

* **Roteiro 07: Ponderação de Trade-offs (Alocação Dinâmica vs. Estática)**
  * **GCC:** `gcc -Wl,--wrap=malloc -Wl,--wrap=calloc -Wl,--wrap=realloc -Wl,--wrap=free static_pool.c -o static_pool`
  * **GDB:** `(gdb) maintenance section-info`, validando que os segmentos `.bss` e `.data` cobrem todo o espaço estático reservado.

* **Roteiro 08: Contestação de Comportamento Indefinido (Undefined Behavior)**
  * **GCC:** `gcc -fsanitize=undefined,address -fno-sanitize-recover=undefined -Wall -Wextra ub_test.c -o ub_test`
  * **GDB:** `(gdb) catch signal SIGSEGV`, `(gdb) run`, `(gdb) backtrace full`.

* **Roteiro 09: Defesa de Padrão de Projeto de Driver (HAL)**
  * **GCC:** `arm-none-eabi-gcc -flto -fvisibility=internal -fPIC -c i2c_driver.c -o i2c_driver.o`
  * **GDB:** `(gdb) ptftype struct i2c_device_t`, `(gdb) print i2c_bus_handle->write_reg(0x68, 0x1B, 0x08)`.

* **Roteiro 10: Avaliação de Risco de Dívida Técnica em Firmware**
  * **GCC:** `gcc -fanalyzer -Wanalyzer-malloc-leak -Wstringop-overflow=4 parser.c -o parser`
  * **GDB:** `(gdb) print sizeof(uart_rx_buffer)`, `(gdb) x/s uart_rx_buffer`.

* **Roteiro 11: Validação de Benchmark de Hardware**
  * **GCC:** `arm-none-eabi-gcc -O3 -fipa-pta -fivopts -S benchmark_timer.c`
  * **GDB:** `(gdb) break start_benchmark`, `(gdb) continue`, `(gdb) print/u $dwt_cyccnt` (ciclos exatos do processador).

* **Roteiro 12: Desmistificação de Alocação de Memória**
  * **GCC:** `gcc -g3 -O0 stack_scope.c -o stack_scope`
  * **GDB:** `(gdb) finish`, `(gdb) x/16xw $sp`, inspecionando o lixo de memória deixado pelo stack frame anterior.

---

## Bloco 3: Gerenciamento de Seções, Linker Scripts e Prazos

* **Roteiro 13: Escalada de Bloqueio de Hardware (Blocker)**
  * **GCC:** `arm-none-eabi-gcc -Wl,--no-undefined -Wl,--warn-common main.o motor_pca9685.o -o system.elf`
  * **GDB:** `(gdb) target remote localhost:3333`, `(gdb) monitor mww 0x40005400 0x00000001` (liberação forçada de registrador via JTAG).

* **Roteiro 14: Redefinição de Escopo de Arquitetura**
  * **GCC:** `arm-none-eabi-gcc -Wl,-Map=firmware_map.map,--cref main.c -o main.elf`
  * **GDB:** `(gdb) print &_etext - &_stext` (tamanho exato da seção de código compilada).

* **Roteiro 15: Alinhamento de Prioridades de Compilação**
  * **GCC:** `gcc -Werror=implicit-function-declaration -Werror=pointer-sign -Wall -Wextra main.c -o main`
  * **GDB:** `(gdb) break main`, `(gdb) run`, testando o binário limpo de avisos.

* **Roteiro 16: Handoff de Código de Baixo Nível**
  * **GCC:** `gcc -rdynamic -g exported_symbols.c -o exported_symbols`
  * **GDB:** `(gdb) info functions motor_*`, `(gdb) info variables *global*`.

* **Roteiro 17: Relatório de Status de Compilação (Sprint)**
  * **GCC:** `gcc -fopt-info-vec-all=vectorization.log -O3 main.c -o main`
  * **GDB:** `gdb -batch -iex "set pagination off" -ex "file test_runner.elf" -ex "run" -ex "quit"`

* **Roteiro 18: Negociação de Prazo para Otimização de Assembly**
  * **GCC:** `arm-none-eabi-gcc -S -fverbose-asm -O2 inline_asm.c -o inline_asm.s`
  * **GDB:** Comparação de contagem de instruções via desmonte após injeção de registradores manuais.

---

## Bloco 4: Mitigação de Conflitos em PRs, Flags Estritas e Tipos

* **Roteiro 19: Mediação de Impasse sobre Arquitetura de Software**
  * **GCC:** `arm-none-eabi-gcc -DCONFIG_USE_DMA_ENGINE=1 -DCONFIG_POLLING_TIMEOUT=500 main.c -o main.elf`
  * **GDB:** `(gdb) set variable config_use_dma = 1`, `(gdb) continue`.

* **Roteiro 20: Correção de Rota em Code Review (C/Assembly)**
  * **GCC:** `gcc -Wformat-security -Werror=format-security -Wstack-protector -fstack-protector-all pr_check.c`
  * **GDB:** `(gdb) break __stack_chk_fail`, `(gdb) run`, interceptando tentativa de corrupção de stack frame.

* **Roteiro 21: Solicitação de Datasheet ou Especificação**
  * **GCC:** `arm-none-eabi-gcc -Wpadded -Wpacked -c spi_register_map.c -o spi_register_map.o`
  * **GDB:** `(gdb) p sizeof(spi_packet_t)`, `(gdb) x/16xb &packet_buffer`.

* **Roteiro 22: Imposição de Critério de Aceite para Deploy em Embarcados**
  * **GCC:** `arm-none-eabi-gcc -Os -flto -ffunction-sections -fdata-sections -Wl,--gc-sections main.c -o main.elf`
  * **GDB:** `(gdb) target remote localhost:3333`, monitoramento contínuo durante ciclo longo de testes via watchdogs.

* **Roteiro 23: Redirecionamento de Foco para Restrição de Hardware**
  * **GCC:** `gcc -Wconversion -Wsign-conversion -Wfloat-conversion arithmetic_limits.c -o limits`
  * **GDB:** `(gdb) print/t raw_adc_value`, avaliando perda de bits em conversões de ponto fixo.

* **Roteiro 24: Validação de Consenso de Protocolo**
  * **GCC:** `gcc -std=c11 -pedantic-errors -Wall -Wextra i2c_protocol.c -o i2c_protocol`
  * **GDB:** `(gdb) print i2c_master_mode_active`, validando bit de controle mestre/escravo.

---

## Bloco 5: Post-Mortem, Análise de Carga e Auditoria de Toolchain

* **Roteiro 25: Post-Mortem de Falha de Firmware (Crash Histórico)**
  * **GCC:** `gcc -g -rdynamic post_mortem.c -o post_mortem`
  * **GDB:** `gdb post_mortem core.dump`, `(gdb) backtrace full`, `(gdb) info registers`.

* **Roteiro 26: Projeção de Carga de Processamento (Stress Test)**
  * **GCC:** `gcc -pg -O2 stress_test.c -o stress_test` (suporte a profiler gprof).
  * **GDB:** Amostragem periódica do ponteiro de instrução para isolamento de hotspots de CPU.

* **Roteiro 27: Resumo Executivo de Arquitetura**
  * **GCC:** Compilação limpa via Makefile estruturado sob cadeias GNU puras.
  * **GDB:** Auditoria de integridade de símbolos de depuração DWARF.

* **Roteiro 28: Histórico Evolutivo de Firmware**
  * **GCC:** `arm-none-eabi-size firmware_v1.elf firmware_v2.elf` (comparação de footprint de Flash e RAM).
  * **GDB:** `(gdb) symbol-file firmware_v1.elf`, validando regressões de comportamento entre versões.

* **Roteiro 29: Contextualização de Impacto de Atualização de Toolchain**
  * **GCC:** `gcc -Wpacked -Wattributes -c toolchain_migration.c -o migration.o`
  * **GDB:** `(gdb) p &struct_instance.field_target`, checando offsets alterados por novas regras de alinhamento do GCC atualizado.

* **Roteiro 30: Síntese de Aprendizado em Engenharia de Baixo Nível**
  * **GCC:** Domínio completo de `arm-none-eabi-gcc` para controle de silício *bare-metal*.
  * **GDB:** Orquestração avançada de depuração via interface JTAG/SWD em ambiente de desenvolvimento embarcado crítico.
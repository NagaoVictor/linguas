\# Banco de Dados de Arquitetura e Baixo Nível: 30 Roteiros em 3 Variações (90 Frases)



\## Bloco 1: Diagnóstico de Baixo Nível e Arquitetura de Hardware



\### Roteiro 01: Diagnóstico de Falha de Hardware/Memória

\* Variação 1 (Técnico Padrão): Ao analisar o comportamento atual do barramento de dados, identificamos um gargalo crítico em \[registrador / periférico, ex: DMA / GPIO], o que compromete diretamente a integridade do clock do sistema. A investigação apontou que a falha decorre de \[instabilidade de tensão / ruído no sinal], agravada pela ausência de pull-up adequado.

\* Variação 2 (Relatório Executivo): O monitoramento do barramento revelou degradação de performance associada a \[registrador / periférico], provocada por \[instabilidade de tensão / ruído no sinal] e pela falta de terminadores adequados.

\* Variação 3 (Slack / Comunicação Ágil): O barramento travou por causa de \[instabilidade de tensão / ruído no sinal] em \[registrador / periférico], quebrando o clock. Precisamos revisar o circuito físico.



\### Roteiro 02: Refatoração de Rotina Crítica em C

\* Variação 1 (Técnico Padrão): O código atual em C para \[rotina de interrupção / manipulação de ponteiros] atingiu o limite de ciclos de clock. Recomenda-se a reescrita utilizando alocação estática e otimização direta de registradores, garantindo latência previsível.

\* Variação 2 (Relatório Executivo): A rotina de \[rotina de interrupção] apresenta ineficiência de processamento, tornando obrigatória sua refatoração em C estático para assegurar restrições de tempo real.

\* Variação 3 (Slack / Comunicação Ágil): Essa função de \[rotina de interrupção] estourou os ciclos. Vou reescrever em C puro com alocação estática para zerar o overhead.



\### Roteiro 03: Validação de Concorrência e Race Condition em C

\* Variação 1 (Técnico Padrão): Em sistemas embarcados multithread, o acesso concorrente a \[buffer circular / variável global] exige o uso estrito de instruções atômicas em Assembly. A ausência de barreira de memória resulta em corrupção de dados intermitente.

\* Variação 2 (Relatório Executivo): Verificou-se instabilidade por race condition no acesso a \[buffer circular], exigindo a implementação compulsória de travas de sincronização a nível de arquitetura.

\* Variação 3 (Slack / Comunicação Ágil): Tem uma race condition feia em \[buffer circular]. Sem barreira de memória, as threads vão corromper os dados no meio da execução.



\### Roteiro 04: Otimização de Performance (Assembly/C)

\* Variação 1 (Técnico Padrão): Com base na análise do disassembler, o compilador gerou instruções redundantes para \[loop de processamento de imagem]. Substituímos o trecho por uma macro em Assembly otimizada para a arquitetura ARM, reduzindo o consumo de ciclos em 40%.

\* Variação 2 (Relatório Executivo): A otimização do trecho \[loop de processamento de imagem] via rotina dedicada em Assembly resultou em ganho de eficiência de 40% no consumo de ciclos de CPU.

\* Variação 3 (Slack / Comunicação Ágil): O compilador gerou código lixo para \[loop de processamento de imagem]. Joguei em Assembly ARM e despencamos 40% de uso de ciclo.



\### Roteiro 05: Relatório de Exceção de Hardware (Kernel Panic / Hard Fault)

\* Variação 1 (Técnico Padrão): Durante a execução da instrução em \[endereço de memória 0x0800...], o processador disparou uma exceção de Hard Fault. O dump da pilha indica um estouro de pilha decorrente de recursão infinita na função.

\* Variação 2 (Relatório Executivo): O log de falha crítica apontou Hard Fault na posição \[endereço de memória], originado por stack overflow decorrente de chamadas recursivas não controladas.

\* Variação 3 (Slack / Comunicação Ágil): A placa deu Hard Fault em \[endereço de memória 0x0800...]. O stack estourou por causa de recursão infinita no código.



\### Roteiro 06: Plano de Rollback de Firmware

\* Variação 1 (Técnico Padrão): O último flash de firmware corrompeu a tabela de vetores de interrupção. O protocolo de emergência exige o curto-circuito do pino de boot para forçar o modo DFU e reverter para a versão estável anterior.

\* Variação 2 (Relatório Executivo): Devido à corrupção da tabela de vetores pós-gravação, aplicou-se o procedimento de recuperação via DFU para restaurar a integridade operacional anterior.

\* Variação 3 (Slack / Comunicação Ágil): O firmware novo corrompeu a tabela de vetores. Vou jumpear o pino de boot, entrar em DFU e voltar pro binário anterior.



\---



\## Bloco 2: Análise Crítica, Compilação e Abordagens de Baixo Nível



\### Roteiro 07: Ponderação de Trade-offs (Alocação Dinâmica vs. Estática)

\* Variação 1 (Técnico Padrão): O uso de malloc oferece flexibilidade de heap, mas introduz fragmentação e determinismo imprevisível. Em contrapartida, a alocação estática de memória em C garante previsibilidade absoluta de tempo de execução para sistemas críticos.

\* Variação 2 (Relatório Executivo): Embora o heap dinâmico traga flexibilidade, recomenda-se a adoção exclusiva de alocação estática para eliminar riscos de fragmentação em ambientes críticos.

\* Variação 3 (Slack / Comunicação Ágil): Nada de malloc aqui. Vamos usar alocação estática para garantir tempo de execução previsível e evitar fragmentação de memória.



\### Roteiro 08: Contestação de Comportamento Indefinido (Undefined Behavior)

\* Variação 1 (Técnico Padrão): A premissa de que o acesso direto a ponteiros não alinhados é seguro nesta arquitetura ignora as restrições do barramento. Na prática, isso aciona uma interrupção de desalinhamento de hardware.

\* Variação 2 (Relatório Executivo): A suposição de segurança no acesso a ponteiros não alinhados invalida-se pelas restrições físicas do barramento, gerando falhas de arquitetura.

\* Variação 3 (Slack / Comunicação Ágil): Achar que ponteiro desalinhado passa de graça nessa arquitetura é ilusão. Vai gerar exceção de hardware na hora.



\### Roteiro 09: Defesa de Padrão de Projeto de Driver (HAL)

\* Variação 1 (Técnico Padrão): A escolha de desacoplar o driver do chip \[PCA9685 / sensor I2C] via uma camada HAL customizada foi essencial para isolar o código de dependências diretas de registradores.

\* Variação 2 (Relatório Executivo): A implementação de uma camada HAL própria para o componente \[sensor I2C] garantiu o desacoplamento necessário frente a alterações diretas de registradores.

\* Variação 3 (Slack / Comunicação Ágil): Criei uma HAL própria pro \[PCA9685 / sensor I2C] para tirar a dependência direta dos registradores e modularizar o código.



\### Roteiro 10: Avaliação de Risco de Dívida Técnica em Firmware

\* Variação 1 (Técnico Padrão): Manter ponteiros nus sem checagem de limites de bounds em rotinas de parsing de pacotes UART acumula vulnerabilidades graves de estouro de buffer.

\* Variação 2 (Relatório Executivo): A ausência de validação de limites em ponteiros para parsing UART representa um vetor latente de buffer overflow que demanda remediação.

\* Variação 3 (Slack / Comunicação Ágil): Deixar ponteiro cru sem validar limite na leitura da UART é pedir para sofrer com buffer overflow depois.



\### Roteiro 11: Validação de Benchmark de Hardware

\* Variação 1 (Técnico Padrão): Os resultados do osciloscópio confirmam que a frequência de chaveamento PWM atingiu exatamente 1.6kHz após a reconfiguração dos registradores do timer.

\* Variação 2 (Relatório Executivo): A aferição instrumental via osciloscópio atestou a estabilização da frequência PWM em 1.6kHz após o ajuste registrador do timer.

\* Variação 3 (Slack / Comunicação Ágil): Medição no osciloscópio batida: o PWM cravou em 1.6kHz depois que reconfigurei os registradores do timer.



\### Roteiro 12: Desmistificação de Alocação de Memória

\* Variação 1 (Técnico Padrão): A crença de que variáveis locais em C desaparecem instantaneamente da RAM é equivocada; o espaço permanece no stack frame até ser sobrescrito por outra chamada de função.

\* Variação 2 (Relatório Executivo): É incorreto assumir a desatribuição imediata de variáveis locais da RAM; o contexto permanece armazenado no stack frame até nova sobrescrita.

\* Variação 3 (Slack / Comunicação Ágil): Achar que variável local some da RAM do nada é engano. O dado fica lá no stack frame até outra função sobrescrever o espaço.



\---



\## Bloco 3: Gestão de Projetos Embarcados e Prazos



\### Roteiro 13: Escalada de Bloqueio de Hardware (Blocker)

\* Variação 1 (Técnico Padrão): A ausência de sinal ACK no barramento I2C impede a inicialização do driver do motor Mecanum. Sem a correção do pull-up físico na placa, o desenvolvimento de cinemática está totalmente travado.

\* Variação 2 (Relatório Executivo): O progresso da cinemática encontra-se bloqueado por falha de resposta ACK no barramento I2C, decorrente de problemas no circuito de pull-up.

\* Variação 3 (Slack / Comunicação Ágil): O I2C não dá ACK e o motor Mecanum não inicializa. Sem corrigir o resistor de pull-up na placa, a cinemática fica travada.



\### Roteiro 14: Redefinição de Escopo de Arquitetura

\* Variação 1 (Técnico Padrão): As restrições de espaço de memória Flash no microcontrolador exigem a remoção de bibliotecas de log em tempo de execução para liberar 15KB para o novo protocolo de comunicação.

\* Variação 2 (Relatório Executivo): Devido à limitação de capacidade da Flash, suprimiram-se os logs em execução para alocar 15KB ao novo protocolo de comunicação.

\* Variação 3 (Slack / Comunicação Ágil): A Flash estourou o limite. Tivemos que arrancar os logs de execução para abrir 15KB para o protocolo novo.



\### Roteiro 15: Alinhamento de Prioridades de Compilação

\* Variação 1 (Técnico Padrão): Devem ser priorizadas as correções de vazamento de memória em C antes de iniciar a implementação do mapeamento de sensores LIDAR.

\* Variação 2 (Relatório Executivo): Estabelece-se como pré-requisito a mitigação de vazamentos de memória pré-existentes antes de prosseguir com a integração do LIDAR.

\* Variação 3 (Slack / Comunicação Ágil): Antes de mexer no mapeamento do LIDAR, precisamos limpar os vazamentos de memória em C. Prioridade absoluta.



\### Roteiro 16: Handoff de Código de Baixo Nível

\* Variação 1 (Técnico Padrão): A documentação da API de controle dos motores via registradores diretos foi atualizada no repositório para que o próximo engenheiro assuma a manutenção sem perda de contexto de pinagem.

\* Variação 2 (Relatório Executivo): O repositório foi atualizado com o mapeamento completo da API de motores para assegurar a continuidade técnica da manutenção.

\* Variação 3 (Slack / Comunicação Ágil): Atualizei o repositório com toda a documentação da API de motores e pinagem para quem for assumir o código não ficar perdido.



\### Roteiro 17: Relatório de Status de Compilação (Sprint)

\* Variação 1 (Técnico Padrão): Neste ciclo, zero warnings de compilação (-Wall -Wextra) foram tolerados, e todos os testes unitários de manipulação de ponteiros passaram no ambiente simulado.

\* Variação 2 (Relatório Executivo): O ciclo atual encerrou-se com conformidade estrita sob as flags `-Wall -Wextra` e aprovação em todos os testes unitários de ponteiros.

\* Variação 3 (Slack / Comunicação Ágil): Sprint fechada sem tolerar nenhum warning (`-Wall -Wextra` limpos) e testes unitários de ponteiros validados no simulador.



\### Roteiro 18: Negociação de Prazo para Otimização de Assembly

\* Variação 1 (Técnico Padrão): A reescrita manual de algoritmos críticos em Assembly para ganho de microssegundos exige mais 3 dias de validação em bancada com analisador lógico.

\* Variação 2 (Relatório Executivo): Solicita-se dilação de 3 dias no cronograma para validação instrumental em bancada da otimização crítica em Assembly.

\* Variação 3 (Slack / Comunicação Ágil): Para reescrever essas rotinas em Assembly e ganhar microssegundos de clock, preciso de mais 3 dias de testes na bancada com o analisador lógico.



\---



\## Bloco 4: Negociação Técnica e Mitigação de Conflitos em Pull Requests



\### Roteiro 19: Mediação de Impasse sobre Arquitetura de Software

\* Variação 1 (Técnico Padrão): Enquanto a equipe diverge entre usar interrupções ou polling para leitura serial, a melhor via arquitetural é implementar uma máquina de estados finos baseada em DMA.

\* Variação 2 (Relatório Executivo): Frente à divergência entre polling e interrupções, propõe-se a arquitetura unificada de máquina de estados controlada por DMA.

\* Variação 3 (Slack / Comunicação Ágil): Deixa de lado a discussão entre polling e interrupção; o ideal aqui é desenhar uma máquina de estados baseada em DMA.



\### Roteiro 20: Correção de Rota em Code Review (C/Assembly)

\* Variação 1 (Técnico Padrão): Neste Pull Request, o uso de strcpy sem validação de tamanho expõe o firmware a buffer overflow. Sugiro substituir por snprintf para garantir a segurança da stack.

\* Variação 2 (Relatório Executivo): Aponta-se vulnerabilidade potencial de buffer overflow por uso de strcpy neste PR, recomendando-se a substituição por snprintf.

\* Variação 3 (Slack / Comunicação Ágil): Nesse PR você usou `strcpy` sem checar tamanho e abriu brecha para buffer overflow. Troca por `snprintf` para blindar a stack.



\### Roteiro 21: Solicitação de Datasheet ou Especificação

\* Variação 1 (Técnico Padrão): A implementação da comunicação SPI está falhando porque o código assume uma polaridade de clock incompatível com o datasheet oficial do componente.

\* Variação 2 (Relatório Executivo): O erro de comunicação SPI decorre de desvio na configuração de polaridade do clock frente às especificações do fabricante.

\* Variação 3 (Slack / Comunicação Ágil): O SPI está quebrando porque a polaridade do clock no código não bate com o que está escrito no datasheet oficial.



\### Roteiro 22: Imposição de Condição Crítica para Deploy em Embarcados

\* Variação 1 (Técnico Padrão): Como condição inegociável para gravar o binário na placa física, o código deve passar por 48 horas de teste de estresse térmico e de consumo sem travamentos.

\* Variação 2 (Relatório Executivo): Estabelece-se como aceite mandatório para gravação em hardware a execução de 48 horas ininterruptas de teste térmico e elétrico.

\* Variação 3 (Slack / Comunicação Ágil): Para gravar o binário na placa final, a regra é clara: 48 horas de estresse térmico e de consumo sem travar, senão não sobe.



\### Roteiro 23: Redirecionamento de Discussão para Restrição de Hardware

\* Variação 1 (Técnico Padrão): O debate sobre a sintaxe do código é secundário; o gargalo real reside no fato de que o barramento SPI está operando acima da frequência máxima suportada pelo escravo.

\* Variação 2 (Relatório Executivo): Discordâncias estilísticas à parte, o problema crítico reside no excesso de frequência do barramento SPI em relação ao limite do componente escravo.

\* Variação 3 (Slack / Comunicação Ágil): Paruem de discutir a sintaxe do código. O gargalo real é que o barramento SPI está rodando acima da frequência que o chip escravo aguenta.



\### Roteiro 24: Validação de Consenso de Protocolo

\* Variação 1 (Técnico Padrão): Para confirmar o alinhamento: o microcontrolador atuará exclusivamente como mestre no barramento I2C, enviando os comandos de posição a cada 20 milissegundos.

\* Variação 2 (Relatório Executivo): Consolidou-se o entendimento de que o microcontrolador exercerá papel exclusivo de mestre I2C, transmitindo comandos a cada 20 ms.

\* Variação 3 (Slack / Comunicação Ágil): Para alinhar e fechar o protocolo: o microcontrolador vai mandar nos pacotes como mestre I2C e disparar os comandos a cada 20ms.



\---



\## Bloco 5: Narrativa Temporal e Relatos de Incidentes de Sistema



\### Roteiro 25: Post-Mortem de Falha de Firmware (Crash Histórico)

\* Variação 1 (Técnico Padrão): O rastreamento cronológico do incidente de ontem revelou que o estouro de pilha ocorreu exatamente após a chamada recursiva descontrolada na rotina de interrupção do timer.

\* Variação 2 (Relatório Executivo): A análise post-mortem indicou que o travamento decorreu de recursão descontrolada na interrupção do timer, esgotando a pilha de execução.

\* Variação 3 (Slack / Comunicação Ágil): Investigando o crash de ontem, descobrimos que o stack estourou bem na hora da chamada recursiva infinita na interrupção do timer.



\### Roteiro 26: Projeção de Carga de Processamento (Stress Test)

\* Variação 1 (Técnico Padrão): Simulando o envio simultâneo de dados por todas as seriais, projetamos que o uso de CPU atingirá 98%, exigindo a migração de rotinas críticas para Assembly puro.

\* Variação 2 (Relatório Executivo): Simulações de pico de tráfego serial apontam saturação de 98% da CPU, demandando a reescrita de rotinas críticas em Assembly.

\* Variação 3 (Slack / Comunicação Ágil): Simulei tráfego máximo em todas as seriais e a CPU bateu 98%. Vamos ter que jogar as rotinas críticas para Assembly puro.



\### Roteiro 27: Resumo Executivo de Arquitetura

\* Variação 1 (Técnico Padrão): A decisão técnica foi consolidada: adotaremos alocação estática de memória em C e drivers enxutos para garantir a máxima estabilidade do sistema embarcado.

\* Variação 2 (Relatório Executivo): Arquitetura aprovada: priorização de alocação estática em C e drivers simplificados para blindar a estabilidade do sistema.

\* Variação 3 (Slack / Comunicação Ágil): Arquitetura fechada: vamos de alocação estática em C e drivers enxutos para garantir que a placa não trave em campo.



\### Roteiro 28: Histórico Evolutivo de Firmware

\* Variação 1 (Técnico Padrão): O projeto evoluiu de um protótipo monolítico mal estruturado para uma arquitetura modular em C estrito, com separação clara entre HAL e lógica de controle.

\* Variação 2 (Relatório Executivo): O firmware evoluiu de estrutura monolítica para um design modular estrito em C, isolando a HAL das regras de negócio.

\* Variação 3 (Slack / Comunicação Ágil): O código saiu daquele protótipo monolítico bagunçado e virou uma estrutura modular limpa em C estrito, separando bem a HAL da lógica.



\### Roteiro 29: Contextualização de Impacto de Atualização de Toolchain

\* Variação 1 (Técnico Padrão): A migração para uma versão mais recente do GCC alterou o alinhamento de structs na memória, quebrando temporariamente a comunicação serial binária.

\* Variação 2 (Relatório Executivo): Alterações no alinhamento de estruturas de dados decorrentes da atualização do GCC impactaram o protocolo de transmissão serial binária.

\* Variação 3 (Slack / Comunicação Ágil): Atualizar a toolchain do GCC mudou o alinhamento das structs na RAM e acabou quebrando a comunicação serial binária temporariamente.



\### Roteiro 30: Síntese de Aprendizado em Engenharia de Baixo Nível

\* Variação 1 (Técnico Padrão): Concluímos este ciclo de otimização compreendendo profundamente como o gerenciamento manual de ponteiros em C impacta diretamente o consumo energético e a estabilidade do hardware.

\* Variação 2 (Relatório Executivo): O presente ciclo consolida o entendimento sobre os reflexos diretos do controle de ponteiros em C na performance energética e estabilidade do hardware.

\* Variação 3 (Slack / Comunicação Ágil): Fechando esse ciclo de estudo: ficou nítido como controlar ponteiro manualmente em C muda diretamente o consumo de energia e a estabilidade da placa.


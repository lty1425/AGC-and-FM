# AGC-and-FM
## Описание проекта
В данном проекте представлены файлы, необходимые для создания интегральных схем двух цифровых устройств:
1) Блок, осуществляющий автоматическую регулировку усиления (АРУ) с постоянной времени, равной 100 отсчетам. Для решения данной задачи была спроектирована логарифмическая АРУ, в которой в качестве ФНЧ был использован фильтр экспоненциального усреднения, функция логарифма аппроксимирована полиномом 4 порядка с помощью встроенной в Matlab функции polyfit, а аппроксимация экспоненты выполняется с помощью полиномов Чебышева. Разрядность входного сигнала составляет 13 бит, а разрядность выходного сигнала 39 бит.
2) Блок, осуществляющий демодуляцию частотно-модулированного сигнала. В связи с тем, что вычисление арктангенса трудно выполнить точно без привлечения значительных вычислительных ресурсов, была использована упрощенная схема демодуляции, состоящая исключительно из сумматоров, умножителей и элементов задержки. Данная схема может применяться для демодуляции «чистых» ЧМ-сигналов (то есть, амплитуда должна быть постоянной). Разрядность входного сигнала составляет 39 бит, а разрядность выходного сигнала 13 бит.
Совместная работа устройств возможно при наличии фильтра Гильберта, разработка цифровой интегральной схемы которого выходит за рамки данной работы. В связи с этим, схемы АРУ и ФМ-демодулятора выполнены как два отдельных устройства, работающие на тактовой частоте 10 МГц при неопределенности тактового сигнала 1%.
## Описание репозитория
В ветке Current_branch ведется разработка проекта, туда в первую очередь вносятся различные изменения, в том числе тестовые.
В ветке main содержится актуальная, работоспособная версия проекта. Все исходные файлы, требующиеся для сборки проекта находятся здесь.
## Описание файлов

AGC.v - Описание верхнего модуля блока АРУ на языке Verilog.
EXPONENTIAL_AVERAGING_FILTER.v - описание фильтра экспоненциального усреднения в составе блока АРУ на языке Verilog.
EXP_APPROX_CHEBYSHEV.v - описание блока аппроксимации экспоненты полиномами Чебышева на языке Verilog.
LN_X_MNK_0_001_to_5000.v - описание блока аппроксимации логарифма полиномом 4 порядка на языке Verilog.
AGC_tb.v - тестовое окружения для проведения симуляций на этапе Behavioral и после этапа Synthesis.
AGC_tb_layout.v - тестовое окружения для проведения симуляций после этапа Layout.
inp_agc.dat - Входной тестовый сигнал для проведения симуляций.
out_agc_expected.dat - Референсный выходной сигнал для проведения симуляций.
AGC.sdc - файл, содержащий информацию о временных ограничениях, необходим на этапах Synthesis и Layout.
AGC_pins - расположение пинов на топологии. Используется на этапе Layout.

X-FAB_typ_AGC.tcl, X-FAB_SLOW_AGC.tcl, X-FAB_FAST_AGC.tcl - скрипты, содержащие пути к библиотечным ячейкам для случаев typical corner, slow corner и fast corner соответственно. Используются на этапе Synthesis.
MyModule_synth_AGC_regs.tcl, MyModule_synth_AGC_regs_SLOW.tcl, MyModule_synth_AGC_regs_FAST.tcl - скрипты, содержащие команды для RTL Compiler для случаев typical corner, slow corner и fast corner соответственно. Используются на этапе Synthesis.
MMMC_AGC_regs.tcl - скрипт, содержащий информацию о библиотечных ячейках при различных условиях. Используется на этапе Layout.
Encounter_AGC.tcl - скрипт, содержащий команды для Encounter, необходимые для генерации топологии. Используется на этапе Layout

FM_demodulator.v - Описание верхнего модуля блока ФМ-демодулятора на языке Verilog.
FM_demodulator_tb.v - тестовое окружения для проведения симуляций на этапе Behavioral и после этапа Synthesis.
FM_demodulator_tb_layout.v - тестовое окружения для проведения симуляций после этапа Layout.
inp_I.dat, inp_Q.dat  - Входные тестовые сигналы для проведения симуляций.
out_fm_expected.dat - Референсный выходной сигнал для проведения симуляций.
FM.sdc  - файл, содержащий информацию о временных ограничениях, необходим на этапах Synthesis и Layout.
pin_FM_no_top - расположение пинов на топологии. Используется на этапе Layout.

X-FAB_typ_FM.tcl , X-FAB_SLOW_FM.tcl, X-FAB_FAST_FM.tcl - скрипты, содержащие пути к библиотечным ячейкам для случаев typical corner, slow corner и fast corner соответственно. Используются на этапе Synthesis.
MyModule_synth_FM.tcl, MyModule_synth_SLOW.tcl, MyModule_synth_FAST.tcl - скрипты, содержащие команды для RTL Compiler для случаев typical corner, slow corner и fast corner соответственно. Используются на этапе Synthesis.
MMMC_FM.tcl - скрипт, содержащий информацию о библиотечных ячейках при различных условиях. Используется на этапе Layout.
Encounter_FM.tcl  - скрипт, содержащий команды для Encounter, необходимые для генерации топологии. Используется на этапе Layout

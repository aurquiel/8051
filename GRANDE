CSEG AT 0000H                    ;COMIENZO DEL CÓDIGO

LJMP CONFIGURACION               ;SALTO A LA CONFIGURACION DEL MICRO

;-----INTERRUPCIONES-INICIO-----
ORG 0003H                       ;INTERRUPCION EXTERNA0, SALTO A SUBRUTINA DE INTERRUPCION
	LJMP EXTERNA0
ORG 000BH                       ;INTERRUPCION TIMER0, SALTO A SUBRUTINA DE INTERRUPCION
	LJMP TIMER0
ORG 0013H                       ;INTERRUPCION EXTERNA1, SALTO A SUBRUTINA DE INTERRUPCION
	LJMP EXTERNA1
ORG 001BH                       ;INTERRUPCION DEL TIMER1,SALTO A SUBRUTINA DE INTERRUPCION
	LJMP TIMER1
ORG 0023H
	LJMP PUERTO            ;INTERRUPCION DEL PUERTO SERIAL,SALTO A SUBRUTINA DE
	                       ;INTERRUPCION
;-----INTERRUPCIONES-FIN-------

INICIO:                         ;ESTE ES EL COMIENZO DE MI PROGRAMA PRINCIPAL

	;AQUI COLOCO LO QUE VOY A HACER
                                                                                                  
LJMP INICIO                     ;ESTE ES MI CICLO INFINITO                                            
                                                                                                      
CONFIGURACION:                  ;ETIQUETA A DONDE SALTO PARA CONFIGURAR EL MICRO
;-----INTERRUPCIONES-INICIO-----
        ;SETB/CLR EA            ;HABILITO O DESHABILITO INTERRUPCION GLOBAL 
        ;SETB/CLR ES            ;HABILITO O DESHABILITO INTERRUPCION PUERTO SERIAL
        ;SETB/CLR ET1           ;HABILITO O DESHABILITO INTERRUPCION DEL TEMPORIZADOR1 SE 
                                ;ACTIVA POR DESBORDE
        ;SETB/CLR ET0           ;HABILITO O DESHABILITO INTERRUPCION DEL TEMPORIZADOR0 SE 
                                ;ACTIVA POR DESBORDE
        ;SETB/CLR EX1           ;HABILITO O DESHABILITO INTERRUPCION EXTERNA1 SE ACTIVA POR 
                                ;FLANCO DE BAJADA
        ;SETB//CLR EX0          ;HABILITO Ó DESHABILITO INTERRUPCION EXTERNA0 SE ACTIVA POR 
                                ;FLANCO DE BAJADA
;-----INTERRUPCIONES-FIN--------
;-BANDERAS-INTERRUPCION-INCIO---
;SOLO PARA SABER CUALES SON LOS NOMBRES DE LOS BITS DE LAS BANDERAS
;TF1                            BANDERA DE INTERUPCION TIMER 1
;TF0                            BANDERA DE INTERUPCION TIMER 0
;IE1                            BANDERA DE INTERRUPCION EXTERNA SE BORRA MEDIANTE HARDWARE
;IT1        ;NO ES UNA BANDERA ES UN BIT DE CONTROL INT. EXTERNA 1 MEDIANTE SOFTWARE
;IE0                            BANDERA DE INTERRUPCION EXTERNA SE BORRA MEDIANTE SOFTWARE
;IT0        ;NO ES UNA BANDERA ES UN BIT DE CONTROL INT. EXTERNA 0 MEDIANTE SOFTWARE
;---BANDERAS-INTERRUPCION-FIN---
;-PRIORIDAD-INTERRUPCION-INICIO-
        ;SETB/CLR PS      ;PRIORIDAD DE INTERRUPCION DEL PUERTO SERIAL
        ;SETB/CLR PT1     ;PRIORIDAD DE INTERRUPCION DEL TEMPORIZADOR1
        ;SETB/CLR PX1     ;PRIORIDAD DE INTERRUPCION EXTERNA1
        ;SETB/CLR PT0     ;PRIORIDAD DE INTERRUPCION DEL TEMPORIZADOR0
        ;SETB/CLR PX0     ;PRIORIDAD DE INTERRUPCION EXTERNA0
;---PRIORIDAD-INTERRUPCION-FIN--
;-----CONFG-TIMERS-INICIO-------
;EL REGISTRO TMOD ESTÁ COMPUESTO POR LOS SIGUIENTES 7 BITS-INCIO
;-BIT-NOMBRE--TEMPORIZADOR--QUE HACE
;  7   GATE         1       ;BIT DE COMPUERTA. CUANDO ES 1, EL TEMPORIZADOR SOLO FUNCIONA
                            ;SI LA SEÑAL INTI ESTA A NIVEL ALTO
;  6   C/T          1       ;BIT DE SELECION CONTADOR TEMPORIZADOR 1=C O=T
;  5   M1           1       ;BIT DE MODO
;  4   M0           1       ;BIT DE MODO
;  3   GATE         0       ;BIT DE COMPUERTA. CUANDO ES 1, EL TEMPORIZADOR SOLO FUNCIONA
                            ;SI LA SEÑAL INTI ESTA A NIVEL ALTO
;  2   C/T          0       ;BIT DE SELECION CONTADOR TEMPORIZADOR 1=C O=T
;  1   M1           0       ;BIT DE MODO
;  0   M0           0       ;BIT DE MODO
;-----MODOS-TIMER-INICIO----
;M1=0 M0=0 MODO0 TEMPORIZADOR DE 13BITS
;M1=0 M0=1 MODO1 TEMPORIZADOR DE 16BITS
;M1=1 M0=0 MODO2 TEMPORIZADOR DE 8BITS AUTORECARGABLE CON LOS VALORES DE THX Y TLX
                            ;DESPUES DEL DESBORADMIENTO AUTOMATICAMENTE
;M1=1 M0=1 MODO3 TEMPORIZADOR DIVIDIDO EL TEMPORIZADOR 0 EN EL MODO 3 SE DIVIDE EN DOS 
                            ;TEMPORIZADORES, TL0 Y TH0 ACTÚAN COMO TEMPORIZADORES 
                            ;SEPARADOS, EN DONDE LOS DESBORDAMIENTOS ESTABLECEN 1 LOS BITS 
                            ;TF0 Y TF1, RESPECTIVAMENTE.
;-----MODOS-TIMERS-FIN------

;MOV TMOD,#XXXXXXXXB     ;CONFIGURACION DEL TMOD CON LO ANTERIORMENTE EXPUESTO

;--CALCULO-THX-TLX-INICIO---
;(1/12)(frecuencia del cristal)=A  ;FRECUENCIA PARA HACER UNA SOLA INSTRUCCIÓN
;B=(1/A)                           ;TIEMPO EN QUE SE TARDA PARA HACER UNA SOLA INSTRUCCIÓN
;C=(Tiempo que quiero)/B           ;APLICANDO UNA REGLA DE TRES
;SI EL TIMER ES DE 8 BITS SOLO HACE FALTA OBTENER TLX 
;THXTLX=(2^8 Ó 2^16 Ó 2^13)-C      ;NOTA TRANSFORMAR LA RESTA A HEXADECIMAL
;-----CALCULO-THX-TLX-FIN----

;-----CONFG-TIMERS-FIN----------

;--CONFIG-PUERTO-SERIAL-INICIO--
;-----REGISTRO SCON-INICIO------
;-BIT-NOMBRE--------------------QUE HACE
;  7   SM0                      ;MODO DEL PUERTO SERIAL
;  6   SM1                      ;MODO DEL PUERTO SERIAL
;  5   SM2                      ;HABILITA LA COMUNICACIÓN ENTRE MÚLTIPLES PROCESADORES EN
                                ;LOS MODOS 2 Y 3, R1 NO SE ACTIVARÁ SI EL NOVENO BIT ES 0
;  4   REN                      ;HABILITACION DEL RECEPTOR
;  3   TB8                      ;BIT DE TRANSMISIÓN 8. EL NOVENO BIT SE TRANSMITE EN LOS ;
                                ;MODOS 2 Y 3, ES PUESTO EN 1/0 MEDIANTE EL SOFTWARE
;  2   RB8                      ;BIT 8 DE RECEPCION
;  1   TI                       ;BANDERA DE INTERRUPCION DE TRANSMISION
;  0   RI                       ;BANDERA DE INTERRUPCION DE RECEPCION

 ;---MODOS_TRANSMISION-INICIO---
;SM1=0 SM0=0                    ;MODO1 REGISTRO DE DESPLAZAMIENTO VELOCIDAD FIJA         
                                ;(FRECUENCIA DEL OSCILADOR/12)
                                ;RXD SE USA COMO ENTRADA Y SALIDA AL MISMO TIEMPO TXD SE 
                                ;CONECTA COMO RELOJ POR CADA PULSO SE ENVIA UN DATO
;SM1=0 SM0=1                    ;MODO2 UART DE 8BITS VELOCIDAD VARIABLE TEMPORIZADOR1
;SM1=1 SM0=0                    ;MODO3 UART DE 9 BITS VELOCIDAD FIJA 1/32 Ó 1/64 
                                ;FRECUENCIA DEL OSCILADOR
;SM1=1 SM0=1                    ;MODO4 UART DE 9 BITS VELOCIDAD VARIABLE TEMPORIZADOR1
 ;----MODOS_TRANSMISION-FIN-----
;-------REGISTRO SCON-FIN-------

;---CALCULO DEL VALOR DEL TIMER1 PARA LA TASA DE TRANSMISION EN BAUDIOS-INICO----------
;TIMER1 DEBE ESTAR EN MODO 2  8BITS AUTRECARGABLE ES EL MODO MAS COMUN UTILIZADO
;TH1 = 256 - ((Crystal / 384) / Baud) SI PCON.7 ES CERO
;TH1 = 256 - ((Crystal / 192) / Baud) SI PCON.7 ES UNO
;PCON.7=SMOD ES UN BIT SE ACTIVA O DESACTIVA SEGUN EL CASO PARA DOBLAR LA FRECUENCIA DE BAUDI
;SETB TR1    ;SE ENCIENDE TIMER1 QUE ES EL QUE GENERA LA TASA DE TRANSMISION
;-----CALCULO DEL VALOR DEL TIMER1 PARA LA TASA DE TRANSMISION EN BAUDIOS-FIN-----------


;MOV SCON,#XXXXXXXB             ;INICIALIZO EL SCON PARA LA OPERACION

;----CONFIG-PUERTO-SERIAL-FIN---

;-------------------BANDERAS-INICIO-----------------------
;REGISTRO-PSW-INICIO-------------------------------------
;-BIT- NOMBRE-DIREECCION--QUE HACE
;  7   CY        D7H      ;Bandera de acarreo. Se activa si ocurre un acarreo
                          ;del bit 7 durante una suma, o se activa cuando
                          ;ocurre un préstamo al bit 7 durante una resta.
;  6   AC        D6H      ;Bandera de acarreo auxiliar. Se activa durante las
                          ;instrucciones de suma si ocurre un acarreo del
                          ;bit 3 hacia el bit 4 o si el resultado en el nibble
                          ;inferior está en el rango de 0AH a 0FH.
;  5   F0        D5H      ;Bandera 0. Disponible para el usuario para
                          ;propósitos generales.
;  4   RS1       D4H      ;Bit 1 de selección de banco de registros.
;  3   RS0       D3H      ;Bit 0 de selección de banco de registros.
;  2   OV        D2H      ;Bandera de desbordamiento. Se activa después de
                          ;una operación de suma o resta si ocurrió un
                          ;desbordamiento aritmético
;  1   -         D1H      ;-
;  0   P         D0H      ;Bandera de paridad. Se activa o borra mediante
                          ;hardware en cada ciclo de instrucción para
                          ;indicar un número impar/par de bits con el
                          ;valor de \u201c1\u201d en el acumulador.
 ;-------------------BANDERAS-FIN--------------------------

;OTRAS COSA A MENCIONAR QUE SPUEDEN SER IMPORTANTES
;LA MEMORIA DE BIT DE DIRECCIONAMIENTO DIRECTO DEL 20H AL 20F TODOS SON BITS DE DIRECCIONAMIENTO DIRECTO

LJMP INICIO                     ;AHORA DESPUES DE CONFIGURARLO  A DIVERTIRSE
                                ;ME VOY A MI CICLO INFINITO

RET


;---INTERRUPCIONES-SUBRUTINAS---
EXTERNA0:
	;CLR IE0		;LIMIPIO LA BANDERA DE LA INTERRUPCION EXTERNA0
RETI

TIMER0:
	;CLR TF0                ;LIMIPIO LA BANDERA DE LA INTERRUPCION DEL TIMER0
RETI

EXTERNA0:
	;CLR IE1		;LIMIPIO LA BANDERA DE LA INTERRUPCION EXTERNA1
RETI

TIMER1:
	;CLR TF1                ;LIMIPIO LA BANDERA DE LA INTERRUPCION DEL TIMER1
RETI

PUERTO:
        ;CLR RI                ;LIMIPIO LA BANDERA DE LA INTERRUPCION DE RECEPCION
        ;CLR TI                ;LIMIPIO LA BANDERA DE LA INTERRUPCION DE TRANSMISION
RETI

END                             ;INDICO EL FIN DE MI CODIGO EN LENGUAJE ENSAMBLADOR

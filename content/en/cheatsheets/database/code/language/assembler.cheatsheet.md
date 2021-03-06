---
title: assembler.cheatsheet

date: 2020-11-14T19:07:13+01:00
---#-#
#-# Operations
#-#

#-# Transfer

Name      Comment                         Code                 Operation                              O D I T S Z A P C
----      -------                         ----                 ---------                              -----------------
MOV       Move (copy)                     MOV dest,source      dest:=source                           . . . . . . . . .
XCHG      Exchange                        XCHG op1,op2         op1:=op2, op2:=op1                     . . . . . . . . .

STC       Set carry                       STC                  CF:=1                                  . . . . . . . . 1
CLC       Clear carry                     CLC                  CF:=0                                  . . . . . . . . 0
CMC       Complement carry                CMC                  CF:=-CF                                . . . . . . . . ±

STD       Set direction                   STD                  DF:=1 (string op's downwards)          . 1 . . . . . . .
CLD       Clear direction                 CLD                  DF:=0 (string op's upwards)            . 0 . . . . . . .

STI       Set interrupt                   STI                  IF:=1                                  . . 1 . . . . . .
CLI       Clear interrupt                 CLI                  IF:=0                                  . . 0 . . . . . .

PUSH      Push onto stack                 PUSH source          DEC SP, [SP]:=source                   . . . . . . . . .
PUSHF     Push flags                      PUSHF                O D I T S Z A P C 286+: also NT, IOPL  . . . . . . . . .
PUSHA     Push all general flags          POPA                 DI, SI, BP, SP, BX, DX, CX, AX         . . . . . . . . .

POP       Pop from stack                  POP dest             dest:=[SP], INC SP                     . . . . . . . . .
POPF      Pop flags                       POPF                 O D I T S Z A P C 286+: also NT, IOPL  ± ± ± ± ± ± ± ± ±
POPA      Pop all general registers       POPA                 DI, SI, BP, SP, BX, DX, CX, AX         . . . . . . . . .

CBW       Convert byte to word            CBW                  AX:=AL (signed)                        . . . . . . . . .
CWD       Convert word to double          CWD                  DX:AD:=AX (signed)                     ± . . . ± ± ± ± ±
CWDE      Conv word to extended double    CWDE                 EAX:=AX (signed)                       . . . . . . . . .

IN     i  Input                           IN dest,port         AL/AX/EAX:=byte/word/double of port    . . . . . . . . .
OUT    i  Output                          OUT port,source      Byte/word/double of port:=AL/AX/EAX    . . . . . . . . .


#-# Arithmetic

Name      Comment                         Code                 Operation                              O D I T S Z A P C
----      -------                         ----                 ---------                              -----------------
ADD       Add                             ADD dest,source      dest:=dest+source                      ± . . . ± ± ± ± ±
ADC       Add with carry                  ADC dest,source      dest:=dest+source+CF                   ± . . . ± ± ± ± ±

SUB       Substract                       SUB dest,source      dest:=dest-source                      ± . . . ± ± ± ± ±
SBB       Substract with borrow           SBB dest,source      dest:=dest-(source+CF)                 ± . . . ± ± ± ± ±

DIV       Divide (unsigned)               DIV op               op=byte: AL:=AX/op           AH:=rest  ? . . . ? ? ? ? ?
DIV       Divide (unsigned)               DIV op               op=word: AX:=DX:AX/op        DX:=rest  ? . . . ? ? ? ? ?
DIV  386  Divide (unsigned)               DIV op               op=doublew: EAX:=EDX:EAX/op EDX:=rest  ? . . . ? ? ? ? ?

IDIV      Signed integer divider          IDIV op              op=byte: AL:=AX/op           AH:=rest  ? . . . ? ? ? ? ?
IDIV      Signed integer divider          IDIV op              op=word: AX:=DX:AX/op        DX:=rest  ? . . . ? ? ? ? ?
IDIV 386  Signed integer divider          IDIV op              op=doublew: EAX:=EDX:EAX/op EDX:=rest  ? . . . ? ? ? ? ?

MUL       Multiply (unsigned)             MUL op               op=byte: AX:=AL*op          if AH=0 ♦  ± . . . ? ? ? ? ±
MUL       Multiply (unsigned)             MUL op               op=word: DX:AX:=AX*op       if DX=0 ♦  ± . . . ? ? ? ? ±
MUL  386  Multiply (unsigned)             MUL op               op=double: EDX:EAX:=EAX/op if EDX=0 ♦  ± . . . ? ? ? ? ±

IMUL   i  Signed integer multiply         IMUL op              op=byte: AX:=AL*op       if AL suff ♦  ± . . . ? ? ? ? ±
IMUL      Signed integer multiply         IMUL op              op=word: DC:AX:=AX*op    if AX suff ♦  ± . . . ? ? ? ? ±
IMUL 386  Signed integer multiply         IMUL op              op=double: EDX:EAX:=EAX*op if EAX . ♦  ± . . . ? ? ? ? ±

INC       Increment                       INC op               op:=op+1 (carry not affected)          ± . . . ± ± ± ± .
DEC       Decrement                       DEC op               op:=op-1 (carry not affected)          ± . . . ± ± ± ± .

CMP       Compare                         CMP op1,op2          op1-op2                                ± . . . ± ± ± ± ±

SAL       Shift arithmetic left           SAL op,quantity                                             i . . . ± ± ? ± ±
SAR       Shift arithmetic right          SAR op,quantity                                             i . . . ± ± ? ± ±
RCL       Rotate left through carry       RCL op,quantity                                             i . . . . . . . ±
RCR       Rotate right through carry      RCR op,quantity                                             i . . . . . . . ±
ROL       Rotate left                     ROL op,quantity                                             i . . . . . . . ±
ROR       Rotate right                    ROR op,quantity                                             i . . . . . . . ±


#-# Logic

Name      Comment                         Code                 Operation                              O D I T S Z A P C
----      -------                         ----                 ---------                              -----------------
NEG       Negate (two-complement)         NEG op               op:=0-op if op=0 then CF:=0 else CF:=1 ± . . . ± ± ± ± ±
NOT       Invert each bit                 NOT op               op:=¬op (invert each bit)              . . . . . . . . .
AND       Logical and                     AND dest,source      dest:=dest∧source                      0 . . . ± ± ? ± 0
OR        Logical or                      OR dest, source      dest:=dest∨source                      0 . . . ± ± ? ± 0
XOR       Logical exclusive or            XOR dest, source     dest:=dest (xor) source                0 . . . ± ± ? ± 0

SHL       Shift logical left              SHL op, quality                                             i . . . ± ± ? ± ±
SHR       Shift logical right             SHR op, quality                                             i . . . ± ± ? ± ±


#-# Misc

Name      Comment                         Code                 Operation                              O D I T S Z A P C
----      -------                         ----                 ---------                              -----------------
NOP       No operation                    NOP                  No operation                           . . . . . . . . .
LEA       Load effective address          LEA dest, source     dest:=address of source                . . . . . . . . .
INT       Interrupt                       INT nr               interrupts prog, runs spec int-prog    . . 0 0 . . . . .


#-# Legend

Symbol    Description
------    -----------
♦         Then CF:=0, OF:=0 else CF:=1, OF:=1
.         Blank
i         For more information se instruction specifications
±         Affected by this instruction
?         Undefined after this instruction



#-#
#-# Jumps
#-#

# Basic (flags remain unchanged)

Name      Comment                         Code                 Operation
----      -------                         ----                 ---------
CALL      Call subroutine                 CALL proc
RET       Return from subroutine          RET

JMP       Jump                            JMP dest
JE        Jump if equal                   JE dest              ≡ JZ
JZ        Jump if zero                    JZ dest              ≡ JE
JCXZ      Jump if CX is zero              JCXZ dest
JECXZ     Jump if ECX is zero             JECXZ dest
JP        Jump if parity (parity even)    JP dest              ≡ JPE
JPE       Jump if parity even             JPE dest             ≡ JP
JPO       Jump if parity odd              JPO dest             ≡ JNP

JNE       Jump if not equal               JNE dest             ≡ JNZ
JNZ       Jump if not zero                JNZ dest             ≡ JNE
JNP       Jump if no parity (parity odd)  JNP dest             ≡ JPO


# Unsigned (cardinal)

Name      Comment                         Code                 Operation
----      -------                         ----                 ---------
JA        Jump if above                   JA dest              ≡ JNBE
JAE       Jump if above or equal          JAE dest             ≡ JNB ≡ JNC
JB        Jump if below                   JB dest              ≡ JNAE ≡ JC
JBE       Jump if below or equal          JBE dest             ≡ JNA
JC        Jump if carry                   JC dest

JNA       Jump if not above               JNA dest             ≡ JBE
JNAE      Jump if not above or equal      JNAE dest            ≡ JB ≡ JC
JNB       Jump if not below               JNB dest             ≡ JAE ≡ JNC
JNBE      Jump if not below or equal      JNBE dest            ≡ JA
JNC       Jump if no carry                JNC dest


# Signed (integer)

Name      Comment                         Code                 Operation
----      -------                         ----                 ---------
JG        Jump if greater                 JG dest              ≡ JNBE
JGE       Jump if greater or equal        JGE dest             ≡ JNL
JL        Jump if less                    JL dest              ≡ JNGE
JLE       Jump if less or equal           JLE dest             ≡ JNG
JO        Jump if overflow                JO dest
JS        Jump if sign (= negative)       JS dest

JNG       Jump if not greater             JNG dest             ≡ JLE
JNGE      Jump if not greater or equal    JNGE dest            ≡ JL
JNL       Jump if not less                JNL dest             ≡ JGE
JNLE      Jump if ont less or equal       JNLE dest            ≡ JG
JNO       Jump if no overflow             JNO dest
JNS       Jump if no sign (= positive)    JNS dest



#-#
#-# General registers
#-#

                 EAX 386
                    │          AX
                    │    AH    │    AL
┌────────┬──────────┼──────────┼──────────┐
│        │          │          │          │ Accumulator
└────────┴──────────┴──────────┴──────────┘
31     24 23      16 15       8 7         0


                 EDX 386
                    │          DX
                    │    DH    │    DL
┌────────┬──────────┼──────────┼──────────┐
│        │          │          │          │ Data mul, div, IO
└────────┴──────────┴──────────┴──────────┘
31     24 23      16 15       8 7         0


                 ECX 386
                    │          CX
                    │    CH    │    CL
┌────────┬──────────┼──────────┼──────────┐
│        │          │          │          │ Count loop, shift
└────────┴──────────┴──────────┴──────────┘
31     24 23      16 15       8 7         0


                 EBX 386
                    │          BX
                    │    BH    │    BL
┌────────┬──────────┼──────────┼──────────┐
│        │          │          │          │ BaseX data ptr
└────────┴──────────┴──────────┴──────────┘
31     24 23      16 15       8 7         0



#-#
#-# Flags
#-#

┌───┬───┬───┬───┬───┬───┬───┬───┐  ┌───┬───┬───┬───┬───┬───┬───┬───┐
│ _ │ _ │ _ │ _ │ O │ D │ I │ T │  │ S │ Z │ _ │ A │ _ │ P │ _ │ C │
└───┴───┴───┴───┴───┴───┴───┴───┘  └───┴───┴───┴───┴───┴───┴───┴───┘

#-# Control (how instructions are carried out)

Flag      Name                         Comment
----      -------                      -------
D         Direction                    1 = String op's process down from high to low address
I         Interrupt                    Whether interrupts can occur. 1 = enabled
T         Trap                         Single step for debugging


#-# Status (result of operations)

Flag      Name                         Comment
----      -------                      -------
C         Carry                        Result of unsigned op. is too large or below zero. 1 = carry/borrow
O         Overflow                     Result of signed op. is too large or small. 1 = overflow/underflow
S         Sign                         Sign of result. Reasonable for integer only. 1 = neg / 0 = pos
Z         Zero                         Result of opertation is zero. 1 = zero
A         Aux. carry                   Similar to carry but restricted to low nibble only
P         Parity                       1 = result has even number of set bits



#-#
#-# Example
#-#

; Project Euler Problem #001
; -----
; If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9.
; The sum of these multiples is 23.
; Find the sum of all the multiples of 3 or 5 below 1000.

; Designed for OS X.
; To assemble and run:
; nasm -f macho project_euler_001.asm \
;   && ld -o project_euler_001 project_euler_001.o -arch i386 -lc -macosx_version_min 10.6 \
;   && ./project_euler_001

section .data
    format db "%i", 10, 0   ; printf output format

section .text
    global start            ; make entry point visible from outside
    extern _printf          ; make the external function available

start:
    and esp, 0xFFFFFFF0     ; round the stack pointer to the nearest multiple of 16
    sub esp, 16             ; we only need room for 2 stack args, but we create space for 4 to keep the stack aligned
    mov dword[esp], format  ; put the printf format as the 1st element in the stack
    mov ebx, 0              ; sum
    mov ecx, 1              ; counter
    mov esi, 3              ; 1st divisor
    mov edi, 5              ; 2nd divisor
    jmp for                 ; jump to the for loop

for:
    cmp ecx, 1000           ; did the counter reach 1000 yet?
    je finish               ; if so, we're done

                            ; check if multiple of 3
    mov eax, ecx            ; set the current counter value as the dividend
    xor edx, edx            ; clear the remainder register
    div esi                 ; divide eax by esi and store the quotient:remainder in eax:edx
    cmp edx, 0              ; is the remainder zero?
    je multiple             ; if so, go update the result

                            ; check if multiple of 5
    mov eax, ecx            ; set the current counter value as the dividend
    xor edx, edx            ; clear the remainder register
    div edi                 ; divide eax by edi and store the quotient:remainder in eax:edx
    cmp edx, 0              ; is the remainder zero?
    je multiple             ; if so, go update the result

    inc ecx                 ; increment counter
    jmp for                 ; next iteration

multiple:
    add ebx, ecx            ; add current element to the sum
    inc ecx                 ; increment counter
    jmp for                 ; next iteration

finish:
    mov dword[esp + 4], ebx ; put ebx as the 2nd element in the stack
    call _printf            ; call printf with the elements from the stack as arguments: printf(format, ebx)
    mov eax, 0x1            ; exit command to kernel
    mov ebx, 0x0            ; exit code
    int 0x80                ; make system call




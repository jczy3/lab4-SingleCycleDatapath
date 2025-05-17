# Lab 4 - Single Cycle Datapath 
# Issues/Bugs:<br>
An issue that I ran into was that I was having problems with noVNC. It disconnected me a few times but I was finally able to access Digital.<br>
# Assembly: <br>
|Instruction   | Binary | Hex    |
|--------------|--------|--------|
| and $t0 $t1 $t2 | 000000 01001 01010 01000 00000 100100| 0x012A4024 |
| addi $t3, $t4, 123    | 001000 01100 01011 0000000001111011 | 0x218B007B          |
| lw $t5, 135($t1)   | 	100011 01001 01101 0000000010000111 | 	0x8D2D0087          |
| sw $t3, 136($t1)    | 	101011 01001 01011 0000000010001000 | 	0xAD2B0088          |
| beq $t3, $zero, -10    | 	000100 01011 00000 1111111111110110 | 	0x1160FFF6          |
<br>
# init.asm tracing <br>
1. lw $v0 31($zero) <br>
$v0 = 0x00000056 <br>
2. add $v1 $v0 $v0 <br>
$v1 = 0x00000056 + 0x00000056 = 0x000000AC <br>
3. sw $v1 132($zero)<br>
Address 132 = 0x000000AC <br>
4. sub $a0 $v1 $v0<br>
$a0 = 0x000000AC - 0x00000056 = 0x00000056<br>
5. addi $a1 $v1 12<br>
$a1 = 0x000000AC + 0x0000000C = 0x000000B8<br>
6. and $a2 $a1 $v1<br>
$a2 = 0x000000B8 & 0x000000AC = 0x000000A8<br>
7. or $a3 $a2 $v0<br>
$a3 = 0x000000A8 | 0x00000056 = 0x000000FE<br>
8. nor $t0 $a2 $v0<br>
$t0 = ~(0x000000A8 | 0x00000056) = 0xFFFFFF01<br>
9. slt $a2 $a1 $a0<br>
$a2 = (0x000000B8 < 0x00000056) ? $a2 = 1 : $a2 = 0<br>
$a2 = 0<br>
10. beq $a2 $zero -8($zero)<br>
$a2 is 0, so branch to instruction 8 bytes or 2 instructions before.<br>
11. lw $t0 132($zero)<br>
$t0 = 0x000000AC<br>

**Register File**
|Reg. Name|Value |
|---------|------|
| `$v0`   | 0x00000056 |
| `$v1`   | 0x000000AC    |
| `$a0`   | 0x00000056    |
| `$a1`   | 0x000000B8    |
| `$a2`   | 0x00000000    |
| `$a3`   | 0x000000FE    |
| `$t0`   | 0x000000AC    |

**RAM**
|Address|Value       |
|------:|------------|
|`31`     | 0x00000056 |
|`132`    | 0x000000AC |
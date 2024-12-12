**To open .dig file, use the Digital program available at https://github.com/hneemann/Digital**

**Description**

This CPU is designed by using **Digital program.** The process starts
with loading a program into a **256 x 13-bit RAM** (Program RAM,
*pRAM*), where the instructions begin execution from address 0x00 until
a stop instruction is encountered. After execution, the CPU waits for a
signal to transmit the results stored in a **256 x 8-bit RAM** (Result
RAM, *rRAM*), displaying values at addresses 0x00 to 0x0F via an **8-bit
output** and **two 7-segment displays**.


**valid (1 bit):** Indicates the program has been fully executed and
results are ready to be sent.

**done (1 bit):** Signals completion of result transmission.

**output (8 bits):** Displays hexadecimal results stored in *rRAM* after
receiving the result signal.


<table>
<colgroup>
<col style="width: 10%" />
<col style="width: 25%" />
<col style="width: 63%" />
</colgroup>
<thead>
<tr class="header">
<th>Opcode</th>
<th>Instruction</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>00000</td>
<td>NOPE</td>
<td>Do nothing; skip to the next instruction</td>
</tr>
<tr class="even">
<td>00001</td>
<td>accA ← Operand</td>
<td>Store an 8-bit operand in accA</td>
</tr>
<tr class="odd">
<td>00010</td>
<td>accB ← Operand</td>
<td>Store an 8-bit operand in accB</td>
</tr>
<tr class="even">
<td>00011</td>
<td>accA ← accB</td>
<td>Copy the value from accB to accA</td>
</tr>
<tr class="odd">
<td>00100</td>
<td>accB ← accA</td>
<td>Copy the value from accA to accB</td>
</tr>
<tr class="even">
<td>00101</td>
<td>regC ← accA</td>
<td>Copy the value from accA to regC</td>
</tr>
<tr class="odd">
<td>00110</td>
<td>accA ← regC</td>
<td>Copy the value from regC to accA</td>
</tr>
<tr class="even">
<td>00111</td>
<td>regC ← M</td>
<td>Store the value from input M in regC</td>
</tr>
<tr class="odd">
<td>01000</td>
<td>regC ← N</td>
<td>Store the value from input N in regC</td>
</tr>
<tr class="even">
<td>01001</td>
<td>accA ← pRAM_adr[Operand]</td>
<td>Store the rightmost 8 bits from pRAM at the address specified by the
operand in accA</td>
</tr>
<tr class="odd">
<td>01010</td>
<td>accA ← rRAM_adr[Operand]</td>
<td>Store the value from rRAM at the address specified by the operand in
accA</td>
</tr>
<tr class="even">
<td>01011</td>
<td>rRAM_adr[Operand] ← accA</td>
<td>Store the value from accA in rRAM at the address specified by the
operand</td>
</tr>
<tr class="odd">
<td>01100</td>
<td>Jump to address Operand</td>
<td>Unconditionally jump to the address specified by the operand</td>
</tr>
<tr class="even">
<td>01101</td>
<td>Jump to address Operand if eq</td>
<td>Jump to the address specified by the operand if the equal flag is
1</td>
</tr>
<tr class="odd">
<td>01110</td>
<td>Jump to address Operand if gr</td>
<td>Jump to the address specified by the operand if the greater flag is
1</td>
</tr>
<tr class="even">
<td>01111</td>
<td>Jump to address Operand if le</td>
<td>Jump to the address specified by the operand if the lesser flag is
1</td>
</tr>
<tr class="odd">
<td>10000</td>
<td>Jump to address Operand if eq or gr</td>
<td>Jump to the address specified by the operand if either the equal
flag or greater flag is 1</td>
</tr>
<tr class="even">
<td>10001</td>
<td>accA ← accA + accB</td>
<td>Add accA and accB and store the result in accA (2’s complement
arithmetic, ignore overflow)</td>
</tr>
<tr class="odd">
<td>10010</td>
<td>accA ← accA - accB</td>
<td>Subtract accB from accA and store the result in accA (2’s complement
arithmetic, ignore overflow)</td>
</tr>
<tr class="even">
<td>10011</td>
<td>accA ← accA * accB</td>
<td>Multiply accA[3..0] by accB[3..0] and store the result in accA
(4-bit unsigned multiplication)</td>
</tr>
<tr class="odd">
<td>10100</td>
<td>accA ← accA / accB</td>
<td>Perform unsigned division of accA by accB and store the result in
accA</td>
</tr>
<tr class="even">
<td>10101</td>
<td>accA ← accA % accB</td>
<td>Perform unsigned modulo of accA by accB and store the result in
accA</td>
</tr>
<tr class="odd">
<td>10110</td>
<td>accA ← accA ^ accB</td>
<td>Compute accA[2..0] raised to the power of accB[2..0] and store the
result in accA (ignore overflow)</td>
</tr>
<tr class="even">
<td>10111</td>
<td>accA CMP accB</td>
<td><p>Compare accA and accB using 2’s complement:</p>
<p>- If accA == accB, set the equal flag to 1</p>
<p>- If accA &gt; accB set greater flag to 1</p>
<p>- If accA &lt; accB set lesser flag to 1</p></td>
</tr>
<tr class="odd">
<td>11000</td>
<td>accA ← NOT(accA)</td>
<td>Bitwise NOT accA and store the result in accA</td>
</tr>
<tr class="even">
<td>11001</td>
<td><p>accA ←</p>
<p>accA AND accB</p></td>
<td>Bitwise AND accA and accB and store the result in accA</td>
</tr>
<tr class="odd">
<td>11010</td>
<td><p>accA ←</p>
<p>accA OR accB</p></td>
<td>Bitwise OR accA and accB and store the result in accA</td>
</tr>
<tr class="even">
<td>11011</td>
<td><p>accA ←</p>
<p>accA XOR accB</p></td>
<td>Bitwise XOR accA and accB and store the result in accA</td>
</tr>
<tr class="odd">
<td>11100</td>
<td><p>accA ←</p>
<p>accA &lt;&lt; accB</p></td>
<td>Left shift accA by the value of accB and store the result in
accA</td>
</tr>
<tr class="even">
<td>11101</td>
<td>isPrime(accA)</td>
<td>Check if accA is a prime number; if true, set the equal flag to
1</td>
</tr>
<tr class="odd">
<td>11111</td>
<td>STOP</td>
<td>Halt execution and wait for the result signal</td>
</tr>
</tbody>
</table>

**This project was developed as part of the CEDT Final Project 2024:
Digital Logic (2110252)**

<h1>samsung-riscv</h1>
<html lang="en">
<body>
<h2>Basic Details</h2>
<b>Name:</b> Bhavya Y
<br>
<b>College:</b> Dayananda Sagar College Of Engineering
<br>
<b>Email:</b> <a href="mailto:demogorgan6627@gmail.com">demogorgan6627@gmail.com</a>
<br>
<b>GitHub Profile:</b> <a href="https://github.com/BHAVYA9-Y">BHAVYA9-Y</a>
<hr>
<!-- Task 1 -->
<details>
<p><summary>
<b>Task 1:</b> Task is to install RISC-V toolchain using VDI link provided,Compiling the C code and Using RISV options O1 and Ofast
</summary></p>
<b>1. Install Ubuntu 18.04 LTS(beaver) on Oracle Virtual Machine Box and open VDI file provided</b>
<br><br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/VM%20Box.png"  alt=Virtual Machine>
<br><br>
<b>2. Compiling C code </b>
<br><br>
<pre><code>cd
gedit sum1ton.c
gcc sum1ton.c
./a.out</code></pre>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/C%20Code.png" alt=C code>
<br><br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/C%20Code%20Output.png"       alt=commands for c compilation>
<br><br>
<b>3. Object Dump and O1 & Ofast Output</b>
<br><br>
<pre><code>cat sum1ton.c
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
ls -ltr sum1ton.o
</code></pre>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/Assembly%20Commands.png"    alt=Commands >
<br><br>
<pre><code>riscv64-unknown-elf-objdump -d sum1ton.o |less </code></pre>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/Object%20Dump.png"  alt=Object dump>
<br><br>
<b>For O1: The number of instructions were 15.</b><br><br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/O1%20Output.png"  alt=O1 output>
<br><br>
<pre><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c</code></pre>
<br>
<b>For Ofast: the number of instructions were 12.</b><br><br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/Ofast%20Output.png"  alt=Ofast output>
<br><br>
</details>
<hr>
    

<!-- End of Task 1-->
<!-- Task 2 -->
<!-- Spike for Sum1ton -->				
<details>
<p><summary>
<b>Task 2:</b> Run and observe the performance of SPIKE Simulation and  under the -O1 and -Ofast Compiler optimization flags.
</summary></p>
<details>
<p><summary>1. Sum of Integers from 1 to n</summary></p>
<b>Debugging sum1ton.o for O1</b>
<pre><p><code>riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
ls -ltr sum1ton.o
spike pk sum1ton.o
spike -d pk sum1ton.o</code></p></pre>
<b>O1 assembly output</b>
<pre>0000000000010184 &ltmain&gt:
   10184:       ff010113                addi    sp,sp,-16
   10188:       00113423                sd      ra,8(sp)
   1018c:       09600793                li      a5,150
   10190:       fff7879b                addiw   a5,a5,-1
   10194:       fe079ee3                bnez    a5,10190 &lt;main+0xc&gt;
   10198:       00003637                lui     a2,0x3
   1019c:       c3d60613                addi    a2,a2,-963 # 2c3d &lt;__BSS_END__+0x5710c&gt;
   101a0:       09600593                li      a1,150
   101a4:       00021537                lui     a0,0x21
   101a8:       19050513                addi    a0,a0,400 # 21190 &lt;__clzdi2+0x48&gt;
   101ac:       26c000ef                jal     ra,10418 &lt;printf&gt;
   101b0:       00000513                li      a0,0
   101b4:       00813083                ld      ra,8(sp)
   101b8:       01010113                addi    sp,sp,16
   101bc:       00008067                ret
</pre>
<p>15 instructions for O1</p>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%202/O1_spike_sum.png" alt="debugging O1">
<br><br>
<b>Debugging sum1ton.o for Ofast</b>
<pre><p><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
spike pk sum1ton.o
spike -d pk sum1ton.o</code></p></pre>
<b>Ofast assembly output</b>
<pre>00000000000100b0 &ltmain&gt:
   100b0:       00003637                lui     a2,0x3
   100b4:       00021537                lui     a0,0x21
   100b8:       ff010113                addi    sp,sp,-16
   100bc:       c3d60613                addi    a2,a2,-963 # 2c3d &lt;main-0xd473&gt;
   100c0:       09600593                li      a1,150
   100c4:       18050513                addi    a0,a0,384 # 21180 &lt;__clzdi2+0x44&gt;
   100c8:       00113423                sd      ra,8(sp)
   100cc:       340000ef                jal     ra,1040c &lt;printf&gt;
   100d0:       00813083                ld      ra,8(sp)
   100d4:       00000513                li      a0,0
   100d8:       01010113                addi    sp,sp,16
   100dc:       00008067                ret
</pre>
<p>12 instructions for Ofast</p>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%202/Ofast_spike_sum.png" alt="debugging Ofast">
</details>	   
                                             <!-- Spike for Square -->	   
<details>
<p><summary>2. Square of a Number</summary></p>
<b>Compiling Square C program</b>
<pre><code>gedit square.c
gcc square.c
./a.out</code></pre>
<pre><code>#inlcude&ltstdio.h&gt
int main(){
               int num = 250;
               int square=num*num;
                printf("The square of %d is %d\n",n,square);
        return 0;
                       }
                   </code></pre>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%202/example%20c%20code%20.png", alt="Square Compilation">
<br><br>
<b>Debugging square.o for O1</b>
<pre><p><code>riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o square.o square.c
spike pk square.o
spike -d pk square.o</code></p></pre>
<b>O1 assembly output</b>
<pre>0000000000010184 &lt;main&gt;:
   10184:       ff010113                addi    sp,sp,-16
   10188:       00113423                sd      ra,8(sp)
   1018c:       0000f637                lui     a2,0xf
   10190:       42460613                addi    a2,a2,1060 # f424 &lt;register_fini-0xc8c&gt;
   10194:       0fa00593                li      a1,250
   10198:       00021537                lui     a0,0x21
   1019c:       18050513                addi    a0,a0,384 # 21180 &lt;__clzdi2+0x44&gt;
   101a0:       26c000ef                jal     ra,1040c &lt;printf&gt;
   101a4:       00000513                li      a0,0
   101a8:       00813083                ld      ra,8(sp)
   101ac:       01010113                addi    sp,sp,16
   101b0:       00008067                ret
</pre>
<p>12 instructions for O1</p>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%202/O1_spike_square.png",alt="Debug O1">
<br><br>
<b>Debugging square.o for Ofast</b>
<pre><p><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o square.o square.c
spike pk square.o
spike -d pk square.o</code></p></pre>
<b>Ofast assembly output</b>  
<pre>00000000000100b0 &lt;main&gt;:
   100b0:       0000f637                lui     a2,0xf
   100b4:       00021537                lui     a0,0x21
   100b8:       ff010113                addi    sp,sp,-16
   100bc:       42460613                addi    a2,a2,1060 # f424 &lt;main-0xc8c&gt;
   100c0:       0fa00593                li      a1,250
   100c4:       18050513                addi    a0,a0,384 # 21180 &lt;__clzdi2+0x44&gt;
   100c8:       00113423                sd      ra,8(sp)
   100cc:       340000ef                jal     ra,1040c &lt;printf&gt;
   100d0:       00813083                ld      ra,8(sp)
   100d4:       00000513                li      a0,0
   100d8:       01010113                addi    sp,sp,16
   100dc:       00008067                ret
</pre>
<p>12 instructions for Ofast</p>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%202/Ofast_spike_square.png",alt="Ofast debug">
<br><br>
</details>
</details>
<hr>   
                                              
<!-- End of Task 2-->
<!-- Task 3 -->
<!-- Objdump instructions-->
<details>
  <p><summary>
    <b>Task 3:</b> 15 unique instructions are determined in the riscv-objdump of code,As it gives exact 32-bit instruction code in their respective instruction type formats.
  </summary></p>

<b>Debugging code to get objdump instructions</b>
<pre><p><code>riscv64-unknown-elf-objdump -d square.o</code></p></pre>
<b>Ofast assembly output</b>
<pre> 00000000000100b0 &ltmain&gt:
   100b0:       00003637                lui     a2,0x3
   100b4:       00021537                lui     a0,0x21
   100b8:       ff010113                addi    sp,sp,-16
   100bc:       c3d60613                addi    a2,a2,-963 # 2c3d &lt;main-0xd473&gt;
   100c0:       09600593                li      a1,150
   100c4:       18050513                addi    a0,a0,384 # 21180 &lt;__clzdi2+0x44&gt;
   100c8:       00113423                sd      ra,8(sp)
   100cc:       340000ef                jal     ra,1040c &lt;printf&gt;
   100d0:       00813083                ld      ra,8(sp)
   100d4:       00000513                li      a0,0
   100d8:       01010113                addi    sp,sp,16
   100dc:       00008067                ret
</pre>
<br>
<img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%203/Ofast%20objdump.png?raw=true">
<br><br>


<h3><b>32 bit instruction format for 15 unique RISC-V instructions:</b></h3>
<br>
<b>1.Instruction code for lui a2,0xf </b>
<br>
<img src="![Image](https://github.com/user-attachments/assets/bff39d8b-0317-4a2c-905f-05724cef98b0)">
<br><br>
<p>
  It is an I-type riscv instruction <br>
<b>Breakdown:</b><br>
  a.opcode:0110111 <br>
  b.Destination register rd:01100(a2/x12) <br>
  c.Immediate imm[31:12]:0000 0000 0000 1111(0xf) <br>
</p>
<p>
<b>Machine code:</b> <br>
  <pre><p><code> Binary:0000000000001111011000110111 <br> Hexadecimal:000F637 </code></p></pre>
</p>
<b>2.Instruction code for lui a0,0x21</b> <br>
<img src="![Image](https://github.com/user-attachments/assets/8ee106e0-abc3-4a16-836b-a12ab9e41886)">
<br><br>
<p>
   It is an I-type riscv instruction <br>
<b>Breakdown:</b> <br>
  a.opcode:0110111 <br>
  b.Destination register rd:01010(a0,x10) <br>
  c.Immediate imm[31:12]:0000 0010 0001 0000 0000 0000(0x21) <br>
</p>
<p>
<b>Machine code:</b> <br>
   <pre><p><code> Binary: 000000100001000000000000010100110111 <br> Hexadecimal: 0x21000537 </code></p></pre>
</p>
<b>3.Instruction code for addi sp,sp,-16</b> <br>
<img src="![Image](https://github.com/user-attachments/assets/098fe60b-6899-4cac-b9f2-94ade3154be8)">
<br><br>
<p>
   It is an I-type riscv instruction <br>
<b>Breakdown:</b> <br>
  a.opcode:0010011 <br>
  b.Source register sp:00010(x2) <br>
  c.Destination register sp:00010(x2) <br>
  d.Immediate Imm[11:0]:111111111000(-16) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:111111111000 00010 000 00010 001011 <br> Hexadecimal:0xfff08093</code></p></pre>
</p>
<b>4.Instruction code for addi a2,a2,1060</b> <br>
<img src="![Image](https://github.com/user-attachments/assets/7d8759ab-d47a-44ce-919c-3c8a36de29e1)">
<br><br>
<p>
   It is an I-type riscv instruction <br>
<b>Breakdown:</b> <br>
  a.opcode:0010011 <br>
  b.Source register a2:01010(x10) <br>
  c.Destination register a2:01010(x10) <br>
  d.Imm[11:0]:000001000001(1060) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000001000001 01010 000 01010 0010011 <br> Hexadecimal:0x041 0x2A 0x0 0x2A 0x13</code></p></pre>
</p>
<b>5.Instruction code for li a1,250 </b> <br>
<img src="![Image](https://github.com/user-attachments/assets/de9d30ce-2ee5-4a8b-b34f-e1ec2060ccff)">
<br><br>
<p>
  It is a pseudo riscv instruction<br>
  Translated to ADDI a1,x0,250 <br>
  <b>Breakdown:</b> <br>
  a.opcode:0010011 <br>
  b.Source register rs1:00000(x0) <br>
  c.Destination register rd:01011(a1=x11) <br>
  d.Imm[11:0]:000000111110(250) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000000111110 00000 000 01011 0010011 <br> Hexadecimal:0x07F00513</code></p></pre>
</p>
<b>6.Instruction code for addi a0,a0,384</b> <br>
<img src="![Image](https://github.com/user-attachments/assets/d465d684-14df-4a08-91aa-3c85d0ed94e1)">
<br><br>
<p>
  It is an I-type riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:0010011 <br>
  b.Source register rs1:01010(a0=x10) <br>
  c.Destination register rd:01010(a0=x10) <br>
  d.Imm[11:0]:000000001100(384) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000000001100 01010 000 01010 0010011 <br> Hexadecimal:00C 2A 0 2A 13</code></p></pre>
</p>
<b>7.Instruction code for sd ra,8(sp) </b> <br>
<img src="![Image](https://github.com/user-attachments/assets/b1e226c5-4c56-4772-b9d0-423112eb6b56)">
<br><br>
<p>
  It is an S-type riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:0100011 <br>
  b.Source register 1 rs1:00010(sp=x2) <br>
  c.Source register 2 rs2:00001(ra=x1) <br>
  d.Imm[11:5]:0000000 01000(8) <br>
  e.Funct3:011 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000000001000 00010 011 00001 0100011 <br> Hexadecimal:0x00826146</code></p></pre>
</p>
<b>8.Instruction code for jal ra,1040c </b> <br>
<img src="![Image](https://github.com/user-attachments/assets/36b70685-a5f2-4c9f-92d3-59abe405c5b9)">
<br><br>
<p>
  It is an J-type riscv instruction <br>
  Offset:Address difference to 1040c(relative to pc),Assuming pc=100b4 <br> Offset=1040c-100b4=3c8 <br>
  <b>Breakdown:</b> <br>
  a.opcode:1101111<br>
  b.Destination register rd[11:7]:00001(x1=ra) <br>
  c.Offset[20]:0 <br>
  d.Offset[10:1]:0000111100(0x3c8 in bits) <br>
  e.Offest[11]:1 <br>
  f.Offset[19:12]:00000011<br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000000110011 1 0000111100 00001 1101111 <br> Hexadecimal:1B 1 FC 1 DF</code></p></pre>
</p>
<b>9.Instruction code for ld ra,8(sp)</b><br>
<img src="![Image](https://github.com/user-attachments/assets/c845e032-bc19-4988-b219-ee029af73100)">
<br><br>
<p>
  It is an I-type riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:0000011 <br>
  b.Source register rs1:00010(sp=x2) <br>
  c.Destination register rd:00001(ra=x1) <br>
  d.Imm[11:5]:0000000001000(8) <br>
  e.Funct3:011 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:0000000001000 00010 011 00001 0000011 <br> Hexadecimal:0x00810203</code></p></pre>
</p>
<b>10.Instruction code for li a0,0 </b> <br>
<img src="![Image](https://github.com/user-attachments/assets/d08beabd-e9eb-48bb-bc80-6788a8b59cd9)"> 
<br><br>
<p>
  It is a pseudo riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:0010011 <br>
  b.Source register rs1:00000(x0=0) <br>
  c.Destination register rd:01010(x10=a0) <br>
  d.Imm[31:20]:(000000000000) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000000000000 00000 000 01010 0010011 <br> Hexadecimal:0x00000513</code></p></pre>
</p>
<b>11.Instruction code for addi sp,sp,16</b><br>
<img src="![Image](https://github.com/user-attachments/assets/caa587dd-1bdb-42fe-b612-b843281797eb)">
<br><br>
<p>
  It is an I-type riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:0010011 <br>
  b.Source register rs1:00010(sp=x2) <br>
  c.Destination register rd:00010(sp=x2) <br>
  d.Imm[11:0]:000000001000(16) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000000001000 00010 000 00010 0010011 <br> Hexadecimal:0x01008093</code></p></pre>
</p>
<b>12.Instruction code for ret</b>
<img src="![Image](https://github.com/user-attachments/assets/aa58be22-f30a-416a-a859-44fe45e61e51)">
<br><br>
<p>
  It is a pesudo riscv instruction <br>
  It is similar to jalr Instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:1100111 <br>
  b.Source register rs1:00001(x1=ra) <br>
  c.Destination register rd:00000(x0=discard) <br>
  d.Imm[31:20]:000000000000 <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:000000000000 00001 000 00000 1100111<br> Hexadecimal:0x00008067</code></p></pre>
</p>
<b>13.Instruction code for auipc a5,0xffff0</b> <br>
<img src="![Image](https://github.com/user-attachments/assets/f26e0cc3-fb96-4e1d-b02b-25bc59d2486a)">
<br><br>
<p>
  It is an U-type riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:0010111 <br>
  b.Destination register rd:01111(a5=x15) <br>
  c.Imm[31:12]:00001111111111111111(0xffff) <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:00001111111111111111 01111 0010111<br> Hexadecimal:FFFF 17 17</code></p></pre>
</p>
<b>14.Instruction code for addi a5,a5,-224 </b> <br>
<img src="![Image](https://github.com/user-attachments/assets/fc8d8fcb-015d-4d5b-ac13-2288f78ec6d0)">
<br><br>
<p>
  It is an I-type riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:0010011 <br>
  b.Source register rs1:01111(a5) <br>
  c.Destination register rd:01111(a5) <br>
  d.Imm[11:0]:1111111111100000(-224 2's complement) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:1111111111100000 01111 000 01111 001011<br> Hexadecimal:FFE0 1F 0 1F 2B</code></p></pre>
</p>
<b>15.Instruction code for beqz a5,100f8</b><br>
<img src="![Image](https://github.com/user-attachments/assets/f1fb17c8-f931-4de7-b4b1-fb691bcb2cae)">
<br><br>
<p>
  It is a psuedo riscv instruction <br>
  <b>Breakdown:</b> <br>
  a.opcode:1100011 <br>
  b.Source register rs1:01111(a5) <br>
  c.Source register rs2:00000(x0) <br>
  d.Imm[11:0]:0000000111100000(100f8) <br>
  e.Funct3:000 <br>
</p>
<p>
<b>Machine code</b> <br>
   <pre><p><code> Binary:0000000111100000 01111 000 00000 1100011 <br> Hexadecimal:0x00F0780C3</code></p></pre>
</p>
</details>

<!-- end of Task 3 -->

<hr>       
</body>
</html>

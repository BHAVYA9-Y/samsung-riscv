# samsung-riscv
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
               int square=num*num
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
                                              <!--End of Task 2-->
       
</body>
</html>

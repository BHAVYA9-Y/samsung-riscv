# samsung-riscv
<h2>Basic Details</h2>
<b>Name:</b> Bhavya Y
<br>
<b>College:</b> Dayananda Sagar College Of Engineering
<br>
<b>Email:</b> <a href="demogorgan6627@gmail.com">demogorgan6627@gmail.com</a>
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
    <img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/created%20virtual%20machine.jpg"  alt=Virtual Machine>
    <br><br>
    <b>2. Compiling C code </b>
    <br><br>
    <pre><code>
    cd
    gedit sum1ton.c
    gcc sum1ton.c
    ./a.out</code></pre>
    <br>
    <img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/example%201.jpg" alt=C code>
    <br><br>
    <img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/c%20code%20compilation.jpg"       alt=commands for c compilation>
    <br><br>
    <b>3. Object Dump and O1 & Ofast Output</b>
    <br><br>
    <pre><code>
    cat sum1ton.c
    riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
    ls -ltr sum1ton.o
    </code></pre>
    <br>
    <img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/command%20for%20options1%20and%20fast.jpg"    alt=Commands >
    <br><br>
    <pre><code>riscv64-unknown-elf-objdump -d sum1ton.o |less </code></pre>
    <br>
    <img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/command%20objdump.jpg"  alt=Object dump>
      <br><br>
      <b>For O1: The number of instructions were 15.</b><br><br>
    <img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/o1%20output.jpg"  alt=O1 output>
    <br><br>
    <pre><code>riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c</code></pre>
    <br>
      <b>For Ofast: the number of instructions were 12.</b><br><br>
    <img src="https://github.com/BHAVYA9-Y/samsung-riscv/blob/main/Task%201/ofast%20output.jpg"  alt=Ofast output>
    <br><br>
    </details>
<hr>
<!-- End of Task 1-->


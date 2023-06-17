# GCC-MISRAC-Checker
#### A GCC-based MISRA-C checker for single-translation-unit-labeled rules.

By Chih-Yuan Chen, Yung-An Fang, Guan-Ren Wang, and Peng-Sheng Chen (High-Performance Computing laboratory, [Chung Cheng University](https://www.ccu.edu.tw/).)

This work targeted at MISRA-C:2012 (the third edition of the specification) Amendment 1. The detailed design information can be obtained from [our paper](https://www.tandfonline.com/doi/full/10.1080/09540091.2023.2222934).

- Chih-Yuan Chen, Yung-An Fang, Guan-Ren Wang & Peng-Sheng Chen (2023) A GCC-based checker for compliance with MISRA-C's single-translation-unit rules, Connection Science, 35:1, DOI: [10.1080/09540091.2023.2222934](https://doi.org/10.1080/09540091.2023.2222934)

----------------------------

#### Building GCC-MISRAC checker

There may be some bugs in the code where we added the compiler option  "**-Wmisra-c**". Therefore, we need to compile the original GCC compiler, then overwrite the modified source code, and finally compile the modified source code that we have modified.

1. Install some required libraries using apt-get.

   ```
   $ sudo apt-get update
   $ sudo apt-get install build-essential libgmp-dev libmpfr-dev libmpc-dev 
   ```

   

2. Download GCC 7.5.0 source code: gcc-7.5.0.tar.xz

   

3. Download the directory misrac-gcc-changed-only

   

4. Uncompress gcc-7.5.0.tar.xz

   ```
   $ tar -Jxvf gcc-7.5.0.tar.xz
   ```

   

5. Copy misrac-gcc-changed-only/c-family/c.opt to gcc-7.5.0/gcc/c-family/

   ```
   $ cp misrac-gcc-changed-only/c-family/c.opt ./gcc-7.5.0/gcc/c-family/
   ```

   

6. Build GCC

   ```
   $ mkdir build-misrac-gcc
   $ cd build-misrac-gcc
   $ ../gcc-7.5.0/configure --prefix=/usr/local/misrac --disable-multilib --disable-bootstrap --enable-languages=c -v
   $ make
   ```

   

7. Replace the original files with the modified files.

   ```
   $ cd ..
   $ cp -R ./misrac-gcc-changed-only/c-family ./gcc-7.5.0/gcc/
   $ cp -R ./misrac-gcc-changed-only/c ./gcc-7.5.0/gcc/
   $ cp -R ./misrac-gcc-changed-only/libcpp ./gcc-7.5.0/
   ```

   

8. Re-build GCC

   ```
   $ cd build-misrac-gcc
   $ make
   ```

   

9. Install GCC-MISRAC checker

   ```
   $ make install
   ```

   

----------------

#### Usage

We add an option "**-Wmisra-c**" to enable MISRAC checker. For example:

```
$ gcc -Wmisra-c test.c
```


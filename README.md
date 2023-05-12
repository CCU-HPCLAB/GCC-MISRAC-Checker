# GCC-MISRAC-Checker
#### A GCC-based MISRA-C checker for single-translation-unit-labeled rules.

By Chih-Yuan Chen, Yung-An Fang, Guan-Ren Wang, and Peng-Sheng Chen (High-Performance Computing laboratory, [Chung Cheng University](https://www.ccu.edu.tw/).)

----------------------------

#### Building GCC-MISRAC checker

1. Download GCC 7.5.0 source code: gcc-7.5.0.tar.xz

   

2. Download the directory misrac-gcc-changed-only

   

3. Uncompress gcc-7.5.0.tar.xz

   ```
   $ tar -Jxvf gcc-7.5.0.tar.xz
   ```

   

4. Copy misrac-gcc-changed-only/c-family/c.opt to gcc-7.5.0/gcc/c-family/

   ```
   $ cp c.opt ./gcc-7.5.0/gcc/c-family/
   ```

   

5. Build GCC

   ```
   $ mkdir build-misrac-gcc
   $ cd build-misrac-gcc
   $ ../gcc-7.5.0/configure --prefix=/usr/local/misrac --disable-multilib --disable-bootstrap --enable-languages=c -v
   $ make
   ```

   

6. Replace the original files with the modified files.

   ```
   $ cd ..
   $ cp -R ./misrac-gcc-changed-only/c-family ./gcc-7.5.0/gcc/
   $ cp -R ./misrac-gcc-changed-only/c ./gcc-7.5.0/gcc/
   $ cp -R ./misrac-gcc-changed-only/libcpp ./gcc-7.5.0/
   ```

   

7. Re-build GCC

   ```
   $ cd build-misrac-gcc
   $ make
   ```

   

8.  Install GCC-MISRAC checker

   ```
   $ make install
   ```

   

----------------

#### Usage

We add an option "**-Wmisra-c**" to enable MISRAC checker. For example:

```
$ gcc -Wmisra-c test.c
```


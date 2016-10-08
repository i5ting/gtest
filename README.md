# gtest

for https://github.com/google/googletest

## Install

- cmake
- make
- make install

```
➜  github ✗ git clone https://github.com/google/googletest.git
➜  github ✗ cd googletest/googletest
➜  googletest git:(master) ✗ mkdir recommand
➜  googletest git:(master) ✗ cd recommand 
➜  recommand git:(master) ✗ ls
➜  recommand git:(master) ✗ 
➜  recommand git:(master) ✗ cmake ../
-- The CXX compiler identification is AppleClang 7.0.2.7000181
-- The C compiler identification is AppleClang 7.0.2.7000181
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Found PythonInterp: /usr/bin/python (found version "2.7.10") 
-- Looking for include file pthread.h
-- Looking for include file pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - found
-- Found Threads: TRUE  
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/sang/workspace/github/googletest/googletest/recommand
➜  recommand git:(master) ✗ make
Scanning dependencies of target gtest
[ 50%] Building CXX object CMakeFiles/gtest.dir/src/gtest-all.cc.o
Linking CXX static library libgtest.a
[ 50%] Built target gtest
Scanning dependencies of target gtest_main
[100%] Building CXX object CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
Linking CXX static library libgtest_main.a
[100%] Built target gtest_main
➜  recommand git:(master) ✗ make install
[ 50%] Built target gtest
[100%] Built target gtest_main
Install the project...
-- Install configuration: ""
-- Installing: /usr/local/lib/libgtest.a
-- Installing: /usr/local/lib/libgtest_main.a
-- Installing: /usr/local/include/gtest
-- Up-to-date: /usr/local/include/gtest/gtest-death-test.h
-- Up-to-date: /usr/local/include/gtest/gtest-message.h
-- Up-to-date: /usr/local/include/gtest/gtest-param-test.h
-- Up-to-date: /usr/local/include/gtest/gtest-param-test.h.pump
-- Up-to-date: /usr/local/include/gtest/gtest-printers.h
-- Up-to-date: /usr/local/include/gtest/gtest-spi.h
-- Up-to-date: /usr/local/include/gtest/gtest-test-part.h
-- Up-to-date: /usr/local/include/gtest/gtest-typed-test.h
-- Up-to-date: /usr/local/include/gtest/gtest.h
-- Up-to-date: /usr/local/include/gtest/gtest_pred_impl.h
-- Up-to-date: /usr/local/include/gtest/gtest_prod.h
-- Installing: /usr/local/include/gtest/internal
-- Installing: /usr/local/include/gtest/internal/custom
-- Up-to-date: /usr/local/include/gtest/internal/custom/gtest-port.h
-- Up-to-date: /usr/local/include/gtest/internal/custom/gtest-printers.h
-- Up-to-date: /usr/local/include/gtest/internal/custom/gtest.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-death-test-internal.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-filepath.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-internal.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-linked_ptr.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-param-util-generated.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-param-util-generated.h.pump
-- Up-to-date: /usr/local/include/gtest/internal/gtest-param-util.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-port-arch.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-port.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-string.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-tuple.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-tuple.h.pump
-- Up-to-date: /usr/local/include/gtest/internal/gtest-type-util.h
-- Up-to-date: /usr/local/include/gtest/internal/gtest-type-util.h.pump
```

## Hello

hello.cc

```
  #include <stdio.h>

  #include "gtest/gtest.h"

  TEST(A, Zero) {
    EXPECT_EQ(1, 1);
  }

  GTEST_API_ int main(int argc, char **argv) {
    printf("Running main() from gtest_main.cc\n");
    testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
  }
```

compile

```
$ g++  -c hello.cc  
$ g++  hello.o /usr/local/lib/libgtest.a  -lpthread -o hello && ./hello
Running main() from gtest_main.cc
[==========] Running 1 test from 1 test case.
[----------] Global test environment set-up.
[----------] 1 test from A
[ RUN      ] A.Zero
[       OK ] A.Zero (0 ms)
[----------] 1 test from A (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test case ran. (0 ms total)
[  PASSED  ] 1 test.
```

## Sample1

- main.cc is main entry
- sample1_unittest is test
- sample1.h && sample1.cc is source

### compile main.cc

```
  #include <stdio.h>

  #include "gtest/gtest.h"

  GTEST_API_ int main(int argc, char **argv) {
    printf("Running main() from gtest_main.cc\n");
    testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
  }
```

run 

```
$ g++ -c main.cc -v
```

### compile source

sample1.h

```
  #ifndef GTEST_SAMPLES_SAMPLE1_H_
  #define GTEST_SAMPLES_SAMPLE1_H_

  // Returns n! (the factorial of n).  For negative n, n! is defined to be 1.
  int Factorial(int n);

  // Returns true iff n is a prime number.
  bool IsPrime(int n);

  #endif  // GTEST_SAMPLES_SAMPLE1_H_
```

sample.cc

```
  #include "sample1.h"

  // Returns n! (the factorial of n).  For negative n, n! is defined to be 1.
  int Factorial(int n) {
    int result = 1;
    for (int i = 1; i <= n; i++) {
      result *= i;
    }

    return result;
  }

  // Returns true iff n is a prime number.
  bool IsPrime(int n) {
    // Trivial case 1: small numbers
    if (n <= 1) return false;

    // Trivial case 2: even numbers
    if (n % 2 == 0) return n == 2;

    // Now, we have that n is odd and n >= 3.

    // Try to divide n by every odd number i, starting from 3
    for (int i = 3; ; i += 2) {
      // We only have to try i up to the squre root of n
      if (i > n/i) break;

      // Now, we have i <= n/i < n.
      // If n is divisible by i, n is not prime.
      if (n % i == 0) return false;
    }

    // n has no integer factor in the range (1, n), and thus is prime.
    return true;
  }
  
```

run

```
$ g++ -c sample1.cc -v
```

### compile test

sample1_unittest.cc

```
  #include <limits.h>
  #include "sample1.h"
  #include "gtest/gtest.h"

  // Tests factorial of negative numbers.
  TEST(FactorialTest, Negative) {
    // This test is named "Negative", and belongs to the "FactorialTest"
    // test case.
    EXPECT_EQ(1, Factorial(-5));
    EXPECT_EQ(1, Factorial(-1));
    EXPECT_GT(Factorial(-10), 0);

    // <TechnicalDetails>
    //
    // EXPECT_EQ(expected, actual) is the same as
    //
    //   EXPECT_TRUE((expected) == (actual))
    //
    // except that it will print both the expected value and the actual
    // value when the assertion fails.  This is very helpful for
    // debugging.  Therefore in this case EXPECT_EQ is preferred.
    //
    // On the other hand, EXPECT_TRUE accepts any Boolean expression,
    // and is thus more general.
    //
    // </TechnicalDetails>
  }

  // Tests factorial of 0.
  TEST(FactorialTest, Zero) {
    EXPECT_EQ(1, Factorial(0));
  }

  // Tests factorial of positive numbers.
  TEST(FactorialTest, Positive) {
    EXPECT_EQ(1, Factorial(1));
    EXPECT_EQ(2, Factorial(2));
    EXPECT_EQ(6, Factorial(3));
    EXPECT_EQ(40320, Factorial(8));
  }


  // Tests IsPrime()

  // Tests negative input.
  TEST(IsPrimeTest, Negative) {
    // This test belongs to the IsPrimeTest test case.

    EXPECT_FALSE(IsPrime(-1));
    EXPECT_FALSE(IsPrime(-2));
    EXPECT_FALSE(IsPrime(INT_MIN));
  }

  // Tests some trivial cases.
  TEST(IsPrimeTest, Trivial) {
    EXPECT_FALSE(IsPrime(0));
    EXPECT_FALSE(IsPrime(1));
    EXPECT_TRUE(IsPrime(2));
    EXPECT_TRUE(IsPrime(3));
  }

  // Tests positive input.
  TEST(IsPrimeTest, Positive) {
    EXPECT_FALSE(IsPrime(4));
    EXPECT_TRUE(IsPrime(5));
    EXPECT_FALSE(IsPrime(6));
    EXPECT_TRUE(IsPrime(23));
  }
  
```

run

```
$ g++ -c sample1_unittest.cc -v
```

run

```
$ g++ main.o sample1.o sample1_unittest.o /usr/local/lib/libgtest.a -lpthread -o sample1 && ./sample1
Running main() from gtest_main.cc
[==========] Running 6 tests from 2 test cases.
[----------] Global test environment set-up.
[----------] 3 tests from FactorialTest
[ RUN      ] FactorialTest.Negative
[       OK ] FactorialTest.Negative (0 ms)
[ RUN      ] FactorialTest.Zero
[       OK ] FactorialTest.Zero (0 ms)
[ RUN      ] FactorialTest.Positive
[       OK ] FactorialTest.Positive (0 ms)
[----------] 3 tests from FactorialTest (0 ms total)

[----------] 3 tests from IsPrimeTest
[ RUN      ] IsPrimeTest.Negative
[       OK ] IsPrimeTest.Negative (0 ms)
[ RUN      ] IsPrimeTest.Trivial
[       OK ] IsPrimeTest.Trivial (0 ms)
[ RUN      ] IsPrimeTest.Positive
[       OK ] IsPrimeTest.Positive (0 ms)
[----------] 3 tests from IsPrimeTest (0 ms total)

[----------] Global test environment tear-down
[==========] 6 tests from 2 test cases ran. (1 ms total)
[  PASSED  ] 6 tests.
```

## Recommend

change directory

```
$ cd recommend
```

compile source && test

```
$ g++ -c sample1.cc sample1_unittest.cc 
```

run test

```
$ g++ -I ./include/ sample1.o sample1_unittest.o libgtest.a libgtest_main.a -lpthread -o sample1 && ./sample1
Running main() from gtest_main.cc
[==========] Running 6 tests from 2 test cases.
[----------] Global test environment set-up.
[----------] 3 tests from FactorialTest
[ RUN      ] FactorialTest.Negative
[       OK ] FactorialTest.Negative (0 ms)
[ RUN      ] FactorialTest.Zero
[       OK ] FactorialTest.Zero (0 ms)
[ RUN      ] FactorialTest.Positive
[       OK ] FactorialTest.Positive (0 ms)
[----------] 3 tests from FactorialTest (1 ms total)

[----------] 3 tests from IsPrimeTest
[ RUN      ] IsPrimeTest.Negative
[       OK ] IsPrimeTest.Negative (0 ms)
[ RUN      ] IsPrimeTest.Trivial
[       OK ] IsPrimeTest.Trivial (0 ms)
[ RUN      ] IsPrimeTest.Positive
[       OK ] IsPrimeTest.Positive (0 ms)
[----------] 3 tests from IsPrimeTest (0 ms total)

[----------] Global test environment tear-down
[==========] 6 tests from 2 test cases ran. (1 ms total)
[  PASSED  ] 6 tests.
```

## Other

- https://github.com/google/googletest/blob/master/googletest/docs/Primer.md
- https://github.com/google/googletest/tree/master/googletest/docs
- https://github.com/google/googletest/tree/master/googletest/samples
- https://github.com/google/googletest/blob/master/googletest/docs/Primer.md#assertions

```
TEST(test_case_name, test_name) {
 ... test body ...
}

TEST_F(test_case_name, test_name) {
 ... test body ...
}
```

## Compile

include path

```
$ echo | g++ -v -x c++ -E -  
  Apple LLVM version 7.0.2 (clang-700.1.81)
  Target: x86_64-apple-darwin14.5.0
  Thread model: posix
   "/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/clang" -cc1 -triple x86_64-apple-macosx10.10.0 -Wdeprecated-objc-isa-usage -Werror=deprecated-objc-isa-usage -E -disable-free -disable-llvm-verifier -main-file-name - -mrelocation-model pic -pic-level 2 -mthread-model posix -mdisable-fp-elim -masm-verbose -munwind-tables -target-cpu core2 -target-linker-version 253.9 -v -dwarf-column-info -resource-dir /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/../lib/clang/7.0.2 -stdlib=libc++ -fdeprecated-macro -fdebug-compilation-dir /Users/sang/workspace/github/gtest -ferror-limit 19 -fmessage-length 181 -stack-protector 1 -mstackrealign -fblocks -fobjc-runtime=macosx-10.10.0 -fencode-extended-block-signature -fcxx-exceptions -fexceptions -fmax-type-align=16 -fdiagnostics-show-option -fcolor-diagnostics -o - -x c++ -
  clang -cc1 version 7.0.2 based upon LLVM 3.7.0svn default target x86_64-apple-darwin14.5.0
  ignoring nonexistent directory "/usr/include/c++/v1"
  #include "..." search starts here:
  #include <...> search starts here:
   /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/../include/c++/v1
   /usr/local/include
   /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin/../lib/clang/7.0.2/include
   /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/include
   /usr/include
   /System/Library/Frameworks (framework directory)
   /Library/Frameworks (framework directory)
  End of search list.
  # 1 "<stdin>"
  # 1 "<built-in>" 1
  # 1 "<built-in>" 3
  # 332 "<built-in>" 3
  # 1 "<command line>" 1
  # 1 "<built-in>" 2
  # 1 "<stdin>" 2
```

区分2点

1.在编译时，引入该库的头文件目录确保通过编译。比如在/usr/local/include：

    g++ -I/usr/local/include *.c -o a.o
  
2.在链接时，引入该库的二进制文件目录确保通过链接。比如你说的/usr/local/lib：
  
    gcc -L/usr/local/lib a.o -o a.out


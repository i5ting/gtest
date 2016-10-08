# gtest

for https://github.com/google/googletest

## hello

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

## sample1

- main.cc is main entry
- sample1_unittest is test
- sample1.h && sample1.cc is source

compile main

```
$ g++ -c main.cc -v
```

compile source

```
$ g++ -c sample1.cc -v
```

compile test

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

## recommend

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


## compile option

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

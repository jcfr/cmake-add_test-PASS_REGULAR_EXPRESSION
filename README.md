# CTest: PASS_REGULAR_EXPRESSION test property

This project aims to provide a basis for discussing the behavior of CTest associated with the `PASS_REGULAR_EXPRESSION` test property.

## Configuring the test case

Download, configure and run tests:


```
git clone https://github.com/jcfr/cmake-add_test-PASS_REGULAR_EXPRESSION

cmake -S cmake-add_test-PASS_REGULAR_EXPRESSION -B cmake-add_test-PASS_REGULAR_EXPRESSION-build

cmake --build cmake-add_test-PASS_REGULAR_EXPRESSION-build

ctest --test-dir cmake-add_test-PASS_REGULAR_EXPRESSION-build
```

Output:

```
ctest --test-dir cmake-add_test-PASS_REGULAR_EXPRESSION-build/
Internal ctest changing into directory: /tmp/cmake-add_test-PASS_REGULAR_EXPRESSION-build
Test project /tmp/cmake-add_test-PASS_REGULAR_EXPRESSION-build
    Start 1: ExpectedPass
1/4 Test #1: ExpectedPass .....................   Passed    0.02 sec
    Start 2: ExpectedFail
2/4 Test #2: ExpectedFail .....................***Failed    0.01 sec
    Start 3: RegexCheckExpectedPass
3/4 Test #3: RegexCheckExpectedPass ...........   Passed    0.01 sec
    Start 4: RegexCheckExpectedFail
4/4 Test #4: RegexCheckExpectedFail ...........   Passed    0.01 sec

75% tests passed, 1 tests failed out of 4

Total Test time (real) =   0.06 sec

The following tests FAILED:
    2 - ExpectedFail (Failed)
Errors while running CTest
Output from these tests are in: /tmp/cmake-add_test-PASS_REGULAR_EXPRESSION-build/Testing/Temporary/LastTest.log
Use "--rerun-failed --output-on-failure" to re-run the failed cases verbosely.
```

## Expected behavior

Test `RegexCheckExpectedFail` should be failing since a exception is raised and the exit code is different from zero.

## Observations

While writing this test case and reviewing the CMake documentation, the following differences in the description associated with the `PASS_REGULAR_EXPRESSION` property were observed:

| CMake version | `PASS_REGULAR_EXPRESSION` description |
|--|--|
| <= 3.20.6 | The output must match this regular expression for the test to pass. |
| >= 3.21 | The output must match this regular expression for the test to pass. The process exit code is ignored. |

The documentation updates was introduced in [cmake@91b8676f8](https://github.com/Kitware/CMake/commit/91b8676f8):

```
Help: Clarify {PASS,FAIL}_REGULAR_EXPRESSION semantics w.r.t. exit code

Also cross-reference them with each other and `SKIP_REGULAR_EXPRESSION`.
```

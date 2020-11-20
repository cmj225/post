---
description: C/C++ unit test framework
---

# Googletest

## Googletest

* c++ unit test framework
*  [googletest primer](https://github.com/google/googletest/blob/master/googletest/docs/primer.md)

## Basic Equation

* basic test equation

  > `ASSERT : !condition -> stop` `EXPECT : !condition -> keep going`
  >
  > `*_TRUE : is true ?` `*_FALSE : is false ?`
  >
  > `*_EQ : ==` `*_NE : !=` `*_LT : <` `*_LE : <=` `*_GT : >` `*_GE : >=` `*_STREQ : ==` `*_STRNE : !=` `*_STRCASEEQ : == && ignoring case` `*_STRCASENE : != && ignoring case`

* Basic Assertion

  > `ASSERT_TRUE(condition);` `ASSERT_FALSE(condition);` `EXPECT_TRUE(condition);` `EXPECT_FALSE(condition);`

* Binary Comparison

  > `ASSERT_EQ(val1, val2);` `ASSERT_NE(val1, val2);` `ASSERT_LT(val1, val2);` `ASSERT_LE(val1, val2);` `ASSERT_GT(val1, val2);` `ASSERT_GE(val1, val2);`
  >
  > `EXPECT_EQ(val1, val2);` `EXPECT_NE(val1, val2);` `EXPECT_LT(val1, val2);` `EXPECT_LE(val1, val2);` `EXPECT_GT(val1, val2);` `EXPECT_GE(val1, val2);`

* String Comparison

  > `ASSERT_STREQ(str1, str2);` `ASSERT_STRNE(str1, str2);` `ASSERT_STRCASEEQ(str1, str2);` `ASSERT_STRCASENE(str1, str2);`

## Test Examples

### Test Class

```cpp
/* Foo.h */
#include <string>

// some test class
class Foo {
  public:
    Foo(std::string name = "Foo") : m_name(name) {}

  public:
    bool isTrue(bool input) {
      return input;
    }

    int sum(int a, int b) {
      return a + b;
    }
}
```

### Simple Tests

```cpp
// simple test
/*
TEST(TestSuiteName, TestName) {
  ... test body ...
};
*/

TEST(FooTest, isTrue) {
  // EXPECT의 경우 기대값과 달라도 Test를 계속 진
  EXPECT_TRUE(isTrue(true));
  EXPECT_FALSE(isTrue(false));
  
  // ASSERT의 경우 기대값과 다르면 Test 자체를 멈춤
  ASSERT_TRUE(isTrue(true));
  ASSERT_FALSE(isFalse(false));
  
  // ... //
  EXPECT_EQ(2, sum(1,1));
  EXPECT_NE(3, sum(1,1));
}
```

### Fixture Tests

```cpp
// Test Fixtures
// Using Same Data Configuration for Multiple Tests {#same-data-multiple-tests}
// 1. googletest constructs a TestFixtureName object (let's call it t1)
// 2. t1.Setup()
// 3. n'th TestName's ... test body ...
// 4. t1.TearDown()
// 5. t1 is distructed
// 6. above steps are repeated on another TestFixtureName object 
class Fixture : public ::testing::Test {
 protected:
  void Setup() override ;
  void TearDown() override;
};

TEST_F(Fixture, TestName) {
  // ... test body ... //
};

```

### Invoking the Tests

* 일반적으로 TEST\(\), TEST\_F\(\)는 googletest에 자동으로 등록 됨
* **`gtest_main`**를 링크하면 **`gtest_main()`**을 entry point로 하여, gtest\_main\(\)에서 **`RUN_ALL_TEST()`**가 불릴 때, 등록된 테스트를 자동으로 실행시켜 줌
* 하지만 별도의
*  main\(\)이 필요한 경우, main\(\)을 만들고 사용할 수 있

### main\(\) custom 

```cpp
/* Google test using Fixture and custom main */
#include "gtest/gtest.h"
#include "Foo.h"

int g_argc;
char** g_argv;

// testing environments
class Fixture : public ::testing::Test {
  protected:
    Fixture() {
      // You can do set-up work for each test hear.
    }
    ~Fixture() {
      // You can do clean-up work that doesn't throw exception here.
    }
    
    // If ctor & dtor are not enough for setting up and cleaning up each test,
    // you can define following methods
    void SetUp() override {
      // Code here will be called immediately after the constructor
      // right befor each test
    }
    void TearDown() override {
      // Code here will be called immediately after each test
      // right after the dtor
    }
}

int main(int argc, char **argv) {
  // remove googletest flags from input args.
  ::testing::InitGoogleTest(&argc, argv);
  
  // check remain input args
  for(int i = 1; i < argc; ++i) {
    print("%d's arg : %s\s", i, argv[i]); 
  } 
  
  // if need argc, argv
  g_argc = argc;
  g_argv = argv;
  
  return RUN_ALL_TESTS();
}
```



## Googletest Flags

* `example --help` 로 지원하는 flag 확인 가능하며, 아래에 쓸만한 flags 정리
* Test Selection
  * `--gtest_list_tests`
  * `--gtest_filter=POSITIVE_PARTTERN[-NEGATIVE_PARTTERNS]`
* Test Execution
  * `--gtest_repeat=[COUNT]`
* Test Output
  * `--gtest_brief=1`  &lt;&lt; only print test failure
  * `--gtest_output=(json|xml)[:DIRECTORY_PATH/|:FILE_PATH]`
  * _`--gtest_stream_result_to=HOST:PORT`_
* Assertion Behavior
  * `--gtest_break_on_failure`

## Googletest with BDD

* BDD pattern을 지원하는 오픈소스가 있음
  * [https://github.com/michaelvlach/cppbdd](https://github.com/michaelvlach/cppbdd)
  * 위 프로젝트에서 gtestbdd.h를 포함하여 프로젝트에서 사용하려 하였지만 동작하지 않음
  * 참고하여 Googletest에서 BDD를 사용할 수 있도록 만듬
    * [https://github.com/cmj225/cppbdd](https://github.com/cmj225/cppbdd)
* 아래와 같이 `Fixture` 에 `BDDUtil` 을 상속시켜 사용하면 됨

```cpp
class FixtureBDD : public ::testing::Test,
                   public cppbdd::BDDUtil {
};

TEST_F(FixtureBDD, bddTest) {
  // ... test body ...
  
  // specify feature
  FEATURE("Feature ... ")
  
  // specify scenario
  SCENARIO("Scenario ... ")
  
  // give some value for setting
  GIVEN("Given ... ")
  // ... give something ...
  
  // make testing state
  WHEN("When ... ")
  
  // check result
  THEN("Then ... ")
}
```


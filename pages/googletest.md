- googletest使用  #CPP #CPP/cmake #googletest
	- 可以参考[googletest primer](https://google.github.io/googletest/primer.html)
	- 使用时包含gtest的头文件和库文件：
	  collapsed:: true
		- ```cmake
		  include_directories(/home/luyimin/My_STL/include/stl)
		  include_directories(/home/luyimin/My_STL/include/googletest)
		  add_executable(${PROJECT_NAME} src/vector_test_alloc.cc)
		  
		  # 链接库文件
		  target_link_libraries(${PROJECT_NAME} PUBLIC 
		  /home/luyimin/My_STL/thirdparty/gtest/libgtest.a
		  /home/luyimin/My_STL/thirdparty/gtest/libgtest_main.a # 使用gtest自带的main函数
		  )
		  
		  ```
	- 如果不适用gtest自带的main函数，就将main函数写为：
	  collapsed:: true
		- ```CPP
		  int main(int argc, char** argv) {
		    testing::InitGoogleTest(&argc, argv);
		    return RUN_ALL_TESTS();
		  }
		  ```
	- 然后就可以写测试宏函数，快乐的断言单元测试了。如：
	  collapsed:: true
		- ```cpp
		  TEST(vec_test_double, push_back) {
		    MY_STL::vector<double, MY_STL::simple_alloc<double, MY_STL::alloc>> vec;
		    vec.push_back(10);
		    ASSERT_EQ(vec.size(), 1);
		    ASSERT_EQ(vec.capacity(), 1);
		  }
		  
		  TEST(vec_test_int, push_back) {
		    MY_STL::vector<int, MY_STL::simple_alloc<int, MY_STL::alloc>> vec;
		    vec.push_back(2);
		    ASSERT_EQ(vec.size(), 1);
		    ASSERT_EQ(vec.capacity(), 1);
		  }
		  
		  TEST(vec_test_int, resize) {
		    MY_STL::vector<int> vec;
		    vec.resize(10);
		    ASSERT_EQ(vec.size(), 10);
		    // ASSERT_EQ(vec.capacity(), 1);
		  }
		  ```
	- `ASSERT_*`是触发后就会终止程序。`EXPECT_*`是期望，触发后不会终止程序
	- gmock是继承下函数的单元测试，详细可以百度
	- `TEST`宏和`TEST_F`宏的区别。合适的选用宏
		- `TEST`宏是单独创建测试用例，各个测试用例之间不会共享状态和资源。
		- `TEST_F`宏，需要在创建一个测试类之后再调用，这会创建一个测试套件，测试套件内共享状态和资源。
		  collapsed:: true
			- ```cpp
			  class Vec_Test: public ::testing::Test {
			  public:
			    // 以下两种命名都可以。在初始化全局环境时调用
			    // static void TearDownTestSuite() {
			    static void TearDownTestCase() {
			      cout << "tear down test suite\n" << std::endl;
			    }
			    // 在退出全局环境时调用
			    // static void SetUpTestSuite() {
			    static void SetUpTestCase() {
			      cout << "set up test suite\n" << std::endl;
			    }
			    
			    // 在调用套件中的每一个测试用例时调用
			    virtual void SetUp() override {
			      cout << "set up\n" << std::endl;
			    }
			    virtual void TearDown()override {
			      cout << "tear down\n" << std::endl;
			    }
			  };
			  //     测试套件名
			  TEST_F(Vec_Test, push_back) {
			    MY_STL::vector<int, MY_STL::simple_alloc<int, MY_STL::alloc>> vec;
			    vec.push_back(12);
			    ASSERT_EQ(vec.size(), 1);
			  }
			  
			  
			  [==========] Running 1 test from 1 test suite.
			  [----------] Global test environment set-up.
			  [----------] 1 test from Vec_Test
			  set up test suite
			  
			  [ RUN      ] Vec_Test.push_back
			  set up
			  
			  tear down
			  
			  [       OK ] Vec_Test.push_back (0 ms)
			  tear down test suite
			  
			  [----------] 1 test from Vec_Test (0 ms total)
			  
			  [----------] Global test environment tear-down
			  [==========] 1 test from 1 test suite ran. (0 ms total)
			  [  PASSED  ] 1 test.
			  ```
-
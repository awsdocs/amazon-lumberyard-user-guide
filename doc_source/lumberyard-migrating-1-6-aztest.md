# Migrating from CryUnitTest to AzTest<a name="lumberyard-migrating-1-6-aztest"></a>

In Lumberyard 1\.6, the CryUnitTest framework for writing tests is no longer available\. The AzTest framework, which is built on top of GoogleTest and GoogleMock, replaces CryUnitTest\. If you have tests written in CryUnitTest, follow these steps to use the AzTest framework for your tests\.

To migrate from CryUnitTest to AzTest, you must:
+ A\. Modify tests to use GoogleTest macros
+ B\. Move tests into test build files
+ C\. Build and run tests

## A\. Modifying Tests to Use GoogleTest Macros<a name="aztest-modify-tests-googletest-macros"></a>

Simply convert the CryUnitTest tests to GoogleTest tests by replacing the following macros\. You must also replace `CryUnitTest.h` with `AzTest/AzTest.h` in your `.cpp` files to get the new macros\.


****  

| CryUnitTest | GoogleTest | 
| --- | --- | 
| CRY\_UNIT\_TEST\_SUITE\(SuiteName\) | No replacement\. You can safely remove these from your code\. | 
| CRY\_UNIT\_TEST\(TestName\) | TEST\(SuiteName, TestName\) | 
| CRY\_UNIT\_TEST\_FIXTURE\(FixtureName\) | class FixtureName : public ::testing::Test | 
| CRY\_UNIT\_TEST\_WITH\_FIXTURE\(TestName, FixtureName\) | TEST\_F\(FixtureName, TestName\) | 
| CRY\_UNIT\_TEST\_ASSERT\(Condition\) | ASSERT\_TRUE\(condition\) | 
| CRY\_UNIT\_TEST\_CHECK\_CLOSE\(ValueA, ValueB, Epsilon\) | ASSERT\_NEAR\(ValueA, ValueB, Epsilon\) | 
| CRY\_UNIT\_TEST\_CHECK\_EQUAL\(ValueA, ValueB\) | ASSERT\_EQ\(ValueA, ValueB\) | 
| CRY\_UNIT\_TEST\_CHECK\_DIFFERENT\(ValueA, ValueB\) | ASSERT\_NE\(ValueA, ValueB\) | 

## B\. Moving Tests into Test Build Files<a name="aztest-move-tests-test-build-files"></a>

AzTest and GoogleTest are not included in normal builds, they are only included in test builds\. Tests must be configured to only build in test builds\. For more information about creating test builds and running tests, see [Using AZ Test Scanner](testing-aztestscanner.md)\.

If your CryUnitTest tests are interspersed with regular engine code, you must move those tests into a separate `.cpp` file\. You can then add the `.cpp` files to a test\-specific `.waf_files` file\. All modules and gems that are shipped with Lumberyard have a `*_test.waf_files` file\. You can add new test files to these `*_test.waf_files` files\. If your module or gem does not have a `*_test.waf_files` file, you can create one and reference it in the module's wscript file\.

## C\. Building and Running Tests<a name="aztest-build-run-tests"></a>

After you complete these migration steps, you can build and run your new tests\. For more information, see [Using AZ Test Scanner](testing-aztestscanner.md)\.

If you encounter issues where your tests no longer work properly, your tests may be relying on in\-engine code to pass\. If this occurs, you must specify that your tests are integration tests by using the `INTEG_TEST` macro instead of `TEST`\.
This tutorial is meant for understanding and standardize writing test cases

## OBJECTIVES
1. To automate the testing procedure
1. To identify areas of testing
1. To standardize way of identifying and writing the test cases
1. To simplify the writing test cases

### MEANS TO ACHIEVE
1. Automated Testing
  1. Develop a framework that fetches all the tests,runs and presents results
  1. Framework which ensures clearing of all tests before the code reaches the customers
1. Identify Areas of testing
  1. Functionality Testing
  1. Boundary conditions testing
  1. Performance testing
1. Identifying Tests
   A system which is designed based of given set of requirements, needs just one set of test cases.
   But given two people the same task of writing test cases for a given system, they may not end up with same test cases. This is just an attempt to achieve the one unique set of test cases by any one.
   Eg: Attempting a simple scenario of "creating an ITEM"
   1. Mandatory Fields
      1. Independently Mandatory
         "Code", "Description"
      1. Dependent Mandatory
         "Warehouse" and "Stock UOM" Depends on "Is Stock Item"
   1. 
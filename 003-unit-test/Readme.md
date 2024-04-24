Link: https://www.johansmarius.dev/2023/07/writing-unit-tests-with-github-copilot.html; repo: https://github.com/JohanSmarius/DemoUnitTestingGithubCopilotChat/tree/main
Title: Writing unit tests with GitHub Copilot
**Add logic**
This code does not have a lot of logic to test. So let's add some logic to the order class. I ask GitHub Copilot to generate the code for calculating the total price for an order.

**First tests**
I can now ask Copilot to generate a unit test for this code using the prompt: "Can you generate a xunit test for the order and orderlineitem class where the order has 2 orderlineitems".
Three unit tests were generated upon this request. One for TotalPrice and two for AddOrderLineItem.

Copilot did generate the code but did not take our own OrderLineItem into account. Our own class does not have a constructor and also does not contain something that looks like an id. Furthermore, if I calculate the total order price for the generated test I get 80 and not 70. In order to get this generated code working I do have to change the code. I do like the usage of the Arrange, Act, Assert pattern in the generated code. This pattern is widely used in all kinds of frameworks. If you are not familiar with the pattern I will give you a short summary. In the arrange section everything needed in the unit test is set up. The actual call to the code is done in the act section. The checks, if everything was executed correctly, are done in de assert section.  Let's fix the generated code.

**Fix generated code**
In unit tests, I usually use factory methods to generate the class to test (or subject under test, sut). 
I asked Copilot to generate a factory method for me, but at the first attempt it generated a separate factory class and the code did not take our own OrderLineItem definition into account. I updated the code to match our code and moved the generated code back into the unit test class. This code generates a precalculated price and quantity. I could have used random numbers in this code, but then it would be impossible for me to check the calculated TotalPrice. I like my unit tests to be as specific as possible to gain the most prediction from them, so I choose the fixed price option.
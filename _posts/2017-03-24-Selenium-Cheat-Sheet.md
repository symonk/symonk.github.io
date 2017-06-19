---
layout: post
title: Selenium Cheat Sheet TBC
bigimg: /img/path.jpg
published: true
---
A brief outlook at selenium, what we can do with it, how we can do those things.  Super handy for upcoming job interviews or just getting a quick refresher!

Wait.......Wait................So, Waits then?
**Implicit Waits:** Implicit waiting in selenium is when we set a particular timer in which we will look for elements, the implicit wait will live with the life of our driver, in order to set the implicit wait:

```
 driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
```

**Explitic Waits:** Explicit waits are typically when we tell the driver to wait for something, usually coupled with the likes of an ExpectedConditions statement, to implement an explicit wait we create a new WebDriverWait object, called wait in this instance, then we will the tell the driver to wait until something is true:

```
WebDriverWait wait = new WebDriverWait(driver, 10);

WebElement element = wait.until(ExpectedConditions.elementToBeClickable(By.id("someid")));
```

In the above instance, we are waiting until an element with the id "someid" is clickable before we continue execution, but there are more things we can wait for, some of these are:

- visibilityOfElement();
- alertIsPresent();
- attributeToBe();
- elementToBeClickable();
- presenceOfElementLocated();

and many, many more.  to see more of the expectedConditions, check them out via the selenium API online which can be found here:  https://seleniumhq.github.io/selenium/docs/api/java/org/openqa/selenium/support/ui/ExpectedConditions.html

**Fluent Waits:** Fluent waits are similar to Explicit waits however there is more control to the user, you can tell the wait how often to poll, how long to wait total and any exceptions that could occur that you want to essentially ignore.  In order to implement a Fluent wait, we will instantiate a new fluentwait, outlined below: (Check every 5 seconds, for 30 seconds and ignore ElementNotFoundExceptions

```
Wait abc = new FluentWait(driver)
				.withTimeout(30, TimeUnit.SECONDS)
				.pollingEvery(5, TimeUnit.SECONDS)
				.ignoring(ElementNotFoundException.class);
```

Driver implementations, for the purpose of this piece we will be outlining how to implement your driver for chrome, there is a wide range of supported browsers so you will have to research those yourself, however it is very similar:

We need to instantiate an instance of chrome driver:

```
System.setProperty("webdriver.chrome.driver", "C:/Automation/chromedriver.exe");
ChromeOptions options = new ChromeOptions();
options.addArguments("--start-maximized");
WebDriver driver = new ChromeDriver();
```

What can we then do with our driver? here are some of the key methods we can utilise with selenium chromedriver:

```
Clear out a textbox
driver.findElement(By.id("id")).clear();
```

``` 
Get the text of a webelement
driver.findElement(By.id("id")).getText();

```

```
Send text/keys to the webelement
driver.findElement(By.id("id")).sendKeys("Hello!");

```

``` 
Get attribute of webelement
driver.findElement(By.id("id")).getAttribute("value");

```

``` 
Get attribute of webelement
driver.findElement(By.id("id")).getAttribute("value");

```

``` 
Click a webelement
driver.findElement(By.id("id")).click();

```

``` 
Check an element is enabled or not (true/false boolean)
driver.findElement(By.id("id")).isEnabled();

```

``` 
**Check an element is displayed or not (true/false boolean)**
driver.findElement(By.id("id")).isDisplayed();

```

```
Check an element is selected or not (true/false boolean)
driver.findElement(By.id("id")).isSelected();

```

``` 
Get current page title
driver.getTitle();

```

``` 
Get the value attribue of a webelement (e.g - current text in the textbox)
driver.findElement(By.id("id")).getValue();

```

Navigating using your driver:
``` 
Go to a particular website
driver.navigate().to("http://www.google.com");

```

``` 
Go to a particular website
driver.get("http://www.google.com");

```

``` 
Refresh the page
driver.navigate().refresh();

```

``` 
Go Back a page
driver.navigate().back();

```

``` 
Go Forward a page
driver.navigate().forward();

```

------------------------------------------------------------
**Locating Elements**

Selenium offers an array of methods to locate webelements on the page, best coupled with PageObjectModel to create objects of your pages for easy reuse and more stable/less brittle testing.  The main locators are outlined below:

- **XPATH** - Traversing through the entire document, very powerful but pretty slow, always opt for ID before this if available.

```
This locates the second input element beneath the element with an id value of ‘register’

driver.findElement(By.xpath(“//input[@id=’myElementId’]”));

```

- **CSS** - Finding an element based on the css class attribute, faster than Xpath but still use ID if you have it available to you.

```
driver.findElement(By.cssSelector(“h1[title]”);

```

- **ID** - Finding an element by its ID attribute - blazing fast and always best to use if applicable

```
driver.findElement(By.id("abc")).click();

```

- **Name** - Similar to ID, we are finding by the name attribute

```
driver.findElement(By.name("abc"));
```

-  **Linktext** - Partial Linktext is also available, essentially the text on the element, avoid if you can, there could be multiple things with the same value on the page and this will use the first one.

```
driver.findElement(By.linkText(“Click Me!”));
driver.findElement(By.partialLinkText("Click M"));

```

-  **Tagname** - Uses the tag attribue to find an element, not really recommended outside of getting the page header/title

```
driver.findElement(By.tagName("h1"));

```

- **Classname** - Finding an element by the class name attribute

```
driver.findElement(By.classname("date-header"));

```

--------------------------------------------------------------------------------
**Selenium Exceptions**

Selenium has a number of different exceptions associated with it,

```
ElementNotVisibleException -> Element is present in the DOM (Document Object Model) but it is not visible, thus we are not able to interact with it.

NoSuchAttributeException -> Looking for an attribue that does not exist on an element, for example By.id("abc").getAttribute("wrong");

NoSuchElementException -> Element simply cannot be found, Fluent/Implicit/explicit wait has expired

NoSuchFrameException -> Switching to a frame which does not exist
NoSuchWindowException -> Switch to a window which does not exist

StaleElementReferenceException -> When the DOM has been updated after you have a reference to a webelement causing it to go stale, calling methods on your now stale element will throw this.

```

---------------------------------------------------------------------------------------
**Interacting with Frames/Windows**

In selenium sometimes we need to change our focus to another window, in order to do that we need to get our current window handle, perhaps get all available windows handles and make the switch, remembering to switch back after:

```	
String current = driver.getWindowHandle(); //Return a string of alphanumeric window handle

Set<String> Handles = driver.getWindowHandles(); //Return a set of window handle

driver.switchTo().window("windowName");
driver.switchTo().window(current);

```

In order to switch to a different frame/alert, we use this simply syntax:

```
Alert alert = driver.switchTo().alert();

Alert alert = driver.switchTo().alert();
alert.dismiss();
alert.accept();
alert.getText();

```

















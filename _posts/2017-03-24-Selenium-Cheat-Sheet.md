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




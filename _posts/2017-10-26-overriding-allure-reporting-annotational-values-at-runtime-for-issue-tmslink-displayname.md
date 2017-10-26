---
layout: post
published: true
title: >-
  Overriding Allure Reporting annotational values at runtime for @Issue,
  @TmsLink, @DisplayName
---
## Setting issueIds, TmsLinkIds and DisplayNames dynamically when passing a junit dataprovider to the @TestMethod.

**Note:** This piece is for the following stack - Allure Junit Adapter with a maven report generator.

A common problem I faced was the issues, testcase links and display names could be set statically at the method level no problem:

```java
@Issue("foo")
public void fooTest() {

} 
```

But what happens if we need to use a dataprovider which includes an IssueId or testCaseID for each test? Here is a quick helping hand to overcome the problem.
**Note**: This is very hacky and hopefully the framework will build this functionality in soon.

```java
 @DataProvider
  public static Object[][] saveCourseData() {
    return new Object[][] {
              { critical, "IssueId01", "19793", "A new course can be successfully added", 0, "Course01", "CourseDesc01", 0, 1, false, true, 200, validSave},     
    };
  }
```

As you can see I have a severity, IssueId, TestcasId as well as some random other test data but we only care about the first 3 rows as its the allure-specific data.  

**Step 1:**

Prepare your test declaration, it MUST contain blank annotations for those values else you will get an exception. e.g:

```java
@Test
    @Step
    @UseDataProvider("saveCourseData")
    @DisplayName("")
    @Issue("")
    @TmsLink("")
    public void savecourse_scenarios_return_appropriate_responses(SeverityLevel severityLevel, String issueId, String testCaseId, String displayName, int courseId, String courseName, String courseDescription, int thumbnailFileId, int locationId, boolean isDeleted, boolean expectedToSave, int statusCode, String expectedMessage) throws NoSuchMethodException, SecurityException, InterruptedException {
```

**Step 2:**

Get the method aka the test method, you will need to pass in each paramater types .class which is a bit of manual effort.

```java
Method m = SaveCourse.class.getDeclaredMethod("savecourse_scenarios_return_appropriate_responses", SeverityLevel.class,String.class, String.class, String.class, int.class, String.class, String.class, int.class, int.class, boolean.class, boolean.class, int.class, String.class);
```

**Step 3 - OPTIONAL:**

Leave any readers an inkling if there is no case or issue regarding the test case with the following:
```java
        if (issueId.equals("")) {
        	issueId = "No known issues";
        }
        
        if (testCaseId.equals("")) {
        	issueId = "No known testcases";
        }
```

**Step 4:**

Note: You must create a class for each Issue, DisplayName, TmsLink which implements the interface respectively:

```java
import java.lang.annotation.Annotation;

import io.qameta.allure.Issue;
public class DynamicIssue implements Issue {

	private String value;
	
	public DynamicIssue(String value) {
		this.value = value;
	}
	
	@Override
	public Class<? extends Annotation> annotationType() {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public String value() {
		return value;
	}
```

Overriding the values on each iteration at runtime!  (**Put this in your @Test method**)
```java
        Issue i = m.getAnnotation(Issue.class);
        DynamicIssue di = new DynamicIssue(issueId);
        tester.changeAnnotationValue(i, "value", di.value());
        
        DisplayName dn = m.getAnnotation(DisplayName.class);
        DynamicIssue ddn = new DynamicIssue(displayName);
        tester.changeAnnotationValue(dn, "value", ddn.value());
        
        TmsLink tl = m.getAnnotation(TmsLink.class);
        DynamicIssue dtl = new DynamicIssue(testCaseId);
        tester.changeAnnotationValue(tl, "value", dtl.value());
```

and last but not least, our helper method to aid us in overriding these values:

```java
import java.lang.annotation.Annotation;
import java.lang.reflect.Field;
import java.lang.reflect.Proxy;
import java.util.Map;

public class tester {
	
	@SuppressWarnings("unchecked")
	public static Object changeAnnotationValue(Annotation annotation, String key, Object newValue){
	    Object handler = Proxy.getInvocationHandler(annotation);
	    Field f;
	    try {
	        f = handler.getClass().getDeclaredField("memberValues");
	    } catch (NoSuchFieldException | SecurityException e) {
	        throw new IllegalStateException(e);
	    }
	    f.setAccessible(true);
	    Map<String, Object> memberValues;
	    try {
	        memberValues = (Map<String, Object>) f.get(handler);
	    } catch (IllegalArgumentException | IllegalAccessException e) {
	        throw new IllegalStateException(e);
	    }
	    Object oldValue = memberValues.get(key);
	    if (oldValue == null || oldValue.getClass() != newValue.getClass()) {
	        throw new IllegalArgumentException();
	    }
	    memberValues.put(key,newValue);
	    return oldValue;
	}
	
}
```

If you encounter a similar problem, you can give me a message @ https://testersio.slack.com/messages (Register with the channel and message me @simonkay for any queries regarding this.  I also took some inspiration/samples from `baeldung`

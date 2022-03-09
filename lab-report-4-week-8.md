# **Lab Report 4**
### **Markdown Testing**

### Links:
[My Markdown Parse Repository](https://github.com/atorshizi/markdown-parse)

[Reviewed Markdown Parse Repository](https://github.com/clingunis/markdown-parse)

### Snippet 1:
Based on VScode's markdown viewer, I expect this test file should have the following three links: 
``` 
`google.com
google.com
ucsd.edu
```
![img-should](pics4/snip1-should.png)

I made two JUnit tests for this file (one for our implementation and one for the group we reviewed). The testing methods are as follows.

``` java
@Test
public void TestOurSnippit1() throws IOException{
    Path fileName = Path.of(PATH + "snip1.md");
    String contents = Files.readString(fileName);
    ArrayList<String> expected = new ArrayList<>();
    expected.add("`google.com");
    expected.add("google.com");
    expected.add("ucsd.edu");
    ArrayList<String> actual = MarkdownParse.getLinks(contents);
    assertEquals(expected, actual);
}

@Test
public void TestReviewedSnippit1() throws IOException{
    Path fileName = Path.of(PATH + "snip1.md");
    String contents = Files.readString(fileName);
    ArrayList<String> expected = new ArrayList<>();
    expected.add("`google.com");
    expected.add("google.com");
    expected.add("ucsd.edu");
    ArrayList<String> actual = MarkdownParseReviewed.getLinks(contents);
    assertEquals(expected, actual);
}
```
For our implementation, the JUnit test failed and this resulting output.
![img-should](pics4/snip1-results.png)

For the group that we reviewed, the JUnit test also failed with the following resulting output.
![img-should](pics4/snip1-resultsR.png)



### Snippet 2:
Based on VScode's markdown viewer, I expect this test file should have the following three links: 
``` 
a.com
a.com(())
example.edu
```
![img-should](pics4/snip2-should.png)

I made two JUnit tests for this file (one for our implementation and one for the group we reviewed). The testing methods are as follows.

``` java
@Test
public void TestOurSnippit2() throws IOException{
    Path fileName = Path.of(PATH + "snip2.md");
    String contents = Files.readString(fileName);
    ArrayList<String> expected = new ArrayList<>();
    expected.add("a.com");
    expected.add("a.com(())");
    expected.add("example.com");
    ArrayList<String> actual = MarkdownParse.getLinks(contents);
    assertEquals(expected, actual);
}

@Test
public void TestReviewedSnippit2() throws IOException{
    Path fileName = Path.of(PATH + "snip2.md");
    String contents = Files.readString(fileName);
    ArrayList<String> expected = new ArrayList<>();
    expected.add("a.com");
    expected.add("a.com(())");
    expected.add("example.com");
    ArrayList<String> actual = MarkdownParseReviewed.getLinks(contents);
    assertEquals(expected, actual);
}
```
For our implementation, the JUnit test failed and this resulting output.
![img-should](pics4/snip2-results.png)

For the group that we reviewed, the JUnit test also failed with the following resulting output.
![img-should](pics4/snip2-resultsR.png)



### Snippet 3:
Based on VScode's markdown viewer, I expect this test file should have the following three links: 
``` 
https://www.twitter.com
https://ucsd-cse15l-w22.github.io/
https://cse.ucsd.edu/
```
![img-should](pics4/snip3-should.png)

I made two JUnit tests for this file (one for our implementation and one for the group we reviewed). The testing methods are as follows.

``` java
@Test
public void TestOurSnippit3() throws IOException{
    Path fileName = Path.of(PATH + "snip3.md");
    String contents = Files.readString(fileName);
    ArrayList<String> expected = new ArrayList<>();
    expected.add("https://www.twitter.com");
    expected.add("https://ucsd-cse15l-w22.github.io/");
    expected.add("https://cse.ucsd.edu/");
    ArrayList<String> actual = MarkdownParse.getLinks(contents);
    assertEquals(expected, actual);
}

@Test
public void TestReviewedSnippit3() throws IOException{
    Path fileName = Path.of(PATH + "snip3.md");
    String contents = Files.readString(fileName);
    ArrayList<String> expected = new ArrayList<>();
    expected.add("https://www.twitter.com");
    expected.add("https://ucsd-cse15l-w22.github.io/");
    expected.add("https://cse.ucsd.edu/");
    ArrayList<String> actual = MarkdownParseReviewed.getLinks(contents);
    assertEquals(expected, actual);
}
```
For our implementation, the JUnit test failed and this resulting output.
![img-should](pics4/snip3-results.png)

For the group that we reviewed, the JUnit test also failed with the following resulting output.
![img-should](pics4/snip3-resultsR.png)



### Questions:
- **Do you think there is a small (<10 lines) code change that will make your program work for snippet 1 and all related cases that use inline code with backticks?**
- *I think the solution to fix the code so that it works for all inline code with backticks would be rather involved and take a long time to implement. This is because the parser would have to check to see if there are open backticks before each potential link and ignore the link if it is part of a code block in markdown; this would require the program to be able to find each backtick and the corresponding backtick that ends the code block and then determine if a potential link if part an unclosed block. Since the code would have to keep track of all opening and closing backtick in the file, this would likely require a separate helper method to determine if a link is part of a block which is definitely a more involved fix.*

- **Do you think there is a small (<10 lines) code change that will make your program work for snippet 2 and all related cases that nest parentheses, brackets, and escaped brackets?**
- *I think this could be fixed by using a stack and pushing in an open bracket/parenthesis while parsing the file and popping the stack once a closed bracket/parenthesis is encountered. This would allow us to find the matching pairs of open and closed brackets and parenthesis is the markdownfile and adding the link in enclosed within the outermost parenthesis after the outermost closed brackets to the array list to return. Because this is involves multiple steps and a stack to keep track of the brackets/parenthesis pairs, this is likely going to be time consuming and more involved.*

- **Do you think there is a small (<10 lines) code change that will make your program work for snippet 3 and all related cases that have newlines in brackets and parentheses?**
- *I think this would be a rather quick fix becuase, based on the preview on VScode, if the ending parenthesis is more than one newline from the end of the text after the opening parenthesis, then it doesn't include the text in between the parenthesis as a link and instead only includes the substring that starts with `https://.` To do this, while the program parses through, it needs to check to see if there is text after the opening brackets/parenthesis on the same line as the opening, if so, then check to see if the closing parenthesis is at the end of the text on the same line, if not then don't include it as a link. If there is text in a new line after the opening parenthesis/brackets then check the current line for the closing parenthesis/brackts and the start of the very next line and a separate method can be created to search for the substring `https://` and include all attached text not involving a space as a link.*
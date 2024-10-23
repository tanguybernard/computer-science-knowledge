# Course


## Kata Java POO

Video Store Kata

https://codingdojo.org/kata/movie-rental/

https://martinfowler.com/articles/refactoring-video-store-js/

https://gitlab.com/azae/craft/movie-rental

Solution

https://elearning.industriallogic.com/gh/submit?Action=PageAction&album=kata&path=kata/videoStore/solution&devLanguage=Java

Solution

https://gitlab.ippon.fr/twitch/live-coding-fr/-/tree/master/movie-rental

On a du polymorphisme on peut avoir un HtmlRenderer

```java
public class ConsoleRenderer implements Renderer {

  @Override
  public String header(String name) {
    return "Rental Record for " + name + "\n";
  }

  @Override
  public String movie(Rental rental, double amount) {
    return "\t" + rental.getMovie().getTitle() + "\t" + String.valueOf(amount) + "\n";
  }

  @Override
  public String footer(double totalAmount, int frequentRenterPoints) {
    return new StringBuilder()
      .append("Amount owed is ")
      .append(totalAmount)
      .append("\n")
      .append("You earned ")
      .append(frequentRenterPoints)
      .append(" frequent renter points")
      .toString();
  }
}

```


## Kata Stream

Employee Report

https://blog.ippon.fr/2021/04/12/mon-catalogue-de-katas/

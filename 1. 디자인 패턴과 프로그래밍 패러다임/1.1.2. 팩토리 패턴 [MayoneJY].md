## 🔹 팩토리 패턴이란?

객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴입니다.

## 🔹 팩토리 패턴을 사용하는 이유는?

- 객체 생성 로직을 팩토리 클래스 내부에 숨겨, 클라이언트 코드가 구체적인 객체 생성 과정에 직접적으로 의존하는 것을 방지합니다.
- 새로운 객체 타입을 추가하거나 기존 객체 타입을 변경할 때, 클라이언트 코드 수정 없이 팩토리 클래스만 변경할 수 있습니다.

## 🔹단점은?

- 각 객체 유형에 대해 별도의 구현 클래스와 팩토리 로직이 필요하기 때문에 클래스 수가 급격히 늘어납니다. 유지 보수가 어려워질 수 있고, 파일 트리 구조가 복잡해질 수 있습니다.
- 객체 생성 로직이 추상화 되어 `new` 키워드를 직접 사용하는 코드가 사라져 직관적으로 파악하기 어려워집니다.
- 팩토리 내부에서 `switch` , `if-else` 로 타입을 분기하면 새로운 타입 추가 시마다 팩토리를 수정해야 합니다.

## 🔹 팩토리 패턴 사용 방법

```java
public interface Parser {
    void parse(String input);
}
```

```java
public class JsonParser implements Parser {
    @Override
    public void parse(String input) {
        System.out.println("Parsing JSON: " + input);
    }
}
```

```java
public class XmlParser implements Parser {
    @Override
    public void parse(String input) {
        System.out.println("Parsing XML: " + input);
    }
}
```

```java
public class ParserFactory {
    public static Parser createParser(String type) {
        if (type == null) {
            throw new IllegalArgumentException("type must not be null");
        }

        switch (type.toLowerCase()) {
            case "json":
                return new JsonParser();
            case "xml":
                return new XmlParser();
            default:
                throw new IllegalArgumentException("Unknown parser type: " + type);
        }
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        Parser parser = ParserFactory.createParser("json");
        parser.parse("{ \"key\": \"value\" }");
    }
}
```

## 🔹 요약

> 팩토리 패턴은 객체 생성을 캡슐화하는 데는 탁월하지만, 클래스 구조의 복잡성 증가, 디버깅 어려움 등의 부작용도 있으므로 상황에 맞게 신중하게 사용하는 것을 권장합니다.
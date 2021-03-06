# Stack
- 가장 마지막에 들어간 데이터가 가장 먼저 나오는 Last-In, First-Out (LIFO) 형식의 자료구조
- 항상 마지막에 값을 저장하고 꺼내기 때문에 성능은 무조건 O(1) 이다.

## 언제 쓸까?
- 컴퓨터에서 CPU가 작업을 진행할때 메모리 주소들을 스택에 넣고 빼고 하면서 작동한다.
- 프로그래밍 언어에서 함수 혹은 메소드가 호출될 때도 차근차근 스택에 쌓인다.
- 수식의 괄호를 검사할 때 사용 가능하다.
- 역순의 문자열을 만들 때 사용 가능하다.
- 기타 등등 많이 있다.

## 스택의 연산
### PUSH
- 배열의 가장 마지막 위치에 데이터를 삽입 한다.
- 만약 배열이 가득 찼다면 Overflow가 발생한다.
- 예제

스택의 길이가 5라고 가정할 경우

```
stack.push(10)
```

스택의 데이터: `[10]`

```
stack.push(90)
```

스택의 데이터: `[10, 90]`

```
stack.push(6)
```

스택의 데이터: `[10, 90, 6]`

```
stack.push(2)
```

스택의 데이터: `[10, 90, 6, 2]`

```
stack.push(57)
```

스택의 데이터: `[10, 90, 6, 2, 57]`

```
stack.push(100)
```

스택의 데이터: `[10, 90, 6, 2, 57]`, Overflow 발생!!

### POP
- 배열의 가장 마지막 위치에서 데이터를 추출 한다.
- 만약 배열이 비어있다면 Underflow가 발생한다.
- 예제

위에서 저장된 스택의 데이터로 POP 연산을 수행

```
stack.pop() // 57 리턴
```

스택의 데이터: `[10, 90, 6, 2]`

```
stack.pop() // 2 리턴
```

스택의 데이터: `[10, 90, 6]`

```
stack.pop() // 6 리턴
```

스택의 데이터: `[10, 90]`

```
stack.pop() // 90 리턴
```

스택의 데이터: `[10]`

```
stack.pop() // 10 리턴
```

스택의 데이터: `[]`

```
stack.pop()
```

스택의 데이터: Underflow 발생!!

### PEEK
- 배열의 가장 마지막 데이터를 조회한다.
- 이때 POP 연산과 다르게 마지막 위치의 데이터가 사라지지는 않는다.
- 예제

스택의 데이터가 `[10, 90, 6]` 일 경우

```
stack.peek()  // 6 리턴
```

```
stack.peek()  // 6 리턴
```

```
stack.peek()  // 6 리턴
```

```
stack.peek()  // 6 리턴
```

... 계속 가능

## 구현
```java
import java.util.ArrayList;
import java.util.List;

public class Stack<T> {
  private List<T> stack = new ArrayList<>();
  private int position = 0;
  private int max;

  public Stack(int max) {
    this.max = max;
  }

  public T pop() throws StackUnderFlow {
    if (isEmpty()) {
      throw new StackUnderFlow();
    } else {
      return stack.remove(--position);
    }
  }

  public void push(T t) throws StackOverFlow {
    if (isFull()) {
      throw new StackOverFlow();
    } else {
      stack.add(t);
      position++;
    }
  }

  public T peek() throws StackUnderFlow {
    if (isEmpty()) {
      throw new StackUnderFlow();
    }
    return stack.get(--position);
  }

  private boolean isEmpty() {
    return stack.isEmpty();
  }

  private boolean isFull() {
    return stack.size() == max;
  }
}
```

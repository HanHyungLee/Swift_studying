## Deinitialization
- init키워드와 유사한 deinit 키워드를 사용한다.
- 클래스에서만 사용 가능하다.

### 1. 사용방법
- 괄호와 파라미터를 가지지 않는다.
```
deinit {
    // perform the deinitialization
}
```

### 2. 동작방식
- 슈퍼클래스의 deinit은 서브클래스로 상속되고, 서브클래스의 deinit이 호출된 후 자동적으로 호출된다. (슈퍼클래스 deinit을 호출하면 에러가 난다.)
- deinitialization은 인스턴스 해제 전에 마지막으로 호출된다.
- deinit이 호출되면 해당 instance가 메모리에서 해제된다.

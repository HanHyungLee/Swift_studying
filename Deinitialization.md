## Deinitialization
- deinit 키워드를 사용한다.
- 클래스에서만 사용 가능하다.

### 1. 사용방법
```
deinit {
    // perform the deinitialization
}
```

### 2. 메모리 해제
- deinitialization은 인스턴스 해제 전에 마지막으로 호출된다.
- 슈퍼클래스의 deinit은 서브클래스로 상속이 가능하며, 서브클래스의 deinit이 호출된 후 자동적으로 호출된다.
- 클래스변수에 nil을 넣으면 메모리에서 해제가 되고, deinit이 호출된다.
- 

# 인자의 값으로 NULL을 절대 허용하지 마세요.



- Null을 사용하는 것은 객체에게 이야기 하는 대신 이 객체를 피하고 무시하는 것
- 객체를 존중한다면

```Java
if (mask.empty()) {
	// 모든 파일을 찾는다.
} else {
	// 마스크를 사용해서 파일을 찾는다.
}
```



더 개선한 코드

```Java
public Iterable<File> find(Mask mask) {
  Collection<File> files = new LinkedList<>();
  for (File file: allFiles) {
    if (mask.matches(file)) {
      files.add(file);
    }
  }
  return files;
}
```



- mask 객체를 존중했다면 조건의 존재 여부를 스스로 결정하게 했을 것



- Null대신

```Java
interface Mask {
	boolean matches(File file)
}
```



```Java
Class AnyFile implements Mask {
	@Override
	boolean matches(File file) {
		return true;
	}
}
```



- 중요하지 않은 NULL 확인 로직으로 코드를 오염시켜서는 안됩니다.



# 느낀점

- Null을 다루는 방법 중 하나인 Optional이 나왔지만 이것을 이용해도 Null을 체크하는 것 만큼이나 부수적인 코드들이 많이 생기는 것 같다.
- Null에 대해 조금 더 고민해 봐야겠다.


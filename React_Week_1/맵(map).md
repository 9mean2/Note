``` JSX
const moveToDone = (id) => {

const deleteTodo = todoList.filter((_, i) => todoList[i].id !== id);

const newDone = todoList.filter((_, i) => todoList[i].id === id);

setTodoList(deleteTodo);

setTodoDoneList([...todoDoneList, ...newDone]);

};
```
스프레드 문법으로 배열을 빼서 들어옴 새로운 객체 
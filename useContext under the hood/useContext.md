# useContext under the hood

اولا يجب ان نعرف ما هيا ال useContext : هي عبارة عن react hook و هي جزء من react `API` تسمح لنا بالاشتراك في ال context و توفر لنا الطريقة لكي نقوم بمشاركة البيانات في ال components tree بدون استخدام `props` بطريقة يدويه او استخدام nesting components كما في المثال اسفل : 


- with introducing nesting: 
```jsx
<MyContext.Consumer>
  {contextValue => (
    <AnotherContext.Consumer>
      {anotherContextValue => (
        <NestedComponent contextValue={contextValue} anotherContextValue={anotherContextValue} />
      )}
    </AnotherContext.Consumer>
  )}
</MyContext.Consumer>
 ```

و لتجنب هذا ال nesting نستعمل `useContext` لجلب البيانات كما في المثال اسفل: 
- without introducing nesting: 
```jsx
const MyComponent = () => {
  const contextValue = useContext(MyContext);
  const anotherContextValue = useContext(AnotherContext);

  return <NestedComponent contextValue={contextValue} anotherContextValue={anotherContextValue} />;
};
```


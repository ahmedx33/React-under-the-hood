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

# حسنا نأتي الان لكيفية عمل ال useContext بطريقة مبسطة

- عندما نستخدم `MyContext.Provider` لنقوم بعمل wrap على components tree حين اذ تقوم بعمل شي يسمى `React Subscription` في كل مره القيمة تتغير وهذا ال `React Subscription` هو بشكل اساسي الطريقة للكونات او components للاشتراك في التغيرات التي في هذا ال context

- عندما نستخدم  `useContext(MyContext)` في ال component تقوم ريأكت بالنظر لأقرب `MyContext.Provider` في ال components tree وتقوم بالاشتراك في التغيرات الخاصه به

- عندما تتغير قيمة ال context  ( بسبب التغيرات في ` value prop` لل `MyContext.Provider` ) تقوم react بعمل re-render لجميع ال components `المشتركة` في هذا ال context

- القيمة المرجعه او `returned value ` بواسطة `useContext` هي دائمًا قيمة ال context الأحدث

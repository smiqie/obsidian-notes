# Scope - область видимости

1. глобальная (global scope)
   ```js
   const num = 10;
   ```
2. локальная (local scope)
   ```js
   {
	   const num2 = 20;
   }
   ```
- локлаьный скоп - видит глоблаьный. local scope образется внутри скобок (`{}`)? 
  ```js
  const num1 = 10; // global
  
  { // local
	  num2 = num1;
  }
  
  function showScopeExample(){ // local scope
      const num0 = 10;
	  return num1 + num0;
  }
  ```
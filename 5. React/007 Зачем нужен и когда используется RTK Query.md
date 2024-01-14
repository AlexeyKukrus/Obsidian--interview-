**ОТВЕТ
	RTK Query - это библиотека Redux Toolkit, предназначенная для работы с API и выполнения любых CRUD-операций

```JSX
//goodsApi.js
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react'

export const goodsApi = createApi({
	reducerPath: 'goodsApi',
	baseQuery: fetchBaseQuery({baseUrl: 'http://localhost:3001/'})
	endpoints: (build) => ({
		getGoods: build.query({
			query: () => `goods`,
		})
	})
});

export const { useGetGoodsQuery } = goodsApi;
```
В этом коде создается экземпляр API с помощью функции createApi из @reduxjs/toolkit/query/react. Этот экземпляр API называется goodsApi.

Свойства, которые передаются в функцию createApi, включают:

- reducerPath: это путь к редьюсеру, в котором будет храниться состояние, связанное с этим API. В данном случае он называется 'goodsApi'.
- baseQuery: это базовый запрос, который будет использоваться для выполнения запросов к серверу. В данном случае используется fetchBaseQuery, который создает базовый запрос с помощью функции fetch из браузера и имеет базовый URL 'http://localhost:3001/'. Вы можете настроить этот URL в соответствии с URL вашего сервера.

Свойство endpoints - это функция, которая принимает build объект, и позволяет определить конечные точки для вашего API. Здесь определен одно конечное точка getGoods, который использует метод build.query. Этот метод определяет конечную точку, которую можно вызывать при необходимости. В данном случае конечная точка getGoods не принимает никаких параметров и возвращает данные с именем goods.

В конце кода экспортируются хуки, сгенерированные для использования с goodsApi. В данном случае экспортируется только useGetGoodsQuery, который может быть использован для выполнения запроса getGoods и получения данных.

Этот код описывает настройку и использование API для получения товаров с вашего сервера.

```JSX
//store.js
import { configureStore } from @reduxjs/toolkit;
import { goodsApi } from './goodsApi'

export  const store = configureStore({
	reducer: {
		[goodsApi.reducerPath] : goodsApi.reducer,
	},
	middleware: (getDefaultMiddleware) => getDefaultMiddleware().concat(goodsApi.middleware)
})
```
Здесь мы создаем Redux-хранилище (store) с помощью функции configureStore из @reduxjs/toolkit. Конфигурация хранилища включает следующие свойства:

- reducer: это объект, содержащий редьюсеры, которые будут управлять состоянием в хранилище. В данном случае, в качестве ключа используется goodsApi.reducerPath, где goodsApi.reducerPath - это путь к редьюсеру, содержащему состояние, связанное с goodsApi. Значением ключа является редьюсер goodsApi.reducer.

- middleware: это функция, которая позволяет добавить дополнительные middleware в хранилище. В данном случае используется getDefaultMiddleware для получения массива middleware по умолчанию, а затем с помощью метода concat добавляется middleware связанное с goodsApi. goodsApi.middleware представляет собой middleware, предоставляемое RTK Query, которое управляет отправкой запросов и обновлением кэша данных.

Наконец, экспортируется созданное хранилище из store.js.

Этот код настраивает Redux-хранилище, добавляя редьюсер и middleware, связанные с API для получения данных о товарах.

```JSX
//index.js
import React from 'react';
import ReactDOM from 'react-dom';
import { Provider } from 'react-redux'
import App from './App';
import { store } from './store'

ReactDOM.render(
	<Provider store={store}>
		<App />
	</Provider>
	document.getElementById('root)
)
```
Передаем store в приложение, с помощью Provider

```JSX
//app.js
import { useGetGoodsQuery } from './redux';

function App() {
	const {data = [], isLoading} = useGetGoodsQuery();
	if (isLoading) return <h1>LOADING...</h1>
	return(
		<div className='App'>
			{data.map(item => (
				<li key={item.id}>
					{item.name}
				</li>
			))}
		</div>
	)
}

export default App
```

Рассмотрим описанный код выше: 
- Сначала мы просто импортировали хук _useGetGoodsQuery
- При вызове хука useGetGoodsQueryбудет автоматически производиться вызов к API для получения всех предметов. Хук в свою очередь возвращает не только вышеуказанные значения, но и также ряд других полезных, таких как isFetching,  isError и другие. 

![](https://habrastorage.org/r/w1560/getpro/habr/upload_files/682/e4c/1cc/682e4c1cc3c01fc1fbe1421ec8a96405.png)

1. Теперь не приходится создавать `action creators` для каждого запроса 
2. Нет нужды создавать множество `reducers` 
3. Обработка состояний запросов (isFetching, isError и др.) теперь производится автоматически 
4. В React компонентах не нужно вызывать метод `dispatch` или использовать `селекторы` для взаимодействия со `store`  

В результате количество написанного кода становится меньше, а его восприятие заметно улучшилось.